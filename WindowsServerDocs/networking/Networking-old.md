---
title: ネットワーク
description: このトピックでは、Windows Server 2016 で利用できるソフトウェア定義ネットワークおよびネットワーク プラットフォーム テクノロジの概要について説明します。
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.date: 05/08/2018
ms.assetid: daaf6b61-5953-4c2d-b6b8-7c885b552646
manager: dougkim
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.openlocfilehash: 1cc30f239f1c4c9107ce0afcfb70647d43384949
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356785"
---
# <a name="networking"></a>ネットワーク

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

>[!TIP]
> 以前のバージョンの Windows Server に関する情報をお探しの場合は、 docs.microsoft.com の他の [Windows Server ライブラリ](/previous-versions/windows/)を参照してください。 また、[このサイトで検索して](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions)、具体的な情報を確認することもできます。

<img src="../media/landing-icons/network.png" style='float:left; padding:.5em;' alt="Icon depicting two networked computers"> ネットワークは、ソフトウェアで定義されたデータ\(センター\)のデータセンター (SDDC) プラットフォームの基本部分であり、 \(Windows\) Server 2016 では、組織のための完全に実現した SDDC ソリューション。

ネットワークをソフトウェアによって定義されたリソースとして管理する場合、アプリケーションのインフラストラクチャ要件を1回記述し、アプリケーションの実行場所 (オンプレミスまたはクラウド) を選択することができます。 

この一貫性により、アプリケーションの拡張が容易になり、アプリケーションをどこでもシームレスに実行できるだけでなく、セキュリティ、パフォーマンス、サービス品質、可用性のいずれについても等しい信頼性が実現されます。

