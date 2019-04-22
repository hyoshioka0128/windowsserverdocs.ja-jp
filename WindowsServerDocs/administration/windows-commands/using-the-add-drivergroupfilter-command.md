---
title: 追加 DriverGroupFilter コマンドを使用してください。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a66c5e68-99ea-4e47-b68d-8109633ae336
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 16962bd87fabd1ee689b962547c2b1aa470283c1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817383"
---
# <a name="using-the-add-drivergroupfilter-command"></a>追加 DriverGroupFilter コマンドを使用してください。



サーバー上のドライバー グループにフィルターを追加します。

## <a name="syntax"></a>構文

```
WDSUTIL /Add-DriverGroupFilter /DriverGroup:<Group Name> [/Server:<Server name>] /FilterType:<Filter Type> /Policy:{Include | Exclude} /Value:<Value> [/Value:<Value> ...]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/DriverGroup:\<グループ名 >|ドライバー グループの名前を指定します。|
|[/Server:\<サーバー名 >]|サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。|
|/FilterType:\<FilterType>|グループに追加するフィルターの種類を指定します。 1 つのコマンドでは、複数のフィルターの種類を指定できます。 各フィルターの種類を記述してください **/policy:enabled** し、少なくとも 1 つ含める **/value**します。 \<FilterType > できる**BiosVendor**、 **BiosVersion**、 **ChassisType**、**製造元**、 **Uuid**、 **OsVersion**、 **OsEdition**、または**OsLanguage**します。 その他のすべてのフィルターの種類の値を取得する方法の詳細については、次を参照してください。[ドライバー グループのフィルター](https://go.microsoft.com/fwlink/?LinkID=155158) (https://go.microsoft.com/fwlink/?LinkID=155158)します。|
|[/ポリシー: {含める | 除外}]|場合 **/policy:enabled** に設定されている **Include**, 、フィルターに一致するクライアント コンピューターがこのグループのドライバーをインストールを許可します。 場合 **/policy:enabled** に設定されている **除外**, 、フィルターに一致するクライアント コンピューターがこのグループのドライバーをインストールする許可されていません。|
|[/値:\<値 >]|対応するクライアントの値を指定 **/FilterType**します。 1 つの型に複数の値を指定できます。 有効な値については、次の一覧を参照してください **ChassisType**します。 その他のすべてのフィルターの種類の値を取得する方法の詳細については、次を参照してください。[ドライバー グループのフィルター](https://go.microsoft.com/fwlink/?LinkID=155158) (https://go.microsoft.com/fwlink/?LinkID=155158)します。</br>**その他**</br>**UnknownChassis**</br>**デスクトップ**</br>**LowProfileDesktop**</br>**PizzaBox**</br>**ミニタワー**</br>**タワー**</br>**ポータブル**</br>**ラップトップ コンピューター**</br>**ノートブック**</br>**ハンドヘルド**</br>**DockingStation**</br>**AllInOne**</br>**SubNotebook**</br>**SpaceSaving**</br>**LunchBox**</br>**MainSystemChassis**</br>**ExpansionChassis**</br>**SubChassis**</br>**BusExpansionChassis**</br>**PeripheralChassis**</br>**StorageChassis**</br>**RackMountChassis**</br>**SealedCaseComputer**</br>**MultiSystemChassis**</br>**CompactPci**</br>**AdvancedTca**|

## <a name="BKMK_examples"></a>例

ドライバー グループにフィルターを追加するには、次のいずれかを入力します。
```
WDSUTIL /Add-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /Policy:Include /Value:Name1 /Value:Name2
```
```
WDSUTIL /Add-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /Policy:Include /Value:Name1 /FilterType:ChassisType /Policy:Exclude /Value:Tower /Value:MiniTower
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)

