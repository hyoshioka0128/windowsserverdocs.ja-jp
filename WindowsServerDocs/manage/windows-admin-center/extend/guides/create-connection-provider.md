---
title: ソリューション拡張機能の接続プロバイダーを作成する
description: ソリューション拡張機能の開発 Windows 管理センター SDK (Project ホノルル)-接続プロバイダーを作成する
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 06/06/2019
ms.localizationpriority: medium
ms.openlocfilehash: ec11b8a6b9129348ec2405548c21fa9d6ec5deff
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87952687"
---
# <a name="create-a-connection-provider-for-a-solution-extension"></a>ソリューション拡張機能の接続プロバイダーを作成する

>適用先:Windows Admin Center、Windows Admin Center Preview

接続プロバイダーは、Windows 管理センターが接続可能なオブジェクト (ターゲット) を定義して通信する際に重要な役割を果たします。 接続プロバイダーは、主に接続が確立されている間にアクションを実行します。たとえば、ターゲットがオンラインで使用可能であることを確認し、接続しているユーザーがターゲットにアクセスするためのアクセス許可を持っていることを確認します。

既定では、Windows 管理センターには次の接続プロバイダーが付属しています。

* サーバー
* Windows クライアント
* フェールオーバー クラスター
* HCI クラスター

独自のカスタム接続プロバイダーを作成するには、次の手順を実行します。

* 接続プロバイダーの詳細をに追加する```manifest.json```
* 接続状態プロバイダーの定義
* アプリケーション層に接続プロバイダーを実装する

## <a name="add-connection-provider-details-to-manifestjson"></a>接続プロバイダーの詳細を manifest.jsに追加する

ここでは、プロジェクトのファイルで接続プロバイダーを定義するために必要な知識について説明し ```manifest.json``` ます。

### <a name="create-entry-in-manifestjson"></a>manifest.jsでエントリを作成する

この ```manifest.json``` ファイルは、\ src フォルダーにあり、特にプロジェクト内のエントリポイントの定義を含みます。 エントリポイントの種類には、ツール、ソリューション、および接続プロバイダーが含まれます。 接続プロバイダーを定義します。

manifest.jsの接続プロバイダーエントリの例を次に示します。

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

"ConnnectionProvider" 型のエントリポイントは、構成されている項目が、接続状態を検証するためにソリューションによって使用されるプロバイダーであることを Windows 管理センターシェルに示します。 接続プロバイダーのエントリポイントには、以下に定義されているいくつかの重要なプロパティが含まれています。

| プロパティ | 説明 |
| -------- | ----------- |
| entryPointType | このプロパティは必須です。 有効な値には、"tool"、"solution"、および "connectionProvider" の3つがあります。 |
| name | ソリューションのスコープ内で接続プロバイダーを識別します。 この値は、完全な Windows 管理センターインスタンス内で一意である必要があります (ソリューションだけではありません)。 |
| path | "接続の追加" UI がソリューションによって構成される場合の URL パスを表します。 この値は、app.config ファイルで構成されているルートにマップする必要があります。 接続 rootNavigationBehavior を使用するようにソリューションのエントリポイントが構成されている場合、このルートは、シェルが接続の追加 UI を表示するために使用するモジュールを読み込みます。 詳細については、rootNavigationBehavior に関するセクションを参照してください。 |
| displayName | ここに入力した値は、ユーザーがソリューションの [接続] ページを読み込んだときに、黒い Windows 管理センターバーの下に、シェルの右側に表示されます。 |
| アイコン | ソリューションを表すために [ソリューション] ドロップダウンメニューで使用されるアイコンを表します。 |
| description | エントリポイントの簡単な説明を入力します。 |
| connectionType | プロバイダーが読み込む接続の種類を表します。 ここに入力した値は、ソリューションのエントリポイントでも使用され、ソリューションでそれらの接続を読み込むことができることを指定します。 ここに入力した値はツールのエントリポイントでも使用され、ツールがこの型と互換性があることを示します。 ここに入力した値は、アプリケーション層の実装手順で、[追加] ウィンドウで RPC 呼び出しに送信される接続オブジェクトでも使用されます。 |
| connectionTypeName | Connections テーブルで、接続プロバイダーを使用する接続を表すために使用されます。 これは、型の複数形の名前であることが想定されています。 |
| connectionTypeUrlName | Windows 管理センターがインスタンスに接続した後に、読み込まれたソリューションを表す URL を作成するために使用されます。 このエントリは、接続後、ターゲットの前に使用されます。 この例では、"connectionexample" という値が URL に表示されます。`http://localhost:6516/solutionexample/connections/connectionexample/con-fake1.corp.contoso.com` |
| connectionTypeDefaultSolution | 接続プロバイダーによって読み込まれる既定のコンポーネントを表します。 この値は、次の組み合わせで指定します。 <br>[a] マニフェストの最上位で定義されている拡張機能パッケージの名前。 <br>[b] 感嘆符 (!); <br>[c] ソリューションエントリポイント名。    <br>"MySample" という名前のプロジェクトと、"example" という名前のソリューションエントリポイントの場合、この値は "msft........ 拡張子! example" になります。 |
| connectionTypeDefaultTool | 接続が成功したときに読み込む必要がある既定のツールを表します。 このプロパティ値は、connectionTypeDefaultSolution に似た2つの部分で構成されています。 この値は、次の組み合わせで指定します。 <br>[a] マニフェストの最上位で定義されている拡張機能パッケージの名前。 <br>[b] 感嘆符 (!); <br>[c] 最初に読み込む必要があるツールのエントリポイントの名前。 <br>"Msft. solutionExample-extension" という名前のプロジェクトと、"example" という名前のソリューションエントリポイントの場合、この値は "msft................. 拡張子! example" になります。 |
| connectionStatusProvider | 「接続状態プロバイダーの定義」セクションを参照してください。 |

