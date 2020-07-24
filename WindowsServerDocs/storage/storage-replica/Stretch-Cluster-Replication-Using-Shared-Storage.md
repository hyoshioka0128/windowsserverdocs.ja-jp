---
title: 共有記憶域を使用したストレッチ クラスター レプリケーション
ms.prod: windows-server
manager: eldenc
ms.author: nedpyle
ms.technology: storage-replica
ms.topic: get-started-article
author: nedpyle
ms.date: 04/26/2019
ms.assetid: 6c5b9431-ede3-4438-8cf5-a0091a8633b0
ms.openlocfilehash: 08b09c9a0684a2938645462875737556d0288c9e
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86961044"
---
# <a name="stretch-cluster-replication-using-shared-storage"></a>共有記憶域を使用したストレッチ クラスター レプリケーション

>適用先:Windows Server 2019、Windows Server 2016、Windows Server (半期チャネル)

この評価の例では、単一のストレッチ クラスター内にこれらのコンピューターとその記憶域を構成します。ここでは、2 つのノードがストレージの 1 つのセットを共有し、2 つのノードが別のストレージのセットを共有し、レプリケーションはクラスター内のミラー化された両方のストレージのセットを維持して、直ちにフェールオーバーできるようにします。 これらのノードとその記憶域は、個別の物理サイトにある必要がありますが、ただし必須ではありません。 サンプルのシナリオに示すように、Hyper-V とファイル サーバー クラスターで別々の作成手順があります。  

> [!IMPORTANT]  
> この評価では、異なるサイト内のサーバーが、ネットワークを介して他のサーバーと通信できる必要がありますが、他のサイトの共有ストレージには物理的に接続されていません。 このシナリオでは、記憶域スペース ダイレクトは使用しません。  

## <a name="terms"></a>用語  
このチュートリアルでは、例として次の環境を使用します。  

-   **SR-SRVCLUS** という 1 つのクラスターを構成する **SR-SRV01**、**SR-SRV02**、**SR-SRV03**、および **SR-SRV04** という名前の 4 つのサーバー。  

-   2 つの異なるデータ センターを表す 2 つの論理 "サイト”、**Redmond** と **Bellevue**。  

> [!NOTE]  
> 使用できるノード数の下限は 2 個 (各サイトに 1 つのノード) です。 ただし、2 つだけのサーバーを使用してサイト間のフェールオーバーを実行することはできません。 ノードは最大で 64 個まで使用することができます。

![Redmond の 2 つのノードと Bellevue サイトにある同一クラスターの 2 つのノードでのレプリケーションを示す図](./media/Stretch-Cluster-Replication-Using-Shared-Storage/Storage_SR_StretchClusterExample.png)  

**図 1: ストレッチ クラスターでの記憶域レプリケーション**  

## <a name="prerequisites"></a>前提条件  
-   Active Directory Domain Services フォレスト (Windows Server 2016 を実行する必要はありません)。  
-   2-64 Windows Server 2019 または Windows Server 2016、Datacenter Edition を実行しているサーバー。 Windows Server 2019 を実行している場合は、通常は Standard Edition を使用することができます。これにより、1つのボリュームのみを最大 2 TB までレプリケートできます。 
-   SAS JBOD (記憶域スペースなどを搭載)、ファイバー チャネル SAN、共有 VHDX、または iSCSI ターゲットを使用する 2 セットの共有記憶域。 記憶域は、HDD と SSD メディアの混在を含み、永続的な予約をサポートしている必要があります。 各記憶域セットを 2 つのサーバーのみが使用できるようにすることができます (非対称)。  
-   記憶域の各セットでは、2 つ以上 (1 つはレプリケートされたデータ用、1 つはログ用) の仮想ディスクの作成が許可される必要があります。 物理記憶域のセクター サイズは、すべてのデータ ディスクで同じである必要があります。 物理記憶域のセクター サイズは、すべてのログ ディスクで同じである必要があります。  
-   同期レプリケーションには、各サーバーで少なくとも 1 つの 1 GbE 接続 (可能であれば RDMA) が必要です。   
-   サーバーごとに 2 GB 以上の RAM と 2 つのコア。 仮想マシンを増やす場合は、追加のメモリとコアが必要です。  
-   すべてのノード間で ICMP、SMB (ポート 445、SMB ダイレクト用に 5445)、WS-MAN (ポート 5985) の双方向トラフィックを許可する適切なファイアウォールおよびルーター ルール。  
-   書き込みの IO 負荷に十分対応できる帯域幅を持ちラウンド トリップ遅延時間が平均 5 ミリ秒である、同期レプリケーション用のサーバー間ネットワーク。 非同期レプリケーションには、遅延時間に関する推奨事項はありません。  
-   レプリケート対象の記憶域を、Windows オペレーティング システムのフォルダーが含まれるドライブに配置することはできません。

これらの要件の多くは、`Test-SRTopology` コマンドレットを使用して判別できます。 記憶域レプリカまたは記憶域レプリカ管理ツール機能を 1 つ以上のサーバーにインストールすると、このツールにアクセスできるようになります。 このツールを使用するために、記憶域レプリカを構成する必要はありません。記憶域レプリカは、コマンドレットをインストールするためだけに構成します。 詳細は、以下の手順に記載されています。  

## <a name="provision-operating-system-features-roles-storage-and-network"></a>オペレーティング システム、機能、役割、記憶域、およびネットワークのプロビジョニング  

1.  Server Core またはデスクトップエクスペリエンス搭載サーバーのインストールオプションを使用して、すべてのサーバーノードに Windows Server をインストールします。  
    > [!IMPORTANT]
    > この時点以降は、常に、すべてのサーバーでビルトイン Administrator グループのメンバーであるドメイン ユーザーとしてログオンします。 今後、グラフィカルなサーバーのインストールまたは Windows 10 コンピューターで実行するとき、PowerShell および CMD プロンプトを昇格してください。

2.  ネットワークの情報を追加し、ノードをドメインに参加させてから再起動します。  
    > [!NOTE]
    > このガイドでは、この時点で、ストレッチ クラスター内に使用する 2 つのサーバーのペアがあることを前提としています。 WAN や LAN ネットワークは、サーバーを分離し、サーバーは、どちらかの物理的または論理的なサイトに属しています。 このガイドでは、**SR-SRV01** と **SR-SRV02** がサイト Redmond にあり、**SR-SRV03** と **SR-SRV04** がサイト **Bellevue** にあると見なしています。  

3.  最初の共有 JBOD 記憶域エンクロージャー、共有 VHDX、iSCSI ターゲット、または FC SAN をサイト **Redmond** 内のサーバーに接続します。  

4.  2 つ目の記憶域のセットをサイト **Bellevue** 内のサーバーに接続します。  

5.  必要に応じて、4 つのすべてのノードに、ベンダー ストレージとエンクロージャの最新のファームウェアとドライバー、最新のベンダー HBA ドライバー、最新のベンダー BIOS および UEFI ファームウェア、最新のベンダー ネットワーク ドライバー、およびマザーボード チップセットの最新のドライバーをインストールします。 必要に応じてノードを再起動します。  

    > [!NOTE]
    > 共有記憶域およびネットワーク ハードウェアの構成については、ハードウェア ベンダーのドキュメントを参照してください。  

6.  サーバーの BIOS および UEFI の設定が、C 状態の無効化、QPI 速度の設定、NUMA の有効化、最大メモリ動作周波数の設定など、高パフォーマンスを有効にする設定であることを確認します。 Windows Server での電源管理が高パフォーマンスに設定されていることを確認します。 必要に応じて再起動します。  

