---
title: popd
description: Pushd コマンドによって最後に格納されたディレクトリにディレクトリを変更する方法について説明します。
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8a4c52d5-9fd1-4eac-9c0c-5767b25728ed
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 8a9e0a301a5f8b46e1907a4f43c5ed9247b85f77
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372231"
---
# <a name="popd"></a>popd

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

現在のディレクトリを、 **pushd**コマンドによって最後に格納されたディレクトリに変更します。
このコマンドの使用方法の例については、「[例](#BKMK_examples)」を参照してください。

## <a name="syntax"></a>構文
```
popd
```

### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>コメント
-   **Pushd**コマンドを使用するたびに、使用するために1つのディレクトリが格納されます。 ただし、 **pushd**コマンドを複数回使用して、複数のディレクトリを格納することができます。
    ディレクトリは、仮想スタックに連続して格納されます。 **Pushd**コマンドを1回使用すると、コマンドを使用するディレクトリがスタックの一番下に配置されます。 コマンドを再度使用すると、2つ目のディレクトリが最初のディレクトリの上に配置されます。 このプロセスは、 **pushd**コマンドを使用するたびに繰り返されます。
    **Popd**コマンドを使用して、現在のディレクトリを、 **pushd**コマンドによって最後に格納されたディレクトリに変更することができます。 **Popd**コマンドを使用すると、スタックの一番上にあるディレクトリがスタックから削除され、現在のディレクトリがそのディレクトリに変更されます。 **Popd**コマンドを再度使用すると、スタック上の次のディレクトリが削除されます。
-   コマンド拡張機能を有効にすると、 **pushd**によって作成されたドライブ文字の割り当てが削除**されます**。

## <a name="BKMK_examples"></a>例
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
-   [pushd](pushd.md)
-   [コマンド ライン構文の記号](command-line-syntax-key.md)

