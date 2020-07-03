---
title: fsutil volume
description: ボリュームのマウントを解除する、またはハードディスクドライブに照会して、ハードディスクドライブ上で現在使用可能な空き領域の容量や特定のクラスターを使用しているファイルを確認するには、fsutil volume コマンドの参照記事。
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
ms.assetid: 0397c204-b3f8-4fd8-b71d-b7efb117766d
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: aef1012cef33aeb2718dac4681b9119ea1a16590
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85929245"
---
# <a name="fsutil-volume"></a>fsutil volume

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8

ボリュームのマウントを解除するか、ハードディスクドライブに照会して、現在ハードディスクドライブで使用できる空き領域の大きさ、または特定のクラスターを使用しているファイルを特定します。

## <a name="syntax"></a>構文

```
fsutil volume [allocationreport] <volumepath>
fsutil volume [diskfree] <volumepath>
fsutil volume [dismount] <volumepath>
fsutil volume [filelayout] <volumepath> <fileID>
fsutil volume [list]
fsutil volume [querycluster] <volumepath> <cluster> [<cluster>] … …
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| 割り当てレポート | 特定のボリュームで記憶域がどのように使用されているかについての情報を表示します。 |
| `<volumepath>` | ドライブ文字を指定します (その後にコロンが続きます)。 |
| diskfree | ハードディスクドライブを照会して、空き領域の容量を確認します。 |
| マウントの解除 | ボリュームのマウントを解除します。 |
| filelayout | 指定されたファイルの NTFS メタデータを表示します。 |
| `<fileID>` | ファイル id を指定します。 |
| list | システム上のすべてのボリュームを一覧表示します。 |
| querycluster | 指定されたクラスターを使用しているファイルを検索します。 **Querycluster**パラメーターを使用して複数のクラスターを指定できます。 |
| `<cluster>` | 論理クラスター番号 (LCN) を指定します。 |

### <a name="examples"></a>例

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

- [fsutil](fsutil.md)

- [NTFS の動作](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc781134(v=ws.10))
