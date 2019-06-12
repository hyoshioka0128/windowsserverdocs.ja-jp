---
title: ソリューションの拡張機能の接続プロバイダーを作成します。
description: ソリューションの拡張機能 Windows Admin Center SDK (プロジェクト ホノルル) の開発 - 接続プロバイダーを作成します。
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 06/06/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: b79e832ee45990d18baf4c211ab68b907134ceb7
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66811839"
---
# <a name="create-a-connection-provider-for-a-solution-extension"></a>ソリューションの拡張機能の接続プロバイダーを作成します。

>適用先:Windows Admin Center、Windows Admin Center プレビュー

接続プロバイダーは、Windows Admin Center の定義および接続可能なオブジェクト、またはターゲットとの通信で重要な役割を果たします。 主に、接続プロバイダーは、オンラインで使用できますが、ターゲットがあることを確認しても、接続するユーザーがターゲットにアクセスする権限を持っていることを確認など、接続が確立されているときにアクションを実行します。

既定では、Windows Admin Center は、次の接続プロバイダーが付属しています。

* Server
* Windows クライアント
* フェールオーバー クラスター
* HCI クラスター

独自のカスタム接続プロバイダーを作成するには、次の手順を実行します。

* 接続プロバイダーの詳細を追加します。 ```manifest.json```
* 接続の状態プロバイダーを定義します。
* アプリケーション層での接続プロバイダーを実装します。

## <a name="add-connection-provider-details-to-manifestjson"></a>接続プロバイダーの詳細を manifest.json に追加します。

プロジェクトの接続プロバイダーを定義するために知っておくべきいきますので```manifest.json```ファイル。

### <a name="create-entry-in-manifestjson"></a>Manifest.json にエントリを作成します。

```manifest.json```ファイル \src フォルダーにあるし、その他のものをプロジェクトのエントリ ポイントの定義が含まれます。 エントリ ポイントの種類には、ツール、ソリューション、および接続プロバイダーが含まれます。 私たちは接続プロバイダーを定義します。

Manifest.json で接続プロバイダーのエントリのサンプルを次に示します。

``` json
    {
      "entryPointType": "connectionProvider",
      "name": "addServer",
      "path": "/add",
      "displayName": "resources:strings:addServer_displayName",
      "icon": "sme-icon:icon-win-server",
      "description": "resources:strings:description",
      "connectionType": "msft.sme.connection-type.server",
      "connectionTypeName": "resources:strings:addServer_connectionTypeName",
      "connectionTypeUrlName": "server",
      "connectionTypeDefaultSolution": "msft.sme.server-manager!servers",
      "connectionTypeDefaultTool": "msft.sme.server-manager!overview",
      "connectionStatusProvider": {
        "powerShell": {
          "script": "## Get-My-Status ##\nfunction Get-Status()\n{\n# A function like this would be where logic would exist to identify if a node is connectable.\n$status = @{label = $null; type = 0; details = $null; }\n$caption = \"MyConstCaption\"\n$productType = \"MyProductType\"\n# A result object needs to conform to the following object structure to be interpreted properly by the Windows Admin Center shell.\n$result = @{ status = $status; caption = $caption; productType = $productType; version = $version }\n# DO FANCY LOGIC #\n# Once the logic is complete, the following fields need to be populated:\n$status.label = \"Display Thing\"\n$status.type = 0 # This value needs to conform to the LiveConnectionStatusType enum. >= 3 represents a failure.\n$status.details = \"success stuff\"\nreturn $result}\nGet-Status"
        },
        "displayValueMap": {
          "wmfMissing-label": "resources:strings:addServer_status_wmfMissing_label",
          "wmfMissing-details": "resources:strings:addServer_status_wmfMissing_details",
          "unsupported-label": "resources:strings:addServer_status_unsupported_label",
          "unsupported-details": "resources:strings:addServer_status_unsupported_details"
        }
      }
    },
```

"ConnnectionProvider"の種類のエントリ ポイントは Windows Admin Center シェルに構成されている項目は、接続状態を検証するソリューションで使用されるプロバイダーであることを示します。 接続プロバイダーのエントリ ポイントには、さまざまな定義は以下の重要なプロパティが含まれています。

