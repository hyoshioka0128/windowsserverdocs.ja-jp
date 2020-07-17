---
title: mklink
description: Mklink コマンドの参照記事。ディレクトリまたはファイルのシンボリックリンクまたはハードリンクを作成します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0ce4df22-2dbc-48fc-9c16-b721ae85f857
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cb8339f7dcb2f397d6b90105e2ccd9bdc8cc07a5
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928534"
---
# <a name="mklink"></a>mklink

ディレクトリまたはファイルのシンボリックリンクまたはハードリンクを作成します。

## <a name="syntax"></a>構文

```
mklink [[/d] | [/h] | [/j]] <link> <target>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| /d | ディレクトリのシンボリック リンクを作成します。 既定では、このコマンドはファイルのシンボリックリンクを作成します。 |
| /h | シンボリック リンクの代わりにハード リンクを作成します。 |
| /j | ディレクトリの分岐点を作成します。 |
| `<link>` | 作成するシンボリックリンクの名前を指定します。 |
| `<target>` | 新しいシンボリック リンクを指すパス (相対パスまたは絶対パス) を指定します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

### <a name="examples"></a>例

、MyFolder、および \Users\User1\Documents という名前のシンボリックリンクを作成し、ディレクトリ内にあるファイルの例をルートディレクトリから削除するには、次のように入力します。

```
mklink /d \MyFolder \Users\User1\Documents
mklink /h \MyFile.file \User1\Documents\example.file
rd \MyFolder
del \MyFile.file
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [del コマンド](del.md)

- [rd コマンド](rd.md)

- [Windows PowerShell の新しい項目](https://docs.microsoft.com/powershell/module/microsoft.powershell.management/new-item?view=powershell-6)
