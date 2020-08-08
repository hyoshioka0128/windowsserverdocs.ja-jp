---
title: SDN テクノロジ
description: このセクションのトピックでは、Windows Server 2016 に含まれるソフトウェア定義ネットワークテクノロジの概要と技術情報について説明します。
manager: grcusanz
ms.topic: article
ms.assetid: b491089c-5bcb-49d4-95b1-915b7ce69f88
ms.author: anpaul
author: AnirbanPaul
ms.date: 02/14/2019
ms.openlocfilehash: 591a81c91dc444cfe48f0fa40142489b72142409
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87952572"
---
# <a name="sdn-technologies"></a>SDN テクノロジ

>適用先:Windows Server 2019、Windows Server 2016、Windows Server (半期チャネル)

このセクションのトピックでは、Windows Server 2016 に含まれるソフトウェア定義ネットワークテクノロジの概要と技術情報について説明します。

## <a name="network-controller"></a>[ネットワーク コントローラー](network-controller/Network-Controller.md)

ネットワークコントローラーは、データセンター内の仮想および物理ネットワークインフラストラクチャの管理、構成、監視、およびトラブルシューティングを行うための、一元化されたプログラミング可能な自動化ポイントを提供します。 ネットワークコントローラーを使用すると、ネットワークデバイスやサービスを手動で構成する代わりに、ネットワークインフラストラクチャの構成を自動化できます。

ネットワークコントローラーは、可用性が高くスケーラブルなサーバーで、次の2つのアプリケーションプログラミングインターフェイス (Api) を提供します。

1. **SOUTHBOUND API** –ネットワークコントローラーがネットワークと通信できるようにします。
2. **NORTHBOUND API** –ネットワークコントローラーと通信できるようにします。

Windows PowerShell、表現的な状態転送 (REST) API、または管理アプリケーションを使用して、次の物理および仮想ネットワークインフラストラクチャを管理できます。

- Hyper-V VM と仮想スイッチ
- 物理ネットワーク スイッチ
- 物理ネットワーク ルーター
- ファイアウォール ソフトウェア
- VPN ゲートウェイ (リモートアクセスサービス (RAS) マルチテナントゲートウェイを含む)
- ロード バランサー

## <a name="hyper-v-network-virtualization"></a>[Hyper-v ネットワーク仮想化](hyper-v-network-virtualization/Hyper-V-Network-Virtualization.md)

Hyper-v ネットワーク仮想化 (HNV) は、仮想ネットワークを使用して、物理ネットワークからアプリケーションとワークロードを抽象化するのに役立ちます。 仮想ネットワークでは、共有の物理ネットワーク ファブリックで実行されているときに、必要なマルチ テナント分離を提供し、リソースの使用率を高めることができます。 既存の投資を確実に転送できるように、既存のネットワーク歯車に仮想ネットワークを設定することができます。 また、仮想ネットワークは、仮想ローカルエリアネットワーク (Vlan) と互換性があります。

## <a name="hyper-v-virtual-switch"></a>[Hyper-V 仮想スイッチ](../../../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md)

Hyper-v 仮想スイッチは、hyper-v サーバーの役割をインストールした後に Hyper-v マネージャーで使用できる、ソフトウェアベースのレイヤー2イーサネットネットワークスイッチです。 このスイッチには、仮想マシンを仮想ネットワークと物理ネットワークの両方に接続するための、プログラムで管理される拡張可能な機能が含まれています。 また、Hyper-v 仮想スイッチでは、セキュリティ、分離、およびサービスレベルに対してポリシーが適用されます。

