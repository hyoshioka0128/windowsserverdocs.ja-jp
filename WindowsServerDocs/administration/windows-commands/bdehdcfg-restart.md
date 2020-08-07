---
title: bdehdcfg restart
description: Bdehdcfg restart コマンドのリファレンス記事。ドライブの準備が完了した後で、コンピューターを再起動する必要があることを bdehdcfg に伝えます。
ms.topic: article
ms.assetid: a98b76bb-36f1-4790-b337-7dc35f606bc6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 67d2a3dd7b4304c26543840d6681b4ec6e655651
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87895097"
---
# <a name="bdehdcfg-restart"></a>bdehdcfg: 再起動

ドライブの準備が完了した後にコンピューターを再起動する必要があることを bdehdcfg コマンドラインツールに通知します。 他のユーザーがコンピューターにログオンしていて、 **quiet**コマンドが指定されていない場合は、コンピューターを再起動するかどうかを確認するメッセージが表示されます。

## <a name="syntax"></a>構文

```
bdehdcfg -target {default|unallocated|<drive_letter> shrink|<drive_letter> merge} -restart
```

#### <a name="parameters"></a>パラメーター

このコマンドには追加のパラメーターはありません。

## <a name="examples"></a>例

**Restart**コマンドを使用するには:

```
bdehdcfg -target default -restart
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bdehdcfg](bdehdcfg.md)
