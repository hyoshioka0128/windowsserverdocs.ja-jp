---
title: サーバー間のストレージレプリケーション
description: Windows 管理センターと PowerShell を含む、Windows Server のサーバー間のレプリケーションに記憶域レプリカをセットアップして使用する方法について説明します。
ms.prod: windows-server
manager: siroy
ms.author: nedpyle
ms.technology: storage-replica
ms.topic: get-started-article
author: nedpyle
ms.date: 04/26/2019
ms.assetid: 61881b52-ee6a-4c8e-85d3-702ab8a2bd8c
ms.openlocfilehash: a21000e857d702846703deb4f55380e1a998f6d2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402960"
---
# <a name="server-to-server-storage-replication-with-storage-replica"></a>記憶域レプリカを使用したサーバー間の記憶域レプリケーション

> 適用対象:Windows Server 2019、Windows Server 2016、Windows Server (半期チャネル)

記憶域レプリカを使用すると、2 台のサーバーがそれぞれ同じボリュームの同じコピーを持つようにデータの同期を構成できます。 このトピックでは、このようなサーバー間のレプリケーション構成の背景、設定方法、環境の管理方法について説明します。

記憶域レプリカを管理するには、 [Windows 管理センター](../../manage/windows-admin-center/overview.md)または PowerShell を使用できます。

