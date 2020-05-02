---
title: pushd
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 396bc545-0f41-473e-b0ac-76fbbb74d390
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e64c4f5090183b7d7b29dc7e040ffd94dc9d57ce
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722773"
---
# <a name="pushd"></a>pushd



**Popd**コマンドで使用する現在のディレクトリを格納し、指定されたディレクトリに変更します。



## <a name="syntax"></a>構文

```
pushd [<Path>]
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|\<パス>|現在のディレクトリを作成するディレクトリを指定します。 このコマンドは、相対パスをサポートしています。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>Remarks

-   **Pushd**コマンドを使用するたびに、使用するために1つのディレクトリが格納されます。 ただし、 **pushd**コマンドを複数回使用して、複数のディレクトリを格納することができます。

    ディレクトリは、仮想スタックに連続して格納されます。 **Pushd**コマンドを1回使用すると、コマンドを使用するディレクトリがスタックの一番下に配置されます。 コマンドを再度使用すると、2つ目のディレクトリが最初のディレクトリの上に配置されます。 このプロセスは、 **pushd**コマンドを使用するたびに繰り返されます。

    **Popd**コマンドを使用して、現在のディレクトリを、 **pushd**コマンドによって最後に格納されたディレクトリに変更することができます。 **Popd**コマンドを使用すると、スタックの一番上にあるディレクトリがスタックから削除され、現在のディレクトリがそのディレクトリに変更されます。 **Popd**コマンドを再度使用すると、スタック上の次のディレクトリが削除されます。
-   コマンド拡張機能が有効になっている場合、 **pushd**コマンドはネットワークパスまたはローカルドライブ文字とパスのいずれかを受け取ります。
-   ネットワークパスを指定した場合、 **pushd**コマンドを実行すると、使用されていないドライブ文字 (Z: から始まる) が一時的に割り当てられます。指定されたネットワークリソース。 次に、コマンドは、現在のドライブとディレクトリを、新しく割り当てられたドライブの指定したディレクトリに変更します。 コマンド拡張機能が有効になっている**popd**コマンドを使用すると、 **pushd**によって作成されたドライブ文字の割り当てが削除**されます**。

## <a name="examples"></a>例

コマンドを使用してバッチプログラム内の**popd**コマンドを実行し、バッチプログラムを実行したディレクトリから現在のディレクトリを変更してから、**次のよう**に変更する方法を説明します。
```
@echo off
rem This batch file deletes all .txt files in a specified directory
pushd %1
del *.txt
popd
cls
echo All text files deleted in the %1 directory
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

[Popd](popd.md)