---
title: nslookup 指
description: Nslookup finger コマンドの参照記事です。このコマンドは、現在のデバイスの finger サーバーに接続します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 11ea2bde-8ccb-4b87-bbad-231dd9e5e858
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 413dc1a38b4fa7ee7bec28991547b5e0b5ef6fb9
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85934764"
---
# <a name="nslookup-finger"></a>nslookup/finger

現在のデバイスの finger サーバーと接続します。

## <a name="syntax"></a>構文

```
finger [<username>] [{[>] <filename> | [>>] <filename>}]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<username>` | 検索するユーザーの名前を指定します。 |
| `<filename>` | 出力を保存するファイル名を指定します。 より大きい ( `>` ) 文字と2つ以上の文字 () を使用して、 `>>` 通常の方法で出力をリダイレクトできます。 |
| /? | コマンド プロンプトにヘルプを表示します。 |
| /help | コマンド プロンプトにヘルプを表示します。 |

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
