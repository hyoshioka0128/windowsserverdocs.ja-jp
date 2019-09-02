---
title: ディスクを管理する
description: この記事では、ディスクを管理する方法について説明します。
ms.date: 06/07/2019
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 344dd363e970b195abe20fcb69e741c450fc7a21
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2019
ms.locfileid: "66812412"
---
# <a name="manage-disks"></a>ディスクを管理する

> **適用対象:** Windows 10、Windows 8.1、Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックと各サブトピックでは、ディスクの管理を使用してコンピューターのディスクを管理する方法について説明します。新しいディスクの初期化、異なるパーティション スタイル間でのディスクの変換、Windows で新しいディスクのオンライン状態を処理する方法についても説明します。

## <a name="online-and-offline-status"></a>オンラインとオフラインの状態

ディスクの管理では、ディスクがオンライン (使用可能) であるか、オフラインであるかが表示されます。

Windows の既定では、新しく検出されたすべてのディスクがオンラインになり、読み取り/書き込みアクセスが設定されます。 Windows Server の既定では、新しく検出されたディスクがオンラインになり、読み取り/書き込みアクセスが設定されます。ただし、共有バス (SCSI、iSCSI、Serial Attached SCSI、ファイバー チャネルなど) 上にある場合を除きます。 共有バス上のディスクは、初めて検出された時はオフラインです。

ディスクがオフラインの場合、ディスクを初期化したり、ディスク上にボリュームを作成したりするには、ディスクをオンラインにする必要があります。

ディスクをオンラインまたはオフラインにするには、ディスク名を右クリックし、適切な操作を選択します。

## <a name="see-also"></a>参照

-   [新しいディスクを初期化する](initialize-new-disks.md)
-   [ディスクを別のコンピューターに移動する](move-disks-to-another-computer.md)
-   [ダイナミック ディスクからベーシック ディスクへの再変換](change-a-dynamic-disk-back-to-a-basic-disk.md)
-   [マスター ブート レコード ディスクから GUID パーティション テーブル ディスクへの変換](change-an-mbr-disk-into-a-gpt-disk.md)
-   [GUID パーティション テーブル ディスクからマスター ブート レコード ディスクへの変換](change-a-gpt-disk-into-an-mbr-disk.md)
-   [仮想ハード ディスクを管理する](manage-virtual-hard-disks.md)