---
title: bitsadmin cache および setlimit
description: キャッシュサイズの制限を設定する bitsadmin cache および setlimit コマンドの参照記事。
ms.topic: article
ms.assetid: 46578835-d5ce-423b-be4d-62ddb9e1908d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 41a1331a19f66e7d84dc3eb57b04d42596a40628
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894702"
---
# <a name="bitsadmin-cache-and-setlimit"></a>bitsadmin cache および setlimit

キャッシュサイズの制限を設定します。

## <a name="syntax"></a>構文

```
bitsadmin /cache /setlimit percent
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| パーセント | ハードディスクの合計領域に対する割合として定義されているキャッシュの制限。 |

## <a name="examples"></a>例

キャッシュサイズの制限を50% に設定するには、次のようにします。

```
bitsadmin /cache /setlimit 50
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin cache コマンド](bitsadmin-cache.md)
