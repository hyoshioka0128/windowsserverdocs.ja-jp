---
title: diskcomp
description: 2つのフロッピーディスクの内容を比較する、「いいね!」を参照してください。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4f56f534-a356-4daa-8b4f-38e089341e42
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e1b15e9b6669a22ac95693e635bae1642c307e09
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719483"
---
# <a name="diskcomp"></a>diskcomp

2つのフロッピーディスクの内容を比較します。 パラメーターを指定せず**に使用**する場合は、現在のドライブを使用して両方のディスクを比較します。


## <a name="syntax"></a>構文

```
diskcomp [<Drive1>: [<Drive2>:]]
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|\<Drive1>|フロッピーディスクの1つを含むドライブを指定します。|
|\<Drive2>|他のフロッピーディスクを含むドライブを指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>Remarks

- ディスクの使用

  この**コマンドは**、フロッピーディスクでのみ機能します。 ハードディスクで**は使用でき**ません。 ドライブ1または*Drive2*のハードディスクドライブを指定*すると、* **次のエラーメッセージが表示さ**れます。  
  ```
  Invalid drive specification
  Specified drive does not exist
  or is nonremovable
  ```  
- ディスクの比較

  比較対象の2つのディスクのすべてのトラックが同じ場合は、**次のメッセージが表示さ**れます。  
  ```
  Compare OK
  ```  
  トラックが同じでない場合は、次のようなメッセージ**が表示されます。**  
  ```
  Compare error on
  side 1, track 2
  ```  
  この比較**が完了する**と、次のメッセージが表示されます。  
  ```
  Compare another diskette (Y/N)?
  ```  
  Y キーを押すと、次の比較のためにディスクを挿入するよう**に求めるメッセージ**が表示されます。 N を押した場合は、比較**が停止し**ます。

  この比較を**行うと、** ディスクのボリューム番号は無視されます。
- ドライブパラメーターの省略

  *Drive2*パラメーターを省略した場合 **、は** *drive2*の現在のドライブを使用します。 両方のドライブパラメーターを省略した場合は、両方に現在のドライブ**が使用さ**れます。 現在のドライブがドライブ1と同じ場合は、必要に応じて**ディスクを交換**するように求める*メッセージが表示*されます。
- 1つのドライブを使用する

  *Drive1*と*Drive2*に同じフロッピーディスクドライブを指定すると、1つのドライブを使用してそれら**を比較し**、必要に応じてディスクを挿入するように求めます。 ディスクの容量と使用可能なメモリの量によっては、ディスクのスワップが必要になる場合があります。
- さまざまな種類のディスクの比較

  1つの片面ディスクと双方向ディスクを比較**することは**できません。また、高密度ディスクでも二重密度ディスクを使用することはできません。 ドライブ*1 のディスク*が、 *Drive2*のディスクと同じ種類でない場合は、次のメッセージ**が表示さ**れます。  
  ```
  Drive types or diskette types not compatible
  ```  
- ネットワークとリダイレクトさ**れたドライブの使用**

  ネットワークドライブまたは**subst**コマンドによって作成されたドライブ**では機能**しません。 これらの種類のいずれかのドライブで**を使用し**ようとすると、**次のエラーメッセージが表示さ**れます。  
  ```
  Invalid drive specification
  ```  
- 元のディスクとコピーを比較する

  **Copy**を使用して作成したディスク**を使用する**と、次のようなメッセージが表示される場合**があります**。  
  ```
  Compare error on 
  side 0, track 0
  ```  
  この種類のエラーは、ディスク上のファイルが同じ場合でも発生する可能性があります。 重複する情報をコピーする場合でも、必ずしも**コピー**先のディスク上の同じ場所に配置する必要はありません。
- 終了**コード**を理解する

  次の表では、各終了コードについて説明します。  

  |終了コード|[説明]|
  |---------|-----------|
  |0|ディスクが同じです|
  |1|相違点が見つかりました|
  |3|ハードエラーが発生しました|
  |4|初期化エラーが発生しました|

  **によって**返される終了コードを処理するには、バッチプログラムの**if**コマンドラインで ERRORLEVEL 環境変数を使用します。

## <a name="examples"></a>例

コンピューターにフロッピーディスクドライブが1つしかない場合 (ドライブ A など)、2つのディスクを比較するには、次のように入力します。
```
diskcomp a: a:
```
必要に応じて、各ディスクを挿入するように**求められ**ます。

**If**コマンドラインで ERRORLEVEL 環境変数を使用するバッチプログラムで、次のよう**な終了コードを処理**する方法を説明します。
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
echo You just pressed CTRL+C to stop the comparison 
goto exit 
:no_compare 
echo Disks are not the same 
goto exit 
:compare_ok 
echo The comparison was successful; the disks are the same 
goto exit 
:exit
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
