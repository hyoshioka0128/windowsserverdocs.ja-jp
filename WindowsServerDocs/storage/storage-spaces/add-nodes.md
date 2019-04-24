---
ms.assetid: 898d72f1-01e7-4b87-8eb3-a8e0e2e6e6da
title: サーバーまたはドライブを記憶域スペース ダイレクトに追加する
ms.prod: windows-server-threshold
ms.author: cosdar
ms.manager: dongill
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 11/06/2017
description: サーバーまたはドライブを記憶域スペース ダイレクト クラスターに追加する方法
ms.localizationpriority: medium
ms.openlocfilehash: ae639b920788911dbc16952d7b61aab85b0a391b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833453"
---
# <a name="adding-servers-or-drives-to-storage-spaces-direct"></a>サーバーまたはドライブを記憶域スペース ダイレクトに追加する

>適用対象:Windows Server 2019、Windows Server 2016

このトピックでは、サーバーやドライブを記憶域スペース ダイレクトに追加する方法について説明します。

## <a name="adding-servers"></a> サーバーの追加

サーバーの追加 (スケール アウトとも呼ばれます) によって、記憶域容量が増えます。また、記憶域のパフォーマンスを向上したり、より優れた記憶域の効率を実現したりすることができます。 展開がハイパーコンバージされている場合、サーバーを追加すると、ワークロードのコンピューティング リソースも増えます。

![4 ノード クラスターにサーバーを追加するアニメーション](media/add-nodes/Scaling-Out.gif)

一般的な展開では、サーバーを追加することで簡単にスケール アウトできます。 次の 2 つの手順を実行するだけです。

