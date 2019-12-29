---
title: Azure ハイブリッド サービスへの Windows Server の接続
description: Azure ハイブリッド サービスを使用して、Windows Server のオンプレミス展開をクラウドに拡張できます。
ms.technology: manage
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.localizationpriority: medium
ms.prod: windows-server
ms.date: 05/31/2019
ms.openlocfilehash: e76d1205c22d6ce484abc86ed5e3c74ac1010f29
ms.sourcegitcommit: e817a130c2ed9caaddd1def1b2edac0c798a6aa2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2019
ms.locfileid: "74945285"
---
# <a name="connecting-windows-server-to-azure-hybrid-services"></a>Azure ハイブリッド サービスへの Windows Server の接続

Azure ハイブリッド サービスを使用して、Windows Server のオンプレミス展開をクラウドに拡張できます。 これらのクラウド サービスには、オンプレミスの Azure への拡張や、Azure からの一元的な管理用に一連の便利な機能が用意されています。

![オンプレミスから Azure への拡張に関するオンプレミスからクラウドへの矢印と、Azure による一元的な管理に関するクラウドからオンプレミスへの矢印を示す図](../media/azure-services/hybrid-framing.png)

Windows Admin Center 内で Azure ハイブリッド サービスを使用すると、次のことができます。

- [仮想マシンを保護し、クラウドベースのバックアップとディザスター リカバリー (HA/DR) を使用します](#back-up-and-protect-your-on-premises-servers-and-vms)。  
- [ストレージによりオンプレミスの容量を拡張し、Azure におけるコンピューティングを実現し、Azure へのネットワーク接続を簡略化します](#extend-on-premises-capacity-with-azure)。
- [クラウドインテリジェント Azure 管理サービスを使用して、アプリケーション、ネットワーク、インフラストラクチャ全体での監視、管理、構成、およびセキュリティを一元化します](#centrally-manage-your-hybrid-environment-from-azure)。  

ほとんどの Azure ハイブリッド サービスは 1 つのアプリのダウンロードといくつかの手動構成の実行によって設定でき、その多くは Windows Admin Center に直接統合されており、簡略化されたセットアップ エクスペリエンスとサーバー中心のサービスのビューを提供します。 Windows Admin Center には Azure portal への便利なインテリジェント ハイパーリンクも備わっているため、接続された Azure リソースを確認できるだけでなく、ハイブリッド環境を一元的に表示することもできます。

## <a name="discover-integrated-services-in-the-azure-hybrid-services-tool"></a>Azure ハイブリッド サービス ツールで統合サービスを見つける

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
- [サーバー向け Azure Arc](https://docs.microsoft.com/azure/azure-arc/servers/overview) を使用して Azure Policy を通じてオンプレミスのサーバーにガバナンス ポリシーを適用する
- [Azure Security Center](https://docs.microsoft.com/azure/security-center/windows-admin-center-integration) を使用して、サーバーをセキュリティで保護し、高度な脅威防止を利用する
- [Azure ネットワーク アダプター](https://aka.ms/WACNetworkAdapter)を使用してオンプレミス サーバーを Azure Virtual Network に接続する
- [Azure の拡張されたネットワーク](https://go.microsoft.com/fwlink/?linkid=2109517&clcid=0x409)を使用して、Azure VM をお使いのオンプレミス ネットワークのようにする

## <a name="back-up-and-protect-your-on-premises-servers-and-vms"></a>オンプレミスのサーバーと VM のバックアップと保護

- **[Azure Backup](https://docs.microsoft.com/azure/backup/backup-overview) を使用して Windows サーバーをバックアップする**  
Windows サーバーを Azure にバックアップして、偶発的または悪意のある削除、破損、およびランサムウェアからの保護に役立てることができます。  
詳細については、[Azure Backup を使用したサーバーのバックアップ](azure-backup.md)に関するページを参照してください。

- **[Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) を使用して Hyper-V 仮想マシンを保護する**  
ビジネスに不可欠なインフラストラクチャが障害発生時に保護されるよう、VM で実行されているワークロードをレプリケートできます。 Windows Admin Center は、セットアップと、Hyper-V サーバーまたはクラスターへの仮想マシンのレプリケーションのプロセスを効率化し、Azure Site Recovery のディザスター リカバリー サービスによって環境の回復性を簡単に高められるようにします。  
詳細については、[Azure Site Recovery と Windows Admin Center を使用した VM の保護](azure-site-recovery.md)に関するページを参照してください。

- **[記憶域レプリカ](https://docs.microsoft.com/windows-server/storage/storage-replica/storage-replica-overview)を使用して Azure で VM への同期または非同期のブロックベースのレプリケーションを使用する**  
セカンダリ サーバーまたは VM への記憶域レプリカを使用して、サーバー間レベルでブロックベースまたはボリュームベースのレプリケーションを構成できます。 Windows Admin Center を使用すると、レプリケーション ターゲット専用の Azure VM を作成できます。これにより、新しい Azure VM 上でストレージを適切にサイズ設定し、構成することができます。  
詳細については、[記憶域レプリカを使用したサーバー間のレプリケーション](https://docs.microsoft.com/windows-server/storage/storage-replica/storage-replica-ui)に関する記事を参照してください。  

## <a name="extend-on-premises-capacity-with-azure"></a>Azure によるオンプレミス容量の拡張

### <a name="extend-storage-capacity"></a>記憶容量の拡張

- **[Azure File Sync](https://aka.ms/afs) を使用してファイル サーバーとクラウドを同期する**  
このサーバー上のファイルを Azure ファイル共有と同期します。 すべてのファイルをローカルに保持するか、クラウド階層化を使用して空き領域を増やし、最も頻繁に使用されるファイルのみをサーバー上にキャッシュし、コールド データをクラウドに階層化します。 クラウド内のデータはバックアップ可能なため、オンプレミス サーバーのバックアップについて心配する必要はありません。 さらに、複数サイト同期により、複数のサーバー間で一連のファイルの同期を保つことができます。
詳しくは、「[Azure File Sync を使用してファイル サーバーをクラウドと同期する](azure-file-sync.md)」をご覧ください。

- **[ストレージ移行サービス](https://docs.microsoft.com/windows-server/storage/storage-migration-service/overview)を使用して Azure でストレージを VM に移行する**  
ステップバイステップ ツールを使用して、Windows および Linux サーバー上のデータのインベントリを作成し、新しい Azure VM にデータを転送します。 Windows Admin Center では、転送元からデータを受信するように適切にサイズ設定され、構成されたジョブ用に新しい Azure VM を作成できます。  
詳細については、「[ストレージ移行サービスを使用してサーバーを移行する](https://docs.microsoft.com/windows-server/storage/storage-migration-service/migrate-data)」を参照してください。

### <a name="extend-compute-capacity"></a>計算容量の拡張

- **Windows Admin Center を離れずに新しい Azure 仮想マシンを作成する**  
Windows Admin Center 内の *[すべての接続]* ページから **[追加]** に移動し、 **[Azure VM]** の下で **[新規作成]** を選択します。 さらに、Azure VM をドメイン参加させて、このステップバイステップの作成ツール内からストレージを構成することもできます。

- **[クラウド監視](https://docs.microsoft.com/windows-server/failover-clustering/deploy-cloud-witness)を使用してフェールオーバー クラスター上で Azure を活用してクォーラムを形成する**  
2 ノード クラスター上でクォーラムを形成するために追加のハードウェアに投資する代わりに、Azure ストレージ アカウントを Azure Stack HCI クラスターまたはその他のフェールオーバー クラスターのクラスター監視機能として機能させることができます。  
詳細については、「[フェールオーバー クラスターのクラウド監視を展開する](https://docs.microsoft.com/windows-server/failover-clustering/deploy-cloud-witness)」を参照してください。  

### <a name="simplify-network-connectivity-between-your-on-premises-and-azure-networks"></a>オンプレミスのネットワークと Azure ネットワーク間のネットワーク接続の簡略化

- **[Azure ネットワーク アダプター](https://aka.ms/WACNetworkAdapter)を使用してオンプレミスのサーバーを Azure 仮想ネットワークに接続する**  
Windows Admin Center を使用すると、オンプレミスのサーバーから Azure 仮想ネットワークへのポイント対サイト VPN のセットアップが簡単になります。  

- **[Azure の拡張されたネットワーク](https://go.microsoft.com/fwlink/?linkid=2109517&clcid=0x409)を使用して、Azure VM をお使いのオンプレミス ネットワークのようにする**  
Windows Admin Center では、サイト間 VPN を設定し、オンプレミスの IP アドレスを Azure vNet に拡張して、IP アドレスの依存関係を損なうことなく、ワークロードを Azure により簡単に移行できます。

## <a name="centrally-manage-your-hybrid-environment-from-azure"></a>Azure からのハイブリッド環境の一元的管理

- **[Azure Monitor for Virtual Machines](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview) を使用して、環境内のすべてのサーバーの電子メール アラートを監視および取得する**  
Virtual Machines Insights とも呼ばれる Azure Monitor を使用して、サーバーの正常性とイベントを監視したり、電子メール アラートを作成したり、環境全体のサーバー パフォーマンスの統合ビューを提供したり、特定のサーバーに接続しているアプリ、システム、サービスを視覚化したりできます。 また、Windows Admin Center では、サーバーの正常性パフォーマンスやクラスターの正常性イベント用に既定の電子メール アラートを設定することもできます。  
詳細については、[Azure Monitor へのサーバーの接続と電子メール通知の構成](azure-monitor.md)に関するページを参照してください。

- **[Azure Update Management](https://docs.microsoft.com/azure/automation/automation-update-management) を使用して、すべての Windows Server のオペレーティング システム更新プログラムを集中管理する**  
複数のサーバーや VM の更新プログラムやパッチをサーバー単位ではなく、1 か所から管理できます。 Azure Update Management では、利用可能な更新プログラムの状態を迅速に評価したり、必要な更新プログラムのインストールをスケジュールしたり、展開結果を確認して更新プログラムの正常適用を検証したりできます。 これは、サーバーが Azure VM か、他のクラウド プロバイダーによってホストされているか、それともオンプレミスかにかかわらず可能です。  
詳細については、[Azure Update Management 用のサーバーの構成](azure-update-management.md)に関するページを参照してください。

- **[Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) を使用してセキュリティの状態を高め、高度な脅威防止を利用する**  
一元化されたインフラストラクチャ セキュリティ管理システムである Azure Security Center を使用すると、データ センターのセキュリティの状態を強化し、Azure 内であるかどうかやオンプレミスであるかどうかにかかわらず、クラウド内のハイブリッド ワークロード全体で高度な脅威防止を使用できます。 Windows Admin Center を使用すると、サーバーを簡単にセットアップして Azure Security Center に簡単に接続できます。  
詳細については、「[Azure Security Center と Windows Admin Center (プレビュー) の統合](https://docs.microsoft.com/azure/security-center/windows-admin-center-integration)」を参照してください。  

- **[サーバー向け Azure Arc](https://docs.microsoft.com/azure/azure-arc/servers/overview) と [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) を使用してハイブリッド環境全体にポリシーを適用してコンプライアンスを順守する**  
Azure からオンプレミスのサーバーのインベントリを作成し、サーバーを整理、管理します。 Azure Policy を使用してサーバーを管理し、RBAC を使用してアクセスを制御し、Azure から追加の管理サービスを有効にすることができます。  

## <a name="clusters-versus-stand-alone-servers-and-vms"></a>クラスター対スタンドアロン サーバーおよび VM

Azure ハイブリッド サービスは、次の構成で Windows サーバーと連携します。

- スタンドアロン物理サーバーと仮想マシン (VM)
- [Azure Stack HCI](../../../azure-stack-hci/index.md) の認定を受けたハイパーコンバージド クラスターや、[Windows Server ソフトウェア定義 (WSSD)](https://www.microsoft.com/cloud-platform/software-defined-datacenter) プログラムを含むクラスター

### <a name="services-for-stand-alone-servers-and-vms"></a>スタンドアロン サーバーおよび VM 向けのサービス

これは、スタンドアロン サーバーと VM に機能を提供する Azure サービスの完全な一覧です。

- [Azure Backup](azure-backup.md) を使用して Windows Admin Center から Windows Server をバックアップする
- [Azure Site Recovery](azure-site-recovery.md) を使用して Windows Admin Center から Hyper-V 仮想マシンを保護する
- [Azure File Sync](azure-file-sync.md) を使用して、ファイル サーバーをクラウドと同期する
- [Azure Update Management](azure-update-management.md) を使用して、オンプレミスとクラウド両方のすべての Windows サーバーについてオペレーティング システムの更新プログラムを管理する
- [Azure Monitor](azure-monitor.md) を使用して、オンプレミスとクラウドの両方でサーバーを監視し、アラートを構成する
- [サーバー向け Azure Arc](https://docs.microsoft.com/azure/azure-arc/servers/overview) を使用して Azure Policy を通じてオンプレミスのサーバーにガバナンス ポリシーを適用する
- [Azure Security Center](https://docs.microsoft.com/azure/security-center/windows-admin-center-integration) を使用して、サーバーをセキュリティで保護し、高度な脅威防止を利用する
- [Azure ネットワーク アダプター](https://aka.ms/WACNetworkAdapter)を使用してオンプレミス サーバーを Azure Virtual Network に接続する
- [Azure の拡張されたネットワーク](https://go.microsoft.com/fwlink/?linkid=2109517&clcid=0x409)を使用して、Azure VM をお使いのオンプレミス ネットワークのようにする

### <a name="services-for-clusters"></a>クラスターのためのサービス

これらは、クラスター全体に次の機能を提供する Azure サービスです。

- [Azure Monitor を使用してハイパーコンバージド クラスターを監視する](../../../storage/storage-spaces/configure-azure-monitor.md)
- [Azure Site Recovery を使用して VM を保護する](azure-site-recovery.md)
- [クラスター クラウド監視を展開する](../../../failover-clustering/deploy-cloud-witness.md)  

## <a name="other-azure-integrated-abilities-of-windows-admin-center"></a>Windows Admin Center のその他の Azure 統合機能

- **[Windows Admin Center](manage-azure-vms.md) で Azure VM 接続を追加する**  
Windows Admin Center を使用すると、Azure VM だけでなくオンプレミス コンピューターを管理することができます。 Azure VNet に接続するように Windows Admin Center ゲートウェイを構成することによって、Windows Admin Center の一貫性があり、簡略化されたツールを使用して Azure 内の仮想マシンを管理できます。  
詳細については、[Azure 内の VM を管理するための Windows Admin Center の構成](manage-azure-vms.md)に関するページを参照してください。

- **[Azure Active Directory (Azure AD)](https://azure.microsoft.com/services/active-directory/) 認証を追加することによって Windows Admin Center にセキュリティ レイヤーを追加する**  
ゲートウェイへのアクセス時に Azure Active Directory (Azure AD) ID を使用して認証を行うようユーザーに要求することによって、さらにセキュリティ レイヤーを Windows Admin Center に追加できます。 Azure AD 認証では、条件付きアクセスや多要素認証など、Azure AD のセキュリティ機能も利用できます。  
詳細については、[Windows Admin Center 用の Azure AD 認証の構成](../configure/user-access-control.md#azure-active-directory)に関するページを参照してください。  

- **Windows Admin Center に埋め込まれた [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview) から直接 Azure リソースを管理する**  
Azure Cloud Shell を利用し Windows Admin Center 内で Bash または PowerShell を取得して、Azure 管理タスクに簡単にアクセスできます。  
詳しくは、「[Azure Cloud Shell の概要](https://docs.microsoft.com/azure/cloud-shell/overview)」をご覧ください。


## <a name="see-also"></a>関連項目

- [Windows Admin Center を Azure に接続する](azure-integration.md)
- [Windows Admin Center を Azure に展開する](deploy-wac-in-azure.md)
