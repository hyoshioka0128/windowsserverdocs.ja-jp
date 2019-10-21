---
title: mklink
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: b7a5f9b819f16d058feb1dee74a8408ed174e04c
ms.sourcegitcommit: b7f55949f166554614f581c9ddcef5a82fa00625
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72588049"
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
|\<Link >|作成されるシンボリック リンクの名前を指定します。|
|\<Target >|新しいシンボリック リンクを指すパス (相対パスまたは絶対パス) を指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="BKMK_examples"></a>例

次の例では、MyFolder という名前のシンボリックリンクと、ルートディレクトリから \Users\User1\Documents ディレクトリへのファイルの作成と削除、およびディレクトリ内のファイルの例を示します。
```
mklink /d \MyFolder \Users\User1\Documents
mklink /h \MyFile.file \User1\Documents\example.file
rd \MyFolder
del \MyFile.file
```
## <a name="additional-references"></a>その他の参照情報
-   [新規-項目](https://docs.microsoft.com/powershell/module/microsoft.powershell.management/new-item?view=powershell-6)
-   [del](https://docs.microsoft.com/windows-server/administration/windows-commands/del)
-   [rmdir](https://docs.microsoft.com/windows-server/administration/windows-commands/rd)
