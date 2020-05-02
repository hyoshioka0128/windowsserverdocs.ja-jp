---
title: extract
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 20dab03e-f6e1-4eb8-b8a1-fd6f1d97ee83
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1cca89a356530e49fbf2b0610ff3ced1c5733847
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725657"
---
# <a name="extract"></a>extract



## <a name="syntax"></a>構文

```
EXTRACT [/Y] [/A] [/D | /E] [/L dir] cabinet [filename ...]
EXTRACT [/Y] source [newname]
EXTRACT [/Y] /C source destination
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|キャビネット|ファイルに2つ以上のファイルが含まれています。|
|filename|キャビネットから抽出するファイルの名前。 ワイルドカードと複数のファイル名 (空白で区切られた) を使用できます。|
|source|圧縮ファイル (1 つのファイルのみを含むキャビネット)。|
|新しい名前|抽出されたファイルを指定する新しいファイル名。 指定されていない場合は、元の名前が使用されます。|
|/A|すべてのキャビネットを処理します。 前述の最初のキャビネットで開始されるキャビネットチェーンに従います。|
|/C|ソースファイルをコピー先にコピーします (DMF ディスクからコピーする場合)。|
|/D|キャビネットディレクトリを表示します (抽出を避けるために、ファイル名を付けて使用します)。|
|/E|Extract (の代わりにを使用*します。* すべてのファイルを抽出する場合)。|
|/L ディレクトリ|抽出されたファイルを配置する場所 (既定は現在のディレクトリ)。|
|/Y|既存のファイルを上書きする前に、メッセージを表示しません。|

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)