---
title: ネットワークの新機能
description: このトピックの「Windows Server 2016 でネットワークの新機能とテクノロジに関する情報概要を提供します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: get-started-article
ms.assetid: 08fb7563-d319-48a9-b181-ca0ca3032c18
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 85b1a573e8ac724a2a9e22863f890db668423cad
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="whats-new-in-networking"></a>ネットワークの新機能

>Windows Server 2016 の適用対象:

Windows Server 2016 で拡張された、または新しいネットワーク テクノロジを次に示します。  
  
このトピックには、次のセクションが含まれています。  
  
-   [新しいネットワーク機能およびテクノロジ](#bkmk_features)  
  
-   [その他のネットワーク テクノロジに対する新機能](#bkmk_existing)  
  
## <a name="bkmk_features"></a>新しいネットワーク機能およびテクノロジ

ネットワークは、ソフトウェア定義されているデータ センター (SDDC) プラットフォームの根幹し、Windows Server 2016 は、組織の完全に実現された SDDC ソリューションに移動するための新機能と更新のソフトウェアによるネットワーク制御 (SDN) テクノロジを提供します。  
  
ソフトウェア定義されているリソースとしてネットワークを管理するときに、アプリケーションのインフラストラクチャ要件を 1 回、説明を選び、アプリケーションを実行する - 内部設置型またはクラウドにします。  この一貫性ことを示し、アプリケーションがスケーリングがより容易になりましたを等しい自信セキュリティ、パフォーマンス、サービス、および可用性の品質シームレスにどこからでも、アプリケーションを実行できます。  
  
次のセクションでは、新しいネットワーク機能およびテクノロジこれらに関する情報を含めます。  
  
### <a name="software-defined-networking-infrastructure"></a>ソフトウェアによるネットワーク制御インフラストラクチャ

新しい、または改良されて SDN インフラストラクチャ テクノロジを次に示します。  
  
-   **ネットワーク コントローラー**します。 新しいネットワーク コントローラーは、Windows Server 2016 での管理、構成、監視、およびデータ センター内の仮想および物理ネットワーク インフラストラクチャのトラブルシューティングを行う自動化の集中管理された、プログラミング可能なポイントを提供します。 ネットワーク コントローラーを使用して、ネットワーク デバイスとサービスを手動で構成を実行するのではなく、ネットワーク インフラストラクチャの構成を自動化することができます。 詳細については、次を参照してください。[ネットワーク コントローラー](sdn/technologies/network-controller/Network-Controller.md)と[展開のソフトウェア定義ネットワーク スクリプトを使用した](https://technet.microsoft.com/library/mt427380.aspx)します。  
  
-   **Hyper-V 仮想スイッチ**します。 Hyper-V 仮想スイッチは、Hyper-V ホストで実行され、分散切り替えとルーティング、作成することができます、ポリシーの実施レイヤーを配置および Microsoft Azure との互換性。 詳細については、次を参照してください。[Hyper-v 仮想スイッチ](../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md)します。  
  
-   **ネットワーク関数仮想化 (NFV)**します。 今日のソフトウェアで定義されているデータ センター、(ロード バランサー、ファイアウォール、ルーター、スイッチ、およびなど) などのハードウェア アプライアンスで実行されているネットワーク機能がますます導入され仮想アプライアンスとして。 この「ネットワーク関数仮想化」は、サーバー仮想化とネットワーク仮想化の自然な流れです。 仮想アプライアンスはすばやく顕在化しつつ、新しい市場を作成します。 興味を引くと両方の仮想化プラットフォームで運動量を取得し、クラウド サービスを続行します。 Windows Server 2016 では、次の NFV テクノロジを利用できます。  
  
    -   **データ センターのファイアウォール**します。 この分散型のファイアウォールは、VM のインターフェイスのレベル、またはサブネット レベルでのファイアウォール ポリシーを適用できるように細かくアクセス制御リスト (Acl) を提供します。  
  
        詳細については、次を参照してください。[データ センターのファイアウォールの概要](sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)します。  
  
    -   **RAS ゲートウェイ**します。 RAS ゲートウェイは、仮想ネットワークとテナントのリモート サイトへのクラウド データ センターから、サイト間 VPN 接続を含め、物理ネットワーク間のトラフィックをルーティングに使用できます。 インターネット キー交換バージョン 2 (IKEv2) を展開する具体的には、サイト間仮想プライベート ネットワーク (Vpn)、レイヤー 3 (L3) VPN、および汎用ルーティング カプセル化 (GRE) ゲートウェイです。 また、ゲートウェイ プールとゲートウェイの M と N の冗長性がサポートされています。ボーダー ゲートウェイ プロトコル (BGP) のルート Reflector 機能がすべてのゲートウェイ シナリオ (IKEv2 VPN、GRE VPN、および L3 VPN) のネットワーク間での動的ルーティングを提供します。  
  
        詳細については、次を参照してください。[RAS ゲートウェイの新](sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md)と[SDN の RAS ゲートウェイ](sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)します。  
          
    - **ソフトウェア ロード バランサー (SLB) とネットワーク アドレス変換 (NAT)**します。 東西部と北南レイヤー 4 のロード バランサーと、NAT がサポートすることで Direct Server Return 戻り値のネットワーク トラフィックが、負荷分散マルチプレクサーをバイパスできますスループットを向上します。  
       詳細については、次を参照してください。[ソフトウェアの負荷分散と #40 です。SLB & #41 です。SDN の](sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md)します。  
  
    詳細については、次を参照してください。[ネットワーク関数仮想化](sdn/technologies/network-function-virtualization/Network-Function-Virtualization.md)します。  
  
-   **プロトコルを標準化**します。 ネットワーク コントローラーは、JavaScript Object Notation (JSON) ペイロードを持つ northbound そのインターフェイスで、Representational State Transfer (REST) を使用します。 ネットワーク コントローラーの southbound インターフェイスは、Open vSwitch データベース Management Protocol (OVSDB) を使用します。  
  
-   **柔軟なカプセル化テクノロジ**します。 これらのテクノロジは、データ平面で動作し、仮想拡張可能 LAN (VxLAN) とネットワーク仮想化汎用ルーティング カプセル化 (NVGRE) の両方をサポートします。 詳細については、次を参照してください。[Windows Server 2016 の GRE トンネリング](../remote/remote-access/ras-gateway/gre-tunneling-windows-server.md)します。  
  
SDN の詳細については、次を参照してください。[ソフトウェア定義ネットワーク (&) #40 です。SDN & #41 です。](sdn/software-defined-networking.md).  
  
### <a name="cloud-scale-fundamentals"></a>クラウド スケールの基礎
 
次のクラウド スケールの基礎を利用できるようになりましたできます。  
  
-   **集約型のネットワーク インターフェイス カード (NIC)**します。 収束の NIC では、リモート ダイレクト メモリ アクセスの RDMA 対応の記憶域、管理用の単一のネットワーク アダプターを使用して、テナント トラフィックを行うことができます。 これにより、以下のネットワーク アダプターをさまざまな種類のサーバーごとのトラフィックを管理する必要があるために、データ センター内の各サーバーに関連付けられている設備投資が削減されます。  
  
-   **パケット ダイレクト**します。  パケット ダイレクトでは、高いネットワーク トラフィックのスループットと低待機時間パケット処理インフラストラクチャを提供します。  
  
-   **スイッチ埋め込みチーミング (SET)**します。        セットは、Hyper-V 仮想スイッチに統合されている NIC チーミング ソリューションです。 セットは、可用性が向上し、フェールオーバーを提供する 1 つのセット チームに最大 8 つの物理 NIC のチーム化できます。 Windows Server 2016 では、サーバー メッセージ ブロック (SMB) と RDMA の使用に制限されているチームのセットを作成できます。 さらに、Hyper-V ネットワーク仮想化のネットワーク トラフィックを分散するのにチームのセットを使用することができます。 詳細については、次を参照してください。[リモート ダイレクト メモリ アクセス (&) #40 です。RDMA と #41 です。スイッチ埋め込みチーミング (&) #40;セットと #41 です。](../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md).  
  
## <a name="bkmk_existing"></a>その他のネットワーク テクノロジに対する新機能

このセクションには、使い慣れたネットワー キング テクノロジに対する新機能に関する情報が含まれています。
  
## <a name="bkmk_dhcp"></a>DHCP  
DHCP は、プライベート イントラネットなど、IP ベース ネットワーク上のホストの構成の複雑さ、管理の負担を軽減するように設計されたインターネット技術標準化委員会 (IETF) 標準です。 DHCP サーバー サービスを使用すると、DHCP クライアントに TCP/IP を構成するプロセスは自動です。  
  
詳細については、次を参照してください。[DHCP の新](technologies/dhcp/What-s-New-in-DHCP.md)します。  
  
## <a name="bkmk_dns"></a>DNS  
DNS は、コンピューターやネットワーク サービスの名前付けの TCP/IP ネットワークで使用されているシステム。 DNS の名前付けコンピューターやサービスをわかりやすい名前を検索します。 アプリケーションで DNS 名を入力すると、すると、DNS サービスは、IP アドレスなど、名前に関連付けられている他の情報に名前を解決することができます。  
  
DNS クライアントおよび DNS サーバーに関する情報を次に示します。  
  
### <a name="bkmk_dnsc"></a>DNS クライアント  
新しい、または改良されて DNS クライアントのテクノロジを次に示します。  
  
-   **DNS クライアント サービスのバインド**します。 Windows 10 では、DNS クライアント サービスは、1 つ以上のネットワーク インターフェイスを備えたコンピューターの拡張サポートを提供します。  
  
詳細については、次を参照してください[Windows Server 2016 での DNS クライアントの新。](dns/What-s-New-in-DNS-Client.md)  
  
### <a name="bkmk_dnss"></a>DNS サーバー  
新規または改善された DNS サーバー テクノロジを次に示します。  
  
-   **DNS のポリシー**します。  DNS サーバーが DNS クエリに応答する方法を指定する DNS ポリシーを構成することができます。 クライアント IP アドレス (場所) に基づいて DNS 応答できる時間帯、およびその他のいくつかのパラメーターです。 DNS のポリシーには、位置情報に対応の DNS、トラフィックの管理、負荷分散、スプリット ブレイン DNS、およびその他のシナリオが有効にします。  
  
-   **ファイルのサポートの Nano Server ベースの DNS**、Nano Server イメージに Windows Server 2016 での DNS サーバーを展開することができます。 この展開オプションは使用することを使用している場合は、ファイル ベースの DNS します。 Nano Server イメージ上で実行されている DNS サーバー、フット、クイック起動を最小化された修正プログラムの適用と、DNS サーバーを実行できます。  
  
    > [!NOTE]   
    > Active Directory 統合 DNS は、Nano Server ではサポートされていません。  
  
-   **応答のレート制限 (RRL)**します。  DNS サーバーに応答レート制限を有効にすることができます。 これにより、悪意のあるシステムで、サービス拒否攻撃を DNS クライアントで開始するように DNS サーバーを使用する可能性を回避します。  
  
-   **名前付きエンティティ (DANE) の DNS ベースの認証**します。   TLSA (トランスポート層セキュリティ認証) レコードを使用すると、状態のどのような証明機関 (CA) が期待どおりに確実から証明書をドメイン名の DNS クライアントに情報を提供します。 これは、場所受注の Web サイト] をポイントする DNS キャッシュが破損する可能性があります、別の CA が発行された証明書を提供と他のユーザーの中間の攻撃を防ぎます。  
  
-   **不明なレコード サポート**します。   
     不明なレコードの機能を使用して Windows DNS サーバーによって明示的にサポートされていないレコードを追加することができます。  
  
-   **IPv6 ルート ヒント**します。   
     ルート ヒントをサポートして IPV6 ルート サーバーを使用して、インターネット名前解決を実行するネイティブ IPV6 を使用することができます。  
  
-   **Windows PowerShell のサポートを強化しました**します。   
      DNS サーバーの新しい Windows PowerShell コマンドレットを利用できます。  
  
詳細については、次を参照してください[Windows Server 2016 での DNS サーバーの新。](dns/What-s-New-in-DNS-Server.md)  
  
## <a name="bkmk_GRE"></a>GRE トンネリング  
RAS ゲートウェイは、サイト間の接続とゲートウェイの M と N の冗長性のようになりました汎用ルーティング カプセル化 (GRE) トンネルの高可用性をサポートします。 GRE は、インターネット プロトコル インターネットワークを介して point-to-point 仮想リンク内のネットワーク レイヤー プロトコルのさまざまなをカプセル化できる軽量のトンネリング プロトコルです。  
  
詳細については、次を参照してください。[Windows Server 2016 の GRE トンネリング](../remote/remote-access/ras-gateway/gre-tunneling-windows-server.md)します。  
  
## <a name="HNV"></a>Hyper-V ネットワーク仮想化  
Windows Server 2012 で導入された、Hyper-V ネットワーク仮想化 (HNV) には、顧客のネットワーク共有の物理ネットワーク インフラストラクチャ上に仮想化が有効にします。 物理ネットワーク ファブリックで必要な最小限の変更、HNV により、サービス プロバイダーを展開し、次の 3 つのクラウド全体でテナント ワークロードを移行して任意の場所の機敏性: サービス プロバイダー クラウド、プライベート クラウド、または Microsoft Azure パブリック クラウドします。  
  
詳細については、次を参照してください[Windows Server 2016 で Hyper-v ネットワーク仮想化の新。](sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md)  
  
## <a name="bkmk_ipam"></a>IPAM  
IPAM では、組織のネットワークの IP アドレスと DNS インフラストラクチャに高度にカスタマイズ可能な管理および監視機能を提供します。 IPAM を使用して、監視、監査、でき動的ホスト構成プロトコル (DHCP) およびドメイン ネーム システム (DNS) を実行しているサーバーを管理できます。  
  
-   **IP アドレス管理を強化**します。  
     IPv4/32、IPv6 場合は/128 のサブネットを処理し、IP アドレス ブロックでの空き IP アドレスのサブネットと範囲の検索などのシナリオは、IPAM 機能が向上しました。  
  
-   **DNS サービスの管理を強化**します。  
     IPAM では、両方のドメインに参加している Active Directory 統合され、ファイルに格納された DNS サーバーの DNS リソース レコード、条件付きフォワーダは、および DNS ゾーンの管理をサポートします。  
  
-   **統合された DNS、DHCP、および IP アドレス (DDI) 管理**します。  
     いくつか新しいエクスペリエンスとの統合のライフ サイクル管理、IP アドレスに関連するすべての DNS リソース レコードを視覚化するなどの操作が有効には、DNS リソース レコードと DNS と DHCP の両方の IP アドレスのライフ サイクル管理に基づいて IP アドレスのインベントリに自動化されています。  
  
-   **複数の Active Directory フォレストのサポート**します。  
     IPAM を使用して、IPAM がインストールされているフォレストおよび各リモートのフォレストの間に双方向信頼関係がある場合は、複数の Active Directory フォレストの DNS および DHCP サーバーを管理することができます。  
  
-   **Role Based Access Control 用 Windows PowerShell のサポート**します。  
     Windows PowerShell を使用して、IPAM オブジェクトにアクセス スコープを設定することができます。  
  
詳細については、次を参照してください。[IPAM の新](technologies/ipam/What-s-New-in-IPAM.md)と[IPAM の管理](technologies/ipam/Manage-IPAM.md)します。  
  