| プロパティ | 説明 |
| -------- | ----------- |
| entryPointType | このプロパティは必須です。 次の 3 つの有効な値:「ツール」、「ソリューション」と「とき」。 | 
| name | ソリューションのスコープ内で、接続プロバイダーを識別します。 この値は、完全な Windows Admin Center インスタンス (ソリューションだけでなく) 内で一意である必要があります。 |
| path | ソリューションで構成する場合は、「接続の追加」、UI の URL パスを表します。 この値は、アプリ routing.module.ts ファイルで構成されているルートにマップする必要があります。 接続 rootNavigationBehavior を使用するソリューションのエントリ ポイントが構成されると、このルートは、接続の追加 UI を表示するシェルによって使用されるモジュールを読み込みます。 詳細については、セクションでは rootNavigationBehavior 上。 |
| displayName | ここに入力した値は、ユーザーには、ソリューションの接続 ページが読み込まれる、黒の Windows Admin Center バーの下のシェルの右側に表示されます。 |
| アイコン●あいこん○ | ソリューションのドロップダウン メニューで、ソリューションを表すために使用するアイコンを表します。 |
| description | エントリ ポイントの簡単な説明を入力します。 |
| connectionType | 読み込みは、プロバイダー接続の種類を表します。 ここに入力した値も指定するため、ソリューションのエントリ ポイントで、ソリューションがそれらの接続を読み込むことができます。 ここに入力した値は、ツールがこの型と互換性があるツールのエントリ ポイントの使用もします。 ここに入力したこの値は、RPC に送信される接続オブジェクトでは使用も、「追加ウィンドウの」アプリケーション レイヤーの実装の手順で呼び出します。 |
| connectionTypeName | 接続の表に、接続プロバイダーを使用する接続を表すために使用します。 これは型の複数形の名前を指定します。 |
| connectionTypeUrlName | URL の作成に使用され、Windows Admin Center がインスタンスに接続した後に読み込まれているソリューションを表します。 このエントリは、ターゲットの前に、接続後に使用されます。 この例では、"connectionexample"は、URL でこの値が表示されます。 `http://localhost:6516/solutionexample/connections/connectionexample/con-fake1.corp.contoso.com` |
| connectionTypeDefaultSolution | 接続プロバイダーによって読み込む必要のある既定のコンポーネントを表します。 この値は、組み合わせです。 <br>[a]; マニフェストの上部にある定義された拡張機能パッケージの名前 <br>[b] 感嘆符 (!)。 <br>[c]、ソリューションのエントリ ポイント名。    <br>「Msft.sme.mySample - 拡張子名」のプロジェクトと、ソリューションのエントリ ポイント名"example"では、この値になります"msft.sme.solutionExample 拡張機能です。 例"。 |
| connectionTypeDefaultTool | 既定の接続が成功すると読み込む必要のあるツールを表します。 このプロパティの値は、connectionTypeDefaultSolution のような 2 つの部分で構成されます。 この値は、組み合わせです。 <br>[a]; マニフェストの上部にある定義された拡張機能パッケージの名前 <br>[b] 感嘆符 (!)。 <br>[c] ツール エントリ ポイント名の最初に読み込む必要のあるツールです。 <br>「Msft.sme.solutionExample - 拡張子名」のプロジェクトと、ソリューションのエントリ ポイント名"example"では、この値になります"msft.sme.solutionExample 拡張機能です。 例"。 |
| connectionStatusProvider | 「接続の状態プロバイダーの定義」セクションを参照してください。 |

## <a name="define-connection-status-provider"></a>接続の状態プロバイダーを定義します。

接続の状態プロバイダーも接続しているユーザーがターゲットにアクセスする権限を持っていることを確認をオンラインで使用できますが、ターゲットを検証するメカニズムです。 現在は、接続状態プロバイダーの 2 つの種類があります。PowerShell、および RelativeGatewayUrl します。

*   <strong>PowerShell 接続の状態プロバイダー</strong> -ターゲットとは、オンラインおよび PowerShell スクリプトを使用してアクセスできるかどうかを決定します。 結果は、以下に定義された 1 つのプロパティ"status"を持つオブジェクトで返される必要があります。
*   <strong>RelativeGatewayUrl 接続状態プロバイダー</strong> -ターゲットとは、オンラインで、rest 呼び出しを使用してアクセスできるかどうかを決定します。 結果は、以下に定義された 1 つのプロパティ"status"を持つオブジェクトで返される必要があります。

### <a name="define-status"></a>状態を定義します。

接続の状態プロバイダーを 1 つのプロパティを持つオブジェクトを返す必要は```status```次の形式に準拠しました。

``` json
{
    status: {
        label: string;
        type: int;
        details: string;
    }
}
```

ステータスのプロパティ:

* <strong>ラベル</strong>- 状態の戻り値の型を記述するラベル。 ランタイムでラベルの値をマップすることに注意してください。 ランタイム内の値のマッピングの下のエントリを参照してください。

