---
title: tree
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 345d3192-401e-4a3b-a8ac-36a85c7be79d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 22875e63526dc3465021c9aa990f6cea388b81e4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385621"
---
# <a name="tree"></a>tree



ドライブのパスまたはディスクのディレクトリ構造をグラフィカルに表示します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
tree [<Drive>:][<Path>] [/f] [/a]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ドライブ >:|ディレクトリ構造を表示するディスクを含むドライブを指定します。|
|\<パス >|ディレクトリ構造を表示するディレクトリを指定します。|
|/f|各ディレクトリ内のファイルの名前が表示されます。|
|/a|**ツリー**で、サブディレクトリをリンクする行を表示するために、グラフィック文字の代わりにテキスト文字を使用することを指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

**ツリー**によって表示される構造は、コマンドプロンプトで指定するパラメーターによって異なります。 ドライブまたはパスを指定しない場合は、現在のドライブの現在のディレクトリで始まるツリー構造が**ツリー**に表示されます。

## <a name="BKMK_examples"></a>例

現在のドライブのディスクにあるすべてのサブディレクトリの名前を表示するには、次のように入力します。
```
tree \
```
一度に1つの画面を表示するには、C ドライブ上のすべてのディレクトリのファイルを次のように入力します。
```
tree c:\ /f | more 
```
C ドライブのすべてのディレクトリの一覧を印刷するには、次のように入力します。
```
tree c:\ /f  prn 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)