---
title: SDN Technologies
description: このセクションのトピックでは、概要と Windows Server 2016 に含まれているソフトウェア定義ネットワーク テクノロジに関する技術情報を提供します。
manager: brianlic
ms.prod: windows-server-threshold
ms.service: virtual-network
ms.technology: networking-sdn
ms.topic: article
ms.assetid: b491089c-5bcb-49d4-95b1-915b7ce69f88
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1f842ac0d1a09106c1898374cf8dd1c7823d7dae
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="sdn-technologies"></a>SDN Technologies

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このセクションのトピックでは、概要と Windows Server 2016 に含まれているソフトウェア定義ネットワーク テクノロジに関する技術情報を提供します。  
  
> [!NOTE]  
> 他のソフトウェアがネットワーク定義のドキュメント ライブラリの以下のセクションでを使用することができます。  
>   
> - [Plan SDN](../plan/Plan-Software-Defined-Networking.md)
> - [Deploy SDN](../deploy/Deploy-Software-Defined-Networking.md)
> - [Manage SDN](../manage/manage-sdn.md)
> - [Security for SDN](../security/sdn-security-top.md)
> - [Troubleshoot SDN](../troubleshoot/Troubleshoot-Software-Defined-Networking.md)

連携して、次のよう、Microsoft のソフトウェアによるネットワーク制御 (SDN) ソリューションを作成する多くのテクノロジがあります。  
  
