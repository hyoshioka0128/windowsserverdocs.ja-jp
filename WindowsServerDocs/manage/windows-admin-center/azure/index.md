---
title: Windows Server を Azure のハイブリッド サービスに接続します。
description: Azure のハイブリッド サービスを使用して、クラウドに移行する Windows Server のオンプレミス デプロイを拡張できます。
ms.technology: manage
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 05/31/2019
ms.openlocfilehash: 460399a57bc229b44d37a9fdd1e4938bf9e7d6ac
ms.sourcegitcommit: fe621b72d45d0259bac1d5b9031deed3dcbed29d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/01/2019
ms.locfileid: "66455362"
---
# <a name="connecting-windows-server-to-azure-hybrid-services"></a>Windows Server を Azure のハイブリッド サービスに接続します。

>適用対象:Windows Server 2019、Windows Server 2016、Windows Server (半期チャネル)

Azure のハイブリッド サービスを使用して、クラウドに移行する Windows Server のオンプレミス デプロイを拡張できます。 これらのクラウド サービスは、次の便利な関数の配列を指定します。

- 仮想マシンを保護し、Azure Site Recovery でクラウド ベースのバックアップとディザスター リカバリー (HA/DR) を使用します。 
- アプリケーション、ネットワークと高度な分析と Azure Monitor での機械学習を利用してインフラストラクチャ全体で何が起こっているかを追跡します。 
- Azure のネットワーク アダプターを使用した Azure へのネットワーク接続を簡略化します。
- 仮想マシンを Azure の更新プログラム管理を最新の状態に保ちます。

Azure のハイブリッド サービスは、次の構成で Windows サーバーと使用します。

