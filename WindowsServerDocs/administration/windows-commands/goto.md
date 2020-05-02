---
title: goto
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e0de1458-1f78-48ff-a746-c285a945a510
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dd61575b8b31ed47463db464f4aad0a048e755b2
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725004"
---
# <a name="goto"></a>goto



Cmd.exe をバッチプログラムのラベル付きの行に指示します。 バッチプログラム内で、 **goto**はラベルで識別される行にコマンド処理を指示します。 ラベルが見つかると、処理が続行され、次の行で始まるコマンドが開始されます。



## <a name="syntax"></a>構文

```
goto <Label> 
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|\<ラベルの>|バッチプログラムでラベルとして使用されるテキスト文字列を指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>Remarks

-   コマンド拡張機能の使用

    コマンド拡張機能が有効になっている場合 (既定)、target ラベルが**EOF**の**goto**コマンドを使用する場合は、現在のバッチスクリプトファイルの末尾に制御を移し、ラベルを定義せずにバッチスクリプトファイルを終了します。 **: EOF**ラベルと共に**goto**を使用する場合は、ラベルの前にコロンを挿入する必要があります。 次に例を示します。  
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

## <a name="examples"></a>例

次のバッチプログラムは、ドライブ A のディスクをシステムディスクとしてフォーマットします。 操作が成功した場合、 **goto**コマンドは処理を**終了**ラベルに渡します。
```
echo off
format a: /s
if not errorlevel 1 goto end
echo An error occurred during formatting.
:end
echo End of batch program. 
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

[Cmd](cmd.md)

[If](if.md)