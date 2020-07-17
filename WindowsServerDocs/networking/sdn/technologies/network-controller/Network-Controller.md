---
title: ネットワーク コントローラー
description: このトピックでは、Windows Server 2016 のネットワークコントローラーの概要について説明します。
manager: grcusanz
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 31f3fa4e-cd25-4bf3-89e9-a01a6cec7893
ms.author: anpaul
author: AnirbanPaul
ms.openlocfilehash: f8221c92dc91d0c2e04df906ccd839a2c9895f94
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859665"
---
# <a name="network-controller"></a>ネットワーク コントローラー

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

新しいネットワーク コント ローラーは、Windows Server 2016 で、管理、構成、監視、およびデータ センター内の仮想および物理ネットワーク インフラストラクチャのトラブルシューティングを行う自動化の集中管理された、プログラミング可能なポイントを提供します。 

ネットワーク コントローラーを使用すると、ネットワーク インフラストラクチャの構成を自動化できます。ネットワーク デバイスとサービスを手動で構成する必要はありません。

> [!NOTE]
> このトピックに加え、次のネットワーク コント ローラーのドキュメントは使用できます。
> - [ネットワークコントローラーの高可用性](network-controller-high-availability.md)
> - [ネットワークコントローラーを展開するためのインストールおよび準備の要件](../../plan/Installation-and-Preparation-Requirements-for-Deploying-Network-Controller.md)  
> - [Windows PowerShell を使用してネットワーク コントローラーを展開する](../../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)  
> - [サーバー マネージャーを使用してネットワーク コントローラー サーバーの役割をインストールする](Install-the-Network-Controller-server-role-using-Server-Manager.md)
> - [ネットワークコントローラーの展開後の手順](post-deploy-steps-nc.md)
> - [ネットワークコントローラーのコマンドレット](https://technet.microsoft.com/library/mt576401.aspx) 

## <a name="network-controller-overview"></a><a name="bkmk_overview"></a>ネットワークコントローラーの概要

ネットワークコントローラーは、可用性が高くスケーラブルなサーバーの役割であり、1つのアプリケーションプログラミングインターフェイス \(API\) を提供して、ネットワークコントローラーがネットワークと通信できるようにします。また、ネットワークコントローラーとの通信を可能にする2つ目の API も用意されています。

ドメインと非ドメイン環境の両方のネットワーク コント ローラーを展開することができます。 ドメイン環境でネットワーク コント ローラーのユーザーとネットワーク デバイスを使用して認証 Kerberos です。非ドメイン環境では、認証に証明書を展開する必要があります。

>[!IMPORTANT]
>ネットワークコントローラーのサーバーの役割を物理ホストに展開しないでください。 ネットワークコントローラーを展開するには、hyper-v ホストにインストールされている VM\) \(Hyper-v 仮想マシンにネットワークコントローラーサーバーの役割をインストールする必要があります。 3つの異なる\-Hyper-v ホスト上の Vm にネットワークコントローラーをインストールした後、Windows PowerShell コマンド**NetworkControllerServer**を使用してネットワークコントローラーにホストを追加することで、ソフトウェアで定義されたネットワーク \(SDN\) 用のハイパー\-V ホストを有効にする必要があります。 これにより、SDN ソフトウェア ロード バランサーが機能するようになります。 詳細については、「 [NetworkControllerServer](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollerserver)」を参照してください。

ネットワーク コントローラーは、Southbound API を使用してネットワーク デバイス、サービス、コンポーネントと通信します。 ネットワーク デバイスの検出、サービス構成の検出、ネットワークについて必要なすべての情報の収集に Southbound API を利用できます。 さらに、Southbound API を使用して、構成の変更などの情報をネットワーク インフラストラクチャに送信することもできます。

ネットワーク コントローラーの Northbound API を利用すると、ネットワーク コントローラーからネットワーク情報を収集し、その情報をネットワークの監視と構成に使用できます。

Network Controller Northbound API を使用すると、ネットワーク上の新しいデバイスの構成、監視、トラブルシューティング、および展開を行うことができます。これには、Windows PowerShell、REST\) API \(REST の状態転送、System Center Virtual Machine Manager などのグラフィカルユーザーインターフェイスを備えた管理アプリケーションを使用します。

>[!NOTE]
>ネットワーク コントローラーの Northbound API は、REST インターフェイスとして実装されています。

ネットワークコントローラーを使用してデータセンターネットワークを管理するには、System Center Virtual Machine Manager \(SCVMM\)などの管理アプリケーションを使用します。 \(System Center Operations Manager また、ネットワークコントローラーでは、管理下にあるネットワークインフラストラクチャの構成、監視、プログラム、およびトラブルシューティングを行うことができます。\)

Windows PowerShell、REST API、または管理アプリケーションを使用することによって、ネットワーク コントローラーで次の物理および仮想ネットワーク インフラストラクチャを管理できます。

- Hyper-V VM と仮想スイッチ

- データ センターのファイアウォール

- リモートアクセスサービス \(RAS\) マルチテナントゲートウェイ、仮想ゲートウェイ、ゲートウェイプール

- ソフトウェアロードバランサー

次の図で、管理者は、ネットワーク コントローラーを直接操作できる管理ツールを使用しています。 ネットワーク コント ローラーは、管理ツールへの仮想および物理の両方のインフラストラクチャを含む、ネットワーク インフラストラクチャに関する情報を提供し、ツールを使用する場合、管理者のアクションに従って構成変更を加えます。  

![ネットワーク コント ローラーの概要](../../../media/Network-Controller/NetController_overview.png)  

テストラボ環境にネットワークコントローラーを展開する場合は、hyper-v ホストにインストールされている VM\) \(Hyper-v 仮想マシンでネットワークコントローラーサーバーの役割を実行できます。

大規模なデータセンターで高可用性を実現するために、3つ以上の Hyper-v ホストにインストールされた3つの Vm を使用してクラスターを展開できます。 詳細については、「[ネットワークコントローラーの高可用性](network-controller-high-availability.md)」を参照してください。

## <a name="network-controller-features"></a><a name="bkmk_features"></a>ネットワークコントローラーの機能

次のネットワーク コントローラーの機能を使用すると、仮想および物理ネットワーク デバイスとサービスの構成と管理を行うことができます。  
  
-   [ファイアウォールの管理](#bkmk_firewall)  
  
-   [ソフトウェアの Load Balancer 管理](#bkmk_slb)  
  
-   [Virtual Network 管理](#bkmk_virtual)  
  
-   [RAS ゲートウェイの管理](#bkmk_gateway)

>[!IMPORTANT]
>ネットワーク コント ローラーのバックアップと復元では、Windows Server 2016 で現在使用できません。
  
### <a name="firewall-management"></a><a name="bkmk_firewall"></a>ファイアウォールの管理

このネットワーク コントローラーの機能を使用すると、データセンターの East/West および North/South 両方のネットワーク トラフィックについて、ワークロード VM のファイアウォール アクセス制御の許可または拒否の規則を構成および管理できます。 ファイアウォール規則は、ワークロード VM の vSwitch ポートに組み込まれるので、データセンター内のワークロード全体に配布されます。 Northbound API を使用すると、ワークロード VM の送受信トラフィックのファイアウォール規則を定義できます。 また、規則で許可または拒否されたトラフィックをログに記録するように、各ファイアウォール規則を構成することもできます。  

詳細については、次を参照してください。 [データ センターのファイアウォールの概要](../../../sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)します。

### <a name="software-load-balancer-management"></a><a name="bkmk_slb"></a>ソフトウェアの Load Balancer 管理

このネットワーク コントローラーの機能を使用すると、複数のサーバーで同じワークロードをホストし、高可用性とスケーラビリティを実現することができます。  
  
詳細については、次を参照してください。 [ソフトウェアによる負荷分散と #40 です。SLB & #41 です。SDN の](../../../sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md)です。  
  
### <a name="virtual-network-management"></a><a name="bkmk_virtual"></a>Virtual Network 管理

このネットワーク コントローラーの機能を使用すると、Hyper-V 仮想スイッチ、個々の VM 上の仮想ネットワーク アダプターなど、Hyper-V のネットワーク仮想化の展開と構成を行うことができます。また、仮想ネットワーク ポリシーの格納と配布を行うこともできます。

ネットワーク コントローラーは、Network Virtualization Generic Routing Encapsulation (NVGRE) と Virtual Extensible Local Area Network (VXLAN) の両方をサポートしています。

### <a name="ras-gateway-management"></a><a name="bkmk_gateway"></a>RAS ゲートウェイの管理

このネットワークコントローラーの機能を使用すると、ゲートウェイサービスをテナントに提供する、RAS ゲートウェイプールのメンバーである仮想マシン (Vm) を展開、構成、および管理することができます。 ネットワーク コント ローラーでは、次のゲートウェイの機能が RAS ゲートウェイを実行する Vm を自動的に展開することができます。

> [!NOTE]
> System Center Virtual Machine Manager で、RAS ゲートウェイには、Windows Server ゲートウェイはという名前です。

- クラスターのゲートウェイ VM を追加および削除し、必要なバックアップのレベルを指定します。

- IPsec を使用した、リモート テナント ネットワークとデータセンター間のサイト間仮想プライベート ネットワーク (VPN) ゲートウェイ接続。

- Generic Routing Encapsulation (GRE) を使用した、リモート テナント ネットワークとデータセンター間のサイト間 VPN ゲートウェイ接続。

- レイヤー 3 の転送機能。

- ボーダー ゲートウェイ プロトコル (BGP) ルーティングでは、そのリモート サイトとテナントの VM ネットワーク間のネットワーク トラフィックのルーティングを管理できます。

ネットワークコントローラーは、テナントの別の接続を別々のゲートウェイに配置できます。 すべてのゲートウェイ接続に対して1つのパブリック IP を使用することも、接続のサブセットに対して異なるパブリック IP を使用することもできます。 ネットワークコントローラーは、すべてのゲートウェイの構成と状態の変更をログに記録します。これは、監査とトラブルシューティングの目的で使用できます。

BGP の詳細については、次を参照してください。 [ボーダー ゲートウェイ プロトコル (&) #40 です。BGP & #41;](../../../../remote/remote-access/bgp/Border-Gateway-Protocol-BGP.md)します。

RAS ゲートウェイの詳細については、次を参照してください。 [SDN の RAS ゲートウェイ](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)します。

## <a name="network-controller-deployment-options"></a>ネットワークコントローラーの展開オプション

System Center Virtual Machine Manager \(VMM\)を使用してネットワークコントローラーを展開するには、「 [vmm ファブリックでの SDN ネットワークコントローラーのセットアップ](https://technet.microsoft.com/system-center-docs/vmm/scenario/sdn-network-controller)」を参照してください。

スクリプトを使用してネットワークコントローラーを展開する方法については、「[スクリプトを使用したソフトウェア定義ネットワークインフラストラクチャの展開](../../deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)」を参照してください。

Windows PowerShell を使用してネットワークコントローラーを展開するには、「 [Windows powershell を使用したネットワークコントローラーの展開](../../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)」を参照してください。
