---
title: クラスター間の記憶域のレプリケーション
ms.prod: windows-server-threshold
manager: siroy
ms.author: nedpyle
ms.technology: storage-replica
ms.topic: get-started-article
ms.assetid: 834e8542-a67a-4ba0-9841-8a57727ef876
author: nedpyle
ms.date: 10/11/2017
description: 記憶域レプリカを使用して、Windows Server 2016 Datacenter Edition を実行しているクラスター間でボリュームをレプリケートする方法を説明します。
ms.openlocfilehash: 46bd5a53ff0e704844f10264a9f3a6fbe0e4d512
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838663"
---
# <a name="cluster-to-cluster-storage-replication"></a>クラスター間の記憶域のレプリケーション

> 適用対象:Windows Server 2016 の Windows Server (半期チャネル)

クラスター間のレプリケーションが、Windows Server 2016 Datacenter Edition で利用可能になりました。これには、記憶域スペース ダイレクト (つまり、共有のない、直接接続された記憶域) を使用したクラスターのレプリケーションが含まれます。 管理と構成は、サーバー間のレプリケーションに似ています。  

これらのコンピューターと記憶域をクラスター間構成で構成します。クラスター間構成では、1 つのクラスターがそれ自体の一連の記憶域、および別のクラスターとその一連の記憶域をレプリケートします。 これらのノードとその記憶域は個別の物理サイトに配置することをお勧めしますが、必須ではありません。  

記憶域レプリカをクラスター間のレプリケーション用に構成できるグラフィカルなツールは Windows Server 2016 Datacenter Edition に用意されていませんが、将来的には Azure Site Recovery でこのシナリオを構成できるようになる予定です。

> [!IMPORTANT]
> このテストでは、4 台のサーバーは一例です。 記憶域スペース ダイレクト クラスターの 8 および 64 ビットの共有記憶域クラスターでは現在、各クラスターで Microsoft によってサポートされているサーバーの任意の数を使用することができます。  
>   
> このガイドでは、記憶域スペース ダイレクトの構成については説明しません。 記憶域スペース ダイレクトを構成する方法の詳細については、「[Windows Server 2016 の記憶域スペース ダイレクト](../storage-spaces/storage-spaces-direct-overview.md)」を参照してください。  

このチュートリアルでは、例として、次の環境を使用します。  

-   後で **SR-SRVCLUSA** というクラスターを構成する 2 台のメンバー サーバー **SR-SRV01** と **SR-SRV02**。  

-   後で **SR-SRVCLUSB** というクラスターを構成する 2 台のメンバー サーバー **SR-SRV03** と **SR-SRV04**。  

-   2 つの異なるデータ センターを表す 2 つの論理 "サイト" である **Redmond** と **Bellevue**。  

![例の環境を示す図。Redmond サイトのクラスターで Bellevue サイトのクラスターがレプリケートされます](./media/Cluster-to-Cluster-Storage-Replication/SR_ClustertoCluster.png)  

**図 1:クラスター間のレプリケーション**  

## <a name="prerequisites"></a>前提条件  

