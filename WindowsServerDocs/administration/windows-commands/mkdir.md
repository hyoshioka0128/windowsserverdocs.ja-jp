---
title: mkdir
description: ディレクトリまたはサブディレクトリを作成する mkdir コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 033a57a2-5deb-4c98-aa78-61ce8df2a330
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 921e369cb1550bca8e26cc0beada4c1f5c1c3d5b
ms.sourcegitcommit: 5e313a004663adb54c90962cfdad9ae889246151
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84354602"
---
# <a name="mkdir"></a>mkdir

ディレクトリまたはサブディレクトリを作成します。 既定で有効になっているコマンド拡張機能では、単一の**mkdir**コマンドを使用して、指定されたパスに中間ディレクトリを作成することができます。

> [!NOTE]
> このコマンドは、 [md コマンド](md.md)と同じです。

## <a name="syntax"></a>構文

```
mkdir [<drive>:]<path>
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
mkdir Directory1
```

ルートディレクトリ内に、コマンド拡張機能が有効になっているディレクトリツリー *Taxes\Property\Current*を作成するには、次のように入力します。

```
mkdir \Taxes\Property\Current
```

前の例と同じようにルートディレクトリ内にディレクトリツリー *Taxes\Property\Current*を作成するには、コマンド拡張機能を無効にして、次の一連のコマンドを入力します。

```
mkdir \Taxes
mkdir \Taxes\Property
mkdir \Taxes\Property\Current
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [md コマンド](md.md)