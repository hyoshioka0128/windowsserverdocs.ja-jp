---
ms.assetid: 0397c204-b3f8-4fd8-b71d-b7efb117766d
title: Fsutil ボリューム
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: c4496cfec94823ae177bc6de4fac83dc977fb61d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376698"
---
# <a name="fsutil-volume"></a>Fsutil ボリューム
>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7

ボリュームのマウントを解除するか、ハードディスクドライブに照会して、現在ハードディスクドライブで使用できる空き領域の大きさ、または特定のクラスターを使用しているファイルを特定します。

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
|割り当てレポート|特定のボリュームで記憶域がどのように使用されているかについての情報を表示します。|
|\<VolumePath >|ドライブ文字を指定します (その後にコロンが続きます)。|
|diskfree|ハードディスクドライブを照会して、空き領域の容量を確認します。|
|マウントの解除|ボリュームのマウントを解除します。|
|filelayout|指定されたファイルの NTFS メタデータを表示します。|
|\<fileid >|ファイル id を指定します。|
|list|システム上のすべてのボリュームを一覧表示します。|
|querycluster|指定されたクラスターを使用しているファイルを検索します。 **Querycluster**パラメーターを使用して複数のクラスターを指定できます。<br /><br />このパラメーターは、次のものに適用されます。Windows Server 2008 R2 および Windows 7。|
|\<cluster >|論理クラスター番号 (LCN) を指定します。|

## <a name="BKMK_examples"></a>例
割り当てられたクラスターレポートを表示するには、次のように入力します。

```
fsutil volume allocationreport C:
```

ドライブ C のボリュームのマウントを解除するには、次のように入力します。

```
fsutil volume dismount c:
```

ドライブ C のボリュームの空き領域の量を照会するには、次のように入力します。

```
fsutil volume diskfree c:
```

指定したファイルに関するすべての情報を表示するには、次のように入力します。

```
fsutil volume C: *
fsutil volume C:\Windows
fsutil volume C: 0x00040000000001bf
```

ディスク上のボリュームを一覧表示するには、次のように入力します。

```
fsutil volume list
```

論理クラスター番号50および0x2000 によって指定されたクラスターを使用しているファイルを検索するには、C ドライブに次のように入力します。

```
fsutil volume querycluster C: 50 0x2000
```

#### <a name="additional-references"></a>その他の参照情報
[コマンド ライン構文の記号](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)

[NTFS の動作](https://go.microsoft.com/fwlink/?LinkId=183396)


