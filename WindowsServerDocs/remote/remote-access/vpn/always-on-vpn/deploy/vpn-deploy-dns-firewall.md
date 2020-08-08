---
title: DNS とファイアウォールの設定を構成する
description: このトピックでは、Windows Server 2016 で Always On VPN を展開するための詳細な手順について説明します。
ms.topic: article
ms.assetid: d8cf3bae-45bf-4ffa-9205-290d555c59da
ms.localizationpriority: medium
ms.author: v-tea
author: Teresa-MOTIV
ms.date: 06/11/2018
ms.openlocfilehash: 99db65c2c5bd78154e14ab9e388eb709351afc11
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87946685"
---
# <a name="step-5-configure-dns-and-firewall-settings"></a>手順 5. DNS とファイアウォールの設定を構成する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows 10

- [**前へ:** 手順 4.NPS サーバーをインストールして構成する](vpn-deploy-nps.md)
- [**次のようになります。** 手順 6.Windows 10 クライアント Always On VPN 接続を構成する](vpn-deploy-client-vpn-connections.md)

この手順では、VPN 接続用の DNS とファイアウォールの設定を構成します。

## <a name="configure-dns-name-resolution"></a>DNS 名前解決の構成

リモート VPN クライアントは、接続するときに、内部のクライアントが使用しているのと同じ DNS サーバーを使用します。これにより、内部ワークステーションの他の部分と同じ方法で名前を解決できます。

このため、外部クライアントが VPN サーバーへの接続に使用するコンピューター名が、VPN サーバーに発行された証明書で定義されているサブジェクトの別名と一致していることを確認する必要があります。

リモートクライアントが VPN サーバーに接続できるようにするには、外部 DNS ゾーンに DNS A (ホスト) レコードを作成します。 A レコードは、VPN サーバーの証明書のサブジェクト代替名を使用する必要があります。

### <a name="to-add-a-host-a-or-aaaa-resource-record-to-a-zone"></a>ホスト (A または AAAA) リソースレコードをゾーンに追加するには

