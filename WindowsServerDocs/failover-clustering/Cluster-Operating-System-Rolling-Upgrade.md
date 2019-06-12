---
title: Cluster Operating System Rolling Upgrade (クラスター オペレーティング システムのローリング アップグレード)
ms.prod: windows-server-threshold
ms.technology: storage-failover-clustering
ms.topic: get-started-article
ms.assetid: 6e102c1f-df26-4eaa-bc7a-d0d55d3b82d5
author: jasongerend
ms.author: jgerend
ms.date: 03/27/2018
ms.openlocfilehash: f56c036768de7c1afcf3327135a7ff7d7a690a8b
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440147"
---
# <a name="cluster-operating-system-rolling-upgrade"></a>クラスターのオペレーティング システムのローリング アップグレード

> 適用対象:Windows Server 2019、Windows Server 2016

クラスター OS のローリング アップグレードすると、管理者は、HYPER-V やスケール アウト ファイル サーバーのワークロードを停止することがなく、クラスター ノードのオペレーティング システムをアップグレードするができます。 この機能を使用すると、サービス レベル アグリーメント (SLA) でのダウンタイムに対するペナルティを回避できます。

クラスター OS のローリング アップグレードには、次の利点が提供されます。

- (クラスターのすべてのクラスター ノードで実行されている) Windows Server 2016 にはダウンタイムなしで HYPER-V 仮想マシンとスケール アウト ファイル サーバー (SOFS) のワークロードを実行しているフェールオーバー クラスターを (クラスター内のすべてのノードで実行されている) Windows Server 2012 R2 からアップグレードできます。 Windows Server 2016 へのフェールオーバーにかかる時間 (5 分未満通常) 中に、SQL Server など、他のクラスター ワークロードは使用できなきます。  
- その他のハードウェアは必要ありません。 さらに追加することができますが、クラスター ノード一時的に、クラスター OS のローリング アップグレード中に、クラスターの可用性を向上させるために小規模なクラスターを処理します。  
- クラスターを停止または再開する必要はありません。  
- 新しいクラスターには必要ありません。 既存のクラスターはアップグレードされます。 さらに、Active Directory に格納されている既存のクラスター オブジェクトが使用されます。  
- アップグレード プロセスは、Windows Server 2016 を実行している顧客伴いません、「ポイント-の-戻り値のない」、すべてのクラスター ノードとするまで、Update-clusterfunctionallevel PowerShell コマンドレットの実行時に元に戻すこと。  
- クラスターの OS が混在モードで実行中に修正プログラムの適用やメンテナンスの操作をサポートできます。  
- PowerShell および WMI を使用してオートメーションがサポートしています。  
- クラスターのパブリック プロパティ**ClusterFunctionalLevel**プロパティは、Windows Server 2016 のクラスター ノードでクラスターの状態を示します。 このプロパティは、フェールオーバー クラスターに属している Windows Server 2016 のクラスター ノードからの PowerShell コマンドレットを使用してクエリできます。  
    ```PowerShell
    Get-Cluster | Select ClusterFunctionalLevel  
    ```  

    値**8**クラスターが Windows Server 2012 R2 の機能レベルで実行されていることを示します。 値**9**クラスターが Windows Server 2016 の機能レベルで実行されていることを示します。  

このガイドでは、クラスター OS のローリング アップグレード プロセス、インストール手順、機能の制限、およびよく寄せられる質問 (Faq) のさまざまな段階について説明し、Windows Server 2016 で次のクラスター OS のローリング アップグレード シナリオに適用されます。  
- HYPER-V クラスター  
- スケール アウト ファイル サーバー クラスター  

Windows Server 2016 では、次のシナリオがサポートされていません。  
-  クラスターの共有記憶域として仮想ハード_ディスク (.vhdx ファイル) を使用してゲスト クラスターの OS のローリング アップグレード  

