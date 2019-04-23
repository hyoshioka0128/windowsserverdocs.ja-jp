---
title: ネットワーク
description: このトピックでは、Windows Server 2016 で利用できるソフトウェア定義ネットワークおよびネットワーク プラットフォーム テクノロジの概要について説明します。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.date: 05/08/2018
ms.assetid: daaf6b61-5953-4c2d-b6b8-7c885b552646
manager: dougkim
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.openlocfilehash: 7caa99f1b6b9e25e5a6f2c4333b033fb3088195d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862593"
---
# <a name="networking"></a>ネットワーク

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

>[!TIP]
> 以前のバージョンの Windows Server に関する情報をお探しの場合は、 docs.microsoft.com の他の [Windows Server ライブラリ](/previous-versions/windows/)を参照してください。 また、[このサイトで検索して](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions)、具体的な情報を確認することもできます。

<img src="../media/landing-icons/network.png" style='float:left; padding:.5em;' alt="Icon depicting two networked computers"> ネットワークが定義されているデータ センターの基礎の一部\(SDDC\)プラットフォーム、および Windows Server 2016 は、ソフトウェアによるネットワーク制御新規および改良された\(SDN\)に移動するのに役立つテクノロジ組織の完全に実現された SDDC ソリューションです。

定義されているソフトウェアのリソースとネットワークを管理するときに、1 回限り、アプリケーションのインフラストラクチャ要件を記述およびを選択し、アプリケーションを実行する - 内部設置型またはクラウドにします。 

この一貫性により、アプリケーションの拡張が容易になり、アプリケーションをどこでもシームレスに実行できるだけでなく、セキュリティ、パフォーマンス、サービス品質、可用性のいずれについても等しい信頼性が実現されます。

