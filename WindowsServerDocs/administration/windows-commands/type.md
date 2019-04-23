---
title: type
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c44fe905-a865-4c97-8cc5-fb95fec7d4d5
author: coreyp-at-msft
ms.author: coreyp
manager: dansimp
ms.openlocfilehash: 4ceb7365d34a2aeca21d1a699730a589f98fd549
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887403"
---
# <a name="type"></a>type


Windows コマンド シェルで**型**は組み込みのコマンドをテキスト ファイルの内容を表示します。 使用して、**型**を変更せずにテキスト ファイルを表示するコマンド。


PowerShell では、**型**を組み込みエイリアスでは、 **[Get-content](https://docs.microsoft.com/powershell/module/microsoft.powershell.management/get-content)** コマンドレットに渡しても、構文が異なりますが、ファイルの内容を表示します。


Windows コマンド シェル (Cmd.exe) 内でこのコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。

## <a name="syntax"></a>構文

```
type [<Drive>:][<Path>]<FileName>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[\<ドライブ >:] [\<パス >]\<ファイル名 >|ファイルまたは表示するファイルの名前と場所を指定します。 複数のファイル名を空白で区切ります。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

-   場合*FileName*スペースが含まれています (たとえば、"ファイル名を含む Spaces.txt") の引用符で囲みます。
-   バイナリ ファイルまたはプログラムによって作成されるファイルを表示する場合は、フォーム フィード文字とエスケープ シーケンスのシンボルを含む画面で、異常な文字を参照してください可能性があります。 これらの文字は、バイナリ ファイルで使用される制御コードを表します。 一般に、使用しないでください、**型**バイナリ ファイルを表示するコマンド。

## <a name="BKMK_examples"></a>例

Holiday.mar という名前のファイルの内容を表示するには、次のように入力します。
```
type holiday.mar 
```
一度に 1 画面ずつ Holiday.mar をという名前の時間のかかるファイルの内容を表示するには、次のように入力します。
```
type holiday.mar | more 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)
