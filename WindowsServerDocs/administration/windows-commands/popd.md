---
title: popd
description: Pushd コマンドによって最後に格納されたディレクトリにディレクトリを変更する方法について説明します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8a4c52d5-9fd1-4eac-9c0c-5767b25728ed
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: a1638f8d0d62b730578cb21fac5a74e58ad06b74
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723297"
---
# <a name="popd"></a>popd

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

現在のディレクトリを、 **pushd**コマンドによって最後に格納されたディレクトリに変更します。


## <a name="syntax"></a>構文
```
popd
```

#### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>Remarks
-   **Pushd**コマンドを使用するたびに、使用するために1つのディレクトリが格納されます。 ただし、 **pushd**コマンドを複数回使用して、複数のディレクトリを格納することができます。
    ディレクトリは、仮想スタックに連続して格納されます。 **Pushd**コマンドを1回使用すると、コマンドを使用するディレクトリがスタックの一番下に配置されます。 コマンドを再度使用すると、2つ目のディレクトリが最初のディレクトリの上に配置されます。 このプロセスは、 **pushd**コマンドを使用するたびに繰り返されます。
    **Popd**コマンドを使用して、現在のディレクトリを、 **pushd**コマンドによって最後に格納されたディレクトリに変更することができます。 **Popd**コマンドを使用すると、スタックの一番上にあるディレクトリがスタックから削除され、現在のディレクトリがそのディレクトリに変更されます。 **Popd**コマンドを再度使用すると、スタック上の次のディレクトリが削除されます。
-   コマンド拡張機能を有効にすると、 **pushd**によって作成されたドライブ文字の割り当てが削除**されます**。

## <a name="examples"></a><a name="BKMK_examples"></a>例
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
-   [pushd](pushd.md)
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)

