---
title: fsutil file
description: ユーザー名でファイルを検索する、ファイルに割り当てられた範囲を照会する、ファイルの短い名前を設定する、ファイルの有効なデータ長を設定する、ファイルのデータをゼロに設定する、または新しいファイルを作成する、fsutil file コマンドの参照記事。
manager: dmoss
ms.author: toklima
author: toklima
ms.assetid: 9f3dc104-dd69-4b03-b824-a29896780164
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 92b048d0ad3a7cb1f0c21dabf3cc14dc9850a251
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87889991"
---
# <a name="fsutil-file"></a>fsutil file

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8

ユーザー名でファイルを検索します (ディスククォータが有効になっている場合)。クエリを使用してファイルの短い名前を設定する、ファイルの有効なデータ長を設定する、ファイルのデータをゼロに設定する、または新しいファイルを作成します。

## <a name="syntax"></a>構文

```
fsutil file [createnew] <filename> <length>
fsutil file [findbysid] <username> <directory>
fsutil file [optimizemetadata] [/A] <filename>
fsutil file [queryallocranges] offset=<offset> length=<length> <filename>
fsutil file [queryextents] [/R] <filename> [<startingvcn> [<numvcns>]]
fsutil file [queryfileid] <filename>
fsutil file [queryfilenamebyid] <volume> <fileid>
fsutil file [queryoptimizemetadata] <filename>
fsutil file [queryvaliddata] [/R] [/D] <filename>
fsutil file [seteof] <filename> <length>
fsutil file [setshortname] <filename> <shortname>
fsutil file [setvaliddata] <filename> <datalength>
fsutil file [setzerodata] offset=<offset> length=<length> <filename>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| createnew | 指定された名前とサイズのファイルを、0で構成されるコンテンツと共に作成します。 |
| `<length>` | ファイルの有効なデータ長を指定します。 |
| findbysid | ディスククォータが有効になっている NTFS ボリューム上の、指定されたユーザーに属するファイルを検索します。 |
| `<username>` | ユーザーのユーザー名またはログオン名を指定します。 |
| `<directory>` | ディレクトリへの完全パスを指定します。たとえば、「C:\」と指定します。 |
| optimizemetadata | これにより、指定されたファイルのメタデータが即座に圧縮されます。 |
| /a | 最適化の前後にファイルのメタデータを分析します。 |
| queryallocranges | NTFS ボリューム上のファイルに割り当てられた範囲を照会します。 ファイルにスパース領域があるかどうかを判断する場合に便利です。 |
| オフセット =`<offset>` | 0に設定する範囲の先頭を指定します。 |
| 長さ =`<length>` | 範囲の長さ (バイト単位) を指定します。 |
| queryextents | ファイルのエクステントをクエリします。 |
| /r | <filename>が再解析ポイントである場合は、そのターゲットではなく開きます。 |
| `<startingvcn>` | クエリする最初の VCN を指定します。 省略した場合は、VCN 0 から開始します。 |
| `<numvcns>` | 照会する VCNs の数。 省略した場合、または0の場合は、EOF までクエリを実行します。 |
| queryfileid | NTFS ボリューム上のファイルのファイル ID を照会します。 |
| `<volume>` | ボリュームをドライブ名の後にコロンを続けて指定します。 |
| queryfilenamebyid | 指定したファイル ID のランダムなリンク名を NTFS ボリュームに表示します。 ファイルは、そのファイルをポイントする複数のリンク名を持つことができるため、ファイル名のクエリの結果としてどのファイルリンクが提供されるかは保証されません。 |
| `<fileid>` | NTFS ボリューム上のファイルの ID を指定します。 |
| queryoptimizemetadata | ファイルのメタデータの状態を照会します。 |
| queryvaliddata | ファイルの有効なデータ長を照会します。 |
| /d | 有効なデータの詳細情報を表示します。 |
| seteof | 指定されたファイルの EOF を設定します。 |
| setshortname | NTFS ボリューム上のファイルの短い名前 (長さは8.3 文字のファイル名) を設定します。 |
| `<shortname>` | ファイルの短い名前を指定します。 |
| setvaliddata | NTFS ボリューム上のファイルの有効なデータ長を設定します。 |
| `<datalength>` | ファイルの長さをバイト単位で指定します。 |
| データの setゼロ | ファイルの範囲 (*オフセット*と*長さ*で指定) をゼロに設定します。これにより、ファイルが空になります。 ファイルがスパースファイルの場合は、基になるアロケーションユニットがデコミットされます。 |

#### <a name="remarks"></a>Remarks

- NTFS には、ファイルの長さに関する重要な概念が2つあります。ファイルの終端 (EOF) マーカーと有効なデータ長 (VDL) です。 EOF は、ファイルの実際の長さを示します。 VDL は、ディスク上の有効なデータの長さを識別します。 VDL と EOF の間の読み取りでは、C2 オブジェクト再利用要件を維持するために、自動的に0が返されます。

- **Setvaliddata**パラメーターは、ボリュームの保守タスク (SeManageVolumePrivilege) の実行特権が必要なため、管理者のみが使用できます。 この機能は、高度なマルチメディアおよび System Area Network シナリオでのみ必要です。 **Setvaliddata**パラメーターには、現在の VDL よりも大きい正の値を指定する必要があります。ただし、現在のファイルサイズよりも小さくする必要があります。

    次の場合にプログラムで VDL を設定すると便利です。

    - ハードウェアチャネルを使用して raw クラスターを直接ディスクに書き込みます。 これにより、プログラムは、この範囲にユーザーに返される有効なデータが含まれていることをファイルシステムに通知することができます。

    - パフォーマンスが問題になる場合は、大きなファイルを作成します。 これにより、ファイルが作成または拡張されたときに、ファイルがゼロでいっぱいになるまでにかかる時間を回避できます。

### <a name="examples"></a>例

ドライブ C の*scottb*によって所有されているファイルを検索するには、次のように入力します。

```
fsutil file findbysid scottb c:\users
```

NTFS ボリューム上のファイルに割り当てられた範囲を照会するには、次のように入力します。

```
fsutil file queryallocranges offset=1024 length=64 c:\temp\sample.txt
```

ファイルのメタデータを最適化するには、次のように入力します。

```
fsutil file optimizemetadata C:\largefragmentedfile.txt
```

ファイルのエクステントを照会するには、次のように入力します。

```
fsutil file queryextents C:\Temp\sample.txt
```

ファイルの EOF を設定するには、次のように入力します。

```
fsutil file seteof C:\testfile.txt 1000
```

ファイルの短い名前を設定するには、ドライブ C で*longfile.txt*に*longfilename.txt* 、次のように入力します。

```
fsutil file setshortname c:\longfilename.txt longfile.txt
```

NTFS ボリューム上の*testfile.txt*という名前のファイルの有効なデータ長を*4096 バイト*に設定するには、次のように入力します。

```
fsutil file setvaliddata c:\testfile.txt 4096
```

NTFS ボリューム上のファイルの範囲をゼロに設定して空にするには、次のように入力します。

```
fsutil file setzerodata offset=100 length=150 c:\temp\sample.txt
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [fsutil](fsutil.md)
