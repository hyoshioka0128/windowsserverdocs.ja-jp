---
title: 記憶域スペース ダイレクトのボリュームの拡張
description: Windows 管理センターと PowerShell を使用して記憶域スペースダイレクトのボリュームのサイズを変更する方法。
ms.reviewer: cosmosdarwin
author: cosmosdarwin
ms.author: cosdar
manager: eldenc
ms.date: 03/10/2020
ms.openlocfilehash: dccc8d25505fb1ac94af81b23334b7f8639dcc01
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971079"
---
# <a name="extending-volumes-in-storage-spaces-direct"></a>記憶域スペース ダイレクトのボリュームの拡張
> 適用先:Windows Server 2019、Windows Server 2016

このトピックでは、Windows 管理センターを使用して[記憶域スペースダイレクト](storage-spaces-direct-overview.md)クラスター上のボリュームのサイズを変更する手順について説明します。

> [!WARNING]
> **サポート対象外: 記憶域スペース ダイレクトで使用される基盤のストレージのサイズ変更。** Azure を含む仮想ストレージ環境で記憶域スペース ダイレクトを実行している場合、仮想マシンが使用する記憶装置のサイズ変更や特性変更はサポートされず、それを行うとデータにアクセスできなくなります。 代わりに、ボリュームを拡張する前に、[サーバーまたはドライブの追加](add-nodes.md)に関するセクションの手順に従って、容量を追加してください。

ボリュームのサイズを変更する方法に関する簡単な動画をご覧ください。

