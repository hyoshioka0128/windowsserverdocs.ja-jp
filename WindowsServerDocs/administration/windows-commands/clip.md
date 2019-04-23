---
title: clip
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: b10876e115c1f0dcac3448948003852449012087
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862393"
---
# <a name="clip"></a>clip



Windows クリップボードにコマンドラインからコマンドの出力をリダイレクトします。 このテキスト出力は、他のプログラムに貼り付けることができます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
<Command> | clip
clip < <FileName>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<コマンド >|コマンドを Windows クリップボードに送信する出力を指定します。|
|\<FileName>|ファイルを Windows クリップボードに送信する内容を指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

使用することができます、**クリップ**コマンドをクリップボードからテキストを受信できる任意のアプリケーションに直接データをコピーします。

## <a name="BKMK_examples"></a>例

Windows クリップボードに一覧表示、現在のディレクトリをコピーするには、次のように入力します。
```
dir | clip
```
Windows クリップボードに Generic.awk と呼ばれるプログラムの出力をコピーするには、次のように入力します。
```
awk -f generic.awk input.txt | clip
```
Windows クリップボードに Readme.txt をという名前のファイルの内容をコピーするには、次のように入力します。
```
clip < readme.txt
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)