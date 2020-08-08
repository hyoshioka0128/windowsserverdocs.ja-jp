---
title: ネットワーク
description: このトピックでは、Windows Server 2016 で利用できるソフトウェア定義ネットワークおよびネットワーク プラットフォーム テクノロジの概要について説明します。
ms.topic: article
ms.date: 05/08/2018
ms.assetid: daaf6b61-5953-4c2d-b6b8-7c885b552646
manager: dougkim
ms.author: anpaul
author: AnirbanPaul
ms.localizationpriority: medium
ms.openlocfilehash: 30939a702f0856461e7b8a08af2dfd40b4a4456d
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997358"
---
# <a name="networking"></a>ネットワーク

> 適用先:Windows Server (半期チャネル)、Windows Server 2016

> [!TIP]
> 以前のバージョンの Windows Server に関する情報をお探しの場合は、 docs.microsoft.com の他の [Windows Server ライブラリ](/previous-versions/windows/)を参照してください。 また、[このサイトで検索して](/search/index?dataSource=previousVersions&search=Windows+Server)、具体的な情報を確認することもできます。

<img src="../media/landing-icons/network.png" style='float:left; padding:.5em;' alt="Icon depicting two networked computers"> ネットワークは、ソフトウェアによって定義されたデータセンターのデータセンター \( (sddc) プラットフォームの基本部分で \) あり、Windows Server 2016 では、 \( \) 組織で完全に実現された SDDC ソリューションへの移行を支援するために、ソフトウェア定義のネットワーク SDN テクノロジが新たに強化されています。

ネットワークをソフトウェアによって定義されたリソースとして管理する場合、アプリケーションのインフラストラクチャ要件を1回記述し、アプリケーションの実行場所 (オンプレミスまたはクラウド) を選択することができます。

この一貫性により、アプリケーションの拡張が容易になり、アプリケーションをどこでもシームレスに実行できるだけでなく、セキュリティ、パフォーマンス、サービス品質、可用性のいずれについても等しい信頼性が実現されます。

