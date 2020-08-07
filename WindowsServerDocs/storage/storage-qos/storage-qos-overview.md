---
title: 記憶域のサービスの品質 (QoS)
manager: dongill
ms.author: JGerend
ms.topic: get-started-article
ms.assetid: 8dcb8cf9-0e08-4fdd-9d7e-ec577ce8d8a0
author: kumudd
ms.date: 10/10/2016
ms.openlocfilehash: 0fd557341d19725a57c52d3786420c8c3357ebdf
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87963738"
---
# <a name="storage-quality-of-service"></a>記憶域のサービスの品質 (QoS)

> 適用先:Windows Server 2019、Windows Server 2016、Windows Server (半期チャネル)

Windows Server 2016 の記憶域のサービスの品質 (QoS) では、Hyper-V とスケールアウト ファイル サーバーの役割を使用して仮想マシンのために記憶域のパフォーマンスを一元的に監視および管理する方法を提供します。 この機能は、同一のファイル サーバー クラスターを使用している複数の仮想マシン間で記憶域リソースの公平性を自動的に向上させ、正規化された IOPS の単位でポリシー ベースの最小と最大のパフォーマンス目標を構成できるようにします。

Windows Server 2016 の記憶域 QoS を使用して、次の作業を実行できます。

-   **ノイズのある近隣ノードの問題を軽減します。** 既定では、記憶域 QoS によって、1 つの仮想マシンがすべての記憶域リソースを消費したり、他の仮想マシンのストレージ帯域幅が枯渇したりしないようにします。

-   **エンド ツー エンドの記憶域のパフォーマンスを監視します。** スケール アウト ファイル サーバーに格納されている仮想マシンが起動されるとすぐに、それらのパフォーマンスが監視されます。 すべての実行中の仮想マシンのパフォーマンスの詳細とスケールアウト ファイル サーバー クラスターの構成を 1 つの場所から表示できます。

-   **ワークロードのビジネス ニーズごとに記憶域 I/O を管理します。** 記憶域 QoS ポリシーは、仮想マシンの最低と最高のパフォーマンスを定義し、それらが満たされることを確認します。 これにより、高密度の過剰にプロビジョニングされた環境でも、仮想マシンの一貫したパフォーマンスを提供します。 ポリシーを満たすことができない場合は、警告を使用して、VM がポリシーを守れない状況または無効なポリシーが割り当てられた状況を追跡します。

このドキュメントでは、新しい記憶域 QoS 機能から企業がメリットを得る方法について説明します。 ここでは、Windows Server、Windows Server フェールオーバー クラスタリング、スケールアウト ファイル サーバー、Hyper-V、Windows PowerShell に関する実用的な知識があることを前提としています。

## <a name="overview"></a><a name="BKMK_Overview"></a>概要
このセクションでは、記憶域 QoS を使用するための要件、記憶域 QoS を使用するソフトウェア定義ソリューションの概要、および記憶域 QoS 関連の用語について説明します。

### <a name="storage-qos-requirements"></a><a name="BKMK_Requirements"></a>記憶域 QoS の要件
記憶域 QoS は、2 つの展開シナリオをサポートしています。

-   **スケールアウト ファイル サーバーを使用する Hyper-V** このシナリオには次の両方が必要です。

    -   スケール アウト ファイル サーバー クラスターである記憶域クラスター

    -   HYPER-V の役割が有効になっている少なくとも 1 つのサーバーが含まれる計算クラスター

    記憶域 QoS では、記憶域サーバー上にフェールオーバー クラスターが必要ですが、計算サーバーはフェールオーバー クラスターになる必要はありません。 すべてのサーバー (記憶域用と計算用の両方) で、Windows Server 2016 を実行している必要があります。

    評価を目的とするスケールアウト ファイル サーバーを展開していない場合は、既存のサーバーまたは仮想マシンを使用して構築するための手順について、「[Windows Server 2012 R2 Storage: Step-by-step with Storage Spaces, SMB Scale-Out and Shared VHDX (Physical)](/archive/blogs/josebda/windows-server-2012-r2-storage-step-by-step-with-storage-spaces-smb-scale-out-and-shared-vhdx-physical)」 (Windows Server 2012 R2 記憶域: 記憶域、SMB スケールアウトおよび共有 VHDX を使用した手順 (物理)) を参照してください。

-   **クラスター共有ボリュームを使用した Hyper-V。** このシナリオでは、次の両方のものが必要です。

    -   HYPER-V の役割が有効になっているコンピューティング クラスター

    -   クラスター共有ボリューム (CSV) を記憶域に使用した Hyper-V

フェールオーバー クラスターが必要です。 すべてのサーバーで、同じバージョンの Windows Server 2016 を実行している必要があります。

### <a name="using-storage-qos-in-a-software-defined-storage-solution"></a><a name="BKMK_SolutionOverview"></a>ソフトウェア定義記憶域ソリューションでの記憶域 QoS を使用
記憶域のサービス品質は、スケールアウト ファイル サーバーおよび Hyper-V によって提供されるマイクロソフトのソフトウェア定義記憶域ソリューションに組み込まれています。 スケールアウト ファイル サーバーは、SMB3 プロトコルを使用して Hyper-V サーバーにファイル共有を公開します。 中央でストレージのパフォーマンスを監視できる新しいポリシー マネージャーがファイル サーバー クラスターに追加されました。

![スケールアウト ファイル サーバーと記憶域 QoS](media/overview-Clustering_SOFSStorageQoS.png)

**図 1: スケールアウト ファイル サーバーのソフトウェア定義記憶域ソリューションでの記憶域 QoS の使用**

Hyper-V サーバーが仮想マシンを起動すると、それらはポリシー マネージャーによって監視されます。 ポリシー マネージャーは、記憶域 QoS ポリシーおよびすべての制限または予約を Hyper-V サーバーに伝達し、Hyper-V サーバーが仮想マシンのパフォーマンスを適切に制御します。

記憶域 QoS ポリシーまたは仮想マシンに必要なパフォーマンスが変化した場合、ポリシー マネージャーが Hyper-V サーバーに通知してそれらの動作を調整します。 このフィードバック ループにより、定義された記憶域 QoS ポリシーに従って、すべての仮想マシンの VHD が継続的に実行されます。

### <a name="glossary"></a><a name="BKMK_Glossary"></a>用語集

|期間|説明|
|--------|---------------|
|正規化された IOPS|すべての記憶域の使用状況は、”正規化された IOPS” で測定されます。  これは、1 秒あたりの記憶域の入出力操作の数です。  8 KB 以下の IO はすべて 1 つの正規化された IO と見なされます。  8 KB より大きいすべての IO は、複数の正規化された IO と見なされます。 たとえば、256 KB の要求は、32 の正規化された IOPS として扱われます。<p>Windows Server 2016 には、IO を正規化するために使用するサイズを指定する機能が含まれています。  記憶域クラスター上で、正規化されたサイズを指定し、クラスター全体の正規化の計算に適用することができます。  既定値は、8 KB のままです。|
|Flow|VHD または VHDX ファイルに対して Hyper-V サーバーによって開かれる各ファイル ハンドルは ”フロー” と見なされます。 仮想マシンに 2 台の仮想ハードディスクが接続されている場合、ファイルごとに 1 つのファイル サーバー クラスターへのフローがあります。 VHDX が複数の仮想マシンで共有されている場合、仮想マシンごとに 1 つのフローがあります。|
|InitiatorName|各フローに対応するスケール アウト ファイル サーバーに報告されている仮想マシンの名前です。|
|InitiatorID|仮想マシンの ID と一致する識別子。  仮想マシンに同じ InitiatorName が指定されている場合でも、これを使用して常に個別のフローの仮想マシンを一意に識別することができます。|
|ポリシー|記憶域 QoS ポリシーは、クラスター データベースに保存され、PolicyId、MinimumIOPS、MaximumIOPS、ParentPolicy、PolicyType というプロパティがあります。|
|PolicyId|ポリシーの一意の識別子。  既定で生成されますが、必要に応じて指定できます。|
|MinimumIOPS|ポリシーによって提供される最小の正規化された IOPS。  ”予約” とも呼ばれます。|
|MaximumIOPS|ポリシーによって提供される最大の正規化された IOPS。  ”制限” とも呼ばれます。|
|Aggregated |指定された MinimumIOPS、MaximumIOPS、および帯域幅は、ポリシーに割り当てられたすべてのフローで共有されます。 ストレージ システムにポリシーが割り当てられたすべての VHD には、全体で共有する 1 つの I/O 帯域幅が割り当てられています。|
|専用|指定された Minimum およびMaximumIOPs と帯域幅が個別の VHD/VHDx に対して管理されるポリシーの種類。|

