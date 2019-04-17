---
title: ネットワーク関数仮想化
description: このトピックを使用すると、データ センターのファイアウォール、マルチテナントの RAS ゲートウェイ、およびソフトウェア負荷分散 (SLB) Windows Server 2016 でのように仮想ネットワーク アプライアンスを展開することができますネットワーク関数仮想化について説明します。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 79df3bbe-48fd-4eff-8df6-35f6317566f3
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7caa9eef42cb7ab95a13d64c1dcd3639b1132eb3
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="network-function-virtualization"></a>ネットワーク関数仮想化

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、データ センターのファイアウォール、マルチテナント RAS ゲートウェイ、およびソフトウェアの負荷分散 \(SLB\) などの仮想ネットワーク アプライアンスを展開することができますネットワーク関数仮想化についてマルチプレクサー \(MUX\) します。
  
>[!NOTE]  
>このトピックに加え、次のネットワーク機能の仮想化のドキュメントは使用できます。  
> - [データ センターのファイアウォールの概要](../../../sdn/technologies/network-function-virtualization/../../../sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)  
> - [SDN の RAS ゲートウェイ](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)  
> - [ソフトウェアの負荷分散 (SLB) SDN](../../../sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md)  
  
今日のソフトウェアで定義されているデータ センター、(ロード バランサー、ファイアウォール、ルーター、スイッチ、およびなど) などのハードウェア アプライアンスで実行されているネットワーク機能がますますされている仮想化仮想アプライアンスとして。 この「ネットワーク関数仮想化」は、サーバー仮想化とネットワーク仮想化の自然な流れです。 仮想アプライアンスはすばやく顕在化しつつ、新しい市場を作成します。 興味を引くと両方の仮想化プラットフォームで運動量を取得し、クラウド サービスを続行します。  
  
