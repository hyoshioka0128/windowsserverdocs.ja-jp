---
title: ソフトウェア定義ネットワーク (SDN)
description: このトピックを使用すると、Windows Server、System Center、および Microsoft Azure に用意されているソフトウェアによるネットワーク制御 (SDN) テクノロジについて説明します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 9a1ea73c-20cd-42c5-95ad-b003b9cc6d64
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 33351ccfa1466f667ef9351768c89b373734075d
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="software-defined-networking-sdn"></a>ソフトウェア定義ネットワーク (SDN)

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、Windows Server Datacenter edition、System Center 2016、および Microsoft Azure に用意されているソフトウェアによるネットワーク制御 (SDN) テクノロジについて説明します。  
  
> [!NOTE]
> このトピックに加え、次の SDN コンテンツは使用できます。
> 
> - [Windows Server の SDN の新機能](sdn-whats-new.md)
> - [Introduction to SDN in Windows Server Datacenter](sdn-intro.md)
> - [SDN Technologies](technologies/Software-Defined-Networking-Technologies.md)  
> - [Plan SDN](plan/Plan-Software-Defined-Networking.md) 
> - [Deploy SDN](deploy/Deploy-Software-Defined-Networking.md)  
> - [Manage SDN](manage/manage-sdn.md)
> - [Security for SDN](security/sdn-security-top.md)
> - [Troubleshoot SDN](troubleshoot/Troubleshoot-Software-Defined-Networking.md)
> - [System Center Technologies for SDN](Sc-Tech-for-Sdn.md)
> - [Microsoft Azure and SDN](Azure_and_Sdn.md)
> - [データ センターとクラウド ネットワーク チームにお問い合わせください。](contact-sdn-team.md)
  
## <a name="bkmk_sdn"></a>ソフトウェア定義ネットワークの概要

ソフトウェア定義ネットワーク \(SDN\) 一元的に構成して、ルーター、スイッチ、およびデータ センター内のゲートウェイなどの物理および仮想ネットワーク デバイスを管理する方法を説明します。 Hyper-V 仮想スイッチにより、Hyper-V ネットワーク仮想化および RAS ゲートウェイなどの仮想ネットワーク要素は不可欠な要素、SDN インフラストラクチャの設計されています。

>[!NOTE]
>Hyper-V ホストと SDN インフラストラクチャ サーバー、ネットワーク コントローラーとソフトウェアの負荷分散のノードなどを実行している仮想マシン \(VMs\) のためには、Windows Server 2016 Datacenter edition をインストールする必要があります。 のみテナント ワークロード SDN\ 制御のネットワークに接続されている Vm が含まれている Hyper-V ホスト、Windows Server 2016 Standard edition を実行することができます。

既存の物理スイッチ、ルーター、およびその他のハードウェア デバイスを引き続き使用できますが、これらのデバイスがソフトウェア定義ネットワークとの互換性のために設計された場合、仮想ネットワークと物理ネットワークの間により緊密な統合を実現できます。  
  
SDN は、ので、ネットワーク プレーンの管理、制御、およびデータ プレーン - は、ネットワーク デバイス自体に不要になったバインドされますが、System Center 2016 のようなデータ センター管理ソフトウェアなど、他のエンティティとして使用する抽象化されている可能性があります。  
  
SDN には、動的に、アプリケーションやワークロードの要件に対応する自動で一元的な方法を提供するデータ センター ネットワークを管理することができます。 ソフトウェア定義ネットワークは、次の機能を提供します。  
  
-   アプリケーションとワークロードをネットワークを仮想化によって達成が基になる物理ネットワークから抽象化する機能。 Hyper-V を使用してサーバー仮想化と同様に、抽象化は、一貫性のある作業、アプリケーションやワークロードを停止方法でです。 たとえば、ソフトウェア定義ネットワークは、IP アドレス、スイッチ、およびロード バランサーなど、物理ネットワーク要素の仮想抽象化を提供します。  
  
-   これら 2 種類のネットワーク間のトラフィック フローをなど、物理および仮想の両方のネットワークの管理制御ポリシーおよびを一元的に定義する機能。  
  
-   新しいワークロードを展開するか、または仮想または物理ネットワーク間でワークロードを移動しても、規模で一貫性のある方法でネットワーク ポリシーを実装する機能。  
  
## <a name="bkmk_ws"></a>Windows Server のテクノロジのソフトウェア定義ネットワーク  
Windows Server には、次のソフトウェア定義ネットワーク テクノロジが含まれています。  

### <a name="bkmk_nc"></a>ネットワーク コントローラー

新しいネットワーク コントローラーは、Windows Server 2016 での管理、構成、監視、および仮想の両方のトラブルシューティングを行う自動化およびデータ センター内の物理ネットワーク インフラストラクチャの集中管理された、プログラミング可能なポイントを提供します。 ネットワーク コントローラーを使用して、ネットワーク デバイスとサービスを手動で構成を実行するのではなく、ネットワーク インフラストラクチャの構成を自動化することができます。  
  