>[!Note]
> Windows Server のダウンロードについては、「[Windows Server 評価版ソフトウェア](https://www.microsoft.com/evalcenter/evaluate-windows-server-technical-preview)」を参照してください。

Windows Server 2016 で追加された新しいネットワーク テクノロジは、次のとおりです。

- ソフトウェア定義ネットワーク:ネットワーク コント ローラーは、管理、構成、監視、およびデータ センター内の仮想および物理ネットワーク インフラストラクチャのトラブルシューティングを行う自動化の集中管理された、プログラミング可能なポイントを提供します。 ネットワーク コント ローラーを使用すると、ネットワーク機能の仮想化を使用して簡単に仮想マシンを展開する \(Vm\) ソフトウェアによる負荷分散の \(SLB\) インターネット、内部設置型、およびクラウド リソース間で必要なテナント接続オプションを提供するには、テナントと RAS ゲートウェイのネットワーク トラフィックの負荷を最適化するためにします。 ネットワーク コント ローラーを使用して Vm と HYPER-V のデータ センターのファイアウォールを管理するホスト。

- ネットワークプラットフォーム:既存のネットワークプラットフォームテクノロジの新機能を使用して、dns ポリシーを使用してクエリに対する dns サーバーの応答をカスタマイズしたり、リモートダイレクトメモリ\(アクセス\) RDMA とイーサネットトラフィックの組み合わせを処理する収束 NIC を使用したりすることができます。では、スイッチ埋め\(込み\)チーミングセットを使用して、RDMA nic に接続されている hyper-v 仮想\(スイッチ\)を作成し、ip アドレス管理 IPAM を使用して DNS ゾーンとサーバー、および DHCP と IP アドレスを管理します。

詳しくは、「[Windows Server によってサポートされているネットワークのシナリオ](windows-server-supported-networking-scenarios.md)」を参照してください。

以下の各セクションでは、SDN テクノロジとネットワーク プラットフォーム テクノロジについて説明します。

## <a name="software-defined-networking-technologies"></a>ソフトウェア定義ネットワーク テクノロジ

### <a name="software-defined-networking-40sdn41sdnsoftware-defined-networkingmd"></a>[ソフトウェア定義ネットワーク&#40;SDN&#41;](sdn/software-defined-networking.md)

このトピックでは、Windows Server、System Center、および Microsoft Azure で提供される SDN テクノロジについて説明します。

>[!NOTE]
>ネットワークコントローラーやソフトウェアの負荷分散ノード\(など\) 、SDN インフラストラクチャサーバーを実行する hyper-v ホストと仮想マシン vm の場合は、Windows Server 2016 Datacenter edition をインストールする必要があります。 SDN\-で制御されるネットワークに接続されているテナントのワークロード vm のみが含まれている hyper-v ホストの場合は、Windows Server 2016 Standard edition を実行できます。

### <a name="deploy-a-software-defined-network-infrastructure-using-scriptssdndeploydeploy-a-software-defined-network-infrastructure-using-scriptsmd"></a>[スクリプトを使用してソフトウェアで定義されたネットワークインフラストラクチャを展開する](sdn/deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)
このガイドは、テスト ラボ環境で仮想ネットワークとゲートウェイのネットワーク コント ローラーを展開する方法を説明します。

### <a name="network-controllersdntechnologiesnetwork-controllernetwork-controllermd"></a>[ネットワーク コントローラー](sdn/technologies/network-controller/Network-Controller.md)

ネットワーク コント ローラーは、管理、構成、監視、およびデータ センター内の仮想および物理ネットワーク インフラストラクチャのトラブルシューティングを行う自動化の集中管理された、プログラミング可能なポイントを提供します。

### <a name="software-load-balancing-40slb41-for-sdnsdntechnologiesnetwork-function-virtualizationsoftware-load-balancing-for-sdnmd"></a>[SDN のソフトウェア&#40;負荷&#41;分散 SLB](sdn/technologies/network-function-virtualization/software-load-balancing-for-sdn.md)

クラウド サービス プロバイダー \(Csp\) ソフトウェアによるネットワーク制御 (SDN) で Windows Server 2016 を展開する企業がソフトウェアの負荷分散を使用することと \(SLB\) をテナントと仮想ネットワークのリソース間でテナントのお客様のネットワーク トラフィックを均等に分散します。 Windows Server SLB により、同じワークロードをホストする複数のサーバーであり、高可用性とスケーラビリティを提供することです。

### <a name="ras-gateway-for-sdnsdntechnologiesnetwork-function-virtualizationras-gateway-for-sdnmd"></a>[SDN の RAS ゲートウェイ](sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)

RAS ゲートウェイは、ソフトウェア ベース、マルチ テナント、ボーダー ゲートウェイ プロトコル \(BGP\) Windows Server 2016 で対応のルーターがクラウド サービス プロバイダー用に設計された \(Csp\) と HYPER-V ネットワーク仮想化を使用して複数のテナント仮想ネットワークをホストしている企業です。 

### <a name="network-function-virtualizationsdntechnologiesnetwork-function-virtualizationnetwork-function-virtualizationmd"></a>[ネットワーク機能の仮想化](sdn/technologies/network-function-virtualization/Network-Function-Virtualization.md)

定義されているソフトウェアのデータ センター内のネットワーク ハードウェア アプライアンスで実行されている関数 \(ロード バランサー、ファイアウォール、ルーター、スイッチなど\) がますます仮想アプライアンスとして仮想化されています。 この「ネットワーク機能の仮想化」は、サーバーの仮想化とネットワーク仮想化の自然な流れです。

### <a name="datacenter-firewall-overviewsdntechnologiesnetwork-function-virtualizationdatacenter-firewall-overviewmd"></a>[Datacenter Firewall の概要](sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)

データ センターのファイアウォールとは、ネットワーク層、5 組 (プロトコル、発信元と宛先のポート番号、送信元と送信先の IP アドレス)、ステートフルなマルチ テナント ファイアウォールです。

## <a name="bkmk_networking"></a>ネットワークテクノロジ

以下では、Windows Server 2016 の各種ネットワーク テクノロジへのリンクを示します。

### <a name="whats-new-in-networkingnetworkingwhat-s-new-in-networkingmd"></a>[ネットワークの新機能](../networking/What-s-New-in-Networking.md)

以下の各セクションでは、Windows Server 2016 の新しいネットワーク テクノロジと、既存テクノロジに対する新機能について説明します。

### <a name="branchcachebranchcachebranchcachemd"></a>[BranchCache](branchcache/BranchCache.md)

BranchCache は、ワイド エリア ネットワーク \(WAN\) 帯域幅最適化テクノロジです。 ユーザーがリモート サーバー上のコンテンツをアクセスするときは、WAN の帯域幅を最適化、BranchCache は、ホストされたクラウド コンテンツ サーバーまたはと、WAN 経由ではなくローカルでコンテンツにアクセスするブランチ オフィスでコンピューターをクライアントに許可するブランチ オフィスの場所にコンテンツをキャッシュ メイン オフィスからコンテンツを取得します。

### <a name="core-network-guide-for-windows-server-2016core-network-guidecore-network-guide-windows-servermd"></a>[Windows Server 2016 のコアネットワークガイド](core-network-guide/core-network-guide-windows-server.md)

「コア ネットワーク ガイド」では、Windows Server ネットワークを展開する方法を説明します。また、「コア ネットワーク必携ガイド」ではネットワーク展開環境に機能を追加する方法について説明します。

### <a name="directaccessremoteremote-accessdirectaccessdirectaccessmd"></a>[DirectAccess](../remote/remote-access/directaccess/DirectAccess.md)

DirectAccess は、リモート ユーザーが組織のネットワーク リソースに接続するための機能です。 

DirectAccess のドキュメントは、Windows Server 2016 の目次で、「[リモート アクセスとサーバー管理](https://docs.microsoft.com/windows-server/remote/)」セクションの「[リモート アクセス](https://docs.microsoft.com/windows-server/remote/remote-access/remote-access)」を参照してください。 詳しくは、「[DirectAccess](../remote/remote-access/directaccess/DirectAccess.md)」を参照してください。

### <a name="domain-name-system-40dns41dnsdns-topmd"></a>[ドメインネームシステム&#40;DNS&#41;](dns/dns-top.md)

ドメイン ネーム システム \(DNS\) は業界標準の TCP/IP を構成するプロトコル群の 1 つと、まとめて DNS クライアントおよび DNS サーバー コンピューター名と IP アドレスのマッピングの名前解決サービスを提供コンピューターとユーザーにします。

### <a name="dynamic-host-configuration-protocol-40dhcp41technologiesdhcpdhcp-topmd"></a>[動的ホスト構成プロトコル&#40;DHCP&#41;](technologies/dhcp/dhcp-top.md)

動的ホスト構成プロトコル \(DHCP\) は自動的にインターネット プロトコルを提供するクライアント/サーバー プロトコル \(IP\) 、IP アドレスとその他のホストに関連するサブネット マスク、デフォルト ゲートウェイなどの構成情報。

### <a name="hyper-v-network-virtualizationsdntechnologieshyper-v-network-virtualizationhyper-v-network-virtualizationmd"></a>[Hyper-v ネットワーク仮想化](sdn/technologies/hyper-v-network-virtualization/Hyper-V-Network-Virtualization.md)

HYPER-V ネットワーク仮想化 \(HNV\) 、共有の物理ネットワーク インフラストラクチャ上に顧客のネットワーク仮想化を使用します。

### <a name="hyper-v-virtual-switchvirtualizationhyper-v-virtual-switchhyper-v-virtual-switchmd"></a>[Hyper-V 仮想スイッチ](../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md)

Hyper-V 仮想スイッチは、Hyper-V サーバーの役割をインストールすると Hyper-V マネージャーで使用できる、ソフトウェアベースのレイヤー 2 イーサネット ネットワーク スイッチです。 このスイッチには、仮想マシンを仮想ネットワークと物理ネットワークの両方に接続するための、プログラムで管理される拡張可能な機能が含まれています。 また、Hyper-V 仮想スイッチでは、セキュリティ、分離、およびサービスのレベルでポリシーを適用できます。 

Hyper-V 仮想スイッチのドキュメントは、Windows Server 2016 の目次で、「**仮想化**」セクションを参照してください。 詳しくは、「[Hyper-V 仮想スイッチの概要](../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md)」を参照してください。

### <a name="ip-address-management-40ipam41technologiesipamipam-topmd"></a>[IP アドレス管理&#40;IPAM&#41;](technologies/ipam/ipam-top.md)

IP アドレス管理 \(IPAM\) はエンド ツー エンドで計画、展開を有効にするためのツールの統合されたスイートの管理および監視機能豊富なユーザー エクスペリエンスと、IP アドレス インフラストラクチャです。 IPAM は、IP アドレス インフラストラクチャのサーバーおよびドメイン ネーム システムに自動的に検出 \(DNS\) 、ネットワーク上のサーバー中心的なインターフェイスからそれらを管理することができます。

### <a name="network-load-balancingtechnologiesnetwork-load-balancingmd"></a>[ネットワーク負荷分散](technologies/Network-Load-Balancing.md)

ネットワーク負荷分散 \(NLB\) 、TCP/IP ネットワーク プロトコルを使用して複数のサーバー間でトラフィックを分散します。 NLB でステートレスなことは SDN 以外の場合、インターネット インフォメーション サービスを実行する Web サーバーなどのアプリケーション \(IIS\), 、負荷の増加に応じてサーバーを追加して、拡張性がします。

### <a name="high-performance-networkingtechnologieshpnhpn-topmd"></a>[高パフォーマンスネットワーク](technologies/hpn/hpn-top.md)

Windows Server 2016 のネットワーク オフロードおよび最適化テクノロジには、ソフトウェアのみ (SO) の機能とテクノロジー、ソフトウェアとハードウェア (SH) の統合機能とテクノロジー、ハードウェアのみ (HO) の機能とテクノロジーがあります。

次のオフロードおよび最適化テクノロジのドキュメントも併せて参照してください。

- [収束ネットワークインターフェイスカード (NIC) 構成ガイド](technologies/conv-nic/cnic-top.md)
- [データセンターブリッジング (DCB)](technologies/dcb/dcb-top.md)
- [Virtual Receive Side Scaling (vRSS)](technologies/vrss/vrss-top.md)


### <a name="network-policy-servertechnologiesnpsnps-topmd"></a>[ネットワークポリシーサーバー](technologies/nps/nps-top.md)

ネットワーク ポリシー サーバー (NPS) を使用すると、接続要求の認証と承認を行うための組織全体のネットワーク アクセス ポリシーを作成して適用できます。

### <a name="network-shell-netshtechnologiesnetshnetshmd"></a>[ネットワーク シェル (netsh)](technologies/netsh/netsh.md)

ネットワークシェル\(の netsh\)ネットワークユーティリティを使用して、windows Server 2016 と windows 10 のネットワークテクノロジを管理できます。

### <a name="network-subsystem-performance-tuningtechnologiesnetwork-subsystemnet-sub-performance-topmd"></a>[ネットワークサブシステムのパフォーマンスチューニング](technologies/network-subsystem/net-sub-performance-top.md)

このトピックでは、サーバーワークロードに適したネットワークアダプターの選択、ネットワークインターフェイスの順序付け、ネットワーク関連のパフォーマンスカウンター、およびパフォーマンスチューニングのネットワークアダプターとその関連ネットワークテクノロジについて説明します。RSS を受信し、並行して\(、\)受信側と RSC を結合します。\) \(

### <a name="nic-teamingtechnologiesnic-teamingnic-teamingmd"></a>[NIC チーミング](technologies/nic-teaming/NIC-Teaming.md)

NIC チーミングには、物理イーサネット ネットワーク アダプターを 1 つまたは複数のソフトウェア ベースの仮想ネットワーク アダプターにグループ化することができます。 これらの仮想ネットワーク アダプターは、高速なパフォーマンスに加え、ネットワーク アダプターに障害が発生した場合のフォールト トレランスを提供します。

### <a name="quality-of-service-qos-policytechnologiesqosqos-policy-topmd"></a>[サービスの品質 (QoS) ポリシー](technologies/qos/qos-policy-top.md)

QoS プロファイルを作成し、その設定をグループポリシーとともに配布することで、QoS ポリシーを Active Directory インフラストラクチャ全体のネットワーク帯域幅を管理する一元的ポイントとして使用できます。

### <a name="remote-accessremoteremote-accessremote-accessmd"></a>[リモート アクセス](../remote/remote-access/remote-access.md)

DirectAccess や仮想プライベートネットワーク\(VPN\)などのリモートアクセステクノロジを使用して、リモートワーカーが内部ネットワークリソースに接続できるようにすることができます。 さらに、ローカルエリアネットワーク\(の LAN\)ルーティングおよび Web アプリケーションプロキシに対してリモートアクセスを使用できます。 Web アプリケーション プロキシには、企業ネットワーク内部の Web アプリケーション用のリバース プロキシ機能があり、ユーザーは任意のデバイスで企業ネットワーク外部から Web アプリケーションにアクセスできます。

リモート アクセスのドキュメントは、Windows Server 2016 の目次で、「[リモート アクセスとサーバー管理](https://docs.microsoft.com/windows-server/remote/)」セクションを参照してください。 詳細については、「[リモート アクセス](../remote/remote-access/remote-access.md)」を参照してください。

Web アプリケーション プロキシ (リモート アクセス サーバー ロールのロール サービス) の詳細については、「[Windows Server 2016 の Web アプリケーション プロキシ](https://docs.microsoft.com/windows-server/remote/remote-access/web-application-proxy/web-application-proxy-windows-server)」を参照してください。

### <a name="virtual-private-networking-vpnremoteremote-accessvpnvpn-topmd"></a>[仮想プライベート ネットワーク (VPN)](../remote/remote-access/vpn/vpn-top.md)

Windows Server 2016 において、**DirectAccess と VPN** は、**リモート アクセス** サーバー ロールのロール サービスです。

リモートアクセスを vpn サーバーとしてインストールする場合は、仮想プライベートネットワーク\(VPN\)を使用して、リモート従業員にインターネット経由で組織のネットワークへの接続を提供すると同時に、情報を保持することもできます。暗号化された接続でのプライバシー。

Windows Server 2016 のリモート アクセス VPN と Windows 10 クライアント コンピューターを使用することにより、Always On VPN を展開できるようになりました。 Always On VPN では、常時接続のリモート VPN クライアントを管理できます。また、リモート ワーカーは、組織ネットワークへの VPN に手動で接続、切断する必要がなくなり、利便性が向上します。

詳細については、「[Windows Server 2016 および Windows 10 のためのリモート アクセス Always On VPN 展開ガイド](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy)」を参照してください。

>[!NOTE]
>VPN のドキュメントは、Windows Server 2016 の目次で、「[リモート アクセスとサーバー管理](https://docs.microsoft.com/windows-server/remote/)」セクションの「[リモート アクセス](https://docs.microsoft.com/windows-server/remote/remote-access/remote-access)」を参照してください。

VPN の詳細については、「[仮想プライベート ネットワーク (VPN)](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/vpn-top)」を参照してください。

### <a name="windows-container-networkinghttpsdocsmicrosoftcomvirtualizationwindowscontainersmanage-containerscontainer-networking"></a>[Windows コンテナーネットワーク](https://docs.microsoft.com/virtualization/windowscontainers/manage-containers/container-networking)

Windows コンテナーのネットワークでは、業界の標準的なツールとワークフローを使用して、Windows 10 と Windows Server ホストの両方のコンテナー エンドポイントを接続するネットワークを作成および管理できます。 Windows コンテナーのネットワークは、プライベート、フラット L2、ルーティング L3 などの、複数のトポロジをサポートします。

また、windows ホストネットワークサービス\(の HNS\)と通信するプラグインを介して、Docker、Kubernetes、または windows PowerShell を使用してホスト上にローカルで作成できるオーバーレイもサポートされています。 ローカルエージェントを介して各\-ノードの HNS に通信することで、高レベルのオーケストレーションシステムを通じてマルチノードクラスターネットワークを作成および管理できます。

### <a name="windows-internet-name-service-winstechnologieswinswins-topmd"></a>[Windows インターネット ネーム サービス (WINS)](technologies/wins/wins-top.md)

Windows インターネット ネーム サービス (WINS) は、コンピューターの NetBIOS 名と IP アドレスを対応付け、コンピューター名の登録と解決を行う従来型サービスです。 WINS よりも DNS の使用をお勧めします。

## <a name="additional-resources"></a>その他のリソース

Windows Server 2016 以前のオペレーティング システムのネットワーク関連情報については、以下を参照してください。

- Windows Server 2012 および Windows Server 2012 R2 [ネットワークの概要](https://technet.microsoft.com/library/hh831357.aspx)
- Windows Server 2008 および Windows Server 2008 R2 [ネットワーク](https://technet.microsoft.com/library/cc753940)
- Windows Server 2003 [Windows server 2003/2003 R2](https://www.microsoft.com/download/details.aspx?id=53314)の提供終了コンテンツ
