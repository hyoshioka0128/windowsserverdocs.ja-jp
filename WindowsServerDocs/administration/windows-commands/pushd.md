---
title: pushd
description: Pushd コマンドの参照記事。 popd コマンドで使用する現在のディレクトリを格納し、指定されたディレクトリに変更します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 396bc545-0f41-473e-b0ac-76fbbb74d390
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 871834ae1ac29eb53be982831e7ede93d9d309cf
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933750"
---
# <a name="pushd"></a>pushd

**Popd**コマンドで使用する現在のディレクトリを格納し、指定されたディレクトリに変更します。

**Pushd**コマンドを使用するたびに、使用するために1つのディレクトリが格納されます。 ただし、 **pushd**コマンドを複数回使用して、複数のディレクトリを格納することができます。 ディレクトリは仮想スタックに連続して格納されるため、 **pushd**コマンドを1回使用すると、コマンドを使用するディレクトリがスタックの一番下に配置されます。 コマンドを再度使用すると、2つ目のディレクトリが最初のディレクトリの上に配置されます。 このプロセスは、 **pushd**コマンドを使用するたびに繰り返されます。

**Popd**コマンドを使用すると、スタックの一番上にあるディレクトリが削除され、現在のディレクトリがそのディレクトリに変更されます。 **Popd**コマンドを再度使用すると、スタック上の次のディレクトリが削除されます。 コマンド拡張機能が有効になっている場合は、 **pushd**コマンドによって作成されたドライブ文字の割り当てが削除**されます**。

## <a name="syntax"></a>構文

```
pushd [<path>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|--|--|
| `<path>` | 現在のディレクトリを作成するディレクトリを指定します。 このコマンドは、相対パスをサポートしています。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>注釈

- コマンド拡張機能が有効になっている場合、 **pushd**コマンドはネットワークパスまたはローカルドライブ文字とパスのいずれかを受け取ります。

- ネットワークパスを指定した場合、 **pushd**コマンドを実行すると、使用されていないドライブ文字 (Z: から始まる) が一時的に割り当てられます。指定されたネットワークリソース。 次に、コマンドは、現在のドライブとディレクトリを、新しく割り当てられたドライブの指定したディレクトリに変更します。 コマンド拡張機能が有効になっている**popd**コマンドを使用すると、 **pushd**によって作成されたドライブ文字の割り当てが削除**されます**。

### <a name="examples"></a>例

バッチプログラムが実行されたディレクトリから現在のディレクトリを変更し、それを元に戻すには、次のようにします。

```
@echo off
rem This batch file deletes all .txt files in a specified directory
pushd %1
del *.txt
popd
cls
echo All text files deleted in the %1 directory
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [popd コマンド](popd.md)
