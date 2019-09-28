---
ms.assetid: 835fc6f1-cc84-4189-b29a-dde90792469e
title: Fsutil ハードリンク
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: de9a04850555b11a42d74826685c249bea15710c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376877"
---
# <a name="fsutil-hardlink"></a>Fsutil ハードリンク
>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7

既存のファイルと新しいファイルの間にハードリンクを作成します。

## <a name="syntax"></a>構文

```
fsutil hardlink create <NewFileName> <ExistingFileName>
fsutil hardlink list <Filename>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------------|---------------|
|作成|既存のファイルと新しいファイルの間に NTFS ハードリンクを確立します。 (NTFS ハードリンクは POSIX ハードリンクに似ています)。|
|\<NewFileName >|ハードリンクを作成するファイルを指定します。|
|\<ExistingFileName >|ハードリンクの作成元となるファイルを指定します。|
|list|終わりの*ファイル名*を一覧表示します。<br /><br />このパラメーターは、次のものに適用されます。Windows Server 2008 R2 および Windows 7。|

## <a name="remarks"></a>コメント

-   ハードリンクは、ファイルのディレクトリエントリです。 すべてのファイルは、少なくとも1つのハードリンクを持つことができます。 NTFS ボリュームでは、各ファイルが複数のハードリンクを持つことができるので、1つのファイルを多数のディレクトリ (または同じディレクトリにあり、異なる名前でも) で表示できます。 すべてのリンクが同じファイルを参照するため、プログラムは任意のリンクを開いてファイルを変更できます。 ファイルへのすべてのリンクが削除された後にのみ、ファイルがファイルシステムから削除されます。 ハードリンクを作成すると、プログラムで他のファイル名と同じように使用できるようになります。

#### <a name="additional-references"></a>その他の参照情報
[コマンド ライン構文の記号](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)


