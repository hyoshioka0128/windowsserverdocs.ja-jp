---
title: 記憶域レプリカに関する既知の問題
ms.prod: windows-server-threshold
manager: siroy
ms.author: nedpyle
ms.technology: storage-replica
ms.topic: get-started-article
author: nedpyle
ms.date: 04/26/2019
ms.assetid: ceddb0fa-e800-42b6-b4c6-c06eb1d4bc55
ms.openlocfilehash: da0a7b309bd671b8dfde2dab7d1736ed0d2f722d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447563"
---
# <a name="known-issues-with-storage-replica"></a>記憶域レプリカに関する既知の問題

>適用対象:Windows Server 2019、Windows Server 2016、Windows Server (半期チャネル)

このトピックでは、Windows Server での記憶域レプリカに関する既知の問題について説明します。

## <a name="after-removing-replication-disks-are-offline-and-you-cannot-configure-replication-again"></a>レプリケーションの削除後ディスクがオフラインになり、再度レプリケーションを構成することができない

Windows Server 2016 では、以前レプリケートされていたボリューム上でレプリケーションをプロビジョニングできないことや、マウントできないボリュームが見つかることがあります。 これは、何らかのエラー状態によりレプリケーションを削除できない場合、または以前データをレプリケートしていたコンピューターにオペレーティング システムを再インストールする場合に発生する可能性があります。  

この問題を修正するには、`Clear-SRMetadata` コマンドレットを使用し、非表示の記憶域レプリカのパーティションをディスクから削除して、書き込み可能な状態に戻す必要があります。  

-   孤立したすべての記憶域レプリカ パーティション データベース スロットを削除し、すべてのパーティションを再マウントするには、次のように `-AllPartitions` パラメーターを使用します。  

    ```  
    Clear-SRMetadata -AllPartitions  
    ```  

-   孤立したすべての記憶域レプリカのログ データを削除するには、次のように `-AllLogs` パラメーターを使用します。  

    ```  
    Clear-SRMetadata -AllLogs  
    ```  

-   孤立したすべてのフェールオーバー クラスターの構成データを削除するには、次のように `-AllConfiguration` パラメーターを使用します。  

    ```  
    Clear-SRMetadata -AllConfiguration  
    ```  

-   個々 のレプリケーション グループのメタデータを削除するには、次のように、`-Name` パラメーターを使用してレプリケーション グループを指定します。  

    ```  
    Clear-SRMetadata -Name RG01 -Logs -Partition  
    ```  

パーティション データベースのクリーンアップ後にサーバーの再起動が必要になる場合があります。これは `-NoRestart` によって一時的に抑制することができますが、サーバーの再起動がコマンドレットによって要求された場合、スキップすることはできません。 このコマンドレットは、データ ボリュームやこれらのボリュームに含まれるデータを削除しません。  

## <a name="during-initial-sync-see-event-log-4004-warnings"></a>初回同期時にイベント ログ 4004 の警告が表示される  
Windows Server 2016 では、レプリケーションの構成時にレプリケーション元と先の両方のサーバーで、初回同期のたびに **StorageReplica\Admin** イベント ログ 4004 の警告 "システム リソースが不足するため、API を終了できません" が複数回表示されることがあります。 5014 エラーも表示される可能性があります。 これは、初回同期とワークロードの実行の両方を行うのに十分なメモリ (RAM) がサーバーにないことを示します。 RAM を追加するか、記憶域レプリカ以外の機能とアプリケーションで使用されている RAM を削減してください。  

## <a name="when-using-guest-clusters-with-shared-vhdx-and-a-host-without-a-csv-virtual-machines-stop-responding-after-configuring-replication"></a>共有 VHDX を使用するゲスト クラスターと CSV を使用しないホストを併用すると、仮想マシンがレプリケーションの構成後に応答を停止する  
Windows Server 2016 では、記憶域レプリカのテストまたはデモのために Hyper-V ゲスト クラスターを使用し、ゲスト クラスターの記憶域として共有 VHDX を使用すると、レプリケーションの構成後に仮想マシンの応答が停止します。 Hyper-V ホストを再起動すると仮想マシンは応答を開始しますが、レプリケーションの構成が不完全になり、レプリケーションは発生しません。  

