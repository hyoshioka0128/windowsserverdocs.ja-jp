---
title: fsutil hardlink
description: Fsutil ハードリンクコマンドの参照記事。既存のファイルと新しいファイルの間にハードリンクを作成します。
manager: dmoss
ms.author: toklima
author: toklima
ms.assetid: 835fc6f1-cc84-4189-b29a-dde90792469e
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: f6a36be6c30e348ac488cfc2a8da7c312f64b3a6
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87889980"
---
# <a name="fsutil-hardlink"></a>fsutil hardlink

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8

既存のファイルと新しいファイルの間にハードリンクを作成します。 ハードリンクは、ファイルのディレクトリエントリです。 すべてのファイルは、少なくとも1つのハードリンクを持つことができます。

NTFS ボリュームでは、各ファイルが複数のハードリンクを持つことができるので、1つのファイルを多数のディレクトリ (または同じディレクトリにあり、異なる名前でも) で表示できます。 すべてのリンクが同じファイルを参照するため、プログラムは任意のリンクを開いてファイルを変更できます。 ファイルへのすべてのリンクが削除された後にのみ、ファイルがファイルシステムから削除されます。 ハードリンクを作成すると、プログラムで他のファイル名と同じように使用できるようになります。

## <a name="syntax"></a>構文

```
fsutil hardlink create <newfilename> <existingfilename>
fsutil hardlink list <filename>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| create | 既存のファイルと新しいファイルの間に NTFS ハードリンクを確立します。 (NTFS ハードリンクは POSIX ハードリンクに似ています)。 |
| \<newfilename> | ハードリンクを作成するファイルを指定します。 |
| \<existingfilename> | ハードリンクの作成元となるファイルを指定します。 |
| list | *ファイル名*へのハードリンクを一覧表示します。 |

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [fsutil](fsutil.md)
