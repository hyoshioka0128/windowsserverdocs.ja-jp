---
title: bitsadmin cache および setlimit
description: キャッシュサイズの制限を設定する bitsadmin cache および setlimit コマンドの参照記事。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 46578835-d5ce-423b-be4d-62ddb9e1908d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: de218990d9176336e779b551bfacc0897df5d114
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923214"
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
