---
title: Windows Server を Azure ハイブリッド サービスに接続します。
description: Azure ハイブリッド サービスを使用して、クラウドに移行する Windows サーバーのオンプレミス展開を拡張できます。
ms.technology: manage
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 04/12/2019
ms.openlocfilehash: 625bd4b79d277dfaa81767cd781c2ba1316d637e
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297026"
---
# Windows Server を Azure ハイブリッド サービスに接続します。

>適用対象: Windows Server 2019、Windows Server 2016

Azure ハイブリッド サービスを使用して、クラウドに移行する Windows サーバーのオンプレミス展開を拡張できます。 これらのクラウド サービスでは、以下を含む、便利な関数の配列を提供します。

- 仮想マシンを保護し、Azure Site Recovery でクラウド ベースのバックアップと障害復旧 (あって/DR) を使用します。 
- アプリケーション、ネットワーク、およびインフラストラクチャと高度な分析と機械学習 Azure モニターでのヘルプの間で何が起こっているかを追跡します。 
- Azure ネットワーク アダプターを使用して Azure へのネットワーク接続を簡略化します。
- 仮想マシンを Azure Update Management による最新の状態に保ちます。

Azure ハイブリッド サービスは、次の構成で Windows サーバーで動作します。

- スタンドアロンの物理サーバーと仮想マシン (Vm)
- クラスター、ハイパーコンバージド クラスターの[Azure スタック HCI](../../../azure-stack-hci/index.md)、および[windows server software-defined (WSSD)](https://www.microsoft.com/en-us/cloud-platform/software-defined-datacenter)プログラムによって認定を含む

Azure portal とダウンロードまたは 2 を使って最も Azure のハイブリッド サービスをセットアップするときに、簡素化されたセットアップ エクスペリエンスとサービスのサーバーを中心としたビューを提供する Windows Admin Center に直接統合多くされます。

## Azure ハイブリッド サービス ツール

[Windows Admin Center](../understand/windows-admin-center.md)で Azure ハイブリッド サービス ツールは、オンプレミスまたはハイブリッドに価値を利用可能なすべての Azure サービスを簡単に検出できる一元的なハブに統合されたすべての Azure サービスを統合環境です。 

![Azure ハイブリッド サービス ツールを示す Windows Admin Center のスクリーン ショット](../media/azure-services/ahs-discover.png)

Azure サービスが既に有効になっていると、サーバーに接続する場合、Azure ハイブリッド サービス ツールは、そのサーバーで有効になっているすべてのサービスを確認するガラスの 1 つのウィンドウとして機能します。 Windows Admin Center 内で関連するツールを簡単に、すぐに利用できる、それらの Azure サービスまたは読み取りを複数のドキュメントとのより深い管理のための Azure portal 起動できます。 

![サーバーに既にインストールされている Azure サービスを示す Windows Admin Center のスクリーン ショット](../media/azure-services/ahs-dayN.png)

Azure ハイブリッド サービス ツールで、次の操作を実行できます。
- [Azure のバックアップ](azure-backup.md)と Windows Admin Center から、Windows Server をバックアップします。
- [Azure Site Recovery](azure-site-recovery.md)を使用した Windows Admin Center から HYPER-V 仮想マシンの保護します。
- [Azure ファイルの同期](azure-file-sync.md)を使用して、クラウドと、ファイル サーバーを同期します。
- すべての Windows サーバーのオペレーティング システムの更新プログラムの管理、オンプレミスまたは[Azure Update Management](azure-update-management.md)による、クラウド
- オンプレミス サーバーの監視またはクラウド、および[Azure モニター](azure-monitor.md)でアラートを構成します。
- [Azure ネットワーク アダプター](https://aka.ms/WACNetworkAdapter)での Azure の仮想ネットワークに、オンプレミス サーバーを接続します。

## スタンドアロン サーバーや Vm のサービス

これは、スタンドアロン サーバーや Vm に機能を提供する Azure サービスの完全な一覧を示します。

- **(新規)[Azure ファイル Sync](https://aka.ms/afs)を使用して、ファイル サーバー、クラウドとの同期します。**  
このサーバーとの Azure ファイル共有上のファイルを同期します。 すべてのファイルをローカルに保存または最も頻繁に使うコールド データをクラウドに階層化、サーバー上のファイルのみ使用してクラウド階層化とキャッシュします。 クラウド内のデータは、オンプレミス サーバー バックアップについて心配する必要がなくなるため、バックアップできます。 さらに、オンサイト マルチに同期できる一連のファイル間で同期複数のサーバー。

- **Windows Admin Center を[Azure Active Directory (Azure AD)](https://azure.microsoft.com/services/active-directory/)認証を追加することでセキュリティ層を追加します。**  
Windows Admin Center に追加のセキュリティ層を追加するには、ゲートウェイにアクセスする Azure Active Directory (Azure AD) の id を使用して認証をユーザーに要求します。 Azure AD 認証では、条件付きアクセスし、多要素認証などの Azure AD のセキュリティ機能を活用することもできます。  
詳しくは、次を参照してください[Windows Admin Center の認証を構成する Azure AD。](../configure/user-access-control.md#azure-active-directory) 。  

- **[Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)で HYPER-V 仮想マシンの保護します。**  
お客様のビジネスに不可欠なインフラストラクチャが障害発生時に保護されるように Vm で実行されているワークロードをレプリケートすることができます。 Windows Admin Center は、Azure Site Recovery の障害回復のサービスと環境の回復性の強化を容易にセットアップし、HYPER-V サーバーまたはクラスターでは、仮想マシンをレプリケートするプロセス効率化します。  
詳しくは、 [Azure Site Recovery と Windows Admin Center を使用した Vm を保護する](azure-site-recovery.md)を参照してください。

- **[Azure Backup](https://docs.microsoft.com/azure/backup/backup-overview) Windows サーバーをバックアップします。**  
Azure、偶発的なまたは悪意のある削除、破損、ランサムウェアからの保護をサポートする、Windows サーバーをバックアップすることができます。  
詳しくは、 [Azure Backup、サーバー バックアップ](azure-backup.md)を参照してください。

- **監視し、環境内[の仮想マシンを監視する Azure](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview)でのすべてのサーバーの電子メール アラートを取得します。**  
サーバーの正常性とイベントを監視をメール アラートを作成、環境全体にわたってサーバーのパフォーマンスの統合のビューを取得し、システムでは、アプリを視覚化 Azure モニター、仮想マシンのインサイトとも呼ばれますを使用して、サービスに接続されている、指定されました。サーバーです。  
詳しくは、[サーバーは、Azure のモニターを接続しメール通知を構成する](azure-monitor.md)を参照してください。

- **[Azure Update Management](https://docs.microsoft.com/azure/automation/automation-update-management)によるすべての Windows サーバーのオペレーティング システムの更新プログラムを集中管理します。**  
サーバーごとではなく、1 つの場所から更新プログラムと複数のサーバーと Vm 用の修正プログラムを管理できます。 Azure 更新プログラムの管理を迅速に利用可能な更新プログラムの状態を評価、必須の更新プログラムのインストールのスケジュールして正常に適用できる更新プログラムを確認する展開の結果を確認できます。 これは可能かどうか、その他のクラウド プロバイダーによってホストされている Azure Vm は、サーバーまたはオンプレミス。  
詳しくは、 [Azure の更新プログラムの管理のサーバーの構成](azure-update-management.md)を参照してください。

- **オンプレミス サーバーに接続すると、 [Azure ネットワーク アダプター](https://aka.ms/WACNetworkAdapter)の Azure Virtual Network**  
Azure ネットワーク アダプターは、Azure の仮想ネットワークにサーバーを安全に接続するために、オンプレミス サーバーを追加できます。  
詳しくは、[オンプレミスで Windows Server と Azure Virtual Network の間での VPN 接続の構成ポイントとサイト](https://aka.ms/WACNetworkAdapter)を参照してください。

- **[Windows Admin Center](manage-azure-vms.md)での Azure IaaS 仮想マシンの管理します。**  
Windows Admin Center を使用して、Azure Vm と同様、オンプレミスのコンピューターを管理することができます。 Azure VNet に接続する、Windows Admin Center ゲートウェイを構成すると、Windows Admin Center は、一貫性があり、シンプルなツールを使用して Azure の仮想マシンを管理できます。 詳しくは、 [Azure で Vm を管理する構成 Windows Admin Center](manage-azure-vms.md)を参照してください。

## クラスターのサービス

これらは、クラスター全体の機能を提供する Azure サービス (これらはすべて統合 Windows Admin Center にまだ)。

- [Azure モニターでのハイパーコンバージド クラスターを監視します。](../../../storage/storage-spaces/configure-azure-monitor.md)
- [Azure Site Recovery を使用した Vm を保護します。](azure-site-recovery.md)
- [クラスターのクラウド監視を展開します。](../../../failover-clustering/deploy-cloud-witness.md)

## 関連項目

- [Windows Admin Center を Azure に接続します。](azure-integration.md)
- [Azure で Windows Admin Center を展開します。](deploy-wac-in-azure.md)