クラスター OS のローリング アップグレードすると、System Center Virtual Machine Manager (SCVMM) 2016 では完全にサポートします。 SCVMM 2016 を使用している場合は、次を参照してください。 [VMM で Windows Server 2016 に Hyper-v ホスト クラスターのローリング アップグレード実行](https://docs.microsoft.com/system-center/vmm/hyper-v-rolling-upgrade?view=sc-vmm-1807)ガイダンスについては、クラスターをアップグレードすると、このドキュメントで説明されている手順を自動化します。  

## <a name="requirements"></a>要件  
クラスター OS のローリング アップグレード プロセスを開始する前に、次の要件を完了します。

- Windows Server (半期チャネル)、Windows Server 2016 または Windows Server 2012 R2 を実行するフェールオーバー クラスターを起動します。
- Windows Server に記憶域スペース ダイレクト クラスターのアップグレード、バージョン 1709 がサポートされていません。
- クラスターのワークロードが HYPER-V Vm、またはスケール アウト ファイル サーバーの場合は、ダウンタイムのアップグレードを期待できます。
- HYPER-V ノードに 2 番目のレベルを示す表 (SLAT) を使用して、次のメソッドのいずれかをサポートする Cpu があることを確認します。  
        -確認、 [SLAT 対応ですか?WP8 SDK ヒント 01](http://blogs.msdn.com/b/devfish/archive/2012/11/06/are-you-slat-compatible-wp8-sdk-tip-01.aspx) CPU が SLATs をサポートしているかを確認する 2 つの方法を説明する記事  
        -ダウンロード、 [Coreinfo v3.31](https://technet.microsoft.com/sysinternals/cc835722) CPU が SLAT をサポートしているかを判断するためのツール。

## <a name="cluster-transition-states-during-cluster-os-rolling-upgrade"></a>クラスター OS のローリング アップグレード中にクラスターの状態の遷移

このセクションでは、クラスター OS のローリング アップグレードを使用して Windows Server 2016 にアップグレードされている Windows Server 2012 R2 クラスターのさまざまな遷移状態について説明します。  

Windows Server 2016 を Windows Server 2012 R2 ノードからクラスターのワークロードを移動、クラスター OS のローリング アップグレード プロセス中に実行されているクラスターのワークロードを維持するためには、ノードは、両方のノードは、Windows Server 2012 R2 オペレーティング システムを実行していた場合に機能します。 Windows Server 2016 のノードがクラスターに追加されると、Windows Server 2012 R2 の互換モードで動作します。 「の OS が混在モード」と呼ばれる、新しい概念クラスター モードにより、同じ内に存在する別のバージョンのノード クラスター (図 1 参照)。  

![クラスター OS のローリング アップグレードの 3 つのステージを示す図: Windows Server 2012 R2 のすべてのノードの OS が混在モードでは、Windows Server 2016 のすべてのノード](media/Cluster-Operating-System-Rolling-Upgrade/Clustering_RollingUpgrade_Overview.png)  
**図 1: クラスター オペレーティング システムの状態遷移**  

Windows Server 2012 R2 クラスターは、クラスターに追加されると、Windows Server 2016 のノードの OS が混在モードになります。 プロセスを完全に元に戻せる - Windows Server 2016 のノードは、クラスターから削除することができ、Windows Server 2012 R2 ノードは、このモードでクラスターに追加することができます。 Update-clusterfunctionallevel PowerShell コマンドレット、クラスターで実行しているときに、「戻すことができない」が発生します。 このコマンドレットを成功させるためには、すべてのノードは、Windows Server 2016 である必要があり、すべてのノードをオンラインにする必要があります。  

## <a name="transition-states-of-a-four-node-cluster-while-performing-rolling-os-upgrade"></a>OS のローリング アップグレードの実行中に、4 ノード クラスターの状態の遷移

このセクションを示していて、共有の記憶域ノードを持つは Windows Server 2012 R2 から Windows Server 2016 にアップグレードを含むクラスターの 4 つの異なる段階について説明します。  

「ステージ 1」は、初期の状態 - Windows Server 2012 R2 クラスターから始めます。  

![初期状態を示す図: Windows Server 2012 R2 のすべてのノード](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage1.png)  
**図 2:初期状態:Windows Server 2012 R2 フェールオーバー クラスター (ステージ 1)**  

「ステージ 2」、2 つのノードがされている一時停止、ドレイン、削除、再フォーマットされ、および Windows Server 2016 をインストールします。  

![OS が混在モードでクラスターを示す図例 4 ノード クラスターから 2 つのノードが、Windows Server 2016 では、を実行し、2 つのノードは、Windows Server 2012 R2 を実行している。](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage2.png)  
**図 3:中間の状態:OS が混在モード:Windows Server 2012 R2 および Windows Server 2016 フェールオーバー クラスター (ステージ 2)**  

「段階 3」、すべてのクラスターのノードが、Windows Server 2016 にアップグレードされ、クラスターが Update-clusterfunctionallevel PowerShell コマンドレットを使用したアップグレードの準備ができます。  

> [!NOTE]  
> この段階でプロセスを完全に切り替えることができます、および Windows Server 2012 R2 ノードは、このクラスターに追加することができます。  

![クラスターが Windows Server 2016 に完全にアップグレードされたクラスターの機能レベルを Windows Server 2016 までを Update-clusterfunctionallevel コマンドレットの準備がであることを示す図](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage3.png)  
**図 4:中間の状態:Windows Server 2016、Update-clusterfunctionallevel (ステージ 3) 対応にアップグレードするすべてのノード**  

Update ClusterFunctionalLevelcmdlet を実行すると、クラスターは「4 段階」、新しい Windows Server 2016 クラスターの機能を使用できる場所を入力します。  

![クラスターのローリング OS アップグレードが正常に完了したことを示す図すべてのノードが、Windows Server 2016 にアップグレードされ、クラスターが Windows Server 2016 クラスターの機能レベルで実行されています。](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage4.png)  
**図 5:最終的な状態:Windows Server 2016 フェールオーバー クラスター (ステージ 4)**  

## <a name="cluster-os-rolling-upgrade-process"></a>クラスター OS のローリング アップグレード プロセス

このセクションでは、クラスター OS のローリング アップグレードを実行するためのワークフローについて説明します。  

![クラスターのアップグレードのワークフローを示す図](media/Cluster-Operating-System-Rolling-Upgrade/Clustering_RollingUpgrade_Workflow.png)  
**図 6:クラスター OS のローリング アップグレード プロセスのワークフロー**  

クラスター OS のローリング アップグレードには、次の手順が含まれています。  

1. よう、オペレーティング システムのアップグレードのクラスターを準備します。  
    1. クラスター OS のローリング アップグレードするには、一度に 1 つのノードをクラスターから削除する必要があります。 オペレーティング システムのアップグレードのためにクラスターからクラスター ノードの 1 つが削除されると、高可用性 Sla を維持するためにクラスターに十分な容量があるかどうかを確認します。 クラスター OS のローリング アップグレードの処理中に 1 つのノードがクラスターから削除されたときに、別のノードにワークロードをフェールオーバーする機能が必要でしょうか。 つまり、 クラスターにクラスター OS のローリング アップグレードの 1 つのノードがクラスターから削除された場合に必要なワークロードを実行する容量があるでしょうか。  
    2. HYPER-V のワークロードでは、すべての Windows Server 2016 の HYPER-V ホストに CPU が Second-level Address テーブル (SLAT) のサポートがあることを確認します。 SLAT 対応のコンピューターだけでは、Windows Server 2016 で HYPER-V ロールを使用できます。  
    3. 確認、ワークロードのバックアップが完了したら、クラスターのバックアップを検討してください。 クラスターにノードを追加するときに、バックアップ操作を停止します。  
    4. すべてのクラスター ノードがオンラインであるかを確認/実行/アップを使用して、 [ `Get-ClusterNode` ](https://docs.microsoft.com/powershell/module/failoverclusters/Get-ClusterNode?view=win10-ps)コマンドレット (図 7 を参照してください)。  

        ![Get-clusternode コマンドレットを実行の結果を示すスクリーン ショット](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_GetClusterNode.png)  
        **図 7:Get-clusternode コマンドレットを使用してノードの状態を判断します。**  

    5. クラスター対応更新 (CAU) を実行している場合は、CAU を使用して現在実行されているかどうかことを確認、**クラスター Aware 更新**UI、または[ `Get-CauRun` ](https://docs.microsoft.com/powershell/module/clusterawareupdating/Get-CauRun?view=win10-ps)コマンドレット (図 8 参照)。 CAU の使用を停止、 [ `Disable-CauClusterRole` ](https://docs.microsoft.com/powershell/module/clusterawareupdating/Disable-CauClusterRole?view=win10-ps)コマンドレット (図 9 を参照してください) を使用して、すべてのノードの一時停止しているし、クラスター OS のローリング アップグレード プロセス中に、CAU をドレインしないようにします。  

        ![Get-caurun コマンドレットの出力を示すスクリーン ショット](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_GetCAU.png)  
        **図 8:使用して、 [ `Get-CauRun` ](https://docs.microsoft.com/powershell/module/clusterawareupdating/Get-CauRun?view=win10-ps)コマンドレットは、クラスターでクラスター対応更新が実行されているかどうかを判断するには**  

        ![Disable-cauclusterrole コマンドレットの出力を示すスクリーン ショット](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_DisableCAU.png)  
        **図 9:クラスター対応更新の役割を使用して、無効にすると、 [ `Disable-CauClusterRole` ](https://docs.microsoft.com/powershell/module/clusterawareupdating/Disable-CauClusterRole?view=win10-ps)コマンドレット**  

2. クラスターの各ノードでは、次のことを行います。  
    1. クラスター マネージャーの UI を使用して、ノードを選択し、使用して、**一時停止 |ドレイン**ノードをドレインするまでにメニュー オプション (図 10 参照) を使用して、または、 [ `Suspend-ClusterNode` ](https://docs.microsoft.com/powershell/module/failoverclusters/Suspend-ClusterNode?view=win10-ps)コマンドレット (図 11 を参照してください)。  

        ![クラスター マネージャーの UI を使用した役割のドレインを実行する方法を示すスクリーン ショット](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_FCM_DrainRoles.png)  
        **図 10:フェールオーバー クラスター マネージャーを使用してノードからの役割のドレイン**  

        ![Suspend-clusternode コマンドレットの出力を示すスクリーン ショット](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_SuspendNode.png)  
        **図 11:使用してノードからの役割をドレイン、 [ `Suspend-ClusterNode` ](https://docs.microsoft.com/powershell/module/failoverclusters/Suspend-ClusterNode?view=win10-ps)コマンドレット**  

    2.  クラスター マネージャーの UI を使用して**削除**からクラスター、または使用停止したノード、 [ `Remove-ClusterNode` ](https://docs.microsoft.com/powershell/module/failoverclusters/Remove-ClusterNode?view=win10-ps)コマンドレット。  

        ![クラスタ ノードの削除のコマンドレットの出力を示すスクリーン ショット](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_RemoveNode.png)  
        **図 12:使用して、クラスターからノードを削除[ `Remove-ClusterNode` ](https://docs.microsoft.com/powershell/module/failoverclusters/Remove-ClusterNode?view=win10-ps)コマンドレット**  

    3.  システム ドライブを再フォーマットしを使用して、ノードで Windows Server 2016 の「オペレーティング システムのクリーン インストール」を実行、**カスタム。Windows のインストールのみ (詳細)** setup.exe オプション インストール (図 13 を参照してください)。 選択しないで、**アップグレードします。Windows をインストールし、ファイル、設定、およびアプリケーション**インプレース アップグレードを推奨しないクラスター OS のローリング アップグレードのためのオプションします。  

        ![選択したカスタム インストール オプションを示す、Windows Server 2016 インストール ウィザードのスクリーン ショット](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_InstallOption.png)  
        **図 13:Windows Server 2016 の使用可能なインストール オプション**  

    4.  適切な Active Directory ドメインにノードを追加します。  
    5.  適切なユーザーを Administrators グループに追加します。  
    6.  サーバー マネージャーの UI または Install-windowsfeature PowerShell コマンドレットを使用して、HYPER-V などの必要があるサーバーの役割をインストールします。  

        ```PowerShell
        Install-WindowsFeature -Name Hyper-V  
        ```  

    7.  サーバー マネージャーの UI または Install-windowsfeature PowerShell コマンドレットを使用して、フェールオーバー クラスタ リング機能をインストールします。  

        ```PowerShell
        Install-WindowsFeature -Name Failover-Clustering  
        ```  

    8.  クラスターのワークロードで必要なその他の機能をインストールします。  
    9. フェールオーバー クラスター マネージャーの UI を使用してネットワークと記憶域の接続設定を確認します。  
    10. Windows ファイアウォールを使用する場合は、ファイアウォールの設定が、クラスターに対して正しいことを確認します。 たとえば、クラスター対応更新 (CAU) 有効になっているクラスターでは、ファイアウォールの構成を必要があります。  
    11. HYPER-V のワークロードでは、仮想スイッチ マネージャー ダイアログを起動する、HYPER-V マネージャーの UI を使用して、(図 14 を参照してください)。  

        使用される仮想スイッチの名前は、クラスター内のすべての HYPER-V ホスト ノードと同じことを確認します。  

        ![HYPER-V 仮想スイッチ マネージャー ダイアログ ボックスの場所を示すスクリーン ショット](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_VMSwitch.png)  
        **図 14:仮想スイッチ マネージャー**  

    12. Windows Server 2016 のノードに (Windows Server 2012 R2 ノードを使用しないで、)、フェールオーバー クラスター マネージャーを使用して (図 15 を参照してください) を使用してクラスターに接続します。  

        ![クラスターの選択 ダイアログを示すスクリーン ショット](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_AddNode.png)  
        **図 15:フェールオーバー クラスター マネージャーを使用してクラスターにノードを追加します。**  

    13. フェールオーバー クラスター マネージャーの UI を使用して、または[ `Add-ClusterNode` ](https://docs.microsoft.com/powershell/module/failoverclusters/Add-ClusterNode?view=win10-ps)コマンドレット (図 16 を参照してください) を使用して、クラスターにノードを追加します。  

        ![Add-clusternode コマンドレットの出力を示すスクリーン ショット](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_AddNode3.png)  
        **図 16:使用してクラスターにノードを追加する[ `Add-ClusterNode` ](https://docs.microsoft.com/powershell/module/failoverclusters/Add-ClusterNode?view=win10-ps)コマンドレット**  

        > [!NOTE]  
        > Windows Server 2016 の最初のノード クラスターに参加して、クラスターが"Mixed OS"モードでは、クラスター コア リソースは、Windows Server 2016 のノードに移動されます。 "混合 OS"モードのクラスターは、新しいノードが、古いノードとの互換モードで実行される完全に機能のクラスターです。 "混合 OS"モードは、クラスターの一時的なモードです。 永続的にするものではありませんし、顧客が 4 週間以内にクラスターのすべてのノードを更新する必要があります。  

    14. Windows Server 2016 の後にノードが正常にクラスターに追加、(必要に応じて) に移動できますクラスターのワークロードのいくつか新しく追加されたノード、クラスター間でワークロードを次のように再調整するには。

        ![Move-clustervirtualmachinerole コマンドレットの出力を示すスクリーン ショット](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_MoveVMRole.png)  
        **図 17:使用してクラスター ワークロード (クラスターの VM ロール) を移動[ `Move-ClusterVirtualMachineRole` ](https://docs.microsoft.com/powershell/module/failoverclusters/Move-ClusterVirtualMachineRole?view=win10-ps)コマンドレット**  

        1. 使用**ライブ マイグレーション**仮想マシンのフェールオーバー クラスター マネージャーから、または[ `Move-ClusterVirtualMachineRole` ](https://docs.microsoft.com/powershell/module/failoverclusters/Move-ClusterVirtualMachineRole?view=win10-ps)コマンドレット (図 17 を参照してください) を使用して仮想マシンのライブ マイグレーションを実行します。  

            ```PowerShell
            Move-ClusterVirtualMachineRole -Name VM1 -Node robhind-host3  
            ```  

        2. 使用**移動**からフェールオーバー クラスター マネージャーまたは[ `Move-ClusterGroup` ](https://docs.microsoft.com/powershell/module/failoverclusters/Move-ClusterGroup?view=win10-ps)他のクラスター ワークロード用のコマンドレット。  

3. すべてのノードを Windows Server 2016 にアップグレードされ、クラスターに追加されたときに、または残りの Windows Server 2012 R2 ノードが削除されたときに、次の操作を行います。  

    > [!IMPORTANT]  
    > -   クラスターの機能レベルを更新した後は、Windows Server 2012 R2 の機能レベルに戻ることはできませんし、Windows Server 2012 R2 ノードをクラスターに追加することはできません。
    > -   まで、 [ `Update-ClusterFunctionalLevel` ](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps)コマンドレットを実行、プロセスを完全に元に戻すことは、このクラスターに Windows Server 2012 R2 ノードを追加することができ、Windows Server 2016 ノードを削除することができます。  
    > -   後に、 [ `Update-ClusterFunctionalLevel` ](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps)コマンドレットの実行、新しい機能は使用できません。  

    1.  フェールオーバー クラスター マネージャーの UI を使用して、または[ `Get-ClusterGroup` ](https://docs.microsoft.com/powershell/module/failoverclusters/Get-ClusterGroup?view=win10-ps)コマンドレット、クラスターの役割のすべてが期待どおりに、クラスターで実行していることを確認します。 次の例では、使用可能記憶域が使用されていない、CSV を使用する代わりに、そのため、使用可能記憶域が表示されます、**オフライン**状態 (図 18 を参照してください)。  

        ![Get-clustergroup コマンドレットの出力を示すスクリーン ショット](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_GetClusterGroup.png)  
        **図 18:使用して実行しているすべてのクラスター グループ (クラスターの役割) の確認、 [ `Get-ClusterGroup` ](https://docs.microsoft.com/powershell/module/failoverclusters/Get-ClusterGroup?view=win10-ps)コマンドレット**  

    2.  すべてのクラスター ノードがオンラインであるかを確認しを実行して、 [ `Get-ClusterNode` ](https://docs.microsoft.com/powershell/module/failoverclusters/Get-ClusterNode?view=win10-ps)コマンドレット。  
    3.  実行、 [ `Update-ClusterFunctionalLevel` ](https://technet.microsoft.com/library/mt589702.aspx)コマンドレットのエラーは返されません (図 19 を参照してください)。  

        ![Update-clusterfunctionallevel コマンドレットの出力を示すスクリーン ショット](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_SelectFunctionalLevel.png)  
        **図 19:PowerShell を使用してクラスターの機能レベルを更新しています**  

    4.  後に、 [ `Update-ClusterFunctionalLevel` ](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps)コマンドレットを実行すると、新しい機能を利用します。  

4. Windows Server 2016 の通常のクラスターの更新プログラムとバックアップを再開します。  

    1. CAU を実行していたいた場合、CAU UI を使用して再起動またはを使用して、 [ `Enable-CauClusterRole` ](https://docs.microsoft.com/powershell/module/clusterawareupdating/Enable-CauClusterRole?view=win10-ps)コマンドレット (図 20 を参照してください)。  

        ![Enable-cauclusterrole の出力を示すスクリーン ショット](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_EnableCAUClusterRole.png)  
        **図 20:有効にするクラスター対応更新の役割を使用して、 [ `Enable-CauClusterRole` ](https://docs.microsoft.com/powershell/module/clusterawareupdating/Enable-CauClusterRole?view=win10-ps)コマンドレット**  

    2. バックアップ操作を再開します。  

5. 有効にして、HYPER-V 仮想マシンで Windows Server 2016 の機能を使用します。  

    1. クラスターを Windows Server 2016 の機能レベルにアップグレードした後、HYPER-V Vm のような多くのワークロードは新しい機能があります。 HYPER-V の新機能の一覧。 参照してください[移行およびアップグレードの仮想マシン](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/migrating_vms)  

    2. 各 HYPER-V ホストのノードでクラスターには、使用、 [ `Get-VMHostSupportedVersion` ](https://docs.microsoft.com/powershell/module/hyper-v/Get-VMHostSupportedVersion?view=win10-ps)ホストでサポートされている HYPER-V VM の構成バージョンを表示するコマンドレットです。  

        ![Get VMHostSupportedVersion コマンドレットの出力を示すスクリーン ショット](media/Cluster-Operating-System-Rolling-Upgrade/Clustering_GetVMHostSupportVersion.png)  
        **図 21:ホストでサポートされている HYPER-V VM の構成バージョンを表示します。**  

   3. 各 HYPER-V ホストのノードでクラスターには、ユーザーと簡単なメンテナンス期間のスケジュール設定、バックアップ、バーチャル マシンをオフにすると、および実行されているを HYPER-V VM の構成のバージョンをアップグレードできる、 [ `Update-VMVersion` ](https://docs.microsoft.com/powershell/module/hyper-v/Update-VMVersion?view=win10-ps)コマンドレット (を参照してください図 22)。 仮想マシンのバージョンに更新され、HYPER-V 統合コンポーネント (IC) の今後の更新する必要がなくなります、HYPER-V の新機能を有効にされます。 このコマンドレットは、VM をホストしている HYPER-V ノードから実行することができます、または`-ComputerName`パラメーターを使用して、VM バージョンをリモートで更新することです。 この例では、ここでバージョンにアップグレード構成 VM1 の 5.0 からこの VM 構成のバージョンなど、実稼働のチェックポイント (アプリケーション整合性バックアップ) とバイナリの VM に関連付けられている多くの新しい HYPER-V 機能を活用するために 7.0構成ファイルです。  

       ![アクションで更新 VMVersion コマンドレットを示すスクリーン ショット](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_StopVM.png)  
       **図 22:更新 VMVersion PowerShell コマンドレットを使用して VM のバージョンをアップグレードします。**  

6. 使用して記憶域プールをアップグレードすることができます、 [Update-storagepool](https://docs.microsoft.com/powershell/module/storage/Update-StoragePool?view=win10-ps) PowerShell コマンドレット - これはオンライン操作です。  

具体的には、HYPER-V プライベート クラウドのシナリオを対象としているし、任意のクラスター ロールのスケール アウト ファイル サーバー クラスターは、クラスター OS のローリング アップグレード プロセスのダウンタイムなくアップグレードできますを使用できます。  

## <a name="restrictions--limitations"></a>制限事項と制限事項  
- この機能は、Windows Server 2016 のバージョンのみを Windows Server 2012 R2 に対してのみ動作します。 この機能は、以前のバージョンの Windows Server 2008、Windows Server 2008 R2、または Windows Server 2012 など、Windows Server を Windows Server 2016 にアップグレードできません。  
- Windows Server 2016 の各ノードには、再フォーマット/新規インストールのみ必要があります。 「インプレース」または「アップグレード」インストールの種類はお勧めします。  
- Windows Server 2016 のノードは、Windows Server 2016 ノードをクラスターに追加するために使用する必要があります。  
- OS が混在モードのクラスターを管理するときに常に Windows Server 2016 を実行している上位レベル ノードから、管理タスクを実行します。 ダウンレベルの Windows Server 2012 R2 ノードには、Windows Server 2016 に対する UI または管理ツールを使用できません。  
- 顧客の OS が混在モードのクラスターの一部の機能が最適化されていないため、クラスターのアップグレードのプロセスをすばやく移動することをお勧めします。  
- 作成または実行中に、クラスターの OS が混在モードで可能な互換性がないのためフェールオーバー時に Windows Server 2016 のノードからダウンレベルの Windows Server 2012 R2 ノードを Windows Server 2016 のノード上の記憶域のサイズを変更しないでください。  

## <a name="frequently-asked-questions"></a>よく寄せられる質問  
**どれくらいの時間、フェールオーバー クラスターで実行できますの OS が混在モードか。**  
    お客様は 4 週間以内にアップグレードを完了することをお勧めします。 Windows Server 2016 でのさまざまな最適化があります。 HYPER-V が正常にアップグレードして、合計 4 時間未満でダウンタイムなしでクラスターのスケール アウト ファイル サーバー。  

**Windows Server 2012、Windows Server 2008 R2、または Windows Server 2008 には、この機能を移植しますか。**  
    以前のバージョンに戻すには、この機能を移植する計画はありません。 Windows Server 2016 以降、Windows Server 2012 R2 クラスターをアップグレードするためのビジョンは、クラスター OS のローリング アップグレードします。  

**Windows Server 2012 R2 クラスターは、クラスター OS のローリング アップグレード プロセスを開始する前にインストールされているすべてのソフトウェア更新プログラムがある必要がありますか。**  
    はい、クラスター OS のローリング アップグレード プロセスを開始する前に最新のソフトウェア更新プログラムすべてのクラスター ノードが更新されることを確認します。  

**実行することができます、 [ `Update-ClusterFunctionalLevel` ](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps)コマンドレット ノードがオフまたは一時停止中ですか?**  
    No. すべてのクラスター ノードとのメンバーシップがアクティブである必要があります、 [ `Update-ClusterFunctionalLevel` ](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps)コマンドレットを実行します。  

**クラスター OS のローリング アップグレードの機能のすべてのクラスター ワークロードについてSQL Server の機能**  
    はい、クラスター OS のローリング アップグレードでは、すべてのクラスター ワークロードに対して機能します。 ただし、HYPER-V とスケール アウト ファイル サーバー クラスターにのみ、ダウンタイムを勧めします。 その他のほとんどのワークロード ダウンタイムが発生するいくつか (通常は、いくつかの分単位) 場合、フェールオーバー、およびフェールオーバーが必要なクラスター OS のローリング アップグレード プロセス中に少なくとも 1 回です。  

**PowerShell を使用してこのプロセスを自動化できますか。**  
    はい、クラスター OS の PowerShell を使用して自動化するローリング アップグレード設計されています。  

**余分な作業負荷とフェールオーバーの容量を持つ大規模なクラスターは複数のノード同時にアップグレードできますか。**  
    [はい]。 OS をアップグレードするクラスターから 1 つのノードが削除されると、クラスターのフェールオーバー ノードが 1 つ減ります。 そこでが削減フェールオーバー容量。 十分なワークロードと容量のフェールオーバー クラスターが大きい場合、複数のノードを同時にアップグレードできます。 クラスター OS のローリング アップグレード プロセス中に、強化されたワークロードとフェールオーバーの容量を提供するクラスターにクラスター ノードを一時的に追加できます。  

**後にクラスターで問題を検出した場合[ `Update-ClusterFunctionalLevel` ](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps)が正常に実行されていますか?**  
    場合はするがバックアップされるクラスター データベースで実行する前に、システム状態バックアップ[ `Update-ClusterFunctionalLevel` ](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps)、権限のあるを実行できる必要があります Windows Server 2012 R2 のクラスター ノードに復元し、元のクラスターの復元データベースおよび構成します。  

**システム ドライブをフォーマットしクリーンアップ OS のインストールを使用する代わりに、各ノードのインプレース アップグレードを使用できますか。**  
    Windows Server のインプレース アップグレードの使用をお勧めできませんが、既定のドライバーが使用されているいくつかのケースで動作する認識しています。 クラスター ノードのインプレース アップグレード中にすべての警告メッセージが表示される注意深く読んでください。  

**場合は、HYPER-V クラスターで HYPER-V VM の HYPER-V レプリケーションを使っていますはレプリケーション、変更されると、クラスター OS のローリング アップグレード プロセスの中にしますか。**  
    はい、HYPER-V レプリカはままと、クラスター OS のローリング アップグレード プロセスの中に残ります。  

**System Center 2016 Virtual Machine Manager (SCVMM) を使用して、クラスター OS のローリング アップグレード プロセスを自動化するのにことができますか。**  
    はい、System Center 2016 で VMM を使用して、クラスター OS のローリング アップグレードのプロセスを自動化できます。  

## <a name="see-also"></a>関連項目  
-   [リリース ノート:Windows Server 2016 に関する重要な問題](../get-started/Release-Notes--Important-Issues-in-Windows-Server-2016-Technical-Preview.md)  
-   [Windows Server 2016 の新機能](../get-started/What-s-New-in-windows-server-2016.md)  
-   [新機能では、Windows Server フェールオーバー クラスタ リングの新機能](whats-new-in-failover-clustering.md)  
