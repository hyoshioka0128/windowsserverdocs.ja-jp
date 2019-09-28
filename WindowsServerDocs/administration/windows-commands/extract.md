---
title: 抽出 (extract)
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 20dab03e-f6e1-4eb8-b8a1-fd6f1d97ee83
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 967f08e271019cc33970419179c9ddbf902b1882
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377263"
---
# <a name="extract"></a>抽出 (extract)



## <a name="syntax"></a>構文

```
EXTRACT [/Y] [/A] [/D | /E] [/L dir] cabinet [filename ...]
EXTRACT [/Y] source [newname]
EXTRACT [/Y] /C source destination
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|キャビネット|ファイルに2つ以上のファイルが含まれています。|
|&lt;ファイル名&gt;|キャビネットから抽出するファイルの名前。 ワイルドカードと複数のファイル名 (空白で区切られた) を使用できます。|
|source|圧縮ファイル (1 つのファイルのみを含むキャビネット)。|
|newname|抽出されたファイルを指定する新しいファイル名。 指定されていない場合は、元の名前が使用されます。|
|/A|すべてのキャビネットを処理します。 前述の最初のキャビネットで開始されるキャビネットチェーンに従います。|
|/C|ソースファイルをコピー先にコピーします (DMF ディスクからコピーする場合)。|
|D|キャビネットディレクトリを表示します (抽出を避けるために、ファイル名を付けて使用します)。|
|/E|Extract (の代わりにを使用*します。* すべてのファイルを抽出する場合)。|
|/L ディレクトリ|抽出されたファイルを配置する場所 (既定は現在のディレクトリ)。|
|/Y|既存のファイルを上書きする前に、メッセージを表示しません。|

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)