* Active Directory Domain Services フォレスト (Windows Server 2016 を実行する必要はありません)。  
* Windows Server 2016 Datacenter Edition がインストールされている少なくとも 4 台のサーバー (2 つのクラスターにそれぞれ 2 台のサーバー)。 最大 2 つの 64 ノード クラスターをサポート。  
* SAS JBOD、ファイバー チャネル SAN、共有 VHDX、記憶域スペース ダイレクト、または iSCSI ターゲットを使う 2 セットのストレージ。 記憶域では HDD メディアと SSD メディアを混在させる必要があります。 各記憶域は、クラスター間に共有アクセスなしで、各クラスターでのみ利用可能となるように設定します。  
* 各記憶域セットでは、2 つ以上の仮想ディスク (レプリケートされたデータ用とログ用) を作成できる必要があります。 物理記憶域のセクター サイズは、すべてのデータ ディスクで同じである必要があります。 物理記憶域のセクター サイズは、すべてのログ ディスクで同じである必要があります。  
* 同期レプリケーションのために各サーバーで少なくとも 1 つのイーサネット/TCP 接続 (可能であれば RDMA)。   
* すべてのノード間での ICMP、SMB (ポート 445 と、SMB ダイレクト用のポート 5445)、WS-MAN (ポート 5985) の双方向トラフィックを許可する適切なファイアウォール規則およびルーター規則。  
* 書き込みの IO 負荷に十分対応できる帯域幅を持ちラウンド トリップ遅延時間が平均 5 ミリ秒である、同期レプリケーション用のサーバー間ネットワーク。 非同期レプリケーションには、遅延時間に関する推奨事項はありません。  
* レプリケート対象の記憶域を、Windows オペレーティング システムのフォルダーが含まれるドライブに配置することはできません。
* 重要な考慮事項と記憶域スペース ダイレクトのレプリケーションの制限事項がある - 以下の詳細な情報を確認してください。

これらの要件の多くは、`Test-SRTopology` コマンドレットを使用して判別できます。 記憶域レプリカまたは記憶域レプリカ管理ツール機能を 1 つ以上のサーバーにインストールすると、このツールにアクセスできるようになります。 このツールを使用するために、記憶域レプリカを構成する必要はありません。記憶域レプリカは、コマンドレットをインストールするためだけに構成します。 詳細は、以下の手順に記載されています。  

## <a name="step-1-provision-operating-system-features-roles-storage-and-network"></a>手順 1:オペレーティング システム、機能、役割、記憶域、およびネットワークのプロビジョニング

1.  Windows Server 2016 Datacenter **(デスクトップ エクスペリエンス)** のインストールの種類で、4 台のサーバー ノードすべてに Windows Server 2016 をインストールします。 Standard Edition が利用可能でも、これには記憶域レプリカが含まれていないため選択しないでください。  

2.  ネットワークの情報を追加し、ドメインに参加させてから再起動します。  

    > [!IMPORTANT]  
    > この時点以降、すべてのサーバーのビルトイン Administrator グループのメンバーであるドメイン ユーザーとして常にログオンします。 今後、グラフィカルなサーバーのインストールまたは Windows 10 コンピューターで実行するとき、Windows PowerShell および CMD プロンプトを昇格してください。  

3.  JBOD ストレージ格納装置、iSCSI ターゲット、FC SAN、またはローカルの固定ディスク (DAS) 記憶域の最初のセットをサイト **Redmond** 内のサーバーに接続します。  

4.  記憶域の 2 番目のセットをサイト **Bellevue** 内のサーバーに接続します。  

5.  必要に応じて、4 つのすべてのノードに、ベンダー ストレージとエンクロージャの最新のファームウェアとドライバー、最新のベンダー HBA ドライバー、最新のベンダー BIOS および UEFI ファームウェア、最新のベンダー ネットワーク ドライバー、およびマザーボード チップセットの最新のドライバーをインストールします。 必要に応じてノードを再起動します。  

    > [!NOTE]  
    > 共有記憶域およびネットワーク ハードウェアの構成については、ハードウェア ベンダーのドキュメントを参照してください。  

6.  サーバーの BIOS および UEFI の設定が、C 状態の無効化、QPI 速度の設定、NUMA の有効化、最大メモリ動作周波数の設定など、高パフォーマンスを有効にする設定であることを確認します。 Windows Server での電源管理が高パフォーマンスに設定されていることを確認します。 必要に応じて再起動します。  

