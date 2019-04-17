---
title: ネットワーク
description: このトピックでは、Windows Server 2016 で利用できるソフトウェア定義ネットワークおよびネットワーク プラットフォーム テクノロジの概要について説明します。
ms.prod: windows-server-threshold
layout: LandingPage
ms.technology: networking
ms.topic: landing-page
ms.assetid: daaf6b61-5953-4c2d-b6b8-7c885b552646
manager: dougkim
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.openlocfilehash: bb5a605ef6438bfa6a2afe4963b8206f9dc84a3a
ms.sourcegitcommit: 07ac08dea2b8f2763c2614a999dc7967018aa0b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2018
ms.locfileid: "6121401"
---
# ネットワーク

>[!TIP]
> 以前のバージョンの Windows Server に関する情報をお探しの場合は、 docs.microsoft.com の他の [Windows Server ライブラリ](/previous-versions/windows/)を参照してください。 また、[このサイトで検索して](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions)、具体的な情報を確認することもできます。

<HR />

ネットワークはソフトウェア定義データセンター \(SDDC\) プラットフォームの根幹であり、Windows Server 2016 では、組織で SDDC ソリューションを完全に実現して移行できるように、各種ソフトウェア定義ネットワーク \(SDN\) テクノロジの新規追加と改善が行われています。

定義されているソフトウェアのリソースとネットワークを管理するときに、1 回限り、アプリケーションのインフラストラクチャ要件を記述およびを選択し、アプリケーションを実行する - 内部設置型またはクラウドにします。 

この一貫性により、アプリケーションの拡張が容易になり、アプリケーションをどこでもシームレスに実行できるだけでなく、セキュリティ、パフォーマンス、サービス品質、可用性のいずれについても等しい信頼性が実現されます。

<HR />

<ul class="cardsF panelContent">
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-whats-new.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h2><a href="../networking/What-s-New-in-Networking.md">ネットワークの新機能</a></h2>
                                        </div>
                                    </div>
                                </div>
                             </div>
                          </a>
                        </li>
                     </ul>
<HR />

<h2>ソフトウェア定義ネットワーク</h2>

<ul class="cardsF panelContent">
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="https://docs.microsoft.com/windows-server/networking/sdn/">ソフトウェア定義ネットワーク (SDN)</a><hr /></h3>このトピックでは、Windows Server、System Center、および Microsoft Azure で提供される SDN テクノロジについて説明します。</p>
                        
                                        <p><b>注意:</b> SDN インフラストラクチャ サーバー (ネットワーク コントローラー、ソフトウェア負荷分散ノードなど) を実行する Hyper-V ホストと仮想マシン \(VM\) には、Windows Server Datacenter Edition をインストールする必要があります。 Hyper-V ホストに含まれたすべてのテナント ワークロード VM が SDN 制御のネットワークに接続されている場合は、Windows Server Standard Edition を実行できます。</p>                                        </div>
                                    </div>
                                </div>
                            </div>
                          </a>
                        </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="sdn/deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md">スクリプトを使用したソフトウェア定義ネットワーク インフラストラクチャの展開</a><hr /></h3>このガイドは、テスト ラボ環境で仮想ネットワークとゲートウェイのネットワーク コント ローラーを展開する方法を説明します。</p>                                        </div>
                                    </div>
                                </div>
                            </div>
                          </a>
                        </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="sdn/technologies/network-controller/Network-Controller.md">ネットワーク コントローラー</a><hr /></h3>ネットワーク コント ローラーは、管理、構成、監視、およびデータ センター内の仮想および物理ネットワーク インフラストラクチャのトラブルシューティングを行う自動化の集中管理された、プログラミング可能なポイントを提供します。</p>                                        </div>
                                    </div>
                                </div>
                            </div>
                          </a>
                        </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="sdn/technologies/network-function-virtualization/software-load-balancing-for-sdn.md">SDN のソフトウェア負荷分散 &#40;SLB&#41;</a><hr /></h3>Windows Server 2016 でソフトウェア定義ネットワーク (SDN) を展開しているクラウド サービス プロバイダー \(CSP\) や企業では、ソフトウェア負荷分散 \(SLB\) を使用して、仮想ネットワーク リソース全体にわたってテナントおよびテナント ユーザーのネットワーク トラフィックを均等に分散することができます。 Windows Server SLB により、同じワークロードをホストする複数のサーバーであり、高可用性とスケーラビリティを提供することです。</p>                                        </div>
                                    </div>
                                </div>
                            </div>
                          </a>
                        </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md">SDN の RAS ゲートウェイ</a><hr /></h3>RAS ゲートウェイは、マルチテナントとボーダー ゲートウェイ プロトコル \(BGP\) に対応した Windows Server 2016 のソフトウェアベース ルーターです。Hyper-V ネットワーク仮想化を使用して複数のテナント仮想ネットワークをホストするクラウド サービス プロバイダー (CSP) や企業向けに設計されています。</p>                                        </div>
                                    </div>
                                </div>
                            </div>
                          </a>
                        </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="sdn/technologies/network-function-virtualization/Network-Function-Virtualization.md">ネットワーク機能の仮想化</a><hr /></h3>ソフトウェア定義データセンターでは、ハードウェア アプライアンス \(ロード バランサー、ファイアウォール、ルーター、スイッチなど\) によって実行されているネットワーク機能の、仮想アプライアンスとしての仮想化が進んでいます。 この「ネットワーク機能の仮想化」は、サーバーの仮想化とネットワーク仮想化の自然な流れです。</p>                                        </div>
                                    </div>
                                </div>
                            </div>
                          </a>
                        </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md">Datacenter Firewall Overview (Datacenter Firewall の概要)</a><hr /></h3>データ センターのファイアウォールとは、ネットワーク層、5 組 (プロトコル、発信元と宛先のポート番号、送信元と送信先の IP アドレス)、ステートフルなマルチ テナント ファイアウォールです。</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
