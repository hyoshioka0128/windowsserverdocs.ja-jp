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
ms.openlocfilehash: 5a90ad13a51a540c6c76adacb7df0225d642573a
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "80857195"
---
# <a name="windows-server-software-defined-datacenter"></a>Windows Server のソフトウェアによるデータセンター

>適用先:Windows Server 2019、Windows Server 2016

![](media/sddc/heading.png)

## <a name="what-is-windows-server-software-defined-datacenter"></a>Windows Server ソフトウェア定義データ センターとは

ソフトウェア定義データ センター (SDDC) は、一般的に、すべてのインフラストラクチャが仮想化されているデータ センターを指す共通の業界用語です。 仮想化が鍵であり、データ センター内のハードウェアとソフトウェアを従来の 1 対 1 の比率を超えて展開できることを意味します。 ハードウェアをエミュレートするソフトウェア ハイパーバイザーによって、オペレーティング システムとアプリケーションは、物理ハードウェアから抽象化され、プロセッサ、メモリ、I/O、ネットワークの柔軟なリソース プールを形成するように多重化されます。
 
Microsoft による SDDC の実装は、この記事で説明する Windows Server テクノロジで構成されます。 ネットワークと記憶域を構築する仮想化プラットフォームを提供する Hyper-V ハイパーバイザーから始まります。 仮想化インフラストラクチャに固有の課題用に開発されたセキュリティ テクノロジは、内部および外部の脅威を軽減します。 Windows Server に組み込まれている PowerShell と、[System Center](https://docs.microsoft.com/system-center/) や [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) の追加により、プロビジョニング、展開、構成、管理をプログラミングして自動化することができます。

Windows Server と System Center に組み込まれているテクノロジは、Windows Server SDDC エクスペリエンスの主な構成要素です。 ただし、仮想化プラットフォームではありますが、その基盤として適切なハードウェアが必要です。 **Windows Server Software-Defined (WSSD) ソリューション**および **Azure Stack HCI ソリューション** プログラムに参加している Microsoft パートナーが、適切なハードウェアを入手し、0 日で稼働できるように企業を支援します。

![](media/sddc/video.png) **[Microsoft SDDC の詳細に関するビデオを見る](https://mva.microsoft.com/training-courses/whats-new-in-windows-server-2016-16457?l=YcsJR6sXC_1006218965)**

![](media/sddc/poster-ico.png) **[このページのポスター サイズの .pdf ファイルをダウンロードする](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/WindowsServerDocs/media/sddc/sddc_poster_0801417_ANSI-E.pdf)**

![](media/sddc/spacer1.png)<a href="https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/WindowsServerDocs//media/sddc/sddc_poster_0801417_ANSI-E.pdf"><img src="media/sddc/poster.png"></a>

## <a name="azure-stack-hci-solutions"></a>Azure Stack HCI ソリューション

適切なハードウェア インフラストラクチャに基づいて Windows Server ソフトウェア定義データ センターを構築することは、成功への重要な第一歩です。 このため、Microsoft は 15 のパートナーと提携して、Microsoft によって検証済みの SDDC の設計と展開のためのベスト プラクティスを作成しました。

Microsoft パートナーは、Window Server 2019 (Azure Stack HCI プログラムを使用) および Windows Server 2016 (Windows Server Software-Defined (WSSD) プログラムを使用) と連携する一連の ソリューションを提供することで、高パフォーマンス、ハイパーコンバージドな記憶域およびネットワーク インフラストラクチャを実現します。 ハイパーコンバージド ソリューションは、業界標準のサーバーやコンポーネントのコンピューティング、記憶域、ネットワークをまとめて、データ センターのインテリジェンスとコントロールを強化します。

![](media/sddc/learn.png) **[Azure Stack HCI ソリューションの詳細](https://azure.microsoft.com/overview/azure-stack/hci)**

![](media/sddc/learn.png) **[WSSD ソリューションの詳細](https://www.microsoft.com/cloud-platform/software-defined-datacenter)**

## <a name="windows-server-virtualized-technologies"></a>Windows Server 仮想化テクノロジ ##

このトピックの残りの部分では、Windows Server SDDC テクノロジと、それぞれのドキュメントへのリンクを示します。 次の表に、テクノロジの一覧を示します。

![](media/sddc/table.png)

![](media/sddc/virtualize.png)

### <a name="windows-server-hyper-converged"></a>Windows Server、ハイパーコンバージド

Windows Server 仮想化テクノロジには、Hyper-V、Hyper-V 仮想スイッチ、保護されたファブリックとシールドされた仮想マシン (VM) に対する更新が含まれており、セキュリティ、スケーラビリティ、信頼性が向上しています。 フェールオーバー クラスタリング、ネットワーク、記憶域に対する更新により、Hyper-V で使用する場合でも、これらのテクノロジの展開と管理が容易になっています。

![](media/sddc/spacer1.png)![](media/sddc/hyper-converged.png)

![](media/sddc/learn.png) **[Windows Server、ハイパーコンバージドの詳細](https://docs.microsoft.com/windows-server/get-started/what-s-new-in-windows-server-2016#computevirtualizationvirtualizationmd)**

### <a name="hyper-v-hypervisor"></a>Hyper-V Hypervisor

Hyper-V は、Windows 用のハイパーバイザー ベースの仮想化テクノロジです。 ハイパーバイザーは仮想化のコアです。 これは、プロセッサ固有の仮想化プラットフォームで、複数の独立したオペレーティング システムで、1 つのハードウェア プラットフォームを共有できるようにします。

![](media/sddc/spacer1.png)![](media/sddc/hypervisor.png)

![](media/sddc/learn.png) **[Hyper-V Hypervisor の詳細](https://www.microsoft.com/cloud-platform/server-virtualization)**

### <a name="guest-clustering-with-shared-vhdx"></a>共有 VHDX を使用したゲスト クラスタリング

![](media/sddc/virtualize-line.png)

共有 VHDX は、柔軟かつ安全で、基になる記憶域トポロジにバインドされていないため、基になる物理記憶域をゲスト OS に提供する必要がありません。 新しい共有 VHDX はオンラインでのサイズ変更をサポートしています。

![](media/sddc/spacer1.png)![](media/sddc/cluster.png)

- 共有 VHDX は、ブロック記憶域または SMB ファイル ベースの記憶域のクラスター共有ボリューム (CSV) に保存できます。
- 保護:共有 VHDX は、Hyper-V レプリカとホスト レベルのバックアップをサポートします。

![](media/sddc/learn.png) **[共有 VHDX によるゲスト クラスタリングの詳細](https://technet.microsoft.com/library/dn281956(v=ws.11).aspx)**

### <a name="hyper-v-replica"></a>Hyper-V レプリカ

![](media/sddc/virtualize-line.png)

証明書を使用したネットワーク経由の統合ソフトウェア ベース VM レプリケーション。 どのサイトでも、サーバー、ネットワーク、記憶域のハードウェアにバインドされません。

![](media/sddc/spacer1.png)![](media/sddc/replica.png)

他の仮想マシンのレプリケーション テクノロジは必要ではないため、コストが削減されます。
- ライブ マイグレーションを自動的に処理します。
- シンプルな構成と管理。Hyper-V マネージャー、PowerShell、または Azure Site Recovery を使用します。

![](media/sddc/learn.png) **[Hyper-V レプリカの詳細](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/set-up-hyper-v-replica)**

![](media/sddc/networking.png)

### <a name="network-controller"></a>ネットワーク コントローラー

![](media/sddc/networking-line.png)

管理、構成、監視、およびデータ センター内の仮想および物理ネットワーク インフラストラクチャのトラブルシューティングを行う自動化の集中管理された、プログラミング可能なポイントです。

![](media/sddc/spacer1.png)![](media/sddc/netcontroller.png)

管理者は、ネットワーク コントローラーを直接操作できる管理ツールを使用しています。 ネットワーク コントローラーは、仮想インフラストラクチャと物理インフラストラクチャの両方を含む、ネットワーク インフラストラクチャに関する情報を管理ツールに提供します。

![](media/sddc/learn.png) **[ネットワーク コントローラーの詳細](https://docs.microsoft.com/windows-server/networking/sdn/technologies/network-controller/network-controller)**

### <a name="datacenter-firewall"></a>データ センターのファイアウォール

![](media/sddc/networking-line.png)

展開し、サービスとして提供するときに、インターネットおよびイントラネット ネットワークからの不要なトラフィックから仮想ネットワークを保護するために、テナント管理者は、ファイアウォール ポリシーをインストールして構成できます。

![](media/sddc/spacer1.png)![](media/sddc/firewall.png)

サービス プロバイダーの管理者やテナント管理者は、ネットワーク コントローラーを介してデータ センターのファイアウォール ポリシーを管理できます。

![](media/sddc/learn.png) **[データ センターのファイアウォールの詳細](https://docs.microsoft.com/windows-server/networking/sdn/technologies/network-function-virtualization/datacenter-firewall-overview)**

### <a name="switch-embedded-teaming"></a>スイッチ埋め込みチーミング

![](media/sddc/networking-line.png)

SET は、Hyper-V と[ソフトウェアによるネットワーク制御 (SDN)](https://docs.microsoft.com/windows-server/networking/sdn/software-defined-networking) スタックが含まれる環境で使用できる代替 NIC チーミング ソリューションです。

![](media/sddc/spacer1.png)![](media/sddc/teaming.png)

![](media/sddc/learn.png) **[スイッチ埋め込みチーミングの詳細](https://docs.microsoft.com/windows-server/networking/sdn/technologies/set-for-sdn)**

### <a name="software-load-balancing"></a>ソフトウェア負荷分散

![](media/sddc/networking-line.png)

SLB により、複数のサーバーで同じワークロードをホストすることができ、高可用性とスケーラビリティを提供できます。 他の VM のワークロードに使用しているのと同じ Hyper-V サーバーで、SLB VM を使用して負荷分散機能をスケールアウトします。 SLB は、クラウド サービス プロバイダーの操作に必要な負荷分散エンドポイントの迅速な作成と削除をサポートしています。 さらに、SLB は、クラスターあたり数十ギガバイトをサポートし、シンプルなプロビジョニング モデルを提供することで、スケールアウトやスケールインが容易です。

![](media/sddc/spacer1.png)![](media/sddc/balancer.png)

![](media/sddc/learn.png) **[ソフトウェア負荷分散の詳細](https://docs.microsoft.com/windows-server/networking/sdn/technologies/network-function-virtualization/software-load-balancing-for-sdn)**


![](media/sddc/storage.png)

### <a name="storage-spaces-direct"></a>記憶域スペース ダイレクト

![](media/sddc/storage-line.png)

記憶域スペース ダイレクトは、業界標準のサーバーとローカルで接続されているドライブを使用して、従来の SAN や NAS アレイの何分の 1 かのコストで、可用性と拡張性が高いソフトウェア定義の記憶域を提供します。 そのアーキテクチャによって、根本的に調達と展開が簡略化されます。

![各ノードにローカルに接続されているドライブが記憶域スペース ダイレクトによってクラスター レベルでプールされ、CSV を使用して VM からアクセスされます](media/sddc/spacer1.png)![](media/sddc/ssd.png)

記憶域スペース ダイレクトは新しいソフトウェア記憶域バスを導入すると共に、現在の Windows Server でなじみのある多くの機能を利用しています。たとえば、フェールオーバー クラスタリング、クラスター共有ボリューム (CSV)、サーバー メッセージ ブロック (SMB) 3、記憶域スペースです。

![](media/sddc/learn.png) **[記憶域スペース ダイレクトの詳細](storage/storage-spaces/storage-spaces-direct-overview.md)**
### <a name="storage-quality-of-service"></a>記憶域のサービスの品質 (QoS) ###

![](media/sddc/storage-line.png)

Hyper-V とスケールアウト ファイル サーバーの役割を使用して仮想マシンの記憶域のパフォーマンスを一元的に監視および管理することで、複数の仮想マシン間の記憶域リソースの公平性を向上させます。

![](media/sddc/spacer1.png)![](media/sddc/qos.png)

記憶域の QoS は、スケールアウト ファイル サーバーおよび Hyper-V によって、SMB3 プロトコルを使用して提供されるマイクロソフトのソフトウェア定義記憶域ソリューションに組み込まれています。 新しいポリシー マネージャーは、記憶域のパフォーマンスの一元的な監視機能を提供します。

![](media/sddc/learn.png) **[記憶域の QoS の詳細](https://docs.microsoft.com/windows-server/storage/storage-qos/storage-qos-overview)**

### <a name="storage-replica"></a>記憶域レプリカ


![](media/sddc/storage-line.png)

障害回復と準備によってデータ損失ゼロを実現し、複数のデータ センターをより効率的に使用して、さまざまなラック、フロア、ビル、建物、大学の構内、都市、国にあるデータを同期的に保護できます。

![](media/sddc/spacer1.png)
![](media/sddc/storage-replica.png)

同期レプリケーション

1. アプリケーションがデータを書き込みます
2. ログ データが書き込まれ、データがリモート サイトにレプリケートされます
3. リモート サイトにログ データが書き込まれます
4. リモート サイトから確認が返されます
5. アプリケーションの書き込みが確認されます

t & t1 :データはボリュームにフラッシュされ、ログは常にライトスルーされます

![](media/sddc/learn.png) **[記憶域レプリカの詳細](https://docs.microsoft.com/windows-server/storage/storage-replica/storage-replica-overview)**

![](media/sddc/security.png)

### <a name="guarded-fabric"></a>保護されたファブリック

![](media/sddc/security-line.png)

クラウド サービス プロバイダーやエンタープライズ プライベート クラウド管理者は、保護されたファブリックを使用して、セキュリティが強化された VM 環境を実現できます。 保護されたファブリックは、1 つホスト ガーディアン サービス (HGS)、通常は、3 ノードのクラスターと、1 つまたは複数の保護されたホスト、シールドされた仮想マシン (VM) のセットで構成されます。

![](media/sddc/spacer1.png)![](media/sddc/guarded-fabric.png)

![](media/sddc/learn.png) **[保護されたファブリックの詳細](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms)**

### <a name="shielded-vms"></a>シールドされた VM

![](media/sddc/security-line.png)

シールドされた VM のデータと状態は、マルウェアとデータ センター管理者の両方による検査、盗難、改ざんから保護されています。

![](media/sddc/spacer1.png)![](media/sddc/shielded.png)

- シールドされた VM は、VM の所有者として指定されているファブリックでのみ実行されます。
- シールドされた VM は、指定された所有者だけが実行できるように、BitLocker またはその他の方法で暗号化されます。
- 実行中の VM をシールドされた VM に変換できます。

![](media/sddc/learn.png) **[シールドされた VM の詳細](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms)**

### <a name="host-guardian-service"></a>ホスト ガーディアン サービス

![](media/sddc/security-line.png)

ホスト ガーディアン サービスでは、暗号化された仮想マシンだけでなく、正当なファブリックへのキーを保持します。

![](media/sddc/spacer1.png)![](media/sddc/guardian.png)

![](media/sddc/learn.png) **[ホスト ガーディアン サービスの詳細](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-manage-hgs)**

### <a name="device-health-attestation"></a>デバイス正常性構成証明

![](media/sddc/security-line.png)

構成証明によって、企業は、運用コストへの影響が最小限またはなしで、ハードウェアの監視、保証されたセキュリティなど、自社組織のセキュリティ水準を引き上げることができます。


![](media/sddc/spacer1.png)![](media/sddc/attestation.png)


ハードウェア信頼モードでは、上記のように、TPM v2.0 ハードウェア ルート信頼とキー リリースのためのコード整合性ポリシーへの準拠によって、最も高いレベルの保証が提供されます。


![](media/sddc/learn.png) **[デバイス正常性構成証明の詳細](https://docs.microsoft.com/windows-server/security/device-health-attestation)**

![](media/sddc/management.png)

### <a name="powershell-desired-state-configuration"></a>PowerShell Desired State Configuration

![](media/sddc/management-line.png)

Windows PowerShell Desired State Configuration は、オープン スタンダードに基づく、Windows に組み込まれた構成管理プラットフォームです。 DSC は、展開ライフサイクル (開発、テスト、実稼働前、実稼働) の各段階、およびスケールアウト中に、機能の信頼性と一貫性を維持するために十分な柔軟性があります。

![](media/sddc/spacer1.png)![](media/sddc/dsc.png)

DSC は、破綻することなく構成を何度も展開できるように、"継続的な展開" をサポートしています。

-  DSC 構成は、迅速な展開のために、元の設定から変更された設定のみを適用します。
-  DSC は、オンプレミス、パブリックまたはプライベート クラウド環境で使用できます。
-  ターゲット システムで PowerShell スクリプトを実行できる限り、Microsoft または Microsoft 以外のソリューションに DSC を統合できます。

![](media/sddc/learn.png) **[PowerShell DSC の詳細](https://docs.microsoft.com/powershell/dsc/overview)**


### <a name="system-center-vmm"></a>System Center VMM

![](media/sddc/management-line.png)

Virtual Machine Manager は、System Center スイートの一部であり、従来のデータ センターを構成、管理、変換し、オンプレミス、サービス プロバイダー、および Azure のクラウドの間で統一された管理エクスペリエンスを提供します。

![](media/sddc/spacer1.png)![](media/sddc/vmm.png)

- データ センター:VMM で 1 つのファブリックとしてデータ センターのコンポーネントを管理します。 
- 仮想化ホスト:VMM は、Hyper-V および VMware 仮想化ホストとクラスターを追加、プロビジョニング、管理できます。
- ネットワーク:VMM は、仮想ネットワークとネットワーク ゲートウェイの作成と管理のサポートを含め、ネットワーク仮想化を提供します。 
- ストレージ:VMM は、ローカルおよびリモートの記憶域を検出、分類、プロビジョニングし、割り当てることができます。

![](media/sddc/learn.png) **[System Center VMM の詳細](https://docs.microsoft.com/system-center/vmm/)**

### <a name="windows-admin-center"></a>Windows Admin Center

![](media/sddc/management-line.png)

Windows Admin Center は、Azure またはクラウドに依存せずに、Windows サーバーのオンプレミス管理を実現する、ローカルに展開されたブラウザー ベースの管理ツール セットです。 Windows Admin Center によって、IT 管理者はサーバー インフラストラクチャのあらゆる側面を完全に管理できるようになります。特に、インターネットに接続されていないプライベート ネットワークでの管理に便利です。

![](media/sddc/spacer1.png)![](media/sddc/architecture.png)

Web サーバーを DNS に公開して、企業ファイアウォールを設定することによって、パブリック インターネットから Windows Admin Center にアクセスできるようになり、あらゆる場所から Microsoft Edge や Google Chrome を使ってサーバーに接続し、管理できます。

![](media/sddc/learn.png) **[Windows Admin Center の詳細](manage/windows-admin-center/overview.md)**
