---
title: ネットワーク
description: このトピックでは、Windows Server 2016 で利用できるソフトウェア定義ネットワークおよびネットワーク プラットフォーム テクノロジの概要について説明します。
ms.prod: windows-server
layout: LandingPage
ms.technology: networking
ms.topic: landing-page
ms.assetid: daaf6b61-5953-4c2d-b6b8-7c885b552646
manager: dougkim
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.openlocfilehash: 0d9c30f52082f10b482df3403fc79daa6c888798
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406775"
---
# <a name="networking"></a>ネットワーク

>[!TIP]
> 以前のバージョンの Windows Server に関する情報をお探しの場合は、 docs.microsoft.com の他の [Windows Server ライブラリ](/previous-versions/windows/)を参照してください。 また、[このサイトで検索して](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions)、具体的な情報を確認することもできます。

<HR />

ネットワークは、ソフトウェアで定義されたデータ\(センター\)のデータセンター (SDDC) プラットフォームの基本部分であり、 \(Windows\) Server 2016 では、組織のための完全に実現した SDDC ソリューション。

ネットワークをソフトウェアによって定義されたリソースとして管理する場合、アプリケーションのインフラストラクチャ要件を1回記述し、アプリケーションの実行場所 (オンプレミスまたはクラウド) を選択することができます。 

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
                                        <h2><a href="./networking/What-s-New-in-Networking.md">ネットワーク&#39;の新機能</a></h2>
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
                                        <p><b>注: </b>ネットワークコントローラーやソフトウェアの負荷分散ノードなど、SDN インフラストラクチャサーバーを実行する Hyper-v ホストと仮想マシン (Vm) については、Windows Server Datacenter edition をインストールする必要があります。 SDN で制御されるネットワークに接続されているテナントワークロード Vm のみが含まれている Hyper-v ホストの場合は、Windows Server Standard edition を実行できます。</p>                                        </div>
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
                                        <h3><a href="sdn/deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md">スクリプトを使用してソフトウェアで定義されたネットワークインフラストラクチャを展開する</a><hr /></h3>このガイドは、テスト ラボ環境で仮想ネットワークとゲートウェイのネットワーク コント ローラーを展開する方法を説明します。</p>                                        </div>
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
                                        <h3><a href="sdn/technologies/network-function-virtualization/software-load-balancing-for-sdn.md">SDN のソフトウェア&#40;負荷&#41;分散 SLB</a><hr /></h3>クラウド サービス プロバイダー (Csp) やソフトウェアによるネットワーク制御 (SDN) で Windows Server 2016 を展開する企業は、ソフトウェアの負荷分散 (SLB) を使用してテナントと仮想ネットワークのリソース間でテナントのお客様のネットワーク トラフィックを均等に分散します。 Windows Server SLB により、同じワークロードをホストする複数のサーバーであり、高可用性とスケーラビリティを提供することです。</p>                                        </div>
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
                                        <h3><a href="sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md">SDN の RAS ゲートウェイ</a><hr /></h3>Windows Server 2016 のソフトウェアベースのマルチテナント、Border Gateway Protocol (BGP) 対応ルーターである RAS ゲートウェイは、クラウドサービスプロバイダー (Csp) と、Hyper-v ネットワークを使用して複数のテナント仮想ネットワークをホストする企業向けに設計されています。仮想化.</p>                                        </div>
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
                                        <h3><a href="sdn/technologies/network-function-virtualization/Network-Function-Virtualization.md">ネットワーク機能の仮想化</a><hr /></h3>ソフトウェア定義データセンターでは、ハードウェアアプライアンス (ロードバランサー、ファイアウォール、ルーター、スイッチなど) によって実行されるネットワーク機能が、仮想アプライアンスとして仮想化されることが増えています。 この&quot;ネットワーク機能の&quot;仮想化は、サーバー仮想化とネットワーク仮想化の自然な流れです。</p>                                        </div>
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
                                        <h3><a href="sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md">Datacenter Firewall の概要</a><hr /></h3>データ センターのファイアウォールとは、ネットワーク層、5 組 (プロトコル、発信元と宛先のポート番号、送信元と送信先の IP アドレス)、ステートフルなマルチ テナント ファイアウォールです。</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
</ul>

<HR />

