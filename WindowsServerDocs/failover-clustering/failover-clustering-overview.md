---
ms.assetid: c9844427-27cf-4d76-b5bb-e06368b092f7
title: フェールオーバー クラスタリング
ms.prod: windows-server-threshold
layout: LandingPage
ms.topic: landing-page
ms.manager: dongill
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 03/08/2019
ms.localizationpriority: high
ms.openlocfilehash: 9e4184e52ef48e758ebc80e63d3d6f952a09cc2c
ms.sourcegitcommit: 8ba2c4de3bafa487a46c13c40e4a488bf95b6c33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/25/2019
ms.locfileid: "66222451"
---
# <a name="failover-clustering-in-windows-server"></a>Windows Server のフェールオーバー クラスタリング

> 適用対象:Windows Server 2019、Windows Server 2016

>[!TIP]
> 以前のバージョンの Windows Server に関する情報をお探しの場合は、 docs.microsoft.com の他の [Windows Server ライブラリ](/previous-versions/windows/)を参照してください。 また、[このサイトで検索して](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions)、具体的な情報を確認することもできます。

<hr />

フェールオーバー クラスターは、互いに連携する個々のコンピューターが集まって形成され、クラスター化された役割 (以前は、クラスター化されたサービス、クラスター化されたアプリケーションと呼ばれていました) の可用性とスケーラビリティを高めます。 クラスター サーバー (ノード) は、物理ケーブルとソフトウェアにより接続されます。 クラスター ノードに障害が発生した場合、他のノードがサービスの提供を開始します。このプロセスを "フェールオーバー" といいます。 また、クラスター化された役割は能動的に監視され、正常に機能しているかどうかが確認されます。 正常に機能していない役割は、再起動されるか、または別のノードに移されます。

フェールオーバー クラスターには、一貫性のある分散名前空間を提供するクラスターの共有ボリューム (CSV) 機能も用意されています。これにより、クラスター化された役割のすべてのノードから共有記憶域にアクセスできます。 フェールオーバー クラスタリング機能により、ユーザーに対するサービスの中断を最小限に抑えることができます。

フェールオーバー クラスタリングには、次のような多くの実用的なアプリケーションがあります。
* Microsoft SQL Server、Hyper-V 仮想マシンなどのアプリケーションを対象とした高可用性 (継続的に使用可能な) ファイル共有記憶域
* 物理サーバー上、または Hyper-V を実行するサーバーにインストールされた仮想マシン上で実行される高可用性のクラスター化された役割


|  |  |
|---------|---------|
|![新着情報](../media/i-whats-new.svg)  | [**フェールオーバー クラスタ リングの新機能**](whats-new-in-failover-clustering.md) |


|  |  |  |
|---------|---------|---------|
|![理解](../media/i-cluster.svg)**を理解します。**  |  ![計画](../media/i-cluster.svg)**計画**  |  ![展開](../media/i-cluster.svg)**展開**       |
| [アプリケーション データ用のスケールアウト ファイル サーバー](sofs-overview.md)    |   [計画フェールオーバー クラスタ リングのハードウェア要件と記憶域オプション](clustering-requirements.md)      |  [Active Directory Domain Services での展開の事前設定のクラスター コンピューター オブジェクト](prestage-cluster-adds.md)  |
|  [クラスターとプール クォーラム](../storage/storage-spaces/understand-quorum.md)   |   [クラスター共有ボリューム (CSV) の使用](failover-cluster-csvs.md)      | [フェールオーバー クラスターの作成](create-failover-cluster.md)        |
|  [障害ドメインの認識](fault-domains.md)   |  [仮想マシンのゲスト クラスターを使用して、記憶域スペース ダイレクト](../storage/storage-spaces/storage-spaces-direct-in-vm.md)       | [2 ノードのファイル サーバーを展開する](../storage/storage-spaces/storage-spaces-direct-in-vm.md)        |
| [簡略化された SMB マルチチャネルと複数 NIC のクラスター ネットワーク](smb-multichannel.md)    |         |  [クォーラムと監視サーバーを管理します。](manage-cluster-quorum.md)       |
|   [VM の負荷分散](vm-load-balancing-overview.md)  |         |   [クラウド監視を展開します。](deploy-cloud-witness.md)      |
|   [クラスター セット](../storage/storage-spaces/cluster-sets.md)  |         |     [ファイル共有監視を展開する](file-share-witness.md)    |
|   [クラスターのアフィニティ](cluster-affinity.md)  |         |    [クラスター オペレーティング システムのローリング アップグレード]()     |
|     |         |     [同じハードウェア上でフェールオーバー クラスターをアップグレードする](upgrade-option-same-hardware.md)    |
|     |         |     [Active Directory のデタッチされたクラスターをデプロイします。](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn265970\(v%3dws.11\))    |


|  |  |  |
|---------|---------|---------|
|![管理](../media/i-cluster.svg)**管理**  |  ![ツールと設定](../media/i-cluster.svg)**ツールと設定**  |  ![コミュニティ リソース](../media/i-cluster.svg)**コミュニティ リソース**       |
| [クラスター対応更新](cluster-aware-updating.md)    |   [フェールオーバー クラスタ リングの PowerShell コマンドレット](https://docs.microsoft.com/powershell/module/failoverclusters/?view=win10-ps)      |  [高可用性 (クラスタ リング) フォーラム](https://go.microsoft.com/fwlink/p/?LinkId=230641)       |
|  [ヘルスサービス](health-service-overview.md)   |   [クラスター対応更新の PowerShell コマンドレット](https://docs.microsoft.com/powershell/module/clusterawareupdating/?view=win10-ps)      | [フェールオーバー クラスタ リングとネットワーク負荷分散のチーム ブログ](http://blogs.msdn.com/b/clustering/)        |
|  [クラスター ドメインの移行](cluster-domain-migration.md)   |         |         |
|  [Windows エラー報告を使用したトラブルシューティング](troubleshooting-using-wer-reports.md)   |         |         |
