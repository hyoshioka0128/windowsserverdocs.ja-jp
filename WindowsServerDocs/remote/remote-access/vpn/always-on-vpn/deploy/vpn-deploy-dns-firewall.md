---
title: DNS とファイアウォールの設定を構成する
description: このトピックでは、Always On VPN では、Windows Server 2016 を展開するための詳細な手順を説明します。
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: d8cf3bae-45bf-4ffa-9205-290d555c59da
ms.localizationpriority: medium
ms.author: pashort
author: shortpatti
ms.date: 06/11/2018
ms.openlocfilehash: 9cee39dbf240cac9701f926600d8efeffe99c214
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749487"
---
# <a name="step-5-configure-dns-and-firewall-settings"></a>手順 5. DNS とファイアウォール設定を構成します。

>適用対象:Windows Server 2016、Windows Server 2012 R2、Windows 10 の Windows Server (半期チャネル)

- [**先の：** 手順 4.NPS サーバーをインストールして構成する](vpn-deploy-nps.md)
- [**次に：** 手順 6.Windows 10 クライアントの Always On VPN 接続を構成する](vpn-deploy-client-vpn-connections.md)

DNS とファイアウォールを構成するこの手順で VPN 接続用に設定します。

## <a name="configure-dns-name-resolution"></a>DNS 名前解決を構成します。

リモート VPN クライアントが、接続を使用、内部クライアントを使用して、同じ DNS サーバー名を内部のワークステーションの残りの部分と同じ方法で解決できます。

このため、外部クライアントが VPN サーバーへの接続に使用するコンピューター名が VPN サーバーに発行された証明書で定義されている、サブジェクト代替名と一致していることを確認する必要があります。

リモート クライアントが VPN サーバーに接続できるようにするには、外部の DNS ゾーンに DNS A (ホスト) レコードを作成できます。 A レコードは、VPN サーバーの証明書のサブジェクト代替名を使用する必要があります。

### <a name="to-add-a-host-a-or-aaaa-resource-record-to-a-zone"></a>ホスト (A または AAAA) リソース レコードをゾーンに追加するには

1. DNS サーバーでサーバー マネージャーで、次のように選択します。**ツール**、し、 **DNS**します。 DNS マネージャーが開きます。
2. DNS マネージャー コンソール ツリーで、管理するサーバーを選択します。
3. 詳細ペインでの**名前**、 をダブルクリックします**前方参照ゾーン**表示を展開します。
4. **前方参照ゾーン**の詳細は、レコードを追加し、選択する前方参照ゾーンを右クリックして**新しいホスト (A または AAAA)** します。 **新しいホスト** ダイアログ ボックスが表示されます。
5. **新しいホスト**の**名前**、VPN サーバーの証明書のサブジェクト代替名を入力します。
6. IP アドレスには、VPN サーバーの IP アドレスを入力します。 Ip バージョン 4 (IPv4) アドレスを入力するホスト (AAAA) リソース レコードを追加するホスト (A) リソース レコード、または IP version 6 (IPv6) を追加する形式が書式設定します。
7. 入力した IP アドレスを含む、範囲の IP アドレスの逆引き参照ゾーンを選択した場合、**関連付けられたポインター (PTR) レコードを作成する**チェック ボックスをオンします。  このオプションを選択すると逆引き参照ゾーンで入力した情報に基づいて、このホストの追加のポインター (PTR) リソース レコードを作成**名前**と**IP アドレス**します。
8. 選択**ホストの追加**します。

## <a name="configure-the-edge-firewall"></a>エッジ ファイアウォールを構成します。

エッジ ファイアウォールでは、パブリック インターネットから外部境界ネットワークを分離します。 この分離の視覚的表現は、トピックの図を参照してください。 [VPN 技術概要で常に](../always-on-vpn-technology-overview.md)します。

できること、エッジ ファイアウォール、および特定のポートを VPN サーバーに転送します。 エッジ ファイアウォールでネットワーク アドレス変換 (NAT) を使用する場合は、ユーザー データグラム プロトコル (UDP) ポート 500 と 4500 のポート フォワーディングを有効にする必要があります。 VPN サーバーの外部インターフェイスに割り当てられている IP アドレスにこれらのポートを転送します。

