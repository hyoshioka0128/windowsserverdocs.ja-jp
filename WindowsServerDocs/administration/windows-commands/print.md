---
title: print
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: aa2325d5-a993-4ed3-b996-255165452db8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8937253da730c2ab77ff03cdeb9f31d24e608eab
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722864"
---
# <a name="print"></a>print



テキスト ファイルをプリンターに送信します。



## <a name="syntax"></a>構文

```
Print [/d:<PrinterName>] [<Drive>:][<Path>]<FileName>[ ...]
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|/d:\<PrinterName>|ジョブを印刷するプリンターを指定します。 ローカルに接続されたプリンターに印刷するには、プリンターが接続されているコンピューターで、ポートを指定します。</br>-パラレル ポートに有効な値は、LPT1、LPT2、LPT3 です。</br>にシリアル ポート用有効な値は、COM1、COM2、COM3、COM4 です。</br>また、キュー名 (\\\\*ServerName*\*PrinterName *) を使用して、ネットワークプリンターを指定することもできます。 プリンターを指定しないと、印刷ジョブが既定では LPT1 に送信されます。|
|\<ドライブ>:|印刷するファイルの場所の論理的または物理的なドライブを指定します。 現在のドライブに印刷するファイルがある場合、このパラメーターは必要ありません。|
|\<パス>|印刷するファイルの場所を指定します。 印刷するファイルが現在のディレクトリにある場合、このパラメーターは必要ありません。|
|\<ファイル名> [...]|必須。 印刷するファイルを指定します。 1 つのコマンドでは、複数のファイルを含めることができます。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>Remarks

-   ファイルは、ローカル コンピューターのシリアル ポートまたはパラレル ポートに接続されているプリンターに送信する場合、バック グラウンドで印刷できます。
-   コマンド プロンプトからさまざまな構成タスクを実行するにを使用して、 **モード** コマンドです。

    の詳細については、「[モード](mode.md)」を参照してください。  
    -   パラレル ポートに接続されているプリンターを構成します。
    -   シリアル ポートに接続されているプリンターを構成します。
    -   プリンターの状態を表示します。
    -   コード ページ切り替えのプリンターを準備します。

## <a name="examples"></a>例

LPT2 に、ローカル コンピューター上のプリンターには、現在のディレクトリに Report.txt に接続されているファイルを送信するには、次のように入力します。
```
print /d:lpt2 report.txt
```
C:\ Accounting ディレクトリにある test.txt ファイルを\\ \\copyroom サーバーの Printer1 印刷キューに送信するには、次のように入力します。
```
print /d:\\copyroom\printer1 c:\accounting\report.txt 
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

[印刷コマンドのリファレンス](print-command-reference.md)

[モード](mode.md)