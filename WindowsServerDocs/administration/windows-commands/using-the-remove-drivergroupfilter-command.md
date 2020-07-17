---
title: DriverGroupFilter を削除します。
description: 削除 DriverGroupFilter のリファレンス記事。サーバー上のドライバーグループからフィルター規則を削除します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 837bd5d4-c79d-4714-942d-9875bd8e61dc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 98d2253cc5148ba4581399d688b74cd426a649fb
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85936332"
---
# <a name="remove-drivergroupfilter"></a>DriverGroupFilter を削除します。



サーバー上のドライバー グループから、フィルタの規則を削除します。

## <a name="syntax"></a>構文

```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:<Group Name> [/Server:<Server name>] /FilterType:<Filter Type>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|DriverGroup\<Group Name>|ドライバー グループの名前を指定します。|
|[/Server:\<Server name>]|サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。|
|[/FilterType:\<FilterType>]|グループから削除するフィルターの種類を指定します。 \<FilterType>次のいずれかを指定できます。</br>**Bios ベンダー**</br>**Bios のバージョン**</br>**ChassisType**</br>**製造元**</br>**Uuid**</br>**OsVersion**</br>**OsEdition**</br>**OsLanguage**|

## <a name="examples"></a>例

フィルターを削除するには、次のいずれかを入力します。
```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer
```
```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /FilterType:OSLanguage
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)