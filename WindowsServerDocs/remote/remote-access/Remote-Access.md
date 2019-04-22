---
title: リモート アクセス
description: このトピックでは、Windows Server 2016 でのリモート アクセス サーバーの役割の概要を示します。
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: eeca4cf7-90f0-485d-843c-76c5885c54b0
ms.author: pashort
author: shortpatti
ms.date: 05/18/2018
ms.openlocfilehash: faf12ad22678fa58ea933613759e3e8414966bca
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818363"
---
# <a name="remote-access"></a>リモート アクセス

>適用先:Windows Server 2016、Windows Server 2012 R2、Windows 10 の Windows Server (半期チャネル)

リモート アクセス ガイドでは、Windows Server 2016 でのリモート アクセス サーバーの役割の概要を提供し、次の項目について説明します。

- [Always On VPN 展開ガイド](vpn/always-on-vpn/deploy/always-on-vpn-deploy.md)
- [ボーダー ゲートウェイ プロトコル&#40;BGP&#41;](bgp/Border-Gateway-Protocol-BGP.md)
- [RAS ゲートウェイ](ras-gateway/RAS-Gateway.md) 
- [リモート アクセス サーバーの役割のドキュメント](ras/Remote-Access-Server-Role-Documentation.md)
- [SDN の RAS ゲートウェイ](../../networking/sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)
- [仮想プライベート ネットワーク (VPN)](vpn/vpn-top.md)
 
その他のネットワーク テクノロジの詳細については、次を参照してください。 [Windows Server 2016 でのネットワー キング](https://docs.microsoft.com/windows-server/networking/networking)します。

リモート アクセス サーバーの役割は、これらの関連するネットワーク アクセス テクノロジの論理的なグループを示します。[リモート アクセス サービス (RAS)](#bkmk_da)、[ルーティング](#bkmk_rras)、および[Web アプリケーション プロキシ](#bkmk_proxy)します。 これらのテクノロジは、リモート アクセス サーバーの役割の*役割サービス*です。 リモート アクセス サーバーの役割をインストールすると、**追加の役割と機能ウィザード**または Windows PowerShell では、これらの 3 つの役割サービスの 1 つ以上をインストールできます。

>[!IMPORTANT]
>仮想マシンにリモート アクセスの展開をしないで\(VM\) Microsoft Azure でします。 Microsoft Azure でのリモート アクセスの使用はサポートされていません。 Azure VM でリモート アクセスを使用して、VPN、DirectAccess、または Windows Server 2016 または Windows Server の以前のバージョンでその他のリモート アクセス機能をデプロイすることはできません。 詳細については、次を参照してください。 [Microsoft Azure 仮想マシンのマイクロソフト サーバー ソフトウェア サポート](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines)します。

## <a name="bkmk_da"></a>リモート アクセス サービス\(RAS\) -RAS ゲートウェイ

インストールするときに、 **DirectAccess と VPN (RAS)** 役割サービス、リモート アクセス サービスのゲートウェイを展開する\( **RAS ゲートウェイ**\)します。 RAS ゲートウェイの 1 つのテナント RAS ゲートウェイの仮想プライベート ネットワークをデプロイする\(VPN\)サーバー、マルチ テナントの RAS ゲートウェイの VPN サーバー、および DirectAccess サーバーとして。

- **RAS ゲートウェイの 1 つのテナント**します。 RAS ゲートウェイを使用して、組織のネットワークおよびリソースへのリモート アクセスでエンドユーザーに提供する VPN 接続を展開できます。 クライアントが Windows 10 を実行している場合は、Always On VPN、リモート コンピューターがインターネットに接続するたびに、クライアントと、組織のネットワークの間で永続的な接続を維持するを展開できます。 RAS ゲートウェイを使用しても、プライマリ オフィスとブランチ オフィス間など、異なる場所にある 2 つのサーバー間のサイト対サイト VPN 接続を作成およびネットワーク アドレス変換を使用することができます\(NAT\)ように内部のユーザー、ネットワークは、インターネットなどの外部リソースにアクセスできます。 さらに、RAS ゲートウェイでは、リモート オフィスの場所では、BGP をサポートするエッジ ゲートウェイもがある場合は、動的ルーティング サービスを提供するボーダー ゲートウェイ プロトコル (BGP) をサポートしています。

- **RAS ゲートウェイのマルチ テナント**します。 ハイパースレッディングを使用している場合は、マルチ テナント、ソフトウェア ベースのエッジ ゲートウェイおよびルーターとして RAS ゲートウェイを展開できます\-仮想ローカル エリア ネットワークにデプロイされた VM ネットワークがあるか、ネットワーク仮想化\(Vlan\)します。 RAS ゲートウェイ、クラウド サービス プロバイダーと\(Csp\)企業はデータ センターを有効にして、インターネットを含む、仮想および物理ネットワーク間のネットワーク トラフィックのルーティングをクラウドとします。 RAS ゲートウェイを使用して、テナントは、どこからでも、データ センター内の VM ネットワークのリソースにアクセスするのにポイントようにサイト VPN 接続を使用できます。 そのリモート サイトと CSP のデータ センター間のサイト対サイト VPN 接続でテナントを指定することもできます。 さらに、BGP で RAS ゲートウェイを構成するには、動的ルーティング用と、ネットワーク アドレス変換を有効にすることができます\(NAT\)に VM ネットワークで Vm のインターネット アクセスを提供します。

>[!IMPORTANT]
> マルチ テナント機能を備えた RAS ゲートウェイも Windows Server 2012 R2 で使用できます。

- **Always On VPN**します。 Always On VPN には、リモート ユーザーが VPN に接続しなくても、共有リソース、イントラネット Web サイト、および内部ネットワーク上でアプリケーションを安全にアクセスができるようにします。 

詳細については、次を参照してください。 [RAS ゲートウェイ](ras-gateway/RAS-Gateway.md)と[ボーダー ゲートウェイ プロトコル (BGP)](bgp/Border-Gateway-Protocol-BGP.md)します。

## <a name="bkmk_rras"></a>ルーティング

リモート アクセスを使用して、ローカル エリア ネットワーク上のサブネット間のネットワーク トラフィックをルーティングすることができます。 ルーティングでは、ネットワーク アドレス変換 (NAT) ルーター、BGP ルーティング情報プロトコル (RIP) やインターネット グループ管理プロトコル (IGMP) を使用してマルチキャスト対応のルーターを実行している LAN ルーターのサポートを提供します。 フル装備のルーターでは、サーバー コンピューターまたは HYPER-V を実行しているコンピューター上の仮想マシン (VM) として RAS をデプロイできます。

サーバー マネージャーで、追加の役割と機能ウィザードを使用していずれかの LAN ルーターとしてリモート アクセスをインストールして、選択、**リモート アクセス**サーバー ロールおよび**ルーティング**役割サービスですまたは、次の種類。Windows PowerShell プロンプトでコマンドし、し、ENTER キーを押します。

```  
Install-RemoteAccess -VpnType RoutingOnly
```  

## <a name="bkmk_proxy"></a>Web アプリケーション プロキシ

Web アプリケーション プロキシとは、Windows Server 2016 でのリモート アクセス役割サービスです。 Web アプリケーション プロキシには、企業ネットワーク内部の Web アプリケーション用のリバース プロキシ機能があり、ユーザーは任意のデバイスで企業ネットワーク外部から Web アプリケーションにアクセスできます。 Web アプリケーション プロキシは、Active Directory フェデレーション サービス (AD FS) を使用して web アプリケーションへのアクセスを事前に認証し、AD FS プロキシとしても機能します。

サーバー マネージャーで、追加の役割と機能ウィザードを使用していずれかの Web アプリケーション プロキシとしてリモート アクセスをインストールして、選択、**リモート アクセス**サーバー ロールおよび**Web アプリケーション プロキシ**; の役割サービスまたはWindows PowerShell プロンプトで次のコマンドを入力し、ENTER キーを押します。  

```  
Install-RemoteAccess -VpnType SstpProxy  
```  

詳細については、次を参照してください。 [Web アプリケーション プロキシ](https://technet.microsoft.com/windows-server-docs/identity/web-application-proxy/web-application-proxy-windows-server)します。


---