7.  役割を次のように構成します。  

    -   **グラフィカルな方法**  

        1.  **ServerManager.exe** を実行し、すべてのサーバー ノードを追加してサーバー グループを作成します。  

        2.  各ノードに**ファイル サーバー**と**記憶域レプリカ**の役割と機能をインストールし、再起動します。  

    -   **Windows PowerShell による方法**  

        SR-SRV04 またはリモート管理コンピューター上で、Windows PowerShell コンソール内で次のコマンドを実行して、4 つのノード上でストレッチ クラスター用に必要な機能と役割をインストールし、ノードを再起動します。  

        ```PowerShell
        $Servers = 'SR-SRV01','SR-SRV02','SR-SRV03','SR-SRV04'  

        $Servers | ForEach { Install-WindowsFeature -ComputerName $_ -Name Storage-Replica,Failover-Clustering,FS-FileServer -IncludeManagementTools -restart }  
        ```  

        詳細については、「[役割、役割サービス、または機能のインストールまたはアンインストール](https://technet.microsoft.com/library/hh831809.aspx)」を参照してください。  

9. 記憶域を次のように構成します。  

    > [!IMPORTANT]  
    > -   各格納装置で、データ用に 1 つとログ用に 1 つの 2 つのボリュームを作成する必要があります。  
    > -   ログとデータのディスクは **MBR** ではなく **GPT** として初期化する必要があります。  
    > -   2 つのデータ ボリュームは、同じサイズでなければなりません。  
    > -   2 つのログ ボリュームのサイズは同じでなければなりません。  
    > -   すべてのレプリケートされたデータ ディスクには、同一のセクター サイズが必要です。  
    > -   すべてのログ ディスクのセクター サイズは、同じである必要があります。  
    > -   ログ ボリュームには、SSD など、フラッシュ ベースのストレージを使用する必要があります。  ログ ストレージには、データ ストレージよりも大きな速度を確保することをお勧めします。 ログ ボリュームは、絶対に他のワークロードに使用しないでください。
    > -   データ ディスクには、HDD、SSD、または階層型の組み合わせを使用でき、ミラーまたはパリティ スペースか、RAID 1 または 10 もしくは RAID 5 または RAID 50 のいずれかを使用できます。  
    > -   ログ ボリュームは、既定では、少なくとも 8 GB である必要があり、ログ要件に応じて増減する可能性があります。
    > -   値が高い表示、NVME または SSD のキャッシュを使用して記憶域スペース ダイレクト (S2D) を使用して、ときに予想される S2D クラスター間で記憶域レプリカ レプリケーションを構成するときに、待機時間よりも。 待機時間の変更が、それに比例してより大幅に高く、パフォーマンス + 容量の構成となしの HDD 層も容量レベルで NVME と SSD を使用する場合を参照してください。

この問題は、低速のメディアと比較した場合、NVME の非常に短い待機時間と組み合わせて記憶域レプリカのログ メカニズム内でのアーキテクチャの制限のために発生します。 S2D キャッシュを使用する場合と、パフォーマンスや容量のレベルではなく、キャッシュ内にすべて最近読み取り/書き込み、アプリケーションの IO と共に、すべての IO の SR ログが発生します。 つまり、同じ速度メディアでは、記憶域レプリカのすべてのアクティビティ - この構成は推奨されませんをサポートしていません (を参照してください https://aka.ms/srfaqのログの推奨事項)。 

を Hdd で S2D を使用する場合は、無効にするか、キャッシュを回避することはできません。 回避策として、SSD、NVME だけを使用する場合、パフォーマンスと容量レベルだけを構成できます。 その構成を使用して、容量レベルのみで処理すること、データ ボリュームでのみ、パフォーマンス レベルの記憶域レプリカのログを配置することを上記で説明した待ち時間の問題を回避できます。 同じは、さまざまな高速および低速の Ssd および NVME なしで実行できました。

この回避策はありません理想的なもちろんと一部の顧客が作成できないに使用します。 最適化と発生する人工的なボトルネックを軽減する今後の更新のログ メカニズム SR チームの作業です。 これは、ETA はありませんが、テスト用の顧客をタップします。 有効な場合、この FAQ が更新されます。 

    -   **JBOD 格納装置の。**  

        1.  各クラスターがそのサイトの記憶域エンクロージャのみを参照できることと、SAS 接続が正しく構成されていることを確認します。  

        2.  記憶域スペースを使用して記憶域をプロビジョニングします。これには、「[スタンドアロン サーバーに記憶域スペースを展開する](https://technet.microsoft.com/library/jj822938.aspx)」の**手順 1 - 3** に従い、Windows PowerShell またはサーバー マネージャーを使用します。  

    -   **Iscsi ターゲット記憶域。**  

        1.  各クラスターがそのサイトのストレージ格納装置のみを参照できることを確認します。 iSCSI を使用する場合は、複数の単一ネットワーク アダプターを使用する必要があります。  

        2.  ベンダーのドキュメントを参照して記憶域をプロビジョニングします。 Windows ベースの iSCSI ターゲットを使用する場合は、「[iSCSI ターゲット ブロック記憶域: 操作方法](https://technet.microsoft.com/library/hh848268.aspx)」を参照してください。  

    -   **FC SAN ストレージ。**  

        1.  各クラスターがそのサイトのストレージ格納装置のみを参照できることと、ホストのゾーンが正しく設定されていることを確認します。  

        2.  ベンダーのドキュメントを参照して記憶域をプロビジョニングします。  

    -   **記憶域スペース ダイレクトします。**  

        1.  記憶域スペース ダイレクトを展開することで、各クラスターがそのサイトのストレージ格納装置のみを参照できることを確認します。 (https://docs.microsoft.com/windows-server/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct) 

        2.  SR ログ ボリュームが常に最も高速なフラッシュ ストレージに配置され、データ ボリュームが低速な大容量ストレージに配置されることを確認します。

10. Windows PowerShell を起動し、`Test-SRTopology` コマンドレットを使用して、記憶域レプリカのすべての要件を満たしているかどうかを判別します。 このコマンドレットは、簡単なテストのために要件のみモードで使用することも、実行時間の長いパフォーマンス評価モードで使用することもできます。  
以下に例を示します。  

   ```PowerShell
   MD c:\temp

   Test-SRTopology -SourceComputerName SR-SRV01 -SourceVolumeName f: -SourceLogVolumeName g: -DestinationComputerName SR-SRV03 -DestinationVolumeName f: -DestinationLogVolumeName g: -DurationInMinutes 30 -ResultPath c:\temp        
   ```

      > [!IMPORTANT]
      > 評価期間中に指定されたソース ボリューム上で書き込み IO 負荷のないテスト サーバーを使用している場合は、ワークロードの追加を検討してください。そうしないと、有用なレポートは生成されません。 実際の数値および推奨されるログのサイズを確認するには、実稼働環境と同様のワークロードでテストする必要があります。 または、単に、テスト中にソース ボリュームにいくつかのファイルをコピーするか、[DISKSPD](https://gallery.technet.microsoft.com/DiskSpd-a-robust-storage-6cd2f223) をダウンロードして実行することで書き込み IO を生成します。 たとえば、D: ボリュームに対する 5 分間の低書き込み IO ワークロードによる一例を次に示します。  
      > `Diskspd.exe -c1g -d300 -W5 -C5 -b8k -t2 -o2 -r -w5 -h d:\test.dat`  

11. **TestSrTopologyReport.html** レポートを調べて、記憶域レプリカの要件を満たしていることを確認します。  

    ![レプリケーション トポロジのレポートの結果を示す画面](./media/Cluster-to-Cluster-Storage-Replication/SRTestSRTopologyReport.png)      

## <a name="step-2-configure-two-scale-out-file-server-failover-clusters"></a>手順 2:2 つのスケールアウト ファイル サーバー フェールオーバー クラスターを構成する  
ここで、2 つの通常のフェールオーバー クラスターを作成します。 構成、検証、テストを完了した後で、記憶域レプリカを使用してレプリケートします。 次のすべての手順は、クラスター ノード上で直接実行することも、Windows Server 2016 RSAT 管理ツールをインストール済みのリモート管理コンピューターから実行することもできます。  

### <a name="graphical-method"></a>グラフィカルな方法  

1.  各サイト内でノードに対して **cluadmin.msc** を実行します。  

2.  提案されたクラスターを検証し、結果を分析して、続行できることを確認します。 以下で使用している例では **SR-SRVCLUSA** と **SR-SRVCLUSB** です。  

3.  2 つのクラスターを作成します。 クラスター名が 15 文字以下であることを確認します。  

4.  ファイル共有監視またはクラウド監視を構成します。  

    > [!NOTE]  
    > Windows Server 2016 では、クラウド (Azure) ベースの監視オプションも追加されました。 ファイル共有監視に代えてこのクォーラム オプションを選択できます。  

    > [!WARNING]  
    > クォーラム構成の詳細については、「[Windows Server 2012 フェールオーバー クラスターでクォーラムを構成および管理する](https://technet.microsoft.com/library/jj612870.aspx)」の「**監視の構成**」セクションを参照してください。 `Set-ClusterQuorum` コマンドレットの詳細については、「[Set-ClusterQuorum](https://technet.microsoft.com/library/hh847275.aspx)」を参照してください。  

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

3.  ドメイン コントローラーまたはその他のなんらかの独立したサーバーでホストされている共有を指す各クラスター内でファイル共有監視またはクラウド (Azure) 監視を構成します。 次に、例を示します。  

    ```PowerShell  
    Set-ClusterQuorum -FileShareWitness \\someserver\someshare  
    ```  

    > [!NOTE]  
    > Windows Server 2016 では、クラウド (Azure) ベースの監視オプションも追加されました。 ファイル共有監視に代えてこのクォーラム オプションを選択できます。  

    > [!WARNING]  
    > クォーラム構成の詳細については、「[Windows Server 2012 フェールオーバー クラスターでクォーラムを構成および管理する](https://technet.microsoft.com/library/jj612870.aspx)」の「**監視の構成**」セクションを参照してください。 `Set-ClusterQuorum` コマンドレットの詳細については、「[Set-ClusterQuorum](https://technet.microsoft.com/library/hh847275.aspx)」を参照してください。  

4.  [スケールアウト ファイル サーバーの構成](https://technet.microsoft.com/library/hh831718.aspx)の手順に従って、両方のクラスターにクラスター化されたスケールアウト ファイル サーバーを作成します。  

## <a name="step-3-set-up-cluster-to-cluster-replication-using-windows-powershell"></a>手順 3:Windows PowerShell を使用してクラスター間レプリケーションを設定します。  
次に、Windows PowerShell を使用してクラスター間のレプリケーションを設定します。 次のすべての手順は、ノード上で直接実行することも、Windows Server 2016 RSAT 管理ツールをインストール済みのリモート管理コンピューターから実行することもできます。  

1.  実行して、他のクラスターへの最初のクラスター フル アクセスを許可、 **Grant SRAccess**最初のクラスター内のノードでコマンドレットまたはリモートでします。  

    ```PowerShell
    Grant-SRAccess -ComputerName SR-SRV01 -Cluster SR-SRVCLUSB  
    ```  

2.  実行して、他のクラスターへの 2 番目のクラスター フル アクセスを許可、 **Grant SRAccess** 2 番目のクラスター内のノードでコマンドレットまたはリモートでします。  

    ```PowerShell
    Grant-SRAccess -ComputerName SR-SRV03 -Cluster SR-SRVCLUSA  
    ```  

3.  ソースと宛先のディスク、ソースと宛先のログ、ソースと宛先のクラスター名、およびログのサイズを指定して、クラスター間のレプリケーションを構成します。 このコマンドは、サーバー上でローカルで実行するか、リモート管理コンピューターを使用して実行できます。  

    ```powershell  
    New-SRPartnership -SourceComputerName SR-SRVCLUSA -SourceRGName rg01 -SourceVolumeName c:\ClusterStorage\Volume2 -SourceLogVolumeName f: -DestinationComputerName SR-SRVCLUSB -DestinationRGName rg02 -DestinationVolumeName c:\ClusterStorage\Volume2 -DestinationLogVolumeName f:  
    ```  

    > [!WARNING]  
    > 既定のログのサイズは、8 GB です。 **Test-SRTopology** コマンドレットの結果に応じて、より大きい値または小さい値を指定して **-LogSizeInBytes** を使用することを検討してください。  

4.  レプリケーション元とレプリケーション先の状態を取得するために、次のように **Get-SRGroup** と **Get-SRPartnership** を使用します。  

    ```powershell
    Get-SRGroup  
    Get-SRPartnership  
    (Get-SRGroup).replicas  
    ```  

5.  次のようにレプリケーションの進行状況を確認します。  

    1.  レプリケーション元サーバーで、次のコマンドを入力し、イベント 5015、5002、5004、1237、5001、2200 を調べます。
        
        ```PowerShell
        Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica -max 20
        ```
    2.  レプリケーション先サーバーで、次のコマンドを実行して、パートナーシップの作成を示す記憶域レプリカ イベントを参照します。 このイベントでは、コピーされたバイト数およびかかった時間が示されます。 以下に例を示します。  
        
        ```powershell
        Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica | Where-Object {$_.ID -eq "1215"} | Format-List
        ```
        この場合の出力例を以下に示します。
        
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
    3. または、レプリカのレプリケーション先サーバー グループでは、コピーの残りのバイト数が常時示されており、PowerShell を使って照会できます。 次に、例を示します。

       ```PowerShell
       (Get-SRGroup).Replicas | Select-Object numofbytesremaining
       ```

       進行状況を確認するサンプルを次に示します (サンプルは終了されません)。  

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

## <a name="step-4-manage-replication"></a>手順 4:レプリケーションを管理する

次に、クラスター間レプリケーションの管理と操作を行います。 次のすべての手順は、クラスター ノード上で直接実行することも、Windows Server 2016 RSAT 管理ツールをインストール済みのリモート管理コンピューターから実行することもできます。  

1.  **Get-ClusterGroup** または**フェールオーバー クラスター マネージャー**を使用して、レプリケーションの現在のソースと宛先およびそれらの状態を判別します。  

2.  レプリケーションのパフォーマンスを測定するには、ソースと宛先の両方のノードで **Get-Counter** コマンドレットを使用します。 カウンター名は次のとおりです。  

    -   \Storage Replica Partition I/O Statistics(*)\Number of times flush paused  

    -   \Storage Replica Partition I/O Statistics(*)\Number of pending flush I/O  

    -   \Storage Replica Partition I/O Statistics(*)\Number of requests for last log write  

    -   \Storage Replica Partition I/O Statistics(*)\Avg.Flush Queue Length  

    -   \Storage Replica Partition I/O Statistics(*)\Current Flush Queue Length  

    -   \Storage Replica Partition I/O Statistics(*)\Number of Application Write Requests  

    -   \Storage Replica Partition I/O Statistics(*)\Avg.Number of requests per log write  

    -   \Storage Replica Partition I/O Statistics(*)\Avg.App Write Latency  

    -   \Storage Replica Partition I/O Statistics(*)\Avg.App Read Latency  

    -   \Storage Replica Statistics(*)\Target RPO  

    -   \Storage Replica Statistics(*)\Current RPO  

    -   \Storage Replica Statistics(*)\Avg.Log Queue Length  

    -   \Storage Replica Statistics(*)\Current Log Queue Length  

    -   \Storage Replica Statistics(*)\Total Bytes Received  

    -   \Storage Replica Statistics(*)\Total Bytes Sent  

    -   \Storage Replica Statistics(*)\Avg.Network Send Latency  

    -   \Storage Replica Statistics(*)\Replication State  

    -   \Storage Replica Statistics(*)\Avg.Message Round Trip Latency  

    -   \Storage Replica Statistics(*)\Last Recovery Elapsed Time  

    -   \Storage Replica Statistics(*)\Number of Flushed Recovery Transactions  

    -   \Storage Replica Statistics(*)\Number of Recovery Transactions  

    -   \Storage Replica Statistics(*)\Number of Flushed Replication Transactions  

    -   \Storage Replica Statistics(*)\Number of Replication Transactions  

    -   \Storage Replica Statistics(*)\Max Log Sequence Number  

    -   \Storage Replica Statistics(*)\Number of Messages Received  

    -   \Storage Replica Statistics(*)\Number of Messages Sent  

    Windows PowerShell でのパフォーマンス カウンターの詳細については、「[Get-Counter](https://technet.microsoft.com/library/hh849685.aspx)」を参照してください。  

3.  1 つのサイトからレプリケーションの方向を移動するには、**Set-SRPartnership** コマンドレットを使用します。  

    ```PowerShell
    Set-SRPartnership -NewSourceComputerName SR-SRVCLUSB -SourceRGName rg02 -DestinationComputerName SR-SRVCLUSA -DestinationRGName rg01  
    ```  

    > [!NOTE]  
    > Windows Server 2016 では、初期同期の進行中に役割の切り替えを行うことができません。このため、初期レプリケーションが完了する前に役割を切り替えようとするとデータの損失につながります。 最初の同期が完了するまでは、強制的に方向を切り替えないでください。

    イベント ログを調べてレプリケーションの方向の変更と回復モードが発生しているかどうかを確認し、調整してください。 調整後、書き込み IO で、新しいレプリケーション元サーバーの所有する記憶域に書き込むことができます。 レプリケーションの方向を変更すると、前のソース コンピューター上で書き込み IO がブロックされます。  

    > [!NOTE]  
    > 宛先クラスター ディスクは、レプリケート中は常に **[Online (No Access) (オンライン (アクセスなし))]** と表示されます。  

4.  Windows Server 2016 でログのサイズを既定の 8 GB から変更するには、ソースとレプリケーション先の両方の記憶域レプリカ グループで **Set-SRGroup** を使用します。  

    > [!IMPORTANT]  
    > 既定のログのサイズは、8 GB です。 **Test-SRTopology** コマンドレットの結果に応じて、より大きい値または小さい値を指定して -LogSizeInBytes を使用することを検討してください。  

5.  レプリケーションを削除するには、各クラスターで **Get-SRGroup**、**Get-SRPartnership**、**Remove-SRGroup**、および **Remove-SRPartnership** を使用します。  

    ```powershell
    Get-SRPartnership | Remove-SRPartnership  
    Get-SRGroup | Remove-SRGroup  
    ```  

    > [!NOTE]  
    > 記憶域レプリカは、宛先ボリュームをマウント解除します。 これは仕様です。

## <a name="see-also"></a>関連項目

-   [記憶域レプリカの概要](storage-replica-overview.md) 
-   [共有記憶域を使用してストレッチ クラスター レプリケーション](stretch-cluster-replication-using-shared-storage.md)  
-   [サーバー対サーバーの記憶域レプリケーション](server-to-server-storage-replication.md)  
-   [記憶域レプリカ:既知の問題](storage-replica-known-issues.md)  
-   [記憶域レプリカ:よく寄せられる質問](storage-replica-frequently-asked-questions.md)  
-   [Windows Server 2016 での記憶域スペース ダイレクト](../storage-spaces/storage-spaces-direct-overview.md)  
