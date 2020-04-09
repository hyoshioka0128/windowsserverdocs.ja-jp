---
title: print
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: aa2325d5-a993-4ed3-b996-255165452db8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 36966d8d3beb032ee0dcee50d9bd5bc0111bf4f5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80837375"
---
# <a name="print"></a>print



テキスト ファイルをプリンターに送信します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
Print [/d:<PrinterName>] [<Drive>:][<Path>]<FileName>[ ...]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/d:\<PrinterName >|ジョブを印刷するプリンターを指定します。 ローカルに接続されたプリンターに印刷するには、プリンターが接続されているコンピューターで、ポートを指定します。</br>-パラレル ポートに有効な値は、LPT1、LPT2、LPT3 です。</br>にシリアル ポート用有効な値は、COM1、COM2、COM3、COM4 です。</br>また、キュー名 (\\\\*ServerName*\*PrinterName *) を使用して、ネットワークプリンターを指定することもできます。 プリンターを指定しないと、印刷ジョブが既定では LPT1 に送信されます。|
|\<ドライブ >:|印刷するファイルの場所の論理的または物理的なドライブを指定します。 現在のドライブに印刷するファイルがある場合、このパラメーターは必要ありません。|
|\<パス >|印刷するファイルの場所を指定します。 印刷するファイルが現在のディレクトリにある場合、このパラメーターは必要ありません。|
|\<ファイル名 > [...]|必須。 印刷するファイルを指定します。 1 つのコマンドでは、複数のファイルを含めることができます。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>コメント

-   ファイルは、ローカル コンピューターのシリアル ポートまたはパラレル ポートに接続されているプリンターに送信する場合、バック グラウンドで印刷できます。
-   コマンド プロンプトからさまざまな構成タスクを実行するにを使用して、 **モード** コマンドです。

    の詳細については、「[モード](mode.md)」を参照してください。  
    -   パラレル ポートに接続されているプリンターを構成します。
    -   シリアル ポートに接続されているプリンターを構成します。
    -   プリンターの状態を表示します。
    -   コード ページ切り替えのプリンターを準備します。

## <a name="examples"></a><a name=BKMK_examples></a>例

LPT2 に、ローカル コンピューター上のプリンターには、現在のディレクトリに Report.txt に接続されているファイルを送信するには、次のように入力します。
```
print /d:lpt2 report.txt
```
C:\ Accounting ディレクトリにある test.txt ファイルを \\\\CopyRoom サーバーの Printer1 印刷キューに送信するには、次のように入力します。
```
print /d:\\copyroom\printer1 c:\accounting\report.txt 
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

[印刷コマンドのリファレンス](print-command-reference.md)

[モード](mode.md)