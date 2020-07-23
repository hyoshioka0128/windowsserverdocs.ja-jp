---
ms.assetid: 898d72f1-01e7-4b87-8eb3-a8e0e2e6e6da
title: サーバーまたはドライブを記憶域スペース ダイレクトに追加する
ms.prod: windows-server
ms.author: cosdar
manager: dongill
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 11/06/2017
description: 記憶域スペースダイレクトクラスターにサーバーまたはドライブを追加する方法
ms.localizationpriority: medium
ms.openlocfilehash: 773bb3a55de27d049d26fa76659d3a4d8057f0fe
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86966394"
---
# <a name="adding-servers-or-drives-to-storage-spaces-direct"></a>サーバーまたはドライブを記憶域スペース ダイレクトに追加する

>適用先:Windows Server 2019、Windows Server 2016

このトピックでは、サーバーやドライブを記憶域スペース ダイレクトに追加する方法について説明します。

## <a name="adding-servers"></a><a name="adding-servers"></a>サーバーの追加

サーバーの追加 (スケール アウトとも呼ばれます) によって、記憶域容量が増えます。また、記憶域のパフォーマンスを向上したり、より優れた記憶域の効率を実現したりすることができます。 展開がハイパーコンバージされている場合、サーバーを追加すると、ワークロードのコンピューティング リソースも増えます。

![4ノードクラスターにサーバーを追加するアニメーション](media/add-nodes/Scaling-Out.gif)

一般的な展開では、サーバーを追加することで簡単にスケール アウトできます。 次の 2 つの手順を実行するだけです。

1. フェールオーバー クラスター スナップインを使用して[クラスター検証ウィザード](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732035(v=ws.10))を実行するか、PowerShell で **Test-Cluster** コマンドレットを使用します (管理者として実行)。 追加する新しいサーバーを含め *\<NewNode>* ます。

   ```PowerShell
   Test-Cluster -Node <Node>, <Node>, <Node>, <NewNode> -Include "Storage Spaces Direct", Inventory, Network, "System Configuration"
   ```

   この処理によって、新しいサーバーが Windows Server 2016 Datacenter Edition を実行していること、既存のサーバーとして同じ Active Directory Domain Services ドメインに参加していること、すべての必要な役割と機能があること、およびネットワークキングが適切に構成されていることが確認されます。

   >[!IMPORTANT]
   > 不要となった古いデータやメタデータが保存されているドライブを再利用している場合は、**Disk Management** または **Reset-PhysicalDisk** コマンドレットを使用して、それらのデータを消去します。 古いデータやメタデータが検出された場合、ドライブがプールされません。

2. クラスター上で次のコマンドレットを実行し、サーバーの追加を完了します。

```
Add-ClusterNode -Name NewNode 
```

   >[!NOTE]
   > 自動プール機能を使用するには、プール数が 1 つである必要があります。 複数のプールを作成するために標準構成を使用しない場合は、**追加の PhysicalDisk**を使用して、自分で優先プールに新しいドライブを追加する必要があります。

### <a name="from-2-to-3-servers-unlocking-three-way-mirroring"></a>サーバーを 2 台から 3 台にスケーリングする: 3 方向ミラーリングのロック解除

![2番目のサーバーを2ノードクラスターに追加する](media/add-nodes/Scaling-2-to-3.png)

サーバーが 2 台の場合は、双方向ミラーリングを行うボリュームを作成するだけです (分散型 RAID-1 に相当)。 サーバーが 3 台の場合は、3 方向ミラーリングを行うボリュームを作成して、フォールト トレランスを向上させることができます。 可能な限り、3 方向のミラーリングを使用することをお勧めします。

双方向ミラーリングを行うボリュームを、3 方向ミラーリングにインプレース アップグレードすることはできません。 代わりに、新しいボリュームを作成し、データをそのボリュームに移行して ([Storage Replica](../storage-replica/server-to-server-storage-replication.md) などを使用したコピー)、以前のボリュームを削除します。

3 方向ミラーリングのボリュームの作成を開始する場合、適切な方法がいくつかあります。 これらの方法は必要に応じて使用してください。 

#### <a name="option-1"></a>方法 1

新しいボリュームを作成するたびに、そのボリュームに対して **PhysicalDiskRedundancy = 2** を指定します。

```PowerShell
New-Volume -FriendlyName <Name> -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size <Size> -PhysicalDiskRedundancy 2
```

#### <a name="option-2"></a>方法 2

代わりに、プールの **ResiliencySetting** オブジェクト (名前は **Mirror**) に対して **PhysicalDiskRedundancyDefault = 2** を設定することもできます。 これにより、新しいミラー ボリュームでは、指定しなくても自動的に *3 方向*ミラーリングが使用されます。

```PowerShell
Get-StoragePool S2D* | Get-ResiliencySetting -Name Mirror | Set-ResiliencySetting -PhysicalDiskRedundancyDefault 2

New-Volume -FriendlyName <Name> -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size <Size>
```

#### <a name="option-3"></a>オプション 3

