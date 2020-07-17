---
title: クラスター間の記憶域のレプリケーション
ms.prod: windows-server
manager: siroy
ms.author: nedpyle
ms.technology: storage-replica
ms.topic: get-started-article
ms.assetid: 834e8542-a67a-4ba0-9841-8a57727ef876
author: nedpyle
ms.date: 04/26/2019
description: 記憶域レプリカを使用して、あるクラスターのボリュームを、Windows Server を実行している別のクラスターにレプリケートする方法について説明します。
ms.openlocfilehash: 21e054d42d0264bb22fbd0e02382ee429958a597
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475669"
---
# <a name="cluster-to-cluster-storage-replication"></a>クラスター間の記憶域のレプリケーション

> 適用先:Windows Server 2019、Windows Server 2016、Windows Server (半期チャネル)

記憶域レプリカは、記憶域スペースダイレクトを使用したクラスターのレプリケーションなど、クラスター間でボリュームをレプリケートできます。 管理と構成は、サーバー間のレプリケーションに似ています。

これらのコンピューターと記憶域をクラスター間構成で構成します。クラスター間構成では、1 つのクラスターがそれ自体の一連の記憶域、および別のクラスターとその一連の記憶域をレプリケートします。 これらのノードとその記憶域は、個別の物理サイトにある必要がありますが、ただし必須ではありません。

> [!IMPORTANT]
> このテストでは、4 台のサーバーは一例です。 各クラスターでは、Microsoft がサポートしている任意の数のサーバーを使用できます。これは現在、記憶域スペースダイレクトクラスターの場合は8、共有記憶域クラスターの場合は64です。
>
> このガイドでは、記憶域スペース ダイレクトの構成については説明しません。 記憶域スペースダイレクトの構成の詳細については、「[記憶域スペースダイレクトの概要](../storage-spaces/storage-spaces-direct-overview.md)」を参照してください。

このチュートリアルでは、例として次の環境を使用します。

-   後で **SR-SRVCLUSA** というクラスターを構成する 2 台のメンバー サーバー **SR-SRV01** と **SR-SRV02**。

-   後で **SR-SRVCLUSB** というクラスターを構成する 2 台のメンバー サーバー **SR-SRV03** と **SR-SRV04**。

-   2 つの異なるデータ センターを表す 2 つの論理 "サイト" である **Redmond** と **Bellevue**。

![例の環境を示す図。Redmond サイトのクラスターで Bellevue サイトのクラスターがレプリケートされます](./media/Cluster-to-Cluster-Storage-Replication/SR_ClustertoCluster.png)

**図 1: クラスター間のレプリケーション**

## <a name="prerequisites"></a>前提条件

* Active Directory Domain Services フォレスト (Windows Server 2016 を実行する必要はありません)。
* 4-128 サーバー (2-64 サーバーの2つのクラスター) は、Windows Server 2019 または Windows Server 2016 (Datacenter Edition) を実行しています。 Windows Server 2019 を実行している場合は、通常は Standard Edition を使用することができます。これにより、1つのボリュームのみを最大 2 TB までレプリケートできます。
* SAS JBOD、ファイバー チャネル SAN、共有 VHDX、記憶域スペース ダイレクト、または iSCSI ターゲットを使う 2 セットのストレージ。 記憶域では HDD メディアと SSD メディアを混在させる必要があります。 各記憶域は、クラスター間に共有アクセスなしで、各クラスターでのみ利用可能となるように設定します。
* 記憶域の各セットでは、2 つ以上 (1 つはレプリケートされたデータ用、1 つはログ用) の仮想ディスクの作成が許可される必要があります。 物理記憶域のセクター サイズは、すべてのデータ ディスクで同じである必要があります。 物理記憶域のセクター サイズは、すべてのログ ディスクで同じである必要があります。
* 同期レプリケーションのために各サーバーで少なくとも 1 つのイーサネット/TCP 接続 (可能であれば RDMA)。
* すべてのノード間で ICMP、SMB (ポート 445、SMB ダイレクト用に 5445)、WS-MAN (ポート 5985) の双方向トラフィックを許可する適切なファイアウォールおよびルーター ルール。
* 書き込みの IO 負荷に十分対応できる帯域幅を持ちラウンド トリップ遅延時間が平均 5 ミリ秒である、同期レプリケーション用のサーバー間ネットワーク。 非同期レプリケーションには、遅延時間に関する推奨事項はありません。
* レプリケート対象の記憶域を、Windows オペレーティング システムのフォルダーが含まれるドライブに配置することはできません。
* 記憶域スペースダイレクトレプリケーションの & には、重要な考慮事項があります。以下の詳細情報を確認してください。