> [!VIDEO https://www.youtube-nocookie.com/embed/hqyBzipBoTI]

## <a name="extending-volumes-using-windows-admin-center"></a>Windows Admin Center を使用したボリュームの拡張

1. Windows Admin Center で、記憶域スペース ダイレクト クラスターに接続し、 **[ツール]** ペインで **[ボリューム]** を選択します。
2. [ボリューム] ページで **[インベントリ]** タブを選択し、サイズを変更するボリュームを選択します。

    ボリュームの詳細ページに、ボリュームのストレージ容量が表示されます。 ボリュームの詳細ページは、ダッシュボードから直接開くこともできます。 ダッシュボードの [アラート] ペインで、ボリュームのストレージ容量が不足している場合に通知が表示されるアラートを選択し、 **[Go To Volume]\(ボリュームへ移動\)** を選択します。

4. ボリュームの詳細ページの上部で、 **[サイズ変更]** を選択します。
5. より大きな新しいサイズを入力し、 **[サイズ変更]** を選択します。

    ボリュームの詳細ページに、ボリュームのストレージ容量が大きいことが示され、ダッシュボードのアラートがクリアされます。

## <a name="extending-volumes-using-powershell"></a>PowerShell を使用したボリュームの拡張

### <a name="capacity-in-the-storage-pool"></a>記憶域プールの容量

ボリュームのサイズを変更する前に、より大きな新しい占有領域に対応できる十分な容量が記憶域プールにあることを確認してください。 たとえば、3 方向ミラー ボリュームのサイズを 1 TB から 2 TB に変更すると、その占有領域は 3 TB から 6 TB に増えます。 サイズ変更を正常に実行するには、記憶域プールに少なくとも 3 TB (6 - 3) の使用可能な容量が必要です。

### <a name="familiarity-with-volumes-in-storage-spaces"></a>記憶域スペースのボリュームに関する知識

記憶域スペース ダイレクトでは、各ボリュームは、クラスターの共有ボリューム (CSV) (ボリューム)、パーティション、ディスク(仮想ディスク)、および複数のストレージ層 (該当する場合) の、複数のスタックされたオブジェクトで構成されます。 ボリュームのサイズを変更するには、これらのオブジェクトのいくつかのサイズを変更する必要があります。

![volumes-in-smapi](media/resize-volumes/volumes-in-smapi.png)

これらに慣れるために、PowerShell で対応する名詞を使用して **Get-** を実行してみてください。

次に例を示します。

```PowerShell
Get-VirtualDisk
```

スタック内のオブジェクト間の関連付けを辿るには、1 つの **Get-** コマンドレットを次のものにパイプ処理します。

たとえば、仮想ディスクからそのボリュームまでを取得する方法を次に示します。

```PowerShell
Get-VirtualDisk <FriendlyName> | Get-Disk | Get-Partition | Get-Volume
```

### <a name="step-1--resize-the-virtual-disk"></a>手順 1 – 仮想ディスクのサイズを変更する

仮想ディスクは、作成方法に応じてストレージ層を使用する場合と使用しない場合があります。

確認するには、次のコマンドレットを実行します。

```PowerShell
Get-VirtualDisk <FriendlyName> | Get-StorageTier
```

コマンドレットから何も返されない場合、仮想ディスクはストレージ層を使用しません。

#### <a name="no-storage-tiers"></a>ストレージ層なし

仮想ディスクにストレージ層がない場合は、**Resize-VirtualDisk** コマンドレットを使用してそのサイズを直接変更できます。

**-Size** パラメーターに新しいサイズを指定します。

```PowerShell
Get-VirtualDisk <FriendlyName> | Resize-VirtualDisk -Size <Size>
```

**VirtualDisk** のサイズを変更すると、それに応じて **Disk** のサイズも自動的に変更されます。

![Resize-VirtualDisk](media/resize-volumes/Resize-VirtualDisk.gif)

#### <a name="with-storage-tiers"></a>ストレージ層あり

仮想ディスクがストレージ層を使用している場合は、**Resize-StorageTier** コマンドレットを使用して、各層のサイズを個別に変更できます。

仮想ディスクからの関連付けを辿って、ストレージ層の名前を取得します。

```PowerShell
Get-VirtualDisk <FriendlyName> | Get-StorageTier | Select FriendlyName
```

次に、各層ごとに、 **-Size** パラメーターに新しいサイズを指定します。

```PowerShell
Get-StorageTier <FriendlyName> | Resize-StorageTier -Size <Size>
```

> [!TIP]
> 使用する層の物理メディアの種類が異なる場合 (**MediaType = SSD** および **MediaType = HDD** など)、各層のより大きな新しい占有領域に対応するために、記憶域プール内に各メディアの種類の十分な容量を確保する必要があります。

**StorageTier** のサイズを変更すると、それに応じて **VirtualDisk** と **Disk** のサイズも自動的に変更されます。

![Resize-StorageTier](media/resize-volumes/Resize-StorageTier.gif)

### <a name="step-2--resize-the-partition"></a>手順 2 – パーティションのサイズを変更する

次に、**Resize-Partition** コマンドレットを使用してパーティションのサイズを変更します。 仮想ディスクに 2 つのパーティションがあることが想定されています。最初のものは予約済みであり、変更しないでください。サイズ変更が必要なものは、**PartitionNumber = 2** および **Type = Basic** です。

**-Size** パラメーターに新しいサイズを指定します。 次に示すように、サポートされている最大サイズを使用することをお勧めします。

```PowerShell
# Choose virtual disk
$VirtualDisk = Get-VirtualDisk <FriendlyName>

# Get its partition
$Partition = $VirtualDisk | Get-Disk | Get-Partition | Where PartitionNumber -Eq 2

# Resize to its maximum supported size
$Partition | Resize-Partition -Size ($Partition | Get-PartitionSupportedSize).SizeMax
```

**Partition** のサイズを変更すると、それに応じて **Volume** と **ClusterSharedVolume** のサイズも自動的に変更されます。

![Resize-Partition](media/resize-volumes/Resize-Partition.gif)

これで完了です。

> [!TIP]
> **Get-Volume** を実行すると、ボリュームに新しいサイズが設定されたことを確認できます。

## <a name="additional-references"></a>その他の参照情報

- [Windows Server 2016 での記憶域スペース ダイレクト](storage-spaces-direct-overview.md)
- [記憶域スペース ダイレクトのボリュームの計画](plan-volumes.md)
- [記憶域スペース ダイレクトのボリュームの作成](create-volumes.md)
- [記憶域スペースダイレクトのボリュームの削除](delete-volumes.md)
