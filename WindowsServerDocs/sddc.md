---
title: Windows Server ソフトウェア定義データ センター
Description: Windows Server SDDC の概要
ms.prod: windows-server
ms.technology: SDDC
ms.topic: get-started article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 06/04/2019
ms.localizationpriority: medium
ms.openlocfilehash: ceab6f99617bcb2e5581f6ea975ea8a71a2ea4b3
ms.sourcegitcommit: 145cf75f89f4e7460e737861b7407b5cee7c6645
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87409963"
---
# <a name="windows-server-software-defined-datacenter"></a>Windows Server のソフトウェアによるデータセンター

>適用先:Windows Server 2019、Windows Server 2016

![見出しの画像](media/sddc/heading.png)

## <a name="what-is-windows-server-software-defined-datacenter"></a>Windows Server ソフトウェア定義データ センターとは

ソフトウェア定義データ センター (SDDC) は、一般的に、すべてのインフラストラクチャが仮想化されているデータ センターを指す共通の業界用語です。 仮想化が鍵であり、データ センター内のハードウェアとソフトウェアを従来の 1 対 1 の比率を超えて展開できることを意味します。 ハードウェアをエミュレートするソフトウェア ハイパーバイザーによって、オペレーティング システムとアプリケーションは、物理ハードウェアから抽象化され、プロセッサ、メモリ、I/O、ネットワークの柔軟なリソース プールを形成するように多重化されます。

