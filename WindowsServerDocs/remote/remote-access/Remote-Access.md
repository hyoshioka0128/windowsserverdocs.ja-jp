---
title: リモート アクセス
description: このトピックでは、Windows Server 2016 のリモートアクセスサーバーの役割の概要について説明します。
manager: dougkim
ms.topic: article
ms.assetid: eeca4cf7-90f0-485d-843c-76c5885c54b0
ms.author: lizross
author: eross-msft
ms.date: 05/18/2018
ms.openlocfilehash: 3efbc9d05beacdcc1d8ceb466f25dfc59f2bae0c
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87970449"
---
# <a name="remote-access"></a>リモート アクセス

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows 10

リモートアクセスガイドでは、Windows Server 2016 のリモートアクセスサーバーの役割の概要について説明し、次の項目について説明します。

- [Always On VPN 展開ガイド](vpn/always-on-vpn/deploy/always-on-vpn-deploy.md)
- [Border Gateway Protocol &#40;BGP&#41;](bgp/Border-Gateway-Protocol-BGP.md)
- [RAS ゲートウェイ](ras-gateway/RAS-Gateway.md)
- [リモート アクセス サーバーの役割のドキュメント](ras/Remote-Access-Server-Role-Documentation.md)
- [SDN の RAS ゲートウェイ](../../networking/sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)
- [仮想プライベート ネットワーク (VPN)](vpn/vpn-top.md)

その他のネットワークテクノロジの詳細については、「 [Windows Server 2016 のネットワーク](../../networking/index.yml)」を参照してください。

リモートアクセスサーバーの役割は、[リモートアクセスサービス (RAS)](#bkmk_da)、[ルーティング](#bkmk_rras)、 [Web アプリケーションプロキシ](#bkmk_proxy)という、関連するネットワークアクセステクノロジを論理的にグループ化したものです。 これらのテクノロジは、リモート アクセス サーバーの役割の*役割サービス*です。 **役割と機能の追加ウィザード**または Windows PowerShell を使用してリモートアクセスサーバーの役割をインストールする場合は、これら3つの役割サービスの1つまたは複数をインストールできます。

>[!IMPORTANT]
>Microsoft Azure の仮想マシン VM にリモートアクセスをデプロイしないでください \( \) 。 Microsoft Azure でのリモートアクセスの使用はサポートされていません。 Windows Server 2016 以前のバージョンの Windows Server では、Azure VM でリモートアクセスを使用して VPN、DirectAccess、またはその他のリモートアクセス機能を展開することはできません。 詳細については、「 [Microsoft Azure の仮想マシンに対する Microsoft サーバーソフトウェアのサポート](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines)」を参照してください。

## <a name="remote-access-service-ras---ras-gateway"></a><a name="bkmk_da"></a>リモートアクセスサービス \( ras \) -ras ゲートウェイ

**DirectAccess および VPN (ras)** 役割サービスをインストールするときに、リモートアクセスサービスゲートウェイの \( **ras ゲートウェイ**を展開し \) ます。 RAS ゲートウェイは、シングルテナントの RAS ゲートウェイ仮想プライベートネットワーク \( VPN \) サーバー、マルチテナント RAS ゲートウェイ VPN サーバー、および DirectAccess サーバーとして展開できます。

- **RAS ゲートウェイ-シングルテナント**。 RAS ゲートウェイを使用すると、VPN 接続を展開して、エンドユーザーが組織のネットワークとリソースにリモートアクセスできるようにすることができます。 クライアントで Windows 10 が実行されている場合、リモートコンピューターがインターネットに接続されている場合は常に、クライアントと組織のネットワークの間に永続的な接続を維持する Always On VPN を展開できます。 RAS ゲートウェイでは、プライマリオフィスとブランチオフィスの間など、異なる場所にある2つのサーバー間にサイト間 VPN 接続を作成し、ネットワーク \( \) 内のユーザーがインターネットなどの外部リソースにアクセスできるようにネットワークアドレス変換 NAT を使用することもできます。 さらに、RAS ゲートウェイでは Border Gateway Protocol (BGP) がサポートされています。これは、リモートオフィスの場所に BGP をサポートするエッジゲートウェイもある場合に動的ルーティングサービスを提供します。

- **RAS ゲートウェイ-マルチテナント**。 Hyper-v ネットワーク仮想化を使用している場合、 \- または仮想ローカルエリアネットワーク vlan を使用してデプロイされた VM ネットワークがある場合は、マルチテナント、ソフトウェアベースのエッジゲートウェイ、およびルーターとして RAS ゲートウェイを展開でき \( \) ます。 クラウドサービスプロバイダーは、RAS ゲートウェイを使用して、 \( \) 仮想ネットワークと物理ネットワーク (インターネットを含む) の間でデータセンターとクラウドネットワークのトラフィックをルーティングできるようにします。 RAS ゲートウェイを使用すると、テナントはポイント対サイト VPN 接続を使用して、どこからでもデータセンター内の VM ネットワークリソースにアクセスできます。 テナントに、リモートサイトと CSP データセンター間のサイト間 VPN 接続を提供することもできます。 また、動的ルーティング用に BGP を使用して RAS ゲートウェイを構成できます。また、ネットワークアドレス変換 NAT を有効にして、 \( \) vm ネットワーク上の Vm にインターネットアクセスを提供できます。

>[!IMPORTANT]
> マルチテナント機能を備えた RAS ゲートウェイは、Windows Server 2012 R2 でも使用できます。

- **ALWAYS ON VPN**。 Always On VPN を使用すると、リモートユーザーは VPN に接続しなくても、内部ネットワーク上の共有リソース、イントラネット Web サイト、およびアプリケーションに安全にアクセスできます。

詳細については、「 [RAS Gateway](ras-gateway/RAS-Gateway.md) and [Border Gateway Protocol (BGP)](bgp/Border-Gateway-Protocol-BGP.md)」を参照してください。

## <a name="routing"></a><a name="bkmk_rras"></a>配線

リモートアクセスを使用して、ローカルエリアネットワーク上のサブネット間でネットワークトラフィックをルーティングすることができます。 ルーティングでは、インターネットグループ管理プロトコル (IGMP) を使用して、ネットワークアドレス変換 (NAT) ルーター、BGP を実行する LAN ルーター、ルーティング情報プロトコル (RIP)、およびマルチキャスト対応のルーターがサポートされます。 全機能を備えたルーターとして、Hyper-v を実行しているコンピューター上のサーバーコンピューターまたは仮想マシン (VM) に RAS を展開できます。

LAN ルーターとしてリモートアクセスをインストールするには、サーバーマネージャーの役割と機能の追加ウィザードを使用して、**リモートアクセス**サーバーの役割と**ルーティング**の役割サービスを選択します。または、Windows PowerShell プロンプトで次のコマンドを入力し、enter キーを押します。

```
Install-RemoteAccess -VpnType RoutingOnly
```

## <a name="web-application-proxy"></a><a name="bkmk_proxy"></a>Web アプリケーション プロキシ

Web アプリケーションプロキシは、Windows Server 2016 のリモートアクセスの役割サービスです。 Web アプリケーション プロキシには、企業ネットワーク内部の Web アプリケーション用のリバース プロキシ機能があり、ユーザーは任意のデバイスで企業ネットワーク外部から Web アプリケーションにアクセスできます。 Web アプリケーションプロキシは、Active Directory フェデレーションサービス (AD FS) (AD FS) を使用して web アプリケーションへのアクセスを事前認証し、AD FS プロキシとしても機能します。

リモートアクセスを Web アプリケーションプロキシとしてインストールするには、サーバーマネージャーの役割と機能の追加ウィザードを使用して、**リモートアクセス**サーバーの役割と**web アプリケーションプロキシ**の役割サービスを選択します。または、Windows PowerShell プロンプトで次のコマンドを入力し、enter キーを押します。

```
Install-RemoteAccess -VpnType SstpProxy
```

詳細については、「 [Web アプリケーションプロキシ](./web-application-proxy/web-application-proxy-windows-server.md)」を参照してください。


---
