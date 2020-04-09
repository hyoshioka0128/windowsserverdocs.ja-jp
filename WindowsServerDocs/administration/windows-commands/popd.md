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
ms.openlocfilehash: b66b5edd2fa068923650f578d13f30631a8602ad
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80837475"
---
# <a name="popd"></a>popd

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

現在のディレクトリを、 **pushd**コマンドによって最後に格納されたディレクトリに変更します。
このコマンドの使用方法の例については、「[例](#BKMK_examples)」を参照してください。

## <a name="syntax"></a>構文
```
popd
```

#### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>コメント
-   **Pushd**コマンドを使用するたびに、使用するために1つのディレクトリが格納されます。 ただし、 **pushd**コマンドを複数回使用して、複数のディレクトリを格納することができます。
    ディレクトリは、仮想スタックに連続して格納されます。 **Pushd**コマンドを1回使用すると、コマンドを使用するディレクトリがスタックの一番下に配置されます。 コマンドを再度使用すると、2つ目のディレクトリが最初のディレクトリの上に配置されます。 このプロセスは、 **pushd**コマンドを使用するたびに繰り返されます。
    **Popd**コマンドを使用して、現在のディレクトリを、 **pushd**コマンドによって最後に格納されたディレクトリに変更することができます。 **Popd**コマンドを使用すると、スタックの一番上にあるディレクトリがスタックから削除され、現在のディレクトリがそのディレクトリに変更されます。 **Popd**コマンドを再度使用すると、スタック上の次のディレクトリが削除されます。
-   コマンド拡張機能を有効にすると、 **pushd**によって作成されたドライブ文字の割り当てが削除**されます**。

## <a name="examples"></a><a name="BKMK_examples"></a>例
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
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)