## <a name="how-to-set-up-storage-qos-and-monitor-basic-performance"></a><a name="BKMK_SetUpQoS"></a>記憶域 QoS とモニターの基本的なパフォーマンスを設定する方法
このセクションでは、新しい記憶域 QoS を有効にする方法およびカスタム ポリシーを適用せずにストレージの記憶域のパフォーマンスを監視する方法について説明します。

### <a name="set-up-storage-qos-on-a-storage-cluster"></a><a name="BKMK_SetupStorageQoSonStorageCluster"></a>記憶域クラスターに記憶域 QoS を設定する
このセクションでは、Windows Server 2016 を実行している新規または既存のフェールオーバー クラスターおよびスケールアウト ファイル サーバー上で記憶域 QoS を有効にする方法について説明します。

#### <a name="set-up-storage-qos-on-a-new-installation"></a>新しいインストール上で記憶域 QoS を設定する
新しいフェールオーバー クラスターが構成済みであり、Windows Server 2016 上でクラスターの共有ボリューム (CSV) を構成した場合、記憶域 QoS 機能は自動的に設定されます。

#### <a name="verify-storage-qos-installation"></a>記憶域 QoS のインストールを確認する
フェールオーバー クラスターを作成し、CSV ディスクを構成した後で、**記憶域 QoS リソースが**クラスター コア リソースとして表示され、フェールオーバー クラスター マネージャーおよび Windows PowerShell の両方に表示されます。 これは、フェールオーバー クラスター システムでこのリソースを管理することを目的としており、このリソースに対してユーザーが何か操作を実行する必要はありません。  フェールオーバー クラスター マネージャーと PowerShell の両方に表示されるのは、新しいヘルス サービスなどの他のフェールオーバー クラスター システム リソースとの一貫性を維持するためです。

![クラスター コア リソース内に表示される記憶域 QoS リソース](media/overview-Clustering_StorageQoSFCM.png)

**図 2： フェールオーバー クラスター マネージャーにクラスター コア リソースとして表示された記憶域 QoS リソース**

記憶域 QoS リソースのステータスを表示するには、以下の PowerShell コマンドレットを使用します。

```PowerShell
PS C:\> Get-ClusterResource -Name "Storage Qos Resource"

Name                   State      OwnerGroup        ResourceType
----                   -----      ----------        ------------
Storage Qos Resource   Online     Cluster Group     Storage QoS Policy Manager
```

### <a name="set-up-storage-qos-on-a-compute-cluster"></a><a name="BKMK_SetupStorageQoSonComputeCluster"></a>コンピューティング クラスターに記憶域 QoS を設定する
Windows Server 2016 の Hyper-V の役割には、記憶域 QoS のサポートが組み込まれており、既定で有効化されます。

#### <a name="install-remote-administration-tools-to-manage-storage-qos-policies-from-remote-computers"></a>リモート コンピューターから記憶域 QoS ポリシーを管理するためのリモート管理ツールをインストールする
リモート サーバー管理ツールを使用して、記憶域 QoS ポリシーを管理し、コンピューティング ホストからのフローを監視することができます。  これらは、すべての Windows Server 2016 のインストールでオプション機能として使用することができ、[Microsoft ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=45520) Web サイトで Windows 10 用に個別にダウンロードできます。

**RSAT-Clustering** オプション機能には、記憶域 QoS を含むフェールオーバー クラスタリングをリモートで管理するための Windows PowerShell モジュールが含まれています。

-   Windows PowerShell: Add-WindowsFeature RSAT-Clustering

**RSAT-Hyper-V-Tools** オプション機能には、Hyper-V をリモートで管理するための Windows PowerShell モジュールが含まれています。

-   Windows PowerShell: Add-WindowsFeature RSAT-Hyper-V-Tools

#### <a name="deploy-virtual-machines-to-run-workloads-for-testing"></a>テスト用ワークロードを実行するための仮想マシンを展開する
適切なワークロードと共にいくつかの仮想マシンをスケールアウト ファイル サーバー上に保存する必要があります。  負荷のシミュレーションをおよびいくつかのストレス テストの実行方法のヒントについては、推奨されるツール (DiskSpd) のページおよびいくつかの使用例「[DiskSpd, PowerShell and storage performance: measuring IOPs, throughput and latency for both local disks and SMB file shares](/archive/blogs/josebda/diskspd-powershell-and-storage-performance-measuring-iops-throughput-and-latency-for-both-local-disks-and-smb-file-shares)」(DiskSpd、PowerShell、および記憶域のパフォーマンス: ローカル ディスクと SMB ファイル共有の両方の IOPS、スループット、および待機時間の測定) を参照してください。

このガイドに表示されるシナリオの例には、5 つの仮想マシンが含まれています。 BuildVM1、BuildVM2、BuildVM3、BuildVM4 は、低から中程度の記憶域の需要でデスクトップのワークロードを実行しています。 TestVm1 は、最も大きな記憶域の需要でオンライン トランザクション処理ベンチマークを実行しています。

### <a name="view-current-storage-performance-metrics"></a>現在のパフォーマンス メトリックを表示する
ここでは、以下の内容について説明します。

-   `Get-StorageQosFlow` コマンドレットを使用したフローのクエリ方法。

-   `Get-StorageQosVolume` コマンドレットを使用したボリュームのパフォーマンスの表示方法。

#### <a name="query-flows-using-the-get-storageqosflow-cmdlet"></a>Get-StorageQosFlow コマンドレットを使用したクエリ フロー

Get StorageQosFlow コマンドレットは、HYPER-V サーバーによって開始されたすべての現在のフローを示しています。 すべてのデータはスケールアウト ファイル サーバー クラスターによって収集されるので、スケールアウト ファイル サーバー クラスター内の任意のノードでこのコマンドレットを使用できます。または、-CimSession パラメーターを使用してリモート サーバーに対して使用することもできます。

**次のサンプル コマンドは、Get-StorageQoSFlow を使用してサーバー上で Hyper-V によって開かれたすべてのファイルを表示する方法を示しています**。

```PowerShell
PS C:\> Get-StorageQosFlow

InitiatorName    InitiatorNodeNam StorageNodeName  FilePath        Status
                 e
-------------    ---------------- ---------------  --------        ------
                                  plang-fs3.pla... C:\ClusterSt... Ok
                                  plang-fs2.pla... C:\ClusterSt... Ok
                                  plang-fs1.pla... C:\ClusterSt... Ok
                                  plang-fs3.pla... C:\ClusterSt... Ok
                                  plang-fs2.pla... C:\ClusterSt... Ok
                                  plang-fs1.pla... C:\ClusterSt... Ok
TR20-VMM         plang-z400.pl... plang-fs1.pla... C:\ClusterSt... Ok
BuildVM4         plang-c2.plan... plang-fs1.pla... C:\ClusterSt... Ok
WinOltp1         plang-c1.plan... plang-fs1.pla... C:\ClusterSt... Ok
BuildVM3         plang-c2.plan... plang-fs1.pla... C:\ClusterSt... Ok
BuildVM1         plang-c2.plan... plang-fs1.pla... C:\ClusterSt... Ok
TR20-VMM         plang-z400.pl... plang-fs1.pla... C:\ClusterSt... Ok
BuildVM2         plang-c2.plan... plang-fs1.pla... C:\ClusterSt... Ok
TR20-VMM         plang-z400.pl... plang-fs1.pla... C:\ClusterSt... Ok
                                  plang-fs3.pla... C:\ClusterSt... Ok
                                  plang-fs2.pla... C:\ClusterSt... Ok
BuildVM4         plang-c2.plan... plang-fs2.pla... C:\ClusterSt... Ok
WinOltp1         plang-c1.plan... plang-fs2.pla... C:\ClusterSt... Ok
BuildVM3         plang-c2.plan... plang-fs2.pla... C:\ClusterSt... Ok
WinOltp1         plang-c1.plan... plang-fs2.pla... C:\ClusterSt... Ok
                                  plang-fs1.pla... C:\ClusterSt... Ok
```

