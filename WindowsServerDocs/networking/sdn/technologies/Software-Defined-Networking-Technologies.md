---
title: SDN テクノロジ
description: このセクションのトピックでは、概要と Windows Server 2016 に含まれているソフトウェア定義ネットワーク テクノロジに関する技術情報を提供します。
manager: dougkim
ms.prod: windows-server-threshold
ms.service: virtual-network
ms.technology: networking-sdn
ms.topic: article
ms.assetid: b491089c-5bcb-49d4-95b1-915b7ce69f88
ms.author: pashort
author: shortpatti
ms.date: 02/14/2019
ms.openlocfilehash: acf3e1dc3e5a229c525ba7cad23819640c0d5261
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59891163"
---
# <a name="sdn-technologies"></a>SDN テクノロジ

>適用対象:Windows Server 2019、Windows Server 2016、Windows Server (半期チャネル)

このセクションのトピックでは、概要と Windows Server 2016 に含まれているソフトウェア定義ネットワーク テクノロジに関する技術情報を提供します。  

## <a name="network-controllernetwork-controllernetwork-controllermd"></a>[ネットワーク コント ローラー](network-controller/Network-Controller.md)

ネットワーク コント ローラーは、automation を管理、構成、監視、および仮想の両方のトラブルシューティングを行うと、データ センターの物理ネットワーク インフラストラクチャの集中管理された、プログラミング可能なポイントを提供します。 ネットワーク コント ローラーとネットワーク デバイスとサービスを手動で構成を実行する代わりにネットワーク インフラストラクチャの構成を自動化できます。 

ネットワーク コント ローラーはスケーラブルな高可用性サーバーであり、2 つのアプリケーション プログラミング インターフェイス (Api) を提供します。

1. **Southbound API** – ネットワークと通信するために、ネットワーク コント ローラーを使用します。
2. **Northbound API** – ネットワーク コント ローラーと通信することができます。

次の物理および仮想ネットワーク インフラストラクチャを管理するのに Windows PowerShell、Representational State Transfer (REST) API、または管理アプリケーションを使用できます。

- Hyper-V VM と仮想スイッチ 
- 物理ネットワーク スイッチ 
- 物理ネットワーク ルーター 
- ファイアウォール ソフトウェア 
- VPN ゲートウェイ、リモート アクセス サービス (RAS) マルチ テナント ゲートウェイを含む 
- ロード バランサー 
  

  
## <a name="hyper-v-network-virtualizationhyper-v-network-virtualizationhyper-v-network-virtualizationmd"></a>[HYPER-V ネットワーク仮想化](hyper-v-network-virtualization/Hyper-V-Network-Virtualization.md)

HYPER-V ネットワーク仮想化 (HNV) では、仮想ネットワークを使用して、アプリケーションや、物理ネットワークからのワークロードを抽象化するのに役立ちます。 仮想ネットワークでは、共有の物理ネットワーク ファブリックで実行されているときに、必要なマルチ テナント分離を提供し、リソースの使用率を高めることができます。 実行できる転送、既存の投資を確保するには、既存のネットワーク装置上の仮想ネットワークを設定することができます。 また、仮想ネットワークは仮想ローカル エリア ネットワーク (Vlan) との互換性です。   
  
  
## <a name="hyper-v-virtual-switchvirtualizationhyper-v-virtual-switchhyper-v-virtual-switchmd"></a>[Hyper-V Virtual Switch](../../../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md) 

HYPER-V 仮想スイッチは、ソフトウェア ベースのレイヤー 2 イーサネット ネットワーク スイッチ、HYPER-V サーバーの役割をインストールした後、HYPER-V マネージャーで使用できます。 このスイッチには、仮想マシンを仮想ネットワークと物理ネットワークの両方に接続するための、プログラムで管理される拡張可能な機能が含まれています。 また、HYPER-V 仮想スイッチは、セキュリティ、分離、およびサービス レベルでポリシーの施行を提供します。
  
