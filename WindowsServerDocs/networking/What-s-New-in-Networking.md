---
title: ネットワークの新機能
description: このトピックでは、Windows Server 2016 でネットワークの新機能とテクノロジに関する概要情報を提供します。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: get-started-article
ms.assetid: 08fb7563-d319-48a9-b181-ca0ca3032c18
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 43ce6290f6559be7cb078032b79519d1681506d4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829193"
---
# <a name="whats-new-in-networking"></a>ネットワークの新機能

>適用対象:Windows Server 2016

Windows Server 2016 で新しいまたは強化されたネットワーク テクノロジを次に示します。  
  このトピックの Upd には、次のセクションにが含まれています。  
  
-   [新しいネットワーク機能とテクノロジ](#bkmk_features)  
  
-   [追加のネットワーク テクノロジに対する新機能](#bkmk_existing)  
  
## <a name="bkmk_features"></a>新しいネットワーク機能とテクノロジ

ネットワークは、ソフトウェア定義されているデータ センター (SDDC) プラットフォームの基礎の一部と、Windows Server 2016 は、組織用に完全に実現された SDDC ソリューションを移動するための新機能と更新のソフトウェア定義ネットワーク (SDN) テクノロジを提供します。  
  
ソフトウェア定義リソースとネットワークを管理するときに、1 回は、アプリケーションのインフラストラクチャ要件を記述および選択し、アプリケーションを実行する、オンプレミスまたはクラウドで。  この一貫性は、アプリケーションがスケールしやすいようになりましたと、セキュリティ、パフォーマンス、サービス、および可用性の品質を等しい自信場所を問わず、アプリケーションをシームレスに実行できることを意味します。  
  
次のセクションでは、機能およびテクノロジの新しいネットワークこれらに関する情報を格納します。  
  
### <a name="software-defined-networking-infrastructure"></a>ソフトウェアによるネットワーク制御インフラストラクチャ

新規または改善された SDN インフラストラクチャ テクノロジを次に示します。  
  
-   **ネットワーク コント ローラー**します。 新しいネットワーク コント ローラーは、Windows Server 2016 で、管理、構成、監視、およびデータ センターの仮想および物理ネットワーク インフラストラクチャのトラブルシューティングを行う自動化の集中管理された、プログラミング可能なポイントを提供します。 ネットワーク コントローラーを使用すると、ネットワーク インフラストラクチャの構成を自動化できます。ネットワーク デバイスとサービスを手動で構成する必要はありません。 詳細については、次を参照してください。[ネットワーク コント ローラー](sdn/technologies/network-controller/Network-Controller.md)と[展開ソフトウェア定義ネットワーク スクリプトを使用して](https://technet.microsoft.com/library/mt427380.aspx)します。  
  
-   **HYPER-V 仮想スイッチ**します。 HYPER-V 仮想スイッチ、HYPER-V ホスト上で実行し、分散の切り替えおよびルーティングを作成することができます、ポリシー強制レイヤーを配置および Microsoft Azure との互換性。 詳しくは、「[Hyper-V 仮想スイッチの概要](../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md)」を参照してください。  
  
-   **ネットワーク関数仮想化 (NFV)** します。 今日のソフトウェアで定義されているデータ センター、(ロード バランサー、ファイアウォール、ルーター、スイッチ、およびなど) などのハードウェア アプライアンスで実行されているネットワークの機能がますます仮想アプライアンスとしてデプロイされているがします。 この「ネットワーク機能の仮想化」は、サーバーの仮想化とネットワーク仮想化の自然な流れです。 仮想アプライアンスは迅速に新たなと、新しい市場を作成します。 常に興味を引くと両方の仮想化プラットフォームで運動量を取得し、クラウド サービスです。 次の NFV テクノロジ Windows Server 2016 で利用できます。  
  
    -   **データ センターのファイアウォール**します。 この分散型のファイアウォールは、VM のインターフェイス レベルまたはサブネット レベルのファイアウォール ポリシーを適用できるように細分化されたアクセス制御リスト (Acl) を提供します。  
  
        詳細については、次を参照してください。 [データ センターのファイアウォールの概要](sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)します。  
  
    -   **RAS ゲートウェイ**します。 RAS ゲートウェイは、仮想ネットワークとクラウド データ センターから、テナントのリモート サイトへのサイト対サイト VPN 接続を含む、物理ネットワーク間のトラフィックのルーティングを使用できます。 インターネット キー交換バージョン 2 (IKEv2) をデプロイする具体的には、サイト対サイト仮想プライベート ネットワーク (Vpn)、レイヤー 3 (L3) VPN、および Generic Routing Encapsulation (GRE) ゲートウェイ。 また、ゲートウェイ プールとゲートウェイの M+N 冗長性がサポートされています。ボーダー ゲートウェイ プロトコル (BGP) ルート Reflector 機能を備えたすべてのゲートウェイ シナリオ (IKEv2 VPN、GRE VPN、および L3 VPN) のネットワーク間の動的ルーティングを提供します。  
  
        詳細については、次を参照してください。 [RAS ゲートウェイで新](sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md)と[SDN の RAS ゲートウェイ](sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)します。  
          
    - **ソフトウェア ロード バランサー (SLB) およびネットワーク アドレス変換 (NAT)** します。 北-南と東-西レイヤー 4 のロード バランサーと NAT がサポートの Direct Server Return 戻り値のネットワーク トラフィックが、負荷分散マルチプレクサーをバイパスできる、スループットを向上します。  
       詳細については、次を参照してください。 [ソフトウェアによる負荷分散と #40 です。SLB & #41 です。SDN の](sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md)です。  
  
    詳細については、次を参照してください。 [ネットワーク機能の仮想化](sdn/technologies/network-function-virtualization/Network-Function-Virtualization.md)します。  
  
-   **プロトコルを標準化**します。 ネットワーク コント ローラーは、JavaScript Object Notation (JSON) ペイロードをその northbound インターフェイスの Representational State Transfer (REST) を使用します。 ネットワーク コント ローラーの southbound インターフェイスは、Open vSwitch Database Management Protocol (OVSDB) を使用します。  
  
-   **柔軟なカプセル化テクノロジ**します。 これらのテクノロジは、データ プレーンで動作し、仮想拡張可能 LAN (VxLAN) と Network Virtualization Generic Routing Encapsulation (NVGRE) の両方をサポートします。 詳細については、次を参照してください。 [Windows Server 2016 の GRE トンネリング](../remote/remote-access/ras-gateway/gre-tunneling-windows-server.md)します。  
  
SDN の詳細については、次を参照してください。[ソフトウェアによるネットワーク制御&#40;SDN&#41;](sdn/software-defined-networking.md)します。  
  
### <a name="cloud-scale-fundamentals"></a>Cloud Scale Fundamentals
 
次のクラウド スケールの基礎は、使用可能なようになりました。  
  
-   **ネットワーク インターフェイス カード (NIC) を収束**します。 収束の NIC を使用すると、管理、リモート ダイレクト メモリ アクセスの RDMA 対応の記憶域を 1 つのネットワーク アダプターを使用して、テナント トラフィック。 これにより、さまざまな種類のサーバーごとのトラフィックを管理する以下のネットワーク アダプターを作成する必要があるために、データ センター内の各サーバーに関連付けられている資本支出が減少します。  
  
-   **パケット ダイレクト**します。  パケット ダイレクトでは、高いネットワーク トラフィックのスループットと低待機時間パケット処理インフラストラクチャを提供します。  
  
-   **スイッチ埋め込みチーミング (SET)** します。        セットは、HYPER-V 仮想スイッチに統合されている NIC チーミング ソリューションです。 セットは、可用性が向上し、フェールオーバーを提供します。 1 つのセット チームに最大 8 つの物理 NIC のチーミングを許可します。 Windows Server 2016 では、サーバー メッセージ ブロック (SMB)、および RDMA の使用に制限されているチームのセットを作成できます。 さらに、チームのセットを使用して、HYPER-V ネットワーク仮想化のネットワーク トラフィックを分散することができます。 詳細については、次を参照してください。 [リモート ダイレクト メモリ アクセス (&) #40 です。RDMA と #41 です。スイッチには、チーム化 (&) #40; が含まれているとセットと #41;](../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)します。  
  
## <a name="bkmk_existing"></a>追加のネットワーク テクノロジに対する新機能

このセクションには、使い慣れたネットワーク テクノロジに対する新機能に関する情報が含まれています。
  
## <a name="bkmk_dhcp"></a>DHCP  
DHCP は、プライベート イントラネットなど、TCP/IP ベースのネットワークにおいて、ホストの構成に伴う管理の負担と複雑さを低減することを目的に策定されたインターネット技術標準化委員会 (IETF) の標準です。 DHCP クライアントに TCP/IP を構成するプロセスは、DHCP サーバー サービスを使うことによって自動化されます。  
  
詳細については、次を参照してください。 [DHCP の新](technologies/dhcp/What-s-New-in-DHCP.md)します。  
  
## <a name="bkmk_dns"></a>DNS  
DNS は、TCP/IP ネットワーク内のコンピューターやネットワーク サービスの名前を解決するためのシステムです。 DNS 名によって、コンピューターやサービスをわかりやすい名前で特定することができます。 ユーザーがアプリケーションで DNS 名を入力すると、DNS サービスは入力された DNS 名を、その名前に関連付けられている他の情報 (IP アドレスなど) に解決できます。  
  
DNS クライアントおよび DNS サーバーに関する情報を次に示します。  
  
### <a name="bkmk_dnsc"></a>DNS クライアント  
新規または改善された DNS クライアント テクノロジを次に示します。  
  
-   **DNS クライアント サービスのバインド**します。 Windows 10 では、DNS クライアント サービスは、1 つ以上のネットワーク インターフェイスを持つコンピューターのサポートの強化を提供します。  
  
詳細については、次を参照してください[Windows Server 2016 での DNS クライアントでは新機能。](dns/What-s-New-in-DNS-Client.md)  
  
### <a name="bkmk_dnss"></a>DNS サーバー  
新規または改善された DNS サーバー テクノロジを次に示します。  
  
-   **DNS のポリシー**します。  DNS サーバーが DNS クエリに応答する方法を指定する DNS ポリシーを構成することができます。 DNS 応答は、クライアントの IP アドレス (場所) に基づくことができますの時間、日、その他のいくつかのパラメーター。 DNS のポリシーには、位置認識 DNS、トラフィック管理、負荷分散、スプリット ブレイン DNS、およびその他のシナリオが有効にします。  
  
-   **ファイルのサポートの Nano Server ベースの DNS**、Windows Server 2016 の Nano Server イメージ上の DNS サーバーを展開することができます。 使用する場合は、この展開オプションが使用できるファイル ベースの DNS です。 Nano Server イメージ上で実行中の DNS サーバーでは、面積、クイック起動、最小化された修正プログラムの適用と、DNS サーバーを実行できます。  
  
    > [!NOTE]   
    > Active Directory 統合 DNS は、Nano Server ではサポートされていません。  
  
-   **応答のレート制限 (RRL)** します。  DNS サーバーで応答レート制限を有効にできます。 これによりには、DNS サーバーを使用して、サービス拒否攻撃では、DNS クライアントを開始する悪意のあるシステムの可能性を回避します。  
  
-   **名前付きエンティティ (DANE) の DNS ベースの認証**します。   TLSA (トランスポート層セキュリティ認証) レコードを使用すると、どのような証明機関 (CA) からドメイン名の証明書が期待される必要があります状態 DNS クライアントに情報を提供します。 これは、場所、独自の web サイトを指す DNS キャッシュが破損する可能性があります、別の CA が発行された証明書を提供とだれかが、中間の攻撃を防ぎます。  
  
-   **不明なレコードのサポート**します。   
     不明なレコードの機能を使用して、Windows DNS サーバーによって明示的にサポートされていないレコードを追加することができます。  
  
-   **IPv6 ルート ヒント**します。   
     ルート ヒントをサポートして、IPV6 ルート サーバーを使用して、インターネット名前解決を実行するネイティブ IPV6 を使用することができます。  
  
-   **Windows PowerShell のサポート強化**します。   
      新しい Windows PowerShell コマンドレットは、DNS サーバー使用できます。  
  
詳細については、次を参照してください[Windows Server 2016 での DNS サーバーでは新機能。](dns/What-s-New-in-DNS-Server.md)  
  
## <a name="bkmk_GRE"></a>GRE トンネリング  
RAS ゲートウェイで、サイト間の接続とゲートウェイの M+N 冗長性の Generic Routing Encapsulation (GRE) トンネルの高可用性を実現できるようになりました。 GRE は軽量のトンネリング プロトコルで、インターネット プロトコル インターネットワークを介して Point-to-Point 仮想リンク内のさまざまなネットワーク レイヤー プロトコルをカプセル化できます。  
  
詳細については、次を参照してください。 [Windows Server 2016 の GRE トンネリング](../remote/remote-access/ras-gateway/gre-tunneling-windows-server.md)します。  
  
## <a name="HNV"></a>HYPER-V ネットワーク仮想化  
Windows Server 2012 で導入された、HYPER-V ネットワーク仮想化 (HNV) を使うと、共有の物理ネットワーク インフラストラクチャ上に顧客のネットワーク仮想化が可能です。 物理ネットワーク ファブリックのために必要な最小限の変更、HNV により、サービス プロバイダーをデプロイし、3 つのクラウド間で任意の場所テナントのワークロードを移行する機敏性: サービス プロバイダーのクラウド、プライベート クラウド、または Microsoft Azure パブリック クラウド。  
  
詳細については、次を参照してください[Windows Server 2016 で Hyper-v ネットワーク仮想化では新機能。](sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md)  
  
## <a name="bkmk_ipam"></a>IPAM  
IPAM では、組織のネットワーク上の IP アドレスと DNS インフラストラクチャの高度にカスタマイズ可能な管理および監視機能を提供します。 IPAM を使用して、監視できる、監査、動的ホスト構成プロトコル (DHCP) およびドメイン ネーム システム (DNS) を実行しているサーバーを管理および。  
  
-   **IP アドレスの管理を強化**します。  
     処理の/32 の IPv4 および IPv6/128 サブネットと IP アドレス ブロックで空き IP アドレスのサブネットと範囲の検索などのシナリオは、IPAM 機能が向上しました。  
  
-   **DNS サービスの管理を強化**します。  
     IPAM では、両方のドメインに参加している Active Directory に統合された、ファイルに格納された DNS サーバー、DNS リソース レコード、条件付きフォワーダー、および DNS ゾーンの管理をサポートしています。  
  
-   **DNS、DHCP、および IP アドレス (DDI) の管理を統合**します。  
     いくつかの新しいエクスペリエンスし統合型ライフ サイクル管理の操作が有効になっているなど、すべての DNS リソースを視覚化する IP に関連するレコード アドレス、IP アドレスの DNS リソース レコードと IP アドレスのライフ サイクル管理に基づく自動インベントリDNS と DHCP の両方の操作。  
  
-   **複数の Active Directory フォレストのサポート**します。  
     IPAM を使用して、IPAM がインストールされているフォレストおよび各リモート フォレストの間に双方向信頼関係がある場合に、複数の Active Directory フォレストの DNS および DHCP サーバーを管理することができます。  
  
-   **ロールベースのアクセス制御用 Windows PowerShell のサポート**します。  
     Windows PowerShell を使用して、IPAM オブジェクトにアクセス スコープを設定することができます。  
  
詳細については、次を参照してください。 [IPAM の新](technologies/ipam/What-s-New-in-IPAM.md)と[IPAM の管理](technologies/ipam/Manage-IPAM.md)します。  
  

