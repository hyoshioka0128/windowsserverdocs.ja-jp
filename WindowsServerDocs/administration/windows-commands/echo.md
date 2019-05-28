---
title: echo
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: eb5c9650b95703f1316e6f5f179b910d22574f68
ms.sourcegitcommit: 8ba2c4de3bafa487a46c13c40e4a488bf95b6c33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/25/2019
ms.locfileid: "66222965"
---
# <a name="echo"></a>echo



メッセージが表示されます。 またはオンまたはオフ コマンド機能をエコーします。 パラメーターを指定せずに使用されている場合**エコー**エコーの現在の設定を表示します。

このコマンドを使用する方法の例については、[例](#examples)を参照してください。

## <a name="syntax"></a>構文

```
echo [<Message>]
echo [on | off]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[\|オフ]|またはエコー機能のコマンドは、オフに切り替えます。 既定ではコマンドのエコーです。|
|\<メッセージ >|画面に表示されるテキストを指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

-   **エコー** *メッセージ*コマンドは特に便利な場合に**エコー**は無効になります。 複数の行であるメッセージを表示する任意のコマンドを表示せずに長いすることができますがいくつかあります**エコー** *メッセージ*コマンドの後に、**オフ エコー**コマンド、バッチ プログラム。
-   ときに**エコー**無効になって、コマンド プロンプト ウィンドウで、コマンド プロンプトが表示されません。 コマンド プロンプトを表示するには、次のように入力します。**にエコーします。**
-   バッチ ファイルで使用する場合**エコー**と**オフ エコー**コマンド プロンプトで、設定には影響しません。
-   バッチ ファイルで特定のコマンドをエコーを防ぐためには、挿入、アット マーク (@)、コマンドの前にします。 を、バッチ ファイル内のすべてのコマンドをエコーしない場合、**オフ エコー**ファイルの先頭にあるコマンド。
-   パイプを表示する ( **|** ) またはリダイレクト文字 (**<** または**>**) を使用する場合**エコー**、パイプまたはリダイレクト文字の直前にキャレット (^) を使用して (たとえば、 **^|**、 **^>**、または **^<** ). カレットを表示するには、連続して 2 つのキャレットを入力 ( **^^** )。

## <a name="examples"></a>例

現在の表示を**エコー**入力を設定する。
```
echo
```
画面上の空白行をエコーするには、次のように入力します。
```
echo.
```

> [!NOTE]
> ピリオドの前にスペースを含めないでください。 それ以外の場合、空白行ではなく、期間が表示されます。

防ぐために、コマンド プロンプトでコマンドをエコーするには、入力します。
```
echo off 
```

> [!NOTE]
> ときに**エコー**無効になって、コマンド プロンプト ウィンドウで、コマンド プロンプトが表示されません。 コマンド プロンプトをもう一度表示するには、入力**エコー**します。

バッチ ファイル内のすべてのコマンドを防ぐために (など、**オフ エコー**コマンド) からバッチ ファイルの種類の最初の行で、画面に表示します。
```
@echo off
```
使用することができます、**エコー**コマンドの一部として、**場合**ステートメント。 たとえば、このようなファイルが見つからない場合は、.rpt のファイル名拡張子およびエコー メッセージに任意のファイルの現在のディレクトリを検索するに次のように入力します。
```
if exist *.rpt echo The report has arrived.
```
次のバッチ ファイルは、.txt ファイル名拡張子を持つファイルの現在のディレクトリを検索し、検索の結果を示すメッセージが表示されます。
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
.Txt ファイルが見つからない場合、バッチ ファイルを実行すると、次のメッセージが表示されます。
```
This directory contains no text files.
```
バッチ ファイルの実行時の .txt ファイルが見つかった場合、次の出力が表示されます (この例では、ファイル File1.txt、File2.txt、File3.txt の存在を想定しています)。
```
This directory contains the following text files:
File1.txt
File2.txt
File3.txt
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)