これらの要件の多くは、`Test-SRTopology` コマンドレットを使用して判別できます。 記憶域レプリカまたは記憶域レプリカ管理ツール機能を 1 つ以上のサーバーにインストールすると、このツールにアクセスできるようになります。 このツールを使用するために、記憶域レプリカを構成する必要はありません。記憶域レプリカは、コマンドレットをインストールするためだけに構成します。 詳細は、以下の手順に記載されています。

## <a name="step-1-provision-operating-system-features-roles-storage-and-network"></a>手順 1: オペレーティング システム、機能、役割、記憶域、およびネットワークのプロビジョニング

1.  Windows server **(デスクトップエクスペリエンス)** のインストールの種類を使用して、4つのサーバーノードすべてに windows server をインストールします。

2.  ネットワークの情報を追加し、ドメインに参加させてから再起動します。

    > [!IMPORTANT]
    > この時点以降は、常に、すべてのサーバーでビルトイン Administrator グループのメンバーであるドメイン ユーザーとしてログオンします。 今後、グラフィカルなサーバーのインストールまたは Windows 10 コンピューターで実行するとき、Windows PowerShell および CMD プロンプトを昇格してください。

3.  JBOD 記憶域エンクロージャ、iSCSI ターゲット、FC SAN、またはローカルの固定ディスク (DAS) 記憶域の最初のセットをサイト **Redmond** 内のサーバーに接続します。

4.  記憶域の 2 つめのセットをサイト **Bellevue** 内のサーバーに接続します。

5.  必要に応じて、4 つのすべてのノードに、ベンダー ストレージとエンクロージャの最新のファームウェアとドライバー、最新のベンダー HBA ドライバー、最新のベンダー BIOS および UEFI ファームウェア、最新のベンダー ネットワーク ドライバー、およびマザーボード チップセットの最新のドライバーをインストールします。 必要に応じてノードを再起動します。

    > [!NOTE]
    > 共有記憶域およびネットワーク ハードウェアの構成については、ハードウェア ベンダーのドキュメントを参照してください。

6.  サーバーの BIOS および UEFI の設定が、C 状態の無効化、QPI 速度の設定、NUMA の有効化、最大メモリ動作周波数の設定など、高パフォーマンスを有効にする設定であることを確認します。 Windows Server での電源管理が高パフォーマンスに設定されていることを確認します。 必要に応じて再起動します。

7.  役割を次のように構成します。

    -   **グラフィカルな方法**

        1.  **ServerManager.exe** を実行し、すべてのサーバー ノードを追加してサーバー グループを作成します。

        2.  **ファイル サーバー**と**記憶域レプリカ**の役割と機能を各ノードでインストールし、再起動します。

    -   **Windows PowerShell による方法**

        SR-SRV04 またはリモート管理コンピューター上で、Windows PowerShell コンソール内で次のコマンドを実行して、4 つのノード上でストレッチ クラスター用に必要な機能と役割をインストールし、ノードを再起動します。

        ```PowerShell
        $Servers = 'SR-SRV01','SR-SRV02','SR-SRV03','SR-SRV04'

        $Servers | ForEach { Install-WindowsFeature -ComputerName $_ -Name Storage-Replica,Failover-Clustering,FS-FileServer -IncludeManagementTools -restart }
        ```

        これらの手順の詳細については、「[役割、役割サービス、または機能のインストールまたはアンインストール](../../administration/server-manager/install-or-uninstall-roles-role-services-or-features.md)」を参照してください。

