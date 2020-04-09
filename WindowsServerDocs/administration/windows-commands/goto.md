---
title: goto
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e0de1458-1f78-48ff-a746-c285a945a510
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 928a9031a7f86261789676257afe95ffc3be8a99
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80842565"
---
# <a name="goto"></a>goto



Cmd.exe をバッチプログラムのラベル付きの行に指示します。 バッチプログラム内で、 **goto**はラベルで識別される行にコマンド処理を指示します。 ラベルが見つかると、処理が続行され、次の行で始まるコマンドが開始されます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
goto <Label> 
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ラベル >|バッチプログラムでラベルとして使用されるテキスト文字列を指定します。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>コメント

-   コマンド拡張機能の使用

    コマンド拡張機能が有効になっている場合 (既定)、target ラベルが**EOF**の**goto**コマンドを使用する場合は、現在のバッチスクリプトファイルの末尾に制御を移し、ラベルを定義せずにバッチスクリプトファイルを終了します。 **: EOF**ラベルと共に**goto**を使用する場合は、ラベルの前にコロンを挿入する必要があります。 例 :  
    ```
    goto:EOF
    ```  
-   有効な*ラベル*値の使用

    *Label*パラメーターではスペースを使用できますが、他の区切り記号 (セミコロンや等号など) を含めることはできません。
-   バッチプログラムのラベルと一致する*ラベル*

    指定する*ラベル*値は、バッチプログラムのラベルと一致する必要があります。 バッチプログラム内のラベルは、コロン (:) で始まる必要があります。 行がコロンで始まる場合は、ラベルとして扱われ、その行のすべてのコマンドは無視されます。 [*ラベル*] に指定したラベルがバッチプログラムに含まれていない場合、バッチプログラムは停止し、次のメッセージが表示されます。  
    ```
    Label not found
    ```  
-   条件付き操作に**goto**を使用する

    他のコマンドと共に**goto**を使用して、条件付き操作を実行できます。 条件付き操作に**goto**を使用する方法の詳細については、「 [If](if.md)コマンドリファレンス」を参照してください。

## <a name="examples"></a><a name=BKMK_examples></a>例

次のバッチプログラムは、ドライブ A のディスクをシステムディスクとしてフォーマットします。 操作が成功した場合、 **goto**コマンドは処理を**終了**ラベルに渡します。
```
echo off
format a: /s
if not errorlevel 1 goto end
echo An error occurred during formatting.
:end
echo End of batch program. 
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

[Cmd](cmd.md)

[もし](if.md)