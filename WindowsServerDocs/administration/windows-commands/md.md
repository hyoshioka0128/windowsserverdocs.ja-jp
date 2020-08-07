---
title: md
description: Md コマンドの参照記事。ディレクトリまたはサブディレクトリを作成します。
ms.topic: article
ms.assetid: 82162d00-cc34-4776-9e55-4b4836dbd6a9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 94dd8f696b97d56fe082f73287a3d50dc7f70883
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87886517"
---
# <a name="md"></a>md

ディレクトリまたはサブディレクトリを作成します。 既定で有効になっているコマンド拡張機能では、1 つを使用できます。 **md** 指定されたパスに中間ディレクトリを作成するコマンドです。

> [!NOTE]
> このコマンドは、 [mkdir コマンド](mkdir.md)と同じです。

## <a name="syntax"></a>構文

```
md [<drive>:]<path>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<drive>`: | 新しいディレクトリを作成するドライブを指定します。 |
| `<path>` | 新しいディレクトリの場所と名前を指定します。 1 つのパスの最大長は、ファイル システムによって決まります。 これは必須パラメーターです。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

### <a name="examples"></a>例

現在のディレクトリ内に*Directory1*という名前のディレクトリを作成するには、次のように入力します。

```
md Directory1
```

ルートディレクトリ内に、コマンド拡張機能が有効になっているディレクトリツリー *Taxes\Property\Current*を作成するには、次のように入力します。

```
md \Taxes\Property\Current
```

前の例と同じようにルートディレクトリ内にディレクトリツリー *Taxes\Property\Current*を作成するには、コマンド拡張機能を無効にして、次の一連のコマンドを入力します。

```
md \Taxes
md \Taxes\Property
md \Taxes\Property\Current
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [mkdir コマンド](mkdir.md)