---
title: pause
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cab3afc3-d046-432f-a0bf-6282f0099032
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 109d162e8d5c4bdd59871a21f16b6f568df4fbd6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861663"
---
# <a name="pause"></a>pause



バッチ ファイルの処理を中断し、次のようなダイアログを表示します。
```
Press any key to continue . . .
```
このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
pause
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

-   実行すると、 **を一時停止** コマンドを次のメッセージが表示されます。  
    ```
    Press any key to continue . . .
    ```  
-   バッチ プログラムを停止するには、CTRL + C を押すと、次のメッセージが表示されます。  
    ```
    Terminate batch job (Y/N)?
    ```  
    Y (yes) キーを押して、このメッセージに応答をバッチ プログラムが終了し、制御がオペレーティング システムに戻ります。
-   挿入することができます、 **を一時停止** コマンドを処理したくないバッチ ファイルのセクションまでにします。 **を一時停止** を一時停止バッチ ファイルの処理には、ctrl キーを押しながら C キーを押してしてバッチ プログラムを停止するには Y キーを押します。

## <a name="BKMK_examples"></a>例

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

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)