</ul>

<HR />

## <a name="bkmk_networking"></a>ネットワー キング テクノロジ

<ul class="cardsF panelContent">
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="branchcache/BranchCache.md">BranchCache</a><hr /></h3>
                                        <p>BranchCache は、ワイド エリア ネットワーク \(WAN\) 帯域幅を最適化するテクノロジです。 ユーザーがリモート サーバー上のコンテンツをアクセスするときは、WAN の帯域幅を最適化、BranchCache は、ホストされたクラウド コンテンツ サーバーまたはと、WAN 経由ではなくローカルでコンテンツにアクセスするブランチ オフィスでコンピューターをクライアントに許可するブランチ オフィスの場所にコンテンツをキャッシュ メイン オフィスからコンテンツを取得します。</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="core-network-guide/core-network-guide-windows-server.md">コア ネットワーク ガイド</a><hr /></h3>
                                        <p>「コア ネットワーク ガイド」では、Windows Server ネットワークを展開する方法を説明します。また、「コア ネットワーク必携ガイド」ではネットワーク展開環境に機能を追加する方法について説明します。</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="../remote/remote-access/directaccess/DirectAccess.md">DirectAccess</a><hr /></h3>
                                        <p>DirectAccess は、リモート ユーザーが組織のネットワーク リソースに接続するための機能です。 </p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="dns/dns-top.md">ドメイン ネーム システム (DNS)"></a><hr /></h3>
                                        <p>ドメイン ネーム システム \(DNS\) は、TCP/IP を構成する業界標準のプロトコル群の 1 つです。コンピューター名と IP アドレスを対応付ける名前解決サービスが、DNS クライアントと DNS サーバーによってコンピューターとユーザーに提供されます。</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="technologies/dhcp/dhcp-top.md">動的ホスト構成プロトコル &#40;DHCP&#41;</a><hr /></h3>
                                        <p>動的ホスト構成プロトコル \(DHCP\) は、インターネットプロトコル \(IP\) ホストに対して、IPアドレスやその他の関連の構成情報 (サブネット マスクや既定のゲートウェイなど) を自動的に提供するクライアント/サーバー プロトコルです。</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="sdn/technologies/hyper-v-network-virtualization/Hyper-V-Network-Virtualization.md">Hyper-V ネットワーク仮想化</a><hr /></h3>
                                        <p>Hyper-Vネットワーク仮想化 \(HNV\) は、共有の物理ネットワーク インフラストラクチャ上でユーザー ネットワークを仮想化します。</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md">Hyper-V 仮想スイッチ</a><hr /></h3>
                                        <p>Hyper-V 仮想スイッチは、Hyper-V サーバーの役割をインストールすると Hyper-V マネージャーで使用できる、ソフトウェアベースのレイヤー 2 イーサネット ネットワーク スイッチです。 このスイッチには、仮想マシンを仮想ネットワークと物理ネットワークの両方に接続するための、プログラムで管理される拡張可能な機能が含まれています。 また、Hyper-V 仮想スイッチでは、セキュリティ、分離、およびサービスのレベルでポリシーを適用できます。 </p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="technologies/ipam/ipam-top.md">IP アドレス管理 &#40;IPAM&#41;</a><hr /></h3>
                                        <p>IP Address Management \(IPAM\) は、IP アドレス インフラストラクチャのエンドツーエンドのプランニング、展開、管理、監視を可能にする、快適なユーザー エクスペリエンスを備えたツールの統合スイートです。 IPAM によって、ネットワーク上の IP アドレス インフラストラクチャ サーバーとドメイン名システム (DNS) サーバーが自動的に検出され、一元的なインターフェイスでこれらのサーバーを管理できます。 </p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="technologies/Network-Load-Balancing.md">ネットワーク負荷分散</a><hr /></h3>
                                        <p>ネットワーク負荷分散 \(NLB\) は、TCP/IP ネットワーク プロトコルを使用して複数のサーバー間でトラフィックを分散します。 SDN 以外の展開環境で NLB を使用すると、インターネットインフォメーションサービス \(IIS\) を実行する Web サーバーなどのステートレスなアプリケーションを、負荷の増加に応じたサーバーの追加によって拡張できます。</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="technologies/hpn/hpn-top.md">ハイパフォーマンス ネットワーク</a><hr /></h3>
                                        <p>Windows Server 2016 のネットワーク オフロードおよび最適化テクノロジには、ソフトウェアのみ (SO) の機能とテクノロジー、ソフトウェアとハードウェア (SH) の統合機能とテクノロジー、ハードウェアのみ (HO) の機能とテクノロジーがあります。</p>

                                        <p>オフロードおよび最適化テクノロジに関する以下のドキュメントも参照してください。<p>
                                        <hr />
                                        <a href="technologies/conv-nic/cnic-top.md">ハイパフォーマンス ネットワーク</a><hr />
                                        <a href="technologies/dcb/dcb-top.md">データ センター ブリッジング (DCB)</a><hr />
                                        <a href="technologies/vrss/vrss-top.md">Virtual Receive Side Scaling (vRSS)</a>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="technologies/nps/nps-top.md">ネットワーク ポリシー サーバー</a><hr /></h3>
                                        <p>
