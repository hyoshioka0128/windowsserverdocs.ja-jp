---
title: mklink
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0ce4df22-2dbc-48fc-9c16-b721ae85f857
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3d6328d972b07b1bebd272788b896fd491e47380
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80839555"
---
# <a name="mklink"></a>mklink
シンボリック リンクを作成します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
mklink [[/d] | [/h] | [/j]] <Link> <Target>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/d|ディレクトリのシンボリック リンクを作成します。 既定では、 **mklink** ファイルのシンボリック リンクを作成します。|
|/h|シンボリック リンクの代わりにハード リンクを作成します。|
|/j|ディレクトリの分岐点を作成します。|
|\<リンク >|作成されるシンボリック リンクの名前を指定します。|
|\<ターゲット >|新しいシンボリック リンクを指すパス (相対パスまたは絶対パス) を指定します。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="examples"></a><a name=BKMK_examples></a>例

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