トラフィックをルーティングする場合は、受信し、UDP を許可するファイアウォール規則を開く必要がありますし、または、VPN サーバーの背後に NAT を実行して、外部 IP アドレスを VPN サーバー上のパブリック インターフェイスに適用する入力方向のポート 500 と 4500 です。

どちらの場合、ファイアウォールは、詳細なパケット検査をサポートしていますが、クライアント接続を確立できない場合、緩和または IKE のセッションの詳細なパケット検査を無効にする必要がありますましょう。

これらの構成を変更する方法については、ファイアウォールのマニュアルを参照してください。

## <a name="configure-the-internal-perimeter-network-firewall"></a>内部の境界ネットワークのファイアウォールを構成します。

内部の境界ネットワークのファイアウォールは、内部の境界ネットワークから組織または企業ネットワークを分離します。 この分離の視覚的表現は、トピックの図を参照してください。 [VPN 技術概要で常に](../always-on-vpn-technology-overview.md)します。

この展開では、境界ネットワーク上のリモート アクセス VPN サーバーが RADIUS クライアントとして構成されます。  VPN サーバーでは、企業ネットワーク上の NPS を RADIUS トラフィックを送信しも、NPS から RADIUS トラフィックを受信します。

双方向にフローする RADIUS トラフィックを許可するファイアウォールを構成します。

>[!NOTE]
>RADIUS クライアントである VPN サーバー用の RADIUS サーバーとして、組織または企業ネットワークの機能上の NPS サーバー。 RADIUS インフラストラクチャの詳細については、次を参照してください。[ネットワーク ポリシー サーバー (NPS)](../../../../../networking/technologies/nps/nps-top.md)します。

### <a name="radius-traffic-ports-on-the-vpn-server-and-nps-server"></a>VPN サーバーと NPS サーバーの RADIUS トラフィックのポート

既定では、NPS および VPN が RADIUS トラフィックをすべてインストールされているネットワーク アダプターのポート 1812、1813、1645、および 1646 でリッスンします。 NPS をインストールするときにセキュリティが強化された Windows ファイアウォールを有効にした場合、IPv6 と IPv4 の両方のトラフィックのインストール プロセス中にこれらのポートに対するファイアウォールの例外が自動的に作成を取得します。

>[!IMPORTANT]
>これらの既定値以外のポート経由で RADIUS トラフィックを送信するようにネットワーク アクセス サーバーを場合、NPS のインストール中にセキュリティが強化された Windows ファイアウォールで作成された例外を削除しを使用したポートに対する例外を作成RADIUS トラフィック。

### <a name="use-the-same-radius-ports-for-the-internal-perimeter-network-firewall-configuration"></a>RADIUS のと同じポートを使用して、内部の境界ネットワークのファイアウォール構成用

で、VPN サーバーと NPS サーバーを RADIUS ポートの既定の構成を使用する場合は、内部の境界ネットワークのファイアウォールで、次のポートを開くことを確認します。

- ポート UDP1812、UDP1813、UDP1645、および UDP1646

NPS 展開に既定の RADIUS ポートを使用していない場合は、使用しているポートで RADIUS トラフィックを許可するファイアウォールを構成する必要があります。 詳細については、次を参照してください。 [RADIUS トラフィックのファイアウォールの構成](../../../../../networking/technologies/nps/nps-firewalls-configure.md)します。

## <a name="next-steps"></a>次のステップ

[手順 6.VPN 接続で常に Windows 10 クライアントを構成](vpn-deploy-client-vpn-connections.md):この手順では、VPN 接続を持つそのインフラストラクチャと通信するために Windows 10 クライアント コンピューターを構成します。 いくつかのテクノロジを使用して、Windows PowerShell、System Center Configuration Manager では、Intune などの Windows 10 の VPN クライアントを構成することができます。 3 つすべては、XML の VPN プロファイルを適切な VPN 設定を構成する必要があります。