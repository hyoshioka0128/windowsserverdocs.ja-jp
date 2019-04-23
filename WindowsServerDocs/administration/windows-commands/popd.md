---
title: popd
description: 最近 pushd コマンドによって格納されているディレクトリにディレクトリを変更する方法について説明します。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 6da6dc9d1fc2d8965f8a081831cb1150375209a4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827463"
---
# <a name="popd"></a>popd

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

によって格納された最も最近ディレクトリに、現在のディレクトリを変更、 **pushd**コマンド。
このコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。

## <a name="syntax"></a>構文
```
popd
```

### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈
-   使用するたびに、 **pushd**コマンドを使用するため、1 つのディレクトリが格納されています。 ただしを使用して複数のディレクトリを格納することができます、 **pushd**複数回のコマンドします。
    ディレクトリは、仮想のスタックに順番に格納されます。 使用する場合、 **pushd**コマンドの後、コマンドを使用するディレクトリは、スタックの一番下に置かれます。 コマンドをもう一度使用する場合は、2 番目のディレクトリが 1 つ目の上に配置されます。 使用するたびに、プロセスが繰り返されます、 **pushd**コマンド。
    使用することができます、 **popd**によって格納される最近ディレクトリに、現在のディレクトリを変更するコマンド、 **pushd**コマンド。 使用する場合、 **popd**コマンド、スタックの上部にあるディレクトリは、スタックから削除され、現在のディレクトリは、そのディレクトリに変更されます。 使用する場合、 **popd**コマンド スタックには、次のディレクトリの削除をもう一度、します。
-   コマンド拡張機能が有効な場合、 **popd**コマンドによって作成された任意のドライブ文字の割り当てを削除します**pushd**します。

## <a name="BKMK_examples"></a>例
次の例を使用する方法を示しています、 **pushd**コマンドと**popd**コマンド バッチ プログラムが実行されたとして戻すから現在のディレクトリを変更するバッチ プログラム。

```
@echo off
rem This batch file deletes all .txt files in a specified directory
pushd %1
del *.txt
popd
cls
echo All text files deleted in the %1 directory
```

## <a name="additional-references"></a>その他の参照
-   [pushd](pushd.md)
-   [コマンドライン構文キー](command-line-syntax-key.md)

