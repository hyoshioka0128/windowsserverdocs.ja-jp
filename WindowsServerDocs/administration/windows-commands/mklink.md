---
title: mklink
description: Mklink コマンドの参照記事。ディレクトリまたはファイルのシンボリックリンクまたはハードリンクを作成します。
ms.topic: article
ms.assetid: 0ce4df22-2dbc-48fc-9c16-b721ae85f857
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 76c97032874fe23fea773dbf5e2d1d862a6048af
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87886430"
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

- [Windows PowerShell の新しい項目](/powershell/module/microsoft.powershell.management/new-item?view=powershell-6)
