---
title: move
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 4302a3403f73892500c3f9deb608e9489c7e91ae
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373530"
---
# <a name="move"></a>move



1つ以上のファイルを1つのディレクトリから別のディレクトリに移動します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
move [{/y | /-y}] [<Source>] [<Target>]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/y|既存の対象ファイルを上書きするかどうかを確認するメッセージを表示しません。|
|/-y|既存の対象ファイルを上書きするかどうかを確認するメッセージが表示されます。|
|\<Source >|移動するファイルのパスと名前を指定します。 ディレクトリを移動または名前変更する場合、 *Source*は現在のディレクトリのパスと名前にする必要があります。|
|\<Target >|ファイルの移動先のパスと名前を指定します。 ディレクトリの移動または名前変更を行う場合、 *Target*は目的のディレクトリパスと名前にする必要があります。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>コメント

-   **/Y**コマンドラインオプションは、copycmd 環境変数で事前に設定されている場合があります。 これは、コマンドラインで **/-y**を使用してオーバーライドできます。 既定では、バッチスクリプト内から**コピー**コマンドを実行しない限り、ファイルを上書きする前にプロンプトが表示されます。
-   暗号化されたファイルを暗号化ファイルシステム (EFS) をサポートしていないボリュームに移動すると、エラーが発生します。 ファイルを最初に復号化するか、EFS をサポートするボリュームにファイルを移動します。

## <a name="BKMK_examples"></a>例

.Xls 拡張子を持つすべてのファイルを \Data ディレクトリから \Second_Q\Reports ディレクトリに移動するには、次のように入力します。
```
move \data\*.xls \second_q\reports\ 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)