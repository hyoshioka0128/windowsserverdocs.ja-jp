---
title: ネットワーク コントローラー
description: このトピックでは、Windows Server 2016 でネットワーク コント ローラーの概要を示します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 31f3fa4e-cd25-4bf3-89e9-a01a6cec7893
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7ace628c6ae9802c0c65d360aedfac8c80ac5537
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875683"
---
# <a name="network-controller"></a>ネットワーク コントローラー

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

新しいネットワーク コント ローラーは、Windows Server 2016 で、管理、構成、監視、およびデータ センター内の仮想および物理ネットワーク インフラストラクチャのトラブルシューティングを行う自動化の集中管理された、プログラミング可能なポイントを提供します。 

ネットワーク コントローラーを使用すると、ネットワーク インフラストラクチャの構成を自動化できます。ネットワーク デバイスとサービスを手動で構成する必要はありません。

> [!NOTE]
> このトピックに加え、次のネットワーク コント ローラーのドキュメントは使用できます。
> - [ネットワーク コント ローラーの高可用性](network-controller-high-availability.md)
> - [インストールとネットワーク コント ローラーを展開するための準備要件](../../plan/Installation-and-Preparation-Requirements-for-Deploying-Network-Controller.md)  
> - [Windows PowerShell を使用してネットワーク コント ローラーを展開します。](../../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)  
> - [サーバー マネージャーを使用して、ネットワーク コント ローラー サーバーの役割をインストールします。](Install-the-Network-Controller-server-role-using-Server-Manager.md)
> - [ネットワーク コント ローラーの展開後の手順](post-deploy-steps-nc.md)
> - [ネットワーク コント ローラーのコマンドレット](https://technet.microsoft.com/library/mt576401.aspx) 

## <a name="bkmk_overview"></a>ネットワーク コント ローラーの概要

ネットワーク コント ローラーは、高可用性と拡張性の高いサーバー ロール、および 1 つのアプリケーション プログラミング インターフェイスを提供します\(API\)ネットワークと通信するために、ネットワーク コント ローラーおよび 2 つ目の API をできるようにすることができますネットワーク コント ローラーと通信します。

ドメインと非ドメイン環境の両方のネットワーク コント ローラーを展開することができます。 ドメイン環境でネットワーク コント ローラーのユーザーとネットワーク デバイスを使用して認証 Kerberos です。非ドメイン環境では、認証に証明書を展開する必要があります。

>[!IMPORTANT]
>物理ホストでネットワーク コント ローラー サーバーの役割を展開しないでください。 ネットワーク コント ローラーを展開するには、HYPER-V 仮想マシンでネットワーク コント ローラー サーバーの役割をインストールする必要があります\(VM\) HYPER-V ホストにインストールされています。 次の 3 つの異なるハイパースレッディング上の Vm でネットワーク コント ローラーをインストールした後\-V のホスト、ハイパースレッディングが有効にする必要があります\-ソフトウェアによるネットワーク制御の V ホスト\(SDN\)ネットワーク コント ローラーを使用するホストを追加することでWindows PowerShell コマンド**新規 NetworkControllerServer**します。 これにより、関数には、SDN ソフトウェア ロード バランサーを有効にします。 詳細については、次を参照してください。[新規 NetworkControllerServer](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollerserver)します。

ネットワーク コントローラーは、Southbound API を使用してネットワーク デバイス、サービス、コンポーネントと通信します。 ネットワーク デバイスの検出、サービス構成の検出、ネットワークについて必要なすべての情報の収集に Southbound API を利用できます。 さらに、Southbound API を使用して、構成の変更などの情報をネットワーク インフラストラクチャに送信することもできます。

ネットワーク コントローラーの Northbound API を利用すると、ネットワーク コントローラーからネットワーク情報を収集し、その情報をネットワークの監視と構成に使用できます。

ネットワーク コント ローラーの Northbound API を使用すると、構成、監視、トラブルシューティング、および Windows PowerShell、Representational State Transfer を使用して、ネットワーク上の新しいデバイスをデプロイ\(REST\) API、または管理アプリケーショングラフィカル ユーザー インターフェイスでは、System Center Virtual Machine Manager など。

>[!NOTE]
>ネットワーク コントローラーの Northbound API は、REST インターフェイスとして実装されています。

ネットワーク コント ローラーで、データ センター ネットワークを管理するには、System Center Virtual Machine Manager などの管理アプリケーションを使用して\(SCVMM\)、および System Center Operations Manager \(SCOM\)、ネットワーク コント ローラーを構成することができます、ため、監視、プログラム、およびその制御下にあるネットワーク インフラストラクチャのトラブルシューティングを行います。

Windows PowerShell、REST API、または管理アプリケーションを使用することによって、ネットワーク コントローラーで次の物理および仮想ネットワーク インフラストラクチャを管理できます。

- Hyper-V VM と仮想スイッチ

- データ センターのファイアウォール

- リモート アクセス サービス\(RAS\)マルチ テナント ゲートウェイ、仮想ゲートウェイおよびゲートウェイ プール

- ソフトウェア ロード バランサー

次の図で、管理者は、ネットワーク コントローラーを直接操作できる管理ツールを使用しています。 ネットワーク コント ローラーは、管理ツールへの仮想および物理の両方のインフラストラクチャを含む、ネットワーク インフラストラクチャに関する情報を提供し、ツールを使用する場合、管理者のアクションに従って構成変更を加えます。  

![ネットワーク コント ローラーの概要](../../../media/Network-Controller/NetController_overview.png)  

HYPER-V 仮想マシンで、ネットワーク コント ローラー サーバーの役割を実行するには、テスト ラボ環境でネットワーク コント ローラーを展開する場合\(VM\) HYPER-V ホストにインストールされています。

大規模なデータ センターで高可用性のためには、3 つ以上の HYPER-V ホストにインストールされている 3 つの Vm を使用してクラスターを展開することができます。 詳細については、次を参照してください。[ネットワーク コント ローラーの高可用性](network-controller-high-availability.md)します。

## <a name="bkmk_features"></a>ネットワーク コント ローラーの機能

次のネットワーク コントローラーの機能を使用すると、仮想および物理ネットワーク デバイスとサービスの構成と管理を行うことができます。  
  
-   [ファイアウォールの管理](#bkmk_firewall)  
  
-   [ソフトウェア ロード バランサーの管理](#bkmk_slb)  
  
-   [仮想ネットワークの管理](#bkmk_virtual)  
  
-   [RAS ゲートウェイの管理](#bkmk_gateway)

>[!IMPORTANT]
>ネットワーク コント ローラーのバックアップと復元では、Windows Server 2016 で現在使用できません。
  
### <a name="bkmk_firewall"></a>ファイアウォールの管理

このネットワーク コントローラーの機能を使用すると、データセンターの East/West および North/South 両方のネットワーク トラフィックについて、ワークロード VM のファイアウォール アクセス制御の許可または拒否の規則を構成および管理できます。 ファイアウォール規則は、ワークロード VM の vSwitch ポートに組み込まれるので、データセンター内のワークロード全体に配布されます。 Northbound API を使用すると、ワークロード VM の送受信トラフィックのファイアウォール規則を定義できます。 また、規則で許可または拒否されたトラフィックをログに記録するように、各ファイアウォール規則を構成することもできます。  

詳細については、次を参照してください。 [データ センターのファイアウォールの概要](../../../sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)します。

### <a name="bkmk_slb"></a>ソフトウェア ロード バランサーの管理

このネットワーク コントローラーの機能を使用すると、複数のサーバーで同じワークロードをホストし、高可用性とスケーラビリティを実現することができます。  
  
詳細については、次を参照してください。 [ソフトウェアによる負荷分散と #40 です。SLB & #41 です。SDN の](../../../sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md)です。  
  
### <a name="bkmk_virtual"></a>仮想ネットワークの管理

このネットワーク コントローラーの機能を使用すると、Hyper-V 仮想スイッチ、個々の VM 上の仮想ネットワーク アダプターなど、Hyper-V のネットワーク仮想化の展開と構成を行うことができます。また、仮想ネットワーク ポリシーの格納と配布を行うこともできます。

ネットワーク コントローラーは、Network Virtualization Generic Routing Encapsulation (NVGRE) と Virtual Extensible Local Area Network (VXLAN) の両方をサポートしています。

### <a name="bkmk_gateway"></a>RAS ゲートウェイの管理

このネットワーク コント ローラーの機能を使用すると、デプロイ、構成、およびゲートウェイ サービスをテナントに提供する、RAS ゲートウェイ プールのメンバーである仮想マシン (Vm) を管理できます。 ネットワーク コント ローラーでは、次のゲートウェイの機能が RAS ゲートウェイを実行する Vm を自動的に展開することができます。

> [!NOTE]
> System Center Virtual Machine Manager で、RAS ゲートウェイには、Windows Server ゲートウェイはという名前です。

- クラスターのゲートウェイ VM を追加および削除し、必要なバックアップのレベルを指定します。

- IPsec を使用した、リモート テナント ネットワークとデータセンター間のサイト間仮想プライベート ネットワーク (VPN) ゲートウェイ接続。

- Generic Routing Encapsulation (GRE) を使用した、リモート テナント ネットワークとデータセンター間のサイト間 VPN ゲートウェイ接続。

- レイヤー 3 の転送機能。

- ボーダー ゲートウェイ プロトコル (BGP) ルーティングでは、そのリモート サイトとテナントの VM ネットワーク間のネットワーク トラフィックのルーティングを管理できます。

ネットワーク コント ローラーは、テナントのさまざまな接続を別のゲートウェイに配置できます。 1 つのパブリック IP を使用して、すべてのゲートウェイ接続または接続のサブセットに対して異なるパブリック ip できます。 ネットワーク コント ローラーのログすべてのゲートウェイの構成と状態の変更は、監査とトラブルシューティングのために使用できます。

BGP の詳細については、次を参照してください。 [ボーダー ゲートウェイ プロトコル (&) #40 です。BGP & #41;](../../../../remote/remote-access/bgp/Border-Gateway-Protocol-BGP.md)します。

RAS ゲートウェイの詳細については、次を参照してください。 [SDN の RAS ゲートウェイ](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)します。

## <a name="network-controller-deployment-options"></a>ネットワーク コント ローラーの展開オプション

System Center Virtual Machine Manager を使用してネットワーク コント ローラーを展開する\(VMM\)を参照してください[VMM ファブリックで SDN ネットワーク コント ローラー設定](https://technet.microsoft.com/system-center-docs/vmm/scenario/sdn-network-controller)します。

スクリプトを使用してネットワーク コント ローラーを展開するを参照してください。 [、ソフトウェア定義ネットワーク インフラストラクチャを使用してスクリプトをデプロイ](../../deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)します。

Windows PowerShell を使用してネットワーク コント ローラーを展開するを参照してください[展開ネットワーク コント ローラーが Windows PowerShell を使用します。](../../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)
