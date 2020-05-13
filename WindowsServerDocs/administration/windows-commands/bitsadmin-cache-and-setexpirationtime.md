---
title: bitsadmin cache および setexpirationtime
description: キャッシュの有効期限を設定する bitsadmin cache と setexpirationtime コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 00ea6e4e-b707-4b31-88dd-b61a78565c8d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: eeb1dbd0439a1a39711e2a074ada4c772b9ca016
ms.sourcegitcommit: aed942d11f1a361fc1d17553a4cf190a864d1268
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83235037"
---
# <a name="bitsadmin-cache-and-setexpirationtime"></a>bitsadmin cache および setexpirationtime

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

キャッシュの有効期限を設定します。

## <a name="syntax"></a>構文

```
bitsadmin /cache /setexpirationtime secs
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| 秒数 | キャッシュの有効期限が切れるまでの秒数。 |

## <a name="examples"></a>例

キャッシュの有効期限を60秒で設定するには、次のようにします。

```
bitsadmin /cache / setexpirationtime 60
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin cache コマンド](bitsadmin-cache.md)
