---
title: "クラスター オペレーティング システムのローリング アップグレード"
ms.prod: windows-server-threshold
ms.technology: storage-failover-clustering
ms.topic: get-started-article
ms.assetid: 6e102c1f-df26-4eaa-bc7a-d0d55d3b82d5
author: jasongerend
ms.author: jgerend
ms.date: 10/17/2017
ms.openlocfilehash: 8463c163294a4d2223a74b7cfeaea6ac5ae4fcfe
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="cluster-operating-system-rolling-upgrade"></a>クラスター オペレーティング システムのローリング アップグレード

> 適用対象: Windows Server (半期チャネル)、Windows Server 2016

クラスター OS のローリング アップグレード、管理者は、Hyper-V やスケール アウト ファイル サーバーのワークロードを停止することがなく、クラスター ノードのオペレーティング システムのアップグレードを有効にします。 この機能を使用して、サービス レベル アグリーメント (SLA) に対してダウンタイム ペナルティを回避できます。

クラスター OS のローリング アップグレードすると、次の利点があります。

- 仮想マシンを Hyper-V とスケール アウト ファイル サーバー (SOFS) ワークロードを実行しているフェールオーバー クラスターはダウンタイムなし (クラスターのすべてのクラスター ノードで実行されている)、Windows Server 2016 に (クラスターのすべてのノードで実行されている) Windows Server 2012 R2 からアップグレードすることができます。 その他のクラスター ワークロード、たとえば、SQL Server は使用できませんにフェールオーバーする Windows Server 2016 にかかる時間 (5 分通常より小さい) 中にします。  
- その他のハードウェアは必要ありません。 追加することができますが、クラスター ノード一時的に、クラスター OS のローリング アップグレード中に、クラスターの可用性を向上させるために小規模なクラスターを処理します。  
- クラスターを停止または再開する必要はありません。  
- 新しいクラスターでは必要ありません。 既存のクラスターをアップグレードします。 さらに、Active Directory に格納されている既存のクラスター オブジェクトが使用されます。  
- アップグレード プロセスは、Windows Server 2016 を実行している顧客が各自の判断、「ポイント-の-ノーリターン」、すべてのクラスター ノードとなるまで、および Update-ClusterFunctionalLevel PowerShell コマンドレットを実行すると元に戻せる状態です。  
- クラスターの OS が混在モードで実行中に修正プログラムの適用やメンテナンスの操作をサポートできます。  
- PowerShell と WMI による自動化がサポートしています。  
- クラスターのパブリック プロパティ**ClusterFunctionalLevel**プロパティは、Windows Server 2016 のクラスター ノードでクラスターの状態を示します。 このプロパティを照会するには、フェールオーバー クラスターに属している Windows Server 2016 のクラスター ノードからの PowerShell コマンドレットを使用します。  
    ```PowerShell
    Get-Cluster | Select ClusterFunctionalLevel  
    ```  

    値**8**クラスターが Windows Server 2012 R2 の機能レベルで実行されていることを示します。 値**9**クラスターが Windows Server 2016 の機能レベルで実行されていることを示します。  

このガイドでは、クラスター OS のローリング アップグレード プロセス、インストール手順、機能の制限、およびよく寄せられる質問 (Faq) のさまざまなステージをについて説明しは、次の Windows Server 2016 でクラスター OS のローリング アップグレード シナリオに適用。  
- Hyper-V クラスター  
- 対応するスケール アウト ファイル サーバー クラスター  

Windows Server 2016 では、次のシナリオがサポートされていません。  
-  仮想ハード_ディスクを使用してクラスターのクラスター OS のゲストのローリング アップグレード (.vhdx file) 共有記憶域として  

