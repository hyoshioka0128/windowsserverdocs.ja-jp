---
title: 追加 DriverGroupFilter
description: Add DriverGroupFilter の Windows コマンドに関するトピック。サーバー上のドライバーグループにフィルターを追加します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a66c5e68-99ea-4e47-b68d-8109633ae336
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6a62baf85462d4340d61196bc154efd6d852f1f7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80832115"
---
# <a name="add-drivergroupfilter"></a>追加 DriverGroupFilter

サーバー上のドライバー グループにフィルターを追加します。

## <a name="syntax"></a>構文

```
WDSUTIL /Add-DriverGroupFilter /DriverGroup:<Group Name> [/Server:<Server name>] /FilterType:<Filter Type> /Policy:{Include | Exclude} /Value:<Value> [/Value:<Value> ...]
```

### <a name="parameters"></a>パラメーター

|         パラメーター          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                            説明                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /Drivergroup:\<グループ名 > |                                                                                                                                                                                                                                                                                                                                                                                                                                                              ドライバー グループの名前を指定します。                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|  [/Server:\<サーバー名 >]  |                                                                                                                                                                                                                                                                                                                                                                                                               サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。                                                                                                                                                                                                                                                                                                                                                                                                               |
| /FilterType:\<FilterType >  |                                                                                                                                                                                                   グループに追加するフィルターの種類を指定します。 1 つのコマンドでは、複数のフィルターの種類を指定できます。 各フィルターの種類を記述してください **/policy:enabled** し、少なくとも 1 つ含める **/value**します。 \<FilterType > には、 **Biosvendor**、 **biosvendor**、 **ChassisType**、 **Manufacturer**、 **Uuid**、 **OsVersion**、 **OsEdition**、または**oslanguage**を指定できます。 他のすべてのフィルターの種類の値を取得する方法については、「[ドライバーグループのフィルター](https://go.microsoft.com/fwlink/?LinkID=155158) (<https://go.microsoft.com/fwlink/?LinkID=155158>)」を参照してください。                                                                                                                                                                                                    |
|     [/ポリシー: {Include      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                             除外}]                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|     [/値:\<値 >]      | 対応するクライアントの値を指定 **/FilterType**します。 1 つの型に複数の値を指定できます。 有効な値については、次の一覧を参照してください **ChassisType**します。 他のすべてのフィルターの種類の値を取得する方法については、「[ドライバーグループのフィルター](https://go.microsoft.com/fwlink/?LinkID=155158) (<https://go.microsoft.com/fwlink/?LinkID=155158>)」を参照してください。</br>**他の**</br>**UnknownChassis**</br>**デスクトップ**</br>**LowProfileDesktop**</br>**PizzaBox**</br>**MiniTower**</br>**塔**</br>**可能**</br>**本体**</br>**ノートブック**</br>**ハンドヘルド**</br>**Docのステーション**</br>**AllInOne**</br>**SubNotebook**</br>**SpaceSaving**</br>**LunchBox**</br>**MainSystemChassis**</br>**全シャーシ**</br>**SubChassis**</br>**Busのシャーシ**</br>**PeripheralChassis**</br>**Storagの Assis**</br>**RackMountChassis**</br>**マイ aledcasecom**</br>**MultiSystemChassis**</br>**CompactPci**</br>**AdvancedTca** |

## <a name="examples"></a><a name=BKMK_examples></a>例

ドライバー グループにフィルターを追加するには、次のいずれかを入力します。
```
WDSUTIL /Add-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /Policy:Include /Value:Name1 /Value:Name2
```
```
WDSUTIL /Add-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /Policy:Include /Value:Name1 /FilterType:ChassisType /Policy:Exclude /Value:Tower /Value:MiniTower
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

