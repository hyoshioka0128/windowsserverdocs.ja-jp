---
title: echo
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fb9fcd0f-5e73-4504-aa95-78204e1a79d3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 343d6327d262401b4be14e472a135062456890f1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377634"
---
# <a name="echo"></a>echo



メッセージを表示するか、コマンドエコー機能をオンまたはオフにします。 パラメーターを指定せずに使用すると、 **echo**は現在のエコー設定を表示します。

このコマンドを使用する方法の例については、[例](#examples)を参照してください。

## <a name="syntax"></a>構文

```
echo [<Message>]
echo [on | off]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[\| off]|コマンドエコー機能をオンまたはオフにします。 コマンドのエコーは既定でオンになっています。|
|\<Message >|画面に表示するテキストを指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>コメント

-   Echo *Message*コマンドは、 **echo**がオフになっている場合に特に役立ちます。 コマンドを何も表示せずに数行のメッセージを表示するには、batch プログラムの**echo off**コマンドの後に複数の**echo** *message*コマンドを含めることができます。
-   **Echo**がオフになっている場合、コマンドプロンプトはコマンドプロンプトウィンドウに表示されません。 コマンドプロンプトを表示するには、「echo on」と入力し**ます。**
-   バッチファイルで使用する場合、 **echo on**と**echo off**は、コマンドプロンプトでの設定には影響しません。
-   バッチファイル内の特定のコマンドがエコーされないようにするには、コマンドの前にアットマーク (@) を挿入します。 バッチファイル内のすべてのコマンドがエコーされないようにするには、ファイルの先頭に**echo off**コマンドを追加します。
-   **Echo**を使用しているときにパイプ ( **|** ) またはリダイレクト文字 ( **<** または **>** ) を表示するには、パイプまたはリダイレクト文字の直前にカレット (^) を使用します (たとえば、 **^|** 、 **0)。** 、または**2**)。 キャレットを表示するには、2つのキャレットを連続して入力します ( **^^** )。

## <a name="examples"></a>使用例

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
> **Echo**がオフになっている場合、コマンドプロンプトはコマンドプロンプトウィンドウに表示されません。 コマンドプロンプトを再度表示するには、「 **echo on**」と入力します。

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

バッチファイルの実行時に .txt ファイルが見つかった場合は、次の出力が表示されます (この例では、File1、File2、および File3 ファイルが存在するものとします)。

```
This directory contains the following text files:
File1.txt
File2.txt
File3.txt
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)