Microsoft による SDDC の実装は、この記事で説明する Windows Server テクノロジで構成されます。 ネットワークと記憶域を構築する仮想化プラットフォームを提供する Hyper-V ハイパーバイザーから始まります。 仮想化インフラストラクチャに固有の課題用に開発されたセキュリティ テクノロジは、内部および外部の脅威を軽減します。 Windows Server に組み込まれている PowerShell と、[System Center](https://docs.microsoft.com/system-center/) や [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) の追加により、プロビジョニング、展開、構成、管理をプログラミングして自動化することができます。

Windows Server と System Center に組み込まれているテクノロジは、Windows Server SDDC エクスペリエンスの主な構成要素です。 ただし、仮想化プラットフォームではありますが、その基盤として適切なハードウェアが必要です。 **Windows Server Software-Defined (WSSD) ソリューション**および **Azure Stack HCI ソリューション** プログラムに参加している Microsoft パートナーが、適切なハードウェアを入手し、0 日で稼働できるように企業を支援します。

![ビデオ アイコン](media/sddc/video.png)**[Microsoft の SDDC の詳細に関するビデオを見る](https://mva.microsoft.com/training-courses/whats-new-in-windows-server-2016-16457?l=YcsJR6sXC_1006218965)**

![ポスター アイコン](media/sddc/poster-ico.png)**[このページのポスター サイズの .pdf ファイルをダウンロードする](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/WindowsServerDocs/media/sddc/sddc_poster_0801417_ANSI-E.pdf)**

## <a name="azure-stack-hci-solutions"></a>Azure Stack HCI ソリューション

適切なハードウェア インフラストラクチャに基づいて Windows Server ソフトウェア定義データ センターを構築することは、成功への重要な第一歩です。 このため、Microsoft は 15 のパートナーと提携して、Microsoft によって検証済みの SDDC の設計と展開のためのベスト プラクティスを作成しました。

Microsoft パートナーは、Window Server 2019 (Azure Stack HCI プログラムを使用) および Windows Server 2016 (Windows Server Software-Defined (WSSD) プログラムを使用) と連携する一連の ソリューションを提供することで、高パフォーマンス、ハイパーコンバージドな記憶域およびネットワーク インフラストラクチャを実現します。 ハイパーコンバージド ソリューションは、業界標準のサーバーやコンポーネントのコンピューティング、記憶域、ネットワークをまとめて、データ センターのインテリジェンスとコントロールを強化します。

![学ぶアイコン](media/sddc/learn.png)**[Azure Stack HCI ソリューションの詳細](https://azure.microsoft.com/overview/azure-stack/hci)**

![学ぶアイコン](media/sddc/learn.png)**[WSSD ソリューションの詳細](https://www.microsoft.com/cloud-platform/software-defined-datacenter)**

## <a name="windows-server-virtualized-technologies"></a>Windows Server 仮想化テクノロジ ##

このトピックの残りの部分では、Windows Server SDDC テクノロジと、それぞれのドキュメントへのリンクを示します。 次の表に、テクノロジの一覧を示します。

![使用可能な Windows Server SDDC テクノロジ](media/sddc/table.png)

![Virtualize anything 見出しバー](media/sddc/virtualize.png)

### <a name="windows-server-hyper-converged"></a>Windows Server、ハイパーコンバージド

Windows Server 仮想化テクノロジには、Hyper-V、Hyper-V 仮想スイッチ、保護されたファブリックとシールドされた仮想マシン (VM) に対する更新が含まれており、セキュリティ、スケーラビリティ、信頼性が向上しています。 フェールオーバー クラスタリング、ネットワーク、記憶域に対する更新により、Hyper-V で使用する場合でも、これらのテクノロジの展開と管理が容易になっています。

![スペース専用の画像](media/sddc/spacer1.png)![Windows Server、ハイパーコンバージド インフラストラクチャの図](media/sddc/hyper-converged.png)

![学ぶアイコン](media/sddc/learn.png)**[Windows Server、ハイパーコンバージドの詳細](https://docs.microsoft.com/windows-server/get-started/what-s-new-in-windows-server-2016#computevirtualizationvirtualizationmd)**

### <a name="hyper-v-hypervisor"></a>Hyper-V Hypervisor

Hyper-V は、Windows 用のハイパーバイザー ベースの仮想化テクノロジです。 ハイパーバイザーは仮想化のコアです。 これは、プロセッサ固有の仮想化プラットフォームで、複数の独立したオペレーティング システムで、1 つのハードウェア プラットフォームを共有できるようにします。

![Hyper-V Hypervisor の図](media/sddc/spacer1.png)![Hyper](media/sddc/hypervisor.png)

![学ぶアイコン](media/sddc/learn.png)**[Hyper-V Hypervisor の詳細](https://www.microsoft.com/cloud-platform/server-virtualization)**

### <a name="guest-clustering-with-shared-vhdx"></a>共有 VHDX を使用したゲスト クラスタリング

![スペース専用の行の画像](media/sddc/virtualize-line.png)

共有 VHDX は、柔軟かつ安全で、基になる記憶域トポロジにバインドされていないため、基になる物理記憶域をゲスト OS に提供する必要がありません。 新しい共有 VHDX はオンラインでのサイズ変更をサポートしています。

![スペース専用の画像](media/sddc/spacer1.png)![ゲスト クラスタリングと共有 VHDX の図](media/sddc/cluster.png)

- 共有 VHDX は、ブロック記憶域または SMB ファイル ベースの記憶域のクラスター共有ボリューム (CSV) に保存できます。
- 保護:共有 VHDX は、Hyper-V レプリカとホスト レベルのバックアップをサポートします。

![学ぶアイコン](media/sddc/learn.png)**[共有 VHDX によるゲスト クラスタリングの詳細](https://technet.microsoft.com/library/dn281956(v=ws.11).aspx)**

### <a name="hyper-v-replica"></a>Hyper-V レプリカ

![スペース専用の行の画像](media/sddc/virtualize-line.png)

証明書を使用したネットワーク経由の統合ソフトウェア ベース VM レプリケーション。 どのサイトでも、サーバー、ネットワーク、記憶域のハードウェアにバインドされません。

![スペース専用の画像](media/sddc/spacer1.png)![Hyper-V レプリカの図](media/sddc/replica.png)

他の仮想マシンのレプリケーション テクノロジは必要ではないため、コストが削減されます。
- ライブ マイグレーションを自動的に処理します。
- シンプルな構成と管理。Hyper-V マネージャー、PowerShell、または Azure Site Recovery を使用します。

![学ぶアイコン](media/sddc/learn.png)**[Hyper-V レプリカの詳細](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/set-up-hyper-v-replica)**

![Connect everything バナー](media/sddc/networking.png)

### <a name="network-controller"></a>ネットワーク コントローラー

![スペース専用の行の画像](media/sddc/networking-line.png)

管理、構成、監視、およびデータ センター内の仮想および物理ネットワーク インフラストラクチャのトラブルシューティングを行う自動化の集中管理された、プログラミング可能なポイントです。

![スペース専用の画像](media/sddc/spacer1.png)![ネットワーク コント ローラーの図](media/sddc/netcontroller.png)

管理者は、ネットワーク コントローラーを直接操作できる管理ツールを使用しています。 ネットワーク コントローラーは、仮想インフラストラクチャと物理インフラストラクチャの両方を含む、ネットワーク インフラストラクチャに関する情報を管理ツールに提供します。

![学ぶアイコン](media/sddc/learn.png)**[ネットワーク コントローラーの詳細](https://docs.microsoft.com/windows-server/networking/sdn/technologies/network-controller/network-controller)**

### <a name="datacenter-firewall"></a>データ センターのファイアウォール

![スペース専用の行の画像](media/sddc/networking-line.png)

展開し、サービスとして提供するときに、インターネットおよびイントラネット ネットワークからの不要なトラフィックから仮想ネットワークを保護するために、テナント管理者は、ファイアウォール ポリシーをインストールして構成できます。

![スペース専用の画像](media/sddc/spacer1.png)![Datacenter Firewall の図](media/sddc/firewall.png)

サービス プロバイダーの管理者やテナント管理者は、ネットワーク コントローラーを介してデータ センターのファイアウォール ポリシーを管理できます。

![学ぶアイコン](media/sddc/learn.png)**[データ センターのファイアウォールの詳細](https://docs.microsoft.com/windows-server/networking/sdn/technologies/network-function-virtualization/datacenter-firewall-overview)**

### <a name="switch-embedded-teaming"></a>スイッチ埋め込みチーミング

![スペース専用の行の画像](media/sddc/networking-line.png)

SET は、Hyper-V と[ソフトウェアによるネットワーク制御 (SDN)](https://docs.microsoft.com/windows-server/networking/sdn/software-defined-networking) スタックが含まれる環境で使用できる代替 NIC チーミング ソリューションです。

![スペース専用の画像](media/sddc/spacer1.png)![スイッチが埋め込まれたチーミングの図](media/sddc/teaming.png)

![学ぶアイコン](media/sddc/learn.png)**[スイッチ埋め込みチーミングの詳細](https://docs.microsoft.com/windows-server/networking/sdn/technologies/set-for-sdn)**

### <a name="software-load-balancing"></a>ソフトウェア負荷分散

![スペース専用の行の画像](media/sddc/networking-line.png)

SLB により、複数のサーバーで同じワークロードをホストすることができ、高可用性とスケーラビリティを提供できます。 他の VM のワークロードに使用しているのと同じ Hyper-V サーバーで、SLB VM を使用して負荷分散機能をスケールアウトします。 SLB は、クラウド サービス プロバイダーの操作に必要な負荷分散エンドポイントの迅速な作成と削除をサポートしています。 さらに、SLB は、クラスターあたり数十ギガバイトをサポートし、シンプルなプロビジョニング モデルを提供することで、スケールアウトやスケールインが容易です。

![スペース専用の画像](media/sddc/spacer1.png)![ソフトウェア負荷分散の図](media/sddc/balancer.png)

![学ぶアイコン](media/sddc/learn.png)**[ソフトウェア負荷分散の詳細](https://docs.microsoft.com/windows-server/networking/sdn/technologies/network-function-virtualization/software-load-balancing-for-sdn)**

![記憶域の図](media/sddc/storage.png)

### <a name="storage-spaces-direct"></a>記憶域スペース ダイレクト

![スペース専用の行の記憶域画像](media/sddc/storage-line.png)

記憶域スペース ダイレクトは、業界標準のサーバーとローカルで接続されているドライブを使用して、従来の SAN や NAS アレイの何分の 1 かのコストで、可用性と拡張性が高いソフトウェア定義の記憶域を提供します。 そのアーキテクチャによって、根本的に調達と展開が簡略化されます。

![スペース専用の画像](media/sddc/spacer1.png)![記憶域スペース ダイレクトの図](media/sddc/ssd.png)

記憶域スペース ダイレクトは新しいソフトウェア記憶域バスを導入すると共に、現在の Windows Server でなじみのある多くの機能を利用しています。たとえば、フェールオーバー クラスタリング、クラスター共有ボリューム (CSV)、サーバー メッセージ ブロック (SMB) 3、記憶域スペースです。

![学ぶアイコン](media/sddc/learn.png)**[記憶域スペース ダイレクトの詳細](storage/storage-spaces/storage-spaces-direct-overview.md)**
### <a name="storage-quality-of-service"></a>記憶域のサービスの品質 (QoS) ###

![スペース専用の行](media/sddc/storage-line.png)

Hyper-V とスケールアウト ファイル サーバーの役割を使用して仮想マシンの記憶域のパフォーマンスを一元的に監視および管理することで、複数の仮想マシン間の記憶域リソースの公平性を向上させます。

![スペース専用の画像](media/sddc/spacer1.png)![記憶域のサービスの品質の図](media/sddc/qos.png)

記憶域の QoS は、スケールアウト ファイル サーバーおよび Hyper-V によって、SMB3 プロトコルを使用して提供されるマイクロソフトのソフトウェア定義記憶域ソリューションに組み込まれています。 新しいポリシー マネージャーは、記憶域のパフォーマンスの一元的な監視機能を提供します。

![学ぶアイコン](media/sddc/learn.png)**[記憶域の QoS の詳細](https://docs.microsoft.com/windows-server/storage/storage-qos/storage-qos-overview)**

### <a name="storage-replica"></a>記憶域レプリカ

![スペース専用の行の記憶域画像](media/sddc/storage-line.png)

障害回復と準備によってデータ損失ゼロを実現し、複数のデータ センターをより効率的に使用して、さまざまなラック、フロア、ビル、建物、大学の構内、都市、国にあるデータを同期的に保護できます。

![スペース専用の画像](media/sddc/spacer1.png)
![記憶域レプリカの図](media/sddc/storage-replica.png)

同期レプリケーション

1. アプリケーションがデータを書き込みます
2. ログ データが書き込まれ、データがリモート サイトにレプリケートされます
3. リモート サイトにログ データが書き込まれます
4. リモート サイトから確認が返されます
5. アプリケーションの書き込みが確認されます

t & t1 :データはボリュームにフラッシュされ、ログは常にライトスルーされます

![学ぶアイコン](media/sddc/learn.png)**[記憶域レプリカの詳細](https://docs.microsoft.com/windows-server/storage/storage-replica/storage-replica-overview)**

![セキュリティの図](media/sddc/security.png)

### <a name="guarded-fabric"></a>保護されたファブリック

![スペース専用の行のセキュリティ画像](media/sddc/security-line.png)

クラウド サービス プロバイダーやエンタープライズ プライベート クラウド管理者は、保護されたファブリックを使用して、セキュリティが強化された VM 環境を実現できます。 保護されたファブリックは、1 つホスト ガーディアン サービス (HGS)、通常は、3 ノードのクラスターと、1 つまたは複数の保護されたホスト、シールドされた仮想マシン (VM) のセットで構成されます。

![保護されたファブリックの図](media/sddc/spacer1.png)![保護されたファブリックの図](media/sddc/guarded-fabric.png)

![学ぶアイコン](media/sddc/learn.png)**[保護されたファブリックの詳細](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms)**

### <a name="shielded-vms"></a>シールドされた VM

![スペース専用の行のセキュリティ画像](media/sddc/security-line.png)

シールドされた VM のデータと状態は、マルウェアとデータ センター管理者の両方による検査、盗難、改ざんから保護されています。

![スペース専用の画像](media/sddc/spacer1.png)![シールドの図](media/sddc/shielded.png)

- シールドされた VM は、VM の所有者として指定されているファブリックでのみ実行されます。
- シールドされた VM は、指定された所有者だけが実行できるように、BitLocker またはその他の方法で暗号化されます。
- 実行中の VM をシールドされた VM に変換できます。

![学ぶアイコン](media/sddc/learn.png)**[シールドされた VM の詳細](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms)**

### <a name="host-guardian-service"></a>ホスト ガーディアン サービス

![スペース専用の行のセキュリティ画像](media/sddc/security-line.png)

ホスト ガーディアン サービスでは、暗号化された仮想マシンだけでなく、正当なファブリックへのキーを保持します。

![スペース専用の画像](media/sddc/spacer1.png)![ガーディアンの図](media/sddc/guardian.png)

![学ぶアイコン](media/sddc/learn.png)**[ホスト ガーディアン サービスの詳細](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-manage-hgs)**

### <a name="device-health-attestation"></a>デバイス正常性構成証明

![スペース専用の行のセキュリティ画像](media/sddc/security-line.png)

構成証明によって、企業は、運用コストへの影響が最小限またはなしで、ハードウェアの監視、保証されたセキュリティなど、自社組織のセキュリティ水準を引き上げることができます。

![スペース専用の画像](media/sddc/spacer1.png)![構成証明の図](media/sddc/attestation.png)

ハードウェア信頼モードでは、上記のように、TPM v2.0 ハードウェア ルート信頼とキー リリースのためのコード整合性ポリシーへの準拠によって、最も高いレベルの保証が提供されます。

![学ぶアイコン](media/sddc/learn.png)**[デバイス正常性構成証明の詳細](https://docs.microsoft.com/windows-server/security/device-health-attestation)**

![管理の図](media/sddc/management.png)

### <a name="powershell-desired-state-configuration"></a>PowerShell Desired State Configuration

![スペース専用の行の管理画像](media/sddc/management-line.png)

Windows PowerShell Desired State Configuration は、オープン スタンダードに基づく、Windows に組み込まれた構成管理プラットフォームです。 DSC は、展開ライフサイクル (開発、テスト、実稼働前、実稼働) の各段階、およびスケールアウト中に、機能の信頼性と一貫性を維持するために十分な柔軟性があります。

![スペース専用の画像](media/sddc/spacer1.png)![Desired State Configuration の図](media/sddc/dsc.png)

DSC は、破綻することなく構成を何度も展開できるように、"継続的な展開" をサポートしています。

-  DSC 構成は、迅速な展開のために、元の設定から変更された設定のみを適用します。
-  DSC は、オンプレミス、パブリックまたはプライベート クラウド環境で使用できます。
-  ターゲット システムで PowerShell スクリプトを実行できる限り、Microsoft または Microsoft 以外のソリューションに DSC を統合できます。

![学ぶアイコン](media/sddc/learn.png)**[PowerShell DSC の詳細](https://docs.microsoft.com/powershell/dsc/overview)**

### <a name="system-center-vmm"></a>System Center VMM

![スペース専用の行の管理画像](media/sddc/management-line.png)

Virtual Machine Manager は、System Center スイートの一部であり、従来のデータ センターを構成、管理、変換し、オンプレミス、サービス プロバイダー、および Azure のクラウドの間で統一された管理エクスペリエンスを提供します。

![スペース専用の画像](media/sddc/spacer1.png)![Virtual Machine Manager の図](media/sddc/vmm.png)

- データ センター:VMM で 1 つのファブリックとしてデータ センターのコンポーネントを管理します。
- 仮想化ホスト:VMM は、Hyper-V および VMware 仮想化ホストとクラスターを追加、プロビジョニング、管理できます。
- ネットワーク:VMM は、仮想ネットワークとネットワーク ゲートウェイの作成と管理のサポートを含め、ネットワーク仮想化を提供します。
- ストレージ:VMM は、ローカルおよびリモートの記憶域を検出、分類、プロビジョニングし、割り当てることができます。

![学ぶアイコン](media/sddc/learn.png)**[System Center VMM の詳細](https://docs.microsoft.com/system-center/vmm/)**

### <a name="windows-admin-center"></a>Windows Admin Center

![スペース専用の行の管理画像](media/sddc/management-line.png)

Windows Admin Center は、Azure またはクラウドに依存せずに、Windows サーバーのオンプレミス管理を実現する、ローカルに展開されたブラウザー ベースの管理ツール セットです。 Windows Admin Center によって、IT 管理者はサーバー インフラストラクチャのあらゆる側面を完全に管理できるようになります。特に、インターネットに接続されていないプライベート ネットワークでの管理に便利です。

![スペース専用の画像](media/sddc/spacer1.png)![アーキテクチャの図](media/sddc/architecture.png)

Web サーバーを DNS に公開して、企業ファイアウォールを設定することによって、パブリック インターネットから Windows Admin Center にアクセスできるようになり、あらゆる場所から Microsoft Edge や Google Chrome を使ってサーバーに接続し、管理できます。

![学ぶアイコン](media/sddc/learn.png)**[Windows Admin Center の詳細](manage/windows-admin-center/overview.md)**