*Capacity* と呼ばれる **StorageTier** テンプレートに対して **PhysicalDiskRedundancy = 2** を設定し、その階層を参照してボリュームを作成します。

```PowerShell
Set-StorageTier -FriendlyName Capacity -PhysicalDiskRedundancy 2 

New-Volume -FriendlyName <Name> -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -StorageTierFriendlyNames Capacity -StorageTierSizes <Size>
```

### <a name="from-3-to-4-servers-unlocking-dual-parity"></a>サーバーを 3 台から 4 台にスケーリングする: デュアル パリティのロック解除

![4番目のサーバーを3ノードクラスターに追加する](media/add-nodes/Scaling-3-to-4.png)

サーバーが 4 台の場合は、デュアル パリティ (一般的にイレイジャー コーディングとも呼ばれます) を使用できます (分散型 RAID-6 に相当)。 3 方向ミラーリングと同じフォールト トレランスが実現されますが、記憶域の効率はより優れています。 詳しくは、「[フォールト トレランスと記憶域の効率](storage-spaces-fault-tolerance.md)」をご覧ください。

小規模な展開から始める場合は、デュアル パリティのボリュームを作成するための適切な方法がいくつかあります。 これらの方法は必要に応じて使用してください。

#### <a name="option-1"></a>方法 1

新しいボリュームを作成するたびに、そのボリュームに対して **PhysicalDiskRedundancy = 2** と **ResiliencySettingName = Parity** を指定します。

```PowerShell
New-Volume -FriendlyName <Name> -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size <Size> -PhysicalDiskRedundancy 2 -ResiliencySettingName Parity
```

#### <a name="option-2"></a>方法 2

プールの **ResiliencySetting** オブジェクト (名前は **Parity**) に対して **PhysicalDiskRedundancy = 2** を設定します。 これにより、新しいパリティ ボリュームでは、指定しなくても自動的に*デュアル* パリティが使用されます。

```PowerShell
Get-StoragePool S2D* | Get-ResiliencySetting -Name Parity | Set-ResiliencySetting -PhysicalDiskRedundancyDefault 2

New-Volume -FriendlyName <Name> -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size <Size> -ResiliencySettingName Parity
```

サーバーが 4 台あれば、個々のボリュームで一部がミラーリングを、一部がパリティを実行する、ミラーリングによって高速化されるパリティを使用することもできます。

この場合、4 台のサーバーで初めて **Enable-ClusterS2D** を実行したときの作成方法と同様に、*Performance* 階層と *Capacity* 階層の両方を持つように **StorageTier** テンプレートを更新する必要があります。 具体的には、データ格納用デバイス (SSD や HDD など) の **MediaType** と、**PhysicalDiskRedundancy = 2** を両方の階層に指定します。 *Performance* 階層には **ResiliencySettingName = Mirror**、*Capacity* 階層には **ResiliencySettingName = Parity** を指定します。

#### <a name="option-3"></a>オプション 3

単に既存の階層テンプレートを削除し、2 つの新しい階層を作成するのが一番簡単な方法です。 これは、階層テンプレートを参照することによって作成された既存のボリュームには影響しません。これはテンプレートにすぎません。

```PowerShell
Remove-StorageTier -FriendlyName Capacity

New-StorageTier -StoragePoolFriendlyName S2D* -MediaType HDD -PhysicalDiskRedundancy 2 -ResiliencySettingName Mirror -FriendlyName Performance
New-StorageTier -StoragePoolFriendlyName S2D* -MediaType HDD -PhysicalDiskRedundancy 2 -ResiliencySettingName Parity -FriendlyName Capacity
```

これで完了です。 これらの階層テンプレートを参照することにより、ミラーリングによってパリティが高速化されたボリュームを作成することができます。

#### <a name="example"></a>例

```PowerShell
New-Volume -FriendlyName "Sir-Mix-A-Lot" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -StorageTierFriendlyNames Performance, Capacity -StorageTierSizes <Size, Size> 
```

### <a name="beyond-4-servers-greater-parity-efficiency"></a>サーバーが 4 台を超える場合: パリティの効率の向上

サーバーの台数が 4 台を超えるスケーリングの場合、新しいボリュームによって、パリティ エンコーディングの効率が向上します。 たとえば、6 ～ 7 台のサーバーの場合、効率は 50.0% から 66.7% に改善されます。これは、(リード-ソロモン 2+2 ではなく) リード-ソロモン 4+2 を使用できるようになるためです。 この新しい効率を実現するために追加の手順は必要ありません。ボリュームを作成するたびに、最適なエンコーディングが自動的に決定されます。

ただし、既存のボリュームは新しい広範なエンコーディングに "変換" されません。** その理由の 1 つは、変換には、展開全体の文字通り*あらゆるビット*に影響を与える大量の計算が必要になるためです。 既存のデータを高い効率でエンコーディングできるようにするには、既存のデータを新しいボリュームに移行します。

詳しくは、「[フォールト トレランスと記憶域の効率](storage-spaces-fault-tolerance.md)」をご覧ください。

