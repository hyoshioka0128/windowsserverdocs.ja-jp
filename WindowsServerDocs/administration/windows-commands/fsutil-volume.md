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
ms.openlocfilehash: 587ff48bd0af80667f9a336323641b87be808b1d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843935"
---
# <a name="fsutil-volume"></a>Fsutil ボリューム
>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7

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

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------------|---------------|
|割り当てレポート|特定のボリュームで記憶域がどのように使用されているかについての情報を表示します。|
|\<VolumePath >|ドライブ文字を指定します (その後にコロンが続きます)。|
|diskfree|ハードディスクドライブを照会して、空き領域の容量を確認します。|
|dismount|ボリュームのマウントを解除します。|
|filelayout|指定されたファイルの NTFS メタデータを表示します。|
|\<fileid >|ファイル id を指定します。|
|リスト|システム上のすべてのボリュームを一覧表示します。|
|querycluster|指定されたクラスターを使用しているファイルを検索します。 **Querycluster**パラメーターを使用して複数のクラスターを指定できます。<p>このパラメーターは、Windows Server 2008 R2 と Windows 7 に適用されます。|
|クラスター > の \<|論理クラスター番号 (LCN) を指定します。|

## <a name="examples"></a><a name="BKMK_examples"></a>例
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

## <a name="additional-references"></a>その他の参照情報
- [コマンド ライン構文の記号](command-line-syntax-key.md)

[Fsutil](Fsutil.md)

[NTFS の動作](https://go.microsoft.com/fwlink/?LinkId=183396)


