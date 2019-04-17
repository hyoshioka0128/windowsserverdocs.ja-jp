---
title: "記憶域レプリカに関する既知の問題"
ms.prod: windows-server-threshold
manager: siroy
ms.author: nedpyle
ms.technology: storage-replica
ms.topic: get-started-article
author: nedpyle
ms.date: 10/13/2016
ms.assetid: ceddb0fa-e800-42b6-b4c6-c06eb1d4bc55
ms.openlocfilehash: 6f02ece1f327cf53667df09e6d13ace001259885
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="known-issues-with-storage-replica"></a>記憶域レプリカに関する既知の問題

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このセクションでは、Windows Server 2016 での記憶域レプリカに関する既知の問題について説明します。  

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

この問題は、Windows 10 バージョン 1607 と Windows Server 2016 の累積的な更新プログラム: 2016 年 12 月 9 日 (KB3201845) で修正されました。 

## <a name="attempting-to-grow-a-replicated-volume-fails-due-to-missing-step"></a>レプリケートされたボリュームを拡大しようとすると、ステップがないために失敗する
まず `-AllowResizeVolume $TRUE` を設定せずにソース サーバーでレプリケートされたボリュームをサイズ変更しようとした場合、次のエラーが発生します。

    PS C:\> Resize-Partition -DriveLetter I -Size 8GB
    Resize-Partition : Failed
    Activity ID: {87aebbd6-4f47-4621-8aa4-5328dfa6c3be}
    At line:1 char:1
    + Resize-Partition -DriveLetter I -Size 8GB
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (StorageWMI:ROOT/Microsoft/.../MSFT_Partition) [Resize-Partition], CimException
        + FullyQualifiedErrorId : StorageWMI 4,Resize-Partition

記憶域レプリカのイベント ログ エラー 10307:

    Attempted to resize a partition that is protected by Storage Replica .

    DeviceName: \Device\Harddisk1\DR1
    PartitionNumber: 7
    PartitionId: {b71a79ca-0efe-4f9a-a2b9-3ed4084a1822}

    Guidance: To grow a source data partition, set the policy on the replication group containing the data partition.

    Set-SRGroup -ComputerName [ComputerName] -Name [ReplicationGroupName] -AllowVolumeResize $true

    Before you grow the source data partition, ensure that the destination data partition has enough space to grow to an equal size. Shrinking of data partition protected by Storage Replica is blocked.

ディスク管理スナップイン エラー: 

    An unexpected error has occurred 

ボリュームをサイズ変更したら、必ず `Set-SRGroup -Name rg01 -AllowVolumeResize $FALSE` を使ってサイズ変更を無効にしてください。 このパラメーターを使うと、管理者はターゲット ボリュームに十分なスペースがあることを確認するまでボリュームのサイズを変更することができません。通常は、記憶域レプリカが存在していることがわからないためです。 

## <a name="attempting-to-move-a-pdr-resource-between-sites-on-an-asynchronous-stretch-cluster-fails"></a>非同期ストレッチ クラスター上のサイト間で PDR リソースを移動する試みが失敗する
非同期ストレッチ クラスター内の関連する記憶域を移動するために、物理ディスク リソースに接続された役割の移動を試みると (一般的な用途のファイル サーバーなど)、エラーが表示されます。

フェールオーバー クラスター マネージャー スナップインを使用する場合:

    Error
    The operation has failed.
    The action 'Move' did not complete.
    Error Code: 0x80071398
    The operation failed because either the specified cluster node is not the owner of the group, or the node is not a possible owner of the group
    
クラスター PowerShell コマンドレットを使用する場合:

    PS C:\> Move-ClusterGroup -Name sr-fs-006 -Node sr-srv07
    Move-ClusterGroup : An error occurred while moving the clustered role 'sr-fs-006'.
    The operation failed because either the specified cluster node is not the owner of the group, or the node is not a
    possible owner of the group
    At line:1 char:1
    + Move-ClusterGroup -Name sr-fs-006 -Node sr-srv07
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (:) [Move-ClusterGroup], ClusterCmdletException
    + FullyQualifiedErrorId : Move-ClusterGroup,Microsoft.FailoverClusters.PowerShell.MoveClusterGroupCommand

このような状況は、Windows Server 2016 の仕様による動作が原因で発生します。 非同期ストレッチ クラスター内でこうした PDR ディスクを移動するには、`Set-SRPartnership` を使用してください。  