ネットワーク コントローラーは、高可用性と拡張性のサーバーの役割であり、1 つのアプリケーション プログラミング インターフェイス (API)、Southbound API - ネットワークと通信するためにネットワーク コントローラーを許可して、2 番目の API、Northbound API - ネットワーク コントローラーと通信することができますを提供します。  
  
Windows PowerShell、Representational State Transfer (REST) API、または管理アプリケーションを使用して、ネットワーク コントローラーを使用して、次の物理および仮想ネットワーク インフラストラクチャを管理します。  
  
-   Hyper-V Vm と仮想スイッチ  
  
-   物理ネットワーク スイッチ  
  
-   物理ネットワーク ルーター  
  
-   ファイアウォール ソフトウェア  
  
-   リモート アクセス サービス (RAS) マルチテナント ゲートウェイを含む、VPN ゲートウェイ  
  
-   ロード バランサー  
  
詳細については、次を参照してください。[ネットワーク コントローラー](../sdn/technologies/network-controller/Network-Controller.md)します。  
  
### <a name="bkmk_hv"></a>Hyper-V ネットワーク仮想化

Hyper-V ネットワーク仮想化では、仮想ネットワークを使用して、アプリケーションや、物理ネットワークからワークロードを抽象化するのに役立ちます。 仮想ネットワークは、リソース使用率を高めるため、共有の物理ネットワーク ファブリックで実行中に必要なマルチテナントの分離を提供します。 実行する転送、既存の投資をようにには、既存のネットワーク装置上の仮想ネットワークを設定することができます。 さらに、仮想ネットワークは仮想ローカル エリア ネットワーク (Vlan) との互換性です。  
  
詳細については、次を参照してください。[Hyper-v ネットワーク仮想化](../sdn/technologies/hyper-v-network-virtualization/Hyper-V-Network-Virtualization.md)します。  
  
### <a name="bkmk_switch"></a>Hyper-V 仮想スイッチ

Hyper-V 仮想スイッチは、ソフトウェア ベースのレイヤー 2 イーサネット ネットワーク スイッチ、Hyper-V サーバーの役割をインストールした後に Hyper-V マネージャーで利用できます。 スイッチには、バーチャル マシンに接続する仮想ネットワークと物理ネットワークの両方のプログラムで管理し、拡張機能が含まれています。 さらに、Hyper-V 仮想スイッチは、セキュリティ、分離、およびサービス レベルでポリシーの施行を提供します。  
  