ネットワーク ポリシー サーバー (NPS) を使用すると、接続要求の認証と承認を行うための組織全体のネットワーク アクセス ポリシーを作成して適用できます。</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="technologies/netsh/netsh.md">ネットワーク シェル (netsh)</a><hr /></h3>
                                        <p>
ネットワーク シェル \(netsh\) は、Windows Server 2016 および Windows 10 でネットワーク テクノロジを管理するためのネットワーク ユーティリティです。</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="technologies/network-subsystem/net-sub-performance-top.md">ネットワーク サブシステムのパフォーマンスの調整</a><hr /></h3>
                                        <p>
このトピックでは、サーバー ワークロードに応じた適切なネットワーク アダプターの選択方法、ネットワーク インターフェイスの順序指定、ネットワーク関連のパフォーマンス カウンター、ネットワーク アダプターのパフォーマンス チューニングとそれに関連するネットワーク テクノロジ (Receive Side Scaling \(RSS\)、Receive Side Coalescing \(RSC\) など) について説明しています。</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="technologies/nic-teaming/NIC-Teaming.md">NIC チーミング</a><hr /></h3>
                                        <p>
NIC チーミングには、物理イーサネット ネットワーク アダプターを 1 つまたは複数のソフトウェア ベースの仮想ネットワーク アダプターにグループ化することができます。 これらの仮想ネットワーク アダプターは、高速なパフォーマンスに加え、ネットワーク アダプターに障害が発生した場合のフォールト トレランスを提供します。</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="technologies/qos/qos-policy-top.md">サービス品質 (QoS) ポリシー</a><hr /></h3>
                                        <p>
