---
ms.assetid: 9f3dc104-dd69-4b03-b824-a29896780164
title: fsutil ファイル
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: ffaf02f74f20f4eb94b94d8f0ffc51f26a62390e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59828123"
---
# <a name="fsutil-file"></a>fsutil ファイル
>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7

(ディスク クォータが有効になっている) 場合、ユーザー名でファイルを検索、ファイルに割り当てられた範囲をクエリ、ファイルの短い名前を設定、ファイルの有効なデータの長さを設定、ファイルの場合、ゼロのデータの設定または新しいファイルを作成します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

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

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------------|---------------|
|createnew|ゼロで構成されるコンテンツのサイズを指定した名前のファイルを作成します。|
|\<filename>|ファイル名と拡張子、たとえば C:\documents\filename.txt を含むファイルへの完全パスを指定します。|
|\<length>|ファイルの有効なデータ長を指定します。|
|findbysid|ディスク クォータが有効になっている NTFS ボリューム上の指定したユーザーに属するファイルを検索します。|
|\<username>|ユーザーのユーザー名またはログイン名を指定します。|
|\<directory>|たとえば C:\users ディレクトリにフルパスを指定します。|
|optimizemetadata|これは、指定されたファイルのメタデータの即時の圧縮を実行します。|
|/A|最適化前後のファイルのメタデータを分析します。|
|queryallocranges|NTFS ボリューム上のファイルに割り当てられた範囲クエリを実行します。 ファイルがスパースのリージョンにあるかどうかを決定するために便利です。|
|offset=\<offset>|ゼロに設定する範囲の開始を指定します。|
|length=\<length>|バイト単位で範囲の長さを指定します。|
|queryextents|ファイルのエクステントを照会します。|
|/R|場合<filename>は再解析ポイントよりも、そのターゲットを開きます。|
|\<startingvcn>|クエリするために、VCN 最初を指定します。 省略した場合は、ために、VCN 0 から始まります。|
|\<numvcns>|クエリを実行する VCNs の数。 場合は省略するか、0、EOF までクエリ。|
|queryfileid|NTFS ボリューム上のファイルのファイル ID を照会します。<br /><br />このパラメーターに適用されます。Windows Server 2008 R2 および Windows 7。|
|\<ボリューム >|ドライブ名の後にコロンと、ボリュームを指定します。|
|queryfilenamebyid|NTFS ボリューム上には、指定されたファイル ID のランダムなリンク名を表示します。 ファイルにはそのファイルを指す 2 つ以上のリンク名を設定できるためファイル名をクエリの結果としてファイル リンクが提供されることは限りません。<br /><br />このパラメーターに適用されます。Windows Server 2008 R2 および Windows 7。|
|\<fileid>|NTFS ボリューム上のファイルの ID を指定します。|
|queryoptimizemetadata|ファイルのメタデータの状態を照会します。|
|queryvaliddata|ファイルに有効なデータ長を照会します。|
|/D|有効なデータの詳細な情報を表示します。|
|seteof|指定されたファイルの EOF を設定します。|
|setshortname|NTFS ボリューム上のファイルの短い名前 (8.3 形式の文字長のファイル名) を設定します。|
|\<shortname>|ファイルの短い名前を指定します。|
|setvaliddata|NTFS ボリューム上のファイルの有効なデータ長を設定します。|
|\<datalength>|ファイルの長さをバイト単位で指定します。|
|setzerodata|範囲を設定 (で指定された*オフセット*と*長さ*) ファイルを空にする、ファイルをゼロにするには、。 ファイルがスパース ファイルの場合は、基になる、アロケーション ユニットは解除されます。|

## <a name="remarks"></a>注釈

-   NTFS は、ファイルの長さの 2 つの重要な概念: ファイル終端 (EOF) マーカーと有効なデータの長さ (VDL)。 EOF では、ファイルの実際の長さを示します。 VDL では、ディスク上の有効なデータの長さを指定します。 VDL と EOF の間で読み取りでは、0 C2 オブジェクトを保持するために再利用の要件を自動的に戻ります。

-   **Setvaliddata**パラメーターを実行するボリュームの保守タスク (SeManageVolumePrivilege) 特権を必要とするため、管理者だけです。 この機能が必要なだけマルチ メディアとシステム エリア ネットワークのシナリオの詳細。 **Setvaliddata**パラメーターは正の値は、現在の VDL よりも大きいが、現在のファイル サイズ未満である必要があります。

    VDL を設定するプログラムに対して有効な場合。

    -   ハードウェアのチャネルから直接ディスクに生のクラスターを記述します。 これにより、この範囲は、ユーザーに返すことができる有効なデータを含むファイル システムに通知するプログラムです。

    -   パフォーマンスが問題である場合は、大きなファイルを作成します。 ファイルが作成または拡張ファイルを 0 がいっぱいになるまでの時間を回避できます。

## <a name="BKMK_examples"></a>例
ドライブ C 上 scottb によって所有されているファイルを検索するには、次のように入力します。

```
fsutil file findbysid scottb c:\users  
```

NTFS ボリューム上のファイルに割り当てられた範囲をクエリするには、次のように入力します。

```
fsutil file queryallocranges offset=1024 length=64 c:\temp\sample.txt  
```

ファイルのメタデータを最適化するには、次のように入力します。

```
fsutil file optimizemetadata C:\largefragmentedfile.txt
```

ファイルのエクステントをクエリするには、次のように入力します。

```
fsutil file queryextents C:\Temp\sample.txt
```

ファイルに EOF を設定するには、次のように入力します。

```
fsutil file seteof C:\testfile.txt 1000
```

ドライブ C に Longfile.txt Longfilename.txt ファイルの短い名前を設定するに次のように入力します。

```
fsutil file setshortname c:\longfilename.txt longfile.txt  
```

有効なデータ長を 4096 バイトの NTFS ボリュームに Testfile.txt をという名前のファイルを設定するには、次のように入力します。

```
fsutil file setvaliddata c:\testfile.txt 4096  
```

NTFS ボリューム上のファイルの範囲を空にしてにゼロに設定するに次のように入力します。

```
fsutil file setzerodata offset=100 length=150 c:\temp\sample.txt  
```

#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文キー](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)


