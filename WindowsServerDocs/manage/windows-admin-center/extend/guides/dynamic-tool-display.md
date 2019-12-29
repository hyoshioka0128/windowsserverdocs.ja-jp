---
title: ソリューションでのツールの可視性の制御
description: ソリューションでのツールの可視性の制御 Windows 管理センター SDK (Project ホノルル)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 440ba3d11da671beedc2c2fb90caa3e176f83877
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385318"
---
# <a name="control-your-tools-visibility-in-a-solution"></a>ソリューションでのツールの可視性の制御 #

>適用先:Windows Admin Center、Windows Admin Center Preview

使用可能なツールの一覧から拡張機能またはツールを除外 (または非表示にする) が必要になる場合があります。 たとえば、ツールが Windows Server 2016 (古いバージョンではない) のみを対象としている場合は、Windows Server 2012 R2 サーバーに接続しているユーザーがまったくツールを表示しないようにする必要があります。 (ユーザーエクスペリエンスを想像してください。クリックすると、ツールが読み込まれるまで待機します。その機能が接続に使用できないというメッセージが表示されます)。ツールのマニフェストの json ファイルで機能を表示 (または非表示) するタイミングを定義できます。

## <a name="options-for-deciding-when-to-show-a-tool"></a>ツールを表示するタイミングを決定するためのオプション ##

特定のサーバーまたはクラスター接続でツールを表示して使用できるようにするかどうかを決定するために使用できるオプションは3つあります。

* localhost
* インベントリ (プロパティの配列)
* スクリプト (script)

### <a name="localhost"></a>LocalHost ###

Condition オブジェクトの localHost プロパティには、接続しているノードが localHost (Windows 管理センターがインストールされている同じコンピューター) であるかどうかを推測するために評価できるブール値が含まれています。 プロパティに値を渡すことによって、いつ (条件) ツールを表示するかを指定します。 たとえば、ユーザーが実際にローカルホストに接続している場合にのみツールを表示するには、次のように設定します。

``` json
"conditions": [
{
    "localhost": true
}]
```

また、接続しているノードが localhost で*ない*場合にのみツールを表示するには、次のようにします。

``` json
"conditions": [
{
    "localhost": false
}]
```

接続しているノードが localhost でない場合にのみツールを表示するように構成設定が表示されるのは次のようになります。

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

SDK には、curated のインベントリプロパティのセットが含まれています。これらのプロパティを使用して、ツールをいつ使用できるようにするかを決定するための条件を作成できます。 ' Inventory ' 配列には、次の9つの異なるプロパティがあります。

| プロパティ名 | 予期される値の型 |
| ------------- | ------------------- |
| コンピューターの製造元 | string |
| operatingSystemSKU | number |
| operatingSystemVersion | version_string (例:"10.1. *") |
| productType | number |
| clusterFqdn | string |
| isHyperVRoleInstalled | boolean |
| isHyperVPowershellInstalled | boolean |
| Ismanagementツールを使用できます | boolean |
| isWmfInstalled | boolean |

インベントリ配列内のすべてのオブジェクトは、次の json 構造に準拠している必要があります。

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
| ge | 以上 |
| lt | less than (次の値より小さい) |
| le | 以下 |
| eq | 等しい |
| ne | not equal to (次の値と等しくない) |
| が | 値が true であるかどうかを確認しています |
| 非 | 値が false かどうかを確認しています |
| は | 項目が文字列内に存在します |
| notContains | 項目が文字列内に存在しません |

#### <a name="data-types"></a>データ型 ####

' Type ' プロパティで使用可能なオプション:

| 種類 | 説明 |
| ---- | ----------- |
| version | バージョン番号 (例:10.1. *) |
| number | 数値 |
| string | 文字列値 |
| boolean | true または false |

#### <a name="value-types"></a>値型 ####

' Value ' プロパティは、次の型を受け取ります。

* string
* number
* boolean

正しい形式のインベントリ条件セットは次のようになります。

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

最後に、カスタム PowerShell スクリプトを実行して、ノードの可用性と状態を識別できます。 すべてのスクリプトは、次の構造を持つオブジェクトを返す必要があります。

``` ps
@{
    State = 'Available' | 'NotSupported' | 'NotConfigured';
    Message = '<Message to explain the reason of state such as not supported and not configured.>';
    Properties =
        @{ Name = 'Prop1'; Value = 'prop1 data'; Type = 'string' },
        @{Name='Prop2'; Value = 12345678; Type='number'; };
}
```
State プロパティは、[ツール] ボックスの一覧で拡張機能を表示または非表示にする決定を制御する重要な値です。  使用できる値は次のとおりです。

| 値 | 説明 |
| ---- | ----------- |
| 使用できます。 | 拡張機能が [ツール] ボックスの一覧に表示されます。 |
| NotSupported | 拡張機能は、[ツール] ボックスの一覧に表示されません。 |
| NotConfigured | これは、ツールが使用可能になる前にユーザーに追加の構成を求めるプロンプトを表示する、今後の作業のためのプレースホルダー値です。  現在この値を指定すると、ツールが表示されます。これは、' Available ' と同等の機能です。 |

たとえば、リモートサーバーに BitLocker がインストールされている場合にのみツールを読み込むようにするには、スクリプトは次のようになります。

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

スクリプトオプションを使用したエントリポイントの構成は次のようになります。

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

## <a name="supporting-multiple-requirement-sets"></a>複数の要件セットのサポート ##

複数の要件セットを使用して、複数の "要件" ブロックを定義することで、どのようなときにツールを表示するかを決定できます。

たとえば、"scenario A" または "scenario B" が true の場合にツールを表示するには、2つの要件ブロックを定義します。いずれかが true の場合 (つまり、要件ブロック内のすべての条件が満たされる場合)、ツールが表示されます。

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

## <a name="supporting-condition-ranges"></a>条件範囲のサポート ##

また、同じプロパティを持つ複数の "条件" ブロックを定義して、さまざまな演算子で条件の範囲を定義することもできます。

同じプロパティが異なる演算子で定義されている場合、値が2つの条件の間にある限り、ツールが表示されます。

たとえば、オペレーティングシステムが6.3.0 と10.0.0 の間のバージョンである限り、このツールが表示されます。

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