7.  役割を次のように構成します。  

    -   **グラフィカルな方法**  

        **ServerManager.exe** を実行し、**[管理]**、**[サーバーの追加]** をクリックしてすべてのサーバー ノードを追加します。  

        > [!IMPORTANT]
        > **フェールオーバー クラスタリング**と**記憶域レプリカ**の役割と機能を各ノードでインストールし、再起動します。 Hyper-V、ファイル サーバーなどの役割を使用する予定の場合は、この時点でそれらもインストールできます。  

    -   **Windows PowerShell を使用する方法**  

        **SR-SRV04** またはリモート管理コンピューター上で、Windows PowerShell コンソール内で次のコマンドを実行して、4 つのノード上でストレッチ クラスター用に必要な機能と役割をインストールし、ノードを再起動します。  

        ```PowerShell  
        $Servers = 'SR-SRV01','SR-SRV02','SR-SRV03','SR-SRV04'  

        $Servers | foreach { Install-WindowsFeature -ComputerName $_ -Name Storage-Replica,Failover-Clustering,FS-FileServer -IncludeManagementTools -restart }  

        ```  

        詳細については、「[役割、役割サービス、または機能のインストールまたはアンインストール](../../administration/server-manager/install-or-uninstall-roles-role-services-or-features.md)」を参照してください。  


8. 記憶域を次のように構成します。  

    > [!IMPORTANT]  
    > -   各格納装置で、データ用に 1 つとログ用に 1 つの 2 つのボリュームを作成する必要があります。  
    > -   ログ ディスクとデータ ディスクは、MBR ではなく GPT として初期化する必要があります。  
    > -   2 つのデータ ボリュームのサイズは同じでなければなりません。  
    > -   2 つのログ ボリュームのサイズは同じでなければなりません。  
    > -   すべてのレプリケートされたデータ ディスクには、同一のセクター サイズが必要です。  
    > -   すべてのログ ディスクには、同一のセクター サイズが必要です。  
    > -   ログ ボリュームでは、フラッシュ ベースのストレージと、高いパフォーマンスの回復性の設定を使用する必要があります。 ログ ストレージには、データ ストレージよりも大きい速度を確保することをお勧めします。 ログ ボリュームは、絶対に他のワークロードに使用しないでください。 
    > -   データ ディスクには、HDD、SSD、または階層型の組み合わせを使用でき、ミラーまたはパリティ スペースか、RAID 1 または 10 もしくは RAID 5 または RAID 50 のいずれかを使用できます。  
    > -  既定ではログ ボリュームは 9 GB 以上である必要がありますが、ログ要件に応じて増減します。  
    > - NTFS または ReFS でフォーマットする必要があります。
    > - ファイル サーバーの役割は、テスト用に必須ファイアウォール ポートを開くため、Test-SRTopology の動作にのみ必要です。  

    -   **JBOD 格納装置の場合:**  

        1.  ペアリングされた各サーバー ノードのセットがそのサイトのストレージ格納装置 (つまり非対称記憶域) のみを参照できることと、SAS 接続が正しく構成されていることを確認します。  

        2.  記憶域スペースを使用して記憶域をプロビジョニングします。これには、「[スタンドアロン サーバーに記憶域スペースを展開する](../storage-spaces/deploy-standalone-storage-spaces.md)」の**手順 1 - 3** に従い、Windows PowerShell またはサーバー マネージャーを使用します。  

    -   **iSCSI ストレージの場合:**  

        1.  ペアリングされた各サーバー ノードのセットがそのサイトのストレージ格納装置 (つまり非対称記憶域) のみを参照できることを確認します。 iSCSI を使用する場合は、複数の単一ネットワーク アダプターを使用する必要があります。  

        2.  ベンダーのドキュメントを参照して記憶域をプロビジョニングします。 Windows ベースの iSCSI ターゲットを使用する場合は、「[iSCSI ターゲット ブロック記憶域: 操作方法](../iscsi/iscsi-target-server.md)」を参照してください。  

    -   **FC SAN ストレージの場合:**  

        1.  ペアリングされた各サーバー ノードのセットがそのサイトのストレージ格納装置 (つまり非対称記憶域) のみを参照できることと、ホストが適切にゾーニングされていることを確認します。  

        2.  ベンダーのドキュメントを参照して記憶域をプロビジョニングします。  

## <a name="configure-a-hyper-v-failover-cluster-or-a-file-server-for-a-general-use-cluster"></a>Hyper-V フェールオーバー クラスターまたは汎用クラスター用のファイル サーバーを構成する

