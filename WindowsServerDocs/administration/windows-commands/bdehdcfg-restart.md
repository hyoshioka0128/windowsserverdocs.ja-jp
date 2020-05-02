---
title: bdehdcfg restart
description: Bdehdcfg restart コマンドのリファレンストピック。ドライブの準備が完了した後にコンピューターを再起動する必要があることを bdehdcfg に伝えます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a98b76bb-36f1-4790-b337-7dc35f606bc6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 684a6a24fe78c0a23ba954981121c7bd99ac56fb
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718624"
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

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bdehdcfg](bdehdcfg.md)
