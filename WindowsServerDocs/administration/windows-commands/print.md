---
title: print
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aa2325d5-a993-4ed3-b996-255165452db8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d85fc5b2cd5f5ba09ebdf4756a5adb60c1759f2a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831553"
---
# <a name="print"></a>print



テキスト ファイルをプリンターに送信します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
Print [/d:<PrinterName>] [<Drive>:][<Path>]<FileName>[ ...]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/d:\<PrinterName>|ジョブを印刷するプリンターを指定します。 ローカルに接続されたプリンターに印刷するには、プリンターが接続されているコンピューターで、ポートを指定します。</br>-パラレル ポートに有効な値は、LPT1、LPT2、LPT3 です。</br>にシリアル ポート用有効な値は、COM1、COM2、COM3、COM4 です。</br>キュー名を使用して、ネットワーク プリンターを指定することもできます (\\\\*ServerName*\*PrinterName *)。 プリンターを指定しないと、印刷ジョブが既定では LPT1 に送信されます。|
|\<ドライブ >:|印刷するファイルの場所の論理的または物理的なドライブを指定します。 現在のドライブに印刷するファイルがある場合、このパラメーターは必要ありません。|
|\<パス >|印刷するファイルの場所を指定します。 印刷するファイルが現在のディレクトリにある場合、このパラメーターは必要ありません。|
|\<ファイル名 > [...]|必須。 印刷するファイルを指定します。 1 つのコマンドでは、複数のファイルを含めることができます。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

-   ファイルは、ローカル コンピューターのシリアル ポートまたはパラレル ポートに接続されているプリンターに送信する場合、バック グラウンドで印刷できます。
-   コマンド プロンプトからさまざまな構成タスクを実行するにを使用して、 **モード** コマンドです。

    参照してください[モード](mode.md)の詳細については。  
    -   パラレル ポートに接続されているプリンターを構成します。
    -   シリアル ポートに接続されているプリンターを構成します。
    -   プリンターの状態を表示します。
    -   コード ページ切り替えのプリンターを準備します。

## <a name="BKMK_examples"></a>例

LPT2 に、ローカル コンピューター上のプリンターには、現在のディレクトリに Report.txt に接続されているファイルを送信するには、次のように入力します。
```
print /d:lpt2 report.txt
```
Printer1 は通常の印刷キューに Report.txt c:\Accounting ディレクトリ内のファイルを送信する、 \\ \\CopyRoom、サーバーの型。
```
print /d:\\copyroom\printer1 c:\accounting\report.txt 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)

[印刷コマンドのリファレンス](print-command-reference.md)

[モード](mode.md)