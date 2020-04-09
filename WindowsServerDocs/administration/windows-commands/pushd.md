---
title: pushd
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 396bc545-0f41-473e-b0ac-76fbbb74d390
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e7866a54e83bd57c8689512a1b75b151f74cb93c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80837095"
---
# <a name="pushd"></a>pushd



**Popd**コマンドで使用する現在のディレクトリを格納し、指定されたディレクトリに変更します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
pushd [<Path>]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<パス >|現在のディレクトリを作成するディレクトリを指定します。 このコマンドは、相対パスをサポートしています。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>コメント

-   **Pushd**コマンドを使用するたびに、使用するために1つのディレクトリが格納されます。 ただし、 **pushd**コマンドを複数回使用して、複数のディレクトリを格納することができます。

    ディレクトリは、仮想スタックに連続して格納されます。 **Pushd**コマンドを1回使用すると、コマンドを使用するディレクトリがスタックの一番下に配置されます。 コマンドを再度使用すると、2つ目のディレクトリが最初のディレクトリの上に配置されます。 このプロセスは、 **pushd**コマンドを使用するたびに繰り返されます。

    **Popd**コマンドを使用して、現在のディレクトリを、 **pushd**コマンドによって最後に格納されたディレクトリに変更することができます。 **Popd**コマンドを使用すると、スタックの一番上にあるディレクトリがスタックから削除され、現在のディレクトリがそのディレクトリに変更されます。 **Popd**コマンドを再度使用すると、スタック上の次のディレクトリが削除されます。
-   コマンド拡張機能が有効になっている場合、 **pushd**コマンドはネットワークパスまたはローカルドライブ文字とパスのいずれかを受け取ります。
-   ネットワークパスを指定した場合、 **pushd**コマンドを実行すると、使用されていないドライブ文字 (Z: から始まる) が一時的に割り当てられます。指定されたネットワークリソース。 次に、コマンドは、現在のドライブとディレクトリを、新しく割り当てられたドライブの指定したディレクトリに変更します。 コマンド拡張機能が有効になっている**popd**コマンドを使用すると、 **pushd**によって作成されたドライブ文字の割り当てが削除**されます**。

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例**では、コマンドと**バッチプログラムで**popd**コマンドを使用して、バッチプログラムが実行されたディレクトリから現在のディレクトリを変更し、それを変更する方法を示しています。
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

[Popd](popd.md)