次のサンプル コマンドは、IOPS で並べ替えられた仮想マシン名、Hyper-V ホスト名、IOPS、および VHD ファイル名を表示するように書式設定されます。

```PowerShell
PS C:\> Get-StorageQosFlow | Sort-Object StorageNodeIOPs -Descending | ft InitiatorName, @{Expression={$_.InitiatorNodeName.Substring(0,$_.InitiatorNodeName.IndexOf('.'))};Label="InitiatorNodeName"}, StorageNodeIOPs, Status, @{Expression={$_.FilePath.Substring($_.FilePath.LastIndexOf('\')+1)};Label="File"} -AutoSize

InitiatorName InitiatorNodeName StorageNodeIOPs Status File
------------- ----------------- --------------- ------ ----
WinOltp1      plang-c1                     3482     Ok IOMETER.VHDX
BuildVM2      plang-c2                      544     Ok BUILDVM2.VHDX
BuildVM1      plang-c2                      497     Ok BUILDVM1.VHDX
BuildVM4      plang-c2                      316     Ok BUILDVM4.VHDX
BuildVM3      plang-c2                      296     Ok BUILDVM3.VHDX
BuildVM4      plang-c2                      195     Ok WIN8RTM_ENTERPRISE_VL_BU...
TR20-VMM      plang-z400                    156     Ok DATA1.VHDX
BuildVM3      plang-c2                       81     Ok WIN8RTM_ENTERPRISE_VL_BU...
WinOltp1      plang-c1                       65     Ok BOOT.VHDX
                                             18     Ok DefaultFlow
                                             12     Ok DefaultFlow
WinOltp1      plang-c1                        4     Ok 9914.0.AMD64FRE.WINMAIN....
TR20-VMM      plang-z400                      4     Ok DATA2.VHDX
TR20-VMM      plang-z400                      3     Ok BOOT.VHDX
                                              0     Ok DefaultFlow
                                              0     Ok DefaultFlow
                                              0     Ok DefaultFlow
                                              0     Ok DefaultFlow
                                              0     Ok DefaultFlow
                                              0     Ok DefaultFlow
                                              0     Ok DefaultFlow
```

次のサンプル コマンドは、InitiatorName を基にしてフローをフィルター処理し、特定の仮想マシンの記憶域のパフォーマンスと設定を簡単に見つける方法を示しています。

```PowerShell
PS C:\> Get-StorageQosFlow -InitiatorName BuildVm1 | Format-List

FilePath           : C:\ClusterStorage\Volume2\SHARES\TWO\BUILDWORKLOAD\BUILDVM1.V
                     HDX
FlowId             : ebfecb54-e47a-5a2d-8ec0-0940994ff21c
InitiatorId        : ae4e3dd0-3bde-42ef-b035-9064309e6fec
InitiatorIOPS      : 464
InitiatorLatency   : 26.2684
InitiatorName      : BuildVM1
InitiatorNodeName  : plang-c2.plang.nttest.microsoft.com
Interval           : 300000
Limit              : 500
PolicyId           : b145e63a-3c9e-48a8-87f8-1dfc2abfe5f4
Reservation        : 500
Status             : Ok
StorageNodeIOPS    : 475
StorageNodeLatency : 7.9725
StorageNodeName    : plang-fs1.plang.nttest.microsoft.com
TimeStamp          : 2/12/2015 2:58:49 PM
VolumeId           : 4d91fc3a-1a1e-4917-86f6-54853b2a6787
PSComputerName     :
MaximumIops        : 500
MinimumIops        : 500
```

`Get-StorageQosFlow` コマンドレットによって次のようなデータが返されます。

-   Hyper-V ホスト名 (InitiatorNodeName)。

-   仮想マシンの名前と ID (InitiatorName と InitiatorId)

-   Hyper-V ホストによって観測された最近の仮想ディスクの平均パフォーマンス (InitiatorIOPS、InitiatorLatency)

-   仮想ディスクの記憶域クラスターによって観測された最新の平均パフォーマンス (StorageNodeIOPS、StorageNodeLatency)

-   ファイルに適用されている現在のポリシー (存在する場合)、および結果の構成 (PolicyId、Reservation、Limit)

-   ポリシーの状態

    -   **Ok** - 問題はありません。

    -   InsufficientThroughput - ポリシーが適用されていますが、Minimum IOPS を提供できません。  この状況は、VM の最小値、またはすべての VM を合わせた最小値が、記憶域ボリュームが提供できる値を超えている場合に発生することがあります。

    -   **UnknownPolicyId** - Hyper-V ホスト上の仮想マシンにポリシーが割り当てられていますが、ファイル サーバーにはありません。  このポリシーを仮想マシンの構成から削除するか、ファイル サーバー クラスター上に一致するポリシーを作成する必要があります。

#### <a name="view-performance-for-a-volume-using-get-storageqosvolume"></a>Get-StorageQosVolume を使用してボリュームのパフォーマンスを表示する
記憶域のパフォーマンス メトリックは、フローごとのパフォーマンス メトリックに加えて、記憶域ボリューム レベルでも収集されます。  これにより、正規化された IOPS、待機時間、ボリュームに適用された合計制限および予約の合計平均使用率を簡単に表示できます。

```PowerShell
PS C:\> Get-StorageQosVolume | Format-List

Interval       : 300000
IOPS           : 0
Latency        : 0
Limit          : 0
Reservation    : 0
Status         : Ok
TimeStamp      : 2/12/2015 2:59:38 PM
VolumeId       : 434f561f-88ae-46c0-a152-8c6641561504
PSComputerName :
MaximumIops    : 0
MinimumIops    : 0

Interval       : 300000
IOPS           : 1097
Latency        : 3.1524
Limit          : 0
Reservation    : 1568
Status         : Ok
TimeStamp      : 2/12/2015 2:59:38 PM
VolumeId       : 4d91fc3a-1a1e-4917-86f6-54853b2a6787
PSComputerName :
MaximumIops    : 0
MinimumIops    : 1568

Interval       : 300000
IOPS           : 5354
Latency        : 6.5084
Limit          : 0
Reservation    : 781
Status         : Ok
TimeStamp      : 2/12/2015 2:59:38 PM
VolumeId       : 0d2fd367-8d74-4146-9934-306726913dda
PSComputerName :
MaximumIops    : 0
MinimumIops    : 781
```

## <a name="how-to-create-and-monitor-storage-qos-policies"></a><a name="BKMK_CreateQoSPolicies"></a>記憶域 QoS ポリシーの作成および監視方法
このセクションでは、記憶域 QoS ポリシーを作成し、それらのポリシーを仮想マシンに適用して、ポリシー適用後の記憶域クラスターを監視する方法について説明します。

### <a name="create-storage-qos-policies"></a>記憶域 QoS ポリシーを作成する
記憶域 QoS ポリシーは、スケールアウト ファイル サーバー クラスターで定義および管理されます。  展開の柔軟性を高めるために必要な数 (記憶域クラスターあたり最大 10,000) のポリシーを作成できます。