1. DNS サーバーの [サーバーマネージャーで、[**ツール**] を選択し、[ **dns**] を選択します。 DNS マネージャーが開きます。
2. DNS マネージャーコンソールツリーで、管理するサーバーを選択します。
3. 詳細ウィンドウの [**名前**] で、[**前方参照ゾーン**] をダブルクリックして、ビューを展開します。
4. [**前方参照ゾーン**の詳細] で、レコードを追加する前方参照ゾーンを右クリックし、[**新しいホスト (a または AAAA)**] を選択します。 [**新しいホスト**] ダイアログボックスが表示されます。
5. [**新しいホスト**] の [**名前**] に、VPN サーバーの証明書のサブジェクト代替名を入力します。
6. [IP アドレス] に、VPN サーバーの IP アドレスを入力します。 IP version 4 (IPv4) 形式でアドレスを入力して、ホスト (A) リソースレコードまたは IP バージョン 6 (IPv6) 形式を追加し、ホスト (AAAA) リソースレコードを追加することができます。
7. 入力した IP アドレスを含め、IP アドレスの範囲に対して逆引き参照ゾーンを作成した場合は、[**関連付けられたポインター (PTR) レコードを作成**する] チェックボックスをオンにします。  このオプションを選択すると、[**名前**] と [ **IP アドレス**] に入力した情報に基づいて、このホストの逆引きゾーンに追加のポインター (PTR) リソースレコードが作成されます。
8. [**ホストの追加**] を選択します。

## <a name="configure-the-edge-firewall"></a>エッジファイアウォールを構成する

エッジファイアウォールは、外部境界ネットワークをパブリックインターネットから分離します。 この分離を視覚的に表現するには、「 [VPN テクノロジの概要](../always-on-vpn-technology-overview.md)」のトピックの図を参照してください Always On。

エッジファイアウォールは、特定のポートを VPN サーバーに許可および転送する必要があります。 エッジファイアウォールでネットワークアドレス変換 (NAT) を使用する場合は、ユーザーデータグラムプロトコル (UDP) ポート500および4500のポートフォワーディングを有効にすることが必要になる場合があります。 これらのポートは、VPN サーバーの外部インターフェイスに割り当てられている IP アドレスに転送します。

受信トラフィックをルーティングし、VPN サーバーで NAT を実行する場合は、ファイアウォール規則を開いて、VPN サーバーのパブリックインターフェイスに適用されている外部 IP アドレスに対して受信する UDP ポート500および4500を許可する必要があります。

どちらの場合でも、ファイアウォールでディープパケットインスペクションがサポートされており、クライアント接続を確立することが困難な場合は、IKE セッションのディープパケットインスペクションを緩和または無効にする必要があります。

これらの構成変更を行う方法については、ファイアウォールのドキュメントを参照してください。

## <a name="configure-the-internal-perimeter-network-firewall"></a>内部境界ネットワークファイアウォールを構成する

内部境界ネットワークファイアウォールによって、組織/企業ネットワークが内部境界ネットワークから切り離されます。 この分離を視覚的に表現するには、「 [VPN テクノロジの概要](../always-on-vpn-technology-overview.md)」のトピックの図を参照してください Always On。

この展開では、境界ネットワーク上のリモートアクセス VPN サーバーは RADIUS クライアントとして構成されます。  VPN サーバーは、企業ネットワーク上の NPS に RADIUS トラフィックを送信し、NPS から RADIUS トラフィックも受信します。

双方向での RADIUS トラフィックのフローを許可するようにファイアウォールを構成します。

>[!NOTE]
>組織または企業ネットワーク上の NPS サーバーは、RADIUS クライアントである VPN サーバーの RADIUS サーバーとして機能します。 RADIUS インフラストラクチャの詳細については、「[ネットワークポリシーサーバー (NPS)](../../../../../networking/technologies/nps/nps-top.md)」を参照してください。

### <a name="radius-traffic-ports-on-the-vpn-server-and-nps-server"></a>VPN サーバーと NPS サーバー上の RADIUS トラフィックポート

既定では、NPS と VPN は、インストールされているすべてのネットワークアダプター上で、ポート1812、1813、1645、および1646の RADIUS トラフィックをリッスンします。 NPS をインストールするときに、セキュリティが強化された Windows ファイアウォールを有効にすると、これらのポートに対するファイアウォールの例外が、IPv6 トラフィックと IPv4 トラフィックの両方のインストールプロセス中に自動的に作成されます。

>[!IMPORTANT]
>ネットワークアクセスサーバーが、これらの既定以外のポートで RADIUS トラフィックを送信するように構成されている場合は、「セキュリティが強化された Windows ファイアウォール」で作成した例外を NPS のインストール時に削除し、RADIUS トラフィックに使用するポートに対して例外を作成します。

### <a name="use-the-same-radius-ports-for-the-internal-perimeter-network-firewall-configuration"></a>内部境界ネットワークファイアウォール構成に同じ RADIUS ポートを使用する

VPN サーバーと NPS サーバーで既定の RADIUS ポート構成を使用する場合は、内部境界ネットワークファイアウォールで次のポートを開いていることを確認してください。

- ポート UDP1812、UDP1813、UDP1645、および UDP1646

NPS の展開で既定の RADIUS ポートを使用していない場合は、使用しているポートで RADIUS トラフィックを許可するようにファイアウォールを構成する必要があります。 詳細については、「 [Configure firewall FOR RADIUS Traffic](../../../../../networking/technologies/nps/nps-firewalls-configure.md)」を参照してください。

## <a name="next-steps"></a>次のステップ

[手順 6.Windows 10 クライアント Always On VPN 接続を構成](vpn-deploy-client-vpn-connections.md)する: この手順では、vpn 接続を使用して、そのインフラストラクチャと通信するように windows 10 クライアントコンピューターを構成します。 Windows PowerShell、Microsoft Endpoint Configuration Manager、Intune などの Windows 10 VPN クライアントを構成するには、いくつかのテクノロジを使用できます。 3つすべてに、適切な VPN 設定を構成するための XML VPN プロファイルが必要です。