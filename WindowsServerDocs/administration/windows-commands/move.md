---
title: move
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fde290a8-d385-450f-8987-ee837fed667d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: efd0cd0716c564a9570647820056ab9c38e41274
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80839375"
---
# <a name="move"></a>move



1つ以上のファイルを1つのディレクトリから別のディレクトリに移動します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
move [{/y | /-y}] [<Source>] [<Target>]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/y|既存の対象ファイルを上書きするかどうかを確認するメッセージを表示しません。|
|/-y|既存の対象ファイルを上書きするかどうかを確認するメッセージが表示されます。|
|\<ソース >|移動するファイルのパスと名前を指定します。 ディレクトリを移動または名前変更する場合、 *Source*は現在のディレクトリのパスと名前にする必要があります。|
|\<ターゲット >|ファイルの移動先のパスと名前を指定します。 ディレクトリの移動または名前変更を行う場合、 *Target*は目的のディレクトリパスと名前にする必要があります。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>コメント

-   **/Y**コマンドラインオプションは、copycmd 環境変数で事前に設定されている場合があります。 これは、コマンドラインで **/-y**を使用してオーバーライドできます。 既定では、バッチスクリプト内から**コピー**コマンドを実行しない限り、ファイルを上書きする前にプロンプトが表示されます。
-   暗号化されたファイルを暗号化ファイルシステム (EFS) をサポートしていないボリュームに移動すると、エラーが発生します。 ファイルを最初に復号化するか、EFS をサポートするボリュームにファイルを移動します。

## <a name="examples"></a><a name=BKMK_examples></a>例

.Xls 拡張子を持つすべてのファイルを \Data ディレクトリから \ Second_Q \Reports ディレクトリに移動するには、次のように入力します。
```
move \data\*.xls \second_q\reports\ 
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)