仮想マシンに割り当てられる各 VHD/VHDX ファイルを、ポリシーを使用して構成することができます。 異なるファイルや仮想マシンで同じポリシーを使用することも、個別のポリシーを使用してそれぞれを構成することもできます。  複数の VHD/VHDX ファイルまたは複数の仮想マシンが、同じポリシーを使用して構成されている場合、それらは一緒に集計され、MinimumIOPS と MaximumIOPS を均等に共有します。 複数の VHD/VHDX ファイルまたは仮想マシンで個別のポリシーを使用する場合、最小値と最大値はそれぞれ個別に追跡されます。

異なる仮想マシン用に複数の類似したポリシーを作成し、仮想マシンの記憶域の需要が同等である場合、それらは同等の IOPS の共有を割り当てられます。  1 つの VM の需要が他の VM より多い場合、IOPS は、その需要に従います。

### <a name="types-of-storage-qos-policies"></a>記憶域 QoS ポリシーの種類
Aggregated (以前の SingleInstance) と Dedicated (以前の MultiInstance) という 2 種類のポリシーがあります。 Aggregated ポリシーは、適用対象者 VHD/VHDX ファイルと仮想マシンを組み合わせたセットの最大値と最小値を適用します。 実際には、指定された IOPS と帯域幅のセットを共有します。 Dedicated ポリシーは、各 VHD/VHDx の最小値と最大値を個別に適用します。 これにより、類似した制限を複数の VHD/VHDx ファイルに適用する単一のポリシーを簡単に作成できます。

たとえば、最小値が 300 IOPS で最大値が 500 IOPS の Aggregated ポリシーを作成するとします。 このポリシーを 5 つの異なる VHD/VHDx ファイルに適用する場合、5 つの VHD/VHDx ファイルの合計が、300 IOPS (需要があり、記憶域システムがそのパフォーマンスを提供できる場合) 以上で 500 IOPS 未満であることが保証されるかどうかを確認します。 VHD/VHDx ファイルの IOPS の需要が同程度で、記憶域システムがそれを提供できる場合、各 VHD/VHDx ファイルは約 100 IOPS を取得します。

ただし、類似した制限を持つ Dedicated ポリシーを作成し、それを 5 つの異なる仮想マシン上の VHD/VHDx ファイルに適用した場合、各仮想マシンは 300 IOPS 以上 500 IOPS 未満を取得します。 仮想マシンに同程度の IOPS の高い需要があり、記憶域システムがそれを提供できる場合、各仮想マシンは、約 500 IOPS を取得します。 .  いずれかの仮想マシンに、同じ MulitInstance ポリシーが構成された複数の VHD/VHDx ファイルがある場合、それらは、VM のそのポリシーが適用されたファイルからの合計 IO が、制限を超えないように制限を共有します。

そのため、同じパフォーマンス特性を示すようにしたい VHD/VHDx ファイルのグループがあり、複数の類似したポリシーを作成するという問題を回避したい場合、単一の Dedicated ポリシーを作成し、各仮想マシンのファイルに適用することができます。

1つの集約されたポリシーに割り当てられた VHD/VHDx ファイルの数を20以下にします。  このポリシーの種類は、クラスター上のいくつかの Vm で集計を行うことを目的としていました。

### <a name="create-and-apply-a-dedicated-policy"></a>Dedicated ポリシーを作成して適用する
最初に次の例に示すように、`New-StorageQosPolicy` コマンドレットを使用して、スケールアウト ファイル サーバー上にポリシーを作成します。

```PowerShell
$desktopVmPolicy = New-StorageQosPolicy -Name Desktop -PolicyType Dedicated -MinimumIops 100 -MaximumIops 200
```

次に、Hyper-V サーバー上の適切な仮想マシンのハード ディスク ドライブにそれを適用します。  前の手順の PolicyId をメモするか、スクリプトの変数に保存します。

次の例に示すように、スケールアウト ファイル サーバー上で PowerShell を使用して、記憶域 QoS ポリシーを作成し、ポリシー ID を取得します。

```PowerShell
PS C:\> $desktopVmPolicy = New-StorageQosPolicy -Name Desktop -PolicyType Dedicated -MinimumIops 100 -MaximumIops 200

C:\> $desktopVmPolicy.PolicyId

Guid
----
cd6e6b87-fb13-492b-9103-41c6f631f8e0
```

次の例に示すように、Hyper-V サーバー上で PowerShell を使用し、ポリシー ID を使用して記憶域 QoS ポリシーを設定します。

```PowerShell
Get-VM -Name Build* | Get-VMHardDiskDrive | Set-VMHardDiskDrive -QoSPolicyID cd6e6b87-fb13-492b-9103-41c6f631f8e0
```

### <a name="confirm-that-the-policies-are-applied"></a>ポリシーが適用されていることを確認します。
次の例に示すように、`Get-StorageQosFlow` PowerShell コマンドレットを使用して、MinimumIOPs と MaximumIOPs が適切なフローに適用されていることを確認します。

```PowerShell
PS C:\> Get-StorageQoSflow | Sort-Object InitiatorName |
 ft InitiatorName, Status, MinimumIOPs, MaximumIOPs, StorageNodeIOPs, Status, @{Expression={$_.FilePath.Substring($_.FilePath.LastIndexOf('\')+1)};Label="File"} -AutoSize

InitiatorName Status MinimumIops MaximumIops StorageNodeIOPs Status File
------------- ------ ----------- ----------- --------------- ------ ----
BuildVM1          Ok         100         200             250     Ok BUILDVM1.VHDX
BuildVM2          Ok         100         200             251     Ok BUILDVM2.VHDX
BuildVM3          Ok         100         200             252     Ok BUILDVM3.VHDX
BuildVM4          Ok         100         200             233     Ok BUILDVM4.VHDX
TR20-VMM          Ok          33         666               1     Ok DATA2.VHDX
TR20-VMM          Ok          33         666               5     Ok DATA1.VHDX
TR20-VMM          Ok          33         666               4     Ok BOOT.VHDX
WinOltp1          Ok           0           0               0     Ok 9914.0.AMD6...
WinOltp1          Ok           0           0            5166     Ok IOMETER.VHDX
WinOltp1          Ok           0           0               0     Ok BOOT.VHDX
```

Hyper-V サーバー上で、提供されたスクリプト **Get-VMHardDiskDrivePolicy.ps1** を使用して、仮想ハード ディスク ドライブにどのポリシーが適用されるか確認します。

```PowerShell
PS C:\> Get-VM -Name BuildVM1 | Get-VMHardDiskDrive | Format-List

Path                          : \\plang-fs.plang.nttest.microsoft.com\two\BuildWorkload
                                \BuildVM1.vhdx
DiskNumber                    :
MaximumIOPS                   : 0
MinimumIOPS                   : 0
QoSPolicyID                   : cd6e6b87-fb13-492b-9103-41c6f631f8e0
SupportPersistentReservations : False
ControllerLocation            : 0
ControllerNumber              : 0
ControllerType                : IDE
PoolName                      : Primordial
Name                          : Hard Drive
Id                            : Microsoft:AE4E3DD0-3BDE-42EF-B035-9064309E6FEC\83F8638B
                                -8DCA-4152-9EDA-2CA8B33039B4\0\0\D
VMId                          : ae4e3dd0-3bde-42ef-b035-9064309e6fec
VMName                        : BuildVM1
VMSnapshotId                  : 00000000-0000-0000-0000-000000000000
VMSnapshotName                :
ComputerName                  : PLANG-C2
IsDeleted                     : False
```

### <a name="query-for-storage-qos-policies"></a>記憶域 QoS ポリシーのクエリ
`Get-StorageQosPolicy`構成されているすべてのポリシーとその状態をスケールアウトファイルサーバーに一覧表示します。

```PowerShell
PS C:\> Get-StorageQosPolicy

Name                 MinimumIops          MaximumIops          Status
----                 -----------          -----------          ------
Default              0                    0                    Ok
Limit500             0                    500                  Ok
SilverVm             500                  500                  Ok
Desktop              100                  200                  Ok
Limit500             0                    0                    Ok
VMM                  100                  2000                 Ok
Vdi                  1                    100                  Ok
```