## <a name="attempting-to-add-disks-to-a-two-node-asymmetric-cluster-returns-no-disks-suitable-for-cluster-disks-found"></a>非対称の 2 ノード クラスターへのディスクの追加を試みると、"クラスター ディスクに適したディスクが見つかりません" というメッセージが返される 
2 つのノードのみでクラスターのプロビジョニングを試みる場合は、記憶域レプリカ ストレッチ レプリケーションを追加する前に、使用可能なディスクへの 2 番目のサイトのディスクの追加を試みます。 次のエラーが表示されます。

    "No disks suitable for cluster disks found. For diagnostic information about disks available to the cluster, use the Validate a Configuration Wizard to run Storage tests." 

クラスターに少なくとも 3 つのノードがある場合、このエラーは発生しません。 この問題は、Windows Server 2016 での非対称記憶域クラスタリング動作に関する設計上のコード変更のために発生します。 

記憶域を追加するには、2 つ目のサイト内のノードで次のコマンドを実行できます。

`Get-ClusterAvailableDisk -All | Add-ClusterDisk`

これは、ノードのローカル ストレージでは機能しません。 記憶域レプリカを使うと、**それぞれ独自の共有ストレージ セットを使う**合計 2 つのノード間でストレッチ クラスターをレプリケートできます。 

## <a name="the-smb-bandwidth-limiter-fails-to-throttle-storage-replica-bandwidth"></a>記憶域レプリカの帯域幅を調整する SMB 帯域幅リミッタが失敗する
記憶域レプリカに帯域幅の制限を指定する場合、制限は無視され、帯域幅全体を使用します。 以下に例を示します。

`Set-SmbBandwidthLimit  -Category StorageReplication -BytesPerSecond 32MB`

この問題は、記憶域レプリカと SMB 間の相互運用性の問題のために発生します。 この問題は、2017 年 7 月の Windows Server 2016 の累積更新プログラムおよび Windows Server バージョン 1709 で修正されました。

## <a name="event-1241-warning-repeated-during-initial-sync"></a>初期同期中に イベント 1241 警告が繰り返される
レプリケーション パートナーシップを非同期に指定すると、ソース コンピューターで警告イベント 1241 が記憶域レプリカの管理者チャネルで繰り返し記録されます。 以下に例を示します。

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

非同期の宛先は、現在切断されています。 接続が復元した後に、RPO が利用可能になる可能性があります。

    The asynchronous destination is unable to keep pace with the source such that the most recent destination log record is no longer present in the source log. The destination will start block copying. The RPO should become available after block copying completes.

これは初期同期中に予期される動作であり、無視しても問題ありません。 この動作は、今後のリリースで変更される可能性があります。 この動作が、継続的な非同期レプリケーション中に発生する場合、パートナーシップを調査して、構成済みのRPO (既定で 30秒) 以上に遅延する理由を判断します。

## <a name="event-4004-warning-repeated-after-rebooting-a-replicated-node"></a>レプリケート ノードを再起動した後にイベント 4004 警告が繰り返される
通常は再現できないまれな状況で、パートナーシップ内のサーバーを再起動すると、レプリケーションが失敗し、再起動されたノードで、アクセス拒否エラーと警告イベント 4004 が記録されます。

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