## <a name="bkmk_networking"></a>ネットワークテクノロジ

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
                                        <p>BranchCache は、ワイド エリア ネットワーク (WAN) 帯域幅最適化テクノロジです。 ユーザーがリモート サーバー上のコンテンツをアクセスするときは、WAN の帯域幅を最適化、BranchCache は、ホストされたクラウド コンテンツ サーバーまたはと、WAN 経由ではなくローカルでコンテンツにアクセスするブランチ オフィスでコンピューターをクライアントに許可するブランチ オフィスの場所にコンテンツをキャッシュ メイン オフィスからコンテンツを取得します。</p>
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
                                        <h3><a href="core-network-guide/core-network-guide-windows-server.md">コアネットワークガイド</a><hr /></h3>
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
                                        <h3><a href="./remote/remote-access/directaccess/DirectAccess.md">DirectAccess</a><hr /></h3>
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
                                        <h3><a href="dns/dns-top.md">ドメインネームシステム (DNS)&quot;&gt;</a><hr /></h3>
                                        <p>ドメインネームシステム (DNS) は、TCP/IP を構成する業界標準のプロトコルスイートの1つであり、DNS クライアントと DNS サーバーの組み合わせにより、コンピューター名から IP アドレスへのマッピング名前解決サービスがコンピューターとユーザーに提供されます。</p>
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
                                        <h3><a href="technologies/dhcp/dhcp-top.md">動的ホスト構成プロトコル&#40;DHCP&#41;</a><hr /></h3>
                                        <p>動的ホスト構成プロトコル (DHCP) は、IP アドレスとその他の関連する構成情報 (サブネットマスク、デフォルトゲートウェイなど) を使用してインターネットプロトコル (IP) ホストを自動的に提供するクライアント/サーバープロトコルです。</p>
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
                                        <h3><a href="sdn/technologies/hyper-v-network-virtualization/Hyper-V-Network-Virtualization.md">Hyper-v ネットワーク仮想化</a><hr /></h3>
                                        <p>Hyper-v ネットワーク仮想化 (HNV) を使用すると、共有の物理ネットワークインフラストラクチャ上にある顧客ネットワークを仮想化することができます。</p>
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
                                        <h3><a href="./virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md">Hyper-V 仮想スイッチ</a><hr /></h3>
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
                                        <h3><a href="technologies/ipam/ipam-top.md">IP アドレス管理&#40;IPAM&#41;</a><hr /></h3>
                                        <p>IP アドレス管理 (IPAM) は、さまざまなユーザーエクスペリエンスを備えた、IP アドレスインフラストラクチャのエンドツーエンドの計画、展開、管理、および監視を可能にするツールの統合スイートです。 IPAM では、ネットワーク上の IP アドレス インフラストラクチャ サーバーとドメイン名システム (DNS) サーバーを自動で検出し、1 つのインターフェイスでこれらのサーバーを管理できます。 </p>
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
                                        <p>ネットワーク負荷分散 (NLB) は、TCP/IP ネットワークプロトコルを使用して複数のサーバーにトラフィックを分散します。 SDN 以外の展開では、NLB によって、インターネットインフォメーションサービス (IIS) を実行している Web サーバーなどのステートレスなアプリケーションが、負荷の増加に応じてサーバーを追加することでスケーラブルになります。</p>
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
                                        <h3><a href="technologies/hpn/hpn-top.md">高パフォーマンスネットワーク</a><hr /></h3>
                                        <p>Windows Server 2016 のネットワーク オフロードおよび最適化テクノロジには、ソフトウェアのみ (SO) の機能とテクノロジー、ソフトウェアとハードウェア (SH) の統合機能とテクノロジー、ハードウェアのみ (HO) の機能とテクノロジーがあります。</p>
                                        <p>オフロードおよび最適化テクノロジに関する以下のドキュメントも参照してください。<p>
                                        <hr />
                                        <a href="technologies/conv-nic/cnic-top.md">高パフォーマンスネットワーク</a><hr />
                                        <a href="technologies/dcb/dcb-top.md">データセンターブリッジング (DCB)</a><hr />
                                        <a href="technologies/vrss/vrss-top.md">仮想 Receive Side Scaling (vRSS)</a>
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
                                        <h3><a href="technologies/nps/nps-top.md">ネットワークポリシーサーバー</a><hr /></h3>
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
ネットワークシェル (netsh) ネットワークユーティリティを使用して、Windows Server 2016 と Windows 10 のネットワークテクノロジを管理できます。</p>
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
                                        <h3><a href="technologies/network-subsystem/net-sub-performance-top.md">ネットワークサブシステムのパフォーマンスチューニング</a><hr /></h3>
                                        <p>
