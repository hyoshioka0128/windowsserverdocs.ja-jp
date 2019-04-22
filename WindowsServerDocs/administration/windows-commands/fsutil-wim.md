---
ms.assetid: 6c6ff819-f349-4aea-b0be-1f637f631736
title: fsutil wim
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: c9186721ce4d3a549964e420cbc16d4893a1859d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826043"
---
# <a name="fsutil-wim"></a>fsutil wim
>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10

ファイルの Windows イメージの WIM バックアップを検出および管理機能を提供します。

## <a name="syntax"></a>構文

```
fsutil wim [enumfiles] <drive name> <data source>
fsutil wim [enumwims] <drive name>
fsutil wim [queryfile] <filename>
fsutil wim [removewim] <drive name> <data source>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------------|---------------|
|enumfiles|バックアップされた WIM ファイルを列挙します。|
|\<ドライブ名 >|ドライブ名を指定します。|
|\<データ ソース >|データ ソースを指定します。|
|enumwims|WIM ファイルのバックアップを列挙します。|
|queryfile|クエリによって、WIM ファイルがバックアップされている場合とそうである場合は、WIM ファイルの詳細を表示します。|
|\<filename>|ファイル名を指定します。|
|removewim|ファイルをバックアップからは、WIM を削除します。|




### <a name="examples"></a>例

データ ソースの 0 から c: ドライブのファイルを列挙するには、次のように入力します。

```
fsutil wim enumfiles C: 0
```

C: ドライブをバッキング WIM ファイルを列挙するには、次のように入力します。

```
fsutil wim enumwims C:
```

WIM でファイルをバックアップするかどうかについては、次のように入力します。

```
fsutil wim C:\Windows\Notepad.exe
```

C: ボリュームとデータ ソース 2 のファイルをバックアップから、wim ファイルを削除するに次のように入力します。

```
fsutil wim removewims C: 2
```

### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文キー](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)