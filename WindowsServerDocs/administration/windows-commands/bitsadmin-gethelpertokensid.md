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
ms.openlocfilehash: b616b9cc80b21c4c6a72fcca55dcdd893fac2730
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928192"
---
# <a name="bitsadmin-gethelpertokensid"></a>bitsadmin gethelpertokensid

BITS 転送ジョブの [ヘルパートークン](https://docs.microsoft.com/windows/win32/bits/helper-tokens-for-bits-transfer-jobs)が設定されている場合、その SID を返します。

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

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