システムのパフォーマンスの状況に応じて、ステータスは時間の経過と共に変化することがあります。

-   **Ok** - そのポリシーを使用しているすべてのフローが、要求された MinimumIOPs を受け取っています。

-   **InsufficientThroughput** - このポリシーを使用している 1 つ以上のフローが Minimum IOPs を受け取っていません。

次のように、パイプを使用してポリシーを `Get-StorageQosPolicy` に渡し、ポリシーを使用するように構成されているすべてのフローのステータスを取得することもできます。

```PowerShell
PS C:\> Get-StorageQosPolicy -Name Desktop | Get-StorageQosFlow | ft InitiatorName, *IOPS, Status, FilePath -AutoSize

InitiatorName MaximumIops MinimumIops InitiatorIOPS StorageNodeIOPS Status FilePat
                                                                           h
------------- ----------- ----------- ------------- --------------- ------ -------
BuildVM4              100          50           187              17     Ok C:\C...
BuildVM3              100          50           194              25     Ok C:\C...
BuildVM1              200         100           195             196     Ok C:\C...
BuildVM2              200         100           193             192     Ok C:\C...
BuildVM4              200         100           187             169     Ok C:\C...
BuildVM3              200         100           194             169     Ok C:\C...
```

### <a name="create-an-aggregated-policy"></a>Aggregated ポリシーを作成する
複数の仮想ハード ディスクで IOPS および帯域幅の 1 つのプールを共有する場合、Aggregated ポリシーを使用できます。  たとえば、同じ Aggregated ポリシーを、2 つの仮想マシンのハード ディスクに適用する場合、最小値は、需要に従ってそれらの間で分割されます。  両方のディスクが、組み合わせた最小値を保証され、それらの合計は、指定された最大 IOPS または帯域幅を超えません。

同じアプローチを使用して、サービスを構成している仮想マシンまたはマルチホスト環境内のテナントに属している仮想マシンのすべての VHD/VHDx ファイルに 1 つの割り当てを提供することもできます。

指定される PolicyType を除いて、Dedicated ポリシーと Aggregated ポリシーの作成プロセスに違いはありません。

次の例は、スケールアウト ファイル サーバー上で Aggregated 記憶域 QoS ポリシーを作成し、policyID を取得する方法を示しています。

```PowerShell
PS C:\> $highPerf = New-StorageQosPolicy -Name SqlWorkload -MinimumIops 1000 -MaximumIops 5000 -PolicyType Aggregated
[plang-fs]: PS C:\Users\plang\Documents> $highPerf.PolicyId

Guid
----
7e2f3e73-1ae4-4710-8219-0769a4aba072
```

次の例は、Hyper-V サーバー上で、前の例で取得した policyID を使用して、記憶域 QoS ポリシーを適用する方法を示しています。

```PowerShell
PS C:\> Get-VM -Name WinOltp1 | Get-VMHardDiskDrive | Set-VMHardDiskDrive -QoSPolicyID 7e2f3e73-1ae4-4710-8219-0769a4aba072
```

次の例は、ファイル サーバーから記憶域 QoS ポリシーの効果を表示する方法を示しています。

```PowerShell
PS C:\> Get-StorageQosFlow -InitiatorName WinOltp1 | format-list InitiatorName, PolicyId, MinimumIOPs, MaximumIOPs, StorageNodeIOPs, FilePath

InitiatorName   : WinOltp1
PolicyId        : 7e2f3e73-1ae4-4710-8219-0769a4aba072
MinimumIops     : 250
MaximumIops     : 1250
StorageNodeIOPs : 0
FilePath        : C:\ClusterStorage\Volume2\SHARES\TWO\BASEVHD\9914.0.AMD64FRE.WIN
                  MAIN.141218-1718_SERVER_SERVERDATACENTER_EN-US.VHDX

InitiatorName   : WinOltp1
PolicyId        : 7e2f3e73-1ae4-4710-8219-0769a4aba072
MinimumIops     : 250
MaximumIops     : 1250
StorageNodeIOPs : 0
FilePath        : C:\ClusterStorage\Volume3\SHARES\THREE\WINOLTP1\BOOT.VHDX

InitiatorName   : WinOltp1
PolicyId        : 7e2f3e73-1ae4-4710-8219-0769a4aba072
MinimumIops     : 1000
MaximumIops     : 5000
StorageNodeIOPs : 4550
FilePath        : C:\ClusterStorage\Volume3\SHARES\THREE\WINOLTP1\IOMETER.VHDX
PS C:\> Get-StorageQosFlow -InitiatorName WinOltp1 | for
mat-list InitiatorName, PolicyId, MinimumIOPs, MaximumIOPs, StorageNodeIOPs, FilePath

InitiatorName   : WinOltp1
PolicyId        : 7e2f3e73-1ae4-4710-8219-0769a4aba072
MinimumIops     : 250
MaximumIops     : 1250
StorageNodeIOPs : 0
FilePath        : C:\ClusterStorage\Volume2\SHARES\TWO\BASEVHD\9914.0.AMD64FRE.WIN
                  MAIN.141218-1718_SERVER_SERVERDATACENTER_EN-US.VHDX

InitiatorName   : WinOltp1
PolicyId        : 7e2f3e73-1ae4-4710-8219-0769a4aba072
MinimumIops     : 250
MaximumIops     : 1250
StorageNodeIOPs : 0
FilePath        : C:\ClusterStorage\Volume3\SHARES\THREE\WINOLTP1\BOOT.VHDX

InitiatorName   : WinOltp1
PolicyId        : 7e2f3e73-1ae4-4710-8219-0769a4aba072
MinimumIops     : 1000
MaximumIops     : 5000
StorageNodeIOPs : 4550
FilePath        : C:\ClusterStorage\Volume3\SHARES\THREE\WINOLTP1\IOMETER.VHDX
```

各仮想ハード ディスクに、その負荷を元にして調整された MinimumIOPs、MaximumIOPs、および MaximumIobandwidth 値が適用されます。  これにより、ディスクのグループで使用される帯域幅の合計量が、ポリシーで定義された範囲内に収まることが保証されます。  上の例では、最初の 2 つのディスクはアイドル状態であり、3 番目のディスクが最大 IOPS までの使用を許可されます。  最初の 2 つのディスクが再び IO の発行を開始した場合、3 番目のディスクの最大 IOPS は自動的に小さくなります。

### <a name="modify-an-existing-policy"></a>既存のポリシーを変更する
Name、MinimumIOPs、MaximumIOPs、および MaximumIoBandwidthcan のプロパティをポリシー作成後に変更することができます。  ただし、ポリシーの種類 (Aggregated/Dedicated) は、ポリシーを作成した後には変更できません。

次の Windows PowerShell コマンドレットは、既存のポリシーの MaximumIOPs プロパティを変更する方法を示しています。

```PowerShell
[DBG]: PS C:\demoscripts>> Get-StorageQosPolicy -Name SqlWorkload | Set-StorageQosPolicy -MaximumIops 6000
```

次のコマンドレットは変更を確認します。

```PowerShell
PS C:\> Get-StorageQosPolicy -Name SqlWorkload

Name                    MinimumIops            MaximumIops            Status
----                    -----------            -----------            ------
SqlWorkload             1000                   6000                   Ok

[plang-fs1]: PS C:\Users\plang\Documents> Get-StorageQosPolicy -Name SqlWorkload | Get-Storag
eQosFlow | Format-Table InitiatorName, PolicyId, MaximumIops, MinimumIops, StorageNodeIops -A
utoSize

InitiatorName PolicyId                             MaximumIops MinimumIops StorageNodeIops
------------- --------                             ----------- ----------- ---------------
WinOltp1      7e2f3e73-1ae4-4710-8219-0769a4aba072        1500         250               0
WinOltp1      7e2f3e73-1ae4-4710-8219-0769a4aba072        1500         250               0
WinOltp1      7e2f3e73-1ae4-4710-8219-0769a4aba072        6000        1000            4507
```

