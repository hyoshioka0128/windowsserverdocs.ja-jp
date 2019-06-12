---
title: if
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 9751dfe3e0cb0965cc2c5169ea19e0f08110b0ff
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438100"
---
# <a name="if"></a>if



バッチ プログラムでは、条件処理を実行します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
if [not] ERRORLEVEL <Number> <Command> [else <Expression>]
if [not] <String1>==<String2> <Command> [else <Expression>]
if [not] exist <FileName> <Command> [else <Expression>]
```
コマンド拡張機能が有効な場合は、次の構文を使用します。
```
if [/i] <String1> <CompareOp> <String2> <Command> [else <Expression>]
if cmdextversion <Number> <Command> [else <Expression>]
if defined <Variable> <Command> [else <Expression>]
```

## <a name="parameters"></a>パラメーター

|        パラメーター        |                                                                                                                                                                                                                説明                                                                                                                                                                                                                 |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|           非           |                                                                                                                                                                              コマンドの実行には、条件が false の場合にのみを指定します。                                                                                                                                                                              |
|  errorlevel\<番号 >   |                                                                                                                                                      Cmd.exe で実行する前のプログラムには、終了コードが返される以上になる場合にのみ、true の条件を指定します*数*します。                                                                                                                                                       |
|       \<コマンド >        |                                                                                                                                                                            上記の条件を満たした場合に実行する必要がありますのコマンドを指定します。                                                                                                                                                                             |
|  \<String1 > = =<String2>  |                                                                                                             条件が真の場合にのみを指定します*String1*と*String2*は同じです。 これらの値には、リテラル文字列またはバッチの変数 (例: %1) を指定できます。 リテラル文字列を引用符で囲む必要はありません。                                                                                                              |
|    存在\<ファイル名 >    |                                                                                                                                                                                       指定したファイル名が存在する場合は、条件が真を指定します。                                                                                                                                                                                        |
|      \<CompareOp>       |                                                                               3 文字の比較演算子を指定します。 次の一覧が有効な値を表す*CompareOp*:</br>**EQU**と等しい</br>**NEQ**等しくないです。</br>**お近くの LSS**より小さい</br>**LEQ**に等しいまたはそれよりも小さい</br>**GTR**より大きい</br>**GEQ**より大きいまたは等しい                                                                                |
|           /i            |                                                            文字列を小文字を区別しない比較。  使用することができます **/i**上、 <em>String1</em> **==** <em>String2</em>のフォーム**場合**します。 これらの比較では、する場合は、両方*String1*と*String2*桁の数字から成るはのみ、文字列を数値に変換され、数値比較を実行します。                                                            |
| cmdextversion\<番号 > | 条件が真の場合にのみ Cmd.exe の機能と等しいコマンド拡張機能に関連付け、または指定された数値より大きい値の内部バージョン番号を指定します。 最初のバージョンには 1 です。 コマンド拡張機能を大幅に強化が追加されたときに 1 ずつ増加します。 **Cmdextversion** (既定ではコマンド拡張機能が有効になっている) 拡張機能が無効で条件がときにコマンド true ことはありません。 |
|   定義されている\<変数 >   |                                                                                                                                                                                            場合は true。 条件を指定します*変数*が定義されています。                                                                                                                                                                                            |
|      \<式 >      |                                                                                                                                                                   コマンドに渡されるコマンドライン コマンドおよびパラメーターを指定します、**他**句。                                                                                                                                                                   |
|           /?            |                                                                                                                                                                                                    コマンド プロンプトにヘルプを表示します。                                                                                                                                                                                                    |

## <a name="remarks"></a>注釈

-   条件が指定されている場合、**場合**句が true の場合、条件を次のコマンドを実行します。条件が false の場合、コマンドで、**場合**句は無視されで指定されている任意のコマンドを実行するコマンドを**他**句。
-   プログラムが停止したら、終了コードを返します。 終了コードを条件として使用する**errorlevel**します。
-   使用する場合**定義**、次の 3 つの変数が環境に追加されます: **%errorlevel%** 、 **%cmdcmdline**、および **%cmdextversion**.  
    -   **%errorlevel%** ERRORLEVEL 環境変数の現在の値の文字列表現に展開します。 これは ERRORLEVEL という名前の既存の環境変数がないことを前提としています-が発生した場合、ERRORLEVEL 値をそのを代わりに取得されます。
    -   **%cmdcmdline** Cmd.exe で Cmd.exe を処理する前に渡された元のコマンド ラインに展開します。 これは CMDCMDLINE という名前の既存の環境変数がないことを前提としています: 代わりに CMDCMDLINE 値を取得する場合は、します。
    -   **%cmdextversion**の現在の値の文字列形式に展開**cmdextversion**します。 これは CMDEXTVERSION という名前の既存の環境変数がないことを前提としています: 代わりに CMDEXTVERSION 値を取得する場合は、します。
-   使用する必要があります、**他**後にコマンドと同じ行で句、**場合**します。

## <a name="BKMK_examples"></a>例

メッセージを表示するには、"データ ファイルを見つけることができません"ファイル Product.dat が見つからない場合に入力します。
```
if not exist product.dat echo Cannot find data file 
```
A ドライブのディスクをフォーマットして、書式設定プロセス中にエラーが発生した場合、エラー メッセージを表示するには、バッチ ファイルで、次の行を入力します。
```
:begin
@echo off
format a: /s
if not errorlevel 1 goto end
echo An error occurred during formatting.
:end
echo End of batch program.
```
Product.dat ファイルを現在のディレクトリから削除するか、Product.dat が見つからない場合は、メッセージを表示するには、バッチ ファイルで、次の行を入力します。
```
IF EXIST Product.dat (
del Product.dat
) ELSE (
echo The Product.dat file is missing.
)
```

> [!NOTE]
> これらの行は、次のように 1 行に結合できます。
> ```
> IF EXIST Product.dat (del Product.dat) ELSE (echo The Product.dat file is missing.)
> ```
> バッチ ファイルを実行した後、ERRORLEVEL 環境変数の値をエコーするには、バッチ ファイルで、次の行を入力します。
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
> ERRORLEVEL 環境変数の値が 1、型の場合は、「正常」のラベルに移動。
> ```
> if %errorlevel% LEQ 1 goto okay
> ```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)

[もし](if.md)

[goto](goto.md)