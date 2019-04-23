---
title: Windows Server 2016 の GRE トンネリング
description: このトピックでは、Windows Server 2016 で RAS ゲートウェイの Generic Routing Encapsulation (GRE) トンネル機能への更新の理解を使用できます。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: df2023bf-ba64-481e-b222-6f709edaa5c1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e0ec077ad5e97edd3db7d1dc4e662bb191f7885b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887863"
---
# <a name="gre-tunneling-in-windows-server-2016"></a>Windows Server 2016 の GRE トンネリング

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

Windows Server 2016 では、更新プログラムを提供する Generic Routing Encapsulation \(GRE\) RAS ゲートウェイの機能をトンネリングします。  
  
GRE は軽量のトンネリング プロトコルで、インターネット プロトコル インターネットワークを介して Point-to-Point 仮想リンク内のさまざまなネットワーク レイヤー プロトコルをカプセル化できます。 Microsoft GRE 実装は、IPv4 と IPv6 にカプセル化できます。  
  
GRE トンネルは多くのシナリオに便利なためです。  
  
-   これらは軽量と RFC 2890 準拠している、さまざまなベンダーのデバイスと相互運用可能なので  
  
-   ボーダー ゲートウェイ プロトコルを使用する\(BGP\)動的ルーティング用  
  
-   使用するための GRE マルチ テナント RAS ゲートウェイを構成するにはソフトウェア定義ネットワークを使った\(SDN\)
  
-   System Center Virtual Machine Manager を使用して、GRE を管理する\-ベースの RAS ゲートウェイ
  
-   GRE RAS ゲートウェイとして構成されている 6 コアの仮想マシンで最大 2.0 Gbps のスループットを実現できます。
  
-   1 つのゲートウェイは、複数の接続モードをサポートしています。  
  
GRE ベースのトンネルにより、テナントの仮想ネットワークと外部ネットワーク間の接続が可能になります。 GRE プロトコルは、軽量で、サポートは GRE はほとんどのネットワーク デバイスで使用できるためデータの暗号化は必要ありませんトンネリングの理想的な選択肢になります。 

サイト間 (S2S) トンネルで GRE がサポートは、このトピックの後半の説明に従って、テナントの仮想ネットワークと、マルチ テナント ゲートウェイを使用してテナントの外部ネットワーク間の転送の問題を解決します。  
  
GRE トンネルの機能は、次の要件に対処する設計されています。  
  
-   ホスティング プロバイダーは、物理スイッチの構成を変更することがなく転送用の仮想ネットワークを作成できる必要があります。  
  
-   ホスティング プロバイダーは、インフラストラクチャ内の物理スイッチの構成を変更することがなく、外部に公開されたネットワークにサブネットを追加できる必要があります。  
GRE トンネルの機能を有効またはマイクロソフトのテクノロジを使用して、そのサービス オファリングでソフトウェアによるネットワーク制御を実装するサービス プロバイダーをホストするためのいくつか主要なシナリオを強化します。  
  
以下は、いくつかのシナリオの例です。  
  
