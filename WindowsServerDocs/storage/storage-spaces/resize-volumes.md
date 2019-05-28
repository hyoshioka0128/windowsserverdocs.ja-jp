---
title: 記憶域スペース ダイレクトのボリュームの拡張
description: 記憶域スペース ダイレクトの Windows Admin Center と PowerShell を使用してボリュームのサイズを変更する方法。
ms.prod: windows-server-threshold
ms.reviewer: cosmosdarwin
author: cosmosdarwin
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.date: 05/07/2019
ms.openlocfilehash: 3be6a4cda20f4d7d7d881ad8a272dc38fd787bba
ms.sourcegitcommit: 75f257d97d345da388cda972ccce0eb29e82d3bc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/14/2019
ms.locfileid: "65613227"
---
# <a name="extending-volumes-in-storage-spaces-direct"></a>記憶域スペース ダイレクトのボリュームの拡張
> 適用対象:Windows Server 2019、Windows Server 2016

このトピックでは上のボリュームのサイズを変更する手順、[記憶域スペース ダイレクト](storage-spaces-direct-overview.md)Windows Admin Center を使用してクラスター。

ボリュームのサイズを変更する方法の簡単なビデオをご覧ください。

> [!VIDEO https://www.youtube-nocookie.com/embed/hqyBzipBoTI]

## <a name="extending-volumes-using-windows-admin-center"></a>Windows Admin Center を使用してボリュームを拡張します。

1. Windows Admin Center で、記憶域スペース ダイレクト クラスターに接続し、**ボリューム**から、**ツール**ウィンドウ。
2. [ボリューム] ページで、選択、**インベントリ**タブ、およびサイズを変更するボリュームを選択します。

    ボリュームの詳細 ページで、ボリュームの記憶域容量が示されます。 ダッシュ ボードから直接、ボリュームの詳細ページを開くこともできます。 ダッシュ ボードの アラート ウィンドウでは、それを通知するボリュームの記憶域の容量が少なくなっています。 場合、アラートを選択し、**ボリュームに移動して**します。

4. ボリュームの詳細ページの上部にある次のように選択します。**サイズを変更する**します。
5. 新しいサイズを入力し、**サイズを変更する**します。

    ボリュームの詳細 ページで、ボリュームの大きな記憶域容量が示されるように、およびダッシュ ボードのアラートをクリアします。

## <a name="extending-volumes-using-powershell"></a>PowerShell を使用してボリュームの拡張

### <a name="capacity-in-the-storage-pool"></a>記憶域プールの容量

ボリュームのサイズを変更する前に、拡張された新しいフットプリントを収容するのに十分な容量が記憶域プールにあることを確認します。 たとえば、3 方向ミラーリング ボリュームを 1 TB から 2 TB に変更すると、そのフットプリントは 3 TB から 6 TB に増加します。 サイズ変更を正常に行うには、記憶域プールに使用か追うな容量が (6 - 3) = 3 TB 以上必要です。

### <a name="familiarity-with-volumes-in-storage-spaces"></a>記憶域スペース内のボリュームに関する知識

記憶域スペース ダイレクトでは、各ボリュームはスタックした複数のオブジェクト、つまりクラスター共有ボリューム (CSV) (ボリューム)、パーティション、ディスク (仮想ディスク)、1 つ以上の記憶域階層 (該当する場合) で構成されています。 ボリュームのサイズを変更するには、これらのオブジェクトのうち複数をサイズ変更する必要があります。

![SMAPI 内のボリューム](media/resize-volumes/volumes-in-smapi.png)

ボリュームについてよく知るため、PowerShell で対応する名詞を使って **Get-** を実行してみます。

例:

```PowerShell
Get-VirtualDisk
```

スタック内のオブジェクト間の関連付けに従うには、パイプを使って **Get-** コマンドレットを次のコマンドレットに渡します。

たとえば、仮想ディスクからそのボリュームを取得する方法を次に示します。

```PowerShell
Get-VirtualDisk <FriendlyName> | Get-Disk | Get-Partition | Get-Volume 
```

### <a name="step-1--resize-the-virtual-disk"></a>手順 1 - 仮想ディスクのサイズ変更

仮想ディスクは、作成方法によって記憶域階層を使うことも使わないこともあります。

確認するには、次のコマンドレットを実行します。

```PowerShell
Get-VirtualDisk <FriendlyName> | Get-StorageTier 
```

コマンドレットにより何も返されない場合、仮想ディスクは記憶域階層を使っていません。

#### <a name="no-storage-tiers"></a>記憶域階層なし

仮想ディスクに記憶域階層がない場合、**Resize-VirtualDisk** コマンドレットを使って直接サイズ変更できます。

**-Size** パラメーターで新しいサイズを指定します。

```PowerShell
Get-VirtualDisk <FriendlyName> | Resize-VirtualDisk -Size <Size>
```

**VirtualDisk** をサイズ変更すると、**Disk** も自動的に追従し、サイズ変更されます。

![仮想ディスクのサイズ変更](media/resize-volumes/Resize-VirtualDisk.gif)

#### <a name="with-storage-tiers"></a>記憶域階層あり

仮想ディスクが記憶域階層を使っている場合、**Resize-StorageTier** コマンドレットを使って各階層を別個にサイズ変更できます。

仮想ディスクからの関連付けに従うことにより、記憶域階層の名前を取得します。

```PowerShell
Get-VirtualDisk <FriendlyName> | Get-StorageTier | Select FriendlyName
```

次に、階層ごとに **-Size** パラメーターで新しいサイズを指定します。

```PowerShell
Get-StorageTier <FriendlyName> | Resize-StorageTier -Size <Size>
```

> [!TIP]
> 階層の物理的なメディアの種類 (**MediaType = SSD** や **MediaType = HDD** など) が異なる場合、各階層の拡張された新しいフットプリントを収容する容量が、メディアの種類ごとに十分記憶域プール内にあることを確認する必要があります。

**StorageTier** をサイズ変更すると、**VirtualDisk** と **Disk** も自動的に追従し、サイズ変更されます。

![記憶域階層のサイズ変更](media/resize-volumes/Resize-StorageTier.gif)

### <a name="step-2--resize-the-partition"></a>手順 2 - パーティションのサイズ変更

次に、**Resize-Partition** コマンドレットを使ってパーティションのサイズを変更します。 仮想ディスクには 2 つのパーティションが必要です。1 つは、変更できない予約パーティション、もう 1 つは **PartitionNumber = 2** および **Type = Basic** が設定された、サイズ変更が必要なパーティションです。

**-Size** パラメーターで新しいサイズを指定します。 以下に示すように、サポートされる最大サイズを使うことをお勧めします。

```PowerShell
# Choose virtual disk
$VirtualDisk = Get-VirtualDisk <FriendlyName>

# Get its partition
$Partition = $VirtualDisk | Get-Disk | Get-Partition | Where PartitionNumber -Eq 2

# Resize to its maximum supported size 
$Partition | Resize-Partition -Size ($Partition | Get-PartitionSupportedSize).SizeMax
```

**Partition** をサイズ変更すると、**Volume** と **ClusterSharedVolume** も自動的に追従し、サイズ変更されます。

![パーティションのサイズ変更](media/resize-volumes/Resize-Partition.gif)

以上で作業は終了です。

> [!TIP]
> **Get-Volume** を実行して、ボリュームが新しいサイズになっていることを確認できます。

## <a name="see-also"></a>関連項目

- [Windows Server 2016 での記憶域スペース ダイレクト](storage-spaces-direct-overview.md)
- [記憶域スペース ダイレクトのボリュームの計画](plan-volumes.md)
- [記憶域スペース ダイレクトのボリュームを作成します。](create-volumes.md)
- [記憶域スペース ダイレクトのボリュームを削除します。](delete-volumes.md)