サーバー ノードを設定したら、次の手順として、次のいずれかの種類のクラスターを作成します。  
*  [Hyper-V フェールオーバー クラスター](#BKMK_HyperV)  
*  [汎用クラスター用のファイル サーバー](#BKMK_FileServer)  

### <a name="configure-a-hyper-v-failover-cluster"></a><a name="BKMK_HyperV"></a>Hyper-v フェールオーバークラスターの構成  

>[!NOTE]
> Hyper-V クラスターではなくファイル サーバー クラスターを作成する場合は、このセクションをスキップして、「[汎用クラスター用のファイル サーバーを構成する](#BKMK_FileServer)」セクションに進んでください。  

次に、通常のフェールオーバー クラスターを作成します。 構成、検証、テストを完了した後で、記憶域レプリカを使用して拡大します。 次のすべての手順は、クラスターノードで直接実行することも、Windows Server リモートサーバー管理ツールを含むリモート管理コンピューターから実行することもできます。  

#### <a name="graphical-method"></a>グラフィカルな方法  

1. **Cluadmin.msc**を実行します。  

2. 提案されたクラスターを検証し、結果を分析して、続行できることを確認します。  

   > [!NOTE]  
   > 非対称ストレージ使用のために起こる、クラスター検証からのストレージ エラーを予測する必要があります。  

3. Hyper-V コンピューター クラスターを作成します。 クラスター名が 15 文字以下であることを確認します。 以下で使用する例は、SR-SRVCLUS です。 ノードが異なるサブネットに存在する場合は、各サブネットのクラスター名の IP アドレスを作成し、"OR" 依存関係を使用する必要があります。  詳細につい[ては、「マルチサブネットクラスターの IP アドレスと依存関係の構成–パート III](https://techcommunity.microsoft.com/t5/Failover-Clustering/Configuring-IP-Addresses-and-Dependencies-for-Multi-Subnet/ba-p/371698)」を参照してください。  

4. サイトの停止が発生した場合に、クォーラムを提供するために、ファイル共有監視またはクラウド監視を構成します。  

   > [!NOTE]  
   > WIndows Server には、クラウド (Azure) ベースの監視のオプションが追加されました。 ファイル共有監視に代えてこのクォーラム オプションを選択できます。  

   > [!WARNING]  
   > クォーラム構成の詳細については、[「Windows Server 2012 フェールオーバー クラスターでクォーラムを構成および管理する」の「監視の構成」](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj612870(v=ws.11))を参照してください。 `Set-ClusterQuorum` コマンドレットの詳細については、「[Set-ClusterQuorum](/powershell/module/failoverclusters/set-clusterquorum)」を参照してください。  

5. 「[Windows Server 2012 の HYPER-V クラスターのネットワークの推奨事項](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn550728(v=ws.11))」を確認し、クラスター ネットワークが最適に構成されていることを確認します。  

6. Redmond サイトでクラスター CSV に 1 台のディスクを追加します。 これを行うには、**[記憶域]** セクションの **[ディスク]** ノードでソース ディスクを右クリックして、**[クラスターの共有ボリュームへの追加]** をクリックします。  

7. 「[Hyper-V クラスターを展開する](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj863389(v=ws.11))」ガイドを使用し、**Redmond** サイトの手順 7 ～ 10 に従って、テスト仮想マシンを作成し、最初のテスト サイトでストレージを共有する 2 つのノード内で、クラスターが通常動作していることを確認します。  

8. 2 ノード ストレッチ クラスターを作成する場合は、作業を続行する前にすべての記憶域を追加する必要があります。 これを行うには、クラスター ノードで管理者アクセス許可を使用して PowerShell セッションを開き、コマンド `Get-ClusterAvailableDisk -All | Add-ClusterDisk` を実行します。

   この動作は、Windows Server 2016 の仕様です。

9. Windows PowerShell を起動し、`Test-SRTopology` コマンドレットを使用して、記憶域レプリカのすべての要件を満たしているかどうかを判別します。  

    たとえば、提案されたストレッチ クラスター ノードでそれぞれ **D:** と **E:** のボリュームを持つ 2 ノードを検証するためにテストを 30 分実行します。
   1. すべての利用可能な記憶域を **SR-SRV01** に移動します。
   2. フェールオーバー クラスター マネージャーの **[役割]** セクションで **[空の役割の作成]** をクリックします。
   3. オンライン記憶域をこの空の役割に追加し、「**新しい役割**」という名前を付けます。
   4. すべての利用可能な記憶域を **SR-SRV03** に移動します。
   5. フェールオーバー クラスター マネージャーの **[役割]** セクションで **[空の役割の作成]** をクリックします。
   6. 空の **[新しい役割 (2)]** を **SR-SRV03** に移動します。
   7. オンライン記憶域をこの空の役割に追加し、「**新しい役割 (2)**」という名前を付けます。
   8. これで、ドライブ文字を付けてすべての記憶域をマウントしたため、`Test-SRTopology` を使用してクラスターを評価できます。

       次に例を示します。

           MD c:\temp  

           Test-SRTopology -SourceComputerName SR-SRV01 -SourceVolumeName D: -SourceLogVolumeName E: -DestinationComputerName SR-SRV03 -DestinationVolumeName D: -DestinationLogVolumeName E: -DurationInMinutes 30 -ResultPath c:\temp        

      > [!IMPORTANT]
      > 評価期間中に指定したソース ボリュームに対する書き込み IO ワークロードのないテスト サーバーを使用している場合は、ワークロードの追加を検討してください。負荷がない場合、Test-SRTopology で有用なレポートは生成されません。 実際の数値および推奨されるログのサイズを確認するには、実稼働環境と同様のワークロードでテストする必要があります。 または、単に、テスト中にソース ボリュームにいくつかのファイルをコピーするか、DISKSPD をダウンロードして実行することでも書き込み I/O を生成できます。 たとえば、D: ボリュームに対する 10 分間の低書き込み IO ワークロードによる例を次に示します。   
       `Diskspd.exe -c1g -d600 -W5 -C5 -b4k -t2 -o2 -r -w5 -i100 d:\test.dat`  

10. **TestSrTopologyReport-< date >.html** レポートを調べて、記憶域レプリカの要件を満たしていることを確認し、初期同期時間の予想およびログの推奨事項をメモします。  

      ![レプリケーション レポートの表示画面](./media/Stretch-Cluster-Replication-Using-Shared-Storage/SRTestSRTopologyReport.png)

11. ディスクを使用可能な記憶域に戻し、一時的な空の役割を削除します。

12. 満足したら、テスト仮想マシンを削除します。 提案されたソース ノードにさらに評価に必要なすべての実際のテスト仮想マシンを追加します。  

13. ストレッチ クラスター サイトの認識を構成し、サーバー **SR SRV01** と **SR SRV02** がサイト **Redmond** に含まれ、**SR SRV03** と **SR SRV04** がサイト **Bellevue** に含まれ、**Redmond** がソース記憶域と仮想マシンのノードの所有権で優先されるようにします。  

    ```PowerShell
    New-ClusterFaultDomain -Name Seattle -Type Site -Description "Primary" -Location "Seattle Datacenter"  
   
    New-ClusterFaultDomain -Name Bellevue -Type Site -Description "Secondary" -Location "Bellevue Datacenter"  
   
    Set-ClusterFaultDomain -Name sr-srv01 -Parent Seattle  
    Set-ClusterFaultDomain -Name sr-srv02 -Parent Seattle  
    Set-ClusterFaultDomain -Name sr-srv03 -Parent Bellevue  
    Set-ClusterFaultDomain -Name sr-srv04 -Parent Bellevue  

    (Get-Cluster).PreferredSite="Seattle"
    ```

    > [!NOTE]
    > Windows Server 2016 には、フェールオーバー クラスター マネージャーを使用してサイトの認識を構成するオプションはありません。  

14. **(省略可能)** DNS サイトのフェールオーバーを高速化するために、クラスターのネットワークと Active Directory を構成します。 HYPER-V ソフトウェア定義ネットワークで拡大された VLAN、ネットワーク抽象化デバイス、短くした DNS の TTL、およびその他の一般的な手法を使用することができます。

    詳細については、Microsoft Ignite セッション「[Stretching Failover Clusters and Using Storage Replica in Windows Server vNext](https://channel9.msdn.com/Events/Ignite/2015/BRK3487)」(Windows Server vNext でのフェールオーバー クラスターの拡大と記憶域レプリカの使用) およびブログ記事「[Enable Change Notifications between Sites - How and Why?](/archive/blogs/qzaidi/enable-change-notifications-between-sites-how-and-why)」(サイト間での変更通知の有効化 - 方法とこれを行う理由) を参照してください。  

15. **(省略可能)** ゲストがノード障害中に長時間一時停止しないように VM の回復性を構成します。 代わりに、10 秒以内に新しいレプリケーション ソース記憶域にフェールオーバーします。  

    ```PowerShell  
    (Get-Cluster).ResiliencyDefaultPeriod=10  
    ```  

    > [!NOTE]
    >  Windows Server 2016 には、フェールオーバー クラスター マネージャーを使用して VM の回復性を構成するオプションはありません。  

#### <a name="windows-powershell-method"></a>Windows PowerShell による方法  

1. 提案されたクラスターをテストし、結果を分析して、続行できることを確認します。  

   ```PowerShell  
   Test-Cluster SR-SRV01, SR-SRV02, SR-SRV03, SR-SRV04  
   ```  

   > [!NOTE]
   >  非対称ストレージ使用のために起こる、クラスター検証からのストレージ エラーを予測する必要があります。  

2. 一般使用ストレージクラスター用のファイルサーバーを作成します (クラスターが使用する独自の静的 IP アドレスを指定する必要があります)。 クラスター名が 15 文字以下であることを確認します。  ノードが異なるサブネットに存在する場合は、"OR" 依存関係を使用して追加のサイトの IP アドレスを作成する必要があります。 詳細につい[ては、「マルチサブネットクラスターの IP アドレスと依存関係の構成–パート III](https://techcommunity.microsoft.com/t5/Failover-Clustering/Configuring-IP-Addresses-and-Dependencies-for-Multi-Subnet/ba-p/371698)」を参照してください。
   ```PowerShell  
   New-Cluster -Name SR-SRVCLUS -Node SR-SRV01, SR-SRV02, SR-SRV03, SR-SRV04 -StaticAddress <your IP here>  
   Add-ClusterResource -Name NewIPAddress -ResourceType “IP Address” -Group “Cluster Group”
   Set-ClusterResourceDependency -Resource “Cluster Name” -Dependency “[Cluster IP Address] or [NewIPAddress]”
   ```  

3. ドメイン コントローラーまたはその他のなんらかの独立したサーバーでホストされている共有を指す各クラスター内でファイル共有監視またはクラウド (Azure) 監視を構成します。 次に例を示します。  

   ```PowerShell  
   Set-ClusterQuorum -FileShareWitness \\someserver\someshare  
   ```  

   > [!NOTE]
   > WIndows Server には、クラウド (Azure) ベースの監視のオプションが追加されました。 ファイル共有監視に代えてこのクォーラム オプションを選択できます。  
    
   クォーラム構成の詳細については、[「Windows Server 2012 フェールオーバー クラスターでクォーラムを構成および管理する」の「監視の構成」](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj612870(v=ws.11))を参照してください。 `Set-ClusterQuorum` コマンドレットの詳細については、「[Set-ClusterQuorum](/powershell/module/failoverclusters/set-clusterquorum)」を参照してください。  

4. 「[Windows Server 2012 の HYPER-V クラスターのネットワークの推奨事項](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn550728(v=ws.11))」を確認し、クラスター ネットワークが最適に構成されていることを確認します。  

5. 2 ノード ストレッチ クラスターを作成する場合は、作業を続行する前にすべての記憶域を追加する必要があります。 これを行うには、クラスター ノードで管理者アクセス許可を使用して PowerShell セッションを開き、コマンド `Get-ClusterAvailableDisk -All | Add-ClusterDisk` を実行します。

   この動作は、Windows Server 2016 の仕様です。

6. 「[Hyper-V クラスターを展開する](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj863389(v=ws.11))」ガイドを使用し、**Redmond** サイトの手順 7 ～ 10 に従って、テスト仮想マシンを作成し、最初のテスト サイトでストレージを共有する 2 つのノード内で、クラスターが通常動作していることを確認します。  

7. 満足したら、テスト VM を削除します。 提案されたソース ノードにさらに評価に必要なすべての実際のテスト仮想マシンを追加します。  

8. ストレッチ クラスター サイトの認識を構成し、サーバー **SR SRV01** と **SR SRV02** がサイト **Redmond** に含まれ、**SR SRV03** と **SR SRV04** がサイト **Bellevue** に含まれ、**Redmond** がソース記憶域と仮想マシンのノードの所有権で優先されるようにします。  

   ```PowerShell  
   New-ClusterFaultDomain -Name Seattle -Type Site -Description "Primary" -Location "Seattle Datacenter"  

   New-ClusterFaultDomain -Name Bellevue -Type Site -Description "Secondary" -Location "Bellevue Datacenter"  

   Set-ClusterFaultDomain -Name sr-srv01 -Parent Seattle  
   Set-ClusterFaultDomain -Name sr-srv02 -Parent Seattle  
   Set-ClusterFaultDomain -Name sr-srv03 -Parent Bellevue  
   Set-ClusterFaultDomain -Name sr-srv04 -Parent Bellevue  

   (Get-Cluster).PreferredSite="Seattle"  
   ```  

9. **(省略可能)** DNS サイトのフェールオーバーを高速化するために、クラスターのネットワークと Active Directory を構成します。 HYPER-V ソフトウェア定義ネットワークで拡大された VLAN、ネットワーク抽象化デバイス、短くした DNS の TTL、およびその他の一般的な手法を使用することができます。  

   詳細については、「[Stretching Failover Clusters and Using Storage Replica in Windows Server vNext](https://channel9.msdn.com/Events/Ignite/2015/BRK3487)」(Windows Server vNext でのフェールオーバー クラスターの拡大と記憶域レプリカの使用) Microsoft Ignite セッションおよび「[Enable Change Notifications between Sites - How and Why?](/archive/blogs/qzaidi/enable-change-notifications-between-sites-how-and-why)」(サイト間での変更通知の有効化 - 方法とこれを行う理由) を参照してください。  

10. **(省略可能)** ゲストがノード障害中に長時間一時停止しないように VM の回復性を構成します。 代わりに、10 秒以内に新しいレプリケーション ソース記憶域にフェールオーバーします。  

    ```PowerShell  
    (Get-Cluster).ResiliencyDefaultPeriod=10  
    ```  

    > [!NOTE]  
    > Windows Server 2016 には、フェールオーバー クラスター マネージャーを使用した VM 回復のオプションはありません。  



### <a name="configure-a-file-server-for-general-use-cluster"></a><a name="BKMK_FileServer"></a>汎用クラスター用のファイルサーバーを構成する  

>[!NOTE]
> 「[HYPER-V フェールオーバー クラスターを構成する](#BKMK_HyperV)」の説明に従って既に HYPER-V フェールオーバー クラスターを構成している場合は、このセクションをスキップしてください。  

次に、通常のフェールオーバー クラスターを作成します。 構成、検証、テストを完了した後で、記憶域レプリカを使用して拡大します。 次のすべての手順は、クラスターノードで直接実行することも、Windows Server リモートサーバー管理ツールを含むリモート管理コンピューターから実行することもできます。  

#### <a name="graphical-method"></a>グラフィカルな方法  

1. cluadmin.msc を実行します。  

2. 提案されたクラスターを検証し、結果を分析して、続行できることを確認します。  
   >[!NOTE]
   >非対称ストレージ使用のために起こる、クラスター検証からのストレージ エラーを予測する必要があります。   
3. 汎用記憶域クラスター用のファイル サーバーを作成します。 クラスター名が 15 文字以下であることを確認します。 以下で使用する例は、SR-SRVCLUS です。  ノードが異なるサブネットに存在する場合は、各サブネットのクラスター名の IP アドレスを作成し、"OR" 依存関係を使用する必要があります。  詳細につい[ては、「マルチサブネットクラスターの IP アドレスと依存関係の構成–パート III](https://techcommunity.microsoft.com/t5/Failover-Clustering/Configuring-IP-Addresses-and-Dependencies-for-Multi-Subnet/ba-p/371698)」を参照してください。  

4. サイトの停止が発生した場合に、クォーラムを提供するために、ファイル共有監視またはクラウド監視を構成します。  
   >[!NOTE]
   > WIndows Server には、クラウド (Azure) ベースの監視のオプションが追加されました。 ファイル共有監視に代えてこのクォーラム オプションを選択できます。                                                                                                                                                                             
   >[!NOTE]
   >  クォーラム構成の詳細については、[「Windows Server 2012 フェールオーバー クラスターでクォーラムを構成および管理する」の「監視の構成」](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj612870(v=ws.11))を参照してください。 Set-ClusterQuorum コマンドレットの詳細については、「[Set-ClusterQuorum](/powershell/module/failoverclusters/set-clusterquorum)」を参照してください。 

5. 2 ノード ストレッチ クラスターを作成する場合は、作業を続行する前にすべての記憶域を追加する必要があります。 これを行うには、クラスター ノードで管理者アクセス許可を使用して PowerShell セッションを開き、コマンド `Get-ClusterAvailableDisk -All | Add-ClusterDisk` を実行します。

   この動作は、Windows Server 2016 の仕様です。

6. クラスター ネットワークが最適に構成されていることを確認します。  
    >[!NOTE]
    > 次の手順に進む前に、ファイル サーバーの役割をすべてのノードにインストールする必要があります。   |  

7. **[役割]** で、**[役割の構成]** をクリックします。 **[開始する前に]** を確認し、**[次へ]** をクリックします。  

8. **[ファイル サーバー]** を選択し、**[次へ]** をクリックします。  

9. **[汎用ファイル サーバー]** が選択されたままにし、**[次へ]** をクリックします。  

10. **クライアント アクセス ポイント**名 (15 文字以下) を指定し、**[次へ]** をクリックします。  

11. データ ボリュームにするディスクを選択して **[次へ]** をクリックします。  

12. 設定を確認して、**[次へ]** をクリックします。 **[完了]** をクリックします。  

13. 新しいファイル サーバーの役割を右クリックし、**[ファイル共有の追加]** をクリックします。 共有を構成するウィザードを実行します。  

14. 省略可能: このサイトの他のストレージを使用する別のファイル サーバーの役割を追加します。  

15. ストレッチ クラスター サイトの認識を構成し、サーバー SR SRV01 と SR SRV02 がサイト Redmond に含まれ、SR SRV03 と SR SRV04 がサイト Bellevue に含まれ、Redmond がソース記憶域と仮想マシンのノードの所有権で優先されるようにします。  

    ```PowerShell  
    New-ClusterFaultDomain -Name Seattle -Type Site -Description "Primary" -Location "Seattle Datacenter"  

    New-ClusterFaultDomain -Name Bellevue -Type Site -Description "Secondary" -Location "Bellevue Datacenter"  

    Set-ClusterFaultDomain -Name sr-srv01 -Parent Seattle  
    Set-ClusterFaultDomain -Name sr-srv02 -Parent Seattle  
    Set-ClusterFaultDomain -Name sr-srv03 -Parent Bellevue  
    Set-ClusterFaultDomain -Name sr-srv04 -Parent Bellevue  

    (Get-Cluster).PreferredSite="Seattle"  
    ```  

      >[!NOTE]
      > Windows Server 2016 には、フェールオーバー クラスター マネージャーを使用してサイトの認識を構成するオプションはありません。  

16. (省略可能) DNS サイトの高速フェール オーバーのためにクラスター ネットワークと Active Directory を構成します。 拡大された VLAN、ネットワーク抽象化デバイス、短くした DNS の TTL、およびその他の一般的な手法を使用することができます。  

詳細については、Microsoft Ignite セッション「[Stretching Failover Clusters and Using Storage Replica in Windows Server vNext](https://channel9.msdn.com/events/ignite/2015/brk3487)」(Windows Server vNext でのフェールオーバー クラスターの拡大と記憶域レプリカの使用) およびブログ記事「[Enable Change Notifications between Sites - How and Why?](/archive/blogs/qzaidi/enable-change-notifications-between-sites-how-and-why)」(サイト間での変更通知の有効化 - 方法とこれを行う理由) を参照してください。    

#### <a name="powershell-method"></a>PowerShell による方法

1. 提案されたクラスターをテストし、結果を分析して、続行できることを確認します。    

    ```PowerShell
    Test-Cluster SR-SRV01, SR-SRV02, SR-SRV03, SR-SRV04
    ```

    > [!NOTE]
    >  非対称ストレージ使用のために起こる、クラスター検証からのストレージ エラーを予測する必要があります。   

2.  HYPER-V 計算クラスターを作成します (クラスターで使用する独自の静的 IP アドレスを指定する必要があります)。 クラスター名が 15 文字以下であることを確認します。  ノードが異なるサブネットに存在する場合は、"OR" 依存関係を使用して追加のサイトの IP アドレスを作成する必要があります。 詳細につい[ては、「マルチサブネットクラスターの IP アドレスと依存関係の構成–パート III](https://techcommunity.microsoft.com/t5/Failover-Clustering/Configuring-IP-Addresses-and-Dependencies-for-Multi-Subnet/ba-p/371698)」を参照してください。  

    ```PowerShell
    New-Cluster -Name SR-SRVCLUS -Node SR-SRV01, SR-SRV02, SR-SRV03, SR-SRV04 -StaticAddress <your IP here> 

    Add-ClusterResource -Name NewIPAddress -ResourceType “IP Address” -Group “Cluster Group”

    Set-ClusterResourceDependency -Resource “Cluster Name” -Dependency “[Cluster IP Address] or [NewIPAddress]”
    ```


3. ドメイン コントローラーまたはその他のなんらかの独立したサーバーでホストされている共有を指す各クラスター内でファイル共有監視またはクラウド (Azure) 監視を構成します。 次に例を示します。  

    ```PowerShell
    Set-ClusterQuorum -FileShareWitness \\someserver\someshare
    ```

    >[!NOTE]
    > Windows Server には、Azure を使用したクラウド監視のオプションが追加されました。 ファイル共有監視に代えてこのクォーラム オプションを選択できます。  

   クォーラム構成の詳細については、「[クラスターとプールのクォーラム](../storage-spaces/understand-quorum.md)について」を参照してください。 Set-ClusterQuorum コマンドレットの詳細については、「[Set-ClusterQuorum](/powershell/module/failoverclusters/set-clusterquorum)」を参照してください。

4.  2 ノード ストレッチ クラスターを作成する場合は、作業を続行する前にすべての記憶域を追加する必要があります。 これを行うには、クラスター ノードで管理者アクセス許可を使用して PowerShell セッションを開き、コマンド `Get-ClusterAvailableDisk -All | Add-ClusterDisk` を実行します。

    この動作は、Windows Server 2016 の仕様です。

5. クラスター ネットワークが最適に構成されていることを確認します。  

6.  ファイル サーバーの役割を構成します。 次に例を示します。

    ```PowerShell  
    Get-ClusterResource  
    Add-ClusterFileServerRole -Name SR-CLU-FS2 -Storage "Cluster Disk 4"  

    MD e:\share01  

    New-SmbShare -Name Share01 -Path f:\share01 -ContinuouslyAvailable $false  
    ```

7. ストレッチ クラスター サイトの認識を構成し、サーバー SR SRV01 と SR SRV02 がサイト Redmond に含まれ、SR SRV03 と SR SRV04 がサイト Bellevue に含まれ、Redmond がソース記憶域と仮想マシンのノードの所有権で優先されるようにします。  

    ```PowerShell
    New-ClusterFaultDomain -Name Seattle -Type Site -Description "Primary" -Location "Seattle Datacenter"  

    New-ClusterFaultDomain -Name Bellevue -Type Site -Description "Secondary" -Location "Bellevue Datacenter"  

    Set-ClusterFaultDomain -Name sr-srv01 -Parent Seattle  
    Set-ClusterFaultDomain -Name sr-srv02 -Parent Seattle  
    Set-ClusterFaultDomain -Name sr-srv03 -Parent Bellevue  
    Set-ClusterFaultDomain -Name sr-srv04 -Parent Bellevue  

    (Get-Cluster).PreferredSite="Seattle"  
    ```

8.  (省略可能) DNS サイトの高速フェール オーバーのためにクラスター ネットワークと Active Directory を構成します。 拡大された VLAN、ネットワーク抽象化デバイス、短くした DNS の TTL、およびその他の一般的な手法を使用することができます。  
    
    詳細については、Microsoft Ignite セッション「[Stretching Failover Clusters and Using Storage Replica in Windows Server vNext](https://channel9.msdn.com/events/ignite/2015/brk3487)」(Windows Server vNext でのフェールオーバー クラスターの拡大と記憶域レプリカの使用) およびブログ記事「[Enable Change Notifications between Sites - How and Why?](/archive/blogs/qzaidi/enable-change-notifications-between-sites-how-and-why)」(サイト間での変更通知の有効化 - 方法とこれを行う理由) を参照してください。

### <a name="configure-a-stretch-cluster"></a>ストレッチ クラスターを構成する  
ここでは、フェールオーバー クラスター マネージャーまたは Windows PowerShell を使用してストレッチ クラスターを構成します。 次のすべての手順は、クラスターノードで直接実行することも、Windows Server リモートサーバー管理ツールを含むリモート管理コンピューターから実行することもできます。  

#### <a name="failover-cluster-manager-method"></a>フェールオーバー クラスター マネージャーを使用する方法  

1.  HYPER-V のワークロードの場合、レプリケートするデータがある 1 つのノード上で、既に構成されていない場合は、使用可能なディスクからクラスター化された共有ボリュームにソース データ ディスクを追加します。 すべてのディスクを追加しないでください。1 つのディスクを追加します。 この時点では、これは非対称の記憶域であるために、半分のディスクがオフラインとして表示されます。  
汎用ファイル サーバーと同様の物理ディスク リソース (PDR) ワークロードをレプリケートする場合、すぐに使用できる役割がアタッチされたディスクが既にあります。  

    ![フェールオーバー クラスター マネージャーの表示画面](./media/Stretch-Cluster-Replication-Using-Shared-Storage/Storage_SR_OnlineDisks2.png)  

2.  CSV ディスクまたは役割がアタッチされたディスクを右クリックし、**[レプリケーション]** をクリックして **[有効]** をクリックします。  

3.  適切なレプリケーション先のデータ ボリュームを選択し、**[次へ]** をクリックします。 表示されるレプリケーション先ディスクには、選択したレプリケーション元ディスクと同じサイズのボリュームがあります。 これらのウィザードのダイアログ間を移動するときには、使用可能な記憶域が自動的に移動し、必要に応じてバックグラウンドでオンラインになります。  

    ![記憶域レプリカの構成ウィザードの [レプリケーション先データ ディスクの選択] ページの表示画面](./media/Stretch-Cluster-Replication-Using-Shared-Storage/Storage_SR_SelectDestinationDataDisk2.png)  

4.  適切なレプリケーション元のログ ディスクを選択し、**[次へ]** をクリックします。 レプリケーション元ログ ボリュームは、回転ディスクではなく SSD または同様の高速なメディアを使用するディスク上に置かれている必要があります。  

5.  適切なレプリケーション先のログ ボリュームを選択し、[次へ] をクリックします。 表示されるレプリケーション先ログ ディスクには、選択したレプリケーション元ログ ディスクと同じサイズのボリュームがあります。  

6.  レプリケーション先ボリュームに、レプリケーション元サーバーからのデータの以前のコピーが含まれていない場合は、**[Overwrite Volume]** (ボリュームを上書き) の値を **[レプリケーション先ボリュームを上書き]** のままにします。 最近のバックアップまたは以前のレプリケーションからの類似したデータがレプリケーション先ボリュームに含まれている場合は、**[シードされたレプリケーション先ディスク]** を選択し、**[次へ]** をクリックします。  

7.  ゼロ PRO レプリケーションを使用する場合は、**[レプリケーション モード]** の値を **[同期レプリケーション]** のままにします。 待機時間が長いネットワーク上でクラスターを拡大する場合やプライマリ サイト ノード上で IO 待機時間を短縮する必要がある場合は、**[非同期レプリケーション]** に変更します。  
8.  レプリケーション グループ内で追加のディスクペアを使用して書き込み順序指定を後で使用する場合は、**[整合性グループ]** の値を **[最も高いパフォーマンス]** のままにします。 このレプリケーション グループにディスクを追加し、保証された書き込み順序指定が必要な場合は、**[書き込み順序を有効にする]** を選択し、**[次へ]** をクリックします。  

9.  **[次へ]** をクリックし、レプリケーションとストレッチ クラスターのフォーメーションを構成します。  

    ![記憶域レプリカの構成ウィザードの [確認] ページの表示画面](./media/Stretch-Cluster-Replication-Using-Shared-Storage/Storage_SR_ConfigureSR2.png)  

10. [概要] 画面で、確認ダイアログの結果をメモします。 Web ブラウザーでレポートを表示できます。  

11. この時点で、クラスターの半分ずつの間に記憶域レプリカのパートナーシップを構成しましたが、レプリケーションは進行中です。 グラフィカル ツールを使用していくつかの方法でレプリケーションの状態を見ることができます。  

    1.  **[レプリケーション ロール]** 列と **[レプリケーション]** タブを使用します。初期同期が完了したら、レプリケーション元とレプリケーション先のディスクのレプリケーションのステータスが **[継続的にレプリケートしています]** になります。   

        ![フェールオーバー クラスター マネージャーのディスクの [レプリケーション] タブの表示画面](./media/Stretch-Cluster-Replication-Using-Shared-Storage/Storage_SR_ReplicationDetails2.png)  

    2.  **eventvwr.exe** を起動します。  

        1.  レプリケーション元サーバー上で、**[アプリケーションとサービス]、[Microsoft]、[Windows]、[記憶域レプリカ]、[管理]** の順に移動し、イベント 5015、5002、5004、1237、5001、2200 を調べます。  

        2.  レプリケーション先サーバー上で、**[アプリケーションとサービス]、[Microsoft]、[Windows]、[記憶域レプリカ]、[操作可]** の順に移動し、イベント 1215 を待機します。 このイベントでは、コピーされたバイト数およびかかった時間が示されます。 例:  

            ```  
            Log Name:      Microsoft-Windows-StorageReplica/Operational  
            Source:        Microsoft-Windows-StorageReplica  
            Date:          4/6/2016 4:52:23 PM  
            Event ID:      1215  
            Task Category: (1)  
            Level:         Information  
            Keywords:      (1)  
            User:          SYSTEM  
            Computer:      SR-SRV03.Threshold.nttest.microsoft.com  
            Description:  
            Block copy completed for replica.  

            ReplicationGroupName: Replication 2  
            ReplicationGroupId: {c6683340-0eea-4abc-ab95-c7d0026bc054}  
            ReplicaName: \\?\Volume{43a5aa94-317f-47cb-a335-2a5d543ad536}\  
            ReplicaId: {00000000-0000-0000-0000-000000000000}  
            End LSN in bitmap:   
            LogGeneration: {00000000-0000-0000-0000-000000000000}  
            LogFileId: 0  
            CLSFLsn: 0xFFFFFFFF  
            Number of Bytes Recovered: 68583161856  
            Elapsed Time (ms): 140  
            ```  

        3.  レプリケーション元サーバー上で、**[アプリケーションとサービス]、[Microsoft]、[Windows]、[記憶域レプリカ]、[管理]** の順に移動し、イベント 5009、1237、5001、5015、5005、2200 を調べ、処理の進行状況を確認します。 このシーケンスではエラーの警告が存在しない必要があります。 イベント 1237 が多くあります。これは進行状況を示します。  

            > [!WARNING]
            > CPU とメモリ使用率は、初期同期が完了するまでは通常より高くなる可能性があります。  

#### <a name="windows-powershell-method"></a>Windows PowerShell による方法  

1.  特権を持つ管理者アカウントで Powershell コンソールが実行されていることを確認します。  
2.  レプリケーション元データストレージを CSV としてクラスターにのみ追加します。 使用可能なディスクのサイズ、パーティション、およびボリューム レイアウトを取得するには、次のコマンドを使用します。  

    ```PowerShell  
    Move-ClusterGroup -Name "available storage" -Node sr-srv01  

    $DiskResources = Get-ClusterResource | Where-Object { $_.ResourceType -eq 'Physical Disk' -and $_.State -eq 'Online' }  
    $DiskResources | foreach {  
        $resource = $_  
        $DiskGuidValue = $resource | Get-ClusterParameter DiskIdGuid  

        Get-Disk | where { $_.Guid -eq $DiskGuidValue.Value } | Get-Partition | Get-Volume |  
            Select @{N="Name"; E={$resource.Name}}, @{N="Status"; E={$resource.State}}, DriveLetter, FileSystemLabel, Size, SizeRemaining  
    } | FT -AutoSize  

    Move-ClusterGroup -Name "available storage" -Node sr-srv03  

    $DiskResources = Get-ClusterResource | Where-Object { $_.ResourceType -eq 'Physical Disk' -and $_.State -eq 'Online' }  
    $DiskResources | foreach {  
        $resource = $_  
        $DiskGuidValue = $resource | Get-ClusterParameter DiskIdGuid  

        Get-Disk | where { $_.Guid -eq $DiskGuidValue.Value } | Get-Partition | Get-Volume |  
            Select @{N="Name"; E={$resource.Name}}, @{N="Status"; E={$resource.State}}, DriveLetter, FileSystemLabel, Size, SizeRemaining  
    } | FT -AutoSize  
    ```  

4.  次のコマンドを使用して正しいディスクを CSV に設定します。  

    ```PowerShell  
    Add-ClusterSharedVolume -Name "Cluster Disk 4"  
    Get-ClusterSharedVolume  
    Move-ClusterSharedVolume -Name "Cluster Disk 4" -Node sr-srv01  
    ```  

5.  次の項目を指定してストレッチ クラスターを構成します。  

    -   レプリケーション元とレプリケーション先のノード (レプリケーション元データは CSV ディスクで、他のすべてのディスクは csv ディスクではありません)。  

    -   レプリケーション元とレプリケーション先のグループ名。  

    -   パーティション サイズが一致するレプリケーション元とレプリケーション先のディスク。  

    -   レプリケーション元とレプリケーション先のログ ボリューム。両方のディスクにログ サイズを格納するための十分な空き領域があり、SSD または同様の高速なメディアが必要です。  

    -   レプリケーション元とレプリケーション先のログ ボリューム。両方のディスクにログ サイズを格納するための十分な空き領域があり、SSD または同様の高速なメディアが必要です。  

    -   ログ サイズ。  

    -   レプリケーション元ログ ボリュームは、回転ディスクではなく SSD または同様の高速なメディアを使用するディスク上に置かれている必要があります。  

    ```PowerShell  
    New-SRPartnership -SourceComputerName sr-srv01 -SourceRGName rg01 -SourceVolumeName "C:\ClusterStorage\Volume1" -SourceLogVolumeName e: -DestinationComputerName sr-srv03 -DestinationRGName rg02 -DestinationVolumeName d: -DestinationLogVolumeName e:  
    ```  

    > [!NOTE]  
    > 各サイトの 1 つのノードで `New-SRGroup` を使用し、`New-SRPartnership` を使用して、すべて一度に実行するのではなく、各段階でレプリケーションを作成することができます。  

6.  レプリケーションの進行状況を確認します。  

    1.  レプリケーション元サーバーで、次のコマンドを入力し、イベント 5015、5002、5004、1237、5001、2200 を調べます。  

        ```PowerShell  
        Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica -max 20  
        ```  

    2.  レプリケーション先サーバーで、次のコマンドを実行して、パートナーシップの作成を示す記憶域レプリカ イベントを参照します。 このイベントでは、コピーされたバイト数およびかかった時間が示されます。 例:  

            Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica | Where-Object {$_.ID -eq "1215"} | fl  

            TimeCreated  : 4/6/2016 4:52:23 PM  
            ProviderName : Microsoft-Windows-StorageReplica  
            Id           : 1215  
            Message      : Block copy completed for replica.  

               ReplicationGroupName: Replication 2  
               ReplicationGroupId: {c6683340-0eea-4abc-ab95-c7d0026bc054}  
               ReplicaName: ?Volume{43a5aa94-317f-47cb-a335-2a5d543ad536}  
               ReplicaId: {00000000-0000-0000-0000-000000000000}  
               End LSN in bitmap:   
               LogGeneration: {00000000-0000-0000-0000-000000000000}  
               LogFileId: 0  
               CLSFLsn: 0xFFFFFFFF  
               Number of Bytes Recovered: 68583161856  
               Elapsed Time (ms): 140  

    3.  レプリケーション先サーバーで、次のコマンドを実行し、イベント 5009、1237、5001、5015、5005、2200 を調べて、処理の進行状況を把握します。 このシーケンスではエラーの警告が存在しない必要があります。 イベント 1237 が多くあります。これは進行状況を示します。  

        ```PowerShell  
        Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica | FL  
        ```  

    4.  または、レプリカのレプリケーション先サーバー グループでは、コピーの残りのバイト数が常時示されており、PowerShell を使って照会できます。 次に例を示します。  

        ```PowerShell  
        (Get-SRGroup).Replicas | Select-Object numofbytesremaining  
        ```  

        進行状況サンプル (終了しません):  

        ```PowerShell  
        while($true) {  

         $v = (Get-SRGroup -Name "Replication 2").replicas | Select-Object numofbytesremaining  
         [System.Console]::Write("Number of bytes remaining: {0}`r", $v.numofbytesremaining)  
         Start-Sleep -s 5  
        }  
        ```  

7.  ストレッチ クラスター内のレプリケーション元とレプリケーション先の状態を取得するには、`Get-SRGroup` と `Get-SRPartnership` を使用して、ストレッチ クラスター内のレプリケーションの構成された状態を表示します。  

    ```PowerShell  
    Get-SRGroup  
    Get-SRPartnership  
    (Get-SRGroup).replicas  
    ```  

### <a name="manage-stretched-cluster-replication"></a>ストレッチ クラスターのレプリケーションを管理する  
次に、ストレッチ クラスターを管理よおよび操作します。 次のすべての手順は、クラスターノードで直接実行することも、Windows Server リモートサーバー管理ツールを含むリモート管理コンピューターから実行することもできます。  

#### <a name="graphical-tools-method"></a>グラフィカル ツールによる方法  

1.  フェールオーバー クラスター マネージャーを使用して、レプリケーションの現在のソースと宛先およびそれらの状態を判別します。  

2.  レプリケーションのパフォーマンスを測定するには、ソースと宛先の両方のノードで **Perfmon.exe** を実行します。  

    1.  宛先ノードで次を実行します。  

        1.  **Storage Replica Statistics** オブジェクトと、データ ボリューム用のすべてのパフォーマンス カウンターを追加します。  

        2.  結果を確認します。  

    2.  移行元ノードで次を実行します。  

        1.  **Storage Replica Statistics** および **Storage Replica Partition I/O Statistics** オブジェクトと、データ ボリューム用のすべてのパフォーマンス カウンターを追加します (後者は現在のレプリケーション元サーバー上のデータにのみ使用できます)。  

        2.  結果を確認します。  

3.  ストレッチ クラスター内のレプリケーションのソースと宛先を変更するには、次の方法を使用します。  

    1.  同じサイト内のノード間でソースのレプリケーションを移動するには、ソース CSV を右クリックし、**[Move Storage]** (記憶域の移動) をクリックして、**[ノードの選択]** をクリックし、同じサイト内のノードを選択します。 ディスクに割り当てられた役割に対して CSV 以外の記憶域を使用している場合は、役割を移動する必要があります。  

    2.  ソースのレプリケーションを 1 つのサイトから別のサイトに移動するには、ソース CSV を右クリックし、**[Move Storage]** (記憶域の移動) をクリックして、**[ノードの選択]** をクリックし、別のサイト内のノードを選択します。 優先されるサイトを構成した場合は、使用可能な最善のノードを使用してレプリケーション元ストレージを優先サイト内のノードに常に移動することができます。 ディスクに割り当てられた役割に対して CSV 以外の記憶域を使用している場合は、役割を移動する必要があります。  

    3.  1 つのサイトから別のサイトへのレプリケーションの方向で予定されたフェールオーバーを実行するには、**ServerManager.exe** または **SConfig** を使用して 1 つのサイトで両方のノードをシャットダウンします。  

    4.  1 つのサイトから別のサイトのレプリケーションの方向で予定外のフェールオーバーを実行するには、1 つのサイトで両方のノードの電源を切ります。  

        > [!NOTE]
        > Windows Server 2016 では、ノードがオンラインになった後に、フェールオーバー クラスター マネージャーまたは Move-ClusterGroup を使用して宛先ディスクを別のサイトに手動で戻す必要のある場合があります。  

        > [!NOTE]
        > 記憶域レプリカは、宛先ボリュームをマウント解除します。 これは仕様です。  

4.  ログサイズを既定の 8 GB から変更するには、コピー元とコピー先の両方のログディスクを右クリックし、[**レプリケーションログ**] タブをクリックします。次に、両方のディスクのサイズを一致するように変更します。  

    > [!NOTE]  
    > 既定のログのサイズは 8 GB です。 `Test-SRTopology` コマンドレットの結果に応じて、より大きい値または小さい値を指定して `-LogSizeInBytes` を使用することを検討してください。  

5.  別のレプリケーションされるディスクのペアを既存のレプリケーション グループに追加するには、使用可能な記憶域内に少なくとも 1 つの余分なディスクがあることを確認する必要があります。 その後で、ソース ディスクを右クリックし、**[Add replication partnership]** (レプリケーション パートナーシップの追加) を選択します。  
    > [!NOTE]  
    > 使用可能記憶域でこの追加の "ダミー" ディスクが必要なのは回帰のためであり、意図しているものではありません。 以前は、フェールオーバー クラスター マネージャーでは通常、ディスクの追加がサポートされており、今後のリリースでも再びサポートされるようになります。  


6.  既存のレプリケーションを削除するには、次の手順を実行します。  

    1.  **cluadmin.msc** を起動します。  

    2.  ソース CSV ディスクを右クリックし、**[レプリケーション]** をクリックして、**[削除]** をクリックします。 警告メッセージを受け入れます。  

    3.  必要に応じて、将来のテスト用に CSV から記憶域を削除し、使用可能な記憶域に戻します。  

        > [!NOTE]  
        > 場合によっては、使用可能な記憶域に戻した後で**DiskMgmt.msc** または **ServerManager.exe** を使用して、ドライブ文字をボリュームに戻す必要があります。  

#### <a name="windows-powershell-method"></a>Windows PowerShell による方法  

1.  **Get-SRGroup** と **(Get-SRGroup).Replicas** を使用して、レプリケーションの現在のソースと宛先およびそれらの状態を判別します。  

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

    Windows PowerShell でのパフォーマンス カウンターの詳細については、「[Get-Counter](/powershell/module/microsoft.powershell.diagnostics/get-counter)」を参照してください。  

3.  ストレッチ クラスター内のレプリケーションのソースと宛先を変更するには、次の方法を使用します。  

    1.  **Redmond** サイトでレプリケーションのソースを 1 つのノードから別のノードに移動するには、Move-ClusterSharedVolume コマンドレットを使用して CSV リソースを移動します。  

        ```PowerShell  
        Get-ClusterSharedVolume | fl *  
        Move-ClusterSharedVolume -Name "cluster disk 4" -Node sr-srv02  
        ```  

    2.  レプリケーションの方向を 1 つのサイトから別の "予定" に移動するには、**Move-ClusterSharedVolume** コマンドレットを使用して CSV リソースを移動します。  

        ```PowerShell 
        Get-ClusterSharedVolume | fl *  
        Move-ClusterSharedVolume -Name "cluster disk 4" -Node sr-srv04  
        ```  

        これにより、他のサイトとノードに適したログとデータも移動します。  

    3.  1 つのサイトから別のサイトのレプリケーションの方向で予定外のフェールオーバーを実行するには、1 つのサイトで両方のノードの電源を切ります。  

        > [!NOTE]  
        > 記憶域レプリカは、宛先ボリュームをマウント解除します。 これは仕様です。  

4.  ログサイズを既定の 8 GB から変更するには、ソースとターゲットの両方のストレージレプリカグループで**セット-SRGroup**を使用します。   たとえば、すべてのログを 2GB に設定するには、次の手順を実行します。  

    ```PowerShell  
    Get-SRGroup | Set-SRGroup -LogSizeInBytes 2GB  
    Get-SRGroup  
    ```  

5.  別のレプリケーションされるディスクのペアを既存のレプリケーション グループに追加するには、使用可能な記憶域内に少なくとも 1 つの余分なディスクがあることを確認する必要があります。 その後で、ソース ディスクを右クリックし、[Add replication partnership] (レプリケーション パートナーシップの追加) を選択します。  
       >[!NOTE]
       >使用可能記憶域でこの追加の "ダミー" ディスクが必要なのは回帰のためであり、意図しているものではありません。 以前は、フェールオーバー クラスター マネージャーでは通常、ディスクの追加がサポートされており、今後のリリースでも再びサポートされるようになります。  

    **Set-SRPartnership** コマンドレットを **-SourceAddVolumePartnership** および **-DestinationAddVolumePartnership** パラメーターと共に使用します。  
6.  レプリケーションを削除するには、各ノードで `Get-SRGroup`、Get-`SRPartnership`、`Remove-SRGroup`、および `Remove-SRPartnership` を使用します。  

    ```PowerShell  
    Get-SRPartnership | Remove-SRPartnership  
    Get-SRGroup | Remove-SRGroup  
    ```  

    > [!NOTE]
    > リモート管理コンピューターを使用している場合は、これらのコマンドレットに対してクラスター名を指定し、さらに 2 つの RG 名を指定する必要があります。  

### <a name="related-topics"></a>関連トピック  
- [記憶域レプリカの概要](storage-replica-overview.md)  
- [サーバー間の記憶域レプリケーション](server-to-server-storage-replication.md)  
- [クラスターからクラスターへの記憶域のレプリケーション](cluster-to-cluster-storage-replication.md)  
- [記憶域レプリカ: 既知の問題](storage-replica-known-issues.md) 
- [記憶域レプリカ:よく寄せられる質問](storage-replica-frequently-asked-questions.md)  

## <a name="see-also"></a>参照  
- [Windows Server 2016](../../get-started/windows-server-2016.md)  
- [Windows Server 2016 での記憶域スペース ダイレクト](../storage-spaces/storage-spaces-direct-overview.md)
