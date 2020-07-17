---
title: bitsadmin cache および setexpirationtime
description: キャッシュの有効期限を設定する bitsadmin cache と setexpirationtime コマンドの参照記事。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 00ea6e4e-b707-4b31-88dd-b61a78565c8d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 60372a74acc6ea5312afb5dafcb3ab7b3299f4d2
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923255"
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

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin cache コマンド](bitsadmin-cache.md)
