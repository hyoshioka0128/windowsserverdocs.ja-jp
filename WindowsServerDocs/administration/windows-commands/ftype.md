---
title: ftype
description: ファイル名拡張子の関連付けで使用されるファイルの種類を表示または変更する、ftype コマンドの参照記事です。
ms.topic: article
ms.assetid: 6fb53cee-9bed-44dd-af5d-bc7cec1dd114
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ed4a8a698328737259f830118fa9c6a482247884
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87888715"
---
# <a name="ftype"></a>ftype

表示またはファイル名拡張子の関連付けで使用されているファイルの種類を変更します。 代入演算子 (=) を指定せずに使用した場合、このコマンドは、指定されたファイルの種類について現在開いているコマンド文字列を表示します。 パラメーターを指定せずに使用した場合、このコマンドは、開いているコマンド文字列が定義されているファイルの種類を表示します。

> [!NOTE]
> このコマンドは cmd.exe 内でのみサポートされており、PowerShell からは使用できません。
> ただし、を `cmd /c ftype` 回避策として使用することもできます。

## <a name="syntax"></a>構文

```
ftype [<filetype>[=[<opencommandstring>]]]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<filetype>` | 表示または変更するファイルの種類を指定します。 |
| `<opencommandstring>` | 指定したファイルの種類のファイルを開くときに使用する開いているコマンド文字列を指定します。|
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>Remarks

次の表方法 **ftype** [開く] コマンド文字列内の変数に置換します。

| 変数 | 置換値 |
| -------- | ----------------- |
| `%0` または `%1` | アソシエーションを起動して、ファイル名と置き換えを取得します。 |
| `%*` | すべてのパラメーターを取得します。 |
| `%2`, `%3`, ... | 最初のパラメーター ( `%2` )、2番目のパラメーター () などを取得し `%3` ます。 |
| `%~<n>` | *N*番目のパラメーターで始まる残りのすべてのパラメーターを取得します。 *n*には、2 ~ 9 の任意の数を指定できます。 |

### <a name="examples"></a>例

開いているコマンド文字列が定義されている現在のファイルの種類を表示するには、次のように入力します。

```
ftype
```

現在開いているコマンド文字列を表示する、 *txtfile* ファイルの種類、種類。

```
ftype txtfile
```

次のような出力が表示されます。

`txtfile=%SystemRoot%\system32\NOTEPAD.EXE %1`

" *Example*" という名前のファイルの種類について開いているコマンド文字列を削除するには、次のように入力します。

```
ftype example=
```

.Pl ファイル名拡張子を PerlScript ファイルの種類に関連付け、PERL を実行する PerlScript ファイルの種類を有効にします。実行可能ファイルで、次のコマンドを入力します。

```
assoc .pl=PerlScript
ftype PerlScript=perl.exe %1 %*
```

Perl スクリプトを呼び出すときに、.pl のファイル名拡張子を入力する必要をなくすためには、次のように入力します。

```
set PATHEXT=.pl;%PATHEXT%
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
