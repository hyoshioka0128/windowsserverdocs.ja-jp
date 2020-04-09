---
title: ネットワーク機能の仮想化
description: このトピックでは、ネットワーク機能の仮想化について説明します。これにより、Windows Server 2016 で Datacenter Firewall、マルチテナント RAS ゲートウェイ、ソフトウェア負荷分散 (SLB) などの仮想ネットワークアプライアンスを展開することができます。
manager: grcusanz
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 79df3bbe-48fd-4eff-8df6-35f6317566f3
ms.author: anpaul
author: AnirbanPaul
ms.openlocfilehash: aed1591756e7b491bd4c9ab325694dfb3e6fddb1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859625"
---
# <a name="network-function-virtualization"></a>ネットワーク機能の仮想化

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、ネットワーク機能の仮想化について説明します。これにより、データセンターファイアウォール、マルチテナント RAS ゲートウェイ、ソフトウェア負荷分散 \(SLB\) マルチプレクサー \(MUX\)などの仮想ネットワークアプライアンスを展開できます。
  
>[!NOTE]  
>このトピックに加え、次のネットワーク機能の仮想化のドキュメントは使用できます。  
> - [Datacenter Firewall の概要](../../../sdn/technologies/network-function-virtualization/../../../sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)  
> - [SDN の RAS ゲートウェイ](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)  
> - [SDN のソフトウェア負荷分散 (SLB)](../../../sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md)  
  
今日のソフトウェアで定義されているデータ センター、(ロード バランサー、ファイアウォール、ルーター、スイッチ、およびなど) などのハードウェア アプライアンスで実行されているネットワークの機能がますますされている仮想化仮想アプライアンスとして。 この「ネットワーク機能の仮想化」は、サーバーの仮想化とネットワーク仮想化の自然な流れです。 仮想アプライアンスが急速に登場し、新しい市場が作成されます。 常に興味を引くと両方の仮想化プラットフォームで運動量を取得し、クラウド サービスです。  
  