このトピックでは、サーバーワークロードに適したネットワークアダプターの選択、ネットワークインターフェイスの順序付け、ネットワーク関連のパフォーマンスカウンター、およびパフォーマンスチューニングのネットワークアダプターとその関連ネットワークテクノロジについて説明します。Receive Side Scaling (RSS)、Receive Side 合体 (RSC) など。</p>
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
                                        <h3><a href="technologies/qos/qos-policy-top.md">サービスの品質 (QoS) ポリシー</a><hr /></h3>
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
                                        <h3><a href="./remote/remote-access/remote-access.md">リモート アクセス</a><hr /></h3>
                                        <p>
DirectAccess や仮想プライベートネットワーク (VPN) などのリモートアクセステクノロジを使用して、リモートワーカーが内部ネットワークリソースに接続できるようにすることができます。 さらに、ローカルエリアネットワーク (LAN) のルーティングおよび Web アプリケーションプロキシに対してリモートアクセスを使用できます。 Web アプリケーション プロキシには、企業ネットワーク内部の Web アプリケーション用のリバース プロキシ機能があり、ユーザーは任意のデバイスで企業ネットワーク外部から Web アプリケーションにアクセスできます。</p>
                                        <p>リモートアクセスサーバーの役割の役割サービスである Web アプリケーションプロキシの詳細については、「 <a href="https://docs.microsoft.com/windows-server/remote/remote-access/web-application-proxy/web-application-proxy-windows-server">Windows server 2016 の Web アプリケーションプロキシ</a>」を参照してください。</p>
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
                                        <h3><a href="https://docs.microsoft.com/virtualization/windowscontainers/container-networking/architecture">Windows コンテナーネットワーク</a><hr /></h3>
                                        <p>
Windows コンテナーのネットワークでは、業界の標準的なツールとワークフローを使用して、Windows 10 と Windows Server ホストの両方のコンテナー エンドポイントを接続するネットワークを作成および管理できます。 Windows コンテナーのネットワークは、プライベート、フラット L2、ルーティング L3 などの、複数のトポロジをサポートします。</p>

                                        <p>また、Windows ホストネットワークサービス (HNS) と通信するプラグインを介して Docker、Kubernetes、または Windows PowerShell を使用してホスト上にローカルで作成できるオーバーレイもサポートされています。 ローカルエージェントを介して各ノードの HNS に通信することで、高レベルのオーケストレーションシステムを通じてマルチノードクラスターネットワークを作成および管理できます。</p>
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
                                        <h3><a href="./remote/remote-access/vpn/vpn-top.md">仮想プライベート ネットワーク (VPN)</a><hr /></h3>
                                        <p>
DirectAccess と VPN は、リモート アクセス サーバー ロールの役割サービスです。</p>
                                        <p>リモートアクセスを VPN サーバーとしてインストールする場合は、仮想プライベートネットワーク (VPN) を使用して、リモート従業員がインターネット経由で組織のネットワークに接続できるようにする一方で、暗号化された接続で情報のプライバシーを維持することもできます.</p>
                                       <p> Windows Server のリモート アクセス VPN と Windows 10 クライアント コンピューターを使用することにより、Always On VPN を展開できます。 Always On VPN では、常時接続のリモート VPN クライアントを管理できます。また、リモート ワーカーは、組織ネットワークへの VPN に手動で接続、切断する必要がなくなり、利便性が向上します。</p>
                                       <p>詳細については、「 <a href="https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy">Windows Server 2016 および windows 10 用のリモートアクセス ALWAYS ON VPN 展開ガイド</a>」を参照してください。</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
</ul>

## <a name="additional-resources"></a>その他のリソース

Windows Server 2016 以前のオペレーティング システムのネットワーク関連情報については、以下を参照してください。

- Windows Server 2012 および Windows Server 2012 R2 [ネットワークの概要](https://technet.microsoft.com/library/hh831357.aspx)
- Windows Server 2008 および Windows Server 2008 R2 [ネットワーク](https://technet.microsoft.com/library/cc753940)
- Windows Server 2003 [Windows server 2003/2003 R2](https://www.microsoft.com/download/details.aspx?id=53314)の提供終了コンテンツ
