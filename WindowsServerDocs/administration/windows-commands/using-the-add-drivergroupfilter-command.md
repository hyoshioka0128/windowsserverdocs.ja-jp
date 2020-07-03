---
title: 追加 DriverGroupFilter
description: 追加 DriverGroupFilter のリファレンス記事。サーバー上のドライバーグループにフィルターを追加します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a66c5e68-99ea-4e47-b68d-8109633ae336
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c8061bbde188fca5dbdd5a97ddfd708aedf1c9be
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85937222"
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
| DriverGroup\<Group Name> |                                                                                                                                                                                                                                                                                                                                                                                                                                                              ドライバー グループの名前を指定します。                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|  [/Server:\<Server name>]  |                                                                                                                                                                                                                                                                                                                                                                                                               サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。                                                                                                                                                                                                                                                                                                                                                                                                               |
| FilterType\<FilterType>  |                                                                                                                                                                                                   グループに追加するフィルターの種類を指定します。 1 つのコマンドでは、複数のフィルターの種類を指定できます。 各フィルターの種類を記述してください **/policy:enabled** し、少なくとも 1 つ含める **/value**します。 \<FilterType>には、 **Biosvendor**、 **biosvendor**、 **ChassisType**、 **Manufacturer**、 **Uuid**、 **OsVersion**、 **OsEdition**、または**oslanguage**を指定できます。 他のすべてのフィルターの種類の値を取得する方法については、「[ドライバーグループのフィルター](https://go.microsoft.com/fwlink/?LinkID=155158) 」 () を参照してください <https://go.microsoft.com/fwlink/?LinkID=155158> 。                                                                                                                                                                                                    |
|     [/ポリシー: {Include      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                             除外}]                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|     [/Value:\<Value>]      | 対応するクライアントの値を指定 **/FilterType**します。 1 つの型に複数の値を指定できます。 有効な値については、次の一覧を参照してください **ChassisType**します。 他のすべてのフィルターの種類の値を取得する方法については、「[ドライバーグループのフィルター](https://go.microsoft.com/fwlink/?LinkID=155158) 」 () を参照してください <https://go.microsoft.com/fwlink/?LinkID=155158> 。</br>**その他**</br>**UnknownChassis**</br>**デスクトップ**</br>**LowProfileDesktop**</br>**PizzaBox**</br>**ミニタワー**</br>**塔**</br>**移植性があります。**</br>**ノート PC**</br>**ノートブック**</br>**ハンドヘルド**</br>**DockingStation**</br>**AllInOne**</br>**SubNotebook**</br>**SpaceSaving**</br>**LunchBox**</br>**MainSystemChassis**</br>**ExpansionChassis**</br>**SubChassis**</br>**BusExpansionChassis**</br>**PeripheralChassis**</br>**Storagの Assis**</br>**RackMountChassis**</br>**SealedCaseComputer**</br>**MultiSystemChassis**</br>**CompactPci**</br>**AdvancedTca** |

## <a name="examples"></a>例

ドライバー グループにフィルターを追加するには、次のいずれかを入力します。
```
WDSUTIL /Add-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /Policy:Include /Value:Name1 /Value:Name2
```
```
WDSUTIL /Add-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /Policy:Include /Value:Name1 /FilterType:ChassisType /Policy:Exclude /Value:Tower /Value:MiniTower
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

