---
title: forfiles
description: Forfiles コマンドのリファレンス記事。ファイルまたは一連のファイルでコマンドを選択して実行します。
ms.topic: article
ms.assetid: 43f6b004-446d-4fdd-91c5-5653613524a4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 05/20/2020
ms.openlocfilehash: 004c27b841629e18eac4d94f7fe0816b42762107
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87890150"
---
# <a name="forfiles"></a>forfiles

ファイルまたはファイルのセットに対してコマンドを選択して実行します。 このコマンドは、バッチファイルで最もよく使用されます。

## <a name="syntax"></a>構文

```
forfiles [/P pathname] [/M searchmask] [/S] [/C command] [/D [+ | -] [{<date> | <days>}]]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| /P`<pathname>` | 検索の開始位置を示すパスを指定します。 既定では、検索は現在の作業ディレクトリから開始されます。 |
| /M`<searchmask>` | 指定された検索マスクに従ってファイルを検索します。 既定の searchmask は `*` です。 |
| /S | **Forfiles**コマンドに対して、サブディレクトリを再帰的に検索するように指示します。 |
| スイッチ`<command>` | 各ファイルに対して指定されたコマンドを実行します。 コマンド文字列は二重引用符で囲む必要があります。 既定のコマンドは `"cmd /c echo @file"` です。 |
| D`[{+\|-}][{<date> | <days>}]` | 指定された期間内に最後に変更された日付のファイルを選択します:<ul><li>日付 **+** **-** が MM/DD/YYYY の形式で指定された日付 () 以上 () またはそれより前*date* () であるファイルを選択します。</li><li>現在の日付に指定された日数を加算した日付、または現在の日付から指定した日数を引いた値 () までの最終更新日を含むファイルを選択 **+** **-** します。</li><li>*Days*の有効な値には、0 ~ 32768 の範囲の任意の数を指定します。 符号が指定されていない場合、 **+** 既定ではが使用されます。</li></ul> |
| /? | コマンドウィンドウにヘルプテキストを表示します。 |

#### <a name="remarks"></a>Remarks

- `forfiles /S`コマンドはに似てい `dir /S` ます。

- **/C**コマンドラインオプションで指定されているように、コマンド文字列で次の変数を使用できます。

    | 変数 | 説明 |
    | -------- | ----------- |
    | @FILE | ファイル名。 |
    | @FNAME | 拡張子のないファイル名です。 |
    | @EXT | ファイル名の拡張子。 |
    | @PATH | ファイルの完全パス。 |
    | @RELPATH | ファイルの相対パス。 |
    | @ISDIR | ファイルの種類がディレクトリの場合、TRUE に評価されます。 それ以外の場合、この変数は FALSE に評価されます。 |
    | @FSIZE | ファイルサイズ (バイト単位)。 |
    | @FDATE | ファイルで最後に変更された日付スタンプ。 |
    | @FTIME | ファイルの最終更新日時スタンプ。 |

- **Forfiles**コマンドを使用すると、に対してコマンドを実行したり、複数のファイルに引数を渡したりすることができます。 たとえば、.txt というファイル名拡張子を持つツリー内のすべてのファイルに対して**type**コマンドを実行できます。 または、すべてのバッチファイル (* .bat) をドライブ C で実行し、ファイル名を最初の引数として Myinput.txt することもできます。

- このコマンドは、次のことができます。

    - ファイルの絶対日付または相対日付で **/d**パラメーターを使用して選択します。

    - やなどの変数を使用して、ファイルのアーカイブツリーを構築し @FSIZE @FDATE ます。

    - 変数を使用して、ファイルをディレクトリと区別し @ISDIR ます。

    - コマンドラインに特殊文字を含めるには、文字の16進コードを 0x*HH*形式 (たとえば、タブの 0x09) で使用します。

- このコマンドは、 `recurse subdirectories` 1 つのファイルのみを処理するように設計されたツールにフラグを実装することによって機能します。

### <a name="examples"></a>例

C ドライブのすべてのバッチファイルの一覧を表示するには、次のように入力します。

```
forfiles /P c:\ /S /M *.bat /C "cmd /c echo @file is a batch file"
```

C ドライブのすべてのディレクトリの一覧を表示するには、次のように入力します。

```
forfiles /P c:\ /S /M *.* /C "cmd /c if @isdir==TRUE echo @file is a directory"
```

現在のディレクトリにある、少なくとも1年前のすべてのファイルを一覧表示するには、次のように入力します。

```
forfiles /S /M *.* /D -365 /C "cmd /c echo @file is at least one year old."
```

2007年1月1日よりも前のバージョンでは、現在のディレクトリ内の各ファイルのテキスト*ファイル*が古くなっていることを表示するには、次のように入力します。

```
forfiles /S /M *.* /D -01/01/2007 /C "cmd /c echo @file is outdated."
```

現在のディレクトリにあるすべてのファイルのファイル名拡張子を列形式で一覧表示し、拡張子の前にタブを追加するには、次のように入力します。

```
forfiles /S /M *.* /C "cmd /c echo The extension of @file is 0x09@ext"
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
