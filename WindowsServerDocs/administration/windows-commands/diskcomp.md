---
title: diskcomp
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4f56f534-a356-4daa-8b4f-38e089341e42
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3945311873dff763a8e9e8cdd3f766c1ed4580b1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837533"
---
# <a name="diskcomp"></a>diskcomp



2 つのフロッピー ディスクの内容を比較します。 パラメーターを指定せずに使用されている場合**あれば**現在のドライブを使用して、両方のディスクを比較します。このコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。

## <a name="syntax"></a>構文

```
diskcomp [<Drive1>: [<Drive2>:]]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ドライブ 1 >|フロッピー ディスクを 1 つを含むドライブを指定します。|
|\<ドライブ 2 >|その他のフロッピー ディスクを含むドライブを指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

-   ディスクを使用します。

    **あれば**コマンドはフロッピー ディスクでのみ使用できます。 使用することはできません**あれば**ハード ディスクを使用します。 用のハード ディスク ドライブを指定する場合*ドライブ 1*または*ドライブ 2*、**あれば**次のエラー メッセージが表示されます。  
    ```
    Invalid drive specification
    Specified drive does not exist
    or is nonremovable
    ```  
-   ディスクを比較します。

    比較対象となる 2 つのディスク上のすべてのトラックは同じですが場合、**あれば**次のメッセージが表示されます。  
    ```
    Compare OK
    ```  
    トラックが同じ場合**あれば**次のようなメッセージが表示されます。  
    ```
    Compare error on
    side 1, track 2
    ```  
    ときに**あれば**比較が完了すると、次のメッセージが表示されます。  
    ```
    Compare another diskette (Y/N)?
    ```  
    Y キーを押す場合**あれば**次の比較のディスクを挿入するように求められます。 キーを押す場合、N**あれば**比較は停止します。

    ときに**あれば**比較は、ディスクのボリュームの番号は無視されます。
-   ドライブのパラメーターを省略します。

    省略した場合、*ドライブ 2*パラメーター、**あれば**の現在のドライブを使用して*ドライブ 2*します。 両方のドライブ パラメーターを省略した場合**あれば**両方の現在のドライブを使用します。 現在のドライブが同じ場合*ドライブ 1*、**あれば**を必要に応じて、ディスクを交換するメッセージが表示されます。
-   1 つのドライブを使用します。

    同じフロッピー ディスク ドライブを指定する場合*ドライブ 1*と*ドライブ 2*、**あれば**1 つのドライブを使用してそれらを比較し、必要に応じて、ディスクを挿入するように求められます。 ディスクと、使用可能なメモリの量の容量に応じて、1 回以上のディスクを交換する必要があります。
-   ディスクのさまざまな種類の比較

    **あれば**両面のディスクも倍密度のディスクを使用した高密度のディスクの片面のディスクを比較することはできません。 場合のディスク*ドライブ 1*でディスクと同じ型ではありません*ドライブ 2*、**あれば**次のメッセージが表示されます。  
    ```
    Drive types or diskette types not compatible
    ```  
-   使用して**あれば**ネットワークおよびリダイレクトされたドライブを使用

    **あれば**ネットワーク ドライブまたはによって作成されたドライブは機能しません、 **subst**コマンド。 使用すると場合**あれば**、これらの型のいずれかのドライブと**あれば**次のエラー メッセージが表示されます。  
    ```
    Invalid drive specification
    ```  
-   コピー元のディスクを比較します。

    使用すると**あれば**を使用して行ったディスクを使用した**コピー**、**あれば**次のようなメッセージを表示することがあります。  
    ```
    Compare error on 
    side 0, track 0
    ```  
    ディスク上のファイルが同じ場合でも、この種のエラーが発生します。 **コピー**重複については、これとは限りませんが設定されない、先のディスクに同じ場所にします。
-   理解**あれば**終了コード

    次の表では、終了コードについて説明します。  
    |終了コード|説明|
    |---------|-----------|
    |0|ディスクは、同じ|
    |1|相違が検出されました|
    |3|ハード エラーが発生しました|
    |4|初期化エラーが発生しました|

    によって返されるプロセス終了コードを**あれば**、ERRORLEVEL 環境変数を使用して、上、**場合**バッチ プログラム内でコマンドライン。

## <a name="BKMK_examples"></a>例

コンピューターに 1 つだけのフロッピー ディスク ドライブ (たとえば、ドライブ A)、2 つのディスクを比較する場合は、次のように入力します。
```
diskcomp a: a:
```
**あれば**必要に応じて、各ディスクを挿入するように求められます。

次の例では、処理する方法を示しています、**あれば**終了コードで、ERRORLEVEL 環境変数を使用するバッチ プログラムで、**場合**コマンドライン。
```
rem Checkout.bat compares the disks in drive A and B 
echo off 
diskcomp a: b: 
if errorlevel 4 goto ini_error 
if errorlevel 3 goto hard_error 
if errorlevel 1 goto no_compare
if errorlevel 0 goto compare_ok 
:ini_error 
echo ERROR: Insufficient memory or command invalid 
goto exit 
:hard_error 
echo ERROR: An irrecoverable error occurred 
goto exit 
:break 
echo "You just pressed CTRL+C" to stop the comparison 
goto exit 
:no_compare 
echo Disks are not the same 
goto exit 
:compare_ok 
echo The comparison was successful; the disks are the same 
goto exit 
:exit
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)
