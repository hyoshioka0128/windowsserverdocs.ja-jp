---
title: "仮想ハード ディスク (VHD) の管理"
description: "この記事では、仮想ハード ディスクを管理する方法について説明します。"
ms.date: 10/12/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 2e371710752d59ebc7a1f8aa2dad3d9189872c47
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="manage-virtual-hard-disks-vhd"></a>仮想ハード ディスク (VHD) の管理

> **適用対象:** Windows 10、Windows 8.1、Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックでは、ディスクの管理を使用して、仮想ハード ディスクを作成、アタッチ、デタッチする方法について説明します。 仮想ハード ディスク (VHD) は仮想化されたハード ディスク ファイルで、一度マウントされると、物理ハード ドライブとほぼ同様に表示され、動作します。 仮想ハード ディスクは、Hyper-V 仮想マシンで最もよく使用されます。 

## <a name="viewing-vhds-in-disk-management"></a>ディスクの管理で VHD を表示する

ディスクの管理では、VHD は物理ディスクと同じように表示されます。 VHD がアタッチされている (つまり、システムで使用できる) 場合、VHD は青で表示されます。 ディスクがデタッチされる (つまり、使用できなくなる) と、そのアイコンは灰色に戻ります。

## <a name="creating-a-vhd"></a>VHD を作成する

> [!NOTE]
> 以下の手順を実行するには、少なくとも **Backup Operators** または **Administrators** グループのメンバーである必要があります。

**VHD を作成するには**

1.  **[アクション]** メニューで、**[VHD の作成]** を選択します。

2.  **[仮想ハード ディスクの作成と接続**] ダイアログ ボックスで、VHD ファイルを格納する物理コンピューター上の場所と、VHD のサイズの両方を指定します。

3.  **[仮想ハード ディスク フォーマット]** で **[容量可変]** または **[容量固定]** を選択し、**[OK]** をクリックします。

## <a name="attaching-and-detaching-a-vhd"></a>VHD をアタッチおよびデタッチする

VHD (先ほど作成した VHD または別の既存の VHD) を使用できるようにするには、以下の手順を実行します。 

1. **[アクション]** メニューで、**[VHD の接続]** を選択します。

2. 完全修飾パスを使用して、VHD の場所を指定します。

VHD をデタッチして使用できないようにするには、ディスクを右クリックし、**[VHD の切断]** を選択して、**[OK]** をクリックします。 VHD をデタッチしても、VHD や VHD に格納されているデータは削除されません。

## <a name="additional-considerations"></a>その他の考慮事項

-   VHD の場所を指定するパスは、完全修飾パスである必要があり、\\Windows ディレクトリにすることはできません。
-   VHD の最小サイズは、3 メガバイト (MB) です。
-   VHD に設定できるのは、ベーシック ディスクのみです。
-   VHD は作成時に初期化されるため、大容量の固定サイズの VHD を作成すると、時間がかかる可能性があります。
