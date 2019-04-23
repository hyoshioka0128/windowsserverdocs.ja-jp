---
title: goto
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e0de1458-1f78-48ff-a746-c285a945a510
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f1ad0190519d58bd879ae391f378d800760c204f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857533"
---
# <a name="goto"></a>goto



バッチ プログラムでは、ラベル付きの行に cmd.exe を指示します。 バッチ プログラム内で**goto**ラベルで識別される行にコマンドの処理に指示します。 ラベルが見つかると、次の行で始まるコマンドを使用してから処理を続行します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
goto <Label> 
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ラベル >|バッチ プログラムでは、ラベルとして使用されるテキスト文字列を指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

-   コマンド拡張機能の使用

    コマンド拡張機能がある場合 (既定値) を有効になっており、使用する、 **goto**コマンドの先のラベルと **: EOF**、現在のバッチ スクリプト ファイルの末尾に制御を転送して、バッチ スクリプト ファイルの終了なし、ラベルを定義します。 使用すると**goto**で、 **: EOF**ラベル、ラベルの前にコロンを挿入する必要があります。 例:  
    ```
    goto:EOF
    ```  
-   有効なを使用して*ラベル*値

    内のスペースを使用することができます、*ラベル*パラメーターが他の区切り記号 (セミコロンや等号など) を含めることはできません。
-   一致する*ラベル*バッチ プログラムでラベルを持つ

    *ラベル*を指定する値はバッチ プログラムでは、ラベルと一致する必要があります。 バッチ プログラム内のラベルは、コロン (:) で始める必要があります。 行は、コロンで始まっている場合は、ラベルとして扱われ、その行のコマンドは無視されます。 バッチ プログラムがで指定したラベルを含まないかどうか*ラベル*、バッチ プログラムは停止し、次のメッセージが表示されます。  
    ```
    Label not found
    ```  
-   使用して**goto**の条件付きの操作

    使用することができます**goto**条件付き操作を実行するには、その他のコマンドを使用します。 使用しての詳細については**goto**条件付きの操作について、[場合](if.md)コマンドのリファレンス。

## <a name="BKMK_examples"></a>例

次のバッチ プログラムは、システム ディスクとして A ドライブのディスクをフォーマットします。 操作が成功した場合、 **goto**コマンドにより、プロセッサが、 **: エンド**ラベル。
```
echo off
format a: /s
if not errorlevel 1 goto end
echo An error occurred during formatting.
:end
echo End of batch program. 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)

[cmd](cmd.md)

[もし](if.md)