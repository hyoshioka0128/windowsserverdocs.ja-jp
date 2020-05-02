---
title: DriverGroup を削除します。
description: ドライバーグループをサーバーから削除する、削除 DriverGroup のリファレンストピックです。
ms.prod: windows-server
ms.topic: article
ms.assetid: 1fefe9df-9782-433c-8abe-3f1a35e50da2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 314c7a73c7aeb49bc6bb96de23ca5bf4387bd932
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720417"
---
# <a name="remove-drivergroup"></a>DriverGroup を削除します。

サーバーからドライバー グループを削除します。

## <a name="syntax"></a>構文

```
WDSUTIL /Remove-DriverGroup /DriverGroup:<Group Name> [/Server:<Server name>]
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|/Drivergroup:\<グループ名>|削除するドライバー グループの名前を指定します。|
|[/Server:\<サーバー名>]|サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。|

## <a name="examples"></a>例

ドライバー グループを削除するには、次のいずれかを入力します。
```
WDSUTIL /Remove-DriverGroup /DriverGroup:PrinterDrivers
```
```
WDSUTIL /Remove-DriverGroup /DriverGroup:PrinterDrivers /Server:MyWdsServer
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)