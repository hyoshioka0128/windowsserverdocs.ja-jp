---
title: title
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 42094e0f1231fee5ac9ef0ec9184ba685c8846b1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385786"
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
|\<String >|コマンド プロンプト ウィンドウのタイトルを指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>コメント

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

[コマンド ライン構文の記号](command-line-syntax-key.md)