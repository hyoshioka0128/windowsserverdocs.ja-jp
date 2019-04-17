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
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2018
ms.locfileid: "6066846"
---
# ネットワーク

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

>[!TIP]
> 以前のバージョンの Windows Server に関する情報をお探しの場合は、 docs.microsoft.com の他の [Windows Server ライブラリ](/previous-versions/windows/)を参照してください。 また、[このサイトで検索して](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions)、具体的な情報を確認することもできます。

<img src="../media/landing-icons/network.png" style='float:left; padding:.5em;' alt="Icon depicting two networked computers"> ネットワークはソフトウェア定義データセンター \(SDDC\) プラットフォームの根幹であり、Windows Server 2016 では、組織で SDDC ソリューションを完全に実現して移行できるように、各種ソフトウェア定義ネットワーク \(SDN\) テクノロジの新規追加と改善が行われています。

定義されているソフトウェアのリソースとネットワークを管理するときに、1 回限り、アプリケーションのインフラストラクチャ要件を記述およびを選択し、アプリケーションを実行する - 内部設置型またはクラウドにします。 

この一貫性により、アプリケーションの拡張が容易になり、アプリケーションをどこでもシームレスに実行できるだけでなく、セキュリティ、パフォーマンス、サービス品質、可用性のいずれについても等しい信頼性が実現されます。