この動作は、**fltmc.exe attach svhdxflt** を使用して、CSV を実行する Hyper-V ホストの要件をバイパスしている場合に発生します。 このコマンド使用はサポートされておらず、用途はテストとデモのみに限られています。  

遅延の原因は、Windows Server 2016 の記憶域 QoS 機能と、手動で接続されている共有 VHDX フィルターの間にある、仕様による相互運用性の問題です。 この問題を解決するには、記憶域 QoS フィルター ドライバーを無効にし、Hyper-V ホストを再起動します。  

```  
SC config storqosflt start= disabled  
```  

## <a name="cannot-configure-replication-when-using-new-volume-and-differing-storage"></a>新しいボリュームと別の記憶域を使用するとレプリケーションを構成できない  
2 つの異なる SAN や、異なるディスクを使用する 2 つの JBOD など、レプリケーション元と先で異なる一連の記憶域を `New-Volume` コマンドレットで使用すると、後で `New-SRPartnership` を使用してレプリケーションを構成できない可能性があります。 以下のようなエラーが表示される場合があります。  

    Data partition sizes are different in those two groups  

ボリュームの作成とフォーマットには、`New-Volume` ではなく `New-Partition**` を使用してください。これは、前者のコマンドレットは、異なるストレージ アレイ上のボリューム サイズを丸める場合があるためです。 NTFS ボリュームをすでに作成してある場合、`Resize-Partition` を使用してボリュームのいずれかを拡大または縮小し、もう片方のボリュームに一致させることができます (これは、ReFS ボリュームでは行うことができません)。 **Diskmgmt** または**サーバー マネージャー**を使用している場合、丸めは発生しません。  

## <a name="running-test-srtopology-fails-with-name-related-errors"></a>Test-SRTopology を実行すると、名前関連のエラーが発生して失敗する

`Test-SRTopology` を使用しようとすると、次のエラーのうちいずれかが表示されます。  

**エラーの例 1:**

    WARNING: Invalid value entered for target computer name: sr-srv03. Test-SrTopology cmdlet does not accept IP address as  
    input for target computer name parameter. NetBIOS names and fully qualified domain names are acceptable inputs  
    WARNING: System.Exception  
    WARNING:    at Microsoft.FileServices.SR.Powershell.TestSRTopologyCommand.BeginProcessing()  
    Test-SRTopology : Invalid value entered for target computer name: sr-srv03. Test-SrTopology cmdlet does not accept IP  
    address as input for target computer name parameter. NetBIOS names and fully qualified domain names are acceptable  
    inputs  
    At line:1 char:1  
    + Test-SRTopology -SourceComputerName sr-srv01 -SourceVolumeName d: -So ...  
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~  
        + CategoryInfo          : InvalidArgument: (:) [Test-SRTopology], Exception  
        + FullyQualifiedErrorId : TestSRTopologyFailure,Microsoft.FileServices.SR.Powershell.TestSRTopologyCommand  

**エラーの例 2:**

    WARNING: Invalid value entered for source computer name

**エラーの例 3:**

    The specified volume cannot be found G: cannot be found on computer SRCLUSTERNODE1

Windows Server 2016 では、このコマンドレットのエラー報告が制限されており、多くの一般的な問題で同じ出力が返されます。 このエラーは、次の理由で表示されることがあります。  

* ドメイン ユーザーではなくローカル ユーザーとしてレプリケーション元のコンピューターにログオンしている。  
* レプリケーション先のコンピューターが実行されていないか、ネットワーク経由でアクセスできない。  
* レプリケーション先のコンピューターに正しくない名前を指定している。  
* レプリケーション先サーバーの IP アドレスを指定している。  
* レプリケーション先コンピューターのファイアウォールで PowerShell や CIM 呼び出しへのアクセスがブロックされている。  
* レプリケーション先のコンピューターで WMI サービスが実行されていない。   
* `Test-SRTopology` コマンドレットを管理コンピューターからリモートで実行するときに CREDSSP を使用していない。
* 指定されたレプリケーション元またはレプリケーション先のボリュームはクラスター ノード上のローカル ディスクであり、クラスター ディスクではない。  