>[!Note]
> Windows Server のダウンロードについては、「[Windows Server 評価版ソフトウェア](https://www.microsoft.com/evalcenter/evaluate-windows-server-technical-preview)」を参照してください。

Windows Server 2016 は、次の新しいネットワーク テクノロジを追加します。

- ソフトウェアの定義済みのネットワーク: ネットワーク コント ローラーは、管理、構成、監視、およびデータ センター内の仮想および物理ネットワーク インフラストラクチャのトラブルシューティングを行う自動化の集中管理された、プログラミング可能なポイントを提供します。 ネットワーク コント ローラーを使用すると、ネットワーク機能の仮想化を使用して簡単に仮想マシンを展開する \(Vm\) ソフトウェアによる負荷分散の \(SLB\) インターネット、内部設置型、およびクラウド リソース間で必要なテナント接続オプションを提供するには、テナントと RAS ゲートウェイのネットワーク トラフィックの負荷を最適化するためにします。 ネットワーク コント ローラーを使用して Vm と HYPER-V のデータ センターのファイアウォールを管理するホスト。

- ネットワーク Platform: は、既存のネットワーク プラットフォーム テクノロジの新機能を使用して、できるポリシーを使用する DNS クエリには、DNS サーバーの応答をカスタマイズするには、ハンドルにリモート ダイレクト メモリ アクセスが組み合わされる収束 NIC を使用して \(RDMA\) とトラフィック、組み込みのチーミングのスイッチを使用して、イーサネット \(設定\) RDMA Nic に接続されている HYPER-V 仮想スイッチを作成して IP アドレスの管理を使用する \(IPAM\) DNS ゾーンおよびサーバーだけでなく、DHCP および IP アドレスを管理します。

詳しくは、「[Windows Server によってサポートされているネットワークのシナリオ](windows-server-supported-networking-scenarios.md)」を参照してください。

以下の各セクションでは、SDN テクノロジとネットワーク プラットフォーム テクノロジについて説明します。

## <a name="software-defined-networking-technologies"></a>ネットワークの定義のソフトウェア テクノロジ

### <a name="software-defined-networking-40sdn41"></a>[ソフトウェアで定義されたネットワーク &#40;SDN&#41;](sdn/software-defined-networking.md)

このトピックを使用すると、Windows Server、System Center および Microsoft Azure に用意されている SDN テクノロジについて説明します。

>[!NOTE]
>\( \) ネットワークコントローラーやソフトウェアの負荷分散ノードなど、SDN インフラストラクチャサーバーを実行する hyper-v ホストと仮想マシン vm の場合は、Windows Server 2016 Datacenter edition をインストールする必要があります。 SDN で制御されるネットワークに接続されているテナントのワークロード Vm のみが含まれている Hyper-v ホストの場合 \- は、Windows Server 2016 Standard edition を実行できます。

### <a name="deploy-a-software-defined-network-infrastructure-using-scripts"></a>[スクリプトを使用してソフトウェア定義ネットワーク インフラストラクチャを展開する](sdn/deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)
このガイドは、テスト ラボ環境で仮想ネットワークとゲートウェイのネットワーク コント ローラーを展開する方法を説明します。

### <a name="network-controller"></a>[ネットワーク コントローラー](sdn/technologies/network-controller/Network-Controller.md)

ネットワーク コント ローラーは、管理、構成、監視、およびデータ センター内の仮想および物理ネットワーク インフラストラクチャのトラブルシューティングを行う自動化の集中管理された、プログラミング可能なポイントを提供します。

### <a name="software-load-balancing-40slb41-for-sdn"></a>[SDN のソフトウェア負荷分散 &#40;SLB&#41;](sdn/technologies/network-function-virtualization/software-load-balancing-for-sdn.md)

クラウド サービス プロバイダー \(Csp\) ソフトウェアによるネットワーク制御 (SDN) で Windows Server 2016 を展開する企業がソフトウェアの負荷分散を使用することと \(SLB\) をテナントと仮想ネットワークのリソース間でテナントのお客様のネットワーク トラフィックを均等に分散します。 Windows Server SLB により、同じワークロードをホストする複数のサーバーであり、高可用性とスケーラビリティを提供することです。

### <a name="ras-gateway-for-sdn"></a>[SDN の RAS ゲートウェイ](sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)

RAS ゲートウェイは、ソフトウェア ベース、マルチ テナント、ボーダー ゲートウェイ プロトコル \(BGP\) Windows Server 2016 で対応のルーターがクラウド サービス プロバイダー用に設計された \(Csp\) と HYPER-V ネットワーク仮想化を使用して複数のテナント仮想ネットワークをホストしている企業です。

### <a name="network-function-virtualization"></a>[ネットワーク機能の仮想化](sdn/technologies/network-function-virtualization/Network-Function-Virtualization.md)

定義されているソフトウェアのデータ センター内のネットワーク ハードウェア アプライアンスで実行されている関数 \(ロード バランサー、ファイアウォール、ルーター、スイッチなど\) がますます仮想アプライアンスとして仮想化されています。 この「ネットワーク機能の仮想化」は、サーバーの仮想化とネットワーク仮想化の自然な流れです。

### <a name="datacenter-firewall-overview"></a>[Datacenter Firewall の概要](sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)

データ センターのファイアウォールとは、ネットワーク層、5 組 (プロトコル、発信元と宛先のポート番号、送信元と送信先の IP アドレス)、ステートフルなマルチ テナント ファイアウォールです。

## <a name="networking-technologies"></a><a name="bkmk_networking"></a>ネットワー キング テクノロジ

次の表は、Windows Server 2016 のネットワー キング テクノロジの一部へのリンクを提供します。

### <a name="whats-new-in-networking"></a>[ネットワークの新機能](../networking/What-s-New-in-Networking.md)

次のセクションを使用すると、新しいネットワーク テクノロジと Windows Server 2016 で既存のテクノロジに対する新機能を検出します。

### <a name="branchcache"></a>[BranchCache](branchcache/BranchCache.md)

BranchCache は、ワイド エリア ネットワーク \(WAN\) 帯域幅最適化テクノロジです。 ユーザーがリモート サーバー上のコンテンツをアクセスするときは、WAN の帯域幅を最適化、BranchCache は、ホストされたクラウド コンテンツ サーバーまたはと、WAN 経由ではなくローカルでコンテンツにアクセスするブランチ オフィスでコンピューターをクライアントに許可するブランチ オフィスの場所にコンテンツをキャッシュ メイン オフィスからコンテンツを取得します。

### <a name="core-network-guide-for-windows-server-2016"></a>[Windows Server 2016 用のコア ネットワーク ガイド](core-network-guide/core-network-guide-windows-server.md)

コア ネットワーク必携ガイドで配置をネットワークに機能を追加するとともに、コア ネットワーク ガイドと Windows Server ネットワークを展開する方法について説明します。

### <a name="directaccess"></a>[DirectAccess](../remote/remote-access/directaccess/DirectAccess.md)

DirectAccess は、リモート ユーザーが組織のネットワーク リソースに接続するための機能です。

DirectAccess のドキュメントは、Windows Server 2016 の目次で、「[リモート アクセスとサーバー管理](../remote/index.yml)」セクションの「[リモート アクセス](../remote/remote-access/remote-access.md)」を参照してください。 詳しくは、「[DirectAccess](../remote/remote-access/directaccess/DirectAccess.md)」を参照してください。

### <a name="domain-name-system-40dns41"></a>[ドメインネームシステム &#40;DNS&#41;](dns/dns-top.md)

ドメイン ネーム システム \(DNS\) は業界標準の TCP/IP を構成するプロトコル群の 1 つと、まとめて DNS クライアントおよび DNS サーバー コンピューター名と IP アドレスのマッピングの名前解決サービスを提供コンピューターとユーザーにします。

### <a name="dynamic-host-configuration-protocol-40dhcp41"></a>[動的ホスト構成プロトコル &#40;DHCP&#41;](technologies/dhcp/dhcp-top.md)

動的ホスト構成プロトコル \(DHCP\) は自動的にインターネット プロトコルを提供するクライアント/サーバー プロトコル \(IP\) 、IP アドレスとその他のホストに関連するサブネット マスク、デフォルト ゲートウェイなどの構成情報。

### <a name="hyper-v-network-virtualization"></a>[Hyper-v ネットワーク仮想化](sdn/technologies/hyper-v-network-virtualization/Hyper-V-Network-Virtualization.md)

Hyper-v ネットワーク仮想化 \( hnv を \) 使用すると、共有物理ネットワークインフラストラクチャ上で顧客ネットワークを仮想化することができます。 "" "

### <a name="hyper-v-virtual-switch"></a>[Hyper-V 仮想スイッチ](../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md)

Hyper-V 仮想スイッチは、Hyper-V サーバーの役割をインストールすると Hyper-V マネージャーで使用できる、ソフトウェアベースのレイヤー 2 イーサネット ネットワーク スイッチです。 このスイッチには、仮想マシンを仮想ネットワークと物理ネットワークの両方に接続するための、プログラムで管理される拡張可能な機能が含まれています。 また、Hyper-V 仮想スイッチでは、セキュリティ、分離、およびサービスのレベルでポリシーを適用できます。

Hyper-V 仮想スイッチのドキュメントは、Windows Server 2016 の目次で、「**仮想化**」セクションを参照してください。 詳しくは、「[Hyper-V 仮想スイッチの概要](../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md)」を参照してください。

### <a name="ip-address-management-40ipam41"></a>[IP アドレス管理 &#40;IPAM&#41;](technologies/ipam/ipam-top.md)

IP アドレス管理 \(IPAM\) はエンド ツー エンドで計画、展開を有効にするためのツールの統合されたスイートの管理および監視機能豊富なユーザー エクスペリエンスと、IP アドレス インフラストラクチャです。 IPAM は、IP アドレス インフラストラクチャのサーバーおよびドメイン ネーム システムに自動的に検出 \(DNS\) 、ネットワーク上のサーバー中心的なインターフェイスからそれらを管理することができます。

### <a name="network-load-balancing"></a>[ネットワーク負荷分散](technologies/Network-Load-Balancing.md)

ネットワーク負荷分散 \(NLB\) 、TCP/IP ネットワーク プロトコルを使用して複数のサーバー間でトラフィックを分散します。 NLB でステートレスなことは SDN 以外の場合、インターネット インフォメーション サービスを実行する Web サーバーなどのアプリケーション \(IIS\), 、負荷の増加に応じてサーバーを追加して、拡張性がします。

### <a name="high-performance-networking"></a>[ハイパフォーマンス ネットワーク](technologies/hpn/hpn-top.md)

Windows Server 2016 のネットワーク オフロードおよび最適化テクノロジには、ソフトウェアのみ (SO) の機能とテクノロジー、ソフトウェアとハードウェア (SH) の統合機能とテクノロジー、ハードウェアのみ (HO) の機能とテクノロジーがあります。

次のオフロードおよび最適化テクノロジのドキュメントも併せて参照してください。

- [コンバージド ネットワーク インターフェイス カード (NIC) 構成ガイド](technologies/conv-nic/cnic-top.md)
- [データセンターブリッジング (DCB)](technologies/dcb/dcb-top.md)
- [Virtual Receive Side Scaling (vRSS)](technologies/vrss/vrss-top.md)


### <a name="network-policy-server"></a>[ネットワーク ポリシー サーバー](technologies/nps/nps-top.md)

ネットワーク ポリシー サーバー (NPS) を使用すると、接続要求の認証と承認を行うための組織全体のネットワーク アクセス ポリシーを作成して適用できます。

### <a name="network-shell-netsh"></a>[ネットワーク シェル (netsh)](technologies/netsh/netsh.md)

ネットワークシェルの \( netsh ネットワークユーティリティを使用して、 \) windows Server 2016 と windows 10 のネットワークテクノロジを管理できます。

### <a name="network-subsystem-performance-tuning"></a>[ネットワークサブシステムのパフォーマンスチューニング](technologies/network-subsystem/net-sub-performance-top.md)

このトピックでは、サーバーワークロードに適したネットワークアダプターの選択、ネットワークインターフェイスの順序付け、ネットワーク関連のパフォーマンスカウンター、およびパフォーマンスチューニングのネットワークアダプターと、Receive Side Scaling \( RSS \) 、Receive side 合体 RSC などの関連ネットワークテクノロジについて説明し \( \) ます。

### <a name="nic-teaming"></a>[NIC チーミング](technologies/nic-teaming/NIC-Teaming.md)

NIC チーミングには、物理イーサネット ネットワーク アダプターを 1 つまたは複数のソフトウェア ベースの仮想ネットワーク アダプターにグループ化することができます。 これらの仮想ネットワーク アダプターでは、高速なパフォーマンスとネットワーク アダプターに障害が発生した場合のフォールト トレランスを提供します。

### <a name="quality-of-service-qos-policy"></a>[サービスの品質 (QoS) ポリシー](technologies/qos/qos-policy-top.md)

QoS プロファイルを作成し、その設定をグループポリシーとともに配布することで、QoS ポリシーを Active Directory インフラストラクチャ全体のネットワーク帯域幅を管理する一元的ポイントとして使用できます。

### <a name="remote-access"></a>[リモート アクセス](../remote/remote-access/remote-access.md)

DirectAccess や仮想プライベートネットワーク VPN などのリモートアクセステクノロジを使用して、 \( \) リモートワーカーが内部ネットワークリソースに接続できるようにすることができます。 さらに、ローカルエリアネットワークの \( LAN \) ルーティングおよび Web アプリケーションプロキシに対してリモートアクセスを使用できます。 Web アプリケーション プロキシには、企業ネットワーク内部の Web アプリケーション用のリバース プロキシ機能があり、ユーザーは任意のデバイスで企業ネットワーク外部から Web アプリケーションにアクセスできます。

リモート アクセスのドキュメントは、Windows Server 2016 の目次で、「[リモート アクセスとサーバー管理](../remote/index.yml)」セクションを参照してください。 詳細については、「[リモート アクセス](../remote/remote-access/remote-access.md)」を参照してください。

Web アプリケーション プロキシ (リモート アクセス サーバー ロールのロール サービス) の詳細については、「[Windows Server 2016 の Web アプリケーション プロキシ](../remote/remote-access/web-application-proxy/web-application-proxy-windows-server.md)」を参照してください。

### <a name="virtual-private-networking-vpn"></a>[仮想プライベート ネットワーク (VPN)](../remote/remote-access/vpn/vpn-top.md)

Windows Server 2016 において、**DirectAccess と VPN** は、**リモート アクセス** サーバー ロールのロール サービスです。

リモートアクセスを VPN サーバーとしてインストールする場合、仮想プライベートネットワーク VPN を使用して、 \( \) リモート従業員にインターネット経由で組織のネットワークへの接続を提供する一方で、暗号化された接続で情報のプライバシーを維持することもできます。

Windows Server 2016 のリモート アクセス VPN と Windows 10 クライアント コンピューターを使用することにより、Always On VPN を展開できるようになりました。 Always On VPN では、常時接続のリモート VPN クライアントを管理できます。また、リモート ワーカーは、組織ネットワークへの VPN に手動で接続、切断する必要がなくなり、利便性が向上します。

詳細については、「[Windows Server 2016 および Windows 10 のためのリモート アクセス Always On VPN 展開ガイド](../remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy.md)」を参照してください。

>[!NOTE]
>VPN のドキュメントは、Windows Server 2016 の目次で、「[リモート アクセスとサーバー管理](../remote/index.yml)」セクションの「[リモート アクセス](../remote/remote-access/remote-access.md)」を参照してください。

VPN の詳細については、「[仮想プライベート ネットワーク (VPN)](../remote/remote-access/vpn/vpn-top.md)」を参照してください。

### <a name="windows-container-networking"></a>[Windows コンテナー ネットワーク](/virtualization/windowscontainers/manage-containers/container-networking)

Windows コンテナーのネットワークでは、業界の標準的なツールとワークフローを使用して、Windows 10 と Windows Server ホストの両方のコンテナー エンドポイントを接続するネットワークを作成および管理できます。 Windows コンテナーのネットワークは、プライベート、フラット L2、ルーティング L3 などの、複数のトポロジをサポートします。

また、Windows ホストネットワークサービスの HNS と通信するプラグインを介して、Docker、Kubernetes、または Windows PowerShell を使用してホスト上にローカルで作成できるオーバーレイもサポートされてい \( \) ます。 \-ローカルエージェントを介して各ノードの HNS に通信することで、高レベルのオーケストレーションシステムを通じてマルチノードクラスターネットワークを作成および管理できます。

### <a name="windows-internet-name-service-wins"></a>[Windows インターネット ネーム サービス (WINS)](technologies/wins/wins-top.md)

Windows インターネット ネーム サービス (WINS) は、コンピューターの NetBIOS 名と IP アドレスを対応付け、コンピューター名の登録と解決を行う従来型サービスです。 WINS よりも DNS の使用をお勧めします。

## <a name="additional-resources"></a>その他の情報

Windows Server 2016 は、次の場所で使用可能な以前のオペレーティング システムのリソースをネットワークです。

- Windows Server 2012 および Windows Server 2012 R2 [ネットワークの概要](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831357(v=ws.11))
- Windows Server 2008 および Windows Server 2008 R2 [ネットワーク](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753940(v=ws.10))
- Windows Server 2003 [Windows server 2003/2003 R2](https://www.microsoft.com/download/details.aspx?id=53314)の提供終了コンテンツ