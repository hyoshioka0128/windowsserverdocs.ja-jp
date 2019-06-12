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
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812412"
---
# <a name="manage-disks"></a>ディスクを管理する

> **適用対象します。** Windows 10、Windows 8.1、Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックとサブトピックのコンピューターでディスクの管理ディスクの管理の使用について説明し、別のパーティションのスタイル、および Windows が新しいディスクのオンライン状態を処理する方法の間でのディスクに変換する、新しいディスクを初期化する方法についての情報が含まれます。

## <a name="online-and-offline-status"></a>オンラインとオフラインの状態

ディスクの管理は、ディスクがオンラインかどうかが表示されます (入手可能)、またはオフラインです。

Windows の既定では、新しく検出されたすべてのディスクがオンラインになり、読み取り/書き込みアクセスが設定されます。 Windows Server の既定では、新しく検出されたディスクがオンラインになり、読み取り/書き込みアクセスが設定されます。ただし、共有バス (SCSI、iSCSI、Serial Attached SCSI、ファイバー チャネルなど) 上にある場合を除きます。 共有バス上のディスクが初めて検出されたオフラインです。

ディスクがオフラインの場合、ディスクを初期化したり、ディスク上にボリュームを作成したりするには、ディスクをオンラインにする必要があります。

ディスクをオンラインまたはオフラインには、ディスク名と適切なアクションを選択して右クリックします。

## <a name="see-also"></a>関連項目

-   [新しいディスクを初期化する](initialize-new-disks.md)
-   [ディスクを別のコンピューターに移動します。](move-disks-to-another-computer.md)
-   [ダイナミック ディスクからベーシック ディスクへの再変換](change-a-dynamic-disk-back-to-a-basic-disk.md)
-   [マスター ブート レコード ディスクを GUID パーティション テーブル ディスクに変更します。](change-an-mbr-disk-into-a-gpt-disk.md)
-   [GUID パーティション テーブル ディスクをマスター ブート レコード ディスクに変更します。](change-a-gpt-disk-into-an-mbr-disk.md)
-   [仮想ハード ディスクを管理する](manage-virtual-hard-disks.md)