-   **[ボーダー ゲートウェイ プロトコル (&) #40 です。BGP & #41 です。](../../../remote/remote-access/bgp/Border-Gateway-Protocol-BGP.md)**  
  
    Windows Server 2016 リモート アクセス サービス (RAS) ゲートウェイで構成されると、ボーダー ゲートウェイ プロトコル (BGP) により、テナントの VM ネットワークとそのリモート サイト間のネットワーク トラフィックのルーティングを管理する機能です。 BGP は、動的ルーティング プロトコルであり、サイト間 VPN 接続を使用して接続されているサイト間のルートが自動的に学習ためルーターを手動でルート構成の必要性が削減されます。  
  
-   **[データ センターのファイアウォールの概要](../../sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)**  
  
    データ センターのファイアウォールは、Windows Server 2016 に付属する新しいサービスです。 これは、ネットワーク層、5 組 (プロトコル、発信元と宛先のポート番号、送信元と送信先の IP アドレス)、ステートフルなマルチテナント ファイアウォールです。 展開すると、サービス プロバイダーによってサービスとして提供される、テナント管理者をインストールでき、インターネットからの不要なトラフィックから仮想ネットワークとイントラネット ネットワークを保護するためにファイアウォール ポリシーを構成できます。  
  
  
-   **[Hyper-V ネットワーク仮想化](../../sdn/technologies/hyper-v-network-virtualization/Hyper-V-Network-Virtualization.md)**  
  
    Hyper-V ネットワーク仮想化 (HNV) では、顧客のネットワーク共有の物理ネットワーク インフラストラクチャ上に仮想化が有効にします。  
  
- **[内部の DNS サービスと #40; Idn & #41 です。SDN の](../../sdn/technologies/Idns-for-Sdn.md)**

    仮想マシンをホスト型 \(VMs\) とアプリケーションは独自のネットワーク内およびインターネット上の外部のリソースと通信するために DNS が必要です。 Idn を提供できますテナント DNS 名前解決サービスでは、ローカルの分離された名前空間とインターネット リソース。

-   **[ネットワーク コントローラー](../../sdn/technologies/network-controller/Network-Controller.md)**  
  
    ネットワーク コントローラーは、管理、構成、監視、およびデータ センター内の仮想および物理ネットワーク インフラストラクチャのトラブルシューティングを行う自動化の集中管理された、プログラミング可能なポイントを提供します。  
  
-   **[ネットワーク関数仮想化](../../sdn/technologies/network-function-virtualization/Network-Function-Virtualization.md)**  
  
    (ロード バランサー、ファイアウォール、ルーター、スイッチ、およびなど) などのハードウェア アプライアンスで実行されているネットワーク機能がますます仮想アプライアンスとして仮想化されています。  
  
    Microsoft は、ネットワーク、スイッチ、ゲートウェイ、Nat、ロード バランサー、およびファイアウォールを仮想化します。  

-   **[SDN の RAS ゲートウェイ](../../sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)**
  
    RAS ゲートウェイは、ソフトウェア ベース、マルチテナント、ボーダー ゲートウェイ プロトコル (BGP) 対応ルーターはクラウド サービス プロバイダー (CSP) や Hyper-V ネットワーク仮想化を使用して複数のテナント仮想ネットワークをホストしているエンタープライズ向けに設計された Windows Server 2016 でです。  
      
- **[リモート ダイレクト メモリ アクセス (&) #40 です。RDMA と #41 です。スイッチ埋め込みチーミング (&) #40;セットと #41 です。](../../../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)**  
  
    収束の NIC を使用すると、単一のネットワーク アダプターを使用して RDMA とイーサネットの両方のトラフィックを結合します。 収束の NIC では、リモート ダイレクト メモリ アクセスの RDMA 対応の記憶域、管理用の単一のネットワーク アダプターを使用して、テナント トラフィックを行うことができます。 これにより、以下のネットワーク アダプターをさまざまな種類のサーバーごとのトラフィックを管理する必要があるために、データ センター内の各サーバーに関連付けられている設備投資が削減されます。  
  
    セットは、Hyper-V 仮想スイッチに統合されている NIC チーミング ソリューションです。 セットは、可用性が向上し、フェールオーバーを提供する 1 つのセット チームに最大 8 つの物理 NIC のチーム化できます。 Windows Server 2016 では、サーバー メッセージ ブロック (SMB) と RDMA の使用に制限されているチームのセットを作成できます。
  

-   **[ソフトウェアの負荷分散と #40 です。SLB & #41 です。SDN の](../../sdn/technologies/network-function-virtualization/software-load-balancing-for-sdn.md)**  

    クラウド サービス プロバイダー (CSP) および展開する企業はソフトウェアによるネットワーク制御 (SDN) Windows Server 2016 では、テナントおよびテナント仮想ネットワークのリソース間でのカスタマー ネットワーク トラフィックを均等に分散するのにソフトウェア負荷分散 (SLB) を使用できます。 Windows Server SLB 有効、同じワークロードをホストする複数のサーバーに高可用性とスケーラビリティを提供します。
  
-   **[System Center](../../sdn/Sc-Tech-for-Sdn.md)**展開し、ネットワーク コントローラー、ソフトウェア ロード バランサー、およびゲートウェイを含め、SDN インフラストラクチャの管理に System Center 2016 Virtual Machine Manager (VMM) と Operations Manager を使用することができます。 また、一元的に定義し、仮想ネットワーク ポリシーを制御およびアプリケーションやワークロードにポリシーをリンク VMM を使用することができます。
  
- **[Windows コンテナー](../technologies/Containers/Container-networking-overview.md)**
    
    Windows Server コンテナーは、軽量のオペレーティング システム仮想化の方法が、同じコンテナー ホストで実行されているその他のサービスからのアプリケーションまたはサービスを分離するために使用します。 これを有効にするのには、それぞれのコンテナーは、オペレーティング システム、プロセス、ファイル システム、レジストリ、および IP アドレスの独自のビューがします。 Windows Server 2016 では、仮想ネットワークへの Windows Server コンテナーを接続できます。 Windows コンテナーの機能はネットワークに関して言えば内の仮想マシンと同じようにします。 各コンテナーは、受信と送信トラフィックを転送する、仮想スイッチに接続されている仮想ネットワーク アダプターを持ちます。 同じホスト上のコンテナー間の分離を強制するには、各 Windows Server と HYPER-V コンテナーをコンテナーのネットワーク アダプターがインストールされているネットワーク コンパートメントが作成されます。 Windows Server のコンテナーでは、ホスト vNIC を使用して、仮想スイッチに接続します。 HYPER-V コンテナーは、(ユーティリティ VM に公開されません) 統合 VM NIC を使用して、仮想スイッチに接続します。

