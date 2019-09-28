---
title: リモート アクセス
description: このトピックでは、Windows Server 2016 のリモートアクセスサーバーの役割の概要について説明します。
manager: dougkim
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: eeca4cf7-90f0-485d-843c-76c5885c54b0
ms.author: pashort
author: shortpatti
ms.date: 05/18/2018
ms.openlocfilehash: d2fa9c82c4cab05b2a60916fee3f09c1ea48a472
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71388913"
---
# <a name="remote-access"></a>リモート アクセス

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows 10

リモートアクセスガイドでは、Windows Server 2016 のリモートアクセスサーバーの役割の概要について説明し、次の項目について説明します。

- [Always On VPN 展開ガイド](vpn/always-on-vpn/deploy/always-on-vpn-deploy.md)
- [Border Gateway Protocol &#40;BGP&#41;](bgp/Border-Gateway-Protocol-BGP.md)
- [RAS ゲートウェイ](ras-gateway/RAS-Gateway.md) 
- [リモート アクセス サーバーの役割のドキュメント](ras/Remote-Access-Server-Role-Documentation.md)
- [SDN の RAS ゲートウェイ](../../networking/sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)
- [仮想プライベート ネットワーク (VPN)](vpn/vpn-top.md)
 
その他のネットワークテクノロジの詳細については、「 [Windows Server 2016 のネットワーク](https://docs.microsoft.com/windows-server/networking/networking)」を参照してください。

リモートアクセスサーバーの役割は、次の関連するネットワークアクセステクノロジを論理的にグループ化したものです。[リモートアクセスサービス (RAS)](#bkmk_da)、[ルーティング](#bkmk_rras)、および[Web アプリケーションプロキシ](#bkmk_proxy)。 これらのテクノロジは、リモート アクセス サーバーの役割の*役割サービス*です。 **役割と機能の追加ウィザード**または Windows PowerShell を使用してリモートアクセスサーバーの役割をインストールする場合は、これら3つの役割サービスの1つまたは複数をインストールできます。

>[!IMPORTANT]
>Microsoft Azure では、仮想マシン \(VM @ no__t-1 にリモートアクセスを展開しないでください。 Microsoft Azure でのリモートアクセスの使用はサポートされていません。 Windows Server 2016 以前のバージョンの Windows Server では、Azure VM でリモートアクセスを使用して VPN、DirectAccess、またはその他のリモートアクセス機能を展開することはできません。 詳細については、「 [Microsoft Azure の仮想マシンに対する Microsoft サーバーソフトウェアのサポート](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines)」を参照してください。

## <a name="bkmk_da"></a>リモートアクセスサービス \( RAS @ no__t-RAS ゲートウェイ

**DirectAccess および VPN (RAS)** 役割サービスをインストールするときに、リモートアクセスサービスゲートウェイ \(**RAS ゲートウェイ**@no__t 展開します。 RAS ゲートウェイは、シングルテナントの RAS ゲートウェイ仮想プライベートネットワーク @no__t 0VPN @ no__t サーバー、マルチテナント RAS ゲートウェイ VPN サーバー、および DirectAccess サーバーとして展開できます。

- **RAS ゲートウェイ-シングルテナント**。 RAS ゲートウェイを使用すると、VPN 接続を展開して、エンドユーザーが組織のネットワークとリソースにリモートアクセスできるようにすることができます。 クライアントで Windows 10 が実行されている場合、リモートコンピューターがインターネットに接続されている場合は常に、クライアントと組織のネットワークの間に永続的な接続を維持する Always On VPN を展開できます。 RAS ゲートウェイを使用すると、プライマリオフィスとブランチオフィスの間など、異なる場所にある2つのサーバー間にサイト間 VPN 接続を作成し、ネットワーク内のユーザーがネットワーク内のユーザーがネットワークアドレス変換 \(NAT @ no__t-1 を使用できるようにすることもできます。インターネットなどの外部リソースにアクセスします。 さらに、RAS ゲートウェイでは Border Gateway Protocol (BGP) がサポートされています。これは、リモートオフィスの場所に BGP をサポートするエッジゲートウェイもある場合に動的ルーティングサービスを提供します。

- **RAS ゲートウェイ-マルチテナント**。 Hyper-v ネットワーク仮想化を使用している場合、または仮想ローカルエリアネットワークを使用してデプロイされた VM ネットワーク \(VLANs @ no__t がある場合は、マルチテナント、ソフトウェアベースのエッジゲートウェイ、およびルーターとして RAS ゲートウェイを展開できます。 RAS ゲートウェイを使用すると、クラウドサービスプロバイダーは @no__t 0CSPs @ no__t と企業が、仮想ネットワークと物理ネットワーク (インターネットを含む) の間でデータセンターとクラウドネットワークのトラフィックをルーティングできるようになります。 RAS ゲートウェイを使用すると、テナントはポイント対サイト VPN 接続を使用して、どこからでもデータセンター内の VM ネットワークリソースにアクセスできます。 テナントに、リモートサイトと CSP データセンター間のサイト間 VPN 接続を提供することもできます。 また、動的ルーティング用の BGP を使用して RAS ゲートウェイを構成できます。また、ネットワークアドレス変換 \(NAT @ no__t-1 を有効にして、VM ネットワーク上の Vm にインターネットアクセスを提供できます。

>[!IMPORTANT]
> マルチテナント機能を備えた RAS ゲートウェイは、Windows Server 2012 R2 でも使用できます。

- **ALWAYS ON VPN**。 Always On VPN を使用すると、リモートユーザーは VPN に接続しなくても、内部ネットワーク上の共有リソース、イントラネット Web サイト、およびアプリケーションに安全にアクセスできます。 

詳細については、「 [RAS Gateway](ras-gateway/RAS-Gateway.md) and [Border Gateway Protocol (BGP)](bgp/Border-Gateway-Protocol-BGP.md)」を参照してください。

## <a name="bkmk_rras"></a>配線

リモートアクセスを使用して、ローカルエリアネットワーク上のサブネット間でネットワークトラフィックをルーティングすることができます。 ルーティングでは、インターネットグループ管理プロトコル (IGMP) を使用して、ネットワークアドレス変換 (NAT) ルーター、BGP を実行する LAN ルーター、ルーティング情報プロトコル (RIP)、およびマルチキャスト対応のルーターがサポートされます。 全機能を備えたルーターとして、Hyper-v を実行しているコンピューター上のサーバーコンピューターまたは仮想マシン (VM) に RAS を展開できます。

LAN ルーターとしてリモートアクセスをインストールするには、サーバーマネージャーの役割と機能の追加ウィザードを使用して、**リモートアクセス**サーバーの役割と**ルーティング**の役割サービスを選択します。または、Windows PowerShell プロンプトで次のコマンドを入力し、enter キーを押します。

```  
Install-RemoteAccess -VpnType RoutingOnly
```  

## <a name="bkmk_proxy"></a>Web アプリケーションプロキシ

Web アプリケーションプロキシは、Windows Server 2016 のリモートアクセスの役割サービスです。 Web アプリケーション プロキシには、企業ネットワーク内部の Web アプリケーション用のリバース プロキシ機能があり、ユーザーは任意のデバイスで企業ネットワーク外部から Web アプリケーションにアクセスできます。 Web アプリケーションプロキシは、Active Directory フェデレーションサービス (AD FS) (AD FS) を使用して web アプリケーションへのアクセスを事前認証し、AD FS プロキシとしても機能します。

リモートアクセスを Web アプリケーションプロキシとしてインストールするには、サーバーマネージャーの役割と機能の追加ウィザードを使用して、**リモートアクセス**サーバーの役割と**web アプリケーションプロキシ**の役割サービスを選択します。または、Windows PowerShell プロンプトで次のコマンドを入力し、enter キーを押します。  

```  
Install-RemoteAccess -VpnType SstpProxy  
```  

詳細については、「 [Web アプリケーションプロキシ](https://technet.microsoft.com/windows-server-docs/identity/web-application-proxy/web-application-proxy-windows-server)」を参照してください。


---