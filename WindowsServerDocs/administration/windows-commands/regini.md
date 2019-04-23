---
title: regini
description: コマンド プロンプトまたはスクリプトを使用してレジストリを変更する方法について説明します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5ff18dc3-5bd8-400a-b311-fd73a3267e8c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 292dfe5755a10a91f2b8bcffaa6412ccda6c6f8a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867633"
---
# <a name="regini"></a>regini

コマンドラインまたはスクリプト、レジストリを変更し、1 つまたは複数のテキスト ファイルに事前設定された変更を適用します。 作成、変更、またはレジストリ キーのアクセス許可を変更するだけでなく、レジストリ キーを削除できます。

形式と Regini.exe を使用して、レジストリを変更するテキストのスクリプト ファイルの内容について詳しくは、次を参照してください。[コマンドラインまたはスクリプトからのレジストリ値またはアクセス許可を変更する方法](https://support.microsoft.com/help/264584/how-to-change-registry-values-or-permissions-from-a-command-line-or-a)します。

## <a name="syntax"></a>構文

```
regini [-m \\machinename | -h hivefile hiveroot][-i n] [-o outputWidth][-b] textFiles...
```

### <a name="parameters"></a>パラメーター

|パラメーター |説明 |
|-m \<\\\\ComputerName>|レジストリを変更すると、リモート コンピューターの名前を指定します。 形式を使用して **\\ \\ComputerName**します。|
|---------------------|-|
|-h \<hivefile hiveroot>|変更をローカル レジストリ ハイブを指定します。 形式でハイブ ファイルの名前と、hive のルートを指定する必要があります **hivefile hiveroot**します。|
|-i \<n>|コマンドの出力のレジストリ キーのツリー構造を示すために使用するインデント レベルを指定します。 **Regdmp.exe** (これは、バイナリ形式で、レジストリ キーの現在のアクセス許可を取得) ツールを使用してインデント、4 の倍数でため、既定値は **4**します。|
|-o \<outputwidth>|文字で、コマンドの出力の幅を指定します。 出力がコマンド ウィンドウに表示され、既定値はウィンドウの幅です。 既定値は、出力をファイルに出力すると場合、 **240** 文字です。|
|-b|指定する **Regini.exe** 出力は次の以前のバージョンとの下位互換性 **Regini.exe**します。 詳細については、「解説」を参照してください。|
|textfiles|レジストリ データを含む 1 つ以上のテキスト ファイルの名前を指定します。 ANSI または Unicode テキスト ファイルの任意の数を指定できます。|

## <a name="remarks"></a>注釈

使用して適用するレジストリ データを含むテキスト ファイルの内容には、主に次のガイドラインが適用 **Regini.exe**します。
-   行の終わりのコメント文字としてセミコロンを使用します。 行の最初の空白以外の文字があります。
-   バック スラッシュを使用すると、行の継続を指定します。 コマンドでは、円記号を (が含まれていない) からすべての文字を無視します。 次の行の最初の空白以外の文字。 円記号の前に 1 つ以上のスペースを含めると、単一の空白に置き換えられます。
-   ハード タブ文字を使用すると、インデントを制御できます。 このインデント; のレジストリ キーのツリー構造を示すただし、これらの文字は、それらの位置に関係なく 1 つのスペースに変換されます。

#### <a name="additional-references"></a>その他の参照情報

-   [コマンドライン構文キー](command-line-syntax-key.md)