* <strong>型</strong>-状態の戻り型。 種類は、次の列挙値があります。 任意の値 2 またはそれ以上、プラットフォームは、接続されているオブジェクトに移動しないと、UI でエラーが表示されます。

   種類:

  | Value | 説明 |
  | ----- | ----------- |
  | 0 | オンライン |
  | 1 | 警告 |
  | 2 | 権限がありません |
  | 3 | エラー |
  | 4 | 致命的です |
  | 5 | Unknown |

* <strong>詳細</strong>- 状態の戻り値の型を記述する追加の詳細。

### <a name="powershell-connection-status-provider-script"></a>接続の状態プロバイダーの PowerShell スクリプト

接続状態プロバイダーの PowerShell スクリプトは、ターゲットがオンラインと PowerShell スクリプトを使用してアクセスできるかどうかを判断します。 1 つの"status"プロパティを持つオブジェクトでは、結果を返す必要があります。 スクリプトの例は、以下に示します。

PowerShell スクリプトの例:

```PowerShell
## Get-My-Status ##

function Get-Status()
{
    # A function like this would be where logic would exist to identify if a node is connectable.
    $status = @{label = $null; type = 0; details = $null; }
    $caption = "MyConstCaption"
    $productType = "MyProductType"

    # A result object needs to conform to the following object structure to be interperated properly by the Windows Admin Center shell.
    $result = @{ status = $status; caption = $caption; productType = $productType; version = $version }

    # DO FANCY LOGIC #

    # Once the logic is complete, the following fields need to be populated:
    $status.label = "Display Thing"
    $status.type = 0 # This value needs to conform to the LiveConnectionStatusType enum. >= 3 represents a failure.
    $status.details = "success stuff"

    return $result
}

Get-Status
```

### <a name="define-relativegatewayurl-connection-status-provider-method"></a>RelativeGatewayUrl 接続状態プロバイダーのメソッドを定義します。

接続の状態プロバイダー```RelativeGatewayUrl```メソッド呼び出す rest API をターゲットがオンラインでアクセス可能かを判断します。 1 つの"status"プロパティを持つオブジェクトでは、結果を返す必要があります。 RelativeGatewayUrl の例では、manifest.json 接続プロバイダーのエントリは、以下に示します。

``` json
    {
      "entryPointType": "connectionProvider",
      "name": "addServer",
      "path": "/add/server",
      "displayName": "resources:strings:addServer_displayName",
      "icon": "sme-icon:icon-win-server",
      "description": "resources:strings:description",
      "connectionType": "msft.sme.connection-type.server",
      "connectionTypeName": "resources:strings:addServer_connectionTypeName",
      "connectionTypeUrlName": "server",
      "connectionTypeDefaultSolution": "msft.sme.server-manager!servers",
      "connectionTypeDefaultTool": "msft.sme.server-manager!overview",
      "connectionStatusProvider": {
        "relativeGatewayUrl": "<URL here post /api>",
        "displayValueMap": {
          "wmfMissing-label": "resources:strings:addServer_status_wmfMissing_label",
          "wmfMissing-details": "resources:strings:addServer_status_wmfMissing_details",
          "unsupported-label": "resources:strings:addServer_status_unsupported_label",
          "unsupported-details": "resources:strings:addServer_status_unsupported_details"
        }
      }
    },
```

RelativeGatewayUrl の使用に関する注意事項:

* "relativeGatewayUrl"では、ゲートウェイの URL からの接続状態を取得する場所を指定します。 この URI は/api からです。 $ConnectionName が URL で見つかった場合は、接続の名前に置き換えられます。
* RelativeGatewayUrl のすべてのプロパティは、ゲートウェイの拡張機能を作成して実現可能ホスト ゲートウェイに対して実行する必要があります。

### <a name="map-values-in-runtime"></a>実行時の値をマップします。

返されるオブジェクトの書式設定に状態で、ラベルと詳細値では、プロバイダーの"defaultValueMap"プロパティにキーと値を含めることで時間を調整します。

たとえば、いつでもその"defaultConnection_test"Windows Admin Center は自動的にラベルまたは詳細は、のいずれかの値としてやって来て、下の値を追加する場合は、構成されているリソースの文字列値でキーを置き換えます。

``` json
    "defaultConnection_test": "resources:strings:addServer_status_defaultConnection_label"
```

## <a name="implement-connection-provider-in-application-layer"></a>アプリケーション層での接続プロバイダーを実装します。

今すぐ OnInit を実装する TypeScript クラスを作成して、アプリケーション層で、接続プロバイダーを実装するためになります。 クラスには、次の機能があります。