- スタンドアロンの物理サーバーと仮想マシン (Vm)
- クラスターの場合、認定を受けたハイパー コンバージド クラスターを含む、 [Azure Stack HCI](https://docs.microsoft.com/azure-stack/operator/azure-stack-hci-overview)、および[Windows Server Software-Defined (WSSD)](https://www.microsoft.com/en-us/cloud-platform/software-defined-datacenter)プログラム

Azure portal と、ダウンロード、または 2 を使用するほとんどの Azure のハイブリッド サービスを設定できますが、多くの簡素化されたセットアップ エクスペリエンスと、サービスのサーバー中心のビューを提供する Windows Admin Center に直接統合は。

## <a name="azure-hybrid-services-tool"></a>Azure のハイブリッド サービス ツール

Azure のハイブリッド サービス ツール[Windows Admin Center](../understand/windows-admin-center.md)オンプレミスに値をもたらす、利用可能なすべての Azure サービスを簡単に見つけることができます、一元管理されたハブに統合されたすべての Azure サービスを統合またはハイブリッド環境です。 

![Azure Hybrid Services ツールを示す Windows Admin Center のスクリーン ショット](../media/azure-services/ahs-discover.png)

Azure サービスが既に有効なサーバーに接続する場合、Azure のハイブリッド サービス ツールは、そのサーバーで有効になっているすべてのサービスを表示するガラスの 1 つのウィンドウとして機能します。 Windows Admin Center 内の関連するツールに簡単に、指先ひとつで、これらの Azure サービスまたは読み取りをドキュメントに複数のより深い管理用の Azure portal 起動できます。 

![サーバーに既にインストールされている Azure サービスを示す Windows Admin Center のスクリーン ショット](../media/azure-services/ahs-dayN.png)

Azure のハイブリッド サービス ツールで、次の操作を実行できます。
- Windows Admin Center から、Windows Server のバックアップ[Azure Backup](azure-backup.md)
- Windows Admin Center から HYPER-V 仮想マシンを保護[Azure Site Recovery](azure-site-recovery.md)
- ファイル サーバー、クラウドとの同期を使用して[Azure File Sync](azure-file-sync.md)
- すべての Windows サーバーのオペレーティング システムの更新プログラムの管理オンプレミスまたはクラウドでの[Azure 更新プログラムの管理](azure-update-management.md)
- オンプレミスのサーバーを監視またはクラウドでのアラートを構成して[Azure Monitor](azure-monitor.md)
- オンプレミス サーバーを使用する Azure 仮想ネットワークに接続[Azure のネットワーク アダプター](https://aka.ms/WACNetworkAdapter)

## <a name="services-for-stand-alone-servers-and-vms"></a>スタンドアロン サーバーと Vm のサービス

これは、スタンドアロン サーバーと Vm の機能を提供する Azure サービスの完全な一覧です。

- **(新規)使用して、ファイル サーバー、クラウドとの同期[Azure File Sync](https://aka.ms/afs)**  
Azure ファイル共有をこのサーバー上のファイルを同期します。 すべてのファイルをローカルに保持または頻繁に使用したクラウドにコールド データを階層化、サーバー上のファイルのみ使用してクラウド階層化およびキャッシュします。 クラウド内のデータは、オンプレミス サーバーのバックアップについて心配する必要がないため、バックアップできます。 さらに、複数サイト同期できる一連のファイルの同期を保つ複数のサーバー。

- **Windows Admin Center を追加することのセキュリティ層を追加[Azure Active Directory (Azure AD)](https://azure.microsoft.com/services/active-directory/)認証**  
ゲートウェイにアクセスする Azure Active Directory (Azure AD) の id を使用して認証を要求することで、Windows Admin Center に追加のセキュリティ層を追加できます。 Azure AD 認証を使用して、条件付きアクセスと多要素認証などの Azure AD のセキュリティ機能を活用することもできます。  
詳細については、次を参照してください。 [Windows Admin Center を構成する Azure AD 認証。](../configure/user-access-control.md#azure-active-directory)  

- **使用して、HYPER-V 仮想マシンを保護する[Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)**  
災害が発生した場合、ビジネスに不可欠なインフラストラクチャが保護されているように、Vm 上で実行されているワークロードをレプリケートすることができます。 Windows Admin Center は、セットアップと、HYPER-V サーバーまたはクラスターの仮想マシンをレプリケートするプロセスが簡単に Azure Site Recovery のディザスター リカバリー サービスを使用して環境の回復性を高める効率化されます。  
詳細については、次を参照してください。 [Windows Admin Center と Azure Site Recovery を使用して Vm を保護する](azure-site-recovery.md)します。

- **Windows サーバーのバックアップを[Azure Backup](https://docs.microsoft.com/azure/backup/backup-overview)**  
Azure に誤ってまたは悪意のある削除や破損、ランサムウェアから保護する、Windows サーバーをバックアップすることができます。  
詳細については、次を参照してください。 [Azure Backup にサーバーのバックアップを](azure-backup.md)します。

- **監視し、使用して環境内のすべてのサーバーの電子メール アラートを取得[仮想マシンの Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview)**  
サーバーの正常性とイベントを監視、電子メール アラートを作成、環境全体のサーバーのパフォーマンスの統合ビューを取得および視覚化アプリケーション、システムでは、Azure Monitor では、仮想マシンの Insights とも呼ばれますを使用してに接続されているサービスを指定サーバー。  
詳細については、次を参照してください。 [Azure Monitor にサーバーを接続し、電子メール通知を構成する](azure-monitor.md)します。

- **すべての Windows サーバーのオペレーティング システムの更新プログラムを一元的に管理[Azure 更新プログラムの管理](https://docs.microsoft.com/azure/automation/automation-update-management)**  
サーバー単位ではなく、1 つの場所から更新プログラムとパッチの複数のサーバーと Vm を管理できます。 Azure の Update Management、すぐに利用可能な更新の状態を評価する、必要な更新プログラムのインストールをスケジュールして正常に適用される更新プログラムを確認する展開の結果を確認できます。 これは、サーバーでの Azure Vm に他のクラウド プロバイダーによってホストされているがかどうかや、オンプレミスでできます。  
詳細については、次を参照してください。[の Azure の更新の管理サーバーを構成する](azure-update-management.md)します。

- **オンプレミス サーバーを使用する Azure 仮想ネットワークに接続する[Azure のネットワーク アダプター](https://aka.ms/WACNetworkAdapter)**  
サーバーを Azure Virtual Network に安全に接続するため、オンプレミスのサーバーには、Azure のネットワーク アダプターを追加できます。  
詳細については、次を参照してください。 [、オンプレミスの Windows Server と Azure 仮想ネットワーク間のポイント対サイト VPN 接続を構成する](https://aka.ms/WACNetworkAdapter)します。

- **Azure IaaS 仮想マシンを管理[Windows Admin Center](manage-azure-vms.md)**  
Windows Admin Center を使用して、Azure Vm だけでなく、オンプレミス マシンを管理することができます。 Azure VNet に接続するため、Windows Admin Center ゲートウェイを構成するには、Windows Admin Center が用意されている、簡略化された一貫性のあるツールを使用して Azure の仮想マシンを管理できます。 詳細については、次を参照してください。 [Azure で Vm を管理する構成の Windows Admin Center](manage-azure-vms.md)します。

## <a name="services-for-clusters"></a>クラスターのサービス

これらは、クラスター全体の機能を提供する Azure サービス (これらすべて統合されていない Windows Admin Center にまだ)。

- [Azure Monitor を使用して、ハイパーコンバージド クラスターを監視します。](../../../storage/storage-spaces/configure-azure-monitor.md)
- [Azure Site Recovery を使用して Vm を保護します。](azure-site-recovery.md)
- [クラスターのクラウド ミラーリング監視サーバーをデプロイします。](../../../failover-clustering/deploy-cloud-witness.md)

## <a name="see-also"></a>関連項目

- [Windows Admin Center を Azure に接続します。](azure-integration.md)
- [Azure で Windows Admin Center を展開します。](deploy-wac-in-azure.md)