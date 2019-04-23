---
ms.assetid: 7787a72e-a26b-415f-b700-a32806803478
title: fsutil fsinfo
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 434dfde2286538367fb96d168b06983cb4357067
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873043"
---
# <a name="fsutil-fsinfo"></a>fsutil fsinfo
>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7

すべてのドライブを一覧表示、ドライブの種類のクエリを実行、ボリューム情報の照会、NTFS に固有のボリューム情報、クエリを実行またはファイル システムの統計情報をクエリします。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
fsutil fsinfo [drives]
fsutil fsinfo [drivetype] <VolumePath>
fsutil fsinfo [ntfsinfo] <RootPath>
fsutil fsinfo [statistics] <VolumePath>
fsutil fsinfo [volumeinfo] <RootPath>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------------|---------------|
|ドライブ|コンピューターのすべてのドライブを一覧表示します。|
|drivetype|ドライブを照会し、その型では、たとえば CD-ROM ドライブを一覧表示します。|
|ntfsinfo|セクター、合計のクラスター、無料のクラスターでは、開始および MFT ゾーンの最後の数など、指定されたボリュームの NTFS の特定のボリューム情報を一覧表示します。|
|sectorinfo|ハードウェアのセクター サイズと配置に関する情報を一覧表示します。|
|統計情報|ファイルのメタデータ、ログ ファイル、および MFT 読み取りおよび書き込みなどの指定ボリュームのシステムの統計情報を一覧表示します。|
|volumeinfo|ファイル システムなどの指定ボリュームの情報を一覧表示し、ディスク クォータ、または、DirectAccess (DAX) ボリューム、ボリュームは、大文字小文字を区別するファイル名をファイル名の unicode をサポートしているかどうか。|
|<"VolumePath">|ドライブ文字 (コロンに続く) を指定します。|
|<"RootPathname">|ルート ドライブのドライブ文字 (コロンに続く) を指定します。|

## <a name="BKMK_examples"></a>例
すべてのコンピューターでドライブを一覧表示するには、次のように入力します。

```
fsutil fsinfo drives
```

次のような出力:

```
Drives: A:\ C:\ D:\ E:\       
```

C ドライブのドライブの種類をクエリするには、次のように入力します。

```
fsutil fsinfo drivetype c:
```

クエリの結果は次のとおりです。

```
Unknown Drive
No such Root Directory
Removable Drive, for example floppy
Fixed Drive
Remote/Network Drive
CD-ROM Drive
Ram Disk
```

ボリューム E のボリューム情報を照会するには、次のように入力します。

```
fsinfo volumeinfo e:\
```

次のような出力:

```
Volume Name :Volume
Serial Number : 0xd0b634d9
Max Component Length : 255
File System Name : NTFS
.
.
.
Supports Named Streams
Is DAX Volume
```

ドライブ F NTFS に固有のボリューム情報のクエリに次のように入力します。

```
fsutil fsinfo ntfsinfo f:
```

次のような出力:

```
NTFS Volume Serial Number : 0xe660d46a60d442cb
Number Sectors :            0x00000000010ea04f
Total Clusters :            0x000000000021d409
.
.
.
Mft Zone End   :            0x0000000000004700       
```

セクターについては、ファイル システムの基になるハードウェアをクエリするには、次のように入力します。

```
fsinfo sectorinfo d:
```

次のような出力:

```
D:\>fsutil fsinfo sectorinfo d:
LogicalBytesPerSector :                                 4096
PhysicalBytesPerSectorForAtomicity :                    4096
.
.
.
Trim Not Supported
DAX capable
```

ドライブ E のファイル システムの統計情報を照会するには、次のように入力します。

```
fsinfo statistics e:
```

次のような出力:

```
File System Type :     NTFS
Version :              1
UserFileReads :        75021
UserFileReadBytes :    1305244512
.
.
.
LogFileWriteBytes :    180936704       
```

#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文キー](Command-Line-Syntax-Key.md)
[Fsutil](Fsutil.md)


