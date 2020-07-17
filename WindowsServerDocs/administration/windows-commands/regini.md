---
title: regini
description: Regini.exe コマンドの参照記事。コマンドラインまたはスクリプトからレジストリを変更し、1つまたは複数のテキストファイルで事前設定された変更を適用します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5ff18dc3-5bd8-400a-b311-fd73a3267e8c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 56e2d4505db56248b6e4ce9c11caaae1df9a4f08
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931014"
---
# <a name="regini"></a>regini

コマンドラインまたはスクリプト、レジストリを変更し、1 つまたは複数のテキスト ファイルに事前設定された変更を適用します。 作成、変更、またはレジストリ キーのアクセス許可を変更するだけでなく、レジストリ キーを削除できます。

regini.exe がレジストリを変更するために使用するテキストスクリプトファイルの形式と内容の詳細については、「[コマンドラインまたはスクリプトからレジストリ値またはアクセス許可を変更する方法](https://support.microsoft.com/help/264584/how-to-change-registry-values-or-permissions-from-a-command-line-or-a)」を参照してください。

## <a name="syntax"></a>構文

```
regini [-m \\machinename | -h hivefile hiveroot][-i n] [-o outputwidth][-b] textfiles...
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|--|--|
| -m`<\\computername>` | レジストリを変更すると、リモート コンピューターの名前を指定します。 ** \\ ComputerName**という形式を使用します。 |
| -h`<hivefile hiveroot>` | 変更をローカル レジストリ ハイブを指定します。 形式でハイブ ファイルの名前と、hive のルートを指定する必要があります **hivefile hiveroot**します。 |
| -i`<n>` | コマンドの出力のレジストリ キーのツリー構造を示すために使用するインデント レベルを指定します。 **regdmp.exe**ツール (レジストリキーの現在のアクセス許可をバイナリ形式で取得) では、4の倍数でインデントが使用されるため、既定値は**4**です。 |
| -o`<outputwidth>` | 文字で、コマンドの出力の幅を指定します。 出力がコマンド ウィンドウに表示され、既定値はウィンドウの幅です。 既定値は、出力をファイルに出力すると場合、 **240** 文字です。 |
| -b | **regini.exe**の出力が以前のバージョンの**regini.exe**と下位互換性があることを指定します。 |
| textfiles | レジストリ データを含む 1 つ以上のテキスト ファイルの名前を指定します。 ANSI または Unicode テキスト ファイルの任意の数を指定できます。 |

#### <a name="remarks"></a>注釈

次のガイドラインは、主に、 **regini.exe**を使用して適用するレジストリデータを含むテキストファイルの内容に適用されます。

- 行の終わりのコメント文字としてセミコロンを使用します。 行の最初の空白以外の文字があります。

- バック スラッシュを使用すると、行の継続を指定します。 コマンドでは、円記号を (が含まれていない) からすべての文字を無視します。 次の行の最初の空白以外の文字。 円記号の前に 1 つ以上のスペースを含めると、単一の空白に置き換えられます。

- ハード タブ文字を使用すると、インデントを制御できます。 このインデント; のレジストリ キーのツリー構造を示すただし、これらの文字は、それらの位置に関係なく 1 つのスペースに変換されます。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
