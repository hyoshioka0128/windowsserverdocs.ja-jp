---
title: 型
description: Windows コマンドのトピックでは、テキストファイルの内容が表示されます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c44fe905-a865-4c97-8cc5-fb95fec7d4d5
author: coreyp-at-msft
ms.author: coreyp
manager: dansimp
ms.openlocfilehash: 3163601d118df315edcae540917313703f677d52
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80832415"
---
# <a name="type"></a>型

Windows コマンドシェルの**type**は、テキストファイルの内容を表示する組み込みコマンドです。 **Type**コマンドを使用して、テキストファイルを変更せずに表示します。

PowerShell では、 **type**は **[Get Content](https://docs.microsoft.com/powershell/module/microsoft.powershell.management/get-content)** コマンドレットへの組み込みエイリアスであり、ファイルの内容も表示されますが、構文は異なります。

Windows コマンドシェル (Cmd.exe) 内でこのコマンドを使用する方法の例については、「[例](#BKMK_examples)」を参照してください。

## <a name="syntax"></a>構文

```
type [<Drive>:][<Path>]<FileName>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[\<ドライブ >:][\<パス >]\<ファイル名 >|表示するファイルの場所と名前を指定します。 複数のファイル名をスペースで区切ります。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>コメント

-   *FileName*にスペースが含まれている場合は、引用符で囲みます (たとえば、ファイル名にスペース .Txt を含めます)。
-   プログラムによって作成されたバイナリファイルまたはファイルを表示すると、フォームフィード文字やエスケープシーケンスのシンボルなど、画面に奇妙な文字が表示されることがあります。 これらの文字は、バイナリファイルで使用される制御コードを表します。 一般に、バイナリファイルの表示には**type**コマンドを使用しないでください。

## <a name="examples"></a><a name=BKMK_examples></a>例

祭日という名前のファイルの内容を表示するには、次のように入力します。
```
type holiday.mar 
```
祝日という名前の長いファイルの内容を一度に1画面ずつ表示するには、次のように入力します。
```
type holiday.mar | more 
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
