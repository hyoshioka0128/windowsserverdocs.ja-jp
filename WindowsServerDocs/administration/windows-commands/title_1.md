---
title: title
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0bbe8bd-201a-4b6c-b617-5d9809881dc8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d1d1ea70849c3beb4503edfdaa5116384c14a2fd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848503"
---
# <a name="title"></a>title



コマンド プロンプト ウィンドウのタイトルを作成します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
title [<String>]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<文字列 >|コマンド プロンプト ウィンドウのタイトルを指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

-   バッチ プログラムのウィンドウのタイトルを作成するには、 **タイトル** バッチ ファイルの先頭にあるコマンドです。
-   ウィンドウのタイトルを設定した後のみを使用してリセットできます、 **タイトル** コマンドです。

## <a name="BKMK_examples"></a>例

次のサンプル スクリプトでコマンド プロンプト ウィンドウのタイトルが「更新ファイル」に変更バッチ ファイルを実行しながら、 **コピー** コマンドです。 コマンドを実行した後、テキスト `Files Updated` が表示されたら、コマンド プロンプト ウィンドウのタイトルが「コマンド プロンプト」に変更しました
```
@echo off
title Updating Files
copy \\server\share\*.xls c:\users\common\*.xls
echo Files Updated.
title Command Prompt
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)