## <a name="configuring-new-storage-replica-partnership-returns-an-error---failed-to-provision-partition"></a>新しい記憶域レプリカのパートナーシップを構成するとエラー "パーティションのプロビジョニングを実行できませんでした" が表示される
`New-SRPartnership` を使用して新しいレプリケーション パートナーシップを作成しようとすると、次のエラーが表示されます。

    New-SRPartnership : Unable to create replication group test01, detailed reason: Failed to provision partition ed0dc93f-107c-4ab4-a785-afd687d3e734.
    At line: 1 char: 1
    + New-SRPartnership -SourceComputerName srv1 -SourceRGName test01
    + Categorylnfo : ObjectNotFound: (MSFT_WvrAdminTasks : root/ Microsoft/. . s) CNew-SRPartnership], CimException
    + FullyQua1ifiedErrorId : Windows System Error 1168 ,New-SRPartnership

これは、システム ドライブと同じパーティション上にあるデータ ボリューム (つまり、**C:** ドライブとその Windows フォルダー) が選択されると発生します。 たとえば、同じパーティションから作成された **C:** と **D:** の両方のボリュームが含まれるドライブ上のデータ ボリュームで発生します。 この操作は記憶域レプリカではサポートされていないため、別のボリュームをレプリケート対象として選択する必要があります。