### <a name="adding-servers-when-using-chassis-or-rack-fault-tolerance"></a>シャーシやラックのフォールト トレランスの使用時にサーバーを追加する

シャーシやラックのフォールト トレランスを使用している展開の場合、新しいサーバーのシャーシまたはラックを指定してから、それをクラスターに追加する必要があります。 こうすることで、記憶域スペース ダイレクトにデータを分散する最適な方法を指示し、フォールト トレランスを最大化することができます。

1. 管理者特権の PowerShell セッションを開き、次のコマンドを使用して、ノードの一時的な障害ドメインを作成します。ここで、 *\<NewNode>* は新しいクラスターノードの名前です。

   ```PowerShell
   New-ClusterFaultDomain -Type Node -Name <NewNode> 
   ```

2. 次のように指定されているように、この一時的な障害ドメインを、新しいサーバーが実際に配置されているシャーシまたはラックに移動し *\<ParentName>* ます。

   ```PowerShell
   Set-ClusterFaultDomain -Name <NewNode> -Parent <ParentName> 
   ```

   詳細については、「[Fault domain awareness in Windows Server 2016](../../failover-clustering/fault-domains.md)」(Windows Server 2016 での障害ドメインの認識) を参照してください。

3. 「[サーバーの追加](#adding-servers)」に従ってクラスターにサーバーを追加します。 新しいサーバーがクラスターに参加すると、(その名前を使用して) プレースホルダー フォールト ドメインに自動的に関連付けられます。

## <a name="adding-drives"></a><a name="adding-drives"></a>ドライブの追加

ドライブの追加 (スケール アップとも呼ばれます) によって、記憶域容量が増え、パフォーマンスも改善できます。 空きスロットがある場合、サーバーを追加することなく、各サーバーにドライブを追加して記憶域容量を拡張することができます。 キャッシュ ドライブやデータ格納用ドライブはいつでも個別に追加できます。

   >[!IMPORTANT]
   > 同じ記憶域構成ですべてのサーバーを構成することを強くお勧めします。

![システムへのドライブの追加を示すアニメーション](media/add-nodes/Scale-Up.gif)

スケール アップするには、ドライブを接続し、Windows から検出されることを確認します。 PowerShell の **Get-PhysicalDisk** コマンドレットを使用し、**CanPool** プロパティを **True** に設定して実行すると、接続したドライブがコマンドレットの出力に表示されます。 **CanPool = False** と表示された場合、**CannotPoolReason** プロパティを調べることでその原因を確認できます。

```PowerShell
Get-PhysicalDisk | Select SerialNumber, CanPool, CannotPoolReason
```

短時間で、対象となるドライブは記憶域スペースダイレクトによって自動的に要求され、記憶域プールに追加されます。ボリュームは[、すべてのドライブに均等](https://techcommunity.microsoft.com/t5/storage-at-microsoft/deep-dive-the-storage-pool-in-storage-spaces-direct/ba-p/425959)に自動的に再分散されます。 以上で作業は終了です。[ボリュームを拡張](resize-volumes.md)したり、[新しいボリュームを作成](create-volumes.md)したりする準備が整いました。

ドライブが表示されない場合、ハードウェアの変更を手動でスキャンします。 スキャンするには、**デバイス マネージャー**の **[操作]** メニューを使用します。 古いデータまたはメタデータが含まれている場合は、再フォーマットすることを検討してください。 これを行うには、**[ディスクの管理]** を使用するか、**Reset-PhysicalDisk** コマンドレットを使用します。

   >[!NOTE]
   > 自動プール機能を使用するには、プール数が 1 つである必要があります。 複数のプールを作成するために標準構成を使用しない場合は、**追加の PhysicalDisk**を使用して、自分で優先プールに新しいドライブを追加する必要があります。

## <a name="optimizing-drive-usage-after-adding-drives-or-servers"></a>ドライブまたはサーバーを追加した後のドライブ使用率の最適化

ドライブを追加または削除すると、プール内のドライブ間でのデータの分散が不安定になることがあります。 場合によっては、特定のドライブがいっぱいになり、プール内の他のドライブの消費量がはるかに少なくなることがあります。

プール全体でもドライブ記憶域スペースダイレクトの割り当てを維持するために、ドライブまたはサーバーをプールに追加した後にドライブの使用率が自動的に最適化されます (これは、共有 SAS エンクロージャを使用する記憶域スペースシステムの手動プロセスです)。 プールに新しいドライブを追加すると、15分後に最適化が開始されます。 プールの最適化は、優先度の低いバックグラウンド操作として実行されるので、特に大容量ハードドライブを使用している場合は、完了までに数時間または数日かかることがあります。

最適化では2つのジョブが使用されます。1つは*Optimize* 、もう1つは再調整*と呼ばれ*、次のコマンドを使用して進行状況を監視できます。

```powershell
Get-StorageJob
```

記憶域プールは、 [optimize-storagepool](/powershell/module/storage/optimize-storagepool?view=win10-ps)コマンドレットを使用して手動で最適化できます。 次に例を示します。

```powershell
Get-StoragePool <PoolName> | Optimize-StoragePool
```