スイッチ埋め込みチーミング (SET) とリモートダイレクトメモリアクセス (RDMA) を使用して、Hyper-v 仮想スイッチを展開することもできます。 詳細については、このトピックの「[リモートダイレクトメモリアクセス (RDMA) とスイッチ埋め込みチーミング (SET)](#remote-direct-memory-access-rdma-and-switch-embedded-teaming-set) 」セクションを参照してください。

## <a name="internal-dns-service-idns-for-sdn"></a>[SDN の内部 DNS サービス (Idn)](Idns-for-Sdn.md)

ホストされている仮想マシン (Vm) とアプリケーションは、ネットワーク内およびインターネット上の外部リソースと通信するために DNS を必要とします。 Idn では、分離されたローカル名前空間とインターネットリソースの DNS 名前解決サービスをテナントに提供できます。

## <a name="network-function-virtualization"></a>[ネットワーク機能の仮想化](network-function-virtualization/Network-Function-Virtualization.md)

ロードバランサー、ファイアウォール、ルーター、スイッチなどのハードウェアアプライアンスは、ますます仮想アプライアンスになりつつあります。 Microsoft は、仮想化されたネットワーク、スイッチ、ゲートウェイ、Nat、ロードバランサー、およびファイアウォールを備えています。 この「ネットワーク機能の仮想化」は、サーバーの仮想化とネットワーク仮想化の自然な流れです。 仮想アプライアンスが急速に登場し、新しい市場が作成されます。 常に興味を引くと両方の仮想化プラットフォームで運動量を取得し、クラウド サービスです。

次のネットワーク機能の仮想化テクノロジを利用できます。

-   **ソフトウェア Load Balancer (SLB) とネットワークアドレス変換 (NAT)**。 Direct Server Return をサポートすることでスループットを向上させます。この場合、ネットワークトラフィックが返されると負荷分散マルチプレクサーがバイパスされる可能性があります。 詳細については、 [SDN のソフトウェア負荷分散/(SLB/) に](network-function-virtualization/software-load-balancing-for-sdn.md)関する説明を参照してください。

-   **データセンターのファイアウォール**。 詳細なアクセス制御リスト (Acl) を提供して、VM インターフェイスレベルまたはサブネットレベルでファイアウォールポリシーを適用できるようにします。 詳細については、「[データセンターファイアウォールの概要](network-function-virtualization/Datacenter-Firewall-Overview.md)」を参照してください。

-   **SDN の RAS ゲートウェイ**。 場所に関係なく、物理ネットワークと VM ネットワークリソースとの間でネットワークトラフィックをルーティングします。 ネットワークトラフィックは、同じ物理的な場所またはさまざまな場所でルーティングできます。 詳細については、「 [SDN の RAS ゲートウェイ](network-function-virtualization/RAS-Gateway-for-SDN.md)」を参照してください。

## <a name="remote-direct-memory-access-rdma-and-switch-embedded-teaming-set"></a>リモート ダイレクト メモリ アクセス (RDMA) とスイッチ埋め込みチーミング (SET)
Windows Server 2016 では、スイッチ埋め込みチーミング (SET) の有無にかかわらず、Hyper-v 仮想スイッチにバインドされているネットワークアダプターで RDMA を有効にすることができます。 これにより、RDMA を使用して同時に設定する場合に、使用するネットワークアダプターを少なくすることができます。

セットは、Hyper-v ホストと、ソフトウェアによるネットワーク制御 (SDN) スタックを Windows Server 2016 に含まれる環境で使用できる代替 NIC チーミング ソリューションです。 SET では、NIC チーミング機能の一部が Hyper-v 仮想スイッチに統合されます。

セットには、1 つまたは 8 物理イーサネット ネットワーク アダプター間で 1 つまたは複数のソフトウェア ベースの仮想ネットワーク アダプターにグループ化することができます。 これらの仮想ネットワーク アダプターでは、高速なパフォーマンスとネットワーク アダプターに障害が発生した場合のフォールト トレランスを提供します。
チームに配置する同じ物理的な HYPER-V ホスト上で、セットのメンバーのネットワーク アダプターをすべてにインストールする必要があります。

さらに、Windows PowerShell コマンドを使用して、データセンターブリッジング (DCB) を有効にしたり、RDMA 仮想 NIC (vNIC) を使用して Hyper-v 仮想スイッチを作成したり、セットと RDMA vNICs を使用して Hyper-v 仮想スイッチを作成したりすることもできます。 詳細については、「[リモートダイレクトメモリアクセス (RDMA) とスイッチ埋め込みチーミング (SET)](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming.md)」を参照してください。

## <a name="border-gateway-protocol-bgp"></a>[Border Gateway Protocol (BGP)](../../../remote/remote-access/bgp/Border-Gateway-Protocol-BGP.md)

Border Gateway Protocol (BGP) は、サイト間 VPN 接続を使用するサイト間のルートを自動的に学習する動的ルーティングプロトコルです。 そのため、BGP ではルーターの手動構成を減らすことができます。   RAS ゲートウェイを構成すると、BGP では、テナントの VM ネットワークとリモートサイト間のネットワークトラフィックのルーティングを管理できます。

## <a name="software-load-balancing-slb-for-sdn"></a>[SDN のソフトウェア負荷分散 (SLB)](network-function-virtualization/software-load-balancing-for-sdn.md)
SDN を展開するクラウドサービスプロバイダー (Csp) と企業は、ソフトウェア負荷分散 (SLB) を使用して、テナントとテナントの顧客ネットワークトラフィックを仮想ネットワークリソース間で均等に分散させることができます。 Windows Server SLB により、同じワークロードをホストする複数のサーバーであり、高可用性とスケーラビリティを提供することです。

## <a name="windows-server-containers"></a>[Windows Server コンテナー](Containers/Container-networking-overview.md)

Windows Server コンテナーは、同じコンテナーホストで実行されている他のサービスからアプリケーションまたはサービスを分離する、オペレーティングシステムの簡易仮想化の方法です。 各コンテナーには、独自のオペレーティングシステム、プロセス、ファイルシステム、レジストリ、および IP アドレスがあり、仮想ネットワークに接続できます。

## <a name="system-center"></a>System Center

[仮想マシン管理 (VMM)](https://docs.microsoft.com/system-center/vmm/)と[Operations Manager](https://docs.microsoft.com/system-center/scom/)で SDN インフラストラクチャを展開および管理します。 VMM では、仮想マシンとサービスを作成してプライベート クラウドにデプロイするために必要なリソースをプロビジョニングし、管理します。  Operations Manager では、問題を特定して早急に対応するために、お客様のエンタープライズ全体でサービス、デバイス、および操作を監視します。


---