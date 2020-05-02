---
title: pause
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: cab3afc3-d046-432f-a0bf-6282f0099032
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 89e76c4f45f59c32ef879fb518a1a92c973f5cdf
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723351"
---
# <a name="pause"></a>pause



バッチ ファイルの処理を中断し、次のようなダイアログを表示します。
```
Press any key to continue . . .
```


## <a name="syntax"></a>構文

```
pause
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>Remarks

- 実行すると、 **を一時停止** コマンドを次のメッセージが表示されます。  
  ```
  Press any key to continue . . .
  ```  
- バッチ プログラムを停止するには、CTRL + C を押すと、次のメッセージが表示されます。  
  ```
  Terminate batch job (Y/N)?
  ```  
  Y (yes) キーを押して、このメッセージに応答をバッチ プログラムが終了し、制御がオペレーティング システムに戻ります。
- 挿入することができます、 **を一時停止** コマンドを処理したくないバッチ ファイルのセクションまでにします。 **を一時停止** を一時停止バッチ ファイルの処理には、ctrl キーを押しながら C キーを押してしてバッチ プログラムを停止するには Y キーを押します。

## <a name="examples"></a>例

いずれのドライブでディスクを変更するユーザーの入力を要求するバッチ ファイルを作成するには、次のように入力します。
```
@echo off 
:Begin 
copy a:*.* 
echo Put a new disk into drive A 
pause 
goto begin
```
この例では、ドライブのディスク上のすべてのファイルは、現在のディレクトリにコピーされます。 メッセージでは、A、ドライブに新しいディスクを挿入するように求められます後、 **を一時停止** コマンドは、ディスクに変更され、処理を再開する任意のキーを押してようにの処理を中断します。 このバッチ ファイルは、無限ループで実行される —、 **goto 開始** コマンドは、バッチ ファイルの先頭のラベルに、コマンド インタープリターを送信します。 このバッチ ファイルを停止するには、ctrl キーを押しながら C キーを押して、Y キーを押します。

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)