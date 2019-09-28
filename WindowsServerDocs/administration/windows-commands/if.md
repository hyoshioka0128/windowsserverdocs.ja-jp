---
title: if
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 698b3fb9-532b-4c2b-af7f-179f8dc57131
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fd7857251b0b6a943f2eea33f56732ec57e7e8d1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375481"
---
# <a name="if"></a>if



バッチプログラムで条件付き処理を実行します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
if [not] ERRORLEVEL <Number> <Command> [else <Expression>]
if [not] <String1>==<String2> <Command> [else <Expression>]
if [not] exist <FileName> <Command> [else <Expression>]
```
コマンド拡張機能が有効になっている場合は、次の構文を使用します。
```
if [/i] <String1> <CompareOp> <String2> <Command> [else <Expression>]
if cmdextversion <Number> <Command> [else <Expression>]
if defined <Variable> <Command> [else <Expression>]
```

## <a name="parameters"></a>パラメーター

|        パラメーター        |                                                                                                                                                                                                                説明                                                                                                                                                                                                                 |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|           非           |                                                                                                                                                                              条件が false の場合にのみコマンドを実行するように指定します。                                                                                                                                                                              |
|  errorlevel \<Number >   |                                                                                                                                                      Cmd.exe によって実行された前のプログラムが、 *Number*以上の終了コードを返した場合にのみ、true 条件を指定します。                                                                                                                                                       |
|       \<Command >        |                                                                                                                                                                            前の条件が満たされた場合に実行するコマンドを指定します。                                                                                                                                                                             |
|  \<String1 > = = <String2>  |                                                                                                             *String1*と*String2*が同じ場合にのみ true 条件を指定します。 これらの値には、リテラル文字列またはバッチ変数 (% 1 など) を指定できます。 リテラル文字列を引用符で囲む必要はありません。                                                                                                              |
|    存在 \<FileName >    |                                                                                                                                                                                       指定されたファイル名が存在する場合に true 条件を指定します。                                                                                                                                                                                        |
|      \<CompareOp >       |                                                                               3文字の比較演算子を指定します。 次の一覧は、 *Compareop*の有効な値を示しています。</br>**等しい**等しい</br>**Neq**等しくない</br>**Lss**より小さい</br>**Leq**以下</br>**Gtr**より大きい</br>**Geq**以上                                                                                |
|           /i            |                                                            大文字小文字を無視するように文字列比較を強制します。  **If**の<em>String1</em> **==** <em>String2</em>形式の **/i**を使用できます。 これらの比較は一般に、 *String1*と*String2*の両方が数字のみで構成されている場合、文字列は数値に変換され、数値比較が実行されます。                                                            |
| cmdextversion \<Number > | Cmd.exe のコマンド拡張機能に関連付けられている内部バージョン番号が、指定された数以上である場合にのみ、true 条件を指定します。 最初のバージョンは1です。 コマンド拡張機能に大幅な拡張が追加されると、1つずつ増加します。 コマンド拡張機能が無効になっている場合 (既定では、コマンド拡張機能が有効になっている場合)、 **cmdextversion**条件は満たされません。 |
|   定義済みの \<Variable >   |                                                                                                                                                                                            *変数*が定義されている場合に true 条件を指定します。                                                                                                                                                                                            |
|      \<Expression >      |                                                                                                                                                                   コマンドラインコマンドと、 **else**句でコマンドに渡すパラメーターを指定します。                                                                                                                                                                   |
|           /?            |                                                                                                                                                                                                    コマンド プロンプトにヘルプを表示します。                                                                                                                                                                                                    |

## <a name="remarks"></a>コメント

-   **If**句に指定された条件が true の場合、条件に従ったコマンドが実行されます。条件が false の場合、 **if**句のコマンドは無視され、コマンドは**else**句で指定されているすべてのコマンドを実行します。
-   プログラムが停止すると、終了コードが返されます。 終了コードを条件として使用するには、 **errorlevel**を使用します。
-   を**定義**した場合、次の3つの変数が環境に追加されます: **% errorlevel%** 、 **% cmdcmdline%** 、および **% cmdextversion%** 。  
    -   **% errorlevel%** は、errorlevel 環境変数の現在の値の文字列形式に展開されます。 これは、ERRORLEVEL という名前の既存の環境変数が存在しないことを前提としています。存在する場合は、代わりに ERRORLEVEL 値が取得されます。
    -   **% cmdcmdline%** は、cmd.exe によって処理される前に cmd.exe に渡された元のコマンドラインに展開されます。 これは、CMDCMDLINE という名前の既存の環境変数が存在しないことを前提としています。存在する場合は、代わりに CMDCMDLINE 値が取得されます。
    -   **% cmdextversion%** は、 **cmdextversion**の現在の値の文字列形式に展開されます。 これは、CMDEXTVERSION という名前の既存の環境変数が存在しないことを前提としています。存在する場合は、代わりに CMDEXTVERSION の値が取得されます。
-   **If**の後のコマンドと同じ行で**else**句を使用する必要があります。

## <a name="BKMK_examples"></a>例

ファイルの製品が見つからない場合に "データファイルが見つかりません" というメッセージを表示するには、次のように入力します。
```
if not exist product.dat echo Cannot find data file 
```
フォーマット処理中にエラーが発生した場合に、ドライブ A のディスクをフォーマットし、エラーメッセージを表示するには、次の行をバッチファイルに入力します。
```
:begin
@echo off
format a: /s
if not errorlevel 1 goto end
echo An error occurred during formatting.
:end
echo End of batch program.
```
現在のディレクトリからファイルの製品 .dat を削除するか、または製品 .dat が見つからない場合はメッセージを表示するには、バッチファイルに次の行を入力します。
```
IF EXIST Product.dat (
del Product.dat
) ELSE (
echo The Product.dat file is missing.
)
```

> [!NOTE]
> これらの行は、次のように1つの行に結合できます。
> ```
> IF EXIST Product.dat (del Product.dat) ELSE (echo The Product.dat file is missing.)
> ```
> バッチファイルを実行した後に ERRORLEVEL 環境変数の値をエコーするには、バッチファイルに次の行を入力します。
> ```
> goto answer%errorlevel%
> :answer1
> echo Program had return code 1
> :answer0
> echo Program had return code 0
> goto end
> :end
> echo Done! 
> ```
> ERRORLEVEL 環境変数の値が1以下の場合、"ok" というラベルにジャンプするには、次のように入力します。
> ```
> if %errorlevel% LEQ 1 goto okay
> ```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)

[もし](if.md)

[へ](goto.md)