---
title: choice
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c65a9119-410b-4dcf-9fa7-4e07d2a7238b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e710b3813525647053365ebf4c764181fc38b3f6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379371"
---
# <a name="choice"></a>choice



バッチプログラムに含まれる1文字の選択肢の一覧から1つの項目を選択するようにユーザーに要求し、選択した選択項目のインデックスを返します。 パラメーターを指定せずに使用した場合、**選択肢**に**Y**と**N**の既定の選択肢が表示されます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
choice [/c [<Choice1><Choice2><…>]] [/n] [/cs] [/t <Timeout> /d <Choice>] [/m <"Text">]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/c \<Choice1 > <Choice2> <...>|作成する選択肢の一覧を指定します。 有効な選択肢は、a-z、a-z、0-9、および拡張 ASCII 文字 (128-254) です。 既定の一覧は "YN" で、`[Y,N]?` として表示されます。|
|/n|選択項目の一覧を非表示にします。選択肢は引き続き有効であり、( **/m**で指定されている場合) メッセージテキストが引き続き表示されます。|
|/cs|選択肢で大文字と小文字を区別することを指定します。 既定では、選択肢の大文字と小文字は区別されません。|
|/t \<Timeout >|**/D**によって指定された既定の選択を使用する前に、一時停止する秒数を指定します。 使用可能な値は**0** ~ **9999**です。 **/T**が**0**に設定されている場合、 **choice**は、既定の選択を返す前に一時停止しません。|
|/d \<Choice >|**/T**によって指定された秒数を待機した後に使用する既定のオプションを指定します。 既定の選択肢は、 **/c**によって指定された選択肢の一覧に含まれている必要があります。|
|/m < "Text" >|選択肢の一覧の前に表示するメッセージを指定します。 **/M**が指定されていない場合は、choice プロンプトだけが表示されます。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>コメント

-   ERRORLEVEL 環境変数は、ユーザーが選択肢の一覧から選択するキーのインデックスに設定されます。 一覧の最初の選択肢は、1、2番目の値が2のようになります。 ユーザーが無効なキーを押すと、警告ビープ音が**鳴ります**。 **Choice**がエラー状態を検出した場合は、ERRORLEVEL 値255を返します。 ユーザーが CTRL + BREAK キーまたは CTRL + C キーを押すと、ERRORLEVEL 値 0**が返され**ます。

> [!NOTE]
> バッチプログラムで ERRORLEVEL 値を使用する場合は、それらを降順に一覧表示します。

## <a name="BKMK_examples"></a>例

Y、N、C の選択肢を表示するには、バッチファイルに次の行を入力します。
```
choice /c ync
```
バッチファイルで**choice**コマンドを実行すると、次のプロンプトが表示されます。
```
[Y,N,C]?
```
Y、N、C の選択肢を非表示にしても、"Yes, No, or Continue" というテキストが表示されるようにするには、バッチファイルに次の行を入力します。
```
choice /c ync /n /m "Yes, No, or Continue?"
```
バッチファイルで**choice**コマンドを実行すると、次のプロンプトが表示されます。
```
Yes, No, or Continue?
```

> [!NOTE]
> **/N**パラメーターを使用していても、 **/m**を使用しない場合、ユーザーは**選択**が入力を待機しているときにプロンプトが表示されません。

前の例で使用したテキストとオプションの両方を表示するには、バッチファイルに次の行を入力します。
```
choice /c ync /m "Yes, No, or Continue"
```
バッチファイルで**choice**コマンドを実行すると、次のプロンプトが表示されます。
```
Yes, No, or Continue [Y,N,C]?
```
5秒の制限時間を設定し、既定値として**N**を指定するには、バッチファイルに次の行を入力します。
```
choice /c ync /t 5 /d n
```
バッチファイルで**choice**コマンドを実行すると、次のプロンプトが表示されます。
```
[Y,N,C]?
```

> [!NOTE]
> この例では、ユーザーが5秒以内にキーを押していない場合、 **choice**は既定で**N**を選択し、エラー値2を返します。 それ以外の場合、 **choice**はユーザーの選択に対応する値を返します。

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)