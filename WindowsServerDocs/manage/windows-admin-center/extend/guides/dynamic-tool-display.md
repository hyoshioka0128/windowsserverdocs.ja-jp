---
title: ソリューションのツールの可視性を制御します。
description: Windows Admin Center SDK (Project Honolulu) ソリューションのツールの可視性を制御します。
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: f3f34b4c86854bfc55cf4b1b57a0fd3c2baf2ffc
ms.sourcegitcommit: be0144eb59daf3269bebea93cb1c467d67e2d2f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2018
ms.locfileid: "4080969"
---
# ソリューションのツールの可視性を制御します。 #

>適用対象: Windows Admin Center、Windows Admin Center Preview

ツールを利用可能なツールの一覧から、拡張機能を除外する (または非表示にする) に必要な場合があります。 たとえば、ツールが Windows Server 2016 (いない以前のバージョン) のみを対象としない場合してすべてのツールは、Windows Server 2012 R2 サーバーに接続しているユーザー。 (、ユーザー エクスペリエンスを想像して [、読み込み、その機能は、接続に使用できることのメッセージを取得するためだけのツールを待ってから、)。ツールの manifest.json ファイルで、この機能を表示する (または非表示にする) を定義できます。

## ツールを表示するタイミングを決定するためのオプション ##

ツールが表示され、特定のサーバーまたはクラスター接続の利用可能にするかどうかを判断に使える 3 つの異なるオプションがあります。

* localhost
* インベントリ (プロパティの配列)
* スクリプト

### LocalHost ###

条件オブジェクトの localHost プロパティには、か接続のノードが localHost (に Windows Admin Center がインストールされている同じコンピューター) である場合に推測を評価できるブール値が含まれています。 タイミング プロパティに値を渡して、指定する (条件) ツールを表示します。 たとえば、ユーザーが実際にはローカル ホストに接続している場合に表示するツールのみ場合、このようなを設定します。

``` json
"conditions": [
{
    "localhost": true
}]
```

また、する場合のみときに表示ツールは、接続しているノード*でない*localhost:

``` json
"conditions": [
{
    "localhost": false
}]
```

ここでは構成設定次のようにのみ表示ツール接続のノードが localhost でない場合です。

``` json
"entryPoints": [
{
    "entryPointType": "tool",
    "name": "main",
    "urlName": "processes",
    "displayName": "resources:strings:displayName",
    "description": "resources:strings:description",
    "icon": "sme-icon:icon-win-serverProcesses",
    "path": "",
    "requirements": [
    {
        "solutionIds": [
        "msft.sme.server-manager!windowsClients"
        ],
        "connectionTypes": [
        "msft.sme.connection-type.windows-client"
        ],
        "conditions": [
        {
            "localhost": true
        }
        ]
    }
    ]
}
```

### インベントリのプロパティ ###

SDK には、事前に整理されたとき、ツールは使用可能かどうかを判断する条件を構築するために使用できるインベントリ プロパティのセットが含まれています。 'インベントリ' 配列には、9 個のさまざまなプロパティがあります。

| プロパティ名 | 予期される値の種類 |
| ------------- | ------------------- |
| computerManufacturer | string |
| operatingSystemSKU | number |
| operatingSystemVersion | version_string (例:"10.1 *")。 |
| productType | number |
| clusterFqdn | string |
| isHyperVRoleInstalled | boolean |
| isHyperVPowershellInstalled | boolean |
| isManagementToolsAvailable | boolean |
| isWmfInstalled | boolean |

インベントリ配列内の各オブジェクトは、次の json 構造に準拠している必要があります。

``` json
"<property name>": {
    "type": "<expected type>",
    "operator": "<defined operator to use>",
    "value": "<expected value to evaluate using the operator>"
}
```

#### 演算子の値 ####

| 演算子 | 説明 |
| -------- | ----------- |
| gt | greater than (次の値より大きい) |
| ge | 以上の値 |
| lt | less than (次の値より小さい) |
| le | 以下に等しい |
| eq | 等しい |
| ne | not equal to (次の値と等しくない) |
|  が  | 値が true のかどうかの確認 |
| じゃない | 値が false の確認 |
| 含まれています | 文字列内の項目に存在します。 |
| notContains | 文字列内の項目が存在しません。 |

#### データ型 ####

'型' プロパティで使用できるオプション:

| 種類 | 説明 |
| ---- | ----------- |
| version | バージョン番号 (例: 10.1 *)。 |
| number | 数値 |
| string | 文字列値 |
| boolean | true または false |

#### 値の型 ####

'Value' プロパティは、これらの型を受け入れます。

* string
* number
* boolean

インベントリの適切な形式の条件セットは、このようになります。

``` json
"entryPoints": [
{
    "entryPointType": "tool",
    "name": "main",
    "urlName": "processes",
    "displayName": "resources:strings:displayName",
    "description": "resources:strings:description",
    "icon": "sme-icon:icon-win-serverProcesses",
    "path": "",
    "requirements": [
    {
        "solutionIds": [
        "msft.sme.server-manager!servers"
        ],
        "connectionTypes": [
        "msft.sme.connection-type.server"
        ],
        "conditions": [
        {
            "inventory": {
            "operatingSystemVersion": {
                "type": "version",
                "operator": "gt",
                "value": "6.3"
            },
            "operatingSystemSKU": {
                "type": "number",
                "operator": "eq",
                "value": "8"
            }
            }
        }
        ]
    }
    ]
}
```

### スクリプト ###

最後に、可用性とノードの状態を識別するカスタム PowerShell スクリプトを実行することができます。 すべてのスクリプトは、次の構造を使ってオブジェクトを返す必要があります。

``` ps
@{
    State = 'Available' | 'NotSupported' | 'NotConfigured';
    Message = '<Message to explain the reason of state such as not supported and not configured.>';
    Properties =
        @{ Name = 'Prop1'; Value = 'prop1 data'; Type = 'string' },
        @{Name='Prop2'; Value = 12345678; Type='number'; };
}
```
状態のプロパティは、ツールの一覧で拡張機能を非表示の意思決定を制御する重要な値です。  許容値は次のとおりです。
| 値 | 説明 |
| ---- | ----------- |
| 使用できます。 | 拡張機能は、ツールの一覧に表示する必要があります。 |
| サポートされて | 拡張機能をツールの一覧に表示されないようにします。 |
| NotConfigured | これは、プレース ホルダーの値は、ツールを利用する前に追加の構成のユーザーに求めます今後の作業です。  現在この値が表示されているツールで発生、"使用可能"に相当する機能。 |

たとえば、リモート サーバーにインストールされている BitLocker がある場合にのみを読み込むためのツールをたい場合、スクリプトは次のよう。

``` ps
$response = @{
    State = 'NotSupported';
    Message = 'Not executed';
    Properties = @{ Name = 'Prop1'; Value = 'prop1 data'; Type = 'string' },
        @{Name='Prop2'; Value = 12345678; Type='number'; };
}

if (Get-Module -ListAvailable -Name servermanager) {
    Import-module servermanager; 
    $isInstalled = (Get-WindowsFeature -name bitlocker).Installed;
    $isGood = $isInstalled;
}

if($isGood) {
    $response.State = 'Available';
    $response.Message = 'Everything should work.';
}

$response
```

次のようなスクリプト オプションを使用して、エントリ ポイントの構成。

``` json
"entryPoints": [
{
    "entryPointType": "tool",
    "name": "main",
    "urlName": "processes",
    "displayName": "resources:strings:displayName",
    "description": "resources:strings:description",
    "icon": "sme-icon:icon-win-serverProcesses",
    "path": "",
    "requirements": [
    {
        "solutionIds": [
        "msft.sme.server-manager!windowsClients"
        ],
        "connectionTypes": [
        "msft.sme.connection-type.windows-client"
        ],
        "conditions": [
        {
            "localhost": true,
            "inventory": {
            "operatingSystemVersion": {
                "type": "version",
                "operator": "eq",
                "value": "10.0.*"
            },
            "operatingSystemSKU": {
                "type": "number",
                "operator": "eq",
                "value": "4"
            }
            },
            "script": "$response = @{ State = 'NotSupported'; Message = 'Not executed'; Properties = @{ Name = 'Prop1'; Value = 'prop1 data'; Type = 'string' }, @{Name='Prop2'; Value = 12345678; Type='number'; }; }; if (Get-Module -ListAvailable -Name servermanager) { Import-module servermanager; $isInstalled = (Get-WindowsFeature -name bitlocker).Installed; $isGood = $isInstalled; }; if($isGood) { $response.State = 'Available'; $response.Message = 'Everything should work.'; }; $response"
        }
        ]
    }
    ]
}
```

## 複数の要件のセットをサポート ##

1 つ以上の一連の要件を使用すると、複数の「要件」ブロックを定義することによって、ツールを表示するのにタイミングを判断します。

場合に、ツールを表示する例では、「シナリオ A」または「シナリオ B」が true の場合、2 つの要件ブロックを定義します。いずれかが true の場合 (つまり、要件ブロック内のすべての条件が満たされている)、ツールが表示されます。

``` json
"entryPoints": [
{
    "requirements": [
    {
        "solutionIds": [
            …"scenario A"…
        ],
        "connectionTypes": [
            …"scenario A"…
        ],
        "conditions": [
            …"scenario A"…
        ]
    },
    {
        "solutionIds": [
            …"scenario B"…
        ],
        "connectionTypes": [
            …"scenario B"…
        ],
        "conditions": [
            …"scenario B"…
        ]
    }
    ]
}

```

## 条件の範囲をサポート ##

複数の「状態」ブロック、同じプロパティではなく、さまざまな演算子を定義することによってもさまざまな条件を定義できます。

同じプロパティを定義するにはさまざまな演算子を使用して、2 つの状態の間にある限り、ツールが表示されます。

たとえば、オペレーティング システムが 6.3.0 で、10.0.0 間のバージョンである限り、このツールが表示されます。

``` json
"entryPoints": [
{
    "entryPointType": "tool",
    "name": "main",
    "urlName": "processes",
    "displayName": "resources:strings:displayName",
    "description": "resources:strings:description",
    "icon": "sme-icon:icon-win-serverProcesses",
    "path": "",
    "requirements": [
    {
        "solutionIds": [
             "msft.sme.server-manager!servers"
        ],
        "connectionTypes": [
             "msft.sme.connection-type.server"
        ],
        "conditions": [
        {
            "inventory": {
                "operatingSystemVersion": {
                    "type": "version",
                    "operator": "gt",
                    "value": "6.3.0"
                },
            }
        },
        {
            "inventory": {
                "operatingSystemVersion": {
                    "type": "version",
                    "operator": "lt",
                    "value": "10.0.0"
                }
            }
        }
        ]
    }
    ]
}

```
