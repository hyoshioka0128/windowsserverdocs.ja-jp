---
title: ソリューション拡張機能の接続プロバイダーを作成します。
description: Windows Admin Center SDK (Project Honolulu) のソリューション拡張機能の開発 - 接続プロバイダーを作成します。
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 883fba96fcb71cb1c6e8162c1564d66924c4e24d
ms.sourcegitcommit: be0144eb59daf3269bebea93cb1c467d67e2d2f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2018
ms.locfileid: "4081139"
---
# ソリューション拡張機能の接続プロバイダーを作成します。

>適用対象: Windows Admin Center、Windows Admin Center Preview

接続のプロバイダーは、Windows Admin Center の定義し、は、接続可能なオブジェクトまたはターゲットと通信で重要な役割を果たします。 主に、接続のプロバイダーは、オンラインで利用できる、ターゲットがあることを確認しも接続しているユーザーがターゲットにアクセスする権限を持っていることを確認など、接続が確立されているときにアクションを実行します。

既定では、Windows Admin Center は、次の接続プロバイダーが付属します。

* Server
* Windows クライアント
* フェールオーバー クラスター
* HCI クラスター

独自のカスタム接続プロバイダーを作成するには、次の手順に従います。

* 接続プロバイダーの詳細情報を追加します。 ```manifest.json```
* 接続状態のプロバイダーを定義します。
* アプリケーションのレイヤーで接続プロバイダーを実装します。

## Manifest.json に接続プロバイダーの詳細を追加します。

プロジェクトの接続のプロバイダーを定義するために知っておくべきについて説明しますので```manifest.json```ファイル。

### Manifest.json のエントリを作成します。

```manifest.json```ファイル \src フォルダーにあるし、特に、プロジェクトのエントリ ポイントの定義が含まれます。 エントリ ポイントの種類には、ツール、ソリューション、および接続プロバイダーが含まれます。 接続プロバイダーを定義しますがあります。

次に示します manifest.json で接続プロバイダー エントリの例。

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

"ConnnectionProvider"の種類のエントリ ポイントは、接続状態を検証するソリューションによって使用されるプロバイダーに構成されている項目が Windows Admin Center のシェルに示します。 接続プロバイダーのエントリ ポイントには、多数重要なプロパティを以下に定義にはが含まれています。

| プロパティ | 説明 |
| -------- | ----------- |
| entryPointType | これは、必要なプロパティです。 次の 3 つの有効な値:「ツール」、「ソリューション」および「とき」します。 | 
| name | ソリューションのスコープ内で接続プロバイダーを識別します。 この値は、完全な Windows Admin Center インスタンス (ソリューションだけでなく) 内で一意である必要があります。 |
| path | ソリューションで構成されている場合は、接続のため、"追加"UI、URL パスを表します。 この値は、アプリ routing.module.ts ファイルで構成されているルートにマップする必要があります。 接続 rootNavigationBehavior を使用するソリューションのエントリ ポイントを構成すると、このルート シェルによって追加接続 UI を表示するために使用するモジュールが読み込まれます。 利用可能なセクションについて詳しく rootNavigationBehavior します。 |
| displayName | ここで入力した値は、ユーザーがソリューションの接続] ページが読み込まれると、黒の Windows Admin Center バーの下のシェルの右側に表示されます。 |
| icon | ソリューションのドロップダウン メニューで、ソリューションを表すために使用するアイコンを表します。 |
| description | エントリ ポイントの簡単な説明を入力します。 |
| クエリ文字列 | プロバイダーが読み込まれます接続の種類を表します。 ここに入力した値は、ソリューションがそれらの接続を読み込むことができることを指定するソリューションのエントリ ポイントにも使用されます。 ここに入力した値は、ツールがこの種類と互換性のあることを示すツールのエントリ ポイントにも使用されます。 ここに入力したこの値は、RPC に送信される接続オブジェクトにも使用される「追加ウィンドウで」、アプリケーション レイヤー実装手順で呼び出します。 |
| connectionTypeName | 接続の表に、接続のプロバイダーを使用する接続を表すために使用します。 これは型の複数の名前を指定します。 |
| connectionTypeUrlName | Windows Admin Center は、インスタンスに接続した後、読み込まれたソリューションを表す URL の作成に使用します。 このエントリは、接続後、ターゲットの前に使用されます。 この例では"connectionexample"は、URL にこの値が表示されます。http://localhost:6516/solutionexample/connections/connectionexample/con-fake1.corp.contoso.com |
| connectionTypeDefaultSolution | 接続プロバイダーで読み込む必要のある既定のコンポーネントを表します。 この値の組み合わせ: なります; マニフェストの上部で定義されている拡張機能パッケージの名前[b] 感嘆符 (!)。[c] ソリューション エントリ ポイント名。    プロジェクト名拡張子を持つ"msft.sme.mySample-"、および名「例」で、ソリューションのエントリ ポイントは、この値になります"msft.sme.solutionExample 拡張! 例"します。 |
| connectionTypeDefaultTool | 成功した接続で読み込む必要のあるツールの既定値を表します。 このプロパティの値は、2 つの部分と同様、connectionTypeDefaultSolution に構成されています。 この値の組み合わせ: なります; マニフェストの上部で定義されている拡張機能パッケージの名前[b] 感嘆符 (!)。[c] ツール エントリ ポイント名の最初に読み込む必要のあるツールです。 プロジェクト名拡張子を持つ"msft.sme.solutionExample-"、および名「例」で、ソリューションのエントリ ポイントは、この値になります"msft.sme.solutionExample 拡張! 例"します。 |
| connectionStatusProvider | 「定義の接続状態プロバイダー」のセクションを参照してください。 |

