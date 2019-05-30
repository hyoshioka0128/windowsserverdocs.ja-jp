---
title: Azure Stack HCI の概要
description: Azure Stack HCI は、検証済みハードウェアを使用して仮想化ワークロードをオンプレミスで実行するハイパーコンバージド Windows Server 2019 クラスターであり、必要に応じて、クラウド ベースのバックアップやサイトの復元のために Azure サービスに接続されます。 Azure Stack HCI ソリューションは、Microsoft 検証済みハードウェアを使用して最適なパフォーマンスと信頼性を確保するもので、NVMe ドライブ、永続的なメモリ、リモート ダイレクト メモリ アクセス (RDMA) ネットワークなどのテクノロジのサポートが含まれます。
ms.technology: storage
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 05/22/2019
ms.openlocfilehash: 92d600eeb833cd70bd714702b1fd950c4fe2cd87
ms.sourcegitcommit: b190fac4bfa5599751a60d3fc3b4c4a64dd9afd7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2019
ms.locfileid: "66008976"
---
# <a name="azure-stack-hci-overview"></a>Azure Stack HCI の概要

>適用対象:Windows Server 2019

Azure Stack HCI は、検証済みハードウェアを使用して仮想化ワークロードをオンプレミスで実行するハイパーコンバージド Windows Server 2019 クラスターであり、必要に応じて、クラウド ベースのバックアップやサイトの復元のために Azure サービスに接続されます。 Azure Stack HCI ソリューションは、Microsoft 検証済みハードウェアを使用して最適なパフォーマンスと信頼性を確保するもので、NVMe ドライブ、永続的なメモリ、リモート ダイレクト メモリ アクセス (RDMA) ネットワークなどのテクノロジのサポートが含まれます。

Azure Stack HCI は、いくつかの製品を組み合わせたソリューションです。

- OEM パートナーのハードウェア

- Windows Server 2019 Datacenter Edition

- Windows Admin Center

- Azure サービス (オプション)

![Azure Stack HCI は、さまざまなハードウェア パートナーから入手できる Microsoft のハイパーコンバージド ソリューションです。](media/AS_HCI_solution.png)

Azure Stack HCI は、さまざまなハードウェア パートナーから入手できる Microsoft のハイパーコンバージド ソリューションです。 Azure Stack HCI がニーズに最適なソリューションであるかどうかを判断するために、ハイパーコンバージド ソリューションに関する次のシナリオを検討してください。

- **古いハードウェアを更新する。** 古いサーバーと記憶域インフラストラクチャを置換し、既存の IT スキルとツールを使用して Windows および Linux 仮想マシンをオンプレミスとエッジで実行します。

- **仮想化ワークロードを統合する。** 効率的なハイパーコンバージド インフラストラクチャ上のレガシ アプリを統合します。 Microsoft Azure などのハイパー スケール データセンターの実行に使用するのと同等のクラウドの効率性を活用します。

- **ハイブリッド クラウド サービス用の Azure に接続する。** オフサイト バックアップ、サイトの復元、クラウド ベースの監視を含め、Azure のクラウド管理およびセキュリティ サービスへのアクセスを合理化します。

## <a name="the-azure-stack-family"></a>Azure Stack ファミリ

Azure Stack HCI は、Azure および Azure Stack ファミリの一部であり、Azure Stack と同様の、ソフトウェアによるコンピューティング、記憶域、およびネットワーク ソフトウェアが使用されています。 さまざまなソリューションの概要を次に示します。