## <a name="how-to-identify-and-address-common-issues"></a><a name="BKMK_KnownIssues"></a>一般的な問題を識別して対処する方法
このセクションでは、無効な記憶域 QoS ポリシーが適用されている仮想マシンを見つける方法、同じポリシーを再作成する方法、仮想マシンからポリシーを削除する方法、記憶域 QoS ポリシーの要件を満たしていない仮想マシンを識別する方法について説明します。

### <a name="identify-virtual-machines-with-invalid-policies"></a><a name="BKMK_FindingVMsWithInvalidPolicies"></a>無効なポリシーが適用されている仮想マシンを識別する

ポリシーが仮想マシンから削除される前にファイル サーバーから削除された場合、仮想マシンはポリシーが適用されていない場合と同様に稼動し続けます。

```PowerShell
PS C:\> Get-StorageQosPolicy -Name SqlWorkload | Remove-StorageQosPolicy

Confirm
Are you sure you want to perform this action?
Performing the operation "DeletePolicy" on target "MSFT_StorageQoSPolicy (PolicyId =
"7e2f3e73-1ae4-4710-8219-0769a4aba072")".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [?] Help (default is "Y"):
```

フローのステータスには、"UnknownPolicyId" と表示されるようになります。

```PowerShell
PS C:\> Get-StorageQoSflow | Sort-Object InitiatorName | ft InitiatorName, Status, MinimumIOPs, MaximumIOPs, StorageNodeIOPs, Status, @{Expression={$_.FilePath.Substring($_.FilePath.LastIndexOf('\')+1)};Label="File"} -AutoSize

InitiatorName          Status MinimumIops MaximumIops StorageNodeIOPs          Status File
-------------          ------ ----------- ----------- ---------------          ------ ----
                           Ok           0           0               0              Ok Def...
                           Ok           0           0              10              Ok Def...
                           Ok           0           0              13              Ok Def...
                           Ok           0           0               0              Ok Def...
                           Ok           0           0               0              Ok Def...
                           Ok           0           0               0              Ok Def...
                           Ok           0           0               0              Ok Def...
                           Ok           0           0               0              Ok Def...
                           Ok           0           0               0              Ok Def...
BuildVM1                   Ok         100         200             193              Ok BUI...
BuildVM2                   Ok         100         200             196              Ok BUI...
BuildVM3                   Ok          50          64              17              Ok WIN...
BuildVM3                   Ok          50         136             179              Ok BUI...
BuildVM4                   Ok          50         100              23              Ok WIN...
BuildVM4                   Ok         100         200             173              Ok BUI...
TR20-VMM                   Ok          33         666               2              Ok DAT...
TR20-VMM                   Ok          25         975               3              Ok DAT...
TR20-VMM                   Ok          75        1025              12              Ok BOO...
WinOltp1      UnknownPolicyId           0           0               0 UnknownPolicyId 991...
WinOltp1      UnknownPolicyId           0           0            4926 UnknownPolicyId IOM...
WinOltp1      UnknownPolicyId           0           0               0 UnknownPolicyId BOO...
```

#### <a name="recreate-a-matching-storage-qos-policy"></a><a name="BKMK_RecreateMatchingPolicy"></a>同じ記憶域 QoS ポリシーを再作成する
ポリシーが誤って削除された場合、古い PolicyId を使用して新しいポリシーを作成することができます。  最初に、必要な PolicyId を取得します。

```PowerShell
PS C:\> Get-StorageQosFlow -Status UnknownPolicyId | ft InitiatorName, PolicyId -AutoSize

InitiatorName PolicyId
------------- --------
WinOltp1      7e2f3e73-1ae4-4710-8219-0769a4aba072
WinOltp1      7e2f3e73-1ae4-4710-8219-0769a4aba072
WinOltp1      7e2f3e73-1ae4-4710-8219-0769a4aba072
```

次に、その PolicyId を使用して新しいポリシーを作成します。

```PowerShell
PS C:\> New-StorageQosPolicy -PolicyId 7e2f3e73-1ae4-4710-8219-0769a4aba072 -PolicyType Aggregated -Name RestoredPolicy -MinimumIops 100 -MaximumIops 2000

Name                    MinimumIops            MaximumIops            Status
----                    -----------            -----------            ------
RestoredPolicy          100                    2000                   Ok
```

最後に、ポリシーが適用されたことを確認します。

```PowerShell
PS C:\> Get-StorageQoSflow | Sort-Object InitiatorName | ft InitiatorName, Status, MinimumIOPs, MaximumIOPs, StorageNodeIOPs, Status, @{Expression={$_.FilePath.Substring($_.FilePath.LastIndexOf('\')+1)};Label="File"} -AutoSize

InitiatorName Status MinimumIops MaximumIops StorageNodeIOPs Status File
------------- ------ ----------- ----------- --------------- ------ ----
                  Ok           0           0               0     Ok DefaultFlow
                  Ok           0           0               8     Ok DefaultFlow
                  Ok           0           0               9     Ok DefaultFlow
                  Ok           0           0               0     Ok DefaultFlow
                  Ok           0           0               0     Ok DefaultFlow
                  Ok           0           0               0     Ok DefaultFlow
                  Ok           0           0               0     Ok DefaultFlow
                  Ok           0           0               0     Ok DefaultFlow
                  Ok           0           0               0     Ok DefaultFlow
BuildVM1          Ok         100         200             192     Ok BUILDVM1.VHDX
BuildVM2          Ok         100         200             193     Ok BUILDVM2.VHDX
BuildVM3          Ok          50         100              24     Ok WIN8RTM_ENTERPRISE_VL...
BuildVM3          Ok         100         200             166     Ok BUILDVM3.VHDX
BuildVM4          Ok          50         100              12     Ok WIN8RTM_ENTERPRISE_VL...
BuildVM4          Ok         100         200             178     Ok BUILDVM4.VHDX
TR20-VMM          Ok          33         666               2     Ok DATA2.VHDX
TR20-VMM          Ok          33         666               2     Ok DATA1.VHDX
TR20-VMM          Ok          33         666              10     Ok BOOT.VHDX
WinOltp1          Ok          25         500               0     Ok 9914.0.AMD64FRE.WINMA...
```

#### <a name="remove-storage-qos-policies"></a><a name="BKMK_RemovePolicyFromVM"></a>記憶域 QoS ポリシーを削除する

ポリシーが意図的に削除された場合、または不要なポリシーが適用されている VM がインポートされた場合、それを削除できます。

```PowerShell
PS C:\> Get-VM -Name WinOltp1 | Get-VMHardDiskDrive | Set-VMHardDiskDrive -QoSPolicyID $null
```

PolicyId が仮想ハード ディスクの設定から削除されると、ステータスが "Ok" になり、最小値または最大値は適用されなくなります。

```PowerShell
PS C:\> Get-StorageQoSflow | Sort-Object InitiatorName | ft InitiatorName, MinimumIOPs, MaximumIOPs, StorageNodeIOPs, Status, @{Expression={$_.FilePath.Substring($_.FilePath.LastIndexOf('\')+1)};Label="File"} -AutoSize

InitiatorName MinimumIops MaximumIops StorageNodeIOPs Status File
------------- ----------- ----------- --------------- ------ ----
                        0           0               0     Ok DefaultFlow
                        0           0              16     Ok DefaultFlow
                        0           0              12     Ok DefaultFlow
                        0           0               0     Ok DefaultFlow
                        0           0               0     Ok DefaultFlow
                        0           0               0     Ok DefaultFlow
                        0           0               0     Ok DefaultFlow
                        0           0               0     Ok DefaultFlow
                        0           0               0     Ok DefaultFlow
BuildVM1              100         200             197     Ok BUILDVM1.VHDX
BuildVM2              100         200             192     Ok BUILDVM2.VHDX
BuildVM3                9           9              23     Ok WIN8RTM_ENTERPRISE_VL_BUILDW...
BuildVM3               91         191             171     Ok BUILDVM3.VHDX
BuildVM4                8           8              18     Ok WIN8RTM_ENTERPRISE_VL_BUILDW...
BuildVM4               92         192             163     Ok BUILDVM4.VHDX
TR20-VMM               33         666               2     Ok DATA2.VHDX
TR20-VMM               33         666               1     Ok DATA1.VHDX
TR20-VMM               33         666               5     Ok BOOT.VHDX
WinOltp1                0           0               0     Ok 9914.0.AMD64FRE.WINMAIN.1412...
WinOltp1                0           0            1811     Ok IOMETER.VHDX
WinOltp1                0           0               0     Ok BOOT.VHDX
```

