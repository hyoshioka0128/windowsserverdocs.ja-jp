---
title: サブコマンド set DriverGroupFilter
description: Windows コマンドに関するトピックでは、ドライバーグループの既存のドライバーグループフィルターを追加または削除する、サブコマンドの set DriverGroupFilter。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 829ab1f0-4514-421e-9cc0-767b238da69c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a808bfd893e1f149a745db865fdc8bd28a618699
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834021"
---
# <a name="subcommand-set-drivergroupfilter"></a>サブコマンド: セット DriverGroupFilter

追加または既存のドライバー グループ フィルターをドライバー グループから削除します。

## <a name="syntax"></a>構文

```
WDSUTIL /Set-DriverGroupFilter /DriverGroup:<Group Name> [/Server:<Server name>] /FilterType:<Filter Type> [/Policy:{Include | Exclude}] [/AddValue:<Value> [/AddValue:<Value> ...]] [/RemoveValue:<Value> [/RemoveValue:<Value> ...]]
```

### <a name="parameters"></a>パラメーター

|         パラメーター          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                               説明                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /Drivergroup:\<グループ名 > |                                                                                                                                                                                                                                                                                                                                                                                                                                                                 ドライバー グループの名前を指定します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|  [/Server:\<サーバー名 >]  |                                                                                                                                                                                                                                                                                                                                                                                                                サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。                                                                                                                                                                                                                                                                                                                                                                                                                 |
| /FilterType:\<FilterType >  |                                                                                                                                                                                                                                                                       追加または削除するドライバー グループのフィルターの種類を指定します。 1 つのコマンドでは、複数のフィルターを指定できます。 各 **/FilterType**, 、追加またはを使用して複数の値を削除することができます **/RemoveValue** と **/AddValue**します。 \<FilterType > には、次のいずれかを指定できます。</br>**Bios ベンダー**</br>**Bios のバージョン**</br>**ChassisType**</br>**Manufacturer**</br>**Uuid**</br>**OsVersion**</br>**OsEdition**</br>**OsLanguage**                                                                                                                                                                                                                                                                        |
|     [/ポリシー: {Include      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                除外}]                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|    [/AddValue:\<値 >]    | フィルターに追加する新しいクライアントの値を指定します。 1 つのフィルターの種類に複数の値を指定できます。 有効な属性の値を次の一覧を参照してください **ChassisType**します。 他のすべてのフィルターの種類の値を取得する方法については、「[ドライバーグループのフィルター](https://go.microsoft.com/fwlink/?LinkID=155158) (<https://go.microsoft.com/fwlink/?LinkID=155158>)」を参照してください。</br>**他の**</br>**UnknownChassis**</br>**デスクトップ**</br>**LowProfileDesktop**</br>**PizzaBox**</br>**MiniTower**</br>**塔**</br>**可能**</br>**本体**</br>**ノートブック**</br>**ハンドヘルド**</br>**Docのステーション**</br>**AllInOne**</br>**SubNotebook**</br>**SpaceSaving**</br>**LunchBox**</br>**MainSystemChassis**</br>**全シャーシ**</br>**SubChassis**</br>**Busのシャーシ**</br>**PeripheralChassis**</br>**Storagの Assis**</br>**RackMountChassis**</br>**マイ aledcasecom**</br>**MultiSystemChassis**</br>**CompactPci**</br>**AdvancedTca** |
|  [/RemoveValue:\<値 >]   |                                                                                                                                                                                                                                                                                                                                                                                                                                     使用して指定したフィルターから削除する既存のクライアントの値を指定 **/AddValue**します。                                                                                                                                                                                                                                                                                                                                                                                                                                      |

## <a name="examples"></a><a name=BKMK_examples></a>例

フィルターを削除するには、次のいずれかを入力します。
```
WDSUTIL /Set-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /Policy:Include /AddValue:Name1 /RemoveValue:Name2
```
```
WDSUTIL /Set-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /Policy:Include /RemoveValue:Name1 /FilterType:ChassisType /Policy:Exclude /AddValue:Tower /AddValue:MiniTower
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)