## <a name="attempting-to-grow-a-replicated-volume-fails-due-to-missing-update"></a>レプリケートされたボリュームを拡大しようとすると、更新プログラムがないために失敗する
レプリケートされたボリュームを拡大しようとすると、次のようなエラーが表示されます。

    PS C:\> Resize-Partition -DriveLetter d -Size 44GB
    Resize-Partition : The operation failed with return code 8
    At line:1 char:1
    + Resize-Partition -DriveLetter d -Size 44GB
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (StorageWMI:ROOT/Microsoft/.../MSFT_Partition
    [Resize-Partition], CimException
    + FullyQualifiedErrorId : StorageWMI 8,Resize-Partition

ディスク管理 MMC スナップインを使用する場合、次のエラーが表示されます。

    Element not found

このエラーは、`Set-SRGroup -Name rg01 -AllowVolumeResize $TRUE` を使用してソース サーバーでボリュームのサイズ変更を正しく有効化した場合にも発生します。 

この問題は、累積更新プログラムの Windows 10 バージョン 1607 (Anniversary Update) および Windows Server 2016 で修正されました。2016 年 12 月 9日 (KB3201845)。 

## <a name="attempting-to-grow-a-replicated-volume-fails-due-to-missing-step"></a>レプリケートされたボリュームを拡大しようとすると、ステップがないために失敗する
まず `-AllowResizeVolume $TRUE` を設定せずにソース サーバーでレプリケートされたボリュームをサイズ変更しようとした場合、次のエラーが発生します。

    PS C:\> Resize-Partition -DriveLetter I -Size 8GB
    Resize-Partition : Failed

アクティビティ ID: {87aebbd6-4f47-4621-8aa4-5328dfa6c3be} 行: 1 文字: 1
    + サイズ変更のパーティションのドライブ文字は、8 GB のサイズ
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (StorageWMI:ROOT/Microsoft/.../MSFT_Partition) [Resize-Partition], CimException
        + FullyQualifiedErrorId : StorageWMI 4,Resize-Partition

Storage Replica Event log error 10307:

    Attempted to resize a partition that is protected by Storage Replica .

    DeviceName: \Device\Harddisk1\DR1
    PartitionNumber: 7
    PartitionId: {b71a79ca-0efe-4f9a-a2b9-3ed4084a1822}

    Guidance: To grow a source data partition, set the policy on the replication group containing the data partition.

    Set-SRGroup -ComputerName [ComputerName] -Name [ReplicationGroupName] -AllowVolumeResize $true

    Before you grow the source data partition, ensure that the destination data partition has enough space to grow to an equal size. Shrinking of data partition protected by Storage Replica is blocked.

Disk Management Snap-in Error: 

    An unexpected error has occurred 

After resizing the volume, remember to disable resizing with `Set-SRGroup -Name rg01 -AllowVolumeResize $FALSE`. This parameter prevents admins from attempting to resize volumes prior to ensuring that there is sufficient space on the destination volume, typically because they were unaware of Storage Replica's presence. 

## Attempting to move a PDR resource between sites on an asynchronous stretch cluster fails
When attempting to move a physical disk resource-attached role - such as a file server for general use - in order to move the associated storage in an asynchronous stretch cluster, you receive an error.

If using the Failover Cluster Manager snap-in:

    Error
    The operation has failed.
    The action 'Move' did not complete.
    Error Code: 0x80071398
    The operation failed because either the specified cluster node is not the owner of the group, or the node is not a possible owner of the group

If using the Cluster powershell cmdlet:

    PS C:\> Move-ClusterGroup -Name sr-fs-006 -Node sr-srv07
    Move-ClusterGroup : An error occurred while moving the clustered role 'sr-fs-006'.
    The operation failed because either the specified cluster node is not the owner of the group, or the node is not a
    possible owner of the group
    At line:1 char:1
    + Move-ClusterGroup -Name sr-fs-006 -Node sr-srv07
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (:) [Move-ClusterGroup], ClusterCmdletException
    + FullyQualifiedErrorId : Move-ClusterGroup,Microsoft.FailoverClusters.PowerShell.MoveClusterGroupCommand

This occurs due to a by-design behavior in Windows Server 2016. Use `Set-SRPartnership` to move these PDR disks in an asynchronous stretched cluster.  

This behavior has been changed in Windows Server, version 1709 to allow manual and automated failovers with asynchronous replication, based on customer feedback.

## Attempting to add disks to a two-node asymmetric cluster returns "No disks suitable for cluster disks found" 
When attempting to provision a cluster with only two nodes, prior to adding Storage Replica stretch replication, you attempt to add the disks in the second site to the Available Disks. You receive the following error:

    "No disks suitable for cluster disks found. For diagnostic information about disks available to the cluster, use the Validate a Configuration Wizard to run Storage tests." 

This does not occur if you have at least three nodes in the cluster. This issue occurs because of a by-design code change in Windows Server 2016 for asymmetric storage clustering behaviors. 

To add the storage, you can run the following command on the node in the second site:

`Get-ClusterAvailableDisk -All | Add-ClusterDisk`

This will not work with node local storage. You can use Storage Replica to replicate a stretch cluster between two total nodes, **each one using its own set of shared storage.** 

## The SMB Bandwidth limiter fails to throttle Storage Replica bandwidth
When specifying a bandwidth limit to Storage Replica, the limit is ignored and full bandwidth used. For example:

`Set-SmbBandwidthLimit  -Category StorageReplication -BytesPerSecond 32MB`

This issue occurs because of an interoperability issue between Storage Replica and SMB. This issue was first fixed in the July 2017 Cumulative Update of Windows Server 2016 and in Windows Server, version 1709.

## Event 1241 warning repeated during initial sync
When specifying a replication partnership is asynchronous, the source computer repeatedly logs warning event 1241 in the Storage Replica Admin channel. For example:

    Log Name:      Microsoft-Windows-StorageReplica/Admin
    Source:        Microsoft-Windows-StorageReplica
    Date:          3/21/2017 3:10:41 PM
    Event ID:      1241
    Task Category: (1)
    Level:         Warning
    Keywords:      (1)
    User:          SYSTEM
    Computer:      sr-srv05.corp.contoso.com
    Description:
    The Recovery Point Objective (RPO) of the asynchronous destination is unavailable.

    LocalReplicationGroupName: rg01
    LocalReplicationGroupId: {e20b6c68-1758-4ce4-bd3b-84a5b5ef2a87}
    LocalReplicaName: f:\
    LocalPartitionId: {27484a49-0f62-4515-8588-3755a292657f}
    ReplicaSetId: {1f6446b5-d5fd-4776-b29b-f235d97d8c63}
    RemoteReplicationGroupName: rg02
    RemoteReplicationGroupId: {7f18e5ea-53ca-4b50-989c-9ac6afb3cc81}
    TargetRPO: 30

    Guidance: This is typically due to one of the following reasons: 

The asynchronous destination is currently disconnected. The RPO may become available after the connection is restored.

    The asynchronous destination is unable to keep pace with the source such that the most recent destination log record is no longer present in the source log. The destination will start block copying. The RPO should become available after block copying completes.

This is expected behavior during initial sync and can safely be ignored. This behavior may change in a later release. If you see this behavior during ongoing asynchronous replication, investigate the partnership to determine why replication is delayed beyond your configured RPO (30 seconds, by default).

## Event 4004 warning repeated after rebooting a replicated node
Under rare and usually unreproducable circumstances, rebooting a server that is in a partnership leads to replication failing and the rebooted node logging warning event 4004 with an access denied error.

    Log Name:      Microsoft-Windows-StorageReplica/Admin
    Source:        Microsoft-Windows-StorageReplica
    Date:          3/21/2017 11:43:25 AM
    Event ID:      4004
    Task Category: (7)
    Level:         Warning
    Keywords:      (256)
    User:          SYSTEM
    Computer:      server.contoso.com
    Description:
    Failed to establish a connection to a remote computer.

    RemoteComputerName: server
    LocalReplicationGroupName: rg01
    LocalReplicationGroupId: {a386f747-bcae-40ac-9f4b-1942eb4498a0}
    RemoteReplicationGroupName: rg02
    RemoteReplicationGroupId: {a386f747-bcae-40ac-9f4b-1942eb4498a0}
    ReplicaSetId: {00000000-0000-0000-0000-000000000000}
    RemoteShareName:{a386f747-bcae-40ac-9f4b-1942eb4498a0}.{00000000-0000-0000-0000-000000000000}
    Status: {Access Denied}
    A process has requested access to an object, but has not been granted those access rights.

    Guidance: Possible causes include network failures, share creation failures for the remote replication group, or firewall settings. Make sure SMB traffic is allowed and there are no connectivity issues between the local computer and the remote computer. You should expect this event when suspending replication or removing a replication partnership.

Note the `Status: "{Access Denied}"` and the message `A process has requested access to an object, but has not been granted those access rights.` This is a known issue within Storage Replica and was fixed in Quality Update September 12, 2017—KB4038782 (OS Build 14393.1715) https://support.microsoft.com/help/4038782/windows-10-update-kb4038782 

## Error "Failed to bring the resource 'Cluster Disk x' online." with a stretch cluster
When attempting to bring a cluster disk online after a successful failover, where you are attempting to make the original source site primary again, you receive an error in Failover Cluster Manager. For example:

    Error
    The operation has failed.
    Failed to bring the resource 'Cluster Disk 2' online.

    Error Code: 0x80071397
    The operation failed because either the specified cluster node is not the owner of the resource, or the node is not a possible owner of the resource.

If you attempt to move the disk or CSV manually, you receive an additional error. For example:

    Error
    The operation has failed.
    The action 'Move' did not complete.

    Error Code: 0x8007138d
    A cluster node is not available for this operation

This issue is caused by one or more uninitialized disks being attached to one or more cluster nodes. To resolve the issue, initialize all attached storage using DiskMgmt.msc, DISKPART.EXE, or the Initialize-Disk PowerShell cmdlet.

We are working on providing an update that permanently resolves this issue. If you are interested in assisting us and you have a Microsoft Premier Support agreement, please email SRFEED@microsoft.com so that we can work with you on filing a backport request.

## GPT error when attempting to create a new SR partnership

When running New-SRPartnership, it fails with error:

    Disk layout type for volume \\?\Volume{GUID}\ is not a valid GPT style layout.
    New-SRPartnership : Unable to create replication group SRG01, detailed reason: Disk layout type for volume
    \\?\Volume{GUID}\ is not a valid GPT style layout.
    At line:1 char:1
    + New-SRPartnership -SourceComputerName nodesrc01 -SourceRGName SRG01 ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (MSFT_WvrAdminTasks:root/Microsoft/...T_WvrAdminTasks) [New-SRPartnership]
    , CimException
    + FullyQualifiedErrorId : Windows System Error 5078,New-SRPartnership

In the Failover Cluster Manager GUI, there is no option to setup Replication for the disk.

When running Test-SRTopology, it fails with: 

    WARNING: Object reference not set to an instance of an object.
    WARNING: System.NullReferenceException
    WARNING:    at Microsoft.FileServices.SR.Powershell.MSFTPartition.GetPartitionInStorageNodeByAccessPath(String AccessPath, String ComputerName, MIObject StorageNode)
       at Microsoft.FileServices.SR.Powershell.Volume.GetVolume(String Path, String ComputerName)
       at Microsoft.FileServices.SR.Powershell.TestSRTopologyCommand.BeginProcessing()
    Test-SRTopology : Object reference not set to an instance of an object.
    At line:1 char:1
    + Test-SRTopology -SourceComputerName nodesrc01 -SourceVolumeName U: - ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidArgument: (:) [Test-SRTopology], NullReferenceException
    + FullyQualifiedErrorId : TestSRTopologyFailure,Microsoft.FileServices.SR.Powershell.TestSRTopologyCommand 

This is caused by the cluster functional level still being set to Windows Server 2012 R2 (i.e. FL 8). Storage Replica is supposed to return a specific error here but instead returns an incorrect error mapping.

Run Get-Cluster | fl * on each node.

If ClusterFunctionalLevel = 9, that is the Windows 2016 ClusterFunctionalLevel version needed to implement Storage Replica on this node.
If ClusterFunctionalLevel is not 9, the ClusterFunctionalLevel will need to be updated in order to implement Storage Replica on this node.

To resolve the issue, raise the cluster functional level by running the PowerShell cmdlet: [Update-ClusterFunctionalLevel](https://docs.microsoft.com/powershell/module/failoverclusters/update-clusterfunctionallevel)

## Small unknown partition listed in DISKMGMT for each replicated volume

When running the Disk Management snap-in (DISKMGMT.MSC), you notice one or more volumes listed with no label or drive letter and 1MB in size. You may be able to delete the unknown volume or you may receive:

    "An Unexpected Error has Occurred"  

This behavior is by design. This not a volume, but a partition. Storage Replica creates a 512KB partition as a database slot for replication operations (the legacy DiskMgmt.msc tool rounds to the nearest MB). Having a partition like this for each replicated volume is normal and desirable. When no longer in use, you are free to delete this 512KB partition; in-use ones cannot be deleted. The partition will never grow or shrink. If you are recreating replication we recommend leaving the partition as Storage Replica will claim unused ones.

To view details, use the DISKPART tool or Get-Partition cmdlet. These partitions will have a GPT Type of `558d43c5-a1ac-43c0-aac8-d1472b2923d1`.

## A Storage Replica node hangs when creating snapshots
When creating a VSS snapshot (through backup, VSSADMIN, etc) a Storage Replica node hangs, and you must force a restart of the node to recover. There is no error, just a hard hang of the server.

This issue occurs when you create a VSS snapshot of the log volume. The underlying cause is a legacy design aspect of VSS, not Storage Replica. The resulting behavior when you snapshot the Storage Replica log volume is a VSS I/O queing mechanism deadlocks the server.

To prevent this behavior, do not snapshot Storage Replica log volumes. There is no need to snapshot Storage Replica log volumes, as these logs cannot be restored. Furthermore, the log volume should never contain any other workloads, so no snapshot is needed in general.

## High IO latency increase when using Storage Spaces Direct with Storage Replica  
When using Storage Spaces Direct with an NVME or SSD cache, you see a greater than expected increase in latency when configuring Storage Replica replication between Storage Spaces Direct clusters. The change in latency is proportionally much higher than you see when using NVME and SSD in a performance + capacity configuration and no HDD tier nor capacity tier.

This issue occurs due to architectural limitations within Storage Replica's log mechanism combined with the extremely low latency of NVME when compared to slower media. When using the Storage Spaces Direct cache, all I/O of Storage Replica logs, along with all recent read/write IO of applications, will occur in the cache and never on the performance or capacity tiers. This means that all Storage Replica activity happens on the same speed media - this configuration is supported but not recommended (see https://aka.ms/srfaq for log recommendations). 

When using Storage Spaces Direct with HDDs, you cannot disable or avoid the cache. As a workaround, if using just SSD and NVME, you can configure just performance and capacity tiers. If using that configuration, and by placing the SR logs on the performance tier only with the data volumes they service being on the capacity tier only, you will avoid the high latency issue described above. The same could be done with a mix of faster and slower SSDs and no NVME.

This workaround is of course not ideal and some customers may not be able to make use of it. The Storage Replica team is working on optimizations and an updated log mechanism for the future to reduce these artificial bottlenecks. This v1.1 log first became available in Windows Server 2019 and its improved performance is described in on the [Server Storage Blog](https://blogs.technet.microsoft.com/filecab/2018/12/13/chelsio-rdma-and-storage-replica-perf-on-windows-server-2019-are-💯/).

## Error "Could not find file" when running Test-SRTopology between two clusters

When running Test-SRTopology between two clusters and their CSV paths, it fails with error: 

    PS C:\Windows\system32> Test-SRTopology -SourceComputerName NedClusterA -SourceVolumeName C:\ClusterStorage\Volume1 -SourceLogVolumeName L: -DestinationComputerName NedClusterB -DestinationVolumeName C:\ClusterStorage\Volume1 -DestinationLogVolumeName L: -DurationInMinutes 1 -ResultPath C:\Temp

    Validating data and log volumes...
    Measuring Storage Replica recovery and initial synchronization performance...
    WARNING: Could not find file '\\NedNode1\C$\CLUSTERSTORAGE\VOLUME1TestSRTopologyRecoveryTest\SRRecoveryTestFile01.txt'.
    WARNING: System.IO.FileNotFoundException
    WARNING:    at System.IO.__Error.WinIOError(Int32 errorCode, String maybeFullPath)
    at System.IO.FileStream.Init(String path, FileMode mode, FileAccess access, Int32 rights, Boolean useRights, FileShare share, Int32 buff
    erSize, FileOptions options, SECURITY_ATTRIBUTES secAttrs, String msgPath, Boolean bFromProxy, Boolean useLongPath, Boolean checkHost)
    at System.IO.FileStream..ctor(String path, FileMode mode, FileAccess access, FileShare share, Int32 bufferSize, FileOptions options)
    at Microsoft.FileServices.SR.Powershell.TestSRTopologyCommand.GenerateWriteIOWorkload(String Path, UInt32 IoSizeInBytes, UInt32 Parallel
    IoCount, UInt32 Duration)
    at Microsoft.FileServices.SR.Powershell.TestSRTopologyCommand.<>c__DisplayClass75_0.<PerformRecoveryTest>b__0()
    at System.Threading.Tasks.Task.Execute()
    Test-SRTopology : Could not find file '\\NedNode1\C$\CLUSTERSTORAGE\VOLUME1TestSRTopologyRecoveryTest\SRRecoveryTestFile01.txt'.
    At line:1 char:1
    + Test-SRTopology -SourceComputerName NedClusterA -SourceVolumeName  ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (:) [Test-SRTopology], FileNotFoundException
    + FullyQualifiedErrorId : TestSRTopologyFailure,Microsoft.FileServices.SR.Powershell.TestSRTopologyCommand 

This is caused by a known code defect in Windows Server 2016. This issue was first fixed in Windows Server, version 1709 and the associated RSAT tools. For a downlevel resolution, please contact Microsoft Support and request a backport update. There is no workaround.

## Error "specified volume could not be found" when running Test-SRTopology between two clusters

When running Test-SRTopology between two clusters and their CSV paths, it fails with error:

    PS C:\> Test-SRTopology -SourceComputerName RRN44-14-09 -SourceVolumeName C:\ClusterStorage\Volume1 -SourceLogVolumeName L: -DestinationComputerName RRN44-14-13 -DestinationVolumeName C:\ClusterStorage\Volume1 -DestinationLogVolumeName L: -DurationInMinutes 30 -ResultPath c:\report

    Test-SRTopology : The specified volume C:\ClusterStorage\Volume1 cannot be found on computer RRN44-14-09. If this is a cluster node, the volume must be part of a role or CSV; volumes in Available Storage are not accessible
    At line:1 char:1
    + Test-SRTopology -SourceComputerName RRN44-14-09 -SourceVolumeName C:\ ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : ObjectNotFound: (:) [Test-SRTopology], Exception
        + FullyQualifiedErrorId : TestSRTopologyFailure,Microsoft.FileServices.SR.Powershell.TestSRTopologyCommand

When specifying the source node CSV as the source volume, you must select the node that owns the CSV. You can either move the CSV to the specified node or change the node name you specified in `-SourceComputerName`. This error received an improved message in Windows Server 2019.

## Unable to access the data drive in Storage Replica after unexpected reboot when BitLocker is enabled

If BitLocker is enabled on both drives (Log Drive and Data Drive) and in both Storage replica drives, if the Primary Server reboots then you are unable to access the Primary Drive even after unlocking the Log Drive from BitLocker.

This is an expected behavior. To recover the data or access the drive, you need to unlock the log drive first and then open Diskmgmt.msc to locate the data drive. Turn the data drive offline and online again. Locate the BitLocker icon on the drive and unlock the drive.

## Issue unlocking the Data drive on secondary server after breaking the Storage Replica partnership

After Disabling the SR Partnership and removing the Storage Replica, it is expected if you are unable to unlock the Secondary Server’s Data drive with its respective password or key. 

You need to use Key or Password of Primary Server’s Data drive to unlock the Secondary Server’s data drive.

## Test Failover doesn't mount when using asynchronous replication

When running Mount-SRDestination to bring a destination volume online as part of the Test Failover feature, it fails with error:

    Mount-SRDestination: Unable to mount SR group <TEST>, detailed reason: The group or resource is not in the correct state to perform the supported operation.
    At line:1 char:1
    + Mount-SRDestination -ComputerName SRV1 -Name TEST -TemporaryP . . .
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (MSFT WvrAdminTasks : root/Microsoft/...(MSFT WvrAdminTasks : root/Microsoft/. T_WvrAdminTasks) (Mount-SRDestination], CimException
        + FullyQua1ifiedErrorId : Windows System Error 5823, Mount-SRDestination.  

If using a synchronous partnership type, test failover works normally.

This is caused by a known code defect in Windows Server, version 1709. To resolve this issue, install the [October 18, 2018 update](https://support.microsoft.com/help/4462932/windows-10-update-kb4462932). This issue isn't present in Windows Server 2019 and Windows Server, version 1809 and newer.

## See also

- [Storage Replica](storage-replica-overview.md)  
- [Stretch Cluster Replication Using Shared Storage](stretch-cluster-replication-using-shared-storage.md)  
- [Server to Server Storage Replication](server-to-server-storage-replication.md)  
- [Cluster to Cluster Storage Replication](cluster-to-cluster-storage-replication.md)  
- [Storage Replica: Frequently Asked Questions](storage-replica-frequently-asked-questions.md)  
- [Storage Spaces Direct](../storage-spaces/storage-spaces-direct-overview.md)  