### <a name="find-virtual-machines-that-are-not-meeting-storage-qos-policies"></a><a name="BKMK_VMsThatDoNotMeetStorageQoSPoilicies"></a>記憶域 QoS ポリシーを満たしていない仮想マシンを見つける
次のようなフローには **InsufficientThroughput** ステータスが割り当てられます。

-   ポリシーによって設定された最小 IOPS が定義されている。

-   最小値を満たすかまたは超えるレートで IO が開始されている。

-   最小 IOP レートを達成していない。

```PowerShell
PS C:\> Get-StorageQoSflow | Sort-Object InitiatorName | ft InitiatorName, MinimumIOPs, MaximumIOPs, StorageNodeIOPs, Status, @{Expression={$_.FilePath.Substring($_.FilePath.LastIndexOf('\')+1)};Label="File"} -AutoSize

InitiatorName MinimumIops MaximumIops StorageNodeIOPs                 Status File
------------- ----------- ----------- ---------------                 ------ ----
                        0           0               0                     Ok DefaultFlow
                        0           0               0                     Ok DefaultFlow
                        0           0              15                     Ok DefaultFlow
                        0           0               0                     Ok DefaultFlow
                        0           0               0                     Ok DefaultFlow
                        0           0               0                     Ok DefaultFlow
                        0           0               0                     Ok DefaultFlow
                        0           0               0                     Ok DefaultFlow
                        0           0               0                     Ok DefaultFlow
BuildVM3               50         100              20                     Ok WIN8RTM_ENTE...
BuildVM3              100         200             174                     Ok BUILDVM3.VHDX
BuildVM4               50         100              11                     Ok WIN8RTM_ENTE...
BuildVM4              100         200             188                     Ok BUILDVM4.VHDX
TR20-VMM               33         666               3                     Ok DATA1.VHDX
TR20-VMM               78        1032             180                     Ok BOOT.VHDX
TR20-VMM               22         968               4                     Ok DATA2.VHDX
WinOltp1             3750        5000               0                     Ok 9914.0.AMD64...
WinOltp1            15000       20000           11679 InsufficientThroughput IOMETER.VHDX
WinOltp1             3750        5000               0                     Ok BOOT.VHDX
```

次の例に示すように、**InsufficientThroughput** を含む、任意のステータスのフローを特定することができます。

```PowerShell
PS C:\> Get-StorageQosFlow -Status InsufficientThroughput | fl

FilePath           : C:\ClusterStorage\Volume3\SHARES\THREE\WINOLTP1\IOMETER.VHDX
FlowId             : 1ca356ff-fd33-5b5d-b60a-2c8659dc803e
InitiatorId        : 2ceabcef-2eba-4f1b-9e66-10f960b50bbf
InitiatorIOPS      : 12168
InitiatorLatency   : 22.983
InitiatorName      : WinOltp1
InitiatorNodeName  : plang-c1.plang.nttest.microsoft.com
Interval           : 300000
Limit              : 20000
PolicyId           : 5d1bf221-c8f0-4368-abcf-aa139e8a7c72
Reservation        : 15000
Status             : InsufficientThroughput
StorageNodeIOPS    : 12181
StorageNodeLatency : 22.0514
StorageNodeName    : plang-fs2.plang.nttest.microsoft.com
TimeStamp          : 2/13/2015 12:07:30 PM
VolumeId           : 0d2fd367-8d74-4146-9934-306726913dda
PSComputerName     :
MaximumIops        : 20000
MinimumIops        : 15000
```

## <a name="monitor-health-using-storage-qos"></a><a name="BKMK_Health"></a>記憶域 QoS を使用して正常性を監視する
新しいヘルス サービスは、記憶域クラスターの監視を簡素化し、任意のノードの対処可能なイベントを 1 つの場所で確認できるようにします。 このセクションでは、`debug-storagesubsystem` コマンドレットを使用して記憶域クラスターの正常性を監視する方法について説明します。

### <a name="view-storage-status-with-debug-storagesubsystem"></a>Debug-StorageSubSystem を使用して記憶域のステータスを表示する
クラスター化された記憶域スペースは、1 つの場所で記憶域クラスターの正常性に関する情報も提供します。 これにより、管理者は、記憶域の展開の現在の問題を識別し、問題が発生または解消したタイミングを監視できます。

