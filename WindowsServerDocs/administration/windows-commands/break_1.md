---
title: break
description: Break_1 の Windows コマンドに関するトピックでは、MS-DOS システムの拡張 CTRL + C チェックを設定またはクリアします。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c89b7357-d69e-4141-826e-73c9ba0fc630
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 809a9321b8b4f8b2d201582f767da132076826d4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848365"
---
# <a name="break"></a>break

MS-DOS システムの拡張された CTRL + C チェックを設定または解除します。 パラメーターを指定せずに使用した場合、 **break**は現在の設定を表示します。

> [!NOTE]
> このコマンドは使用されなくなりました。 このコマンドは、既存の MS-DOS ファイルとの互換性を維持する目的でのみ含まれていますが、この機能は自動的に果たされるため、コマンド ラインでは何の効果もありません。

## <a name="syntax"></a>構文

```
break=[on|off]
```

## <a name="remarks"></a>コメント

コマンド拡張機能が有効になっていて、Windows プラットフォームで実行されている場合、 **break**コマンドをバッチファイルに挿入すると、デバッガーによってデバッグされている場合に、ハードコーディングされたブレークポイントが入力されます。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)