---
title: 削除 DriverGroupFilter コマンドを使用してください。
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 837bd5d4-c79d-4714-942d-9875bd8e61dc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 75b4a1446b5fb4db4132a39b6e5ba70cd1c4ab4b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362921"
---
# <a name="using-the-remove-drivergroupfilter-command"></a>削除 DriverGroupFilter コマンドを使用してください。



サーバー上のドライバー グループから、フィルタの規則を削除します。

## <a name="syntax"></a>構文

```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:<Group Name> [/Server:<Server name>] /FilterType:<Filter Type>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/Drivergroup: \<Group Name >|ドライバー グループの名前を指定します。|
|[/Server: \<Server name >]|サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。|
|[/FilterType: \<FilterType >]|グループから削除するフィルターの種類を指定します。 \<FilterType > には、次のいずれかを指定できます。</br>**Bios ベンダー**</br>**Bios のバージョン**</br>**ChassisType**</br>**Manufacturer**</br>**Uuid**</br>**OsVersion**</br>**OsEdition**</br>**OsLanguage**|

## <a name="BKMK_examples"></a>例

フィルターを削除するには、次のいずれかを入力します。
```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer
```
```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /FilterType:OSLanguage
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)