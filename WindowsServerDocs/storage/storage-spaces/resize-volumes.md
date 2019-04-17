---
title: 記憶域スペース ダイレクトのボリュームの拡張
ms.assetid: fa48f8f7-44e7-4a0b-b32d-d127eff470f0
ms.prod: windows-server-threshold
ms.author: cosmosdarwin
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 01/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51f58ec23c55a6cb1664d800d6f4a75dae545899
ms.sourcegitcommit: dfd25348ea3587e09ea8c2224237a3e8078422ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2018
ms.locfileid: "4678651"
---
# 記憶域スペース ダイレクトのボリュームの拡張
> 適用対象: Windows Server 2019、Windows Server 2016

このトピックでは、[記憶域スペース ダイレクト](storage-spaces-direct-overview.md)でボリュームのサイズを変更する手順について説明します。

## 前提条件

### 記憶域プールの容量

ボリュームのサイズを変更する前に、拡張された新しいフットプリントを収容するのに十分な容量が記憶域プールにあることを確認します。 たとえば、3 方向ミラーリング ボリュームを 1 TB から 2 TB に変更すると、そのフットプリントは 3 TB から 6 TB に増加します。 サイズ変更を正常に行うには、記憶域プールに使用か追うな容量が (6 - 3) = 3 TB 以上必要です。

### 記憶域スペース内のボリュームに関する知識

記憶域スペース ダイレクトでは、各ボリュームはスタックした複数のオブジェクト、つまりクラスター共有ボリューム (CSV) (ボリューム)、パーティション、ディスク (仮想ディスク)、1 つ以上の記憶域階層 (該当する場合) で構成されています。 ボリュームのサイズを変更するには、これらのオブジェクトのうち複数をサイズ変更する必要があります。

![SMAPI 内のボリューム](media/resize-volumes/volumes-in-smapi.png)

ボリュームについてよく知るため、PowerShell で対応する名詞を使って **Get-** を実行してみます。

次に、例を示します。

```PowerShell
Get-VirtualDisk
```

スタック内のオブジェクト間の関連付けに従うには、パイプを使って **Get-** コマンドレットを次のコマンドレットに渡します。

たとえば、仮想ディスクからそのボリュームを取得する方法を次に示します。

```PowerShell
Get-VirtualDisk <FriendlyName> | Get-Disk | Get-Partition | Get-Volume 
```

## 手順 1 - 仮想ディスクのサイズ変更

仮想ディスクは、作成方法によって記憶域階層を使うことも使わないこともあります。

確認するには、次のコマンドレットを実行します。

```PowerShell
Get-VirtualDisk <FriendlyName> | Get-StorageTier 
```

コマンドレットにより何も返されない場合、仮想ディスクは記憶域階層を使っていません。

### 記憶域階層なし

仮想ディスクに記憶域階層がない場合、**Resize-VirtualDisk** コマンドレットを使って直接サイズ変更できます。

**-Size** パラメーターで新しいサイズを指定します。

```PowerShell
Get-VirtualDisk <FriendlyName> | Resize-VirtualDisk -Size <Size>
```

**VirtualDisk** をサイズ変更すると、**Disk** も自動的に追従し、サイズ変更されます。

![仮想ディスクのサイズ変更](media/resize-volumes/Resize-VirtualDisk.gif)

### 記憶域階層あり

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

## 手順 2 - パーティションのサイズ変更

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

## 関連項目

- [Windows Server 2016 の記憶域スペース ダイレクト](storage-spaces-direct-overview.md)
- [記憶域スペース ダイレクトのボリュームの計画](plan-volumes.md)
- [記憶域スペース ダイレクトのボリュームの作成](create-volumes.md)