`Status: "{Access Denied}"` とメッセージ `A process has requested access to an object, but has not been granted those access rights.` に注意してください。これは記憶域レプリカの既知の問題であり、2017 年 9 月 12 日の品質更新プログラム (KB4038782 (OS ビルド 14393.1715) https://support.microsoft.com/en-us/help/4038782/windows-10-update-kb4038782) で修正されました。 

## <a name="error-failed-to-bring-the-resource-cluster-disk-x-online-with-a-stretch-cluster"></a>ストレッチ クラスターで「リソース 'クラスター ディスク x' をオンラインにできませんでした」エラーが発生する  
正常なフェールオーバー後にクラスター ディスクをオンラインにしようとするとき、元のソース サイトを再度プライマリにしようとすると、フェールオーバー クラスター マネージャーでエラーが発生します。 以下に例を示します。

    Error
    The operation has failed.
    Failed to bring the resource 'Cluster Disk 2' online.
    
    Error Code: 0x80071397
    The operation failed because either the specified cluster node is not the owner of the resource, or the node is not a possible owner of the resource.
    
ディスクまたは CSV を手動で移動しようとすると、さらにエラーが表示されます。 以下に例を示します。

    Error
    The operation has failed.
    The action 'Move' did not complete.
    
    Error Code: 0x8007138d
    A cluster node is not available for this operation

この問題は、1 つ以上の初期化されていないディスクが 1 つ以上のクラスター ノードにアタッチされることにより発生します。 問題を解決するには、DiskMgmt.msc、DISKPART.EXE、または Initialize-Disk PowerShell コマンドレットを使って、アタッチされたすべてのストレージを初期化します。

Microsoft はこの問題を完全に解決するための更新プログラムの提供に取り組んでいます。 マイクロソフト プレミア サポート契約をお持ちのお客様で、この問題の解決にご協力いただける方は、バックポート要求の提出のため、SRFEED@microsoft.com までメールでご連絡ください。

## <a name="gpt-error-when-attempting-to-create-a-new-sr-partnership"></a>新しい SR パートナーシップを作成しようとすると GPT エラーが発生する

New-SRPartnership の実行中にエラーが発生します。 

    Disk layout type for volume \\?\Volume{GUID}\ is not a valid GPT style layout.
    New-SRPartnership : Unable to create replication group SRG01, detailed reason: Disk layout type for volume
    \\?\Volume{GUID}\ is not a valid GPT style layout.
    At line:1 char:1
    + New-SRPartnership -SourceComputerName nodesrc01 -SourceRGName SRG01 ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (MSFT_WvrAdminTasks:root/Microsoft/...T_WvrAdminTasks) [New-SRPartnership]
    , CimException
    + FullyQualifiedErrorId : Windows System Error 5078,New-SRPartnership

フェールオーバー クラスター マネージャーの GUIでは、ディスクのレプリケーションを設定するオプションはありません。

Test-SRTopology の実行中に、次のように失敗します。 

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

これはクラスター機能レベルが Windows Server 2012 R2 (FL 8 など) に設定されたままであることにより発生します。 記憶域レプリカは、固有のエラーを返すべきですが、正しくないエラー マッピングが返されています。

Get-Cluster | fl * を各ノードで実行します。

ClusterFunctionalLevel が 9 である場合、それは記憶域レプリカをこのノードに実装するために必要な Windows 2016 ClusterFunctionalLevel のバージョンです。
ClusterFunctionalLevel が 9でない場合、このノードで記憶域レプリカを実装するためには、ClusterFunctionalLevel を更新する必要があります。

この問題を解決するには、PowerShell コマンドレット Update-ClusterFunctionalLevel (https://technet.microsoft.com/itpro/powershell/windows/failoverclusters/update-clusterfunctionallevel を参照) を実行して、クラスターの機能レベルを上げます。

## <a name="small-unknown-partition-listed-in-diskmgmt-for-each-replicated-volume"></a>レプリケートされた各ボリュームに対し、DISKMGMT に小さな不明パーティションが表示される

ディスク管理スナップイン (DISKMGMT.MSC) を実行すると、ラベルやドライブ文字がない 1 MB のサイズのボリュームが 1 つまたは複数表示されます。 この不明なボリュームは削除できる場合もありますが、できない場合は以下のエラー メッセージが表示されることがあります。

    "An Unexpected Error has Occurred"  

この動作は仕様です。 これはボリュームではなくパーティションです。 記憶域レプリカによって、レプリケーション操作のためのデータベース スロットとして 512 KB のパーティションが作成されます (レガシー DiskMgmt.msc ツールによって、MB 単位で最も近いサイズに丸められます) レプリケートされた各ボリュームにこのようなパーティションが作成されることは、正常であり適切です。 この 512 KB のパーティションは、不要になれば削除できますが、使用中は削除できません。 パーティションのサイズは、拡大縮小しません。 レプリケーションを再作成する場合は、ストレージ レプリカが未使用のパーティションを要求できるように、パーティションを削除せずにおくことをお勧めします。

詳細を表示するには、DISKPART ツールまたは Get-Partition コマンドレットを使用します。 これらのパーティションには、`558d43c5-a1ac-43c0-aac8-d1472b2923d1` という GPT タイプが割り当てられます。 

## <a name="see-also"></a>関連項目  
- [記憶域レプリカ](storage-replica-overview.md)  
- [共有記憶域を使用したストレッチ クラスター レプリケーション](stretch-cluster-replication-using-shared-storage.md)  
- [サーバー間の記憶域レプリケーション](server-to-server-storage-replication.md)  
- [クラスター間の記憶域のレプリケーション](cluster-to-cluster-storage-replication.md)  
- [記憶域レプリカ: よく寄せられる質問](storage-replica-frequently-asked-questions.md)  
- [記憶域スペース ダイレクト](../storage-spaces/storage-spaces-direct-overview.md)  
