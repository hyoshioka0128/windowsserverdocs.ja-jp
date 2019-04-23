---
title: pushd
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 396bc545-0f41-473e-b0ac-76fbbb74d390
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 548f39921c1f6aa3837e6443e396922396eb84f7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887463"
---
# <a name="pushd"></a>pushd



使用するための現在のディレクトリを格納、 **popd**コマンド、および指定したディレクトリに、変更します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
pushd [<Path>]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<パス >|現在のディレクトリを作成するディレクトリを指定します。 このコマンドは、相対パスをサポートします。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

-   使用するたびに、 **pushd**コマンドを使用するため、1 つのディレクトリが格納されています。 ただしを使用して複数のディレクトリを格納することができます、 **pushd**複数回のコマンドします。

    ディレクトリは、仮想のスタックに順番に格納されます。 使用する場合、 **pushd**コマンドの後、コマンドを使用するディレクトリは、スタックの一番下に置かれます。 コマンドをもう一度使用する場合は、2 番目のディレクトリが 1 つ目の上に配置されます。 使用するたびに、プロセスが繰り返されます、 **pushd**コマンド。

    使用することができます、 **popd**によって格納される最近ディレクトリに、現在のディレクトリを変更するコマンド、 **pushd**コマンド。 使用する場合、 **popd**コマンド、スタックの上部にあるディレクトリは、スタックから削除され、現在のディレクトリは、そのディレクトリに変更されます。 使用する場合、 **popd**コマンド スタックには、次のディレクトリの削除をもう一度、します。
-   コマンド拡張機能が有効な場合、 **pushd**コマンドは、ネットワーク パスまたはローカル ドライブ文字とパスを受け付けます。
-   ネットワーク パスを指定した場合、 **pushd**コマンドは、最高の未使用のドライブ文字を (Z で始まる) を一時的に割り当てます指定されたネットワーク リソース。 コマンドでは、新しく割り当てられたドライブ上の指定したディレクトリに、現在のドライブとディレクトリを変更します。 使用する場合、 **popd**コマンド拡張機能を有効にすると、コマンド、 **popd**コマンドによって作成されたドライブ文字の割り当てを削除します**pushd**します。

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

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)

[popd](popd.md)