9. 記憶域を次のように構成します。

    > [!IMPORTANT]
    > -   各格納装置で、データ用に 1 つとログ用に 1 つの 2 つのボリュームを作成する必要があります。
    > -   ログとデータのディスクは **MBR** ではなく **GPT** として初期化する必要があります。
    > -   2 つのデータ ボリュームのサイズは同じでなければなりません。
    > -   2 つのログ ボリュームのサイズは同じでなければなりません。
    > -   すべてのレプリケートされたデータ ディスクには、同一のセクター サイズが必要です。
    > -   すべてのログ ディスクのセクター サイズは、同じである必要があります。
    > -   ログ ボリュームには、SSD など、フラッシュ ベースのストレージを使用する必要があります。  ログ ストレージには、データ ストレージよりも大きな速度を確保することをお勧めします。 ログ ボリュームは、絶対に他のワークロードに使用しないでください。
    > -   データ ディスクには、HDD、SSD、または階層型の組み合わせを使用でき、ミラーまたはパリティ スペースか、RAID 1 または 10 もしくは RAID 5 または RAID 50 のいずれかを使用できます。
    > -   ログボリュームは、既定では 8 GB 以上である必要があり、ログ要件に基づいて、より大きいか小さくなることがあります。
    > -   NVME または SSD のキャッシュで記憶域スペースダイレクト (記憶域スペースダイレクト) を使用すると、記憶域スペースダイレクトクラスター間で記憶域レプリカのレプリケーションを構成するときに予想よりも長い待機時間が増加することがわかります。 待機時間の変更は、パフォーマンス + 容量の構成で NVME と SSD を使用する場合よりも大幅に高くなります。また、HDD 階層も容量レベルもありません。

    この問題は、低速メディアと比べて、SR のログメカニズムにおけるアーキテクチャの制限により、NVME の待機時間が非常に短いことが原因で発生します。 記憶域スペースダイレクト記憶域スペースダイレクトキャッシュを使用する場合、すべての最新の読み取り/書き込み IO と共に、SR ログのすべての IO がキャッシュ内で発生し、パフォーマンスレベルまたは容量レベルには反映されません。 これは、すべての SR アクティビティが同じ速度のメディアで行われることを意味します。この構成はサポートされていません ( https://aka.ms/srfaq ログの推奨事項については、「」を参照してください)。

    Hdd で記憶域スペースダイレクトを使用する場合、キャッシュを無効にしたり回避したりすることはできません。 回避策として、SSD と NVME のみを使用する場合は、パフォーマンスレベルと容量レベルのみを構成できます。 この構成を使用していて、そのサービスがキャパシティレベルのみにあるデータボリュームに対してのみ、パフォーマンスレベルに SR ログを配置した場合は、前述の高待機時間の問題を回避できます。 これは、高速で低速な Ssd と NVME が混在している場合にも実行できます。

    この回避策はもちろん理想的ではなく、一部のお客様はそれを利用できない可能性があります。 SR チームは、今後発生する人為的なボトルネックを減らすために、最適化および更新されたログメカニズムを使用しています。 これには ETA はありませんが、テストのために顧客をタップできる場合は、この FAQ が更新されます。

-   **JBOD 格納装置の場合:**

1. 各クラスターがそのサイトの記憶域エンクロージャのみを参照できることと、SAS 接続が正しく構成されていることを確認します。

2. 記憶域スペースを使用して記憶域をプロビジョニングします。これには、「[スタンドアロン サーバーに記憶域スペースを展開する](../storage-spaces/deploy-standalone-storage-spaces.md)」の**手順 1 - 3** に従い、Windows PowerShell またはサーバー マネージャーを使用します。

-   **iSCSI ターゲット記憶域の場合:**

1. 各クラスターがそのサイトのストレージ格納装置のみを参照できることを確認します。 iSCSI を使用する場合は、複数の単一ネットワーク アダプターを使用する必要があります。

2. ベンダーのドキュメントを参照して記憶域をプロビジョニングします。 Windows ベースの iSCSI ターゲットを使用する場合は、「[iSCSI ターゲット ブロック記憶域: 操作方法](../iscsi/iscsi-target-server.md)」を参照してください。

-   **FC SAN ストレージの場合:**

1. 各クラスターがそのサイトのストレージ格納装置のみを参照できることと、ホストのゾーンが正しく設定されていることを確認します。

2. ベンダーのドキュメントを参照して記憶域をプロビジョニングします。

-   **記憶域スペース ダイレクトの場合:**

1. 記憶域スペース ダイレクトを展開することで、各クラスターがそのサイトのストレージ格納装置のみを参照できることを確認します。 (https://docs.microsoft.com/windows-server/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)

2. SR ログ ボリュームが常に最も高速なフラッシュ ストレージに配置され、データ ボリュームが低速な大容量ストレージに配置されることを確認します。

3. Windows PowerShell を起動し、`Test-SRTopology` コマンドレットを使用して、記憶域レプリカのすべての要件を満たしているかどうかを判別します。 このコマンドレットは、簡単なテストのために要件のみモードで使用することも、実行時間の長いパフォーマンス評価モードで使用することもできます。
   たとえば、オブジェクトに適用された

   ```PowerShell
   MD c:\temp

   Test-SRTopology -SourceComputerName SR-SRV01 -SourceVolumeName f: -SourceLogVolumeName g: -DestinationComputerName SR-SRV03 -DestinationVolumeName f: -DestinationLogVolumeName g: -DurationInMinutes 30 -ResultPath c:\temp
   ```

     > [!IMPORTANT]
     > 評価期間中に指定されたソース ボリューム上で書き込み IO 負荷のないテスト サーバーを使用している場合は、ワークロードの追加を検討してください。そうしないと、有用なレポートは生成されません。 実際の数値および推奨されるログのサイズを確認するには、実稼働環境と同様のワークロードでテストする必要があります。 または、テスト中にソースボリュームにいくつかのファイルをコピーするか、 [Diskspd](https://gallery.technet.microsoft.com/DiskSpd-a-robust-storage-6cd2f223)をダウンロードして実行し、書き込み io を生成します。 たとえば、D: ボリュームに対する5分間の低書き込み IO ワークロードの例を次に示します。`Diskspd.exe -c1g -d300 -W5 -C5 -b8k -t2 -o2 -r -w5 -h d:\test.dat`

4. **TestSrTopologyReport.html** レポートを調べて、記憶域レプリカの要件を満たしていることを確認します。

   ![レプリケーション トポロジのレポートの結果を示す画面](./media/Cluster-to-Cluster-Storage-Replication/SRTestSRTopologyReport.png)

## <a name="step-2-configure-two-scale-out-file-server-failover-clusters"></a>手順 2: 2 つのスケールアウト ファイル サーバー フェールオーバー クラスターを構成する
ここで、2 つの通常のフェールオーバー クラスターを作成します。 構成、検証、テストを完了した後で、記憶域レプリカを使用してレプリケートします。 次のすべての手順は、クラスターノードで直接実行することも、Windows Server リモートサーバー管理ツールを含むリモート管理コンピューターから実行することもできます。

### <a name="graphical-method"></a>グラフィカルな方法

1.  各サイト内でノードに対して **cluadmin.msc** を実行します。

2.  提案されたクラスターを検証し、結果を分析して、続行できることを確認します。 以下で使用している例では **SR-SRVCLUSA** と **SR-SRVCLUSB** です。

3.  2 つのクラスターを作成します。 クラスター名が 15 文字以下であることを確認します。

4.  ファイル共有監視またはクラウド監視を構成します。

    > [!NOTE]
    > WIndows Server には、クラウド (Azure) ベースの監視のオプションが追加されました。 ファイル共有監視に代えてこのクォーラム オプションを選択できます。

    > [!WARNING]
    > クォーラム構成の詳細については、「[クォーラムの構成と管理](../../failover-clustering/manage-cluster-quorum.md)」の「**監視の構成**」セクションを参照してください。 `Set-ClusterQuorum` コマンドレットの詳細については、「[Set-ClusterQuorum](https://docs.microsoft.com/powershell/module/failoverclusters/set-clusterquorum)」を参照してください。

5.  **Redmond** サイトでクラスター CSV に 1 台のディスクを追加します。 これを行うには、**[記憶域]** セクションの **[ディスク]** ノードでソース ディスクを右クリックして、**[クラスターの共有ボリュームへの追加]** をクリックします。

6.  [スケールアウト ファイル サーバーの構成](https://technet.microsoft.com/library/hh831718.aspx)の手順に従って、両方のクラスターにクラスター化されたスケールアウト ファイル サーバーを作成します。

### <a name="windows-powershell-method"></a>Windows PowerShell による方法

1.  提案されたクラスターをテストし、結果を分析して、続行できることを確認します。

    ```PowerShell
    Test-Cluster SR-SRV01,SR-SRV02
    Test-Cluster SR-SRV03,SR-SRV04
    ```

2.  クラスターを作成します (クラスターには独自の静的 IP アドレスを指定する必要があります)。 各クラスター名が 15 文字以下であることを確認します。

    ```PowerShell
    New-Cluster -Name SR-SRVCLUSA -Node SR-SRV01,SR-SRV02 -StaticAddress <your IP here>
    New-Cluster -Name SR-SRVCLUSB -Node SR-SRV03,SR-SRV04 -StaticAddress <your IP here>
    ```

3.  ドメイン コントローラーまたはその他のなんらかの独立したサーバーでホストされている共有を指す各クラスター内でファイル共有監視またはクラウド (Azure) 監視を構成します。 次に例を示します。

    ```PowerShell
    Set-ClusterQuorum -FileShareWitness \\someserver\someshare
    ```

    > [!NOTE]
    > WIndows Server には、クラウド (Azure) ベースの監視のオプションが追加されました。 ファイル共有監視に代えてこのクォーラム オプションを選択できます。

    > [!WARNING]
    > クォーラム構成の詳細については、「[クォーラムの構成と管理](../../failover-clustering/manage-cluster-quorum.md)」の「**監視の構成**」セクションを参照してください。 `Set-ClusterQuorum` コマンドレットの詳細については、「[Set-ClusterQuorum](https://docs.microsoft.com/powershell/module/failoverclusters/set-clusterquorum)」を参照してください。

4.  [スケールアウト ファイル サーバーの構成](https://technet.microsoft.com/library/hh831718.aspx)の手順に従って、両方のクラスターにクラスター化されたスケールアウト ファイル サーバーを作成します。

## <a name="step-3-set-up-cluster-to-cluster-replication-using-windows-powershell"></a>手順 3: Windows PowerShell を使用してクラスター間のレプリケーションを設定する
次に、Windows PowerShell を使用してクラスター間のレプリケーションを設定します。 次のすべての手順は、ノード上で直接実行することも、Windows Server が含まれているリモート管理コンピューターから実行することもできリモートサーバー管理ツール

1. 最初のクラスターの任意のノードで**Grant-sraccess**コマンドレットを実行して、またはリモートで、他のクラスターへのフルアクセスを最初のクラスターに許可します。  Windows Server リモートサーバー管理ツール

   ```PowerShell
   Grant-SRAccess -ComputerName SR-SRV01 -Cluster SR-SRVCLUSB
   ```

2. 2番目のクラスター内の任意のノードで**grant-SRAccess**コマンドレットを実行して、またはリモートで、もう一方のクラスターに対して、2番目のクラスターへのフルアクセスを許可します。

   ```PowerShell
   Grant-SRAccess -ComputerName SR-SRV03 -Cluster SR-SRVCLUSA
   ```

3. ソースと宛先のディスク、ソースと宛先のログ、ソースと宛先のクラスター名、およびログのサイズを指定して、クラスター間のレプリケーションを構成します。 このコマンドは、サーバー上でローカルで実行するか、リモート管理コンピューターを使用して実行できます。

   ```powershell
   New-SRPartnership -SourceComputerName SR-SRVCLUSA -SourceRGName rg01 -SourceVolumeName c:\ClusterStorage\Volume2 -SourceLogVolumeName f: -DestinationComputerName SR-SRVCLUSB -DestinationRGName rg02 -DestinationVolumeName c:\ClusterStorage\Volume2 -DestinationLogVolumeName f:
   ```

   > [!WARNING]
   > 既定のログのサイズは 8 GB です。 **Test-srtopology**コマンドレットの結果に応じて、より大きい値または小さい値を指定して **-logsizeinbytes**を使用することもできます。

4. レプリケーション元とレプリケーション先の状態を取得するために、次のように **Get-SRGroup** と **Get-SRPartnership** を使用します。

   ```powershell
   Get-SRGroup
   Get-SRPartnership
   (Get-SRGroup).replicas
   ```

5. 次のようにレプリケーションの進行状況を確認します。

   1.  レプリケーション元サーバーで、次のコマンドを入力し、イベント 5015、5002、5004、1237、5001、2200 を調べます。

       ```PowerShell
       Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica -max 20
       ```
   2.  レプリケーション先サーバーで、次のコマンドを実行して、パートナーシップの作成を示す記憶域レプリカ イベントを参照します。 このイベントでは、コピーされたバイト数およびかかった時間が示されます。 例:

       ```powershell
       Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica | Where-Object {$_.ID -eq "1215"} | Format-List
       ```
       出力の例を次に示します。

       ```
       TimeCreated  : 4/8/2016 4:12:37 PM
       ProviderName : Microsoft-Windows-StorageReplica
       Id           : 1215
       Message      : Block copy completed for replica.
           ReplicationGroupName: rg02
           ReplicationGroupId:
           {616F1E00-5A68-4447-830F-B0B0EFBD359C}
           ReplicaName: f:\
           ReplicaId: {00000000-0000-0000-0000-000000000000}
           End LSN in bitmap:
           LogGeneration: {00000000-0000-0000-0000-000000000000}
           LogFileId: 0
           CLSFLsn: 0xFFFFFFFF
           Number of Bytes Recovered: 68583161856
           Elapsed Time (seconds): 117
       ```
   3. または、レプリカのレプリケーション先サーバー グループでは、コピーの残りのバイト数が常時示されており、PowerShell を使って照会できます。 次に例を示します。

      ```PowerShell
      (Get-SRGroup).Replicas | Select-Object numofbytesremaining
      ```

      進行状況サンプル (終了しません):

      ```PowerShell
        while($true) {
        $v = (Get-SRGroup -Name "Replication 2").replicas | Select-Object numofbytesremaining
        [System.Console]::Write("Number of bytes remaining: {0}`n", $v.numofbytesremaining)
        Start-Sleep -s 5
       }
       ```

6. 宛先クラスターの宛先サーバーで、次のコマンドを実行し、イベント 5009、1237、5001、5015、5005、2200 を調べて、処理の進行状況を把握します。 このシーケンスではエラーの警告が存在しない必要があります。 イベント 1237 が多くあります。これは進行状況を示します。

   ```PowerShell
   Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica | FL
   ```
   > [!NOTE]
   > 宛先クラスター ディスクは、レプリケート中は常に **[Online (No Access) (オンライン (アクセスなし))]** と表示されます。

## <a name="step-4-manage-replication"></a>手順 4: レプリケーションを管理する

次に、クラスター間レプリケーションの管理と操作を行います。 次のすべての手順は、クラスターノードで直接実行することも、Windows Server リモートサーバー管理ツールを含むリモート管理コンピューターから実行することもできます。

1.  **Get-ClusterGroup** または**フェールオーバー クラスター マネージャー**を使用して、レプリケーションの現在のソースと宛先およびそれらの状態を判別します。  Windows Server リモートサーバー管理ツール

2.  レプリケーションのパフォーマンスを測定するには、ソースと宛先の両方のノードで **Get-Counter** コマンドレットを使用します。 カウンター名は次のとおりです。

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

    Windows PowerShell でのパフォーマンス カウンターの詳細については、「[Get-Counter](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Diagnostics/Get-Counter)」を参照してください。

3.  1 つのサイトからレプリケーションの方向を移動するには、**Set-SRPartnership** コマンドレットを使用します。

    ```PowerShell
    Set-SRPartnership -NewSourceComputerName SR-SRVCLUSB -SourceRGName rg02 -DestinationComputerName SR-SRVCLUSA -DestinationRGName rg01
    ```

    > [!NOTE]
    > Windows Server では、初期同期の実行中に役割の切り替えが行われないようにします。これは、初期レプリケーションの完了を許可する前に切り替えようとした場合にデータが失われる可能性があるためです。 最初の同期が完了するまでは、強制的に方向を切り替えないでください。

    イベント ログを調べてレプリケーションの方向の変更と回復モードが発生しているかどうかを確認し、調整してください。 調整後、書き込み IO で、新しいレプリケーション元サーバーの所有する記憶域に書き込むことができます。 レプリケーションの方向を変更すると、前のソース コンピューター上で書き込み IO がブロックされます。

    > [!NOTE]
    > 宛先クラスター ディスクは、レプリケート中は常に **[Online (No Access) (オンライン (アクセスなし))]** と表示されます。

4.  ログサイズを既定の 8 GB から変更するには、ソースとターゲットの両方のストレージレプリカグループで**セット-SRGroup**を使用します。

    > [!IMPORTANT]
    > 既定のログのサイズは 8 GB です。 **Test-SRTopology** コマンドレットの結果に応じて、より大きい値または小さい値を指定して -LogSizeInBytes を使用することを検討してください。

5.  レプリケーションを削除するには、各クラスターで **Get-SRGroup**、**Get-SRPartnership**、**Remove-SRGroup**、および **Remove-SRPartnership** を使用します。

    ```powershell
    Get-SRPartnership | Remove-SRPartnership
    Get-SRGroup | Remove-SRGroup
    ```

    > [!NOTE]
    > 記憶域レプリカは、宛先ボリュームをマウント解除します。 これは仕様に基づく制限事項です。

## <a name="additional-references"></a>その他のリファレンス

-   [記憶域レプリカの概要](storage-replica-overview.md)
-   [共有記憶域を使用した拡張クラスターレプリケーション](stretch-cluster-replication-using-shared-storage.md)
-   [サーバー間の記憶域レプリケーション](server-to-server-storage-replication.md)
-   [記憶域レプリカ: 既知の問題](storage-replica-known-issues.md)
-   [記憶域レプリカ:よく寄せられる質問](storage-replica-frequently-asked-questions.md)
-   [Windows Server 2016 での記憶域スペース ダイレクト](../storage-spaces/storage-spaces-direct-overview.md)
