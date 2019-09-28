---
title: break
description: '**Break_1**の Windows コマンドのトピック-MS-DOS システムの拡張 CTRL + C チェックを設定またはクリアします。 パラメーターを指定せずに使用した場合、 **break**は現在の設定を表示します。 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c89b7357-d69e-4141-826e-73c9ba0fc630
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 73afdac29efbfd9efec88d297cf4185ca1b92d62
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380491"
---
# <a name="break"></a>break



MS-DOS システムの拡張された CTRL + C チェックを設定または解除します。 パラメーターを指定せずに使用した場合、 **break**は現在の設定を表示します。

> [!NOTE]
> このコマンドは使用されなくなりました。 これは、既存の MS-DOS ファイルとの互換性を保持するためだけに備えられていますが、機能は自動で実行されるためコマンド ラインでは無効です。

## <a name="syntax"></a>構文

```
break=[on|off]
```

## <a name="remarks"></a>コメント

コマンド拡張機能が有効になっていて、Windows プラットフォームで実行されている場合、 **break**コマンドをバッチファイルに挿入すると、デバッガーによってデバッグされている場合に、ハードコーディングされたブレークポイントが入力されます。

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)