1. フェールオーバー クラスター スナップインを使用して[クラスター検証ウィザード](https://technet.microsoft.com/library/cc732035(v=ws.10).aspx)を実行するか、PowerShell で **Test-Cluster** コマンドレットを使用します (管理者として実行)。 このとき、追加する新しいサーバー *\<NewNode>* を指定します。

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
   > 自動プール機能を使用するには、プール数が 1 つである必要があります。 標準構成を避けて複数のプールを作成した場合、**Add-PhysicalDisk** を使用して手動で目的のプールに新しいドライブを追加する必要があります。

### <a name="from-2-to-3-servers-unlocking-three-way-mirroring"></a>サーバーを 2 台から 3 台にスケーリングする: 3 方向ミラーリングのロック解除

![3 番目のサーバーを 2 ノード クラスターに追加します。](media/add-nodes/Scaling-2-to-3.png)

サーバーが 2 台の場合は、双方向ミラーリングを行うボリュームを作成するだけです (分散型 RAID-1 に相当)。 サーバーが 3 台の場合は、3 方向ミラーリングを行うボリュームを作成して、フォールト トレランスを向上させることができます。 可能な限り、3 方向ミラーリングを使用することをお勧めします。

双方向ミラーリングを行うボリュームを、3 方向ミラーリングにインプレース アップグレードすることはできません。 代わりに、新しいボリュームを作成し、データをそのボリュームに移行して ([Storage Replica](../storage-replica/server-to-server-storage-replication.md) などを使用したコピー)、以前のボリュームを削除します。

3 方向ミラーリングのボリュームの作成を開始する場合、適切な方法がいくつかあります。 これらの方法は必要に応じて使用してください。 

#### <a name="option-1"></a>オプション 1

新しいボリュームを作成するたびに、そのボリュームに対して **PhysicalDiskRedundancy = 2** を指定します。

```PowerShell
New-Volume -FriendlyName <Name> -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size <Size> -PhysicalDiskRedundancy 2
```

#### <a name="option-2"></a>オプション 2

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

![4 番目のサーバーを 3 ノード クラスターに追加します。](media/add-nodes/Scaling-3-to-4.png)

サーバーが 4 台の場合は、デュアル パリティ (一般的にイレイジャー コーディングとも呼ばれます) を使用できます (分散型 RAID-6 に相当)。 3 方向ミラーリングと同じフォールト トレランスが実現されますが、記憶域の効率はより優れています。 詳しくは、「[フォールト トレランスと記憶域の効率](storage-spaces-fault-tolerance.md)」をご覧ください。

小規模な展開から始める場合は、デュアル パリティのボリュームを作成するための適切な方法がいくつかあります。 これらの方法は必要に応じて使用してください。

#### <a name="option-1"></a>オプション 1

新しいボリュームを作成するたびに、そのボリュームに対して **PhysicalDiskRedundancy = 2** と **ResiliencySettingName = Parity** を指定します。

```PowerShell
New-Volume -FriendlyName <Name> -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size <Size> -PhysicalDiskRedundancy 2 -ResiliencySettingName Parity
```

#### <a name="option-2"></a>オプション 2

プールの **ResiliencySetting** オブジェクト (名前は **Parity**) に対して **PhysicalDiskRedundancy = 2** を設定します。 これにより、新しいパリティ ボリュームでは、指定しなくても自動的に*デュアル* パリティが使用されます。

```PowerShell
Get-StoragePool S2D* | Get-ResiliencySetting -Name Parity | Set-ResiliencySetting -PhysicalDiskRedundancyDefault 2

New-Volume -FriendlyName <Name> -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size <Size> -ResiliencySettingName Parity
```

サーバーが 4 台あれば、個々のボリュームで一部がミラーリングを、一部がパリティを実行する、ミラーリングによって高速化されるパリティを使用することもできます。

この場合、4 台のサーバーで初めて **Enable-ClusterS2D** を実行したときの作成方法と同様に、*Performance* 階層と *Capacity* 階層の両方を持つように **StorageTier** テンプレートを更新する必要があります。 具体的には、データ格納用デバイス (SSD や HDD など) の **MediaType** と、**PhysicalDiskRedundancy = 2** を両方の階層に指定します。 *Performance* 階層には **ResiliencySettingName = Mirror**、*Capacity* 階層には **ResiliencySettingName = Parity** を指定します。

#### <a name="option-3"></a>オプション 3

単に既存の階層テンプレートを削除し、2 つの新しい階層を作成するのが一番簡単な方法です。 この方法は、階層テンプレートを参照して作成された既存のボリュームには影響しません。テンプレートのみが影響を受けます。

```PowerShell
Remove-StorageTier -FriendlyName Capacity

New-StorageTier -StoragePoolFriendlyName S2D* -MediaType HDD -PhysicalDiskRedundancy 2 -ResiliencySettingName Mirror -FriendlyName Performance
New-StorageTier -StoragePoolFriendlyName S2D* -MediaType HDD -PhysicalDiskRedundancy 2 -ResiliencySettingName Parity -FriendlyName Capacity
```

以上で作業は終了です。 これらの階層テンプレートを参照することにより、ミラーリングによってパリティが高速化されたボリュームを作成することができます。

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

1. 管理者特権の PowerShell セッションを開き、次のコマンドを使用して、ノードに一時的なフォールト ドメインを作成します。この *\<NewNode>* は新しいクラスター ノードの名前です。

   ```PowerShell
   New-ClusterFaultDomain -Type Node -Name <NewNode> 
   ```

2. この一時的なフォールト ドメインを、新しいサーバーを実際に配置するシャーシまたはラックに移行します (*\<ParentName>* で指定します)。

   ```PowerShell
   Set-ClusterFaultDomain -Name <NewNode> -Parent <ParentName> 
   ```

   詳しくは、「[Windows Server 2016 での障害ドメインの認識](../../failover-clustering/fault-domains.md)」をご覧ください。

3. 「[サーバーの追加](#adding-servers)」に従ってクラスターにサーバーを追加します。 新しいサーバーがクラスターに参加すると、(その名前を使用して) プレースホルダー フォールト ドメインに自動的に関連付けられます。

## <a name="adding-drives"></a> ドライブの追加

ドライブの追加 (スケール アップとも呼ばれます) によって、記憶域容量が増え、パフォーマンスも改善できます。 空きスロットがある場合、サーバーを追加することなく、各サーバーにドライブを追加して記憶域容量を拡張することができます。 キャッシュ ドライブやデータ格納用ドライブはいつでも個別に追加できます。

   >[!IMPORTANT]
   > 同じ記憶域構成ですべてのサーバーを構成することを強くお勧めします。

![システムにドライブを追加することを示すアニメーション](media/add-nodes/Scale-Up.gif)

スケール アップするには、ドライブを接続し、Windows から検出されることを確認します。 PowerShell の **Get-PhysicalDisk** コマンドレットを使用し、**CanPool** プロパティを **True** に設定して実行すると、接続したドライブがコマンドレットの出力に表示されます。 **CanPool = False** と表示された場合、**CannotPoolReason** プロパティを調べることでその原因を確認できます。

```PowerShell
Get-PhysicalDisk | Select SerialNumber, CanPool, CannotPoolReason
```

短時間で、記憶域スペース ダイレクトから対象のドライブに自動的に要求が送信され、記憶域プールに追加されます。ボリュームは、自動的に、[すべてのドライブ全体で均等に再分散されます](https://blogs.technet.microsoft.com/filecab/2016/11/21/deep-dive-pool-in-spaces-direct/)。 以上で作業は終了です。[ボリュームを拡張](resize-volumes.md)したり、[新しいボリュームを作成](create-volumes.md)したりする準備が整いました。

ドライブが表示されない場合、ハードウェアの変更を手動でスキャンします。 スキャンするには、**デバイス マネージャー**の **[操作]** メニューを使用します。 古いデータまたはメタデータが含まれている場合は、再フォーマットすることを検討してください。 これを行うには、**[ディスクの管理]** を使用するか、**Reset-PhysicalDisk** コマンドレットを使用します。

   >[!NOTE]
   > 自動プール機能を使用するには、プール数が 1 つである必要があります。 標準構成を避けて複数のプールを作成した場合、**Add-PhysicalDisk** を使用して手動で目的のプールに新しいドライブを追加する必要があります。

## <a name="optimizing-drive-usage-after-adding-drives-or-servers"></a>ドライブまたはサーバーを追加した後のドライブ使用率を最適化します。

時間の経過と共にドライブが追加または削除されると、プール内のドライブ間でデータの分布になりますが不均等になります。 場合によっては、その結果で特定のドライブがいっぱいプール内の他のドライブがある程度消費の削減になります。

プール全体でもドライブの割り当てに保つためには、記憶域スペース ダイレクトが自動的に最適化ドライブ使用率 (これは、エンクロージャの共有の SAS を使用する記憶域スペースのシステムの手動プロセス) プールにドライブやサーバーを追加した後。 最適化では、プールに新しいドライブを追加した後、15 分を開始します。 プールの最適化のため、かかる時間または日で完了すると、特に大容量のハード ドライブを使用している場合、優先順位の低いバック グラウンド操作として実行します。

最適化と呼ばれる 1 つの 2 つのジョブを使用して*最適化*もう 1 つ*を再調整*- し、次のコマンドでその進行状況を監視できます。

```powershell
Get-StorageJob
```

記憶域プールを手動で最適化することができます、 [Optimize-storagepool](https://docs.microsoft.com/powershell/module/storage/optimize-storagepool?view=win10-ps)コマンドレット。 次に例を示します。

```powershell
Get-StoragePool <PoolName> | Optimize-StoragePool
```
