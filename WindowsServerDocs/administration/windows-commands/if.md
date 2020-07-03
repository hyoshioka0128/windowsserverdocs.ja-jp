---
title: if
description: If コマンドのリファレンス記事。バッチプログラムで条件付き処理を実行します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 698b3fb9-532b-4c2b-af7f-179f8dc57131
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dd55ebb6ae3562906efdc710f7a067a7e7514e59
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85924474"
---
# <a name="if"></a>if

バッチプログラムで条件付き処理を実行します。

## <a name="syntax"></a>Syntax

```
if [not] ERRORLEVEL <number> <command> [else <expression>]
if [not] <string1>==<string2> <command> [else <expression>]
if [not] exist <filename> <command> [else <expression>]
```

コマンド拡張機能が有効になっている場合は、次の構文を使用します。

```
if [/i] <string1> <compareop> <string2> <command> [else <expression>]
if cmdextversion <number> <command> [else <expression>]
if defined <variable> <command> [else <expression>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- |------------ |
| not | 条件が false の場合にのみコマンドを実行するように指定します。 |
| errorlevel`<number>` | Cmd.exe によって実行された前回のプログラムが、 *number*以上の終了コードを返した場合にのみ、true の条件を指定します。 |
| `<command>` | 前の条件が満たされた場合に実行するコマンドを指定します。 |
| `<string1>==<string2>` | *String1*と*string2*が同じ場合にのみ true 条件を指定します。 これらの値には、リテラル文字列またはバッチ変数 (など) を指定でき `%1` ます。 リテラル文字列を引用符で囲む必要はありません。 |
| まだ`<filename>` | 指定されたファイル名が存在する場合に true 条件を指定します。 |
| `<compareop>` | 次のように、3文字の比較演算子を指定します。<ul><li>**等しい**-Equal to</li><li>**Neq** -等しくない</li><li>**Lss** -より小さい</li><li>**Leq** -以下</li><li>**Gtr** -より大きい</li><li>**Geq** -以上</li></ul> |
| /i | 大文字小文字を無視するように文字列比較を強制します。 **/I**は、 `string1==string2` **if**の形式で使用できます。 これらの比較は一般に、 *string1*と*string2*の両方が数字のみで構成されている場合、文字列は数値に変換され、数値比較が実行されます。 |
| cmdextversion`<number>` | Cmd.exe のコマンド拡張機能に関連付けられている内部バージョン番号が指定した数以上の場合にのみ、true 条件を指定します。 最初のバージョンは1です。 コマンド拡張機能に大幅な拡張が追加されると、1つずつ増加します。 コマンド拡張機能が無効になっている場合 (既定では、コマンド拡張機能が有効になっている場合)、 **cmdextversion**条件は満たされません。 |
| defined `<variable>` | *変数*が定義されている場合に true 条件を指定します。 |
| `<expression>` | コマンドラインコマンドと、 **else**句でコマンドに渡すパラメーターを指定します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>注釈

- **If**句に指定された条件が true の場合、条件に従ったコマンドが実行されます。条件が false の場合、 **if**句のコマンドは無視され、コマンドは**else**句で指定されているすべてのコマンドを実行します。

- プログラムが停止すると、終了コードが返されます。 終了コードを条件として使用するには、 **errorlevel**パラメーターを使用します。

- を**定義**した場合、次の3つの変数が環境に追加されます: **% errorlevel%**、 **% cmdcmdline%**、および **% cmdextversion%**。

  - **% errorlevel%**: errorlevel 環境変数の現在の値の文字列形式に展開されます。 この変数は、ERRORLEVEL という名前の既存の環境変数が存在しないことを前提としています。 存在する場合は、代わりに ERRORLEVEL 値を取得します。

  - **% cmdcmdline%**: Cmd.exe によって処理される前に Cmd.exe に渡された元のコマンドラインに展開されます。 これは、CMDCMDLINE という名前の既存の環境変数が存在しないことを前提としています。 存在する場合は、代わりに CMDCMDLINE 値を取得します。

  - **% cmdextversion%**: **cmdextversion**の現在の値の文字列形式に展開されます。 これは、CMDEXTVERSION という名前の既存の環境変数が存在しないことを前提としています。 存在する場合は、代わりに CMDEXTVERSION の値を取得します。

- **If**の後のコマンドと同じ行で**else**句を使用する必要があります。

### <a name="examples"></a>例

**ファイルの製品が見つからない場合、"データファイルが見つかりません**" というメッセージが表示されるようにするには、次のように入力します。

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

バッチファイルを実行した後に ERRORLEVEL 環境変数の値をエコーするには、バッチファイルに次の行を入力します。

```
goto answer%errorlevel%
:answer1
echo The program returned error level 1
goto end
:answer0
echo The program returned error level 0
goto end
:end
echo Done!
```

ERRORLEVEL 環境変数の値が1以下の場合は、[ok] を指定すると、次のように入力します。

```
if %errorlevel% LEQ 1 goto okay
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [goto コマンド](goto.md)