## 接続状態のプロバイダーを定義します。

接続状態のプロバイダーは、ターゲットがオンラインで利用できる、検証するメカニズムも接続しているユーザーがターゲットにアクセスする権限を持っていることを確認します。 現在は、接続状態のプロバイダーの 2 つの種類: PowerShell、および RelativeGatewayUrl します。

*   PowerShell の接続状態のプロバイダー
    *   ターゲットがオンラインと PowerShell スクリプトを使ってアクセスできるかを判断します。 結果は、以下に定義されている 1 つのプロパティ"status"を持つオブジェクトで返される必要があります。
*   RelativeGatewayUrl 接続状態のプロバイダー
    *   ターゲットがオンラインと rest 呼び出しを使ってアクセスできるかを判断します。 結果は、以下に定義されている 1 つのプロパティ"status"を持つオブジェクトで返される必要があります。

### 状態を定義します。

接続状態のプロバイダーを 1 つのプロパティを持つオブジェクトを返す必要は```status```次の形式に準拠しています。

``` json
{
    status: {
        label: string;
        type: int;
        details: string;
    }
}
```

ステータスのプロパティ

* Label
    * ステータスの戻り値の型を表すラベル。 実行時にマップできるラベルの値に注意してください。 ランタイムでマッピング値の下のエントリを参照してください。

* 種類
    * ステータス戻り値の型です。 型では、次の列挙値があります。 任意の値を 2 以上、プラットフォームは、接続されているオブジェクトを移動しないと、エラーは、UI に表示されます。

種類:

| 値 | 説明 |
| ----- | ----------- |
| 0 | オンライン |
| 1 | Warning |
| 2 | 権限がありません |
| 3 | エラー |
| 4 | 重大で致命的です |
| 5 | Unknown |

* 詳細
    * 状態を示す追加の詳細は、型を返します。

### 接続状態プロバイダーの PowerShell スクリプト

ターゲットは、オンラインと PowerShell スクリプトを使ってアクセスできるかどうかは、接続状態のプロバイダー PowerShell スクリプトを決定します。 結果は、"status"1 つのプロパティを持つオブジェクトで返される必要があります。 スクリプトの例は、次に示します。

PowerShell スクリプトの例

``` ts
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

### RelativeGatewayUrl 接続状態のプロバイダーのメソッドを定義します。

接続状態のプロバイダー```RelativeGatewayUrl```メソッドは、rest API、ターゲットがオンラインでアクセスできるかどうかを呼び出します。 結果は、"status"1 つのプロパティを持つオブジェクトで返される必要があります。 RelativeGatewayUrl の例の manifest.json 接続プロバイダー エントリは、次に示します。

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

RelativeGatewayUrl の使用に関するメモ:

* "relativeGatewayUrl"では、ゲートウェイ URL からの接続の状態を取得する場所を指定します。 この URI は、/api からの相対します。 URL に $connectionName が見つかった場合、接続の名前で置き換えられます。
* ホスト ゲートウェイは、ゲートウェイの拡張機能を作成して実行することに対する relativeGatewayUrl のすべてのプロパティを実行する必要があります。

### 実行時の値にマップします。

オブジェクトの戻り値の書式設定に状態でラベルと詳細情報の値は、プロバイダーの"defaultValueMap"プロパティのキーと値を含めることによって、時間を調整します。

たとえば、いつでもその"defaultConnection_test"表示ラベルまたは詳細については、のいずれかの値として Windows Admin Center が自動的には、下の値を追加する場合は、構成済みのリソース文字列値でキーを置き換えます。

``` json
    "defaultConnection_test": "resources:strings:addServer_status_defaultConnection_label"
```

## アプリケーションのレイヤーで接続プロバイダーを実装します。

OnInit を実装する TypeScript クラスを作成して、アプリケーション レイヤーで接続プロバイダーを実装する行いましょうできるようになりました。 クラスには、次の機能があります。

| 機能 | 説明 |
| -------- | ----------- |
| コンス トラクター (プライベート appContextService: AppContextService、プライベート ルート: ActivatedRoute) |  |
| パブリック ngOnInit() |  |
| パブリック onSubmit() | 追加接続しようとしたときにシェルを更新するためのロジックが含まれています |
| パブリック onCancel() | 追加の接続が取り消されると、シェルを更新するロジックが含まれています |

### OnSubmit を定義します。

```onSubmit``` 問題 RPC コールバック「追加接続」のシェルに通知するアプリのコンテキストにします。 基本的な呼び出しは、このような"updateData"を使用します。

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

結果は、接続のプロパティを次の構造に準拠しているオブジェクトの配列です。

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

### OnCancel を定義します。

```onCancel``` 空の接続の配列を渡すことによって、「接続の追加」試行をキャンセルします。

``` ts
this.appContextService.rpc.updateData(EnvironmentModule.nameOfShell, '##', <RpcUpdateData>{ results: { connections: [] } });
```

## 接続プロバイダーの例

接続のプロバイダーを実装するための完全な TypeScript クラスを下回っています。 注: が「クエリ文字列」文字列と一致する、"クエリ文字列 manifest.json で接続プロバイダーで定義されています。

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