Microsoft には、Windows Server 2012 R2 で始まる仮想アプライアンスとしてスタンドアロン ゲートウェイが含まれています。 詳細については、次を参照してください。[Windows Server ゲートウェイ](https://technet.microsoft.com/library/dn313101.aspx)します。 今すぐと Windows Server 2016 Microsoft を展開し、ネットワーク関数仮想化市場への投資が続行されます。  
  
## <a name="virtual-appliance-benefits"></a>仮想アプライアンスの利点  
仮想アプライアンスは、動的かつ簡単にカスタマイズした、事前構成済みの仮想マシンになっているために変更します。 1 つまたは複数の仮想マシンにパッケージ化、更新、および単位として管理できます。 ネットワーク (SDN) 定義されているソフトウェアと連携して、機敏性と柔軟性今日のクラウド ベースのインフラストラクチャにします。 例えば：  
  
-   SDN には、プールされたおよび動的なリソースとして、ネットワークが表示されます。  
  
-   SDN には、テナントの分離が容易になります。  
  
-   SDN には、スケールとパフォーマンスが最大化します。  
  
-   仮想アプライアンスには、シームレスな容量拡張とワークロード モビリティが有効にします。  
  
-   仮想アプライアンスには、運用の複雑さが最小限に抑えます。  
  
-   仮想アプライアンスは、取得、展開、および事前に統合されたソリューションの管理を簡単に顧客に知らせます。  
  
    -   お客様に簡単に移動できます仮想アプライアンス任意の場所、クラウドで。  
  
    -   お客様は、仮想アプライアンスをスケール アップまたはダウンに基づいて動的に要求します。  
  
Microsoft SDN の詳細については、次を参照してください。[ソフトウェアがネットワーク定義](https://technet.microsoft.com/windows-server-docs/networking/sdn/software-defined-networking--sdn-)します。  
  
### <a name="what-network-functions-are-being-virtualized"></a>どのようなネットワーク機能が仮想化されているか。  
仮想化されたネットワーク機能の市場はすぐに増大しています。 次のネットワーク機能を仮想化します。  
  
-   **セキュリティ**  
  
    -   ファイアウォール  
  
    -   ウイルス対策  
  
    -   DDoS (分散型サービス拒否)  
  
    -   Ip アドレス/ID (侵入防止システム/侵入検出システム)  
  
-   **アプリケーション/WAN オプティマイザー.**  
  
-   **Edge**  
  
    -   サイト間ゲートウェイ  
  
    -   L3 ゲートウェイ  
  
    -   ルーター  
  
    -   スイッチ  
  
    -   NAT  
  
    -   ロード バランサー (端) ではありません。  
  
    -   HTTP プロキシ  
  
## <a name="why-microsoft-is-a-great-platform-for-virtual-appliances"></a>なぜマイクロソフトは、仮想アプライアンスに適したプラットフォーム  
![仮想ネットワーク スタック](../../../media/Network-Function-Virtualization/Microsoft-Network-Function-Virtualization.png)  
  
マイクロソフトのプラットフォームは最適なプラットフォームを構築し、仮想アプライアンスを展開するエンジニア リングされています。 理由を次に示します。  
  
-   Microsoft では、Windows Server 2016 で重要な仮想化されたネットワーク機能を提供します。  
  
-   好みのベンダーからの仮想アプライアンスを展開することができます。  
  
-   展開、構成、および Windows Server 2016 に付属している Microsoft ネットワーク コントローラーで、仮想アプライアンスを管理することができます。 ネットワーク コントローラーの詳細については、次を参照してください。[ネットワーク コントローラー](../../../sdn/technologies/network-controller/Network-Controller.md)します。  
  
-   Hyper-V では、必要な上位のゲスト オペレーティング システムをホストできます。  
  
## <a name="network-function-virtualization-in-windows-server-2016"></a>Windows Server 2016 でネットワーク関数仮想化  
  
### <a name="virtual-appliances-functions-provided-by-microsoft"></a>Microsoft によって提供される仮想アプライアンス関数  
Windows Server 2016 では、次の仮想アプライアンスが用意されています。  
  
**ソフトウェア ロード バランサー**  
  
データ センターのスケールで動作して 4 層のロード バランサーです。 これは、Azure 環境内で大規模に展開されている Azure のロード バランサーのようなバージョンです。 Microsoft ソフトウェア ロード バランサーの詳細については、次を参照してください。[ソフトウェア負荷分散 (SLB) SDN の](https://technet.microsoft.com/library/mt632286.aspx)します。 Microsoft Azure の負荷分散サービスの詳細については、次を参照してください。[Microsoft Azure の負荷分散サービス](https://azure.microsoft.com/blog/2014/04/08/microsoft-azure-load-balancing-services/)します。  
  
**ゲートウェイ**します。 RAS ゲートウェイは、次のゲートウェイ機能のすべての組み合わせを提供します。  
  
-   **サイト間ゲートウェイ**  
  
    RAS ゲートウェイは、ボーダー ゲートウェイ プロトコル (BGP) の対応、マルチテナント ゲートウェイへのアクセスし、リモートのサイトからサイト間 VPN 接続経由で、リソースを管理するテナントを使用して、クラウドおよびテナントの物理ネットワーク内の仮想リソース間のネットワーク トラフィック フローをことができます。 RAS ゲートウェイの詳細については、次を参照してください。[RAS ゲートウェイの高可用性](https://technet.microsoft.com/library/mt631692.aspx)と[RAS ゲートウェイ](https://technet.microsoft.com/library/mt626650.aspx)します。  
  
-   **転送ゲートウェイ**  
  
    RAS ゲートウェイは、仮想ネットワークとホスティング プロバイダーの物理ネットワーク間のトラフィックをルーティングします。 たとえば、テナントが 1 つまたは複数の仮想ネットワークを作成、ホスティング プロバイダーで物理ネットワーク上の共有リソースへのアクセスを必要がある場合は、転送ゲートウェイは、仮想ネットワークとユーザーが必要なサービスと仮想ネットワーク上の操作を提供する物理ネットワーク間のトラフィックをルーティングできます。 詳細については、次を参照してください。[RAS ゲートウェイの高可用性](https://technet.microsoft.com/library/mt631692.aspx)と[RAS ゲートウェイ](https://technet.microsoft.com/library/mt626650.aspx)します。  
  
-   **GRE トンネル ゲートウェイ**  
  
    GRE ベースのテナントの仮想ネットワークと外部ネットワーク間トンネル接続が可能にします。 GRE プロトコル軽量で、サポートは GRE はほとんどのネットワーク デバイスで利用可能であるため、データの暗号化は必要ありませんトンネリングに最適なソリューションになります。 サイト間 (S2S) トンネルの GRE サポートは、テナントの仮想ネットワークとマルチテナント ゲートウェイを使用して、テナントの外部ネットワーク間の転送の問題を解決します。 GRE トンネルの詳細については、次を参照してください。[Windows Server 2016 の GRE トンネリング](https://technet.microsoft.com/library/dn765485.aspx)します。  
  
**BGP のルーティングのコントロール平面**  
  
Hyper-V ネットワーク仮想化 (HNV) ルーティング コントロールは、すべての顧客の住所平面ルートを実行し、動的には学習し、仮想ネットワーク内の分散の RAS ゲートウェイ ルーターを更新する制御平面に論理的で一元的なエンティティです。 詳細については、次を参照してください。[RAS ゲートウェイの高可用性](https://technet.microsoft.com/library/mt631692.aspx)と[RAS ゲートウェイ](https://technet.microsoft.com/library/mt626650.aspx)します。  
  
**分散型のマルチテナント ファイアウォール**  
  
ファイアウォールは、仮想ネットワークのネットワーク層を保護します。 各テナント VM の SDN vSwitch ポートで、ポリシーが適用されます。 すべてのトラフィック フローが保護: 東西部と北南です。 ポリシーは、テナント ポータルを介してプッシュし、ネットワーク コントローラーに整列該当するすべてのホストします。 分散型のマルチテナント ファイアウォールの詳細については、次を参照してください。[データ センターのファイアウォールの概要](../../../sdn/technologies/network-function-virtualization/../../../sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)します。  
  