QoS プロファイルを作成し、その設定をグループポリシーとともに配布することで、QoS ポリシーを Active Directory インフラストラクチャ全体のネットワーク帯域幅を管理する一元的ポイントとして使用できます。</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="technologies/wins/wins-top.md">Windows インターネット ネーム サービス (WINS)</a><hr /></h3>
                                        <p>
Windows インターネット ネーム サービス (WINS) は、コンピューターの NetBIOS 名と IP アドレスを対応付け、コンピューター名の登録と解決を行う従来型サービスです。 WINS よりも DNS の使用をお勧めします。</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="../remote/remote-access/remote-access.md">リモート アクセス</a><hr /></h3>
                                        <p>
DirectAccess や仮想プライベート ネットワーク \(VPN\) などのリモート アクセス テクノロジを使用すると、リモート ワーカーから内部ネットワーク リソースへの接続機能を提供できます。 リモート アクセスはまた、ローカル エリア ネットワーク \(LAN\) ルーティングや Web アプリケーション プロキシにも利用できます。 Web アプリケーション プロキシには、企業ネットワーク内部の Web アプリケーション用のリバース プロキシ機能があり、ユーザーは任意のデバイスで企業ネットワーク外部から Web アプリケーションにアクセスできます。</p>

                                        <p>Web アプリケーション プロキシ (リモート アクセス サーバー ロールの役割サービス) の詳細については、「<a href="https://docs.microsoft.com/windows-server/remote/remote-access/web-application-proxy/web-application-proxy-windows-server">Windows Server 2016 の Web アプリケーション プロキシ」をご覧ください</a></p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="https://docs.microsoft.com/virtualization/windowscontainers/container-networking/architecture">Windows コンテナー ネットワーク</a><hr /></h3>
                                        <p>
Windows コンテナーのネットワークでは、業界の標準的なツールとワークフローを使用して、Windows 10 と Windows Server ホストの両方のコンテナー エンドポイントを接続するネットワークを作成および管理できます。 Windows コンテナーのネットワークは、プライベート、フラット L2、ルーティング L3 などの、複数のトポロジをサポートします。</p>

                                        <p>また、Windows ホスト ネットワーク サービス \(HNS\) と通信するプラグインを介して、Docker、Kubernetes、または Windows PowerShell を使用し、ホスト上でローカルに作成できるオーバーレイもサポートされています。 ローカル エージェントを介して各ノードの HNS と通信し、高度なオーケストレーション システムを通じて、マルチノード クラスター ネットワークを作成および管理できます。</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="../remote/remote-access/vpn/vpn-top.md">仮想プライベート ネットワーク (VPN)</a><hr /></h3>
                                        <p>
DirectAccess と VPN は、リモート アクセス サーバー ロールの役割サービスです。</p>

                                        <p>リモートアクセスを VPN サーバーとしてインストールすると、仮想プライベートネットワーク \(VPN\) を使用して、リモートの従業員がインターネット経由で組織ネットワークに接続できる環境を提供できるとともに、接続の暗号化によって情報プライバシーを維持できます。</p>

                                       <p> Windows Server のリモート アクセス VPN と Windows 10 クライアント コンピューターを使用することにより、Always On VPN を展開できます。 Always On VPN では、常時接続のリモート VPN クライアントを管理できます。また、リモート ワーカーは、組織ネットワークへの VPN に手動で接続、切断する必要がなくなり、利便性が向上します。</p>

                                       <p>詳細については、「<a href="https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy">Windows Server 2016 および Windows 10 のためのリモート アクセス Always On VPN 展開ガイド」を参照してください</a></p>
                    </div>
                </div>
            </div>
        </div>
    </li>
</ul>

## その他のリソース

Windows Server 2016 以前のオペレーティング システムのネットワーク関連情報については、以下を参照してください。

- Windows Server 2012 および Windows Server 2012 R2: 「[ネットワークの概要](https://technet.microsoft.com/library/hh831357.aspx)」
- Windows Server 2008 および Windows Server 2008 R2: 「[ネットワーク](https://technet.microsoft.com/library/cc753940)」
- Windows Server 2003: 「[Windows Server 2003/2003 R2 の削除されたコンテンツ](https://www.microsoft.com/download/details.aspx?id=53314)」
