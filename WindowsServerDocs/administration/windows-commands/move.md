---
title: move
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fde290a8-d385-450f-8987-ee837fed667d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d651e586c31ff64664079bdd10ffde3701ec317d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824993"
---
# <a name="move"></a>move



1 つまたは複数のファイルを 1 つのディレクトリから別のディレクトリに移動します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
move [{/y | /-y}] [<Source>] [<Target>]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/y|既存の変換先ファイルを上書きすることを確認するプロンプトを表示しません。|
|/y|既存の変換先ファイルを上書きすることを確認するメッセージを表示します。|
|\<ソース >|ファイルまたは移動するファイルの名前とパスを指定します。 移動またはディレクトリの名前を変更する場合*ソース*現在のディレクトリ パスと名前にする必要があります。|
|\<ターゲット >|ファイルの移動先の名前とパスを指定します。 移動またはディレクトリの名前を変更する場合*ターゲット*目的のディレクトリ パスと名前にする必要があります。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

-   **/Y**コマンド ライン オプションは、/z で事前に設定されている可能性があります。 これをオーバーライドすることができます **/y**コマンドラインでします。 既定ではない限り、ファイルを上書きする前に、**コピー**バッチ スクリプトからコマンドを実行します。
-   エラーの結果の暗号化ファイル システム (EFS) をサポートしていないボリュームに暗号化されたファイルを移動します。 最初のファイルを復号化か、ファイルを EFS をサポートするボリュームに移動します。

## <a name="BKMK_examples"></a>例

拡張子 .xls を持つすべてのファイルを \Data ディレクトリから \Second_Q\Reports ディレクトリに移動するに次のように入力します。
```
move \data\*.xls \second_q\reports\ 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)