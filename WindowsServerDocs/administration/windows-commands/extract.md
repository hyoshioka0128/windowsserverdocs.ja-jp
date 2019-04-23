---
title: 抽出 (extract)
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 9113c34b61b98fb738bc0aff03193ab73b1abbd7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882313"
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
|キャビネット|ファイルには、2 つ以上のファイルが含まれています。|
|&lt;ファイル名&gt;|キャビネットから抽出するファイルの名前。 ワイルドカードと空白で区切って複数のファイル名を使用できます。|
|source|圧縮ファイル (1 つのファイルのキャビネット)。|
|newname|抽出されたファイルを提供する新しいファイル名。 指定しない場合、元の名前が使用されます。|
|/A|すべてのキャビネットを処理します。 以降で説明したように最初のキャビネット キャビネットのチェーンに依存します。|
|/C|ソース ファイルを送信先 (DMF ディスクからコピー) 先にコピーします。|
|/D|キャビネット ディレクトリ (ファイル名に抽出を回避するために使用) を表示します。|
|/E|抽出 (の代わりに使用*します。* すべてのファイルを抽出)。|
|/L dir|(既定値は現在のディレクトリ) 抽出したファイルを配置する場所。|
|/Y|既存のファイルを上書きする前にプロンプトは表示されません。|

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)