- [Azure](https://azure.microsoft.com) - パブリック クラウド サービスを使用する
- [Azure Stack](https://azure.microsoft.com/overview/azure-stack) - クラウド サービスをオンプレミスで運用する
- [Azure Stack HCI](https://azure.microsoft.com/overview/azure-stack/hci) - 仮想化アプリをオンプレミスで実行する (必要に応じて Azure に接続する)

![Azure と Azure Stack ではクラウド サービスが実行され、Azure Stack HCI では仮想化アプリケーションがオンプレミスで実行される](media/azure_family.png)

|Azure: パブリック クラウド サービスを使用する|Azure Stack: クラウド サービスをオンプレミスで運用する|Azure Stack HCI: 仮想化アプリをオンプレミスで実行する|
|-----------------|-----------------|-----------------|
|既存のアプリを移行および最新化し、新規のクラウド ネイティブ アプリをビルドするためのオンデマンドのセルフ サービス コンピューティング リソース用。|整合性のある Azure サービスをオンプレミスで使用して、切断時に、または規制の要件を満たすために、クラウド アプリケーションをエッジでビルドして実行します。| 仮想化アプリケーションをオンプレミスで実行し、古いサーバー インフラストラクチャを置換して統合し、クラウド サービス用の Azure に接続します。|
|世界中の 54 地域で 100 を超えるサービスを利用できます。|Windows と Linux 用の Azure VM、Azure Web Apps と Azure Functions、Azure Key Vault、Azure Resource Manager、Azure Marketplace、コンテナー、Azure IoT と Event Hubs、管理ツール (プラン、サービス、RBAC)。|管理と Azure サービスへの統合アクセスのために、Windows Server 2019 および Windows Admin Center と共に Hyper V と記憶域スペース ダイレクトを利用した、検証済み HCI ソリューション。|

参考情報:

- 詳細については、[Azure Stack HCI](https://azure.microsoft.com/overview/azure-stack/hci) ソリューションの Web サイトを参照してください。
- Microsoft 専門家の Jeff Woolsey と Vijay Tewari による[新しい Azure Stack HCI ソリューションに関するディスカッション](https://aka.ms/AzureStackOverviewVideo)をご覧ください。

## <a name="hyperconverged-efficiencies"></a>ハイパーコンバージドの効率性

Azure Stack HCI ソリューションは、業界標準の x86 サーバーおよびコンポーネント上の高度に仮想化されたコンピューティング、記憶域、およびネットワークを 1 つにまとめたものです。 同じクラスター内のリソースを結合すると、デプロイ、管理、および拡張を簡単に行えるようになります。 選択したコマンドラインによる自動化、または Windows Admin Center を使用して、管理を行います。

Microsoft クラウドの基礎となるハイパーバイザー テクノロジである Hyper-V と、NVMe、永続的なメモリ、およびリモート ダイレクト メモリ アクセス (RDMA) ネットワークに対する組み込みサポートを備えた記憶域スペース ダイレクト テクノロジを使用して、サーバー アプリケーションに対して業界をリードする仮想マシンのパフォーマンスを実現します。

シールド仮想マシン、ネットワーク マイクロセグメンテーション、および保存時と転送時のデータのネイティブ暗号化を使用して、アプリとデータを安全に保ちます。

## <a name="hybrid-capabilities"></a>ハイブリッド機能

パブリック クラウド内のハイパーコンバージド インフラストラクチャ プラットフォームと連携することで、クラウドとオンプレミスを活用できます。 チームは、次の Azure インフラストラクチャ管理サービスへの組み込みの統合を使用して、クラウド スキルの構築を開始できます。

- Azure Site Recovery。高可用性と "サービスとしてのディザスター リカバリー" (DRaaS) を実現します。

- Azure Monitor。AI を利用した高度な分析によってアプリケーション、ネットワーク、およびインフラストラクチャ全体での状況を追跡する、集中管理ハブです。

- クラウド監視。クラスター クォーラムの軽量のタイ ブレーカーとして Azure を使用します。

- Azure Backup。オフサイト データの保護とランサムウェアからの保護を行います。

- Azure Update Management。Azure とオンプレミスで実行されている Windows VM に対して、更新の評価と更新のデプロイを行います。

- Azure ネットワーク アダプター。ポイント対サイト VPN 経由でオンプレミスのリソースを Azure の VM に接続します。

- Azure File Sync を使用して、ファイル サーバーをクラウドと同期します。

詳細については、[Azure ハイブリッド サービスへの Windows Server の接続](..\manage\windows-admin-center\azure\index.md)に関するページを参照してください。

## <a name="management-tools-and-system-center"></a>管理ツールと System Center

Azure Stack HCI では、Azure Stack と同様の、仮想化およびソフトウェアによる記憶域とネットワーク ソフトウェアが使用されています。 クラスターに対する完全な管理者権限が与えられた Azure Stack HCI では、[Windows Admin Center](..\manage\windows-admin-center\overview.md) と [System Center](https://www.microsoft.com/cloud-platform/system-center) のほか、[Hyper-V](../virtualization/hyper-v/hyper-v-on-windows-server.md)、[記憶域スペース ダイレクト](..\storage\storage-spaces\storage-spaces-direct-overview.md)、PowerShell や、5Nine Manager などのサードパーティ ツールの任意の機能を使用できます。

Microsoft Azure は、Windows Server や、Windows Server に含まれている Hyper-V と同じプラットフォーム上で実行されます。 Windows Server と System Center には、Microsoft Azure のようにグローバルなデータセンター ネットワークを運営する Microsoft の経験を活かした機能改善やベスト プラクティスが含まれています。そのためお客様は、ソフトウェアによるネットワーク テクノロジを使用する際に、Microsoft と同じテクノロジをデプロイして優れた柔軟性、自動化機能、および制御機能を実現できます。

System Center Virtual Machine Management (VMM) と System Center Operations Manager を使用して、インフラストラクチャをデプロイおよび管理します。 VMM では、仮想マシンとサービスを作成してプライベート クラウドにデプロイするのに必要なリソースをプロビジョニングおよび管理します。 Operations Manager では、早急な対応が必要な問題を識別するために、エンタープライズ全体でサービス、デバイス、および操作を監視します。

## <a name="hardware-partners"></a>ハードウェア パートナー

15 のパートナーから、Windows Server 2019 を実行する検証済み Azure Stack HCI ソリューションを購入できます。 ご希望の Microsoft パートナーが、設計やビルドに時間をかけずに稼働を開始し、実装およびサポート サービスのために単一の窓口を提供します。

次の Microsoft パートナーから現在入手できる、70 種類を超える Azure Stack HCI ソリューションについては、[Azure Stack HCI の Web サイト](https://azure.microsoft.com/overview/azure-stack/hci)を参照してください: ASUS、Axellio、bluechip、DataON、Dell EMC、Fujitsu、HPE、Hitachi、Huawei、Lenovo、NEC、primeLine Solutions、QCT、SecureGUARD、および Supermicro。

## <a name="faq"></a>FAQ

### <a name="what-do-azure-stack-and-azure-stack-hci-solutions-have-in-common"></a>Azure Stack ソリューションと Azure Stack HCI ソリューションの共通点は何ですか?

Azure Stack HCI ソリューションは、Azure Stack と同じ Hyper-V ベースの、ソフトウェアによるコンピューティング、記憶域、およびネットワーク テクノロジを備えています。 どちらのサービスも、信頼性と、基になるハードウェア プラットフォームとの互換性を確保するための、厳格なテストおよび検証条件を満たしています。

### <a name="how-are-they-different"></a>これらの違いは何ですか?

Azure Stack では、クラウド サービスをオンプレミスで運用します。 Azure IaaS サービスと PaaS サービスをオンプレミスで実行して、どこにいても一貫性のある方法でクラウド アプリケーションをビルドおよび実行することができます。これは Azure portal でオンプレミスで管理されます。

Azure Stack HCI では、仮想化ワークロードをオンプレミスで実行します。これは、Windows Admin Center と使い慣れた Windows Server ツールを使用して管理されます。 必要に応じて、クラウド ベースのサイトの復元、監視、およびその他のハイブリッド シナリオで Azure に接続できます。

### <a name="why-is-microsoft-bringing-its-hci-offering-to-the-azure-stack-family"></a>Microsoft がその HCI サービスを Azure Stack ファミリに追加する理由は何ですか?

Microsoft のハイパーコンバージド テクノロジは、既に Azure Stack の基盤となっています。

Microsoft の多くのお客様は複雑な IT 環境を備えており、弊社の目標は、適切なビジネス ニーズに合った適切なテクノロジを備えたソリューションを提供することです。 Azure Stack HCI は、Windows Server 2016 ベースの Windows Server Software-Defined (WSSD) ソリューションを進化させたもので、以前はハードウェア パートナーから入手できました。 弊社は、インフラストラクチャ管理サービス用に Azure とシームレスに接続する新しいオプションの提供を開始したため、Azure Stack HCI を Azure Stack ファミリに追加しました。

### <a name="does-azure-stack-hci-need-to-be-connected-to-azure"></a>Azure Stack HCI は Azure に接続する必要がありますか?

いいえ、完全に任意です。 オフサイトのバックアップやディザスター リカバリー、クラウド ベースの監視や更新の管理などのハイブリッド シナリオで、Azure との統合を活用できますが、これらは任意です。 切断された状態で実行することを希望するか、またはその必要がある場合、弊社は十分に理解したうえで対応します。

### <a name="how-does-azure-stack-hci-relate-to-windows-server"></a>Azure Stack HCI は Windows Server とどのように関連しますか?

Windows Server 2019 は、ほぼすべての Azure 製品の基盤です。 価値の認められる機能はすべて、Windows Server で引き続き採用され、サポートされます。 Azure Stack HCI は、HCI をオンプレミスでデプロイするのに推奨される方法であり、パートナーの Microsoft 検証済みハードウェアが使用されています。

### <a name="will-i-be-able-to-upgrade-from-azure-stack-hci-to-azure-stack"></a>Azure Stack HCI から Azure Stack にアップグレードすることはできますか? 

いいえ。ただし、お客様は Azure Stack HCI から Azure Stack または Azure にワークロードを移行できます。

### <a name="what-azure-services-can-i-connect-to-azure-stack-hci"></a>どの Azure サービスを Azure Stack HCI に接続できますか?

Azure Stack HCI を接続できる Azure サービスの最新のリストについては、[Azure ハイブリッド サービスへの Windows Server の接続](../azure-hybrid-services/index.md)に関するページを参照してください。

### <a name="how-does-the-cost-of-azure-stack-hci-compare-to-azure-stack"></a>Azure Stack と Azure Stack HCI のコストはどのように異なりますか? 

Azure Stack は、サービスとサポートを含む完全に統合されたシステムとして販売されています。 Azure Stack は、弊社のパートナーから、お客様が管理するシステムまたは完全に管理されたサービスとして購入できます。 ベース システムに加えて、Azure Stack または Azure で実行される Azure サービスは、従量課金制で販売されています。

Azure Stack HCI ソリューションは、従来の購入モデルに従います。 Azure Stack HCI パートナーから検証済みハードウェアを購入でき、既存のさまざまなチャネルからソフトウェア (ソフトウェアによるデータセンター機能を備えた Windows Server 2019 Datacenter Edition と、Windows Admin Center) を購入できます。 Windows Admin Center で使用できる Azure サービスについては、Azure サブスクリプションで課金されます。

### <a name="how-do-i-buy-azure-stack-hci-solutions"></a>Azure Stack HCI ソリューションを購入するにはどうすればよいですか?

次の手順に従います。

1. ご希望のハードウェア パートナーから、Microsoft 検証済みハードウェア システムを購入します。
1. 管理と、クラウド サービス用に Azure に接続する機能を目的として、Windows Server 2019 Datacenter Edition と Windows Admin Center をインストールします。
1. 必要に応じて Azure アカウントを使用して、クラウド ベースの管理およびセキュリティ サービスをワークロードにアタッチします。

![Azure Stack HCI ソリューションを購入するには、ハードウェア パートナーと、お客様のニーズに最適な構成を選択します。](media/howbuy_ashci.png)

## <a name="compare-azure-stack-and-azure-stack-hci"></a>Azure Stack と Azure Stack HCI を比較する

組織がデジタル変換を行うと、パブリック クラウド サービスを使用して最新のアーキテクチャ上に構築し、レガシ アプリケーションを更新することで、すばやい移行が可能になります。 ただし、技術や規制上の障害などが原因で、多くのワークロードをオンプレミスで保持する必要があります。 次の表では、必要なときに必要な機能を提供する Microsoft ハイブリッド クラウド戦略を確認できます。こうした戦略により、ワークロードが存在するすべての場所でクラウド イノベーションが実現されます。

|Azure Stack|Azure Stack HCI|
|--------|-------|
|新しいスキル、革新的なプロセス|同じスキル、使い慣れたプロセス|
|データセンター内の Azure サービス|データセンターを Azure サービスに接続|

### <a name="when-to-use-azure-stack"></a>Azure Stack を使用する場合

|Azure Stack|Azure Stack HCI|
|--------|-------|
|セルフ サービスの "サービスとしてのインフラストラクチャ" (IaaS) には、Azure Stack を使用します。この場合、併置されている複数のテナントに対する強力な分離と正確な使用状況の追跡およびチャージバックが可能です。 サービス プロバイダーおよびエンタープライズ プライベート クラウドに最適です。 Azure Marketplace のテンプレートです。|Azure Stack HCI では、マルチテナントはネイティブに適用または提供されません。|
|Web Apps、Functions、Event Hubs など、"サービスとしてのプラットフォーム" (PaaS) に依存するアプリをオンプレミスで開発および実行するには、Azure Stack を使用します。 これらのサービスは、Azure の場合とまったく同じように Azure Stack で実行され、整合性のあるハイブリッド開発およびランタイム環境が実現されます。|Azure Stack HCI では、PaaS サービスはオンプレミスで実行されません。
|コードとしてのインフラストラクチャなどの DevOps プラクティス、継続的統合と継続的デプロイ (CI/CD)、および Azure と整合性のある VM 拡張機能などの便利な機能を使用して、アプリのデプロイと操作を最新化するには、Azure Stack を使用します。 Dev チームと DevOps チームに最適です。|Azure Stack HCI には、DevOps ツールはネイティブに含まれません。

### <a name="when-to-use-azure-stack-hci"></a>Azure Stack HCI を使用する場合

|Azure Stack|Azure Stack HCI|
|---------------|---------------|
|Azure Stack には、最低 4 つのノードとその独自のネットワーク スイッチが必要です。|リモート オフィス/ブランチ オフィス (ROBO) の最小フットプリントを実現するには、Azure Stack HCI を使用します。 わずか 2 個のサーバー ノードとスイッチレス バックツーバック ネットワークから開始して、最大限のシンプルさと手頃な価格を実現できます。 ハードウェアの提供は、4 個のドライブと 64 GB のメモリから、ノードあたり 1 万ドル未満で開始できます。
|Azure Stack では、Azure との整合性を保つために Hyper-V の構成可能性と機能が制限されます。|Exchange、SharePoint、SQL Server などの従来のエンタープライズ アプリに対する実用本位の Hyper-V 仮想化、およびファイル サーバー、DNS、DHCP、IIS、AD などの Windows Server ロールの仮想化には、Azure Stack HCI を使用します。 シールド VM など、Hyper-V のすべての機能に無制限にアクセスできます。|
|Azure Stack では、これらのインフラストラクチャ テクノロジは公開されません。|アーキテクチャの大きな変更なしに、古い記憶域配列やネットワーク アプライアンスを、ソフトウェアによるインフラストラクチャに置き換えるには、Azure Stack HCI を使用します。 組み込みの記憶域スペース ダイレクトと、ソフトウェアによるネットワーク (SDN) により、Hyper-V 環境との摩擦のない統合が実現されます。|