クラスター OS のローリング アップグレードすると、System Center Virtual Machine Manager (SCVMM) 2016 では完全にサポートします。 SCVMM 2016 を使用している場合は、次を参照してください。[Windows Server 2012 R2 のアップグレードは、VMM での Windows Server 2016 にクラスター](https://technet.microsoft.com/library/mt445417.aspx)ガイダンスについては、クラスターをアップグレードすると、このドキュメントで説明されている手順を自動化することにします。  

## <a name="requirements"></a>要件  
クラスター OS のローリング アップグレード プロセスを開始する前に、次の要件を完了します。

- Windows Server (半期チャネル)、Windows Server 2016、または Windows Server 2012 R2 を実行しているフェールオーバー クラスターを起動します。
- Windows Server に、記憶域スペース ダイレクト クラスターをアップグレードするバージョン 1709 はサポートされていません。
- Hyper-V Vm、またはスケール アウト ファイル サーバー クラスターのワークロードがある場合は、ダウンタイムのアップグレードをことができます。
- Hyper-V ノードが第 2 レベル アドレス指定テーブル (SLAT) を使用して、次の方法のいずれかをサポートする Cpu があることを確認します。  
        -確認、[SLAT 対応していますか?WP8 SDK のヒント: 01](http://blogs.msdn.com/b/devfish/archive/2012/11/06/are-you-slat-compatible-wp8-sdk-tip-01.aspx) CPU が SLATs をサポートしているかを確認する 2 つの方法を説明する記事  
        -Download、[Coreinfo v3.31](https://technet.microsoft.com/sysinternals/cc835722) CPU が SLAT をサポートしているかを決定するツールです。

## <a name="cluster-transition-states-during-cluster-os-rolling-upgrade"></a>クラスター OS のローリング アップグレード中にクラスターの移行の状態

このセクションでは、クラスター OS のローリング アップグレードを使用して Windows Server 2016 にアップグレードされる Windows Server 2012 R2 クラスターのさまざまな状態の遷移について説明します。  

Windows Server 2012 R2 ノードから Windows Server 2016 へのクラスター ワークロードの移行、クラスター OS のローリング アップグレード プロセス中に実行するクラスター ワークロードを維持するためには、ノードは、両方のノードは、Windows Server 2012 R2 オペレーティング システムを実行していた場合は動作します。 Windows Server 2016 のノードがクラスターに追加されると、Windows Server 2012 R2 の互換モードで動作します。 「の OS が混在モード」と呼ばれる、新しいクラスターの概念的なモードでは、同じ内に存在するさまざまなバージョンのノード クラスター (図 1 を参照してください)。  

![クラスター OS のローリング アップグレードの 3 つのステージを示す図: Windows Server 2012 R2 のすべてのノードの OS が混在モード、および Windows Server 2016 のすべてのノード](media/Cluster-Operating-System-Rolling-Upgrade/Clustering_RollingUpgrade_Overview.png)  
**図 1: クラスター オペレーティング システムの状態遷移**  

Windows Server 2012 R2 クラスターは、Windows Server 2016 のノードがクラスターに追加される際の OS が混在モードを入力します。 プロセスは完全に元に戻せる状態 - Windows Server 2016 のノードは、クラスターから削除することができますおよび Windows Server 2012 R2 ノードは、このモードでは、クラスターに追加することができます。 Update-ClusterFunctionalLevel PowerShell コマンドレット、クラスターで実行している場合は、「戻すことができない」です。 このコマンドレットを成功させるためには、すべてのノードは、Windows Server 2016 である必要があり、すべてのノードをオンラインにする必要があります。  

## <a name="transition-states-of-a-four-node-cluster-while-performing-rolling-os-upgrade"></a>4 ノード クラスター OS のローリング アップグレードの実行中の状態の遷移

このセクションを示していて、共有の記憶域ノードは Windows Server 2012 R2 から Windows Server 2016 にアップグレードを使用するクラスターの 4 つの異なる段階について説明します。  

「ステージ 1」は、初期状態 - Windows Server 2012 R2 クラスターに開始しました。  

![初期状態を示す図: Windows Server 2012 R2 のすべてのノード](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage1.png)  
**図 2: 初期状態: Windows Server 2012 R2 フェールオーバー クラスター (ステージ 1)**  

「ステージ 2」は、2 つのノードが一時停止、ドレイン、削除、再フォーマットされ、およびされている Windows Server 2016 をインストールします。  

![OS が混在モードで、クラスターを示す図 2 つのノード、例 4 ノード クラスターから、Windows Server 2016 を実行していると、2 つのノードは、Windows Server 2012 R2 を実行している。](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage2.png)  
**図 3: 中間の状態: の OS が混在モード: Windows Server 2012 R2 および Windows Server 2016 のフェールオーバー クラスター (ステージ 2)**  

「ステージ 3」、Windows Server 2016 にアップグレードしたすべてのクラスターのノードと、クラスターが Update-ClusterFunctionalLevel PowerShell コマンドレットでアップグレードする準備ができてします。  

> [!NOTE]  
> この段階でプロセスを完全に切り替えることができます、および Windows Server 2012 R2 ノードは、このクラスターに追加することができます。  

![クラスターが完全に、Windows Server 2016 にアップグレードされたクラスターの機能レベルを Windows Server 2016 までを移植する準備が整った Update-ClusterFunctionalLevel コマンドレットであることを示す図](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage3.png)  
**図 4: 中間の状態: Windows Server 2016、Update-ClusterFunctionalLevel (ステージ 3) の準備ができてにアップグレードするすべてのノード**  

Update-ClusterFunctionalLevelcmdlet を実行すると、クラスターは「4 ステージ」、新しい Windows Server 2016 クラスター機能を使用できる場所を入力します。  

![クラスター ローリング OS のアップグレードが正常に完了したがされたを示す図Windows Server 2016 にアップグレードしたすべてのノードとクラスターは、Windows Server 2016 クラスターの機能レベルで実行しています。](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage4.png)  
**図 5: 最終状態: Windows Server 2016 のフェールオーバー クラスター (ステージ 4)**  

## <a name="cluster-os-rolling-upgrade-process"></a>クラスター OS のローリング アップグレード プロセス

このセクションでは、クラスター OS のローリング アップグレードを実行するためのワークフローについて説明します。  

![クラスターのアップグレードのワークフローを示す図](media/Cluster-Operating-System-Rolling-Upgrade/Clustering_RollingUpgrade_Workflow.png)  
**図 6: クラスター OS のローリング アップグレードのプロセス ワークフロー**  

クラスター OS のローリング アップグレードには、次の手順が含まれています。  

1. 次のように、オペレーティング システムのアップグレードのクラスターを準備します。  
    1. クラスター OS のローリング アップグレードするには、一度に 1 つのノードをクラスターから削除する必要があります。 オペレーティング システムのアップグレードのクラスターから 1 つのクラスター ノードが削除される HA Sla を維持するためにクラスターに十分な容量があるかどうかを確認します。 クラスター OS のローリング アップグレードのプロセス中に 1 つのノードがクラスターから削除されたときに別のノードにワークロードをフェールオーバーする機能を言い換えるは必要ですか。 クラスターはクラスター OS のローリング アップグレードの 1 つのノードがクラスターから削除された場合に、必要なワークロードを実行する能力をいますか。  
    2. Hyper-V のワークロードの場合、すべての Windows Server 2016 の Hyper-V ホストが CPU Second Level Address テーブル (SLAT) のサポートがあることを確認します。 SLAT 対応コンピューターだけでは、Windows Server 2016 で Hyper-V ロールを使用できます。  
    3. チェック、ワークロードのバックアップが完了したら、し、クラスターをバックアップを検討してください。 クラスターにノードを追加するときに、バックアップ操作を停止します。  
    4. すべてのクラスター ノードがオンラインでことを確認]、[実行/アップを使用して、[`Get-ClusterNode`](https://technet.microsoft.com/library/ee460990.aspx)コマンドレット (図 7 を参照してください)。  

        ![Get-ClusterNode コマンドレットの実行の結果が表示される [screencap]](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_GetClusterNode.png)  
        **図 7: Get-ClusterNode コマンドレットを使用して、ノードの状態を判断します。**  

    5. クラスター対応更新 (CAU) を実行している場合は、CAU が現在使用して実行していることを確認、**クラスタ認識して更新**UI、または[`Get-CauRun`](https://technet.microsoft.com/library/hh847230.aspx)コマンドレット (図 8 を参照してください)。 CAU の使用を停止、[`Disable-CauClusterRole`](https://technet.microsoft.com/library/hh847219.aspx)コマンドレット (図 9 を参照してください) を使用して、任意のノードから一時停止またはクラスター OS のローリング アップグレード プロセス中に、CAU によってドレインを防止します。  

        ![Get-CauRun コマンドレットの出力を示す [screencap]](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_GetCAU.png)  
        **図 8: を使用して、[`Get-CauRun`](https://technet.microsoft.com/library/hh847230.aspx)コマンドレットは、クラスターでクラスター対応更新プログラムが実行されているかどうかを決定するには**  

        ![Disable-CauClusterRole コマンドレットの出力を示す [screencap]](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_DisableCAU.png)  
        **図 9: は、クラスター対応更新の役割を使用して、無効にすると、[`Disable-CauClusterRole`](https://technet.microsoft.com/library/hh847219.aspx)コマンドレット**  

2. クラスターの各ノードでは、次の手順を実行します。  
    1. クラスター マネージャーの UI を使用して、ノードを選択し、使用、**一時停止 |ドレイン**ノードのドレインを実行するメニュー オプション (図 10 を参照してください) を使用して、または、[`Suspend-ClusterNode`](https://technet.microsoft.com/library/ee461051.aspx)コマンドレット (図 11 を参照してください)。  

        ![クラスター マネージャーの UI での役割のドレインを実行する方法を示す [screencap]](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_FCM_DrainRoles.png)  
        **図 10: フェールオーバー クラスター マネージャーを使用してノードからの役割のドレイン**  

        ![Suspend-ClusterNode コマンドレットの出力を示す [screencap]](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_SuspendNode.png)  
        **図 11: ドレインからノードを使用して、役割、[`Suspend-ClusterNode`](https://technet.microsoft.com/library/ee461051.aspx)コマンドレット**  

    2.  クラスター マネージャーの UI を使用して**削除**クラスター、または使用から一時停止したノード、[`Remove-ClusterNode`](https://technet.microsoft.com/library/ee461001.aspx)コマンドレット。  

        ![Remove-ClusterNode コマンドレットの出力を示す [screencap]](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_RemoveNode.png)  
        **図 12: を使用して、クラスターからノードを削除する[`Remove-ClusterNode`](https://technet.microsoft.com/library/ee461001.aspx)コマンドレット**  

    3.  システム ドライブを再フォーマットし、ノードを使用して、[Windows Server 2016 の「オペレーティング システムのクリーン インストール」を実行、**カスタム: Windows のみをインストール (詳細)** setup.exe のインストール (「図 13) オプション。 選択しないように、**アップグレード: Windows のインストールと状態で保持するファイル、設定、およびアプリケーション**インプレース アップグレードをお勧めしないクラスター OS のローリング アップグレードのためのオプションです。  

        ![選択したカスタム インストール オプションを示す Windows Server 2016 のインストール ウィザードの [screencap]](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_InstallOption.png)  
        **Windows Server 2016 の図 13: 利用可能なインストール オプション**  

    4.  適切な Active Directory ドメインに、ノードを追加します。  
    5.  適切なユーザーを Administrators グループに追加します。  
    6.  サーバー マネージャーの UI または Install-WindowsFeature PowerShell コマンドレットを使用して、Hyper-V などの必要があるサーバーの役割をインストールします。  

        ```PowerShell
        Install-WindowsFeature -Name Hyper-V  
        ```  

    7.  サーバー マネージャーの UI または Install-WindowsFeature PowerShell コマンドレットを使用して、フェールオーバー クラスタ リング機能をインストールします。  

        ```PowerShell
        Install-WindowsFeature -Name Failover-Clustering  
        ```  

    8.  クラスターのワークロードに必要なすべての追加機能をインストールします。  
    9. フェールオーバー クラスター マネージャーの UI を使用してネットワークと記憶域の接続設定を確認します。  
    10. Windows ファイアウォールを使用する場合は、ファイアウォール設定が、クラスターの正しいことを確認します。 たとえば、クラスター対応更新 (CAU) 有効になっているクラスターでは、ファイアウォールの構成を必要があります。  
    11. Hyper-V のワークロードの場合、Hyper-V マネージャーの UI を使用して仮想スイッチ マネージャー] ダイアログを起動 (図 14 参照)。  

        使用する仮想スイッチの名前が、クラスター内のすべての Hyper-V ホスト ノードで同じであることを確認します。  

        ![Hyper-V 仮想スイッチ マネージャー] ダイアログ ボックスの位置を示す [screencap]](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_VMSwitch.png)  
        **図 14: 仮想スイッチ マネージャー**  

    12. Windows Server 2016 のノードに (Windows Server 2012 R2 ノードを使用しない、)、フェールオーバー クラスター マネージャーを使用して (図 15 を参照してください) を使用して、クラスターに接続します。  

        ![クラスターの選択] ダイアログの表示 [screencap]](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_AddNode.png)  
        **図 15: フェールオーバー クラスター マネージャーを使用して、クラスターにノードを追加します。**  

    13. フェールオーバー クラスター マネージャーの UI を使用して、または[`Add-ClusterNode`](https://technet.microsoft.com/library/ee461047.aspx)コマンドレット (図 16 を参照してください) を使用して、クラスターにノードを追加します。  

        ![Add-ClusterNode コマンドレットの出力を示す [screencap]](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_AddNode3.png)  
        **図 16: を使用して、クラスター ノードに追加する[`Add-ClusterNode`](https://technet.microsoft.com/library/ee461047.aspx)コマンドレット**  

        > [!NOTE]  
        > Windows Server 2016 の最初のノード クラスターに参加するときに、クラスターは"混在 OS"モードでを入力し、クラスター コア リソースは、Windows Server 2016 のノードに移動します。 "混在 OS"モードのクラスターは、完全に機能クラスター ノードの古い互換モードで新しいノードが実行される場所です。 "混在 OS"モードは、クラスターの一時的なモードです。 永続的なするものではありませんし、お客様が 4 週間以内にそのクラスターのすべてのノードの更新プログラムを含んでいます。  

    14. Windows Server 2016 の後にノードが正常にクラスターに追加、ことができます (必要に応じて) に移動するクラスター ワークロードのいくつか、新しく追加されたノード次のように、クラスター全体での作業負荷を再調整するために。

        ![Move-ClusterVirtualMachineRole コマンドレットの出力を示す [screencap]](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_MoveVMRole.png)  
        **図 17: 移行を使用してクラスター ワークロード (クラスターの VM ロール) [`Move-ClusterVirtualMachineRole`](https://technet.microsoft.com/library/ee461041.aspx)コマンドレット**  

        1. 使用**ライブ マイグレーション**バーチャル マシンのフェールオーバー クラスター マネージャーから、または[`Move-ClusterVirtualMachineRole`](https://technet.microsoft.com/library/ee461041.aspx)コマンドレット (図 17 を参照してください) を使用して仮想マシンのライブ マイグレーションを実行します。  

            ```PowerShell
            Move-ClusterVirtualMachineRole -Name VM1 -Node robhind-host3  
            ```  

        2. 使用**移動**フェールオーバー クラスター マネージャーから、または[`Move-ClusterGroup`](https://technet.microsoft.com/library/ee461002.aspx)コマンドレットは他のクラスター ワークロードにします。  

3. すべてのノードには Windows Server 2016 にアップグレードされ、クラスターに戻す場合や Windows Server 2012 R2 の残りのノードが削除されている場合は、次の操作を行います。  

    > [!IMPORTANT]  
    > -   クラスターの機能レベルを更新した後は、Windows Server 2012 R2 の機能レベルに戻すことはできませんし、Windows Server 2012 R2 ノードがクラスターに追加することはできません。
    > -   されるまで、[`Update-ClusterFunctionalLevel`](https://technet.microsoft.com/library/mt589702.aspx)コマンドレットを実行、プロセスは完全に元に戻せる状態、および Windows Server 2012 R2 ノードは、このクラスターに追加することができますおよび Windows Server 2016 のノードを削除することができます。  
    > -   後に、[`Update-ClusterFunctionalLevel`](https://technet.microsoft.com/library/mt589702.aspx)コマンドレットの実行、新機能が利用可能になります。  

    1.  フェールオーバー クラスター マネージャーの UI を使用して、または[`Get-ClusterGroup`](https://technet.microsoft.com/library/ee461017.aspx)コマンドレット、期待どおりにすべてのクラスターの役割をクラスターで実行していることを確認します。 次の例で使用可能記憶域が使用されていない、CSV を使用する代わりに、そのため、使用可能記憶域が表示されます、**オフライン**状態 (図 18 参照)。  

        ![Get-ClusterGroup コマンドレットの出力を示す [screencap]](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_GetClusterGroup.png)  
        **使用して図 18: を実行しているすべてのクラスター グループ (クラスターの役割) を確認する、[`Get-ClusterGroup`](https://technet.microsoft.com/library/ee461017.aspx)コマンドレット**  

    2.  すべてのクラスター ノードがオンラインでことを確認しを使用してを実行している、[`Get-ClusterNode`](https://technet.microsoft.com/library/ee460990.aspx)コマンドレット。  
    3.  実行、[`Update-ClusterFunctionalLevel`](https://technet.microsoft.com/library/mt589702.aspx)コマンドレットのエラーは返されません (図 19 を参照してください)。  

        ![Update-ClusterFunctionalLevel コマンドレットの出力を示す [screencap]](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_SelectFunctionalLevel.png)  
        **図 19: PowerShell を使用してクラスターの機能レベルを更新します。**  

    4.  後に、[`Update-ClusterFunctionalLevel`](https://technet.microsoft.com/library/mt589702.aspx)コマンドレットの実行、新しい機能を利用します。  

4. Windows Server 2016 では、通常のクラスター更新プログラムとバックアップを再開します。  

    1. CAU を実行していた以前場合、CAU UI を使用して再起動するかを使用して、[`Enable-CauClusterRole`](https://technet.microsoft.com/library/hh847229.aspx)コマンドレット (図 20 を参照してください)。  

        ![Enable-CauClusterRole の出力を示す [screencap]](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_EnableCAUClusterRole.png)  
        **図 20: 有効にするクラスター対応更新を使用して役割、[`Enable-CauClusterRole`](https://technet.microsoft.com/library/hh847229.aspx)コマンドレット**  

    2. バックアップ操作を再開します。  

5. 有効にして、Hyper-V 仮想マシンで Windows Server 2016 の機能を使用します。  

    1. クラスターが機能レベルが Windows Server 2016 にアップグレードされたら、Hyper-V Vm のような多くのワークロードは新しい機能があります。 Hyper-V の新機能の一覧です。 参照してください[移行およびアップグレードの仮想マシン](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/migrating_vms)  

    2. 各 Hyper-V ホスト クラスター内のノードを使用して、[`Get-VMHostSupportedVersion`](https://technet.microsoft.com/library/mt653838.aspx)コマンドレットをホストでサポートされている Hyper-V VM 構成バージョンを表示します。  

        ![Get-VMHostSupportedVersion コマンドレットの出力を示す [screencap]](media/Cluster-Operating-System-Rolling-Upgrade/Clustering_GetVMHostSupportVersion.png)  
        **図 21: は、ホストでサポートされている Hyper-V VM 構成バージョンを表示します。**  

   3.  ユーザーと、簡単なメンテナンス期間のスケジュール設定、バックアップ、仮想マシンをオフにするを実行して Hyper-V ホストの各ノードで、クラスター、Hyper-V VM 構成バージョンをアップグレードすることができます、[`Update-VMVersion`](https://technet.microsoft.com/library/mt484146.aspx)コマンドレット (図 22 を参照してください)。 仮想マシンのバージョンの更新プログラム、インストールされた Hyper-v の新機能、Hyper-V 統合コンポーネント (IC) の今後の更新の必要性を排除することを有効にします。 このコマンドレットは、仮想マシンをホストしている Hyper-V ノードから実行することができます、または`-ComputerName`パラメーターを使用して、VM バージョンをリモートで更新することです。 この例では次のとおりお VM1 の構成バージョンからアップグレード 5.0 7.0 に実稼働のチェックポイント (アプリケーション整合性のあるバックアップ) とバイナリの VM の構成ファイルなどのこの VM 構成バージョンに関連付けられている多くの新しい Hyper-V 機能を活用します。  

        ![[Screencap] アクションで Update-VMVersion コマンドレットを示す](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_StopVM.png)  
        **図 22: Update-VMVersion PowerShell コマンドレットを使用して VM バージョンをアップグレードします。**  

4.  使用して、記憶域プールをアップグレードすることができます、[Update-storagepool](https://technet.microsoft.com/itpro/powershell/windows/storage/update-storagepool) PowerShell コマンドレットのオンライン操作です。  

ただし、プライベート クラウドのシナリオ、具体的には Hyper-v ホストを対象としているし、すべてのクラスターの役割に使用できる対応するスケール アウト ファイル サーバー クラスターは、クラスター OS のローリング アップグレード プロセス、ダウンタイムなしでアップグレードすることができます。  

## <a name="restrictions--limitations"></a>制限/制限事項  
- この機能は、Windows Server 2012 R2 に Windows Server 2016 バージョンのみに対してのみ動作します。 この機能は、Windows Server 2016 に Windows Server 2008、Windows Server 2008 R2、または Windows Server 2012 などの Windows Server の以前のバージョンをアップグレードすることはできません。  
- Windows Server 2016 の各ノードには、再フォーマット/新規インストールのみをする必要があります。 「インプレース」または「アップグレード」インストールの種類はお勧めします。  
- Windows Server 2016 のノードは、ノードを追加する Windows Server 2016 をクラスターに使用する必要があります。  
- OS が混在モードのクラスターを管理するときに常に Windows Server 2016 を実行している上位レベル] ノードから管理タスクを実行します。 ダウンレベルの Windows Server 2012 R2 ノードは、Windows Server 2016 に対して UI または管理ツールを使用できません。  
- 顧客の OS が混在モードのクラスターの一部の機能に最適化されていないために、クラスターのアップグレードのプロセスをすばやく移動をお勧めします。  
- 作成またはクラスターの実行中の OS が混在モードで可能な非互換性のためフェールオーバーで Windows Server 2016 のノードからダウンレベルの Windows Server 2012 R2 のノードには、Windows Server 2016 のノード上の記憶域をサイズ変更しないでください。  

## <a name="frequently-asked-questions"></a>よく寄せられる質問  
**どのくらいの期間、フェールオーバー クラスターで実行できますの OS が混在モードですか。**  
    4 週間以内にアップグレードを完了する顧客をお勧めします。 Windows Server 2016 で多くの最適化があります。 お正常にアップグレードされた Hyper-V とスケール アウト ファイル サーバー クラスターの 4 時間より小さい合計でダウンタイムなしでします。  

**Windows Server 2012、Windows Server 2008 R2、または Windows Server 2008 に戻るには、この機能を移植するですか。**  
    以前のバージョンに戻すには、この機能を移植する予定はありません。 Windows Server 2016 には、Windows Server 2012 R2 のクラスターをアップグレードするための当社のビジョンはクラスター OS のローリング アップグレードです。  

**Windows Server 2012 R2 クラスターはクラスター OS のローリング アップグレード プロセスを開始する前にインストールされているすべてのソフトウェアの更新がある必要がありますか。**  
    はい、クラスター OS のローリング アップグレード プロセスを開始する前にすべてのクラスター ノードが最新のソフトウェアの更新に更新されたことを確認します。  

**実行することができます、[`Update-ClusterFunctionalLevel`](https://technet.microsoft.com/library/mt589702.aspx)コマンドレット ノードは無効になってまたは一時停止中ですか?**  
    違います。 すべてのクラスター ノードとでのメンバーシップをアクティブにする必要があります、[`Update-ClusterFunctionalLevel`](https://technet.microsoft.com/library/mt589702.aspx)コマンドレットを実行します。  

**クラスター OS のローリング アップグレードの動作のすべてのクラスター ワークロード SQL Server に対する動作しますか。**  
    はい、クラスター OS のローリング アップグレードは、すべてのクラスター ワークロードの動作します。 ただし、Hyper-V とスケール アウト ファイル サーバー クラスターにのみ、ダウンタイムがあります。 その他のほとんどのワークロードが発生するときにある程度のダウンタイム (通常、いくつかの分)、フェールオーバー、およびフェールオーバーが必要なクラスター OS のローリング アップグレード プロセス中に少なくとも 1 回です。  

**PowerShell を使用してこのプロセスを自動化することができますか。**  
    はい、OS のローリング クラスターを PowerShell を使用して自動化するアップグレード設計されています。  

**余分なワークロードとフェールオーバーの容量を持つ大規模なクラスターは複数のノード同時にアップグレードできますか。**  
    うん。 クラスター OS のアップグレードから 1 つのノードが削除されると、クラスター フェールオーバーの少ないノードが 1 つ、したがっては削減フェールオーバー容量。 十分なワークロードと容量のフェールオーバーで大規模なクラスターの複数のノードを同時にアップグレードできます。 クラスター OS のローリング アップグレード プロセス中に強化されたワークロードと容量のフェールオーバーを提供するクラスターへ、クラスター ノードを一時的に追加できます。  

**場合の対処を見つけるには、問題の後、クラスター内[`Update-ClusterFunctionalLevel`](https://technet.microsoft.com/library/mt589702.aspx)が正常に実行されたか?**  
    場合はするがバックアップ クラスター データベースに実行する前に、システム状態バックアップ[`Update-ClusterFunctionalLevel`](https://technet.microsoft.com/library/mt589702.aspx)、権限のあるを実行できる必要があります、Windows Server 2012 R2 のクラスター ノードに復元し、元のクラスター データベースと構成を復元します。  

**システム ドライブをフォーマットし、クリーンアップ OS のインストールを使用する代わりに、各ノードのインプレース アップグレードを使用できますか。**  
    Windows Server の一括アップグレードの使用をお勧めしませんは、既定のドライバーが使用されているいくつかの場合の動作に注意してください。 クラスタ ノードのインプレース アップグレード中にすべての警告メッセージが表示される慎重に参照してください。  

**場合は、Hyper-V クラスターでは、Hyper-V バーチャル マシンの Hyper-V レプリケーションを使用している、レプリケーションはそのまま残りますと、クラスター OS のローリング アップグレード プロセスの中にしますか。**  
    はいと、クラスター OS のローリング アップグレード プロセスの中には、Hyper-V レプリカはそのまま維持します。  

**System Center 2016 Virtual Machine Manager (SCVMM) を使用して、クラスター OS のローリング アップグレード プロセスを自動化するのにことができますか。**  
    はい、System Center 2016 で VMM を使用して、クラスター OS のローリング アップグレード プロセスを自動化できます。  

## <a name="see-also"></a>参照してください。  
-   [Windows Server 2016 での重要な問題のリリース ノートには:](../get-started/Release-Notes--Important-Issues-in-Windows-Server-2016-Technical-Preview.md)  
-   [Windows Server 2016 の新機能](../get-started/What-s-New-in-windows-server-2016.md)  
-   [Windows Server のフェールオーバー クラスタ リングの新機能](whats-new-in-failover-clustering.md)  