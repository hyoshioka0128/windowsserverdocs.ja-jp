---
title: mklink
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0ce4df22-2dbc-48fc-9c16-b721ae85f857
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e4bfa1c928b5bc5f4c5a885378f0f1d1c9b99cf5
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2020
ms.locfileid: "83437137"
---
# <a name="mklink"></a>mklink
シンボリック リンクを作成します。



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
|\<リンク>|作成されるシンボリック リンクの名前を指定します。|
|\<Target>|新しいシンボリック リンクを指すパス (相対パスまたは絶対パス) を指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="examples"></a>例

MyFolder という名前のシンボリックリンクの作成と削除を、ルートディレクトリから \Users\User1\Documents ディレクトリに、ディレクトリ内にあるファイルの例を次に示します。
```
mklink /d \MyFolder \Users\User1\Documents
mklink /h \MyFile.file \User1\Documents\example.file
rd \MyFolder
del \MyFile.file
```
## <a name="additional-references"></a>その他のリファレンス
-   [新規-項目](https://docs.microsoft.com/powershell/module/microsoft.powershell.management/new-item?view=powershell-6)
-   [del](https://docs.microsoft.com/windows-server/administration/windows-commands/del)
-   [rmdir](https://docs.microsoft.com/windows-server/administration/windows-commands/rd)
