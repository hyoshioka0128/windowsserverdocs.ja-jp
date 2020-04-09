---
title: echo
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fb9fcd0f-5e73-4504-aa95-78204e1a79d3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5e6e9c3c79cc8006efba0c97a574e3d6d94a6f7e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80845245"
---
# <a name="echo"></a>echo



メッセージを表示するか、コマンドエコー機能をオンまたはオフにします。 パラメーターを指定せずに使用すると、 **echo**は現在のエコー設定を表示します。

このコマンドを使用する方法の例については、[例](#examples)を参照してください。

## <a name="syntax"></a>構文

```
echo [<Message>]
echo [on | off]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[on \| off]|コマンドエコー機能をオンまたはオフにします。 コマンドのエコーは既定でオンになっています。|
|\<メッセージ >|画面に表示するテキストを指定します。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>コメント

-   Echo **echo** *Message*コマンドは、 **echo**がオフになっている場合に特に役立ちます。 コマンドを何も表示せずに数行のメッセージを表示するには、batch プログラムの**echo off**コマンドの後に複数の**echo** *message*コマンドを含めることができます。
-   **Echo**がオフになっている場合、コマンドプロンプトはコマンドプロンプトウィンドウに表示されません。 コマンドプロンプトを表示するには、「echo on」と入力し**ます。**
-   バッチファイルで使用する場合、 **echo on**と**echo off**は、コマンドプロンプトでの設定には影響しません。
-   バッチファイル内の特定のコマンドがエコーされないようにするには、コマンドの前にアットマーク (@) を挿入します。 バッチファイル内のすべてのコマンドがエコーされないようにするには、ファイルの先頭に**echo off**コマンドを追加します。
-   **Echo**を使用しているときにパイプ ( **|** ) またはリダイレクト文字 ( **<** または **>** ) を表示するには、パイプまたはリダイレクト文字の直前 (たとえば、 **^|** 、 **^>** 、 **^<** ) にカレット (^) を使用します。 キャレットを表示するには、2つのキャレットを連続して入力します ( **^^** )。

## <a name="examples"></a>例

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

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