スイッチ埋め込みチーミング (SET) とリモート ダイレクト メモリ アクセス (RDMA)、HYPER-V 仮想スイッチを展開することもできます。 詳細については、セクションをご覧ください。[リモート ダイレクト メモリ アクセス (RDMA) とスイッチ埋め込みチーミング (SET)](#bkmk_rdma)このトピックの「します。  

## <a name="internal-dns-service-idns-for-sdnidns-for-sdnmd"></a>[SDN の内部の DNS サービス (Idn)](Idns-for-Sdn.md)

ホストされている仮想マシン (Vm) とアプリケーションにネットワーク内およびインターネット上の外部のリソースと通信する DNS が必要です。 Idn、テナントを分離、ローカルの名前空間とインターネット リソースの DNS 名前解決サービスを提供できます。 
  
## <a name="network-function-virtualizationnetwork-function-virtualizationnetwork-function-virtualizationmd"></a>[ネットワーク関数仮想化](network-function-virtualization/Network-Function-Virtualization.md)

ロード バランサー、ファイアウォール、ルーター、スイッチなどのハードウェア アプライアンスでは、仮想アプライアンスがますます。 Microsoft は、ネットワーク、スイッチ、ゲートウェイ、Nat、ロード バランサー、およびファイアウォールを仮想化します。 この「ネットワーク機能の仮想化」は、サーバーの仮想化とネットワーク仮想化の自然な流れです。 仮想アプライアンスは迅速に新たなと、新しい市場を作成します。 常に興味を引くと両方の仮想化プラットフォームで運動量を取得し、クラウド サービスです。 
  
次のネットワーク機能の仮想化テクノロジを利用できます。  
  
-   **ソフトウェア ロード バランサー (SLB) およびネットワーク アドレス変換 (NAT)** します。 戻り値のネットワーク トラフィックを負荷分散マルチプレクサーをバイパスできる Direct Server Return をサポートすることによってスループットを向上します。 詳細については、次を参照してください。 [SDN のソフトウェアの負荷分散/(SLB/)](network-function-virtualization/software-load-balancing-for-sdn.md)します。
  
-   **データ センターのファイアウォール**します。 VM インターフェイス レベルまたはサブネット レベルのファイアウォール ポリシーを適用することを有効にする詳細なアクセス制御リスト (Acl) を提供します。 詳細については、次を参照してください。[データ センターのファイアウォールの概要](network-function-virtualization/Datacenter-Firewall-Overview.md)します。
  
-   **SDN の RAS ゲートウェイ**します。 場所に関係なく、物理ネットワークと VM ネットワークのリソースの間のネットワーク トラフィックをルーティングします。 物理的に同じ場所またはさまざまな場所でネットワーク トラフィックをルーティングすることができます。 詳細については、次を参照してください。 [SDN の RAS ゲートウェイ](network-function-virtualization/RAS-Gateway-for-SDN.md)します。

  
## <a name="remote-direct-memory-access-rdma-and-switch-embedded-teaming-sethttpsdocsmicrosoftcomwindows-servervirtualizationhyper-v-virtual-switchrdma-and-switch-embedded-teaming"></a>[リモート ダイレクト メモリ アクセス (RDMA) とスイッチ埋め込みチーミング (SET)](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming)  
Windows Server 2016 ではなくスイッチ埋め込みチーミング (SET) または HYPER-V 仮想スイッチにバインドするネットワーク アダプターで RDMA を有効にできます。 これにより、RDMA、SET を使用するときに、以下のネットワーク アダプターを使用すると同時にします。  
  
セットは、Hyper-v ホストと、ソフトウェアによるネットワーク制御 (SDN) スタックを Windows Server 2016 に含まれる環境で使用できる代替 NIC チーミング ソリューションです。 セットは、HYPER-V 仮想スイッチにいくつかの NIC チーミング機能を統合します。  
  
セットには、1 つまたは 8 物理イーサネット ネットワーク アダプター間で 1 つまたは複数のソフトウェア ベースの仮想ネットワーク アダプターにグループ化することができます。 これらの仮想ネットワーク アダプターは、高速なパフォーマンスに加え、ネットワーク アダプターに障害が発生した場合のフォールト トレランスを提供します。  
チームに配置する同じ物理的な HYPER-V ホスト上で、セットのメンバーのネットワーク アダプターをすべてにインストールする必要があります。  
  
さらに、Windows PowerShell コマンドを使用して、データ センター ブリッジング (DCB) を有効化、RDMA 仮想 NIC (vNIC) と、HYPER-V 仮想スイッチを作成、SET と RDMA Vnic で HYPER-V 仮想スイッチを作成することができます。  

  

## <a name="border-gateway-protocol-bgpremoteremote-accessbgpborder-gateway-protocol-bgpmd"></a>[ボーダー ゲートウェイ プロトコル (BGP)](../../../remote/remote-access/bgp/Border-Gateway-Protocol-BGP.md)
  
ボーダー ゲートウェイ プロトコル (BGP) は、サイト対サイト VPN 接続を使用してサイト間のルートを自動的に学習を動的ルーティング プロトコルです。 そのため、BGP では、ルーターの手動構成が減少します。   RAS ゲートウェイを構成すると、BGP では、テナントの VM ネットワークとリモートのサイト間のネットワーク トラフィックのルーティングを管理することができます。  
  
## <a name="software-load-balancing-slb-for-sdnnetwork-function-virtualizationsoftware-load-balancing-for-sdnmd"></a>[ソフトウェアの負荷分散 (SLB) SDN](network-function-virtualization/software-load-balancing-for-sdn.md)
クラウド サービス プロバイダー (Csp) や SDN を展開する企業は、ソフトウェア負荷分散 (SLB) を使用してテナントおよび仮想ネットワーク リソース間でテナントのカスタマー ネットワーク トラフィックを均等に分散します。 Windows Server SLB により、同じワークロードをホストする複数のサーバーであり、高可用性とスケーラビリティを提供することです。 

## <a name="windows-server-containerscontainerscontainer-networking-overviewmd"></a>[Windows Server コンテナー](Containers/Container-networking-overview.md)

Windows Server コンテナーは、軽量のオペレーティング システム仮想化の方法が、同じコンテナー ホストで実行されている他のサービスからアプリケーションやサービスを分離します。 各コンテナーには、独自のオペレーティング システム、プロセス、ファイル システム、レジストリ、および IP アドレスは、仮想ネットワークに接続することができます。 


## <a name="system-center"></a>System Center  
デプロイし、管理は、SDN インフラストラクチャを[Virtual Machine Management (VMM)](https://docs.microsoft.com/system-center/vmm/)と[Operations Manager](https://docs.microsoft.com/system-center/scom/)します。 Vmm では、プロビジョニングし、作成してプライベート クラウドに仮想マシンとサービスをデプロイするために必要なリソースを管理します。  Operations manager では、早急な対応の問題を識別するために、エンタープライズ全体でサービス、デバイス、および操作を監視します。 


---