Microsoft には、Windows Server 2012 R2 で始まる仮想アプライアンスとしてスタンドアロン ゲートウェイが含まれています。 詳細については、「[Windows Server ゲートウェイ](https://technet.microsoft.com/library/dn313101.aspx)」を参照してください。 今すぐ Windows Server 2016 microsoft を展開し、ネットワーク機能の仮想化市場への投資を続行します。  
  
## <a name="virtual-appliance-benefits"></a>仮想アプライアンスの利点  
仮想アプライアンスは、動的かつ簡単にカスタマイズした、事前構成済みの仮想マシンのため、変更です。 1 つまたは複数の仮想マシンをパッケージ化、更新、および単位として管理できます。 ネットワーク (SDN) を定義したソフトウェアと連携して、機敏性と柔軟性今日のクラウド ベースのインフラストラクチャにします。 例 :  
  
-   SDN は、プールされたおよび動的なリソースとして、ネットワークを表示します。  
  
-   SDN には、テナントの分離が容易になります。  
  
-   SDN には、拡張性とパフォーマンスが最大化します。  
  
-   仮想アプライアンスでは、シームレスな容量の拡張とワークロードを移動できるようにします。  
  
-   仮想アプライアンスには、運用に伴う複雑さが最小限に抑えます。  
  
-   仮想アプライアンスは、取得、配置、および事前に統合されたソリューションの管理を簡単に顧客に知らせます。  
  
    -   お客様に簡単に移動できます仮想アプライアンス任意の場所、クラウドで。  
  
    -   顧客は、仮想アプライアンスをスケール アップまたはダウンに基づいて動的に要求します。  
  
Microsoft SDN の詳細については、次を参照してください。 [ソフトウェア定義されるネットワーク](https://technet.microsoft.com/windows-server-docs/networking/sdn/software-defined-networking--sdn-)します。  
  
### <a name="what-network-functions-are-being-virtualized"></a>どのようなネットワーク機能が仮想化されているか。  
仮想化されたネットワーク機能の市場はすぐに増加しています。 次のネットワーク機能を仮想化します。  
  
-   **セキュリティ**  
  
    -   ファイアウォール  
  
    -   ウイルス対策  
  
    -   DDoS (分散型サービス拒否)  
  
    -   Ip アドレス/ID (侵入防止システム/侵入検出システム)  
  
-   **アプリケーション/WAN オプティマイザー**  
  
-   **自動**  
  
    -   サイト間ゲートウェイ  
  
    -   L3 ゲートウェイ  
  
    -   ルーター  
  
    -   スイッチ  
  
    -   NAT  
  
    -   ロード バランサー (端) ではありません。  
  
    -   HTTP プロキシ  
  
## <a name="why-microsoft-is-a-great-platform-for-virtual-appliances"></a>なぜマイクロソフトは、仮想アプライアンスに適したプラットフォーム  
![仮想ネットワーク スタック](../../../media/Network-Function-Virtualization/Microsoft-Network-Function-Virtualization.png)  
  
Microsoft プラットフォームが最適なプラットフォームをビルドし、仮想アプライアンスを展開するエンジニア リングされています。 理由は次のとおりです。  
  
-   Microsoft では、Windows Server 2016 で重要な仮想化されたネットワーク機能を提供します。  
  
-   好みのベンダーからの仮想アプライアンスを展開することができます。  
  
-   展開、構成、および Windows Server 2016 に付属している Microsoft ネットワーク コント ローラーで、仮想アプライアンスを管理することができます。 ネットワーク コント ローラーの詳細については、次を参照してください。 [ネットワーク コント ローラー](../../../sdn/technologies/network-controller/Network-Controller.md)します。  
  
-   HYPER-V では、必要な最上位のゲスト オペレーティング システムをホストできます。  
  
## <a name="network-function-virtualization-in-windows-server-2016"></a>Windows Server 2016 のネットワーク機能の仮想化  
  
### <a name="virtual-appliances-functions-provided-by-microsoft"></a>Microsoft によって提供される仮想アプライアンス関数  
Windows Server 2016 では、次の仮想アプライアンスが用意されています。  
  
**ソフトウェアロードバランサー**  
  
データ センターのスケールで動作している 4 層のロード バランサーです。 これは、Azure 環境内で大規模に展開されている Azure のロード バランサーのようなバージョンです。 Microsoft ソフトウェア ロード バランサーの詳細については、次を参照してください。 [ソフトウェア負荷分散 (SLB) SDN の](https://technet.microsoft.com/library/mt632286.aspx)です。 Microsoft Azure の負荷分散サービスの詳細については、次を参照してください。 [Microsoft Azure の負荷分散サービス](https://azure.microsoft.com/blog/2014/04/08/microsoft-azure-load-balancing-services/)します。  
  
**ゲートウェイ**します。 RAS ゲートウェイは、次のゲートウェイの機能のすべての組み合わせを提供します。  
  
-   **サイト対サイトゲートウェイ**  
  
    RAS ゲートウェイは、ボーダー ゲートウェイ プロトコル (BGP) の対応、マルチ テナント ゲートウェイにアクセスして、リモート サイトからサイト間 VPN 接続経由で、リソースを管理するテナントを使用して、クラウドおよびテナントの物理ネットワーク内の仮想リソース間のネットワーク トラフィック フローを許可します。 RAS ゲートウェイの詳細については、次を参照してください。 [RAS ゲートウェイの高可用性](https://technet.microsoft.com/library/mt631692.aspx) と [RAS ゲートウェイ](https://technet.microsoft.com/library/mt626650.aspx)します。  
  
-   **ゲートウェイの転送**  
  
    RAS ゲートウェイは、仮想ネットワークとプロバイダーのホストの物理ネットワーク間のトラフィックをルーティングします。 たとえば、テナントが 1 つまたは複数の仮想ネットワークを作成、ホスティング プロバイダーで物理ネットワーク上の共有リソースへのアクセスを必要がある場合は、転送ゲートウェイは、仮想ネットワークとユーザーが必要なサービスと仮想ネットワーク上の操作を提供する物理ネットワーク間のトラフィックをルーティングできます。 詳細については、次を参照してください。 [RAS ゲートウェイの高可用性](https://technet.microsoft.com/library/mt631692.aspx) と [RAS ゲートウェイ](https://technet.microsoft.com/library/mt626650.aspx)します。  
  
-   **GRE トンネルゲートウェイ**  
  
    GRE ベースのトンネルにより、テナントの仮想ネットワークと外部ネットワーク間の接続が可能になります。 GRE プロトコルは、軽量で、サポートは GRE はほとんどのネットワーク デバイスで利用可能であるため、データの暗号化は必要ありませんトンネリングにとって最適な選択肢になります。 サイト間 (S2S) トンネルの GRE サポートは、マルチテナント ゲートウェイを使用して、テナントの仮想ネットワークとテナントの外部ネットワーク間の転送の問題を解決します。 GRE トンネルの詳細については、次を参照してください。 [GRE は、Windows Server 2016 でトンネリング](https://technet.microsoft.com/library/dn765485.aspx)します。  
  
**BGP を使用したルーティングコントロールプレーン**  
  
HYPER-V ネットワーク仮想化 (HNV) ルーティング コントロールは、すべての顧客の住所平面ルートを実行し、動的には学習を仮想ネットワークには、分散の RAS ゲートウェイ ルーターを更新する制御平面に論理的で一元的なエンティティです。 詳細については、次を参照してください。 [RAS ゲートウェイの高可用性](https://technet.microsoft.com/library/mt631692.aspx) と [RAS ゲートウェイ](https://technet.microsoft.com/library/mt626650.aspx)します。  
  
**分散マルチテナントファイアウォール**  
  
ファイアウォールは、仮想ネットワークのネットワーク層を保護します。 各テナント VM の SDN vSwitch ポートでは、ポリシーが適用されます。 すべてのトラフィック フローが保護: 東西部と北南です。 ポリシーは、テナント ポータルを介してプッシュし、ネットワーク コント ローラーに適用可能なすべてのホストに整列します。 分散型のマルチ テナント ファイアウォールの詳細については、次を参照してください。 [データ センターのファイアウォールの概要](../../../sdn/technologies/network-function-virtualization/../../../sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)します。  
  