#### <a name="vm-with-invalid-policy"></a>無効なポリシーが適用された VM
無効なポリシーが適用されている VM も記憶域サブシステムの正常性監視を介して報告されます。  以下に、「[無効なポリシーが適用されている VM を見つける](#BKMK_FindingVMsWithInvalidPolicies)」セクションで説明されているものと同じ状態の例を示します。

```PowerShell
C:\> Get-StorageSubSystem -FriendlyName Clustered* | Debug-StorageSubSystem

EventTime                 :
FaultId                   : 0d16d034-9f15-4920-a305-f9852abf47c3
FaultingObject            :
FaultingObjectDescription : Storage QoS Policy 5d1bf221-c8f0-4368-abcf-aa139e8a7c72
FaultingObjectLocation    :
FaultType                 : Storage QoS policy used by consumer does not exist.
PerceivedSeverity         : Minor
Reason                    : One or more storage consumers (usually Virtual Machines) are
                            using a non-existent policy with id
                            5d1bf221-c8f0-4368-abcf-aa139e8a7c72. Consumer details:

                            Flow ID: 1ca356ff-fd33-5b5d-b60a-2c8659dc803e
                            Initiator ID: 2ceabcef-2eba-4f1b-9e66-10f960b50bbf
                            Initiator Name: WinOltp1
                            Initiator Node: plang-c1.plang.nttest.microsoft.com
                            File Path:
                            C:\ClusterStorage\Volume3\SHARES\THREE\WINOLTP1\IOMETER.VHDX
RecommendedActions        : {Reconfigure the storage consumers (usually Virtual Machines)
                            to use a valid policy., Recreate any missing Storage QoS
                            policies.}
PSComputerName            :
```

#### <a name="lost-redundancy-for-a-storage-spaces-virtual-disk"></a>記憶域スペース仮想ディスクの冗長性が失われる

この例では、クラスター化された記憶域スペースに、3 方向ミラーとして作成された仮想ディスクがあります。  障害が発生したディスクはシステムから削除されましたが、交換用のディスクは追加されませんでした。  記憶域サブシステムは、HealthStatus **Warning** で、冗長性が失われたことを報告していますが、ボリュームは引き続きオンラインになっているので OperationalStatus は "**OK**" になっています。

```PowerShell
PS C:\> Get-StorageSubSystem -FriendlyName Clustered*

FriendlyName                   HealthStatus                   OperationalStatus
------------                   ------------                   -----------------
Clustered Windows Storage o... Warning                        OK

[plang-fs1]: PS C:\Users\plang\Documents> Get-StorageSubSystem -FriendlyName Clustered* | Deb
ug-StorageSubSystem

EventTime                 :
FaultId                   : dfb4b672-22a6-4229-b2ed-c29d7485bede
FaultingObject            :
FaultingObjectDescription : Virtual disk 'Two'
FaultingObjectLocation    :
FaultType                 : VirtualDiskDegradedFaultType
PerceivedSeverity         : Minor
Reason                    : Virtual disk 'Two' does not have enough redundancy remaining to
                            successfully repair or regenerate its data.
RecommendedActions        : {Rebalance the pool, replace failed physical disks, or add new
                            physical disks to the storage pool, then repair the virtual
                            disk.}
PSComputerName            :
```

### <a name="sample-script-for-continuous-monitoring-of-storage-qos"></a>記憶域 QoS を継続的に監視するためのサンプル スクリプト

このセクションには、WMI スクリプトを使用して一般的な障害を監視できる方法を示すサンプル スクリプトが含まれています。  このスクリプトは、開発者が正常性イベントをリアルタイムで取得するための出発点として設計されています。

**スクリプトの例:**

```PowerShell
param($cimSession)
# Register and display events
Register-CimIndicationEvent -Namespace root\microsoft\windows\storage -ClassName msft_storagefaultevent -CimSession $cimSession

while ($true)
{
     $e = (Wait-Event)
     $e.SourceEventArgs.NewEvent
     Remove-Event $e.SourceIdentifier
}
```

## <a name="frequently-asked-questions"></a>よく寄せられる質問

### <a name="how-do-i-retain-a-storage-qos-policy-being-enforced-for-my-virtual-machine-if-i-move-its-vhdvhdx-files-to-another-storage-cluster"></a>仮想マシンの VHD/VHDx ファイルを別の記憶域クラスターに移動する場合、その仮想マシンに適用されている記憶域 QoS ポリシーをどのようにして維持すればよいですか

ポリシーを指定する VHD/VHDx ファイルの設定は、ポリシー ID の GUID です。  ポリシーが作成されるときに、**PolicyID** パラメーターを使用して GUID を指定できます。  このパラメータが指定されていない場合、ランダムな GUID が作成されます。  そのため、VM が現在 VHD/VHDx ファイルを保存している記憶域クラスター上で PolicyID を取得し、移動先の記憶域クラスター上で同一のポリシーを作成して、その後で同じ GUID での作成を指定することができます。  VM ファイルが新しい記憶域クラスターに移動されたときには、同じ GUID のポリシーが有効になります。

System Center Virtual Machine Manager を使用して、複数の記憶域クラスターにポリシーを適用すると、このシナリオを簡単に実行できます。
### <a name="if-i-change-the-storage-qos-policy-why-dont-i-see-it-take-effect-immediately-when-i-run-get-storageqosflow"></a>記憶域 QoS ポリシーを変更した場合、Get-StorageQoSFlow を実行したときに直ちに有効にならないのはなぜですか

ポリシーの最大値に到達したフローがあり、ポリシーをより高い値または低い値に変更し、PowerShell コマンドレットを使用してフローの待機時間/IOPS/帯域幅を直ちに決定した場合、フローに対するポリシー変更のすべての効果が表示されるまでに最大 5 分かかります。  新しい制限は、数秒で有効になりますが、**Get-StorgeQoSFlow** PowerShell コマンドレットは、5 分間のスライディング ウィンドウを使用し、各カウンターの平均を使用します。  そのようにしないと、PowerShell コマンドレットを続けて複数回実行し、現在の値が表示される場合、IOPS と待機時間の値が秒ごとに大きく変動する可能性があるので、大幅に異なる値が表示されることがあります。

### <a name="what-new-functionality-was-added-in-windows-server-2016"></a><a name="BKMK_Updates"></a>Windows Server 2016 にはどのような新機能が追加されていますか

Windows Server 2016 では、記憶域 QoS ポリシーの種類の名前が変更されました。  **Multi-instance** ポリシーの種類の名前が **Dedicated** に変更され、**Single-instance** の名前が **Aggregated** に変更されました。 Dedicated ポリシーの管理動作も変更されました。同じ **Dedicated** ポリシーが適用されている同じ仮想マシン内の VHD/VHDX ファイルは I/O の割り当てを共有しません。

Windows Server 2016 には、次に示す 2 つの新しい記憶域 QoS 機能があります。

-   **最大帯域幅**

    Windows Server 2016 の記憶域 QoS では、ポリシーに割り当てられたフローが消費できる最大帯域幅を指定する機能が導入されました。  **StorageQosPolicy** コマンドレットでそれを指定するときには、**MaximumIOBandwidth** パラメーターを使用し、出力は 1 秒あたりのバイト単位で表示されます。
    **MaximimIops** と **MaximumIOBandwidth** の両方がポリシーで設定されている場合、それらの両方が有効になり、フローが最初に到達した方が、そのフローの I/O を制限します。

-   **IOPS 正規化が構成可能**

    記憶域 QoS は、IOPS の正規化を使用します。  既定値では、正規化サイズとして 8K を使用します。  Windows Server 2016 の記憶域 QoS では、記憶域クラスターに対して異なる正規化サイズを指定する機能が導入されました。  この正規化サイズは、記憶域クラスター上のすべてのフローに適用され、変更されると直ちに (数秒で) 有効になります。  最小値は 1 KB で最大値は 4 GB です (4 MB を超える IO は通常発生しないので、4 MB を超える値に設定しないことをお勧めします)。

    正規化の計算を変更したために IOPS の正規化を変更すると、記憶域 QoS の出力で、同じ IO パターン/スループットでも異なる IOPS の数値が表示されることに注意する必要があります。  記憶域クラスター間の IOPS を比較している場合は、各クラスターで使用している正規化の値が、報告される正規化済み IOPS に影響するので、その値を確認する必要があります。

#### <a name="example-1-creating-a-new-policy-and-viewing-the-maximum-bandwidth-on-the-storage-cluster"></a>例 1: 記憶域クラスター上で新しいポリシーを作成して最大帯域幅を表示する
PowerShell で、数値を表示する単位を指定できます。  次の例では、最大帯域幅の値として 10 MB を使用します。  記憶域 QoS は、これを変換して、1 秒あたりのバイト数として保存します。そのため、10 MB は 10485760 バイト/秒に変換されます。

```PowerShell
PS C:\Windows\system32> New-StorageQosPolicy -Name HR_VMs -MaximumIops 1000 -MinimumIops 20 -MaximumIOBandwidth 10MB

Name   MinimumIops MaximumIops MaximumIOBandwidth Status
----   ----------- ----------- ------------------ ------
HR_VMs 20          1000        10485760           Ok

PS C:\Windows\system32> Get-StorageQosPolicy

Name    MinimumIops MaximumIops MaximumIOBandwidth Status
----    ----------- ----------- ------------------ ------
Default 0           0           0                  Ok
HR_VMs  20          1000        10485760           Ok

PS C:\Windows\system32> Get-StorageQoSFlow | fL InitiatorName,FilePath,InitiatorIOPS,InitiatorLatency,InitiatorBandwidth

InitiatorName      : testsQoS
FilePath           : C:\ClusterStorage\Volume2\TESTSQOS\VIRTUAL HARD DISKS\TESTSQOS.VHDX
InitiatorIOPS      : 5
InitiatorLatency   : 1.5455
InitiatorBandwidth : 37888
```

#### <a name="example-2-get-iops-normalization-settings-and-specify--a-new-value"></a>例 2: IOPS 正規化の設定を取得し、新しい値を指定する

次の例では、記憶域クラスターの IOPS 正規化の設定 (既定値の 8 KB) を取得し、32 KB に設定して、もう一度表示する方法を示します。  この例で、"32 KB" を指定するのは、PowerShell では単位の指定が許可されていて、バイトに変換する必要がないためです。   出力には、1 秒あたりのバイト数で値が表示されます。

```PowerShell
PS C:\Windows\system32> Get-StorageQosPolicyStore

IOPSNormalizationSize
---------------------
8192

PS C:\Windows\system32> Set-StorageQosPolicyStore -IOPSNormalizationSize 32KB
PS C:\Windows\system32> Get-StorageQosPolicyStore

IOPSNormalizationSize
---------------------
32768
```

## <a name="see-also"></a>参照
- [Windows Server 2016](../../get-started/windows-server-2016.md)
- [Windows Server 2016 の記憶域レプリカに関する記事](../storage-replica/storage-replica-overview.md)
- [Windows Server 2016 での記憶域スペース ダイレクト](../storage-spaces/storage-spaces-direct-overview.md)
