---
title: expand
description: 展開コマンドの参照記事。1つ以上の圧縮ファイルを展開します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 66de0488-a0c4-40c2-9b03-e40c107ba343
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 918d629ea0d3d87ea42184580c1be84740d4f79d
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86958234"
---
# <a name="expand"></a>expand

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

1つ以上の圧縮ファイルを展開します。 また、このコマンドを使用して、配布ディスクから圧縮ファイルを取得することもできます。

**Expand**コマンドは、別のパラメーターを使用して Windows 回復コンソールから実行することもできます。 詳細については、「 [Windows 回復環境 (WinRE)](/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference)」を参照してください。

## <a name="syntax"></a>構文

```
expand [/r] <source> <destination>
expand /r <source> [<destination>]
expand /i <source> [<destination>]
expand /d <source>.cab [/f:<files>]
expand <source>.cab /f:<files> <destination>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| /r | 展開されたファイルの名前を変更します。 |
| source | 展開するファイルを指定します。 *ソース*は、ドライブ文字とコロン、ディレクトリ名、ファイル名、またはこれらの組み合わせで構成されます。 ワイルドカード (**&#42;** または **?**) を使用できます。 |
| destination | ファイルの展開先を指定します。<p>*ソース*が複数のファイルで構成されていて、 **/r**を指定していない場合、*コピー先*はディレクトリである必要があります。 *宛先*には、ドライブ文字とコロン、ディレクトリ名、ファイル名、またはこれらの組み合わせを使用できます。 宛先 `file | path` の指定。 |
| /i | 展開されたファイルの名前を変更しますが、ディレクトリ構造は無視します。 |
| /d | 展開元のファイル一覧を表示します。 はファイルを展開したり展開したりしません。 |
| /f`<files>` | 拡張するキャビネット (.cab) ファイル内のファイルを指定します。 ワイルドカード (**&#42;** または **?**) を使用できます。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
