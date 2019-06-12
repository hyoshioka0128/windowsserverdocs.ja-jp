---
title: start
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0173f9b3-5cd7-4edb-b01e-d02193b4fadc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ab7388633681120442544adf4ee0e337d8599854
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441225"
---
# <a name="start"></a>start



指定したプログラムまたはコマンドを実行する別のコマンド プロンプト ウィンドウを起動します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
start ["<Title>"] [/d <Path>] [/i] [{/min | /max}] [{/separate | /shared}] [{/low | /normal | /high | /realtime | /abovenormal | belownormal}] [/affinity <HexAffinity>] [/wait] [/b {<Command> | <Program>} [<Parameters>]]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|"\<タイトル >"|コマンド プロンプト ウィンドウのタイトル バーに表示するタイトルを指定します。|
|/d\<パス >|スタートアップ ディレクトリを指定します。|
|/i|Cmd.exe スタートアップ環境を新しいコマンド プロンプト ウィンドウに渡します。 場合 **/i** が指定されていない、現在の環境を使用します。|
|/min \| max/|最小化することを指定 ( **/min**) または最大化 (**最大**) 新しいコマンド プロンプト ウィンドウです。|
|/separate \| /shared|別のメモリ領域で 16 ビット プログラムを起動 ( **/separate**) または共有メモリの領域 ( **/共有**)。 64 ビット プラットフォームでは、これらのオプションはサポートされていません。|
|/low \| /normal \| /high \| /realtime \| /abovenormal \| /belownormal|指定した優先度クラスでは、アプリケーションを起動します。 有効な優先度クラスの値は **低/** , 、**通常/** , 、 **/高**, 、 **/realtime**, 、 **/abovenormal**, と **/belownormal**します。|
|/affinity \<HexAffinity >|新しいアプリケーションを (16 進数として表されます)、指定されたプロセッサ関係マスクを適用します。|
|/wait|アプリケーションを起動し、終了するまで待機します。|
|/b|新しいコマンド プロンプト ウィンドウを開くことがなく、アプリケーションを起動します。 CTRL キーを押しながら C キーの処理には、アプリケーションは CTRL + C 処理を有効にしない限りは無視されます。 アプリケーションを中断するのにには、CTRL キーを押しながら BREAK キーを使用します。|
|/b\<コマンド > \| \<プログラム >|開始するコマンドまたはプログラムを指定します。|
|\<パラメーター >|コマンドまたはプログラムに渡すパラメーターを指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

- コマンドとして、ファイルの名前を入力して、ファイルの関連付けを通じて非実行可能ファイルを実行できます。
- 拡張機能またはパスの修飾子を持たない最初のトークンとして文字列"CMD"を含むコマンドを実行すると、"CMD"は COMSPEC 変数の値に置き換えられます。 これを取得できないように **cmd** 、現在のディレクトリからです。
- 32 ビットのグラフィカル ユーザー インターフェイス (GUI) アプリケーションを実行するときに **cmd** アプリケーションのコマンド プロンプトに戻る前に終了を待ちません。 この動作は、コマンド スクリプトからアプリケーションを実行する場合に発生しません。
- 拡張機能が含まれていない最初のトークンを使用するコマンドを実行すると Cmd.exe、PATHEXT 環境変数の値を使用して、どのような順序で検索する拡張機能を決定します。 PATHEXT 変数の既定値は、します。  
  ```
  .COM;.EXE;.BAT;.CMD 
  ```  
  構文は、各拡張機能を分離することをセミコロンで区切って、パス変数と同じことに注意してください。
- 他の拡張機能との一致がない場合、実行可能ファイルを検索するとき **開始** ディレクトリ名が名前に一致するかどうかかどうかを確認します。 そのような場合は、 **開始** そのパスに Explorer.exe を開きます。

## <a name="BKMK_examples"></a>例

コマンド プロンプトで、Myapp プログラムを起動し、現在のコマンド プロンプト ウィンドウの使用を保持する次のように入力します。
```
start myapp 
```
表示する、 **開始** 個別のコマンド ライン ヘルプ トピックの「コマンド プロンプト ウィンドウで型を最大化します。
```
start /max start /?
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)
