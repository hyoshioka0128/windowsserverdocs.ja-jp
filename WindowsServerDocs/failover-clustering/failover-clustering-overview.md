---
ms.assetid: c9844427-27cf-4d76-b5bb-e06368b092f7
title: フェールオーバー クラスタリング
ms.topic: landing-page
manager: lizross
author: JasonGerend
ms.author: jgerend
ms.date: 06/06/2019
ms.localizationpriority: high
ms.openlocfilehash: 41f5eef75e20a4da740141620493d2daa254b0a1
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87992854"
---
# <a name="failover-clustering-in-windows-server"></a>Windows Server のフェールオーバー クラスタリング

> 適用先:Windows Server 2019、Windows Server 2016

フェールオーバー クラスターは、互いに連携する個々のコンピューターが集まって形成され、クラスター化された役割 (以前は、クラスター化されたサービス、クラスター化されたアプリケーションと呼ばれていました) の可用性とスケーラビリティを高めます。 クラスター サーバー (ノード) は、物理ケーブルとソフトウェアにより接続されます。 クラスター ノードに障害が発生した場合、他のノードがサービスの提供を開始します。このプロセスを "フェールオーバー" といいます。 また、クラスター化された役割は能動的に監視され、正常に機能しているかどうかが確認されます。 正常に機能していない役割は、再起動されるか、または別のノードに移されます。

フェールオーバー クラスターには、一貫性のある分散名前空間を提供するクラスターの共有ボリューム (CSV) 機能も用意されています。これにより、クラスター化された役割のすべてのノードから共有記憶域にアクセスできます。 フェールオーバー クラスタリング機能により、ユーザーに対するサービスの中断を最小限に抑えることができます。

フェールオーバー クラスタリングには、次のような多くの実用的なアプリケーションがあります。

* Microsoft SQL Server、Hyper-V 仮想マシンなどのアプリケーションを対象とした高可用性の (継続的に使用可能な) ファイル共有記憶域。
* 物理サーバー上、または Hyper-V を実行するサーバーにインストールされた仮想マシン上で実行される高可用性のクラスター化された役割。

| **概要**                                                               |  **計画**                          |  **展開**       |
| -------------                                                                |  --------------                        | --------------------- |
| [フェールオーバー クラスタリングの新機能](whats-new-in-failover-clustering.md)    | [フェールオーバー クラスタリングのハードウェア要件と記憶域オプションの計画](clustering-requirements.md)  | [フェールオーバー クラスターの作成](create-failover-cluster.md) |
| [アプリケーション データ用のスケールアウト ファイル サーバー](sofs-overview.md)               | [クラスター共有ボリューム (CSV) の使用](failover-cluster-csvs.md) | [2 ノードのファイル サーバーを展開する](deploy-two-node-clustered-file-server.md) |
|  [クラスターとプール クォーラム](../storage/storage-spaces/understand-quorum.md)   |  [ゲスト仮想マシン クラスターで記憶域スペース ダイレクトを使用する](../storage/storage-spaces/storage-spaces-direct-in-vm.md)       | [Active Directory Domain Services でクラスター コンピューター アカウントを事前設定する](prestage-cluster-adds.md) |
| [障害ドメインの認識](fault-domains.md)                                 |                                 | [Active Directory でクラスターのアカウントを構成する](configure-ad-accounts.md) |
| [簡略化された SMB マルチチャネルと複数 NIC のクラスター ネットワーク](smb-multichannel.md) |                       | [クォーラムと監視を管理する](manage-cluster-quorum.md) |
| [VM の負荷分散](vm-load-balancing-overview.md)                         |                             | [クラウド監視を展開する](deploy-cloud-witness.md) |
| [クラスター セット](../storage/storage-spaces/cluster-sets.md)                  |                             |[ファイル共有監視を展開する](file-share-witness.md) |
| [クラスターのアフィニティ](cluster-affinity.md)                                     |                            | [クラスター オペレーティング システムのローリング アップグレード](cluster-operating-system-rolling-upgrade.md) |
|                                                                             |                            | [同じハードウェア上でフェールオーバー クラスターをアップグレードする](upgrade-option-same-hardware.md) |
|                                                                            |                             | [Active Directory からデタッチされたクラスターを展開する](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn265970\(v%3dws.11\))

|**管理**  |  **ツールと設定**  |  **コミュニティ リソース**       |
| ------------- |  -------------- | --------------------- |
| [クラスター対応更新](cluster-aware-updating.md)    |   [フェールオーバー クラスタリング用 PowerShell コマンドレット](/powershell/module/failoverclusters/?view=win10-ps)      |  [高可用性 (クラスタリング) フォーラム](https://go.microsoft.com/fwlink/p/?LinkId=230641)       |
|  [ヘルスサービス](health-service-overview.md)   |   [クラスター対応更新の PowerShell コマンドレット](/powershell/module/clusterawareupdating/?view=win10-ps)      | [フェールオーバー クラスタリングおよびネットワークの負荷分散チームによるブログ](https://blogs.msdn.com/b/clustering/)        |
|  [クラスター ドメインの移行](cluster-domain-migration.md)   |         |         |
|  [Windows エラー報告を使用したトラブルシューティング](troubleshooting-using-wer-reports.md)   |         |         |