-   [テナントの物理ネットワークにテナントの仮想ネットワークからのアクセス](#BKMK_Access)  
  
-   [高速の接続](#BKMK_Speed)  
  
-   [VLAN ベースの分離との統合](#BKMK_Integration)  
  
-   [リソースにアクセスする共有](#BKMK_Shared)  
  
-   [テナントにサード パーティ製デバイスのサービス](#BKMK_thirdparty)  
  
## <a name="key-scenarios"></a>主なシナリオ

次に、GRE トンネル機能アドレスである主なシナリオを示します。  
  
### <a name="BKMK_Access"></a>テナントの物理ネットワークにテナントの仮想ネットワークからのアクセス

このシナリオでは、テナントのホスティング サービス プロバイダー プレミス上にある物理ネットワークにテナントの仮想ネットワークからのアクセスを提供するスケーラブルな方法を使用できます。 マルチ テナント ゲートウェイ GRE トンネル エンドポイントが確立されている、サード パーティのデバイスの物理ネットワーク上の他の GRE トンネル エンドポイントが確立されています。 仮想ネットワーク内の仮想および物理ネットワーク上のサード パーティのデバイス間でレイヤー 3 のトラフィックがルーティングされます。  
  
![ホスト側の物理ネットワークとテナント仮想ネットワークを接続している GRE トンネル](../../media/gre-tunneling-in-windows-server/GRE_.png)  
  
### <a name="BKMK_Speed"></a>高速の接続

このシナリオでは、テナントのオンプレミス ネットワークからホスティング サービス プロバイダー ネットワークにある自分の仮想ネットワークへの高速接続を提供するスケーラブルな方法を使用できます。 テナントは、マルチ プロトコル ラベルの切り替え (MPLS)、ホスティング サービス プロバイダーのエッジ ルーターとテナントの仮想ネットワークにマルチ テナント ゲートウェイの間 GRE トンネルが確立されている場所を使用して、サービス プロバイダーのネットワークに接続します。  
  
![テナント エンタープライズ MPLS ネットワークとテナント仮想ネットワークを接続している GRE トンネル](../../media/gre-tunneling-in-windows-server/GRE-.png)  
  
### <a name="BKMK_Integration"></a>VLAN ベースの分離との統合

このシナリオでは、HYPER-V ネットワーク仮想化と VLAN ベースの分離を統合することができます。 ホスティング プロバイダー ネットワーク上の物理ネットワークには、VLAN ベースの分離を使用してロード バランサーが含まれています。 マルチ テナント ゲートウェイは、物理ネットワーク上のロード バランサーと仮想ネットワーク上のマルチ テナント ゲートウェイの間の GRE トンネルを確立します。  
  
ソースと宛先間の複数のトンネルを確立して、GRE キーは、トンネルを区別するために使用します。  
  
![複数の GRE トンネリング テナント仮想ネットワークを接続](../../media/gre-tunneling-in-windows-server/GRE-VLANIsolation.png)  
  
### <a name="BKMK_Shared"></a>リソースにアクセスする共有

このシナリオでは、ホスティング プロバイダー ネットワーク上にある物理ネットワーク上の共有リソースにアクセスできます。  
  
複数のテナント仮想ネットワークと共有するホスティング プロバイダー ネットワークにある物理ネットワーク上のサーバー上にある共有サービスがあります。  
  
重複しないサブネットを持つテナント ネットワーク GRE トンネル経由で、一般的なネットワークにアクセスします。 1 つのテナント ゲートウェイは、そのため、適切なテナント ネットワークにパケットをルーティング、GRE トンネル間ルーティングします。  
  
このシナリオでは、サード パーティ製ハードウェア アプライアンスで、1 つのテナント ゲートウェイを交換できます。  
  
![複数の仮想ネットワークを接続する複数のトンネルを使用して、シングル テナント ゲートウェイ](../../media/gre-tunneling-in-windows-server/GRE-SharedResource.png)  
  
### <a name="BKMK_thirdparty"></a>テナントにサード パーティ製デバイスのサービス

このシナリオは、(ハードウェア ロード バランサー) などのサード パーティ製のデバイスを統合するテナントの仮想ネットワークのトラフィック フローに使用できます。 たとえば、エンタープライズ サイトからのトラフィックは、マルチ テナント ゲートウェイ S2S トンネルを通過します。 トラフィックは、GRE トンネル経由で、ロード バランサーにルーティングされます。 ロード バランサーは、企業の仮想ネットワーク上の複数の仮想マシンにトラフィックをルーティングします。 同じことは、可能性のある仮想ネットワーク内の IP アドレスを重複している別のテナントは発生します。 ネットワーク トラフィックは、Vlan を使用して、ロード バランサー上に分離され、Vlan をサポートするすべてのレイヤー 3 デバイスに適用されます。  
  
![複数の GRE トンネリング サード パーティ製のデバイスに仮想ネットワークを接続](../../media/gre-tunneling-in-windows-server/GREThirdParty.png)  
  
## <a name="configuration-and-deployment"></a>構成と展開

GRE トンネルは、S2S インターフェイス内で追加のプロトコルとして公開されます。 同様の方法で、次のネットワークのブログで説明されている、IPSec S2S トンネルとして実装されます。[Windows Server 2012 R2 を使用してマルチ テナント サイト対サイト (間 S2S) VPN Gateway](https://blogs.technet.com/b/networking/archive/2013/09/29/multi-tenant-site-to-site-s2s-vpn-gateway-with-windows-server-2012-r2.aspx)  
  
GRE トンネル ゲートウェイを含むゲートウェイをデプロイする例については、次のトピックを参照してください。  
  
[スクリプトを使用してソフトウェア定義ネットワーク インフラストラクチャをデプロイします。](../../../networking/sdn/deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)
  
## <a name="more-information"></a>詳細情報

S2S ゲートウェイの展開に関する詳細については、次のトピックを参照してください。  
  
-   [RAS ゲートウェイ](RAS-Gateway.md)  
  
-   [ボーダー ゲートウェイ プロトコル&#40;BGP&#41;](../bgp/Border-Gateway-Protocol-BGP.md)  
  
-   [新機能！Windows Server 2012 R2 RAS マルチ テナント ゲートウェイ展開ガイド](https://blogs.technet.com/b/wsnetdoc/archive/2014/03/26/new-windows-server-2012-r2-RAS-multitenant-gateway-deployment-guide.aspx)  
  
-   [RAS マルチ テナント ゲートウェイとボーダー ゲートウェイ プロトコル (BGP) のデプロイします。](https://blogs.technet.com/b/wsnetdoc/archive/2014/04/03/deploy-border-gateway-protocol-bgp-with-the-RAS-multitenant-gateway.aspx)  
  


