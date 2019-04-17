---
title: ネットワーク コントローラー
description: このトピックでは、Windows Server 2016 のネットワーク コントローラーの概要を説明します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 31f3fa4e-cd25-4bf3-89e9-a01a6cec7893
ms.author: pashort
author: shortpatti
ms.openlocfilehash: acb9abbd716e9930fb01431e7004abb72a7da10c
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="network-controller"></a>ネットワーク コントローラー

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

新しいネットワーク コントローラーは、Windows Server 2016 での管理、構成、監視、およびデータ センター内の仮想および物理ネットワーク インフラストラクチャのトラブルシューティングを行う自動化の集中管理された、プログラミング可能なポイントを提供します。 

ネットワーク コントローラーを使用して、ネットワーク デバイスとサービスを手動で構成を実行するのではなく、ネットワーク インフラストラクチャの構成を自動化することができます。

> [!NOTE]
> このトピックに加え、次のネットワーク コントローラーのドキュメントは使用できます。
> - [ネットワーク コントローラーの高可用性](network-controller-high-availability.md)
> - [インストールとネットワーク コントローラーを展開するための準備の要件](../../plan/Installation-and-Preparation-Requirements-for-Deploying-Network-Controller.md)  
> - [Windows PowerShell を使用してネットワーク コントローラーを展開します。](../../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)  
> - [サーバー マネージャーを使用して、ネットワーク コントローラー サーバーの役割をインストールします。](Install-the-Network-Controller-server-role-using-Server-Manager.md)
> - [後の Post-Deploymentネットワーク コントローラーの手順を実行します。](post-deploy-steps-nc.md)
> - [ネットワーク コントローラーのコマンドレット](https://technet.microsoft.com/library/mt576401.aspx) 

## <a name="bkmk_overview"></a>ネットワーク コントローラーの概要

ネットワーク コントローラーは、高可用性と拡張性のサーバーの役割であり、提供 1 つのアプリケーション プログラミング インターフェイスでは、ネットワークと通信するためにネットワーク コントローラー \(API\) と 2 番目の API ネットワーク コントローラーと通信することができます。

ドメインと非ドメイン環境の両方のネットワーク コントローラーを展開することができます。 ドメイン環境でネットワーク コントローラーがユーザーとネットワーク デバイスを使用して認証 Kerberos です。非ドメイン環境では、認証に証明書を展開する必要があります。

>[!IMPORTANT]
>物理ホスト上で、ネットワーク コントローラー サーバーの役割を展開しないでください。 ネットワーク コントローラーを展開するには、Hyper-V 仮想マシンのネットワーク コントローラー サーバーの役割をインストールする必要があります \(VM\) Hyper-V ホストにインストールされています。 Windows PowerShell コマンドを使用してネットワーク コントローラーにホストを追加することでのソフトウェアがネットワーク定義 \(SDN\) Hyper\ V ホストを有効にする必要があります Vm 上で次の 3 つの異なる Hyper\ V ホストでネットワーク コントローラーをインストールした後**新規 NetworkControllerServer**します。 これにより、有効にすると、SDN ソフトウェア ロード バランサーが機能します。 詳細については、次を参照してください。[新規 NetworkControllerServer](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollerserver)します。

ネットワーク コントローラーは、Southbound API を使用して、ネットワーク デバイス、サービス、およびコンポーネントと通信します。 Southbound api をネットワーク コントローラーできますネットワーク デバイスの検出、サービスの構成を検出およびすべてのネットワークについて必要な情報を収集します。 さらに、Southbound API を使用ネットワーク コントローラーに対して行った構成の変更など、ネットワーク インフラストラクチャに情報を送信します。

ネットワーク コントローラーの Northbound API は、ネットワーク コントローラーからネットワーク情報を収集し、それを監視し、ネットワークの構成を使用する機能を提供します。

ネットワーク コントローラーの Northbound API を使用すると、構成、監視、トラブルシューティング、およびグラフィカル ユーザー インターフェイス、System Center Virtual Machine Manager などの Windows PowerShell、Representational 状態転送 \(REST\) API、または管理アプリケーションを使用して、ネットワーク上の新しいデバイスを展開できます。

>[!NOTE]
>ネットワーク コントローラーの Northbound API は、REST インターフェイスとして実装されます。

ネットワーク コントローラーを使用すると、構成、監視、プログラム、およびその管理下にあるネットワーク インフラストラクチャのトラブルシューティングを行うために、System Center Virtual Machine Manager \(SCVMM\)、および System Center Operations Manager \(SCOM\) などの管理アプリケーションを使用してネットワーク コントローラーと、データ センター ネットワークを管理できます。

Windows PowerShell、REST API、または管理アプリケーションを使用して、ネットワーク コントローラーを使用して、次の物理および仮想ネットワーク インフラストラクチャを管理します。

- Hyper-V Vm と仮想スイッチ

- データ センターのファイアウォール

- リモート アクセス サービス \(RAS\) マルチテナント ゲートウェイ、仮想ゲートウェイおよびゲートウェイ プール

- ソフトウェア ロード バランサー

次の図では、管理者は、ネットワーク コントローラーと直接対話する管理ツールを使用します。 ネットワーク コントローラーは、仮想と物理インフラストラクチャの両方が管理ツールを含む、ネットワーク インフラストラクチャに関する情報を提供し、ツールを使用する場合、管理者の操作に従って構成の変更を行います。  

![ネットワーク コントローラーの概要](../../../media/Network-Controller/NetController_overview.png)  

Hyper-V 仮想マシンで、ネットワーク コントローラー サーバーの役割を実行するには、テスト ラボ環境でネットワーク コントローラーを展開している場合、Hyper-v ホストにインストールされている \(VM\) します。

大規模なデータ センターで高可用性の 3 つ以上の Hyper-V ホストにインストールされている 3 つの Vm を使用してクラスターを展開することができます。 詳細については、次を参照してください。[ネットワーク コントローラーの高可用性](network-controller-high-availability.md)します。

## <a name="bkmk_features"></a>ネットワーク コントローラーの機能

次のネットワーク コントローラーの機能を構成および管理仮想および物理ネットワーク デバイスとサービスを許可します。  
  
-   [ファイアウォール管理](#bkmk_firewall)  
  
-   [ソフトウェア ロード バランサー管理](#bkmk_slb)  
  
-   [仮想ネットワークの管理](#bkmk_virtual)  
  
-   [RAS ゲートウェイの管理](#bkmk_gateway)

>[!IMPORTANT]
>ネットワーク コントローラーのバックアップと復元では、Windows Server 2016 で現在利用できません。
  
### <a name="bkmk_firewall"></a>ファイアウォール管理

このネットワーク コントローラーの機能を構成し、ワークロード Vm のファイアウォール アクセス制御規則を許可または拒否の East/west および North/south のネットワーク トラフィック、データ センター内の両方を管理できます。 ファイアウォール規則、ワークロード Vm の vSwitch ポートに組み込まれると、データ センター内のワークロード全体配布されるようにします。 Northbound API を使用すると、ワークロード VM の受信と送信の両方のトラフィックのファイアウォール規則を定義できます。 トラフィックがで許可または拒否規則をログに記録するには、各ファイアウォール規則を構成することもできます。  

詳細については、次を参照してください。[データ センターのファイアウォールの概要](../../../sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)します。

### <a name="bkmk_slb"></a>ソフトウェア ロード バランサー管理

このネットワーク コントローラーの機能では、高可用性とスケーラビリティを提供する、同じワークロードをホストする複数のサーバーを有効にすることができます。  
  
詳細については、次を参照してください。[ソフトウェアの負荷分散と #40 です。SLB & #41 です。SDN の](../../../sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md)します。  
  
### <a name="bkmk_virtual"></a>仮想ネットワークの管理

このネットワーク コントローラーの機能を展開して、Hyper-V 仮想スイッチと、個々 の Vm 上の仮想ネットワーク アダプターを含む、Hyper-V ネットワーク仮想化を構成して保存し、仮想ネットワーク ポリシーを配布できます。

ネットワーク コントローラーは、ネットワーク仮想化汎用ルーティング カプセル化 (NVGRE) と仮想拡張可能なローカル エリア ネットワーク (VXLAN) の両方をサポートします。

### <a name="bkmk_gateway"></a>RAS ゲートウェイの管理

このネットワーク コントローラーの機能を使用すると、展開、構成、およびテナントにゲートウェイ サービスを提供する、RAS ゲートウェイ プールのメンバーである仮想マシン (Vm) を管理できます。 ネットワーク コントローラーでは、次のゲートウェイ機能が RAS ゲートウェイを実行する Vm を自動的に展開することができます。

> [!NOTE]
> System Center Virtual Machine Manager で、RAS ゲートウェイは、Windows Server ゲートウェイをいいます。

- 追加し、ゲートウェイ Vm をクラスターから削除し、必要なバックアップのレベルを指定します。

- リモート テナント ネットワークと IPsec を使用して、データ センター間のサイト間仮想プライベート ネットワーク (VPN) ゲートウェイ接続。

- リモート テナント ネットワークと汎用ルーティング カプセル化 (GRE) を使用して、データ センター間でサイト間 VPN ゲートウェイ接続。

- レイヤー 3 の転送機能の。

- ボーダー ゲートウェイ プロトコル (BGP) ルーティング、テナントの VM ネットワークとそのリモート サイト間のネットワーク トラフィックのルーティングを管理できます。

ネットワーク コントローラーは、異なるゲートウェイ上のテナント別の接続を配置できます。 1 つのパブリック IP を使用して、すべてのゲートウェイ接続またはサブセットの接続のパブリック ip を異なるできます。 ネットワーク コントローラーのログのすべてのゲートウェイの構成と状態の変化は、監査とトラブルシューティングのために使用できます。

BGP の詳細については、次を参照してください。[ボーダー ゲートウェイ プロトコル (&) #40 です。BGP & #41 です。](../../../../remote/remote-access/bgp/Border-Gateway-Protocol-BGP.md).

RAS ゲートウェイの詳細については、次を参照してください。[SDN の RAS ゲートウェイ](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)します。

## <a name="network-controller-deployment-options"></a>ネットワーク コントローラーの展開オプション

System Center Virtual Machine Manager \(VMM\) を使用してネットワーク コントローラーを展開するを参照してください。[VMM ファブリックにおける、SDN ネットワーク コントローラーをセットアップ](https://technet.microsoft.com/system-center-docs/vmm/scenario/sdn-network-controller)します。

スクリプトを使用してネットワーク コントローラーを展開するを参照してください。[、ソフトウェア定義ネットワーク インフラストラクチャを使用してスクリプトを展開](../../deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)します。

Windows PowerShell を使用してネットワーク コントローラーを展開するを参照してください[展開ネットワーク コントローラーが Windows PowerShell を使用します。。](../../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)