| 関数 | 説明 |
| -------- | ----------- |
| constructor(private appContextService:AppContextService、プライベート ルート:ActivatedRoute) |  |
| public ngOnInit() |  |
| public onSubmit() | 追加の接続試行が行われたときに、シェルを更新するロジックが含まれています |
| public onCancel() | 追加の接続試行が取り消されたときに、シェルを更新するロジックが含まれています |

### <a name="define-onsubmit"></a>OnSubmit を定義します。

```onSubmit``` 問題、RPC は、「追加の接続」のシェルに通知するアプリのコンテキストにコールバックしています。 基本的な呼び出しでは、このような"updateData"を使用します。

``` ts
this.appContextService.rpc.updateData(
    EnvironmentModule.nameOfShell,
    '##',
    <RpcUpdateData>{
        results: {
            connections: connections,
            credentials: this.useCredentials ? this.creds : null
        }
    }
);
```

結果は、次の構造に準拠しているオブジェクトの配列である接続のプロパティです。

``` ts

/**
 * The connection attributes class.
 */
export interface ConnectionAttribute {

    /**
     * The id string of this attribute
     */
    id: string;

    /**
     * The value of the attribute. used for attributes that can have variable values such as Operating System
     */
    value?: string | number;
}

/**
 * The connection class.
 */
export interface Connection {

    /**
     * The id of the connection, this is unique per connection
     */
    id: string;

    /**
     * The type of connection
     */
    type: string;

    /**
     * The name of the connection, this is unique per connection type
     */
    name: string;

    /**
     * The property bag of the connection
     */
    properties?: ConnectionProperties;

    /**
     * The ids of attributes identified for this connection
     */
    attributes?: ConnectionAttribute[];

    /**
     * The tags the user(s) have assigned to this connection
     */
    tags?: string[];
}

/**
 * Defines connection type strings known by core
 * Be careful that these strings match what is defined by the manifest of @msft-sme/server-manager
 */
export const connectionTypeConstants = {
    server: 'msft.sme.connection-type.server',
    cluster: 'msft.sme.connection-type.cluster',
    hyperConvergedCluster: 'msft.sme.connection-type.hyper-converged-cluster',
    windowsClient: 'msft.sme.connection-type.windows-client',
    clusterNodesProperty: 'nodes'
};
```

### <a name="define-oncancel"></a>OnCancel を定義します。

```onCancel``` 接続が空の配列を渡すことによって、「接続の追加」の試行をキャンセルします。

``` ts
this.appContextService.rpc.updateData(EnvironmentModule.nameOfShell, '##', <RpcUpdateData>{ results: { connections: [] } });
```

## <a name="connection-provider-example"></a>接続プロバイダーの例

接続プロバイダーを実装するための完全な TypeScript クラスが未満です。 "ConnectionType"文字列が、"connectionType manifest.json で接続プロバイダーで定義されていると一致することに注意してください。

``` ts
import { Component, OnInit } from '@angular/core';
import { ActivatedRoute } from '@angular/router';
import { AppContextService } from '@msft-sme/shell/angular';
import { Connection, ConnectionUtility } from '@msft-sme/shell/core';
import { EnvironmentModule } from '@msft-sme/shell/dist/core/manifest/environment-modules';
import { RpcUpdateData } from '@msft-sme/shell/dist/core/rpc/rpc-base';
import { Strings } from '../../generated/strings';

@Component({
  selector: 'add-example',
  templateUrl: './add-example.component.html',
  styleUrls: ['./add-example.component.css']
})
export class AddExampleComponent implements OnInit {
  public newConnectionName: string;
  public strings = MsftSme.resourcesStrings<Strings>().SolutionExample;
  private connectionType = 'msft.sme.connection-type.example'; // This needs to match the connectionTypes value used in the manifest.json.
  
  constructor(private appContextService: AppContextService, private route: ActivatedRoute) {
    // TODO:
  }

  public ngOnInit() {
    // TODO
  }

  public onSubmit() {
    let connections: Connection[] = [];

    let connection = <Connection> {
      id: ConnectionUtility.createConnectionId(this.connectionType, this.newConnectionName),
      type: this.connectionType,
      name: this.newConnectionName
    };

    connections.push(connection);

    this.appContextService.rpc.updateData(
      EnvironmentModule.nameOfShell,
      '##',
      <RpcUpdateData> {
        results: {
          connections: connections,
          credentials: null
        }
      }
    );
  }

  public onCancel() {
    this.appContextService.rpc.updateData(
      EnvironmentModule.nameOfShell, '##', <RpcUpdateData>{ results: { connections: [] } });
  }
}

```