>[!Note]
> Windows Server のダウンロードについては、「[Windows Server 評価版ソフトウェア](https://www.microsoft.com/evalcenter/evaluate-windows-server-technical-preview)」を参照してください。

Windows Server 2016 で追加された新しいネットワーク テクノロジは、次のとおりです。

- ソフトウェアの定義済みのネットワーク: ネットワーク コント ローラーは、管理、構成、監視、およびデータ センター内の仮想および物理ネットワーク インフラストラクチャのトラブルシューティングを行う自動化の集中管理された、プログラミング可能なポイントを提供します。 ネットワーク コントローラーでは、ネットワーク機能の仮想化を使用して、ソフトウェア負荷分散 \(SLB\) 用の仮想マシン \(VMs\) を容易に展開し、テナントのネットワーク トラフィックの負荷を最適化することができます。また、RAS ゲートウェイを使用して、インターネット、オンプレミス、クラウド リソースの中から、必要な接続オプションをテナントに提供できます。 ネットワーク コント ローラーを使用して Vm と HYPER-V のデータ センターのファイアウォールを管理するホスト。

- ネットワーク プラットフォーム: 既存のネットワーク プラットフォーム テクノロジの新機能により、DNS ポリシーを使用して、クエリに対する DNS サーバー応答をカスタマイズできるようになりました。またコンバージド NIC を使用して、リモート ダイレクト メモリ アクセス \(RDMA\) とイーサネットのトラフィックを一括処理できます。スイッチ埋め込みチーミング \(SET\) によって、RDMA NIC に接続された Hyper-V 仮想スイッチを作成したり、IP アドレス管理 \(IPAM\) を使用して、DNS ゾーンやサーバー、さらに DHCP アドレスと IP アドレスを管理したりすることも可能になりました。

詳しくは、「[Windows Server によってサポートされているネットワークのシナリオ](windows-server-supported-networking-scenarios.md)」を参照してください。

以下の各セクションでは、SDN テクノロジとネットワーク プラットフォーム テクノロジについて説明します。

## ソフトウェア定義ネットワーク テクノロジ

### [ソフトウェアには、ネットワーク構成と #40; が定義されています。SDN & #41 です。](sdn/software-defined-networking.md)

このトピックでは、Windows Server、System Center、および Microsoft Azure で提供される SDN テクノロジについて説明します。

>[!NOTE]
>SDN インフラストラクチャ サーバー (ネットワーク コントローラー、ソフトウェア負荷分散ノードなど) を実行する Hyper-V ホストと仮想マシン \(VM\) には、Windows Server 2016 Datacenter Edition をインストールする必要があります。 Hyper-V ホストに含まれたすべてのテナント ワークロード VM が SDN 制御のネットワークに接続されている場合は、Windows Server 2016 Standard Edition を実行できます。

### [スクリプトを使用したソフトウェア定義ネットワーク インフラストラクチャの展開](sdn/deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)
このガイドは、テスト ラボ環境で仮想ネットワークとゲートウェイのネットワーク コント ローラーを展開する方法を説明します。

### [ネットワーク コントローラー](sdn/technologies/network-controller/Network-Controller.md)

ネットワーク コント ローラーは、管理、構成、監視、およびデータ センター内の仮想および物理ネットワーク インフラストラクチャのトラブルシューティングを行う自動化の集中管理された、プログラミング可能なポイントを提供します。

### [SDN のソフトウェア負荷分散 &#40;SLB&#41;](sdn/technologies/network-function-virtualization/software-load-balancing-for-sdn.md)

Windows Server 2016 でソフトウェア定義ネットワーク (SDN) を展開しているクラウド サービス プロバイダー \(CSP\) や企業では、ソフトウェア負荷分散 \(SLB\) を使用して、仮想ネットワーク リソース全体にわたってテナントおよびテナント ユーザーのネットワーク トラフィックを均等に分散することができます。 Windows Server SLB により、同じワークロードをホストする複数のサーバーであり、高可用性とスケーラビリティを提供することです。

### [SDN の RAS ゲートウェイ](sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)

RAS ゲートウェイは、マルチテナントとボーダー ゲートウェイ プロトコル \(BGP\) に対応した Windows Server 2016 のソフトウェアベース ルーターです。Hyper-V ネットワーク仮想化を使用して複数のテナント仮想ネットワークをホストするクラウド サービス プロバイダー (CSP) や企業向けに設計されています。 

### [ネットワーク機能の仮想化](sdn/technologies/network-function-virtualization/Network-Function-Virtualization.md)

ソフトウェア定義データセンターでは、ハードウェア アプライアンス \(ロード バランサー、ファイアウォール、ルーター、スイッチなど\) によって実行されているネットワーク機能の、仮想アプライアンスとしての仮想化が進んでいます。 この「ネットワーク機能の仮想化」は、サーバーの仮想化とネットワーク仮想化の自然な流れです。

### [Datacenter Firewall Overview (Datacenter Firewall の概要)](sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)

データ センターのファイアウォールとは、ネットワーク層、5 組 (プロトコル、発信元と宛先のポート番号、送信元と送信先の IP アドレス)、ステートフルなマルチ テナント ファイアウォールです。

## <a name="bkmk_networking"></a>ネットワー キング テクノロジ

以下では、Windows Server 2016 の各種ネットワーク テクノロジへのリンクを示します。

### [ネットワークの新機能](../networking/What-s-New-in-Networking.md)

以下の各セクションでは、Windows Server 2016 の新しいネットワーク テクノロジと、既存テクノロジに対する新機能について説明します。

### [BranchCache](branchcache/BranchCache.md)

BranchCache は、ワイド エリア ネットワーク \(WAN\) 帯域幅を最適化するテクノロジです。 ユーザーがリモート サーバー上のコンテンツをアクセスするときは、WAN の帯域幅を最適化、BranchCache は、ホストされたクラウド コンテンツ サーバーまたはと、WAN 経由ではなくローカルでコンテンツにアクセスするブランチ オフィスでコンピューターをクライアントに許可するブランチ オフィスの場所にコンテンツをキャッシュ メイン オフィスからコンテンツを取得します。

### [Windows Server 2016 のコア ネットワーク ガイド](core-network-guide/core-network-guide-windows-server.md)

「コア ネットワーク ガイド」では、Windows Server ネットワークを展開する方法を説明します。また、「コア ネットワーク必携ガイド」ではネットワーク展開環境に機能を追加する方法について説明します。

### [DirectAccess](../remote/remote-access/directaccess/DirectAccess.md)

DirectAccess は、リモート ユーザーが組織のネットワーク リソースに接続するための機能です。 

DirectAccess のドキュメントは、Windows Server 2016 の目次で、「[リモート アクセスとサーバー管理](https://docs.microsoft.com/windows-server/remote/)」セクションの「[リモート アクセス](https://docs.microsoft.com/windows-server/remote/remote-access/remote-access)」を参照してください。 詳しくは、「[DirectAccess](../remote/remote-access/directaccess/DirectAccess.md)」を参照してください。

### [ドメイン ネーム システム &#40;DNS&#41;](dns/dns-top.md)

ドメイン ネーム システム \(DNS\) は、TCP/IP を構成する業界標準のプロトコル群の 1 つです。コンピューター名と IP アドレスを対応付ける名前解決サービスが、DNS クライアントと DNS サーバーによってコンピューターとユーザーに提供されます。

### [動的ホスト構成プロトコル &#40;DHCP&#41;](technologies/dhcp/dhcp-top.md)

動的ホスト構成プロトコル \(DHCP\) は、インターネットプロトコル \(IP\) ホストに対して、IPアドレスやその他の関連の構成情報 (サブネット マスクや既定のゲートウェイなど) を自動的に提供するクライアント/サーバー プロトコルです。

### [Hyper-V ネットワーク仮想化](sdn/technologies/hyper-v-network-virtualization/Hyper-V-Network-Virtualization.md)

Hyper-Vネットワーク仮想化 \(HNV\) は、共有の物理ネットワーク インフラストラクチャ上でユーザー ネットワークを仮想化します。

### [Hyper-V 仮想スイッチ](../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md)

Hyper-V 仮想スイッチは、Hyper-V サーバーの役割をインストールすると Hyper-V マネージャーで使用できる、ソフトウェアベースのレイヤー 2 イーサネット ネットワーク スイッチです。 このスイッチには、仮想マシンを仮想ネットワークと物理ネットワークの両方に接続するための、プログラムで管理される拡張可能な機能が含まれています。 また、Hyper-V 仮想スイッチでは、セキュリティ、分離、およびサービスのレベルでポリシーを適用できます。 

Hyper-V 仮想スイッチのドキュメントは、Windows Server 2016 の目次で、「**仮想化**」セクションを参照してください。 詳しくは、「[Hyper-V 仮想スイッチの概要](../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md)」を参照してください。

### [IP アドレス管理 &#40;IPAM&#41;](technologies/ipam/ipam-top.md)

IP Address Management \(IPAM\) は、IP アドレス インフラストラクチャのエンドツーエンドのプランニング、展開、管理、監視を可能にする、快適なユーザー エクスペリエンスを備えたツールの統合スイートです。 IPAM によって、ネットワーク上の IP アドレス インフラストラクチャ サーバーとドメイン名システム (DNS) サーバーが自動的に検出され、一元的なインターフェイスでこれらのサーバーを管理できます。

### [ネットワーク負荷分散](technologies/Network-Load-Balancing.md)

ネットワーク負荷分散 \(NLB\) は、TCP/IP ネットワーク プロトコルを使用して複数のサーバー間でトラフィックを分散します。 SDN 以外の展開環境で NLB を使用すると、インターネットインフォメーションサービス \(IIS\) を実行する Web サーバーなどのステートレスなアプリケーションを、負荷の増加に応じたサーバーの追加によって拡張できます。

### [ハイパフォーマンス ネットワーク](technologies/hpn/hpn-top.md)

Windows Server 2016 のネットワーク オフロードおよび最適化テクノロジには、ソフトウェアのみ (SO) の機能とテクノロジー、ソフトウェアとハードウェア (SH) の統合機能とテクノロジー、ハードウェアのみ (HO) の機能とテクノロジーがあります。

次のオフロードおよび最適化テクノロジのドキュメントも併せて参照してください。

- [コンバージド ネットワーク インターフェイス カード (NIC) 構成ガイド](technologies/conv-nic/cnic-top.md)
- [データ センター ブリッジング (DCB)](technologies/dcb/dcb-top.md)
- [Virtual Receive Side Scaling (vRSS)](technologies/vrss/vrss-top.md)


### [ネットワーク ポリシー サーバー](technologies/nps/nps-top.md)

ネットワーク ポリシー サーバー (NPS) を使用すると、接続要求の認証と承認を行うための組織全体のネットワーク アクセス ポリシーを作成して適用できます。

### [ネットワーク シェル (netsh)](technologies/netsh/netsh.md)

ネットワーク シェル \(netsh\) は、Windows Server 2016 および Windows 10 でネットワーク テクノロジを管理するためのネットワーク ユーティリティです。

### [ネットワーク サブシステムのパフォーマンスの調整](technologies/network-subsystem/net-sub-performance-top.md)

このトピックでは、サーバー ワークロードに応じた適切なネットワーク アダプターの選択方法、ネットワーク インターフェイスの順序指定、ネットワーク関連のパフォーマンス カウンター、ネットワーク アダプターのパフォーマンス チューニングとそれに関連するネットワーク テクノロジ (Receive Side Scaling \(RSS\)、Receive Side Coalescing \(RSC\) など) について説明しています。

### [NIC チーミング](technologies/nic-teaming/NIC-Teaming.md)

NIC チーミングには、物理イーサネット ネットワーク アダプターを 1 つまたは複数のソフトウェア ベースの仮想ネットワーク アダプターにグループ化することができます。 これらの仮想ネットワーク アダプターは、高速なパフォーマンスに加え、ネットワーク アダプターに障害が発生した場合のフォールト トレランスを提供します。

### [サービス品質 (QoS) ポリシー](technologies/qos/qos-policy-top.md)

QoS プロファイルを作成し、その設定をグループポリシーとともに配布することで、QoS ポリシーを Active Directory インフラストラクチャ全体のネットワーク帯域幅を管理する一元的ポイントとして使用できます。

### [リモート アクセス](../remote/remote-access/remote-access.md)

DirectAccess や仮想プライベート ネットワーク \(VPN\) などのリモート アクセス テクノロジを使用すると、リモート ワーカーから内部ネットワーク リソースへの接続機能を提供できます。 リモート アクセスはまた、ローカル エリア ネットワーク \(LAN\) ルーティングや Web アプリケーション プロキシにも利用できます。 Web アプリケーション プロキシには、企業ネットワーク内部の Web アプリケーション用のリバース プロキシ機能があり、ユーザーは任意のデバイスで企業ネットワーク外部から Web アプリケーションにアクセスできます。

リモート アクセスのドキュメントは、Windows Server 2016 の目次で、「[リモート アクセスとサーバー管理](https://docs.microsoft.com/windows-server/remote/)」セクションを参照してください。 詳細については、「[リモート アクセス](../remote/remote-access/remote-access.md)」を参照してください。

Web アプリケーション プロキシ (リモート アクセス サーバー ロールのロール サービス) の詳細については、「[Windows Server 2016 の Web アプリケーション プロキシ](https://docs.microsoft.com/windows-server/remote/remote-access/web-application-proxy/web-application-proxy-windows-server)」を参照してください。

### [仮想プライベート ネットワーク (VPN)](../remote/remote-access/vpn/vpn-top.md)

Windows Server 2016 において、**DirectAccess と VPN** は、**リモート アクセス** サーバー ロールのロール サービスです。

リモートアクセスを VPN サーバーとしてインストールすると、仮想プライベートネットワーク \(VPN\) を使用して、リモートの従業員がインターネット経由で組織ネットワークに接続できる環境を提供できるとともに、接続の暗号化によって情報プライバシーを維持できます。

Windows Server 2016 のリモート アクセス VPN と Windows 10 クライアント コンピューターを使用することにより、Always On VPN を展開できるようになりました。 Always On VPN では、常時接続のリモート VPN クライアントを管理できます。また、リモート ワーカーは、組織ネットワークへの VPN に手動で接続、切断する必要がなくなり、利便性が向上します。

詳細については、「[Windows Server 2016 および Windows 10 のためのリモート アクセス Always On VPN 展開ガイド](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy)」を参照してください。

>[!NOTE]
>VPN のドキュメントは、Windows Server 2016 の目次で、「[リモート アクセスとサーバー管理](https://docs.microsoft.com/windows-server/remote/)」セクションの「[リモート アクセス](https://docs.microsoft.com/windows-server/remote/remote-access/remote-access)」を参照してください。

VPN の詳細については、「[仮想プライベート ネットワーク (VPN)](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/vpn-top)」を参照してください。

### [Windows コンテナーのネットワーク](https://docs.microsoft.com/virtualization/windowscontainers/manage-containers/container-networking)

Windows コンテナーのネットワークでは、業界の標準的なツールとワークフローを使用して、Windows 10 と Windows Server ホストの両方のコンテナー エンドポイントを接続するネットワークを作成および管理できます。 Windows コンテナーのネットワークは、プライベート、フラット L2、ルーティング L3 などの、複数のトポロジをサポートします。

また、Windows ホスト ネットワーク サービス \(HNS\) と通信するプラグインを介して、Docker、Kubernetes、または Windows PowerShell を使用し、ホスト上でローカルに作成できるオーバーレイもサポートされています。 ローカル エージェントを介して各ノードの HNS と通信し、高度なオーケストレーション システムを通じて、マルチノード クラスター ネットワークを作成および管理できます。

### [Windows インターネット ネーム サービス (WINS)](technologies/wins/wins-top.md)

Windows インターネット ネーム サービス (WINS) は、コンピューターの NetBIOS 名と IP アドレスを対応付け、コンピューター名の登録と解決を行う従来型サービスです。 WINS よりも DNS の使用をお勧めします。

## その他のリソース

Windows Server 2016 以前のオペレーティング システムのネットワーク関連情報については、以下を参照してください。

- Windows Server 2012 および Windows Server 2012 R2: 「[ネットワークの概要](https://technet.microsoft.com/library/hh831357.aspx)」
- Windows Server 2008 および Windows Server 2008 R2: 「[ネットワーク](https://technet.microsoft.com/library/cc753940)」
- Windows Server 2003: 「[Windows Server 2003/2003 R2 の削除されたコンテンツ](https://www.microsoft.com/download/details.aspx?id=53314)」
