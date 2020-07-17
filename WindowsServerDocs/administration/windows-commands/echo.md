---
title: echo
description: Echo コマンドの参照記事。メッセージを表示したり、コマンドエコー機能をオンまたはオフにしたりします。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fb9fcd0f-5e73-4504-aa95-78204e1a79d3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bc463efef38e07c1ce8b9ebee1ddd7bdfd7d3066
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85930526"
---
# <a name="echo"></a>echo

メッセージを表示するか、コマンドエコー機能をオンまたはオフにします。 パラメーターを指定せずに使用すると、 **echo**は現在のエコー設定を表示します。

## <a name="syntax"></a>構文

```
echo [<message>]
echo [on | off]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| [オン \| オフ] | コマンドエコー機能をオンまたはオフにします。 コマンドのエコーは既定でオンになっています。 |
| `<message>` | 画面に表示するテキストを指定します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>注釈

- コマンドは、 `echo <message>` **echo**がオフになっている場合に特に便利です。 コマンドを何も表示せずに、数行のメッセージを表示するには、 `echo <message>` batch プログラムの**echo off**コマンドの後にいくつかのコマンドを含めることができます。

- **エコー**をオフにすると、コマンドプロンプトウィンドウにコマンドプロンプトは表示されません。 コマンドプロンプトを表示するには、「echo on」と入力し**ます。**

- バッチファイルで使用する場合、 **echo on**と**echo off**は、コマンドプロンプトでの設定には影響しません。

- バッチファイル内の特定のコマンドがエコーされないようにするには、 `@` コマンドの前にサインインを挿入します。 バッチファイル内のすべてのコマンドがエコーされないようにするには、ファイルの先頭に**echo off**コマンドを追加します。

- `|`Echo を使用しているときにパイプ () またはリダイレクト文字 (または) を表示するには、 `<` `>` **echo** `^` パイプまたはリダイレクト文字の直前にカレット () を使用します。 たとえば、、 `^|` 、など) を使用 `^>` `^<` します。 キャレットを表示するには、2つのキャレットを連続して入力し `^^` ます ()。

### <a name="examples"></a>例

現在の**エコー**設定を表示するには、次のように入力します。

```
echo
```

画面上の空白行をエコーするには、次のように入力します。

```
echo.
```

> [!NOTE]
> ピリオドの前にスペースを入れないでください。 それ以外の場合は、空白行ではなくピリオドが表示されます。

コマンドプロンプトでコマンドがエコーされないようにするには、次のように入力します。

```
echo off
```

> [!NOTE]
> **Echo**がオフになっていると、コマンドプロンプトウィンドウにコマンドプロンプトは表示されません。 コマンドプロンプトを再度表示するには、「 **echo on**」と入力します。

バッチファイル内のすべてのコマンド ( **echo off**コマンドを含む) が画面に表示されないようにするには、バッチファイルの1行目で次のように入力します。

```
@echo off
```

**Echo**コマンドは、 **if**ステートメントの一部として使用できます。 たとえば、現在のディレクトリで、ファイル名拡張子が rpt のファイルを検索し、そのようなファイルが見つかった場合はメッセージをエコーするには、次のように入力します。

```
if exist *.rpt echo The report has arrived.
```

次のバッチファイルでは、現在のディレクトリで .txt というファイル名拡張子を持つファイルを検索し、検索結果を示すメッセージを表示します。

```
@echo off
if not exist *.txt (
echo This directory contains no text files.
) else (
   echo This directory contains the following text files:
   echo.
   dir /b *.txt
   )
```

バッチファイルの実行時に .txt ファイルが見つからない場合は、次のメッセージが表示されます。

```
This directory contains no text files.
```

バッチファイルの実行時に .txt ファイルが見つかった場合は、次の出力が表示されます (この例では、File1.txt、File2.txt、File3.txt 存在するファイル)。

```
This directory contains the following text files:
File1.txt
File2.txt
File3.txt
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
