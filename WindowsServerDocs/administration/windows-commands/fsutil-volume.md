---
ms.assetid: 0397c204-b3f8-4fd8-b71d-b7efb117766d
title: fsutil ボリューム
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: a8576dce4be639a516f8898e78bb6db12c91e171
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882453"
---
# <a name="fsutil-volume"></a>fsutil ボリューム
>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7

ボリュームのマウントを解除またはハード ディスク ドライブの空き領域の量は、ハード ディスク ドライブで現在利用またはファイルは、特定のクラスターを使用してクエリを実行します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
fsutil volume [allocationreport] <VolumePath>
fsutil volume [diskfree] <VolumePath>
fsutil volume [dismount] <VolumePath>
fsutil volume [filelayout] <VolumePath> <fileid>
fsutil volume [list]
fsutil volume [querycluster] <VolumePath> <Cluster> [<Cluster>] … …
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------------|---------------|
|allocationreport|指定したボリューム上の記憶域の使用方法についての情報を表示します。|
|\<VolumePath >|ドライブ文字 (コロンに続く) を指定します。|
|diskfree|ハード ディスク ドライブに空き領域の量を決定するクエリを実行します。|
|マウントの解除|ボリュームのマウントを解除します。|
|filelayout|指定されたファイルの NTFS メタデータが表示されます。|
|\<fileid>|ファイル id を指定します。|
|list|すべてのシステムのボリュームの一覧を表示します。|
|querycluster|どのファイルが指定されたクラスターを使用して検索します。 複数のクラスターを指定することができます、 **querycluster**パラメーター。<br /><br />このパラメーターに適用されます。Windows Server 2008 R2 および Windows 7。|
|\<クラスター >|論理クラスター番号 (LCN) を指定します。|

## <a name="BKMK_examples"></a>例
割り当てられたクラスター、レポートを表示するには、次のように入力します。

```
fsutil volume allocationreport C:
```

ドライブ C 上のボリュームをマウント解除には、次のように入力します。

```
fsutil volume dismount c:
```

ドライブ C 上のボリュームの空き領域の量を照会するには、次のように入力します。

```
fsutil volume diskfree c:
```

指定されたファイルに関するすべての情報を表示するには、次のように入力します。

```
fsutil volume C: *
fsutil volume C:\Windows
fsutil volume C: 0x00040000000001bf
```

ディスク上のボリュームを一覧表示するには、次のように入力します。

```
fsutil volume list
```

50 および 0x2000、C ドライブの論理クラスター番号で指定された、クラスターを使用しているファイルを検索するには、次のように入力します。

```
fsutil volume querycluster C: 50 0x2000
```

#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文キー](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)

[NTFS のしくみ](https://go.microsoft.com/fwlink/?LinkId=183396)