>[!Note]
> Windows Server のダウンロードについては、「[Windows Server 評価版ソフトウェア](https://www.microsoft.com/evalcenter/evaluate-windows-server-technical-preview)」を参照してください。

Windows Server 2016 で追加された新しいネットワーク テクノロジは、次のとおりです。

- ソフトウェアには、ネットワークが定義されています。ネットワーク コント ローラーは、管理、構成、監視、およびデータ センター内の仮想および物理ネットワーク インフラストラクチャのトラブルシューティングを行う自動化の集中管理された、プログラミング可能なポイントを提供します。 ネットワーク コント ローラーを使用すると、ネットワーク機能の仮想化を使用して簡単に仮想マシンを展開する \(Vm\) ソフトウェアによる負荷分散の \(SLB\) インターネット、内部設置型、およびクラウド リソース間で必要なテナント接続オプションを提供するには、テナントと RAS ゲートウェイのネットワーク トラフィックの負荷を最適化するためにします。 ネットワーク コント ローラーを使用して Vm と HYPER-V のデータ センターのファイアウォールを管理するホスト。

- ネットワーク プラットフォーム:既存のネットワーク プラットフォーム テクノロジの新機能を使用して、できるポリシーを使用する DNS クエリには、DNS サーバーの応答をカスタマイズするには、リモート ダイレクト メモリ アクセスがハンドルにまとめられることの収束の NIC を使用して\(RDMA\)とイーサネットのトラフィック、スイッチ埋め込みチーミングを使用して、\(設定\)枚の RDMA Nic に接続されている HYPER-V 仮想スイッチを作成して IP アドレスの管理を使用する\(IPAM\) DNS ゾーンおよびサーバーだけでなく、DHCP および IP アドレスを管理します。

詳しくは、「[Windows Server によってサポートされているネットワークのシナリオ](windows-server-supported-networking-scenarios.md)」を参照してください。

以下の各セクションでは、SDN テクノロジとネットワーク プラットフォーム テクノロジについて説明します。

## <a name="software-defined-networking-technologies"></a>ソフトウェア定義ネットワーク テクノロジ

### <a name="software-defined-networking-40sdn41sdnsoftware-defined-networkingmd"></a>[ソフトウェア定義ネットワーク&#40;SDN&#41;](sdn/software-defined-networking.md)

このトピックでは、Windows Server、System Center、および Microsoft Azure で提供される SDN テクノロジについて説明します。

>[!NOTE]
>HYPER-V ホストとバーチャル マシンの\(Vm\)ノード ネットワーク コント ローラーとソフトウェアの負荷分散など、SDN インフラストラクチャ サーバーを実行するインストール必要となる Windows Server 2016 Datacenter edition。 HYPER-V ホストのみが含まれているテナントの SDN に接続されているワークロード Vm\-制御のネットワークでは、Windows Server 2016 Standard edition を実行することができます。

### <a name="deploy-a-software-defined-network-infrastructure-using-scriptssdndeploydeploy-a-software-defined-network-infrastructure-using-scriptsmd"></a>[スクリプトを使用してソフトウェア定義ネットワーク インフラストラクチャをデプロイします。](sdn/deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)
このガイドは、テスト ラボ環境で仮想ネットワークとゲートウェイのネットワーク コント ローラーを展開する方法を説明します。

### <a name="network-controllersdntechnologiesnetwork-controllernetwork-controllermd"></a>[ネットワーク コント ローラー](sdn/technologies/network-controller/Network-Controller.md)

ネットワーク コント ローラーは、管理、構成、監視、およびデータ センター内の仮想および物理ネットワーク インフラストラクチャのトラブルシューティングを行う自動化の集中管理された、プログラミング可能なポイントを提供します。

### <a name="software-load-balancing-40slb41-for-sdnsdntechnologiesnetwork-function-virtualizationsoftware-load-balancing-for-sdnmd"></a>[ソフトウェアの負荷分散&#40;SLB&#41; SDN の](sdn/technologies/network-function-virtualization/software-load-balancing-for-sdn.md)

クラウド サービス プロバイダー \(Csp\) ソフトウェアによるネットワーク制御 (SDN) で Windows Server 2016 を展開する企業がソフトウェアの負荷分散を使用することと \(SLB\) をテナントと仮想ネットワークのリソース間でテナントのお客様のネットワーク トラフィックを均等に分散します。 Windows Server SLB により、同じワークロードをホストする複数のサーバーであり、高可用性とスケーラビリティを提供することです。

### <a name="ras-gateway-for-sdnsdntechnologiesnetwork-function-virtualizationras-gateway-for-sdnmd"></a>[SDN の RAS ゲートウェイ](sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)

RAS ゲートウェイは、ソフトウェア ベース、マルチ テナント、ボーダー ゲートウェイ プロトコル \(BGP\) Windows Server 2016 で対応のルーターがクラウド サービス プロバイダー用に設計された \(Csp\) と HYPER-V ネットワーク仮想化を使用して複数のテナント仮想ネットワークをホストしている企業です。 

### <a name="network-function-virtualizationsdntechnologiesnetwork-function-virtualizationnetwork-function-virtualizationmd"></a>[ネットワーク関数仮想化](sdn/technologies/network-function-virtualization/Network-Function-Virtualization.md)

定義されているソフトウェアのデータ センター内のネットワーク ハードウェア アプライアンスで実行されている関数 \(ロード バランサー、ファイアウォール、ルーター、スイッチなど\) がますます仮想アプライアンスとして仮想化されています。 この「ネットワーク機能の仮想化」は、サーバーの仮想化とネットワーク仮想化の自然な流れです。

### <a name="datacenter-firewall-overviewsdntechnologiesnetwork-function-virtualizationdatacenter-firewall-overviewmd"></a>[データ センターのファイアウォールの概要](sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)

データ センターのファイアウォールとは、ネットワーク層、5 組 (プロトコル、発信元と宛先のポート番号、送信元と送信先の IP アドレス)、ステートフルなマルチ テナント ファイアウォールです。

## <a name="bkmk_networking"></a>ネットワーク テクノロジ

以下では、Windows Server 2016 の各種ネットワーク テクノロジへのリンクを示します。

### <a name="whats-new-in-networkingnetworkingwhat-s-new-in-networkingmd"></a>[ネットワークの新機能新機能](../networking/What-s-New-in-Networking.md)

以下の各セクションでは、Windows Server 2016 の新しいネットワーク テクノロジと、既存テクノロジに対する新機能について説明します。

### <a name="branchcachebranchcachebranchcachemd"></a>[BranchCache](branchcache/BranchCache.md)

BranchCache は、ワイド エリア ネットワーク \(WAN\) 帯域幅最適化テクノロジです。 ユーザーがリモート サーバー上のコンテンツをアクセスするときは、WAN の帯域幅を最適化、BranchCache は、ホストされたクラウド コンテンツ サーバーまたはと、WAN 経由ではなくローカルでコンテンツにアクセスするブランチ オフィスでコンピューターをクライアントに許可するブランチ オフィスの場所にコンテンツをキャッシュ メイン オフィスからコンテンツを取得します。

### <a name="core-network-guide-for-windows-server-2016core-network-guidecore-network-guide-windows-servermd"></a>[Windows Server 2016 用のコア ネットワーク ガイド](core-network-guide/core-network-guide-windows-server.md)

「コア ネットワーク ガイド」では、Windows Server ネットワークを展開する方法を説明します。また、「コア ネットワーク必携ガイド」ではネットワーク展開環境に機能を追加する方法について説明します。

### <a name="directaccessremoteremote-accessdirectaccessdirectaccessmd"></a>[DirectAccess](../remote/remote-access/directaccess/DirectAccess.md)

DirectAccess は、リモート ユーザーが組織のネットワーク リソースに接続するための機能です。 

DirectAccess のドキュメントは、Windows Server 2016 の目次で、「[リモート アクセスとサーバー管理](https://docs.microsoft.com/windows-server/remote/)」セクションの「[リモート アクセス](https://docs.microsoft.com/windows-server/remote/remote-access/remote-access)」を参照してください。 詳しくは、「[DirectAccess](../remote/remote-access/directaccess/DirectAccess.md)」を参照してください。

### <a name="domain-name-system-40dns41dnsdns-topmd"></a>[ドメイン ネーム システム&#40;DNS&#41;](dns/dns-top.md)

ドメイン ネーム システム \(DNS\) は業界標準の TCP/IP を構成するプロトコル群の 1 つと、まとめて DNS クライアントおよび DNS サーバー コンピューター名と IP アドレスのマッピングの名前解決サービスを提供コンピューターとユーザーにします。

### <a name="dynamic-host-configuration-protocol-40dhcp41technologiesdhcpdhcp-topmd"></a>[動的ホスト構成プロトコル&#40;DHCP&#41;](technologies/dhcp/dhcp-top.md)

動的ホスト構成プロトコル \(DHCP\) は自動的にインターネット プロトコルを提供するクライアント/サーバー プロトコル \(IP\) 、IP アドレスとその他のホストに関連するサブネット マスク、デフォルト ゲートウェイなどの構成情報。

### <a name="hyper-v-network-virtualizationsdntechnologieshyper-v-network-virtualizationhyper-v-network-virtualizationmd"></a>[HYPER-V ネットワーク仮想化](sdn/technologies/hyper-v-network-virtualization/Hyper-V-Network-Virtualization.md)

HYPER-V ネットワーク仮想化 \(HNV\) 、共有の物理ネットワーク インフラストラクチャ上に顧客のネットワーク仮想化を使用します。

### <a name="hyper-v-virtual-switchvirtualizationhyper-v-virtual-switchhyper-v-virtual-switchmd"></a>[Hyper-V Virtual Switch](../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md)

Hyper-V 仮想スイッチは、Hyper-V サーバーの役割をインストールすると Hyper-V マネージャーで使用できる、ソフトウェアベースのレイヤー 2 イーサネット ネットワーク スイッチです。 このスイッチには、仮想マシンを仮想ネットワークと物理ネットワークの両方に接続するための、プログラムで管理される拡張可能な機能が含まれています。 また、Hyper-V 仮想スイッチでは、セキュリティ、分離、およびサービスのレベルでポリシーを適用できます。 

Hyper-V 仮想スイッチのドキュメントは、Windows Server 2016 の目次で、「**仮想化**」セクションを参照してください。 詳しくは、「[Hyper-V 仮想スイッチの概要](../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md)」を参照してください。

### <a name="ip-address-management-40ipam41technologiesipamipam-topmd"></a>[IP アドレス管理&#40;IPAM&#41;](technologies/ipam/ipam-top.md)

IP アドレス管理 \(IPAM\) はエンド ツー エンドで計画、展開を有効にするためのツールの統合されたスイートの管理および監視機能豊富なユーザー エクスペリエンスと、IP アドレス インフラストラクチャです。 IPAM は、IP アドレス インフラストラクチャのサーバーおよびドメイン ネーム システムに自動的に検出 \(DNS\) 、ネットワーク上のサーバー中心的なインターフェイスからそれらを管理することができます。

### <a name="network-load-balancingtechnologiesnetwork-load-balancingmd"></a>[ネットワーク負荷分散](technologies/Network-Load-Balancing.md)

ネットワーク負荷分散 \(NLB\) 、TCP/IP ネットワーク プロトコルを使用して複数のサーバー間でトラフィックを分散します。 NLB でステートレスなことは SDN 以外の場合、インターネット インフォメーション サービスを実行する Web サーバーなどのアプリケーション \(IIS\), 、負荷の増加に応じてサーバーを追加して、拡張性がします。

### <a name="high-performance-networkingtechnologieshpnhpn-topmd"></a>[高パフォーマンスのネットワーク](technologies/hpn/hpn-top.md)

Windows Server 2016 のネットワーク オフロードおよび最適化テクノロジには、ソフトウェアのみ (SO) の機能とテクノロジー、ソフトウェアとハードウェア (SH) の統合機能とテクノロジー、ハードウェアのみ (HO) の機能とテクノロジーがあります。

次のオフロードおよび最適化テクノロジのドキュメントも併せて参照してください。

- [収束ネットワーク インターフェイス カード (NIC) の構成ガイド](technologies/conv-nic/cnic-top.md)
- [データ センター ブリッジング (DCB)](technologies/dcb/dcb-top.md)
- [仮想 Receive Side Scaling (vRSS)](technologies/vrss/vrss-top.md)


### <a name="network-policy-servertechnologiesnpsnps-topmd"></a>[ネットワーク ポリシー サーバー](technologies/nps/nps-top.md)

ネットワーク ポリシー サーバー (NPS) を使用すると、接続要求の認証と承認を行うための組織全体のネットワーク アクセス ポリシーを作成して適用できます。

### <a name="network-shell-netshtechnologiesnetshnetshmd"></a>[ネットワーク シェル (Netsh)](technologies/netsh/netsh.md)

ネットワーク シェルを使用する\(netsh\)ネットワーク ユーティリティの Windows Server 2016 および Windows 10 でのネットワーク テクノロジを管理します。

### <a name="network-subsystem-performance-tuningtechnologiesnetwork-subsystemnet-sub-performance-topmd"></a>[ネットワーク サブシステムのパフォーマンス チューニング](technologies/network-subsystem/net-sub-performance-top.md)

このトピックでは、情報を提供しますサーバーの負荷を適切なネットワーク アダプターを選択すると、ネットワーク インターフェイスを順序付けには、ネットワーク関連のパフォーマンス カウンターおよびパフォーマンスのチューニングなどのネットワーク アダプターと、ネットワーク関連のテクノロジ。Receive Side Scaling \(RSS\)、受信側 Coalescing \(RSC\)、およびその他。

### <a name="nic-teamingtechnologiesnic-teamingnic-teamingmd"></a>[NIC チーミング](technologies/nic-teaming/NIC-Teaming.md)

NIC チーミングには、物理イーサネット ネットワーク アダプターを 1 つまたは複数のソフトウェア ベースの仮想ネットワーク アダプターにグループ化することができます。 これらの仮想ネットワーク アダプターは、高速なパフォーマンスに加え、ネットワーク アダプターに障害が発生した場合のフォールト トレランスを提供します。

### <a name="quality-of-service-qos-policytechnologiesqosqos-policy-topmd"></a>[サービス (QoS) ポリシーの品質](technologies/qos/qos-policy-top.md)

QoS プロファイルを作成し、その設定をグループポリシーとともに配布することで、QoS ポリシーを Active Directory インフラストラクチャ全体のネットワーク帯域幅を管理する一元的ポイントとして使用できます。

### <a name="remote-accessremoteremote-accessremote-accessmd"></a>[リモート アクセス](../remote/remote-access/remote-access.md)

DirectAccess と仮想プライベート ネットワークなどのリモート アクセス テクノロジを使用する\(VPN\)を内部ネットワーク リソースへの接続とリモート ワーカーを提供します。 ローカル エリア ネットワークのリモート アクセスを使用するさらに、 \(LAN\)ルーティング、および Web アプリケーション プロキシの。 Web アプリケーション プロキシには、企業ネットワーク内部の Web アプリケーション用のリバース プロキシ機能があり、ユーザーは任意のデバイスで企業ネットワーク外部から Web アプリケーションにアクセスできます。

リモート アクセスのドキュメントは、Windows Server 2016 の目次で、「[リモート アクセスとサーバー管理](https://docs.microsoft.com/windows-server/remote/)」セクションを参照してください。 詳細については、「[リモート アクセス](../remote/remote-access/remote-access.md)」を参照してください。

Web アプリケーション プロキシ (リモート アクセス サーバー ロールのロール サービス) の詳細については、「[Windows Server 2016 の Web アプリケーション プロキシ](https://docs.microsoft.com/windows-server/remote/remote-access/web-application-proxy/web-application-proxy-windows-server)」を参照してください。

### <a name="virtual-private-networking-vpnremoteremote-accessvpnvpn-topmd"></a>[仮想プライベート ネットワーク (VPN)](../remote/remote-access/vpn/vpn-top.md)

Windows Server 2016 において、**DirectAccess と VPN** は、**リモート アクセス** サーバー ロールのロール サービスです。

仮想プライベート ネットワークを使用するにはリモート アクセスを VPN サーバーとしてインストールするときに\(VPN\) - インターネット経由で情報を維持しながら、組織のネットワークに接続しているリモート従業員を提供するには暗号化された接続プライバシーを保護します。

Windows Server 2016 のリモート アクセス VPN と Windows 10 クライアント コンピューターを使用することにより、Always On VPN を展開できるようになりました。 Always On VPN では、常時接続のリモート VPN クライアントを管理できます。また、リモート ワーカーは、組織ネットワークへの VPN に手動で接続、切断する必要がなくなり、利便性が向上します。

詳細については、「[Windows Server 2016 および Windows 10 のためのリモート アクセス Always On VPN 展開ガイド](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy)」を参照してください。

>[!NOTE]
>VPN のドキュメントは、Windows Server 2016 の目次で、「[リモート アクセスとサーバー管理](https://docs.microsoft.com/windows-server/remote/)」セクションの「[リモート アクセス](https://docs.microsoft.com/windows-server/remote/remote-access/remote-access)」を参照してください。

VPN の詳細については、「[仮想プライベート ネットワーク (VPN)](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/vpn-top)」を参照してください。

### <a name="windows-container-networkinghttpsdocsmicrosoftcomvirtualizationwindowscontainersmanage-containerscontainer-networking"></a>[Windows コンテナーのネットワーク](https://docs.microsoft.com/virtualization/windowscontainers/manage-containers/container-networking)

Windows コンテナーのネットワークでは、業界の標準的なツールとワークフローを使用して、Windows 10 と Windows Server ホストの両方のコンテナー エンドポイントを接続するネットワークを作成および管理できます。 Windows コンテナーのネットワークは、プライベート、フラット L2、ルーティング L3 などの、複数のトポロジをサポートします。

Windows ホストのネットワーク サービスと通信するプラグインによって、Docker、Kubernetes、または Windows PowerShell を使用して、ホストにローカルで作成できるオーバーレイもサポートされています\(HNS\)します。 作成して複数の管理\-ローカル エージェントを各ノードの HNS を通じて通信することでより高いレベルのオーケストレーション システムを介してクラスター ネットワークのノード。

### <a name="windows-internet-name-service-winstechnologieswinswins-topmd"></a>[Windows インターネット ネーム サービス (WINS)](technologies/wins/wins-top.md)

Windows インターネット ネーム サービス (WINS) は、コンピューターの NetBIOS 名と IP アドレスを対応付け、コンピューター名の登録と解決を行う従来型サービスです。 WINS よりも DNS の使用をお勧めします。

## <a name="additional-resources"></a>その他のリソース

Windows Server 2016 以前のオペレーティング システムのネットワーク関連情報については、以下を参照してください。

- Windows Server 2012 および Windows Server 2012 R2 [ネットワークの概要](https://technet.microsoft.com/library/hh831357.aspx)
- Windows Server 2008 および Windows Server 2008 R2 [ネットワーク](https://technet.microsoft.com/library/cc753940)
- Windows Server 2003: 「[Windows Server 2003/2003 R2 の削除されたコンテンツ](https://www.microsoft.com/download/details.aspx?id=53314)」
