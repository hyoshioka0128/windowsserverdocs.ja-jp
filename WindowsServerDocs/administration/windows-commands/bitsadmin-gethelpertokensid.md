---
title: bitsadmin gethelpertokensid
description: BITS 転送ジョブのヘルパートークンが設定されている場合、その SID を返す bitsadmin geの pertokensid コマンドの参照記事。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 3c8ef7502c524994454c697e2fa7d5dee223da5d
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86955464"
---
# <a name="bitsadmin-gethelpertokensid"></a>bitsadmin gethelpertokensid

BITS 転送ジョブの [ヘルパートークン](/windows/win32/bits/helper-tokens-for-bits-transfer-jobs)が設定されている場合、その SID を返します。

> [!NOTE]
> このコマンドは、BITS 3.0 以前ではサポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /gethelpertokensid <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前の BITS 転送ジョブの SID を取得するには、次のようにします。

```
bitsadmin /gethelpertokensid myDownloadJob
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
