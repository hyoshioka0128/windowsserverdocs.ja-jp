---
title: tree
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: de22de1c9d62ba79c1aa68248109cca88009703a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872633"
---
# <a name="tree"></a>tree



グラフィカル ドライブまたはディスクのパスのディレクトリ構造を表示します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
tree [<Drive>:][<Path>] [/f] [/a]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ドライブ >:|ディレクトリ構造を表示するディスクを格納するドライブを指定します。|
|\<パス >|ディレクトリ構造を表示するディレクトリを指定します。|
|/f|各ディレクトリにファイルの名前が表示されます。|
|/a|指定します**ツリー**グラフィック文字ではなくサブディレクトリにリンクしている線を表示するテキストの文字を使用することです。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

によって表示される構造**ツリー**コマンド プロンプトで、指定したパラメーターに応じて異なります。 ドライブまたはパスを指定しない場合**ツリー**以降、現在のドライブの現在のディレクトリ ツリー構造が表示されます。

## <a name="BKMK_examples"></a>例

を現在のドライブのディスク上のすべてのサブディレクトリの名前を表示するには、次のように入力します。
```
tree \
```
C ドライブには、すべてのディレクトリ内のファイルを一度に 1 つの画面を表示します。 次のように入力します。
```
tree c:\ /f | more 
```
ドライブ C 上のすべてのディレクトリの一覧を印刷するに次のように入力します。
```
tree c:\ /f  prn 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)