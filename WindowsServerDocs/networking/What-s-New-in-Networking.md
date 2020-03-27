---
title: ネットワークの新機能
description: このトピックでは、Windows Server 2016 でのネットワークの新機能とテクノロジの概要について説明します。
ms.prod: windows-server
ms.technology: networking
ms.topic: get-started-article
ms.assetid: 08fb7563-d319-48a9-b181-ca0ca3032c18
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 35c3c3b2610918e8b0fd69ccf04422e3f6df4d0e
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80318547"
---
# <a name="whats-new-in-networking"></a>ネットワークの新機能

>適用対象: Windows Server 2016

Windows Server 2016 の新機能または強化されたネットワークテクノロジは次のとおりです。  
  Upd このトピックの内容は次のとおりです。  
  
-   [新しいネットワーク機能とテクノロジ](#bkmk_features)  
  
-   [追加のネットワークテクノロジの新機能](#bkmk_existing)  
  
## <a name="new-networking-features-and-technologies"></a><a name="bkmk_features"></a>新しいネットワーク機能とテクノロジ

ネットワークは、ソフトウェア定義データセンター (SDDC) プラットフォームの基本部分であり、Windows Server 2016 では、組織にとって完全に実現された SDDC ソリューションへの移行を支援するための、ソフトウェアによるネットワーク制御 (SDN) テクノロジが新たに強化されています。  
  
ネットワークをソフトウェアによって定義されたリソースとして管理する場合、アプリケーションのインフラストラクチャ要件を1回記述し、アプリケーションの実行場所 (オンプレミスまたはクラウド) を選択することができます。  この一貫性は、アプリケーションのスケーリングが容易になり、セキュリティ、パフォーマンス、サービス品質、可用性に関して自信を持ってアプリケーションをシームレスに実行できるようになることを意味します。  
  
次のセクションでは、これらの新しいネットワーク機能とテクノロジについて説明します。  
  
### <a name="software-defined-networking-infrastructure"></a>ソフトウェア定義ネットワークインフラストラクチャ

次に、新しい SDN インフラストラクチャテクノロジと強化された SDN インフラストラクチャテクノロジを示します。  
  
-   **ネットワークコントローラー**。 Windows Server 2016 の新機能ネットワークコントローラーは、データセンター内の仮想および物理ネットワークインフラストラクチャの管理、構成、監視、およびトラブルシューティングを行うための、一元化されたプログラミング可能な自動化ポイントを提供します。 ネットワーク コントローラーを使用すると、ネットワーク インフラストラクチャの構成を自動化できます。ネットワーク デバイスとサービスを手動で構成する必要はありません。 詳細については、「[ネットワークコントローラー](sdn/technologies/network-controller/Network-Controller.md) 」と「[スクリプトを使用したソフトウェア定義ネットワークの展開](https://technet.microsoft.com/library/mt427380.aspx)」を参照してください。  
  
-   **Hyper-v 仮想スイッチ**。 Hyper-v 仮想スイッチは、Hyper-v ホスト上で実行され、分散型の切り替えとルーティング、および Microsoft Azure と整合し、互換性のあるポリシーの適用層を作成できます。 詳しくは、「[Hyper-V 仮想スイッチの概要](../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md)」を参照してください。  
  
-   **ネットワーク機能の仮想化 (NFV)** 。 現在のソフトウェア定義データセンターでは、ハードウェアアプライアンス (ロードバランサー、ファイアウォール、ルーター、スイッチなど) によって実行されるネットワーク機能が、仮想アプライアンスとして展開されることが増えています。 この「ネットワーク機能の仮想化」は、サーバーの仮想化とネットワーク仮想化の自然な流れです。 仮想アプライアンスが急速に登場し、新しい市場が作成されます。 常に興味を引くと両方の仮想化プラットフォームで運動量を取得し、クラウド サービスです。 Windows Server 2016 では、次の NFV テクノロジを利用できます。  
  
    -   **データセンターのファイアウォール**。 この分散型ファイアウォールは、きめ細かなアクセス制御リスト (Acl) を提供します。これにより、ファイアウォールポリシーを VM インターフェイスレベルまたはサブネットレベルで適用できます。  
  
        詳細については、次を参照してください。 [データ センターのファイアウォールの概要](sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)します。  
  
    -   **RAS ゲートウェイ**。 RAS ゲートウェイを使用して、クラウドデータセンターからテナントのリモートサイトへのサイト間 VPN 接続など、仮想ネットワークと物理ネットワーク間のトラフィックをルーティングできます。 具体的には、インターネットキー交換バージョン 2 (IKEv2) のサイト間仮想プライベートネットワーク (Vpn)、レイヤー 3 (L3) VPN、および汎用ルーティングカプセル化 (GRE) ゲートウェイを展開できます。 さらに、ゲートウェイプールと M + N 個のゲートウェイの冗長性がサポートされるようになりました。および Border Gateway Protocol (BGP) とルートリフレクター機能を使用すると、すべてのゲートウェイシナリオ (IKEv2 VPN、GRE VPN、および L3 VPN) のネットワーク間で動的ルーティングを行うことができます。  
  
        詳細については、「 [Ras ゲートウェイの新機能](sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md)」および「 [SDN の ras ゲートウェイ](sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)」を参照してください。  
          
    - **ソフトウェア Load Balancer (SLB) とネットワークアドレス変換 (NAT)** 。 北南部と東西部のレイヤー4のロードバランサーと NAT は、Direct Server Return をサポートすることでスループットを向上させます。この場合、ネットワークトラフィックの戻り値は、負荷分散マルチプレクサーをバイパスできます。  
       詳細については、次を参照してください。 [ソフトウェアによる負荷分散と #40 です。SLB & #41 です。SDN の](sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md)です。  
  
    詳細については、次を参照してください。 [ネットワーク機能の仮想化](sdn/technologies/network-function-virtualization/Network-Function-Virtualization.md)します。  
  
-   **標準化**されたプロトコル。 ネットワークコントローラーは、JavaScript Object Notation (JSON) ペイロードを使用して、northbound インターフェイスで表現を使用します。 ネットワークコントローラーの southbound インターフェイスでは、Open vSwitch のデータベース管理プロトコル ([のデータの表示]) を使用します。  
  
-   **柔軟なカプセル化テクノロジ**。 これらのテクノロジはデータプレーンで動作し、仮想拡張 LAN (VxLAN) とネットワーク仮想化汎用ルーティングカプセル化 (NVGRE) の両方をサポートします。 詳細については、「 [Windows Server 2016 の GRE トンネリング](../remote/remote-access/ras-gateway/gre-tunneling-windows-server.md)」を参照してください。  
  
SDN の詳細については、「 [Software &#40;Defined&#41;network SDN](sdn/software-defined-networking.md)」を参照してください。  
  
### <a name="cloud-scale-fundamentals"></a>クラウドスケールの基礎
 
次のクラウドスケールの基礎を利用できるようになりました。  
  
-   **収束ネットワークインターフェイスカード (NIC)** 。 収束 NIC を使用すると、管理、リモートダイレクトメモリアクセス (RDMA) 対応の記憶域、およびテナントトラフィックに対して単一のネットワークアダプターを使用できます。 これにより、サーバーごとに異なる種類のトラフィックを管理するために必要なネットワークアダプターが少なくなるため、データセンター内の各サーバーに関連付けられている設備投資が削減されます。  
  
-   **パケットダイレクト**。  パケットダイレクトは、ネットワークトラフィックのスループットと待機時間の短いパケット処理インフラストラクチャを提供します。  
  
-   **埋め込みチーミング (SET) を切り替え**ます。        SET は、HYPER-V 仮想スイッチに統合されている NIC チーミング ソリューションです。 SET は最大 8 つの物理 NIC を 1 つのチームにチーミングし、可用性を向上させ、フェールオーバーを提供します。 Windows Server 2016 では、サーバー メッセージ ブロック (SMB) および RDMA の使用に制限されている SET チームを作成できます。 さらに、SET チームを使用して、HYPER-V ネットワーク仮想化のネットワーク トラフィックを分散することができます。 詳細については、次を参照してください。 [リモート ダイレクト メモリ アクセス (&) #40 です。RDMA と #41 です。スイッチには、チーム化 (&) #40; が含まれているとセットと #41;](../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)します。  
  
## <a name="new-features-for-additional-networking-technologies"></a><a name="bkmk_existing"></a>追加のネットワークテクノロジの新機能

ここでは、使い慣れたネットワークテクノロジの新機能について説明します。
  
## <a name="dhcp"></a><a name="bkmk_dhcp"></a>列挙  
DHCP は、プライベート イントラネットなど、TCP/IP ベースのネットワークにおいて、ホストの構成に伴う管理の負担と複雑さを低減することを目的に策定されたインターネット技術標準化委員会 (IETF) の標準です。 DHCP クライアントに TCP/IP を構成するプロセスは、DHCP サーバー サービスを使うことによって自動化されます。  
  
詳細については、「 [DHCP の新機能](technologies/dhcp/What-s-New-in-DHCP.md)」を参照してください。  
  
## <a name="dns"></a><a name="bkmk_dns"></a>DNS  
DNS は、TCP/IP ネットワーク内のコンピューターやネットワーク サービスの名前を解決するためのシステムです。 DNS 名によって、コンピューターやサービスをわかりやすい名前で特定することができます。 ユーザーがアプリケーションで DNS 名を入力すると、DNS サービスは入力された DNS 名を、その名前に関連付けられている他の情報 (IP アドレスなど) に解決できます。  
  
DNS クライアントと DNS サーバーに関する情報を次に示します。  
  
### <a name="dns-client"></a><a name="bkmk_dnsc"></a>DNS クライアント  
次に、新しいまたは強化された DNS クライアントテクノロジを示します。  
  
-   **DNS クライアントのサービスバインド**。 Windows 10 では、DNS クライアントサービスは、複数のネットワークインターフェイスを持つコンピューターの拡張サポートを提供します。  
  
詳細については、「 [Windows Server 2016 の DNS クライアントの新機能](dns/What-s-New-in-DNS-Client.md)」を参照してください。  
  
### <a name="dns-server"></a><a name="bkmk_dnss"></a>DNS サーバー  
次に、新しいまたは強化された DNS サーバーテクノロジを示します。  
  
-   **DNS ポリシー**。  Dns ポリシーを構成して、dns サーバーが DNS クエリにどのように応答するかを指定できます。 DNS 応答は、クライアントの IP アドレス (場所)、時刻、およびその他のいくつかのパラメーターに基づいています。 DNS ポリシーを使用すると、場所を認識する DNS、トラフィック管理、負荷分散、スプリットブレイン DNS などのシナリオが可能になります。  
  
-   **Nano server でのファイルベースの dns のサポート**では、Windows server 2016 の dns サーバーを nano server イメージに展開できます。 この展開オプションは、ファイルベースの DNS を使用している場合に使用できます。 Nano Server イメージで DNS サーバーを実行することで、フットプリントの削減、クイックブート、および修正プログラムの適用を最小限に抑えて、DNS サーバーを実行できます。  
  
    > [!NOTE]   
    > Active Directory 統合 DNS は、Nano Server ではサポートされていません。  
  
-   **応答レート制限 (RRL)** 。  DNS サーバーで応答率の制限を有効にすることができます。 これにより、dns サーバーを使用している悪意のあるシステムが、DNS クライアントでサービス拒否攻撃を開始する可能性を回避できます。  
  
-   **名前付きエンティティ (DANE) の DNS ベースの認証**。   TLSA (トランスポート層セキュリティ認証) レコードを使用して、証明書の発行元の証明機関 (CA) がドメイン名に対して要求する情報を DNS クライアントに提供することができます。 これにより、他のユーザーが DNS キャッシュを破損して独自の web サイトを参照し、別の CA から発行された証明書を提供する man-in-the-middle 攻撃を防ぐことができます。  
  
-   **不明なレコードのサポート**。   
     不明なレコード機能を使用して、Windows DNS サーバーで明示的にサポートされていないレコードを追加することができます。  
  
-   **IPv6 のルートヒント**。   
     IPV6 ルートサーバーを使用して、インターネットの名前解決を実行するには、ネイティブ IPV6 ルートヒントのサポートを使用できます。  
  
-   **Windows PowerShell のサポートが強化**されました。   
      DNS サーバーでは、新しい Windows PowerShell コマンドレットを使用できます。  
  
詳細については、「 [Windows server 2016 の DNS サーバーの新機能](dns/What-s-New-in-DNS-Server.md)」を参照してください。  
  
## <a name="gre-tunneling"></a><a name="bkmk_GRE"></a>GRE トンネリング  
RAS ゲートウェイは、サイト間接続のための高可用性汎用ルーティングカプセル化 (GRE) トンネルと、ゲートウェイの M + N 冗長性をサポートするようになりました。 GRE は軽量のトンネリング プロトコルで、インターネット プロトコル インターネットワークを介して Point-to-Point 仮想リンク内のさまざまなネットワーク レイヤー プロトコルをカプセル化できます。  
  
詳細については、「 [Windows Server 2016 の GRE トンネリング](../remote/remote-access/ras-gateway/gre-tunneling-windows-server.md)」を参照してください。  
  
## <a name="hyper-v-network-virtualization"></a><a name="HNV"></a>Hyper-v ネットワーク仮想化  
Windows Server 2012 で導入された Hyper-v ネットワーク仮想化 (HNV) を使用すると、共有の物理ネットワークインフラストラクチャ上で顧客ネットワークを仮想化することができます。 HNV では、物理ネットワークファブリックに必要な変更を最小限に抑えて、サービスプロバイダーは、サービスプロバイダークラウド、プライベートクラウド、または Microsoft Azure パブリッククラウドの3つのクラウド全体で、テナントのワークロードをデプロイおよび移行する機敏性を提供します。  
  
詳細については、「 [Windows Server 2016 での Hyper-v ネットワーク仮想化の新機能](sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md)」を参照してください。  
  
## <a name="ipam"></a><a name="bkmk_ipam"></a>IPAM  
IPAM は、組織のネットワーク上の IP アドレスと DNS インフラストラクチャに高度なカスタマイズが可能な管理および監視機能を提供します。 IPAM を使用すると、動的ホスト構成プロトコル (DHCP) とドメインネームシステム (DNS) を実行しているサーバーの監視、監査、および管理を行うことができます。  
  
-   **IP アドレスの管理が強化**されました。  
     IPv4/32 および IPv6/128 サブネットの処理や、IP アドレスブロック内の空き IP アドレスのサブネットと範囲の検索などのシナリオでは、IPAM 機能が強化されています。  
  
-   強化された**DNS サービス管理**。  
     IPAM では、ドメインに参加している Active Directory 統合 DNS サーバーとファイルベースの DNS サーバーの両方について、DNS リソースレコード、条件付きフォワーダー、および DNS ゾーン管理がサポートされています。  
  
-   **統合 DNS、DHCP、IP アドレス (DDI) の管理**。  
     いくつかの新しいエクスペリエンスと統合ライフサイクル管理操作が可能になりました。たとえば、IP アドレスに関連するすべての DNS リソースレコードの視覚化、DNS リソースレコードに基づく IP アドレスの自動インベントリ、IP アドレスのライフサイクル管理などです。DNS と DHCP の両方の操作に使用します。  
  
-   **複数の Active Directory フォレストのサポート**。  
     Ipam がインストールされているフォレストと各リモートフォレストの間に双方向の信頼関係がある場合は、IPAM を使用して複数の Active Directory フォレストの DNS および DHCP サーバーを管理できます。  
  
-   **Windows PowerShell では、ロールベースの Access Control がサポートして**います。  
     Windows PowerShell を使用して、IPAM オブジェクトのアクセススコープを設定できます。  
  
詳細については、「 [ipam の新機能](technologies/ipam/What-s-New-in-IPAM.md)」および「 [ipam の管理](technologies/ipam/Manage-IPAM.md)」を参照してください。  
  

