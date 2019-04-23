---
title: 削除 DriverGroupFilter コマンドを使用してください。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: a546ead7220273955368c582ac1e3f9b3f61c191
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883433"
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
|/DriverGroup:\<グループ名 >|ドライバー グループの名前を指定します。|
|[/Server:\<サーバー名 >]|サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。|
|[/FilterType:\<FilterType>]|グループから削除するフィルターの種類を指定します。 \<FilterType > 次のいずれかを指定できます。</br>**BiosVendor**</br>**BiosVersion**</br>**ChassisType**</br>**Manufacturer**</br>**uuid**</br>**osVersion**</br>**OsEdition**</br>**OsLanguage**|

## <a name="BKMK_examples"></a>例

フィルターを削除するには、次のいずれかを入力します。
```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer
```
```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /FilterType:OSLanguage
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)