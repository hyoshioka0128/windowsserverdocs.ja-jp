---
title: extract
description: 抽出コマンドの参照記事。ソースの場所からファイルを抽出します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 20dab03e-f6e1-4eb8-b8a1-fd6f1d97ee83
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1de26d444f8c8fdc838fc2fe0c662afefe8c172c
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932378"
---
# <a name="extract"></a>extract

キャビネットまたはソースからファイルを抽出します。

## <a name="syntax"></a>構文

```
extract [/y] [/a] [/d | /e] [/l dir] cabinet [filename ...]
extract [/y] source [newname]
extract [/y] /c source destination
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| キャビネット | 2つ以上のファイルを抽出する場合は、を使用します。 |
| filename | キャビネットから抽出するファイルの名前。 ワイルドカードと複数のファイル名 (空白で区切られた) を使用できます。 |
| source | 圧縮ファイル (1 つのファイルのみを含むキャビネット)。 |
| 新しい名前 | 抽出されたファイルを指定する新しいファイル名。 指定されていない場合は、元の名前が使用されます。 |
| /a | すべてのキャビネットを処理します。 前述の最初のキャビネットで開始されるキャビネットチェーンに従います。 |
| /c | ソースファイルをコピー先にコピーします (DMF ディスクからコピーする場合)。 |
| /d | キャビネットディレクトリを表示します (抽出を避けるために、ファイル名を付けて使用します)。 |
| /e | Extract (の代わりにを使用*します。* すべてのファイルを抽出する場合)。 |
| /l ディレクトリ | 抽出されたファイルを配置する場所 (既定は現在のディレクトリ)。 |
| /y | 既存のファイルを上書きする前にメッセージを表示しません。 |

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
