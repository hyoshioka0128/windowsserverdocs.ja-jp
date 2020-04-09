---
title: DriverGroupFilter を削除します。
description: 削除 DriverGroupFilter の Windows コマンドに関するトピックでは、サーバー上のドライバーグループからフィルター規則を削除します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 837bd5d4-c79d-4714-942d-9875bd8e61dc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 08914b66c37d327ddef2a50d2f98adcfdbb88ffe
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830495"
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
|/Drivergroup:\<グループ名 >|ドライバー グループの名前を指定します。|
|[/Server:\<サーバー名 >]|サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。|
|[/FilterType:\<FilterType >]|グループから削除するフィルターの種類を指定します。 \<FilterType > には、次のいずれかを指定できます。</br>**Bios ベンダー**</br>**Bios のバージョン**</br>**ChassisType**</br>**Manufacturer**</br>**Uuid**</br>**OsVersion**</br>**OsEdition**</br>**OsLanguage**|

## <a name="examples"></a><a name=BKMK_examples></a>例

フィルターを削除するには、次のいずれかを入力します。
```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer
```
```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /FilterType:OSLanguage
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)