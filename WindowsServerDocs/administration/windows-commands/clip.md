---
title: clip
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 85322d85-3376-4806-845b-93ac77fe27bf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 82186869782c47f41930d46b4c33a710e6addedf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379352"
---
# <a name="clip"></a>clip



コマンドの出力をコマンドラインから Windows クリップボードにリダイレクトします。 その後、このテキスト出力を他のプログラムに貼り付けることができます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
<Command> | clip
clip < <FileName>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<Command >|出力を Windows クリップボードに送信するコマンドを指定します。|
|\<ファイル名 >|Windows クリップボードに送信する内容を含むファイルを指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>コメント

**Clip**コマンドを使用すると、クリップボードからテキストを受信できる任意のアプリケーションにデータを直接コピーできます。

## <a name="BKMK_examples"></a>例

現在のディレクトリの一覧を Windows クリップボードにコピーするには、次のように入力します。
```
dir | clip
```
汎用のプログラムの出力を Windows クリップボードにコピーするには、次のように入力します。
```
awk -f generic.awk input.txt | clip
```
Readme.txt という名前のファイルの内容を Windows クリップボードにコピーするには、次のように入力します。
```
clip < readme.txt
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)