Windows 管理センターで記憶域レプリカを使用する場合の概要ビデオを次に示します。
> [!video https://www.microsoft.com/videoplayer/embed/3aa09fd4-867b-45e9-953e-064008468c4b?autoplay=false]


## <a name="prerequisites"></a>前提条件  

* Active Directory Domain Services フォレスト (Windows Server 2016 を実行する必要はありません)。  
* Windows Server 2019 または Windows Server 2016, Datacenter Edition を実行する2台のサーバー。 Windows Server 2019 を実行している場合は、通常は Standard Edition を使用することができます。これにより、1つのボリュームのみを最大 2 TB までレプリケートできます。  
* SAS JBOD、ファイバー チャネル SAN、iSCSI ターゲット、またはローカル SCSI/SATA ストレージを使用する 2 セットの記憶域。 記憶域では HDD メディアと SSD メディアを混在させる必要があります。 各記憶域セットは、共有アクセスなしで、各サーバーでのみ利用可能となるように設定します。  
* 各記憶域セットでは、2 つ以上の仮想ディスク (レプリケートされたデータ用とログ用) を作成できる必要があります。 物理記憶域のセクター サイズは、すべてのデータ ディスクで同じである必要があります。 物理記憶域のセクター サイズは、すべてのログ ディスクで同じである必要があります。  
* 同期レプリケーションのために各サーバーで少なくとも 1 つのイーサネット/TCP 接続 (可能であれば RDMA)。   
* すべてのノード間での ICMP、SMB (ポート 445 と、SMB ダイレクト用のポート 5445)、WS-MAN (ポート 5985) の双方向トラフィックを許可する適切なファイアウォール規則およびルーター規則。  
* 書き込みの IO 負荷に十分対応できる帯域幅を持ちラウンド トリップ遅延時間が平均 5 ミリ秒である、同期レプリケーション用のサーバー間ネットワーク。 非同期レプリケーションには待機時間の推奨事項はありません。<br>
オンプレミスのサーバーと Azure Vm の間でレプリケートする場合は、オンプレミスのサーバーと Azure Vm の間にネットワークリンクを作成する必要があります。 これを行うには、 [expressroute](#add-azure-vm-expressroute)または[サイト間 vpn gateway 接続](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)を使用するか、Azure vm に vpn ソフトウェアをインストールして、オンプレミスのネットワークに接続します。
* レプリケート対象の記憶域を、Windows オペレーティング システムのフォルダーが含まれるドライブに配置することはできません。

> [!IMPORTANT]
>  このシナリオでは、各サーバーが別の物理または論理サイト上に存在する必要があります。 各サーバーは、ネットワーク経由で相互に通信できる必要があります。  


これらの要件の多くは、`Test-SRTopology cmdlet` を使用して確認できます。 記憶域レプリカまたは記憶域レプリカ管理ツール機能を 1 つ以上のサーバーにインストールすると、このツールにアクセスできるようになります。 このツールを使用するために、記憶域レプリカを構成する必要はありません。記憶域レプリカは、コマンドレットをインストールするためだけに構成します。 詳細は、以下の手順に記載されています。  

## <a name="windows-admin-center-requirements"></a>Windows 管理センターの要件

記憶域レプリカと Windows 管理センターを一緒に使用するには、次のものが必要です。

| System                        | オペレーティング システム                                            | 必須     |
|-------------------------------|-------------------------------------------------------------|------------------|
| 2 台のサーバー <br>(Azure Vm を含むオンプレミスのハードウェア、Vm、クラウド Vm の任意の組み合わせ)| Windows Server 2019、Windows Server 2016、または Windows Server (半期チャネル) | 記憶域レプリカ  |
| 1台の PC                     | Windows 10                                                  | Windows Admin Center |

> [!NOTE]
> 現時点では、サーバーで Windows 管理センターを使用して記憶域レプリカを管理することはできません。

## <a name="terms"></a>用語  
このチュートリアルでは、例として、次の環境を使用します。  

-   **SR-SRV05** および **SR-SRV06** という名前の 2 台のサーバー。  

-   2 つの異なるデータ センターを表す 2 つの論理 "サイト" である **Redmond** と **Bellevue**。  

![施設 5 のサーバーを施設 9 のサーバーでレプリケートしていることを示す図](media/Server-to-Server-Storage-Replication/Storage_SR_ServertoServer.png)  

**図 1: サーバー間のレプリケーション**  

## <a name="step-1-install-and-configure-windows-admin-center-on-your-pc"></a>手順 1:PC への Windows 管理センターのインストールと構成

Windows 管理センターを使用して記憶域レプリカを管理している場合は、次の手順を使用して、記憶域レプリカを管理するように PC を準備します。
1. [Windows 管理センター](../../manage/windows-admin-center/overview.md)をダウンロードしてインストールします。
2. [リモートサーバー管理ツール](https://www.microsoft.com/download/details.aspx?id=45520)をダウンロードしてインストールします。
    - Windows 10 バージョン1809以降を使用している場合は、次のようにインストールします。オンデマンド機能からの Windows PowerShell 用記憶域レプリカモジュール。
3. **[スタート]** ボタンを選択し、「 **powershell**」と入力して、[ **Windows powershell]** を右クリックし、 **[管理者として実行]** を選択して、powershell セッションを管理者として開きます。
4. 次のコマンドを入力して、ローカルコンピューターで WS-MANAGEMENT プロトコルを有効にし、クライアントでのリモート管理の既定の構成を設定します。

    ```PowerShell
    winrm quickconfig
    ```

5. 「 **Y** 」と入力して winrm サービスを有効にし、Winrm ファイアウォールの例外を有効にします。

## <a name="provision-os"></a>手順 2:オペレーティング システム、機能、役割、記憶域、およびネットワークのプロビジョニング

1.  Windows server のインストールの種類 **(デスクトップエクスペリエンス)** を使用して、両方のサーバーノードに windows server をインストールします。 
 
    ExpressRoute 経由でネットワークに接続された Azure VM を使用するには、「 [expressroute 経由でネットワークに接続されている AZURE vm の追加](#add-azure-vm-expressroute)」を参照してください。

3.  ネットワーク情報を追加し、サーバーを Windows 10 管理 PC と同じドメインに参加させ (使用している場合)、サーバーを再起動します。  

    > [!NOTE]
    > この時点以降、すべてのサーバーのビルトイン Administrator グループのメンバーであるドメイン ユーザーとして常にログオンします。 今後、グラフィカルなサーバーのインストールまたは Windows 10 コンピューターで実行するとき、PowerShell および CMD プロンプトを昇格してください。  

3.  JBOD 記憶域エンクロージャ、iSCSI ターゲット、FC SAN、またはローカル固定ディスク (DAS) の最初のセットをサイト**Redmond**のサーバーに接続します。  

4.  2番目の記憶域のセットをサイト**Bellevue**内のサーバーに接続します。  

5.  必要に応じて、両方のノードに最新のベンダー記憶域、格納装置ファームウェアとドライバー、最新のベンダー HBA ドライバー、最新のベンダー BIOS/UEFI ファームウェア、最新のベンダー ネットワーク ドライバー、および最新のマザーボード チップセット ドライバーをインストールします。 必要に応じてノードを再起動します。  

    > [!NOTE]
    > 共有記憶域およびネットワーク ハードウェアの構成については、ハードウェア ベンダーのドキュメントを参照してください。  

6.  サーバーの BIOS および UEFI の設定が、C 状態の無効化、QPI 速度の設定、NUMA の有効化、最大メモリ動作周波数の設定など、高パフォーマンスを有効にする設定であることを確認します。 Windows Server の電源管理が高パフォーマンスに設定されていることを確認します。 必要に応じて再起動します。  

7.  役割を次のように構成します。  

    -   **Windows 管理センターの方法**
        1. Windows 管理センターで、サーバーマネージャーに移動し、いずれかのサーバーを選択します。
        2. **[役割 & 機能]** に移動します。
        3. [**機能** > ] **[記憶域レプリカ]** の順に選択し、 **[インストール]** をクリックします。
        4. もう一方のサーバーでも繰り返します。
    -   **サーバーマネージャーメソッド**  

        1.  **ServerManager.exe** を実行してサーバー グループを作成し、すべてのサーバー ノードを追加します。  

        2.  各ノードに**ファイル サーバー**と**記憶域レプリカ**の役割と機能をインストールし、再起動します。  

    -   **Windows PowerShell メソッド**  

        SR-SRV06 またはリモート管理コンピューターの Windows PowerShell コンソールで、次のコマンドを実行して必要な機能と役割をインストールし、再起動します。  

        ```powershell  
        $Servers = 'SR-SRV05','SR-SRV06'  

        $Servers | ForEach { Install-WindowsFeature -ComputerName $_ -Name Storage-Replica,FS-FileServer -IncludeManagementTools -restart }  
        ```  

        詳細については、「[役割、役割サービス、または機能のインストールまたはアンインストール](../../administration/server-manager/install-or-uninstall-roles-role-services-or-features.md)」を参照してください。  

8.  記憶域を次のように構成します。  

    > [!IMPORTANT]  
    > -   各格納装置で、データ用に 1 つとログ用に 1 つの 2 つのボリュームを作成する必要があります。  
    > -   ログ ディスクとデータ ディスクは、MBR ではなく GPT として初期化する必要があります。  
    > -   2 つのデータ ボリュームは、同じサイズでなければなりません。  
    > -   2 つのログ ボリュームのサイズは同じでなければなりません。  
    > -   すべてのレプリケートされたデータ ディスクには、同一のセクター サイズが必要です。  
    > -   すべてのログ ディスクのセクター サイズは、同じである必要があります。  
    > -   ログ ボリュームには、SSD など、フラッシュ ベースのストレージを使用する必要があります。 ログ ストレージには、データ ストレージよりも大きな速度を確保することをお勧めします。 ログ ボリュームは、絶対に他のワークロードに使用しないでください。
    > -   データ ディスクには、HDD、SSD、または階層型の組み合わせを使用でき、ミラーまたはパリティ スペースか、RAID 1 または 10 もしくは RAID 5 または RAID 50 のいずれかを使用できます。  
    > -   ログ ボリュームは既定で 9 GB 以上である必要があり、ログ要件に応じて拡大または縮小する可能性もあります。  
    > -   ファイル サーバーの役割は、テスト用に必須ファイアウォール ポートを開くため、Test-SRTopology の動作にのみ必要です。
    
    - **JBOD エンクロージャの場合:**  

        1.  各サーバーがそのサイトのストレージ格納装置のみを参照できることと、SAS 接続が正しく構成されていることを確認します。  

        2.  記憶域スペースを使用して記憶域をプロビジョニングします。これには、「[スタンドアロン サーバーに記憶域スペースを展開する](../storage-spaces/deploy-standalone-storage-spaces.md)」の**手順 1 - 3** に従い、Windows PowerShell またはサーバー マネージャーを使用します。  

    - **ISCSI ストレージの場合:**  

        1.  各クラスターがそのサイトのストレージ格納装置のみを参照できることを確認します。 iSCSI を使用する場合は、複数の単一ネットワーク アダプターを使用する必要があります。    

        2.  ベンダーのドキュメントを参照して記憶域をプロビジョニングします。 Windows ベースの iSCSI ターゲットを使用する場合は、「[iSCSI ターゲット ブロック記憶域: 操作方法](../iscsi/iscsi-target-server.md)」を参照してください。  

    - **FC SAN ストレージの場合:**  

        1.  各クラスターがそのサイトのストレージ格納装置のみを参照できることと、ホストのゾーンが正しく設定されていることを確認します。   

        2.  ベンダーのドキュメントを参照して記憶域をプロビジョニングします。  

    - **ローカル固定ディスクストレージの場合:**  

        -   記憶域にシステムボリューム、ページファイル、ダンプファイルが含まれていないことを確認してください。  

        -   ベンダーのドキュメントを参照して記憶域をプロビジョニングします。  

9. Windows PowerShell を起動し、**Test-SRTopology** コマンドレットを使用して、記憶域レプリカのすべての要件を満たしているかどうかを判別します。 このコマンドレットは、簡単なテストのために要件のみモードで使用することも、実行時間の長いパフォーマンス評価モードで使用することもできます。  

    たとえば、それぞれ **F:** と **G:** のボリュームがあるノード候補を検証して、テストを 30 分間実行する場合は次のようになります。  
        
    ```PowerShell
    MD c:\temp  

    Test-SRTopology -SourceComputerName SR-SRV05 -SourceVolumeName f: -SourceLogVolumeName g: -DestinationComputerName SR-SRV06 -DestinationVolumeName f: -DestinationLogVolumeName g: -DurationInMinutes 30 -ResultPath c:\temp  
    ```

    > [!IMPORTANT]
      > 評価期間中に指定したソース ボリュームに対する書き込み IO 負荷のないテスト サーバーを使用している場合は、ワークロードの追加を検討してください。負荷がない場合、有用なレポートは生成されません。 実際の数値および推奨されるログのサイズを確認するには、実稼働環境と同様のワークロードでテストする必要があります。 または、単に、テスト中にソース ボリュームにいくつかのファイルをコピーするか、[DISKSPD](https://gallery.technet.microsoft.com/DiskSpd-a-robust-storage-6cd2f223) をダウンロードして実行することでも書き込み I/O を生成できます。 たとえば、D: ボリュームに対する 10 分間の低書き込み IO ワークロードによる例を次に示します。  
      >
      > `Diskspd.exe -c1g -d600 -W5 -C5 -b8k -t2 -o2 -r -w5 -i100 -j100 d:\test` 

10. 図2に示す**TestSrTopologyReport**レポートを調べて、記憶域レプリカの要件を満たしていることを確認します。  

    ![トポロジのレポートを表示している画面](media/Server-to-Server-Storage-Replication/SRTestSRTopologyReport.png)

    **図 2:ストレージレプリケーショントポロジレポート**

## <a name="step-3-set-up-server-to-server-replication"></a>手順 3:サーバー間のレプリケーションをセットアップする
### <a name="using-windows-admin-center"></a>Windows 管理センターを使用する

1. 移行元サーバーを追加します。
    1. **[追加]** ボタンを選択します。
    2. **[サーバー接続の追加]** を選択します。
    3. サーバーの名前を入力し、 **[送信]** を選択します。
2. **[すべての接続]** ページで、移行元サーバーを選択します。
3. ツール パネルから **記憶域レプリカ** を選択します。
4. 新しいパートナーシップを作成するには、 **[新規]** を選択します。
5. パートナーシップの詳細を入力し、 **[作成]** を選択します。 <br>
   ![新しい [パートナーシップ] 画面には、8 GB のログサイズなどの、パートナーシップの詳細が表示されます。](media/Storage-Replica-UI/Honolulu_SR_Create_Partnership.png)

    **図 3:新しいパートナーシップを作成する**

> [!NOTE]
> Windows 管理センターの記憶域レプリカからパートナーシップを削除しても、レプリケーショングループ名は削除されません。

### <a name="using-windows-powershell"></a>Windows PowerShell を使用する

次に、Windows PowerShell を使用してサーバー間のレプリケーションを構成します。 次のすべての手順は、ノード上で直接実行するか、Windows Server リモートサーバー管理ツールを含むリモート管理コンピューターから実行する必要があります。  

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
    > 既定のログのサイズは、8 GB です。 `Test-SRTopology` コマンドレットの結果に応じて、より大きい値または小さい値を指定して -LogSizeInBytes を使用することを検討してください。  

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

    2.  レプリケーション先サーバーで、次のコマンドを実行して、パートナーシップの作成を示す記憶域レプリカ イベントを参照します。 このイベントでは、コピーされたバイト数およびかかった時間が示されます。 例:  

        ```PowerShell  
        Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica | Where-Object {$_.ID -eq "1215"} | fl  
        ```
        次に出力の例を示します。
        ```
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
        > 記憶域レプリカは、宛先のボリュームとそのドライブ文字またはマウント ポイントをマウント解除します。 これは仕様です。  

    3.  または、レプリカのレプリケーション先サーバー グループでは、コピーの残りのバイト数が常時示されており、PowerShell を使って照会できます。 以下に例を示します。  

        ```PowerShell  
        (Get-SRGroup).Replicas | Select-Object numofbytesremaining  
        ```  

        進行状況を確認するサンプルを次に示します (サンプルは終了されません)。  

        ```PowerShell  
        while($true) {  

         $v = (Get-SRGroup -Name "RG02").replicas | Select-Object numofbytesremaining  
         [System.Console]::Write("Number of bytes remaining: {0}`r", $v.numofbytesremaining)  
         Start-Sleep -s 5  
        }  
        ```  

    4.  レプリケーション先サーバーで、次のコマンドを実行し、イベント 5009、1237、5001、5015、5005、2200 を調べて、処理の進行状況を把握します。 このシーケンスではエラーの警告が存在しない必要があります。 イベント 1237 が多くあります。これは進行状況を示します。  

        ```PowerShell  
        Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica | FL  
        ```  

## <a name="step-4-manage-replication"></a>手順 4:レプリケーションを管理する

これで、サーバー間のレプリケートされたインフラストラクチャを管理および運用できるようになります。 次のすべての手順は、ノード上で直接実行することも、Windows Server リモートサーバー管理ツールが含まれているリモート管理コンピューターから実行することもできます。  

1.  `Get-SRPartnership` と `Get-SRGroup` を使用して、現在のレプリケーション元とレプリケーション先およびそれらの状態を判別します。  

2.  レプリケーションのパフォーマンスを測定するには、ソースと宛先の両方のノードで `Get-Counter` コマンドレットを使用します。 カウンター名は次のとおりです。  

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

    Windows PowerShell でのパフォーマンス カウンターの詳細については、「[Get-Counter](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Diagnostics/Get-Counter)」を参照してください。  

3.  レプリケーションの方向を片方のサイトから移すには、`Set-SRPartnership` コマンドレットを使用します。  

    ```PowerShell  
    Set-SRPartnership -NewSourceComputerName sr-srv06 -SourceRGName rg02 -DestinationComputerName sr-srv05 -DestinationRGName rg01  
    ```  

    > [!WARNING]  
    > Windows Server では、初期同期の実行中に役割の切り替えが行われないようにします。初期レプリケーションの完了を許可する前に切り替えようとすると、データが失われる可能性があります。 初期同期が完了するまで、強制的に方向を切り替えないでください。  

    イベント ログを調べてレプリケーションの方向の変更と回復モードが発生しているかどうかを確認し、調整してください。 調整後、書き込み IO で、新しいレプリケーション元サーバーの所有する記憶域に書き込むことができます。 レプリケーションの方向を変更すると、前のソース コンピューター上で書き込み IO がブロックされます。  

4.  レプリケーションを削除するには、各ノードで `Get-SRGroup`、`Get-SRPartnership`、`Remove-SRGroup`、および `Remove-SRPartnership` を使用します。 `Remove-SRPartnership` コマンドレットは、レプリケーション先サーバーではなく、現在のレプリケーション ソース上でのみ実行してください。 両方のサーバーで `Remove-Group` を実行します。 たとえば、2 台のサーバーからすべてのレプリケーションを削除するには、次の手順に従います。  

    ```powershell
    Get-SRPartnership  
    Get-SRPartnership | Remove-SRPartnership  
    Get-SRGroup | Remove-SRGroup  
    ```  

## <a name="replacing-dfs-replication-with-storage-replica"></a>DFS レプリケーションを記憶域レプリカに置き換える  
多くの Microsoft ユーザーは、ホーム フォルダーおよび部門別の共有のような非構造化ユーザー データの災害復旧ソリューションとして、DFS レプリケーションを展開しています。 DFS レプリケーションは、Windows Server 2003 R2 以降のすべてのオペレーティング システムに付属しており、帯域幅の狭いネットワークで動作するため、ノードが多数あり、待機時間が長く変更の少ない環境に適しています。 ただし、DFS レプリケーションには、データ レプリケーション ソリューションとして重要な以下の制限があります。  
* 使用中または開いているファイルはレプリケートされません。  
* 同期的にレプリケートされません。  
* 非同期レプリケーションの待機期間は数分、数時間、または数日かかることがあります。  
* 電源中断の後に時間のかかる一貫性チェックが必要になるデータベースを使用します。  
* 通常、マルチマスターとして構成されます。これにより、双方向のフローに変更が加えられ、新しいデータが上書きされる可能性があります。  

記憶域レプリカには、これらの欠点はありません。 ただし、いくつかの制限はあり、環境によっては利点が薄くなる可能性があります。  

* ボリューム間で実行できるのは 1 対 1 のレプリケーションのみです。 複数のサーバー間で異なるボリュームをレプリケートすることができます。  
* 非同期レプリケーションはサポートされていますが、低帯域幅で待機時間の長いネットワーク用には設計されていません。  
* レプリケーションの進行中に、宛先の保護されたデータへのユーザーアクセスを許可しません。  

これらの要素が障害とならない場合は、記憶域レプリカを使用し、DFS レプリケーション サーバーをこの新しいテクノロジで置き換えることができます。   
このプロセスの概要は次のとおりです。  

1. Windows Server を2台のサーバーにインストールし、記憶域を構成します。 環境によっては、既存の一連のサーバーのアップグレードまたはクリーン インストールを行うことになります。  
2. レプリケートするデータが C ドライブ以外の 1 つ以上のデータ ボリューム上に存在することを確認します。   
   a.  バックアップやファイルのコピー、シン プロビジョニングされた記憶域を使用して片方のサーバー上のデータをシードし、時間を節約することもできます。 DFS レプリケーションとは異なり、メタデータのようなセキュリティを完全に一致させる必要はありません。  
3. 移行元サーバーでデータを共有し、DFS 名前空間を使用してアクセスできるようにします。 これは、サーバー名が障害の発生しているサイトにあるサーバーの名前に変更された場合でも、ユーザーがサーバーにアクセスできるようにするために重要です。  
   a.  レプリケーション先サーバーで一致する共有を作成することができます。この共有は、通常の操作中には利用できません。   
   b.  移行先サーバーを DFS 名前空間に追加しないでください。または、実行する場合は、すべてのフォルダーターゲットが無効になっていることを確認してください。  
4. 記憶域レプリカのレプリケーションを有効にして、初回の同期を完了します。レプリケーションは、同期的と非同期的のどちらでも実行できます。   
   a.  ただし、レプリケーション先サーバーでの IO データの一貫性を保つために、同期的に実行することをお勧めします。   
   b.  ボリューム シャドウ コピーを有効にして、VSSADMIN またはその他のお好みのツールで定期的にスナップショットを撮ることを強くお勧めします。 これによって、アプリケーションは一貫してデータ ファイルをディスクにフラッシュするようになります。 障害が発生した場合、レプリケーション先サーバー上の部分的に非同期レプリケート済みのスナップショットからファイルを回復できます。 スナップショットは、ファイルと共にレプリケートされます。  
5. 障害が発生するまでは正常に動作します。  
6. レプリケーション先サーバーを新しいソース サーバーに切り替えると、このサーバーのレプリケート済みボリュームがユーザーに示されます。  
7. 同期レプリケーションを使用している場合、ソース サーバーの損失時にユーザーがトランザクション保護なし (これはレプリケーションには関係ありません) でデータを書き込むアプリケーションを使用していない限り、データの復元は必要ありません。 非同期レプリケーションを使用している場合、VSS スナップショットをマウントする必要性が高くなりますが、アプリケーションのスナップショットの一貫性を保つため、どのような場合でも VSS の使用を検討してください。  
8. サーバーとその共有を DFS 名前空間フォルダーターゲットとして追加します。   
9. これによって、ユーザーがデータにアクセスできるようになります。  

   > [!NOTE]
   > 障害回復の計画は複雑な問題であるため、細心の注意が必要です。 Runbook の作成と、年単位でのライブ フェールオーバー ドリルの実行を強くお勧めします。 実際の障害発生時には混乱の中での対応となり、また経験豊富な担当者は手が空いていない場合もあります。  

## <a name="add-azure-vm-expressroute"></a>ExpressRoute 経由でネットワークに接続されている Azure VM の追加

1. [Azure portal に ExpressRoute を作成](https://docs.microsoft.com/azure/expressroute/expressroute-howto-circuit-portal-resource-manager)します。<br>ExpressRoute が承認されると、リソースグループがサブスクリプションに追加されます。この新しいグループを表示するには、 **[リソースグループ]** に移動します。 仮想ネットワーク名をメモしておきます。
![ExpressRoute によって追加されたリソースグループを示す Azure portal](media/Server-to-Server-Storage-Replication/express-route-resource-group.png)
    
    **図 4:ExpressRoute に関連付けられているリソース-仮想ネットワーク名をメモします。**
1. [新しいリソースグループを作成](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal)します。
1. [ネットワークセキュリティグループを追加](https://docs.microsoft.com/azure/virtual-network/virtual-networks-create-nsg-arm-pportal)します。 作成時に、作成した ExpressRoute に関連付けられているサブスクリプション ID を選択し、作成したばかりのリソースグループを選択します。
<br><br>必要な受信および送信のセキュリティ規則をネットワークセキュリティグループに追加します。 たとえば、VM へのリモートデスクトップアクセスを許可することができます。
1. 次の設定を使用して[AZURE VM を作成](https://docs.microsoft.com/azure/virtual-machines/windows/quick-create-portal)します (図5を参照)。
    - **パブリック IP アドレス**:なし
    - **仮想ネットワーク**:ExpressRoute で追加したリソースグループからメモした仮想ネットワークを選択します。
    - **ネットワークセキュリティグループ (ファイアウォール)** :前に作成したネットワークセキュリティグループを選択します。
    ![ExpressRoute ネットワーク設定](media/Server-to-Server-Storage-Replication/azure-vm-express-route.png)
    **を示す仮想マシンの作成図 5:ExpressRoute のネットワーク設定を選択しているときに VM を作成する**
1. VM が作成されたら、 [「手順 2:オペレーティングシステム、機能、役割、記憶域、およびネットワーク](#provision-os)をプロビジョニングします。


## <a name="related-topics"></a>関連トピック  
- [記憶域レプリカの概要](storage-replica-overview.md)  
- [共有記憶域を使用した拡張クラスターレプリケーション](stretch-cluster-replication-using-shared-storage.md)  
- [クラスターからクラスターへの記憶域のレプリケーション](cluster-to-cluster-storage-replication.md)
- [記憶域レプリカ:既知の問題](storage-replica-known-issues.md)  
- [記憶域レプリカ:よく寄せられる質問](storage-replica-frequently-asked-questions.md)
- [Windows Server 2016 の記憶域スペースダイレクト](../storage-spaces/storage-spaces-direct-overview.md)  
