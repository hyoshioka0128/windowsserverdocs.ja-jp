---
title: Azure ハイブリッド サービスへの Windows Server の接続
description: Azure ハイブリッド サービスを使用して、Windows Server のオンプレミス展開をクラウドに拡張できます。
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
# <a name="connecting-windows-server-to-azure-hybrid-services"></a>Azure ハイブリッド サービスへの Windows Server の接続

>適用対象:Windows Server 2019、Windows Server 2016、Windows Server (半期チャネル)

Azure ハイブリッド サービスを使用して、Windows Server のオンプレミス展開をクラウドに拡張できます。 これらのクラウド サービスは、次のような一連の便利な機能を提供します。

- Azure Site Recovery によって、仮想マシンを保護し、クラウドベースのバックアップとディザスター リカバリー (HA/DR) を使用します。 
- Azure Monitor での高度な分析と機械学習を活用してて、アプリケーション、ネットワーク、およびインフラストラクチャ全体での状況を追跡します。 
- Azure ネットワーク アダプターを使用して Azure へのネットワーク接続を簡略化します。
- Azure Update Management を使用して仮想マシンを最新の状態に保ちます。

Azure ハイブリッド サービスは、次の構成で Windows サーバーと連携します。

- スタンドアロン物理サーバーと仮想マシン (VM)
- [Azure Stack HCI](https://docs.microsoft.com/azure-stack/operator/azure-stack-hci-overview) の認定を受けたハイパーコンバージド クラスターや、[Windows Server ソフトウェア定義 (WSSD)](https://www.microsoft.com/en-us/cloud-platform/software-defined-datacenter) プログラムを含むクラスター

ほとんどの Azure ハイブリッド サービスは Azure portal と 1 つか 2 つのダウンロードによって設定でき、その多くは Windows Admin Center に直接統合されており、簡略化されたセットアップ エクスペリエンスとサーバー中心のサービスのビューを提供します。

## <a name="azure-hybrid-services-tool"></a>Azure ハイブリッド サービス ツール

[Windows Admin Center](../understand/windows-admin-center.md) の Azure ハイブリッド サービス ツールは、統合されたすべての Azure サービスを一元管理されたハブに集約します。このハブでは、オンプレミスまたはハイブリッド環境に価値をもたらす、利用可能なすべての Azure サービスを簡単に見つけることができます。 

![Azure ハイブリッド サービス ツールを示している Windows Admin Center のスクリーンショット](../media/azure-services/ahs-discover.png)

Azure サービスが既に有効になっているサーバーに接続した場合、Azure ハイブリッド サービス ツールは、そのサーバーで有効になっているすべてのサービスを見渡せる 1 枚の窓ガラスとしてとして機能します。 Windows Admin Center 内の関連ツールへのアクセス、Azure サービスの詳細な管理のための Azure portal への移動、ドキュメントでの詳細確認などの作業を指先ひとつで簡単に実行できます。 

![サーバーに既にインストールされている Azure サービスを示す Windows Admin Center のスクリーンショット](../media/azure-services/ahs-dayN.png)

Azure ハイブリッド サービス ツールから、次の操作を実行できます。
- [Azure Backup](azure-backup.md) を使用して Windows Admin Center から Windows Server をバックアップする
- [Azure Site Recovery](azure-site-recovery.md) を使用して Windows Admin Center から Hyper-V 仮想マシンを保護する
- [Azure File Sync](azure-file-sync.md) を使用して、ファイル サーバーをクラウドと同期する
- [Azure Update Management](azure-update-management.md) を使用して、オンプレミスとクラウド両方のすべての Windows サーバーについてオペレーティング システムの更新プログラムを管理する
- [Azure Monitor](azure-monitor.md) を使用して、オンプレミスとクラウドの両方でサーバーを監視し、アラートを構成する
- [Azure ネットワーク アダプター](https://aka.ms/WACNetworkAdapter)を使用してオンプレミス サーバーを Azure Virtual Network に接続する

## <a name="services-for-stand-alone-servers-and-vms"></a>スタンドアロン サーバーおよび VM 向けのサービス

これは、スタンドアロン サーバーと VM に機能を提供する Azure サービスの完全な一覧です。

- **(新規) [Azure File Sync](https://aka.ms/afs) を使用してファイル サーバーをクラウドと同期する**  
このサーバー上のファイルを Azure ファイル共有と同期します。 すべてのファイルをローカルに保持するか、クラウド階層化を使用して、最も頻繁に使用されるファイルのみをサーバー上にキャッシュし、コールド データをクラウドに階層化します。 クラウド内のデータはバックアップ可能なため、オンプレミス サーバーのバックアップについて心配する必要はありません。 さらに、複数サイト同期により、複数のサーバー間で一連のファイルの同期を保つことができます。

- **[Azure Active Directory (Azure AD)](https://azure.microsoft.com/services/active-directory/) 認証を追加することによって Windows Admin Center にセキュリティ レイヤーを追加する**  
ゲートウェイへのアクセス時に Azure Active Directory (Azure AD) ID を使用して認証を行うようユーザーに要求することによって、さらにセキュリティ レイヤーを Windows Admin Center に追加できます。 Azure AD 認証では、条件付きアクセスや多要素認証など、Azure AD のセキュリティ機能も利用できます。  
詳細については、[Windows Admin Center 用の Azure AD 認証の構成](../configure/user-access-control.md#azure-active-directory)に関するページを参照してください。  

- **[Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) を使用して Hyper-V 仮想マシンを保護する**  
ビジネスに不可欠なインフラストラクチャが障害発生時に保護されるよう、VM で実行されているワークロードをレプリケートできます。 Windows Admin Center は、セットアップと、Hyper-V サーバーまたはクラスターへの仮想マシンのレプリケーションのプロセスを効率化し、Azure Site Recovery のディザスター リカバリー サービスによって環境の回復性を簡単に高められるようにします。  
詳細については、[Azure Site Recovery と Windows Admin Center を使用した VM の保護](azure-site-recovery.md)に関するページを参照してください。

- **[Azure Backup](https://docs.microsoft.com/azure/backup/backup-overview) を使用して Windows サーバーをバックアップする**  
Windows サーバーを Azure にバックアップして、偶発的または悪意のある削除、破損、およびランサムウェアからの保護に役立てることができます。  
詳細については、[Azure Backup を使用したサーバーのバックアップ](azure-backup.md)に関するページを参照してください。

- **[Azure Monitor for Virtual Machines](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview) を使用して、環境内のすべてのサーバーの電子メール アラートを監視および取得する**  
Virtual Machines Insights とも呼ばれる Azure Monitor を使用して、サーバーの正常性とイベントを監視したり、電子メール アラートを作成したり、環境全体のサーバー パフォーマンスの統合ビューを提供したり、特定のサーバーに接続しているアプリ、システム、サービスを視覚化したりできます。  
詳細については、[Azure Monitor へのサーバーの接続と電子メール通知の構成](azure-monitor.md)に関するページを参照してください。

- **[Azure Update Management](https://docs.microsoft.com/azure/automation/automation-update-management) を使用して、すべての Windows Server のオペレーティング システム更新プログラムを集中管理する**  
複数のサーバーや VM の更新プログラムやパッチをサーバー単位ではなく、1 か所から管理できます。 Azure Update Management では、利用可能な更新プログラムの状態を迅速に評価したり、必要な更新プログラムのインストールをスケジュールしたり、展開結果を確認して更新プログラムの正常適用を検証したりできます。 これは、サーバーが Azure VM か、他のクラウド プロバイダーによってホストされているか、それともオンプレミスかにかかわらず可能です。  
詳細については、[Azure Update Management 用のサーバーの構成](azure-update-management.md)に関するページを参照してください。

- **[Azure ネットワーク アダプター](https://aka.ms/WACNetworkAdapter)を使用してオンプレミス サーバーを Azure Virtual Network に接続する**  
Azure ネットワーク アダプターをオンプレミス サーバーに追加して、Azure Virtual Network へのサーバーの安全な接続に役立てることができます。  
詳細については、[オンプレミス Windows Server と Azure Virtual Network 間のポイント対サイト VPN 接続の構成](https://aka.ms/WACNetworkAdapter)に関するページを参照してください。

- **[Windows Admin Center](manage-azure-vms.md) を使用して Azure IaaS 仮想マシンを管理する**  
Windows Admin Center を使用すると、Azure VM だけでなくオンプレミス コンピューターを管理することができます。 Azure VNet に接続するように Windows Admin Center ゲートウェイを構成することによって、Windows Admin Center の一貫性があり、簡略化されたツールを使用して Azure 内の仮想マシンを管理できます。 詳細については、[Azure 内の VM を管理するための Windows Admin Center の構成](manage-azure-vms.md)に関するページを参照してください。

## <a name="services-for-clusters"></a>クラスターのためのサービス

これらは、クラスター全体に機能を提供する Azure サービスです (まだ Windows Admin Center に統合されていないものもあります)。

- [Azure Monitor を使用してハイパーコンバージド クラスターを監視する](../../../storage/storage-spaces/configure-azure-monitor.md)
- [Azure Site Recovery を使用して VM を保護する](azure-site-recovery.md)
- [クラスター クラウド監視を展開する](../../../failover-clustering/deploy-cloud-witness.md)

## <a name="see-also"></a>関連項目

- [Windows Admin Center を Azure に接続する](azure-integration.md)
- [Windows Admin Center を Azure に展開する](deploy-wac-in-azure.md)