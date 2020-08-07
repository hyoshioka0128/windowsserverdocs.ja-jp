---
title: rd
description: ディレクトリを削除する rd コマンドの参照記事です。
ms.topic: article
ms.assetid: 42e672f6-5bc2-4c16-af25-18e7ed2dd555
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f1baacb12a0169d9915897a3d6672870c6a21927
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87884356"
---
# <a name="rd"></a>rd

ディレクトリを削除します。

**Rd**コマンドは、別のパラメーターを使用して Windows 回復コンソールから実行することもできます。 詳細については、「 [Windows 回復環境 (WinRE)](/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference)」を参照してください。

> [!NOTE]
> このコマンドは、 [rmdir コマンド](rmdir.md)と同じです。

## <a name="syntax"></a>構文

```
rd [<drive>:]<path> [/s [/q]]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|--|--|
| `[<drive>:]<path>` | 場所を削除するディレクトリの名前を指定します。 *パス* が必要です。 指定したパスの先頭に円記号 (\) を含めると、 \) ルートディレクトリ (現在のディレクトリに関係なく) から*パス*が開始されます。 *path* |
| /s | (指定されたディレクトリとすべてのファイルを含むすべてのサブディレクトリ) は、ディレクトリ ツリーを削除します。 |
| /q | クワイエット モードを指定します。 ディレクトリ ツリーを削除するときに、確認を表示しません。 **/Q**パラメーターは、 **/s**も指定されている場合にのみ機能します。<p>**注意:** Quiet モードで実行すると、ディレクトリツリー全体が確認なしで削除されます。 **/Q**コマンドラインオプションを使用する前に、重要なファイルが移動またはバックアップされていることを確認してください。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>Remarks

- 隠しファイルやシステムファイルなど、ファイルが格納されているディレクトリを削除することはできません。 これを行おうとすると、次のメッセージが表示されます。

    `The directory is not empty`

    **Dir/a**コマンドを使用して、すべてのファイル (隠しファイルおよびシステムファイルを含む) を一覧表示します。 使用して、 **attrib** コマンドに **-h** 隠しファイル属性を削除する **-s** システム ファイルの属性を削除するか、 **-h-s** 削除両方非表示にしてシステム ファイル属性。 非表示の後にファイルの属性が削除されていると、ファイルを削除することができます。

- **Rd**コマンドを使用して、現在のディレクトリを削除することはできません。 現在のディレクトリを削除しようとすると、次のエラーメッセージが表示されます。

    `The process can't access the file because it is being used by another process.`

    このエラーメッセージが表示された場合は、(現在のディレクトリのサブディレクトリではなく) 別のディレクトリに変更してから、再試行してください。

### <a name="examples"></a>例

目的のディレクトリを安全に削除できるように親ディレクトリに変更するには、次のように入力します。

```
cd ..
```

現在のディレクトリから*test* (およびそのすべてのサブディレクトリとファイル) という名前のディレクトリを削除するには、次のように入力します。

```
rd /s test
```

で非表示モードを、前の例を実行するには、次のように入力します。

```
rd /s /q test
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