Windows Server 2016 で Hyper-V 仮想スイッチでは、スイッチ埋め込みチーミング (SET) とリモート ダイレクト メモリ アクセス (RDMA) を展開することができます。 詳細については、セクションを参照して[リモート ダイレクト メモリ アクセス (RDMA) とスイッチ埋め込みチーミング (SET)](#bkmk_rdma)このトピックの「します。  
  
Hyper-V 仮想スイッチの詳細については、次を参照してください。[Hyper-v 仮想スイッチ](../../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md)します。

### <a name="bkmk_idns"></a>内部の DNS サービスと #40; Idn & #41 です。

仮想マシンをホスト型 \(VMs\) とアプリケーションは独自のネットワーク内およびインターネット上の外部のリソースと通信するために DNS が必要です。 Idn を提供できますテナント DNS 名前解決サービスでは、ローカルの分離された名前空間とインターネット リソース。

詳細については、次を参照してください。[Internal DNS Service (&) #40; Idn & #41 です。SDN の](technologies/Idns-for-Sdn.md)します。
  
### <a name="bkmk_nfv"></a>ネットワーク関数仮想化

今日のソフトウェアで定義されているデータ センター、(ロード バランサー、ファイアウォール、ルーター、スイッチ、およびなど) などのハードウェア アプライアンスで実行されているネットワーク機能がますますされている仮想化仮想アプライアンスとして。 この「ネットワーク関数仮想化」は、サーバー仮想化とネットワーク仮想化の自然な流れです。 仮想アプライアンスはすばやく顕在化しつつ、新しい市場を作成します。 興味を引くと両方の仮想化プラットフォームで運動量を取得し、クラウド サービスを続行します。  
  
次のネットワーク機能の仮想化テクノロジを利用できます。  
  
-   **ソフトウェア ロード バランサー (SLB) とネットワーク アドレス変換 (NAT)**します。 東西部と北南レイヤー 4 のロード バランサーと、NAT がサポートすることで Direct Server Return 戻り値のネットワーク トラフィックが、負荷分散マルチプレクサーをバイパスできますスループットを向上します。 詳細については、次を参照してください。[ソフトウェア負荷分散 (SLB) SDN の](technologies/network-function-virtualization/software-load-balancing-for-sdn.md)します。  
  
-   **データ センターのファイアウォール**します。 この分散型のファイアウォールは、VM のインターフェイスのレベル、またはサブネット レベルでのファイアウォール ポリシーを適用できるように細かくアクセス制御リスト (Acl) を提供します。  
  
    詳細については、次を参照してください。[データ センターのファイアウォールの概要](../sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)します。  
  
-   **RAS ゲートウェイ**します。 仮想ネットワークと仮想化されていないネットワーク間のトラフィックのブリッジのゲートウェイを使用することができます。具体的には、サイト間 VPN ゲートウェイを展開する、転送ゲートウェイ、および汎用ルーティング カプセル化 (GRE) ゲートウェイ。 さらに、M と N の冗長性のゲートウェイをサポートします。 詳細については、次を参照してください。[SDN の RAS ゲートウェイ](technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)します。
  
詳細については、次を参照してください。[ネットワーク関数仮想化](technologies/network-function-virtualization/Network-Function-Virtualization.md)します。  
  
### <a name="bkmk_rdma"></a>リモート ダイレクト メモリ アクセス (RDMA) とスイッチ埋め込みチーミング (SET)  
Windows Server 2016 ではなくスイッチ埋め込みチーミング (SET) または Hyper-V 仮想スイッチにバインドされているネットワーク アダプターで RDMA を有効にできます。 これにより、RDMA とセットを使用するときに、以下のネットワーク アダプターを使用する、同時にします。  
  
セットは、Hyper-v ホストと、ソフトウェアによるネットワーク制御 (SDN) スタックを Windows Server 2016 に含まれる環境で使用できる代替 NIC チーミング ソリューションです。 セットは、NIC チーミング機能の一部を Hyper-V 仮想スイッチに統合します。  
  
セットでは、1 つまたは 8 物理イーサネット ネットワーク アダプターに 1 つまたは複数のソフトウェア ベースの仮想ネットワーク アダプター間でグループ化することができます。 これらの仮想ネットワーク アダプターは、高速なパフォーマンスとネットワーク アダプターに障害が発生した場合のフォールト トレランスを提供します。  
チームに配置する同じ物理的な Hyper-V ホスト上で、セット メンバーのネットワーク アダプターをすべてにインストールする必要があります。  
  
さらに、データ センター ブリッジング (DCB) を有効にし、RDMA 仮想 NIC (vNIC) で Hyper-V 仮想スイッチを作成し、SET と RDMA Vnic で Hyper-V 仮想スイッチを作成する Windows PowerShell コマンドを使用することができます。  
  
詳細については、次を参照してください。[リモート ダイレクト メモリ アクセス (RDMA) とスイッチ埋め込みチーミング (SET)](https://technet.microsoft.com/library/mt403349.aspx)します。  
  
### <a name="bkmk_rras"></a>SDN の RAS ゲートウェイ  
RAS ゲートウェイは、ソフトウェア ベース、マルチテナント、ボーダー ゲートウェイ プロトコル (BGP) 対応ルーターはクラウド サービス プロバイダー (CSP) や Hyper-V ネットワーク仮想化を使用して複数のテナント仮想ネットワークをホストしているエンタープライズ向けに設計された Windows Server 2016 でです。  
  
RAS ゲートウェイは、ゲートウェイ プール、M と N の冗長性、複数の種類のサイト間 VPN 接続、およびゲートウェイ インフラストラクチャの柔軟な設計の選択肢を提供するために BGP ルート Reflector を提供します。  
  
詳細については、次を参照してください[SDN の RAS ゲートウェイ。](technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)  
  
### <a name="bkmk_slb"></a>ソフトウェアの負荷分散 (SLB)  
クラウド サービス プロバイダー (CSP) および展開する企業はソフトウェアによるネットワーク制御 (SDN) Windows Server 2016 では、テナントおよびテナント仮想ネットワークのリソース間でのカスタマー ネットワーク トラフィックを均等に分散するのにソフトウェア負荷分散 (SLB) を使用できます。 Windows Server SLB 有効、同じワークロードをホストする複数のサーバーに高可用性とスケーラビリティを提供します。  
  
詳細については、次を参照してください。[ソフトウェアの負荷分散と #40 です。SLB & #41 です。SDN の](../sdn/technologies/network-function-virtualization/software-load-balancing-for-sdn.md)します。

### <a name="windows-server-containers"></a>Windows Server のコンテナー

Windows Server コンテナーは、軽量のオペレーティング システム仮想化の方法が、同じコンテナー ホストで実行されているその他のサービスからのアプリケーションまたはサービスを分離するために使用します。 これを有効にするのには、それぞれのコンテナーは、オペレーティング システム、プロセス、ファイル システム、レジストリ、および IP アドレスの独自のビューがします。 Windows Server 2016 では、仮想ネットワークへの Windows Server コンテナーを接続できます。 詳細については、次を参照してください。[Windows Server のコンテナー](technologies/containers/Container-networking-overview.md)します。

### <a name="contact-the-datacenter-and-cloud-networking-product-team"></a>データ センターとクラウド ネットワークの製品チームにお問い合わせください。

関心のある Microsoft やその他の SDN 顧客 SDN テクノロジについて説明するがあるかのさまざまな方法を行うのために連絡します。

詳細については、次を参照してください。[データ センターとクラウド ネットワーク チームにお問い合わせください](contact-sdn-team.md)します。
