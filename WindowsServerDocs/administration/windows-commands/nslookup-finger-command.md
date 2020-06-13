---
title: nslookup 指
description: Nslookup finger コマンドのリファレンストピックです。このコマンドは、現在のデバイスの finger サーバーに接続します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 11ea2bde-8ccb-4b87-bbad-231dd9e5e858
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6341e7297ea661fd9afd4f4b0bb5048d82099b94
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721495"
---
# <a name="nslookup-finger"></a>nslookup/finger

現在のデバイスの finger サーバーと接続します。

## <a name="syntax"></a>構文

```
finger [<username>] [{[>] <filename> | [>>] <filename>}]
```

### <a name="parameters"></a>パラメーター

| パラメーター | Description |
| --------- | ----------- |
| `<username>` | 検索するユーザーの名前を指定します。 |
| `<filename>` | 出力を保存するファイル名を指定します。 より大きい ( `>` ) 文字と2つ以上の文字 () を使用して、 `>>` 通常の方法で出力をリダイレクトできます。 |
| /? | コマンド プロンプトにヘルプを表示します。 |
| /help | コマンド プロンプトにヘルプを表示します。 |

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
