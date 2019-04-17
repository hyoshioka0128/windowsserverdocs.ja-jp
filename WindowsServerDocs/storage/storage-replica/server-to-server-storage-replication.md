---
title: "サーバー間の記憶域レプリケーション"
ms.prod: windows-server-threshold
manager: siroy
ms.author: nedpyle
ms.technology: storage-replica
ms.topic: get-started-article
author: nedpyle
ms.date: 10/11/2016
ms.assetid: 61881b52-ee6a-4c8e-85d3-702ab8a2bd8c
ms.openlocfilehash: 9dd2820f641e23dceb5c2ac7110efda0d3345dcf
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="server-to-server-storage-replication"></a>サーバー間の記憶域レプリケーション

> 適用対象: Windows Server (半期チャネル)、Windows Server 2016

記憶域レプリカを使用すると、2 台のサーバーがそれぞれ同じボリュームの同じコピーを持つようにデータの同期を構成できます。 このトピックでは、このようなサーバー間のレプリケーション構成の背景、設定方法、環境の管理方法について説明します。

記憶域レプリカの管理には、PowerShell または [Azure サーバー管理ツール](https://blogs.technet.microsoft.com/servermanagement/)を利用できます。

> [!IMPORTANT]
>  このシナリオでは、各サーバーが別の物理または論理サイト上に存在する必要があります。 各サーバーは、ネットワーク経由で相互に通信できる必要があります。  

## <a name="terms"></a>用語  
このチュートリアルでは、例として次の環境を使用します。  

-   **SR-SRV05** および **SR-SRV06** という名前の 2 台のサーバー。  

-   2 つの異なるデータ センターを表す 2 つの論理 "サイト" である **Redmond** と **Bellevue**。  

![施設 5 のサーバーを施設 9 のサーバーでレプリケートしていることを示す図](media/Server-to-Server-Storage-Replication/Storage_SR_ServertoServer.png)  

**図 1: サーバー間のレプリケーション**  

## <a name="prerequisites"></a>前提条件  

* Active Directory Domain Services フォレスト (Windows Server 2016 を実行する必要はありません)。  
* Windows Server 2016 Datacenter Edition がインストールされている 2 台のサーバー。  
* SAS JBOD、ファイバー チャネル SAN、iSCSI ターゲット、またはローカル SCSI/SATA ストレージを使用する 2 セットの記憶域。 記憶域では HDD メディアと SSD メディアを混在させる必要があります。 各記憶域セットは、共有アクセスなしで、各サーバーでのみ利用可能となるように設定します。  
* 各記憶域セットでは、2 つ以上の仮想ディスク (レプリケートされたデータ用とログ用) を作成できる必要があります。 物理記憶域のセクター サイズは、すべてのデータ ディスクで同じである必要があります。 物理記憶域のセクター サイズは、すべてのログ ディスクで同じである必要があります。  
* 同期レプリケーションのために各サーバーで少なくとも 1 つのイーサネット/TCP 接続 (可能であれば RDMA)。   
* すべてのノード間での ICMP、SMB (ポート 445 と、SMB ダイレクト用のポート 5445)、WS-MAN (ポート 5985) の双方向トラフィックを許可する適切なファイアウォール規則およびルーター規則。  
* 書き込みの IO 負荷に十分対応できる帯域幅を持ちラウンド トリップ遅延時間が平均 5 ミリ秒である、同期レプリケーション用のサーバー間ネットワーク。 非同期レプリケーションには、遅延時間に関する推奨事項はありません。  
* レプリケート対象の記憶域を、Windows オペレーティング システムのフォルダーが含まれるドライブに配置することはできません。

これらの要件の多くは、`Test-SRTopology cmdlet` を使用して確認できます。 記憶域レプリカまたは記憶域レプリカ管理ツール機能を 1 つ以上のサーバーにインストールすると、このツールにアクセスできるようになります。 このツールを使用するために記憶域レプリカを構成する必要はありません。記憶域レプリカは、コマンドレットをインストールするためだけに構成します。 詳細は、以下の手順に記載されています。  

## <a name="provision-operating-system-features-roles-storage-and-network"></a>オペレーティング システム、機能、役割、記憶域、およびネットワークのプロビジョニング  
1.  Windows Server 2016 Datacenter **(デスクトップ エクスペリエンス)** のインストールの種類で、両方のサーバー ノードに Windows Server 2016 をインストールします。 Standard Edition が利用可能でも、これには記憶域レプリカが含まれていないため選択しないでください。  

2.  ネットワークの情報を追加し、ドメインに参加させてから再起動します。  

    > [!NOTE]
    > この時点以降、すべてのサーバーのビルトイン Administrator グループのメンバーであるドメイン ユーザーとして常にログオンします。 今後、グラフィカルなサーバー インストールまたは Windows 10 コンピューターで実行するときは、必ず PowerShell プロンプトおよび CMD プロンプトで昇格を行ってください。  

3.  JBOD ストレージ格納装置、iSCSI ターゲット、FC SAN、またはローカルの固定ディスク (DAS) 記憶域の最初のセットをサイト **Redmond** 内のサーバーに接続します。  

4.  記憶域の 2 つめのセットをサイト **Bellevue** 内のサーバーに接続します。  

5.  必要に応じて、両方のノードに最新のベンダー記憶域、格納装置ファームウェアとドライバー、最新のベンダー HBA ドライバー、最新のベンダー BIOS/UEFI ファームウェア、最新のベンダー ネットワーク ドライバー、および最新のマザーボード チップセット ドライバーをインストールします。 必要に応じてノードを再起動します。  

    > [!NOTE]
    > 共有記憶域およびネットワーク ハードウェアの構成については、ハードウェア ベンダーのドキュメントを参照してください。  

6.  サーバーの BIOS および UEFI の設定が、C 状態の無効化、QPI 速度の設定、NUMA の有効化、最大メモリ動作周波数の設定など、高パフォーマンスを有効にする設定であることを確認します。 Windows Server での電源管理が高パフォーマンスに設定されていることを確認します。 必要に応じて再起動します。  

7.  役割を次のように構成します。  

    -   **グラフィカルな方法**  

        1.  **ServerManager.exe** を実行してサーバー グループを作成し、すべてのサーバー ノードを追加します。  

        2.  各ノードに**ファイル サーバー**と**記憶域レプリカ**の役割と機能をインストールし、再起動します。  

    -   **Windows PowerShell による方法**  

        SR-SRV06 またはリモート管理コンピューターの Windows PowerShell コンソールで、次のコマンドを実行して必要な機能と役割をインストールし、再起動します。  

        ```  
        $Servers = 'SR-SRV05','SR-SRV06'  

        $Servers | ForEach { Install-WindowsFeature -ComputerName $_ -Name Storage-Replica,FS-FileServer -IncludeManagementTools -restart }  
        ```  

        詳細については、「[役割、役割サービス、または機能のインストールまたはアンインストール](http://technet.microsoft.co/library/hh831809.aspx)」を参照してください。  

8.  記憶域を次のように構成します。  

    > [!IMPORTANT]  
    > -   各格納装置で、データ用に 1 つとログ用に 1 つの 2 つのボリュームを作成する必要があります。  
    > -   ログ ディスクとデータ ディスクは、MBR ではなく GPT として初期化する必要があります。  
    > -   2 つのデータ ボリュームのサイズは同じでなければなりません。  
    > -   2 つのログ ボリュームのサイズは同じでなければなりません。  
    > -   すべてのレプリケートされたデータ ディスクには、同一のセクター サイズが必要です。  
    > -   すべてのログ ディスクのセクター サイズは、同じである必要があります。  
    > -   ログ ボリュームには、SSD など、フラッシュ ベースのストレージを使用する必要があります。 ログ ストレージには、データ ストレージよりも大きな速度を確保することをお勧めします。 ログ ボリュームは、絶対に他のワークロードに使用しないでください。
    > -   データ ディスクには、HDD、SSD、または階層型の組み合わせを使用でき、ミラーまたはパリティ スペース、RAID 1 または 10、RAID 5 または RAID 50 のいずれかを使用できます。  
    > -   ログ ボリュームは既定で 9 GB 以上である必要があり、ログ要件に応じて拡大または縮小する可能性もあります。  
    > -   ファイル サーバーの役割は、テスト用に必須ファイアウォール ポートを開くため、Test-SRTopology の動作にのみ必要です。
    
    - **JBOD 格納装置の場合:**  

        1.  各サーバーがそのサイトのストレージ格納装置のみを参照できることと、SAS 接続が正しく構成されていることを確認します。  

        2.  記憶域スペースを使用して記憶域をプロビジョニングします。これには、「[スタンドアロン サーバーに記憶域スペースを展開する](http://technet.microsoft.com/library/jj822938.aspx)」の**手順 1 - 3** に従い、Windows PowerShell またはサーバー マネージャーを使用します。  

    - **iSCSI ストレージの場合:**  

        1.  各クラスターがそのサイトのストレージ格納装置のみを参照できることを確認します。 iSCSI を使用する場合は、複数の単一ネットワーク アダプターを使用する必要があります。    

        2.  ベンダーのドキュメントを参照して記憶域をプロビジョニングします。 Windows ベースの iSCSI ターゲットを使用する場合は、「[iSCSI ターゲット ブロック記憶域: 操作方法](http://technet.microsoft.com/library/hh848268.aspx)」を参照してください。  

    - **FC SAN ストレージの場合:**  

        1.  各クラスターがそのサイトのストレージ格納装置のみを参照できることと、ホストのゾーンが正しく設定されていることを確認します。   

        2.  ベンダーのドキュメントを参照して記憶域をプロビジョニングします。  

    - **ローカル固定ディスク (DAS) 記憶域の場合:**  

        -   記憶域にシステム ボリューム、ページ ファイル、ダンプ ファイルが含まれていないことを確認します。  

        -   ベンダーのドキュメントを参照して記憶域をプロビジョニングします。  

9. Windows PowerShell を起動し、**Test-SRTopology** コマンドレットを使用して、記憶域レプリカのすべての要件を満たしているかどうかを判別します。 このコマンドレットは、簡単なテストのために要件のみモードで使用することも、実行時間の長いパフォーマンス評価モードで使用することもできます。  

    たとえば、それぞれ **F:** と **G:** のボリュームがあるノード候補を検証して、テストを 30 分間実行する場合は次のようになります。  

        MD c:\temp  

        Test-SRTopology -SourceComputerName SR-SRV05 -SourceVolumeName f: -SourceLogVolumeName g: -DestinationComputerName SR-SRV06 -DestinationVolumeName f: -DestinationLogVolumeName g: -DurationInMinutes 30 -ResultPath c:\temp  

    > [!IMPORTANT]
      > 評価期間中に指定したソース ボリュームに対する書き込み IO 負荷のないテスト サーバーを使用している場合は、ワークロードの追加を検討してください。負荷がない場合、有用なレポートは生成されません。 実際の数値および推奨されるログのサイズを得るには、実稼働環境と同様のワークロードでテストする必要があります。 または、単に、テスト中にソース ボリュームにいくつかのファイルをコピーするか、[DISKSPD](https://gallery.technet.microsoft.com/DiskSpd-a-robust-storage-6cd2f223) をダウンロードして実行することでも書き込み I/O を生成できます。 たとえば、D: ボリュームに対する 10 分間の低書き込み IO ワークロードによる例を次に示します。  
      >
      > `Diskspd.exe -c1g -d600 -W5 -C5 -b8k -t2 -o2 -r -w5 -i100 d:\test` 

10. **TestSrTopologyReport.html** レポートを調べて、記憶域レプリカの要件を満たしていることを確認します。  

    ![トポロジのレポートを表示している画面](media/Server-to-Server-Storage-Replication/SRTestSRTopologyReport.png)  

## <a name="configure-server-to-server-replication-using-windows-powershell"></a>Windows PowerShell を使用してサーバー間のレプリケーションを構成する  
次に、Windows PowerShell を使用してサーバー間のレプリケーションを構成します。 次のすべての手順は、ノード上で直接実行するか、Windows Server 2016 RSAT 管理ツールをインストールしたリモート管理コンピューターから実行する必要があります。  

無料のサーバー マネージャー ツール (SMT) を使用した記憶域レプリカのグラフィック管理がサポートされています。 この管理ツール セットのプレビュー版の提供状況については、Azure ドキュメントを確認してください。 このドキュメントは、SMT の一般提供開始後に更新されます。

1. PowerShell コンソールを管理者として使用していることを確認します。  
2. レプリケーション元とレプリケーション先のディスク、ログ、およびノードと、ログのサイズを指定して、サーバー間のレプリケーションを構成します。  

    ```PowerShell  
    New-SRPartnership -SourceComputerName sr-srv05 -SourceRGName rg01 -SourceVolumeName f: -SourceLogVolumeName g: -DestinationComputerName sr-srv06 -DestinationRGName rg02 -DestinationVolumeName f: -DestinationLogVolumeName g:  
    ```  

   出力:
   ```PowerShell
   DestinationComputerName : SR-SRV06
   DestinationRGName       : rg02
   SourceComputerName      : SR-SRV05
   PSComputerName          :
   ```

    > [!IMPORTANT]
    > 既定のログのサイズは 8 GB です。 `Test-SRTopology` コマンドレットの結果に応じて、より大きい値または小さい値を指定して -LogSizeInBytes を使用することを検討してください。  

2.  レプリケーション元とレプリケーション先の状態の取得するために、`Get-SRGroup` と `Get-SRPartnership` を次のとおり使用します。  

    ```PowerShell  
    Get-SRGroup  
    Get-SRPartnership  
    (Get-SRGroup).replicas  
    ```
    出力:

    ```PowerShell
    CurrentLsn             : 0
    DataVolume             : F:\
    LastInSyncTime         :
    LastKnownPrimaryLsn    : 1
    LastOutOfSyncTime      :
    NumOfBytesRecovered    : 37731958784
    NumOfBytesRemaining    : 30851203072
    PartitionId            : c3999f10-dbc9-4a8e-8f9c-dd2ee6ef3e9f
    PartitionSize          : 68583161856
    ReplicationMode        : synchronous
    ReplicationStatus      : InitialBlockCopy
    PSComputerName         :
    ```

3.  次のようにレプリケーションの進行状況を確認します。  

    1.  レプリケーション元サーバーで、次のコマンドを入力し、イベント 5015、5002、5004、1237、5001、2200 を調べます。  

        ```PowerShell  
        Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica -max 20  
        ```  

    2.  レプリケーション先サーバーで、次のコマンドを実行して、パートナーシップの作成を示す記憶域レプリカ イベントを参照します。 このイベントでは、コピーされたバイト数およびかかった時間が示されます。 以下に例を示します。  

        ```PowerShell  
        Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica | Where-Object {$_.ID -eq "1215"} | fl  

        TimeCreated  : 4/8/2016 4:12:37 PM  
        ProviderName : Microsoft-Windows-StorageReplica  
        Id           : 1215  
        Message      : Block copy completed for replica.  

                ReplicationGroupName: rg02  
                ReplicationGroupId: {616F1E00-5A68-4447-830F-B0B0EFBD359C}  
                ReplicaName: f:\  
                ReplicaId: {00000000-0000-0000-0000-000000000000}  
                End LSN in bitmap:   
                LogGeneration: {00000000-0000-0000-0000-000000000000}  
                LogFileId: 0  
                CLSFLsn: 0xFFFFFFFF  
                Number of Bytes Recovered: 68583161856  
                Elapsed Time (ms): 117  
        ```  

        > [!NOTE]
        > 記憶域レプリカによって、インストール先のボリュームとそのドライブ文字またはマウント ポイントがマウント解除されます。 これは仕様です。  

    3.  または、レプリカのレプリケーション先サーバー グループでは、コピーの残りのバイト数が常時示されており、PowerShell を使って照会できます。 以下に例を示します。  

        ```  
        (Get-SRGroup).Replicas | Select-Object numofbytesremaining  
        ```  

        進行状況を確認するサンプルを次に示します (サンプルは終了されません)。  

        ```  
        while($true) {  

         $v = (Get-SRGroup -Name "RG02").replicas | Select-Object numofbytesremaining  
         [System.Console]::Write("Number of bytes remaining: {0}`r", $v.numofbytesremaining)  
         Start-Sleep -s 5  
        }  
        ```  

    4.  レプリケーション先サーバーで次のコマンドを実行し、イベント 5009、1237、5001、5015、5005、2200 を調べて、処理の進行状況を把握します。 このシーケンスではエラーの警告が存在しない必要があります。 イベント 1237 が多くあります。これは進行状況を示します。  

        ```  
        Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica | FL  
        ```  

## <a name="manage-replication"></a>レプリケーションを管理する  
これで、サーバー間のレプリケートされたインフラストラクチャを管理および運用できるようになります。 次のすべての手順は、ノード上で直接実行することも、Windows Server 2016 RSAT 管理ツールをインストール済みのリモート管理コンピューターから実行することもできます。  

1.  `Get-SRPartnership` と `Get-SRGroup` を使用して、現在のレプリケーション元とレプリケーション先およびそれらの状態を判別します。  

2.  レプリケーションのパフォーマンスを測定するには、ソースと宛先の両方のノードで `Get-Counter` コマンドレットを使用します。 カウンター名は次のとおりです。  

    -   \Storage Replica Partition I/O Statistics(*)\Number of times flush paused  

    -   \Storage Replica Partition I/O Statistics(*)\Number of pending flush I/O  

    -   \Storage Replica Partition I/O Statistics(*)\Number of requests for last log write  

    -   \Storage Replica Partition I/O Statistics(*)\Avg. Flush Queue Length  

    -   \Storage Replica Partition I/O Statistics(*)\Current Flush Queue Length  

    -   \Storage Replica Partition I/O Statistics(*)\Number of Application Write Requests  

    -   \Storage Replica Partition I/O Statistics(*)\Avg. Number of requests per log write  

    -   \Storage Replica Partition I/O Statistics(*)\Avg. App Write Latency  

    -   \Storage Replica Partition I/O Statistics(*)\Avg. App Read Latency  

    -   \Storage Replica Statistics(*)\Target RPO  

    -   \Storage Replica Statistics(*)\Current RPO  

    -   \Storage Replica Statistics(*)\Avg. Log Queue Length  

    -   \Storage Replica Statistics(*)\Current Log Queue Length  

    -   \Storage Replica Statistics(*)\Total Bytes Received  

    -   \Storage Replica Statistics(*)\Total Bytes Sent  

    -   \Storage Replica Statistics(*)\Avg. Network Send Latency  

    -   \Storage Replica Statistics(*)\Replication State  

    -   \Storage Replica Statistics(*)\Avg. Message Round Trip Latency  

    -   \Storage Replica Statistics(*)\Last Recovery Elapsed Time  

    -   \Storage Replica Statistics(*)\Number of Flushed Recovery Transactions  

    -   \Storage Replica Statistics(*)\Number of Recovery Transactions  

    -   \Storage Replica Statistics(*)\Number of Flushed Replication Transactions  

    -   \Storage Replica Statistics(*)\Number of Replication Transactions  

    -   \Storage Replica Statistics(*)\Max Log Sequence Number  

    -   \Storage Replica Statistics(*)\Number of Messages Received  

    -   \Storage Replica Statistics(*)\Number of Messages Sent  

    Windows PowerShell でのパフォーマンス カウンターの詳細については、「[Get-Counter](http://technet.microsoft.com/library/hh849685.aspx)」を参照してください。  

3.  レプリケーションの方向を片方のサイトから移すには、`Set-SRPartnership` コマンドレットを使用します。  

    ```  
    Set-SRPartnership -NewSourceComputerName sr-srv06 -SourceRGName rg02 -DestinationComputerName sr-srv05 -DestinationRGName rg01  
    ```  

    > [!WARNING]  
    > Windows Server 2016 では、初期同期の進行中に役割の切り替えを行うことができません。このため、初期レプリケーションが完了する前に役割を切り替えようとするとデータの損失につながります。 最初の同期が完了するまでは、強制的に方向を切り替えないでください。  

    イベント ログを調べてレプリケーションの方向の変更と回復モードが発生しているかどうかを確認し、調整してください。 調整後、書き込み IO で、新しいレプリケーション元サーバーの所有する記憶域に書き込むことができます。 レプリケーションの方向を変更すると、前のソース コンピューター上で書き込み IO がブロックされます。  

4.  レプリケーションを削除するには、各ノードで `Get-SRGroup`、`Get-SRPartnership`、`Remove-SRGroup`、および `Remove-SRPartnership` を使用します。 `Remove-SRPartnership` コマンドレットは、レプリケーション先サーバーではなく、現在のレプリケーション ソース上でのみ実行してください。 両方のサーバーで `Remove-Group` を実行します。 たとえば、2 台のサーバーからすべてのレプリケーションを削除するには、次の手順に従います。  

    ```  
    Get-SRPartnership  
    Get-SRPartnership | Remove-SRPartnership  
    Get-SRGroup | Remove-SRGroup  
    ```  

## <a name="replacing-dfs-replication-with-storage-replica"></a>DFS レプリケーションを記憶域レプリカに置き換える  
多くの Microsoft ユーザーは、ホーム フォルダーおよび部門別の共有のような非構造化ユーザー データの災害復旧ソリューションとして、DFS レプリケーションを展開しています。 DFS レプリケーションは、Windows Server 2003 R2 以降のすべてのオペレーティング システムに付属しており、帯域幅の狭いネットワークで動作するため、ノードが多数あり、待機時間が長く変更の少ない環境に適しています。 ただし、DFS レプリケーションには、データ レプリケーション ソリューションとして重要な以下の制限があります。  
* 使用中のファイルや開いているファイルはレプリケートされません。  
* レプリケーションは同期的に行われません。  
* 非同期レプリケーションの待機期間は数分、数時間、または数日かかることがあります。  
* 電源中断の後に時間のかかる一貫性チェックが必要になるデータベースを使用します。  
* 通常はマルチマスターとして構成されおり、双方向のフローを変更することができるため、より新しいデータが上書きされる可能性があります。  

記憶域レプリカには、これらの欠点はありません。 ただし、いくつかの制限はあり、環境によっては利点が薄くなる可能性があります。  

* ボリューム間で実行できるのは 1 対 1 のレプリケーションのみです。 複数のサーバー間で異なるボリュームをレプリケートすることはできます。  
* 非同期レプリケーションはサポートされますが、帯域幅が狭く待機時間の長いネットワーク向けには設計されていません。  
* レプリケーションの実行中、ユーザーはレプリケーション先の保護されたデータにアクセスできません。  

これらの要素が障害とならない場合は、記憶域レプリカを使用し、DFS レプリケーション サーバーをこの新しいテクノロジで置き換えることができます。   
このプロセスの概要は次のとおりです。  

1.  2 台のサーバーに Windows Server 2016 をインストールして記憶域を構成します。 環境によっては、既存の一連のサーバーのアップグレードまたはクリーン インストールを行うことになります。  
2.  レプリケートするデータが C ドライブ以外の 1 つ以上のデータ ボリューム上に存在することを確認します。   
」を参照します。  バックアップやファイルのコピー、シン プロビジョニングされた記憶域を使用して片方のサーバー上のデータをシードし、時間を節約することもできます。 DFS レプリケーションとは異なり、メタデータのようなセキュリティを完全に一致させる必要はありません。  
3.  レプリケーション元サーバー上でデータを共有し、DFS 名前空間を介してアクセスできるようにします。 これは、サーバー名が障害の発生しているサイトにあるサーバーの名前に変更された場合でも、ユーザーがサーバーにアクセスできるようにするために重要です。  
」を参照します。  レプリケーション先サーバーで一致する共有を作成することができます。この共有は、通常の操作中には利用できません。   
b.  レプリケーション先サーバーを DFS 名前空間の名前空間に追加しないでください。追加する場合は、すべてのフォルダー ターゲットを無効にしてください。  
4.  記憶域レプリカのレプリケーションを有効にして、初回の同期を完了します。レプリケーションは、同期的と非同期的のどちらでも実行できます。   
」を参照します。  ただし、レプリケーション先サーバーでの IO データの一貫性を保つために、同期的に実行することをお勧めします。   
b.  ボリューム シャドウ コピーを有効にして、VSSADMIN またはその他のお好みのツールで定期的にスナップショットを撮ることを強くお勧めします。 これによって、アプリケーションは一貫してデータ ファイルをディスクにフラッシュするようになります。 障害が発生した場合、レプリケーション先サーバー上の部分的に非同期レプリケート済みのスナップショットからファイルを回復できます。 スナップショットは、ファイルと共にレプリケートされます。  
5.  障害が発生するまでは正常に動作します。  
6.  レプリケーション先サーバーを新しいソース サーバーに切り替えると、このサーバーのレプリケート済みボリュームがユーザーに示されます。  
7.  同期レプリケーションを使用している場合、ソース サーバーの損失時にユーザーがトランザクション保護なし (これはレプリケーションには関係ありません) でデータを書き込むアプリケーションを使用していない限り、データの復元は必要ありません。 非同期レプリケーションを使用している場合、VSS スナップショットをマウントする必要性が高くなりますが、アプリケーションのスナップショットの一貫性を保つため、どのような場合でも VSS の使用を検討してください。  
8.  DFS 名前空間のフォルダー ターゲットとして、サーバーおよびその共有を追加します。   
9.  これによって、ユーザーがデータにアクセスできるようになります。  

 > [!NOTE]
 > 障害回復の計画は複雑な問題であるため、細心の注意が必要です。 Runbook の作成と、年単位でのライブ フェールオーバー ドリルの実行を強くお勧めします。 実際の障害発生時には混乱の中での対応となり、また経験豊富な担当者は手が空いていない場合もあります。  

## <a name="related-topics"></a>関連トピック  
- [記憶域レプリカの概要](storage-replica-overview.md)  
- [共有記憶域を使用したストレッチ クラスター レプリケーション](stretch-cluster-replication-using-shared-storage.md)  
- [クラスター間の記憶域のレプリケーション](cluster-to-cluster-storage-replication.md)
- [記憶域レプリカ: 既知の問題](storage-replica-known-issues.md)  
- [記憶域レプリカ: よく寄せられる質問](storage-replica-frequently-asked-questions.md)  

## <a name="see-also"></a>関連項目  
- [Windows Server 2016](../../get-started/windows-server-2016.md)  
- [Windows Server 2016 の記憶域スペース ダイレクト](../storage-spaces/storage-spaces-direct-overview.md)  
