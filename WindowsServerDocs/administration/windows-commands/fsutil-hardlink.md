---
ms.assetid: 835fc6f1-cc84-4189-b29a-dde90792469e
title: fsutil hardlink
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 69474bd1817471176598afba508cd80c8fa1df8a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840053"
---
# <a name="fsutil-hardlink"></a>fsutil hardlink
>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7

既存のファイルと新しいファイルのハード リンクを作成します。

## <a name="syntax"></a>構文

```
fsutil hardlink create <NewFileName> <ExistingFileName>
fsutil hardlink list <Filename>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------------|---------------|
|作成|既存のファイルと新しいファイルの間に、NTFS ハード リンクを確立します。 (NTFS のハード リンクは、POSIX のハード リンクと似ています)。|
|\<NewFileName>|ハード リンクを作成するファイルを指定します。|
|\<ExistingFileName >|ハード リンクを作成するファイルを指定します。|
|list|ハードリンクを一覧表示*Filename*します。<br /><br />このパラメーターに適用されます。Windows Server 2008 R2 および Windows 7。|

## <a name="remarks"></a>注釈

-   ハード リンクは、ファイルのディレクトリ エントリです。 すべてのファイルは、少なくとも 1 つのハード リンクを持つと見なさことができます。 NTFS ボリュームで各ファイルは 1 つのファイルは、多くのディレクトリ (または、別の名前と同じディレクトリ内) を表示できるように複数のハード リンクを持つことができます。 すべてのリンクは、同じファイルを参照するため、プログラムは、リンクを開くし、ファイルを変更します。 ファイルは、すべてのリンクが削除された後にのみ、ファイル システムから削除されます。 ハード リンクを作成したら、プログラムの他の任意のファイル名のように使用できます。

#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文キー](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)


