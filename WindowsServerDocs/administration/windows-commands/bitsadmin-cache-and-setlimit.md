---
title: bitsadmin cache および setlimit
description: キャッシュサイズの制限を設定する bitsadmin cache と setlimit コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 46578835-d5ce-423b-be4d-62ddb9e1908d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a4c41102bfb87ff6d48113c4e85a821b821b5b01
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718288"
---
# <a name="bitsadmin-cache-and-setlimit"></a>bitsadmin cache および setlimit

キャッシュサイズの制限を設定します。

## <a name="syntax"></a>構文

```
bitsadmin /cache /setlimit percent
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| -------------- | -------------- |
| パーセント | ハードディスクの合計領域に対する割合として定義されているキャッシュの制限。 |

## <a name="examples"></a>例

キャッシュサイズの制限を50% に設定するには、次のようにします。

```
bitsadmin /cache /setlimit 50
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin cache コマンド](bitsadmin-cache.md)
