---
title: Windows Server 2016 の GRE トンネリング
description: このトピックを使用すると、Windows Server 2016 の RAS ゲートウェイに対する汎用ルーティングカプセル化 (GRE) トンネル機能の更新について理解できます。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: df2023bf-ba64-481e-b222-6f709edaa5c1
ms.author: lizross
author: eross-msft
ms.openlocfilehash: d246f0e56681f75e4336ed225d1557a0e05c581b
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80308556"
---
# <a name="gre-tunneling-in-windows-server-2016"></a>Windows Server 2016 の GRE トンネリング

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

Windows Server 2016 では、汎用ルーティングカプセル化の更新プログラムとして、RA ゲートウェイの GRE\) トンネル機能 \(ます。  
  
GRE は軽量のトンネリング プロトコルで、インターネット プロトコル インターネットワークを介して Point-to-Point 仮想リンク内のさまざまなネットワーク レイヤー プロトコルをカプセル化できます。 Microsoft GRE 実装では、IPv4 と IPv6 をカプセル化できます。  
  
GRE トンネルは、次のような多くのシナリオで役に立ちます。  
  
-   軽量で RFC 2890 に準拠しているため、さまざまなベンダーデバイスとの相互運用が可能です。  
  
-   動的ルーティングには Border Gateway Protocol \(BGP\) を使用できます。  
  
-   ソフトウェアで定義されたネットワーク \(SDN\) で使用するために、GRE マルチテナント RAS ゲートウェイを構成でき
  
-   System Center Virtual Machine Manager を使用して GRE\-ベースの RAS ゲートウェイを管理できます。
  
-   GRE RAS ゲートウェイとして構成されている6コア仮想マシンで最大 2.0 Gbps のスループットを実現できます。
  
-   1つのゲートウェイで複数の接続モードがサポートされる  
  
GRE ベースのトンネルにより、テナントの仮想ネットワークと外部ネットワーク間の接続が可能になります。 GRE プロトコルは軽量であるため、GRE のサポートはほとんどのネットワークデバイスで利用可能であるため、データの暗号化を必要としないトンネリングに最適な選択肢になります。 

サイト間 (S2S) トンネルの GRE サポートは、このトピックで後述するように、マルチテナントゲートウェイを使用して、テナント仮想ネットワークとテナント外部ネットワーク間の転送の問題を解決します。  
  
GRE トンネル機能は、次の要件に対応するように設計されています。  
  
-   ホスティングプロバイダーは、物理スイッチ構成を変更せずに、転送用の仮想ネットワークを作成できる必要があります。  
  
-   ホスティングプロバイダーは、インフラストラクチャ内の物理スイッチの構成を変更せずに、外部に接続するネットワークにサブネットを追加できる必要があります。  
GRE トンネル機能では、Microsoft テクノロジを使用してサービスプロバイダーをホスティングするためのいくつかの重要なシナリオを実現し、サービスオファリングにソフトウェア定義ネットワークを実装します。  
  
シナリオの例をいくつか次に示します。  
  
-   [テナントの仮想ネットワークからテナントの物理ネットワークへのアクセス](#BKMK_Access)  
  
-   [高速接続](#BKMK_Speed)  
  
-   [VLAN ベースの分離との統合](#BKMK_Integration)  
  
-   [共有リソースへのアクセス](#BKMK_Shared)  
  
-   [テナントへのサードパーティ製デバイスのサービス](#BKMK_thirdparty)  
  
## <a name="key-scenarios"></a>主要なシナリオ

GRE トンネル機能が対処する主なシナリオを次に示します。  
  
### <a name="access-from-tenant-virtual-networks-to-tenant-physical-networks"></a><a name="BKMK_Access"></a>テナントの仮想ネットワークからテナントの物理ネットワークへのアクセス

このシナリオでは、ホスティングサービスプロバイダーの内部に配置されたテナントの仮想ネットワークからテナントの物理ネットワークへのアクセスを、スケーラブルな方法で提供できます。 GRE トンネルエンドポイントはマルチテナントゲートウェイ上に確立され、もう1つの GRE トンネルエンドポイントは、物理ネットワーク上のサードパーティデバイスで確立されます。 レイヤー3のトラフィックは、仮想ネットワーク内の仮想マシンと物理ネットワーク上のサードパーティデバイスの間でルーティングされます。  
  
![ホスト側の物理ネットワークとテナントの仮想ネットワークを接続する GRE トンネル](../../media/gre-tunneling-in-windows-server/GRE_.png)  
  
### <a name="high-speed-connectivity"></a><a name="BKMK_Speed"></a>高速接続

このシナリオでは、オンプレミスのテナントネットワークからホスティングサービスプロバイダーネットワークに配置されている仮想ネットワークへの高速接続を実現するスケーラブルな方法を使用できます。 テナントは、プロトコルラベルの切り替え (MPLS) を使用してサービスプロバイダーネットワークに接続します。これにより、ホスティングサービスプロバイダーのエッジルーターとテナントの仮想ネットワークへのマルチテナントゲートウェイとの間に GRE トンネルが確立されます。  
  
![テナントエンタープライズ MPLS ネットワークとテナント仮想ネットワークを接続する GRE トンネル](../../media/gre-tunneling-in-windows-server/GRE-.png)  
  
### <a name="integration-with-vlan-based-isolation"></a><a name="BKMK_Integration"></a>VLAN ベースの分離との統合

このシナリオでは、VLAN ベースの分離と Hyper-v ネットワーク仮想化を統合できます。 ホスティングプロバイダーネットワーク上の物理ネットワークには、VLAN ベースの分離を使用するロードバランサーが含まれています。 マルチテナントゲートウェイは、物理ネットワーク上のロードバランサーと仮想ネットワーク上のマルチテナントゲートウェイとの間で GRE トンネルを確立します。  
  
送信元と送信先の間には複数のトンネルを確立できます。また、GRE キーはトンネルを区別するために使用されます。  
  
![テナント仮想ネットワークを接続する複数の GRE トンネル](../../media/gre-tunneling-in-windows-server/GRE-VLANIsolation.png)  
  
### <a name="access-shared-resources"></a><a name="BKMK_Shared"></a>共有リソースへのアクセス

このシナリオでは、ホスティングプロバイダーネットワークに配置されている物理ネットワーク上の共有リソースにアクセスできます。  
  
複数のテナント仮想ネットワークと共有するホスティングプロバイダーネットワークに配置されている物理ネットワーク上のサーバーに、共有サービスが配置されている場合があります。  
  
重複しないサブネットを持つテナントネットワークは、GRE トンネル経由で共通ネットワークにアクセスします。 1つのテナントゲートウェイが GRE トンネル間でルーティングされるため、適切なテナントネットワークにパケットがルーティングされます。  
  
このシナリオでは、単一のテナントゲートウェイをサードパーティのハードウェアアプライアンスに置き換えることができます。  
  
![複数のトンネルを使用して複数の仮想ネットワークに接続するシングルテナントゲートウェイ](../../media/gre-tunneling-in-windows-server/GRE-SharedResource.png)  
  
### <a name="services-of-third-party-devices-to-tenants"></a><a name="BKMK_thirdparty"></a>テナントへのサードパーティ製デバイスのサービス

このシナリオは、サードパーティ製デバイス (ハードウェアロードバランサーなど) をテナントの仮想ネットワークトラフィックフローに統合するために使用できます。 たとえば、エンタープライズサイトから送信されるトラフィックは、S2S トンネルを介してマルチテナントゲートウェイに渡されます。 トラフィックは、GRE トンネル経由でロードバランサーにルーティングされます。 ロードバランサーは、企業の仮想ネットワーク上の複数の仮想マシンにトラフィックをルーティングします。 仮想ネットワーク内の IP アドレスが重複する可能性がある別のテナントでも同じことが行われます。 ネットワークトラフィックは、Vlan を使用してロードバランサー上で分離され、Vlan をサポートするすべてのレイヤー3デバイスに適用されます。  
  
![サードパーティのデバイスに仮想ネットワークを接続する複数の GRE トンネル](../../media/gre-tunneling-in-windows-server/GREThirdParty.png)  
  
## <a name="configuration-and-deployment"></a>構成と展開

GRE トンネルは、S2S インターフェイス内で追加のプロトコルとして公開されます。 これは、次のネットワークのブログで説明されている IPSec S2S トンネルと同様の方法で実装されます。 [Windows Server 2012 R2 でのマルチテナントサイト間 (S2S) VPN Gateway](https://blogs.technet.com/b/networking/archive/2013/09/29/multi-tenant-site-to-site-s2s-vpn-gateway-with-windows-server-2012-r2.aspx)  
  
GRE トンネルゲートウェイを含むゲートウェイを展開する例については、次のトピックを参照してください。  
  
[スクリプトを使用してソフトウェアで定義されたネットワークインフラストラクチャを展開する](../../../networking/sdn/deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)
  
## <a name="more-information"></a>詳細

S2S ゲートウェイの展開の詳細については、次のトピックを参照してください。  
  
-   [RAS ゲートウェイ](RAS-Gateway.md)  
  
-   [Border Gateway Protocol &#40;BGP&#41;](../bgp/Border-Gateway-Protocol-BGP.md)  
  
-   [新機能！Windows Server 2012 R2 RAS マルチテナントゲートウェイ展開ガイド](https://blogs.technet.com/b/wsnetdoc/archive/2014/03/26/new-windows-server-2012-r2-RAS-multitenant-gateway-deployment-guide.aspx)  
  
-   [RAS マルチテナントゲートウェイを使用して Border Gateway Protocol (BGP) を展開する](https://blogs.technet.com/b/wsnetdoc/archive/2014/04/03/deploy-border-gateway-protocol-bgp-with-the-RAS-multitenant-gateway.aspx)  
  