## <a name="define-connection-status-provider"></a>接続状態プロバイダーの定義

接続状態プロバイダーは、ターゲットがオンラインで使用可能であることを検証するメカニズムであり、接続しているユーザーがターゲットにアクセスするためのアクセス許可を持っていることも確認します。 現在、PowerShell と RelativeGatewayUrl の2種類の接続状態プロバイダーがあります。

*   <strong>Powershell 接続状態プロバイダー</strong> -ターゲットがオンラインであり、powershell スクリプトでアクセスできるかどうかを判断します。 結果は、以下に定義されている1つのプロパティ "status" を持つオブジェクトで返される必要があります。
*   <strong>RelativeGatewayUrl 接続状態プロバイダー</strong> -ターゲットがオンラインであり、rest 呼び出しでアクセスできるかどうかを判断します。 結果は、以下に定義されている1つのプロパティ "status" を持つオブジェクトで返される必要があります。

### <a name="define-status"></a>状態の定義

接続状態プロバイダーは、 ```status``` 次の形式に準拠する1つのプロパティを持つオブジェクトを返す必要があります。

``` json
{
    status: {
        label: string;
        type: int;
        details: string;
    }
}
```

状態のプロパティ:

* <strong>Label</strong> -ステータスの戻り値の型を説明するラベル。 [ラベル] の値は、実行時にマップできます。 実行時のマッピング値については、以下のエントリを参照してください。

* <strong>Type</strong> -状態の戻り値の型。 型には、次の列挙値があります。 値が2以上の場合、プラットフォームは接続されているオブジェクトに移動せず、エラーが UI に表示されます。

   な

  | 値 | 説明 |
  | ----- | ----------- |
  | 0 | オンライン |
  | 1 | 警告 |
  | 2 | 権限がありません |
  | 3 | エラー |
  | 4 | 致命的 |
  | 5 | Unknown |

* <strong>詳細</strong>-ステータスの戻り値の型を説明する追加の詳細。

### <a name="powershell-connection-status-provider-script"></a>PowerShell 接続状態プロバイダースクリプト

接続状態プロバイダーの PowerShell スクリプトは、ターゲットがオンラインであり、PowerShell スクリプトでアクセスできるかどうかを判断します。 結果は、1つのプロパティ "status" を持つオブジェクトで返される必要があります。 スクリプトの例を次に示します。

Powershell スクリプトの例:

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

### <a name="define-relativegatewayurl-connection-status-provider-method"></a>RelativeGatewayUrl 接続状態プロバイダーメソッドの定義

接続状態プロバイダーメソッドは、 ```RelativeGatewayUrl``` REST API を呼び出して、ターゲットがオンラインでアクセス可能かどうかを判断します。 結果は、1つのプロパティ "status" を持つオブジェクトで返される必要があります。 RelativeGatewayUrl の manifest.jsの接続プロバイダーエントリの例を次に示します。

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

* "relativeGatewayUrl" は、ゲートウェイの URL から接続の状態を取得する場所を指定します。 この URI は、/apiからの相対値です。 URL に $connectionName が見つかった場合は、接続の名前に置き換えられます。
* すべての relativeGatewayUrl プロパティをホストゲートウェイに対して実行する必要があります。これは、ゲートウェイ拡張機能を作成することによって実現できます。

### <a name="map-values-in-runtime"></a>実行時のマップ値

Status return オブジェクトの label および details の値は、プロバイダーの "defaultValueMap" プロパティにキーと値を含めることで、チューニング時に書式設定できます。

たとえば、次の値を追加した場合、ラベルまたは詳細の値として "defaultConnection_test" が表示されるたびに、Windows 管理センターは自動的にキーを構成済みのリソース文字列値に置き換えます。

``` json
    "defaultConnection_test": "resources:strings:addServer_status_defaultConnection_label"
```

## <a name="implement-connection-provider-in-application-layer"></a>アプリケーション層に接続プロバイダーを実装する

次に、OnInit を実装する TypeScript クラスを作成して、アプリケーション層に接続プロバイダーを実装します。 クラスには、次の関数があります。

| 機能 | 説明 |
| -------- | ----------- |
| コンストラクター (プライベート appContextService: AppContextService、プライベートルート: ActivatedRoute) |  |
| パブリック ngOnInit () |  |
| パブリック onSubmit () | 接続の追加試行時にシェルを更新するロジックが含まれています |
| パブリック onCancel () | 接続の追加試行が取り消されたときにシェルを更新するロジックが含まれています |

### <a name="define-onsubmit"></a>OnSubmit の定義

```onSubmit```アプリケーションコンテキストに対して RPC コールバックを発行して、"接続の追加" をシェルに通知します。 基本的な呼び出しでは、次のように "updateData" を使用します。

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

結果は、次の構造に準拠するオブジェクトの配列である接続プロパティになります。

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

### <a name="define-oncancel"></a>OnCancel の定義

```onCancel```空の接続配列を渡すことによって、"接続の追加" をキャンセルします。

``` ts
this.appContextService.rpc.updateData(EnvironmentModule.nameOfShell, '##', <RpcUpdateData>{ results: { connections: [] } });
```

## <a name="connection-provider-example"></a>接続プロバイダーの例

接続プロバイダーを実装するための完全な TypeScript クラスを次に示します。 "ConnectionType" 文字列は、の manifest.jsの接続プロバイダーで定義されている "connectionType" と一致します。

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
