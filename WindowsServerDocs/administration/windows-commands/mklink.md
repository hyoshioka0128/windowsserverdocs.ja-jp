---
title: mklink
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0ce4df22-2dbc-48fc-9c16-b721ae85f857
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: eabbf159a64ab5df7f45ece390d0c2fdb9956b80
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826333"
---
# <a name="mklink"></a>mklink
シンボリック リンクを作成します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
mklink [[/d] | [/h] | [/j]] <Link> <Target>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/d|ディレクトリのシンボリック リンクを作成します。 既定では、 **mklink** ファイルのシンボリック リンクを作成します。|
|/h|シンボリック リンクの代わりにハード リンクを作成します。|
|/j|ディレクトリの分岐点を作成します。|
|\<リンク >|作成されるシンボリック リンクの名前を指定します。|
|\<ターゲット >|新しいシンボリック リンクを指すパス (相対パスまたは絶対パス) を指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="BKMK_examples"></a>例

\Users\User1\Documents ディレクトリへのルート ディレクトリから MyDocs をという名前のシンボリック リンクを作成するには、次のように入力します。
```
mklink /d \MyDocs \Users\User1\Documents
```
## <a name="additional-references"></a>その他の参照情報
-   [新しい項目](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.management/new-item?view=powershell-6)
