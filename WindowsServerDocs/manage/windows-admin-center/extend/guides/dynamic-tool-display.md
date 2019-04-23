---
title: ソリューション内のツールの表示を制御します。
description: Windows Admin Center SDK (プロジェクト ホノルル) ソリューションのツールの表示を制御します。
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: f3f34b4c86854bfc55cf4b1b57a0fd3c2baf2ffc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839253"
---
# <a name="control-your-tools-visibility-in-a-solution"></a>ソリューション内のツールの表示を制御します。 #

>適用先:Windows Admin Center、Windows Admin Center プレビュー

拡張機能またはツールを使用可能なツールの一覧からを除外する (または非表示にする) 必要な場合がある可能性があります。 たとえば、ツールが Windows Server 2016 (いない以前のバージョン) のみを対象とする場合たくない、ツールがまったく表示する Windows Server 2012 R2 サーバーに接続するユーザー。 (ユーザー エクスペリエンスを想像してください、クリックして、ツールを読み込むの機能が、接続に使用できないことのメッセージを取得するためだけを待機します)。ツールの manifest.json ファイルで、機能の表示 (または非表示) するタイミングを定義できます。

## <a name="options-for-deciding-when-to-show-a-tool"></a>ツールを表示するタイミングを決定するためのオプション ##

ツールが表示され、特定のサーバーまたはクラスターの接続を使用するかどうかを判断する際、3 つの異なるオプションがあります。

* localhost
* インベントリ (プロパティの配列)
* スクリプト (script)

### <a name="localhost"></a>LocalHost ###

条件オブジェクトの localHost プロパティは、かどうかに接続するノードが localHost (Windows Admin Center にインストールされている同じコンピューター) である場合の推測に評価されるブール値を含みます。 ときに、プロパティに値を渡すことによって指定する (条件) ツールを表示します。 たとえば、ユーザーがローカル ホストに実際には接続している場合に表示するツールが欲しい場合、このようなを設定します。

``` json
"conditions": [
{
    "localhost": true
}]
```

または、ときに表示するためのツールが欲しい場合、接続元ノード*ない*localhost:

``` json
"conditions": [
{
    "localhost": false
}]
```

構成設定の外観のみを表示するツールを接続するノードが localhost ではないときに次に示します。

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

### <a name="inventory-properties"></a>インベントリのプロパティ ###

SDK には、事前に精選されたかを確認する、ツールが使用できるかどうかの条件を作成に使用できるインベントリのプロパティのセットが含まれています。 [インベントリ] 配列には、9 つの異なるプロパティがあります。

| プロパティ名 | 予期される値型 |
| ------------- | ------------------- |
| computerManufacturer | string |
| operatingSystemSKU | number |
| operatingSystemVersion | version_string (例。"10.1.*") |
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

#### <a name="operator-values"></a>演算子の値 ####

| 演算子 | 説明 |
| -------- | ----------- |
| gt | greater than (次の値より大きい) |
| ge | 大きいまたは等しい |
| lt | less than (次の値より小さい) |
| le | 等しいまたはそれよりも小さい |
| eq | 等しい |
| ne | not equal to (次の値と等しくない) |
| が | 値が true のかどうかにチェック |
| 非 | 確認のかどうか、値は false |
| 含まれています | 項目を文字列に存在します |
| notContains | 項目が文字列内に存在しません |

#### <a name="data-types"></a>データ型 ####

'Type' プロパティの使用可能なオプション:

| 種類 | 説明 |
| ---- | ----------- |
| version | バージョン番号 (例。10.1.*) |
| number | 数値の値 |
| string | 文字列値 |
| boolean | true または false |

#### <a name="value-types"></a>値型 ####

'Value' プロパティは、これらの型を受け取ります。

* string
* number
* boolean

インベントリの適切な形式の条件セットのようになります。

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

### <a name="script"></a>スクリプト ###

最後に、可用性とノードの状態を識別するためにカスタム PowerShell スクリプトを実行することができます。 すべてのスクリプトでは、次の構造を持つオブジェクトを返す必要があります。

``` ps
@{
    State = 'Available' | 'NotSupported' | 'NotConfigured';
    Message = '<Message to explain the reason of state such as not supported and not configured.>';
    Properties =
        @{ Name = 'Prop1'; Value = 'prop1 data'; Type = 'string' },
        @{Name='Prop2'; Value = 12345678; Type='number'; };
}
```
State プロパティは、ツールの一覧で、拡張機能を非表示の意思決定を制御する重要な値です。  使用できる値は次のとおりです。
| 値 | 説明 |
| ---- | ----------- |
| 使用できます。 | 拡張機能は、ツールの一覧に表示する必要があります。 |
| NotSupported | 拡張機能は、ツールの一覧で表示されませんする必要があります。 |
| NotConfigured | これは、ツールを利用する前に、追加の構成のユーザーを指示する将来のプレース ホルダーの値です。  現在この値は、表示されているツールになります、'使用可能な' 機能と等価です。 |

たとえば、リモート サーバーにインストールされている BitLocker がある場合にのみを読み込むためのツール、する場合、スクリプトはようになります。

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

スクリプト オプションを使用して、エントリ ポイントの構成のようになります。

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

## <a name="supporting-multiple-requirement-sets"></a>複数の要件セットをサポート ##

要件の 1 つ以上のセットを使用すると、複数の「要件」ブロックを定義することで、ツールを表示するのにかを判断します。

場合、ツールに表示する例では、「シナリオ A」または「シナリオ B」が true の場合、2 つの要件のブロック; の定義いずれかが true の場合 (つまり、要件ブロック内のすべての条件が満たされた、)、ツールが表示されます。

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

## <a name="supporting-condition-ranges"></a>条件の範囲のサポート ##

複数の「条件」ブロック、同じプロパティではなく、さまざまな演算子を定義することでさまざまな条件を定義することもできます。

さまざまな演算子を使用して同じプロパティを定義するときは、2 つの条件の間にある限り、ツールが表示されます。

たとえば、オペレーティング システムが 6.3.0 と 10.0.0 の間のバージョンである限り、このツールが表示されます。

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
