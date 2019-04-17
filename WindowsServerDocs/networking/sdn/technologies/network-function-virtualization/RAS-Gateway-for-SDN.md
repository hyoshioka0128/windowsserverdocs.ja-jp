---
title: SDN の RAS ゲートウェイ
description: このトピックを使用すると、マルチテナントとボーダー ゲートウェイ プロトコル (BGP) Windows Server 2016 での対応のルーターは、RAS ゲートウェイは、ソフトウェア ベース、について説明します。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a32357a5-ab1a-4a4c-848a-7a4ed65b1921
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 052911dcd52df82ef4e259de0c64078c54f00195
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="ras-gateway-for-sdn"></a>SDN の RAS ゲートウェイ

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

については、ソフトウェア ベース、マルチテナント、ボーダー ゲートウェイ プロトコル (BGP) 対応のルーターはクラウド サービス プロバイダー (CSP) や Hyper-V ネットワーク仮想化を使用して複数のテナント仮想ネットワークをホストしているエンタープライズ向けに設計された Windows Server 2016 では、RAS ゲートウェイは、このトピックを使用することができます。  
  
> [!NOTE]  
> このトピックに加え、次のトピックの RAS ゲートウェイを利用できます。  
>   
> -   [RAS ゲートウェイの新機能](../../../sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md)  
> -   [RAS ゲートウェイ展開アーキテクチャ](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-Deployment-Architecture.md)  
> -   [RAS ゲートウェイの高可用性](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-High-Availability.md)  
> -   [ボーダー ゲートウェイ プロトコル (&) #40 です。BGP & #41 です。](../../../../remote/remote-access/bgp/Border-Gateway-Protocol-BGP.md)  
> -   [BGP Windows PowerShell コマンド リファレンス](../../../../remote/remote-access/bgp/BGP-Windows-PowerShell-Command-Reference.md)  
  
Windows Server 2016 では、RAS ゲートウェイは、リソースがある場所に関係なく、VM ネットワーク リソースと物理ネットワーク間のネットワーク トラフィックをルーティングします。 RAS ゲートウェイを使用して、物理ネットワークと仮想ネットワークまたはインターネット経由でさまざまな異なる物理的な場所に物理的に同じ場所にある間のネットワーク トラフィックをルーティングすることができます。  
  
マルチテナント機能は、複数のテナントの仮想マシンのワークロードをサポートするには、まだそれを切り分ける、その他のすべてのワークロードが同じインフラストラクチャで実行中のクラウド インフラストラクチャの機能です。 個々 のテナントの複数のワークロードを相互接続できますリモートで管理するが、これらのシステムでは、他のテナントのワークロードで相互に通信はしないしたり他のテナント リモートで管理できます。  
  
## <a name="prerequisites-for-installing-ras-gateway-for-sdn"></a>SDN の RAS ゲートウェイをインストールするための前提条件  
Windows インターフェイスを使用して、SDN で使用するためのマルチテナント モードで RAS ゲートウェイを展開するときに、リモート アクセスをインストールすることはできません。 代わりに、Windows PowerShell を使用する必要があります。  
  
RAS ゲートウェイをインストールするには、Windows PowerShell を使用して、前に追加する Windows PowerShell を使用する必要がありますが、**RemoteAccess** Windows の機能です。 これを行うには、Windows PowerShell プロンプトで次のコマンドを実行します。  
  
`Add-WindowsFeature -Name RemoteAccess -IncludeAllSubFeature -IncludeManagementTools`  
  
このコマンドを追加、**RemoteAccess**機能と機能の Windows PowerShell コマンド。  
  
追加した後**RemoteAccess**、サーバーに、マルチテナント モードで RAS ゲートウェイとボーダー ゲートウェイ プロトコル (BGP) としてリモート アクセスをインストールすることができます。  
  
詳細については、Windows PowerShell リファレンスのトピックを参照してください。[Install-remoteaccess](https://technet.microsoft.com/library/hh918408.aspx)します。  
  
## <a name="ras-gateway-features"></a>RAS ゲートウェイの機能  
Windows Server 2016 での RAS ゲートウェイの機能を次に示します。 これらの機能すべてを一度に 1 つを使用する高可用性プールの RAS ゲートウェイを展開することができます。  
  
-   **サイト間 VPN**します。 この RAS ゲートウェイの機能では、サイト間 VPN 接続を使用して、インターネット経由で別の物理的な場所にある 2 つのネットワークに接続することができます。 データ センターで複数のテナントをホストする CSP の場合は、RAS ゲートウェイはマルチテナント ゲートウェイ ソリューションへのアクセスし、リモートのサイトからサイト間 VPN 接続経由で、リソースを管理するテナントを使用して、データ センター内の仮想リソースとテナントの物理ネットワーク間のネットワーク トラフィック フローをことができますを提供します。  
  
-   **ポイント ツー サイト VPN**します。 この RAS ゲートウェイの機能では、リモートの場所から組織のネットワークに接続するには、組織の従業員または管理者を使用します。  マルチテナント展開の場合、テナントのネットワーク管理者は、CSP データ センターの仮想ネットワーク リソースにアクセス ポイント ツー サイト VPN 接続を使用できます。  
  
-   **GRE トンネリング**します。 汎用ルーティング カプセル化(GRE) ベースのテナントの仮想ネットワークと外部ネットワーク間トンネル接続が可能にします。 GRE プロトコルは、軽量で、サポートは GRE はほとんどのネットワーク デバイスで利用可能なためデータの暗号化は必要ありませんトンネリングに最適なソリューションになります。 サイト間 (S2S) トンネルの GRE サポートは、このトピックで後述するように、テナントの仮想ネットワークと、マルチテナント ゲートウェイを使用して、テナントの外部ネットワーク間の転送の問題を解決します。  
  
-   **ボーダー ゲートウェイ プロトコル (BGP) を動的にルーティング**します。 BGP は、動的ルーティング プロトコルであり、サイト間 VPN 接続を使用して接続されているサイト間のルートが自動的に学習ためルーターを手動でルート構成の必要性が削減されます。 組織になど RAS ゲートウェイの BGP 対応ルーターを使用して接続されている複数のサイトがある場合は、自動的に計算して互いにネットワーク接続の中断またはエラーが発生した場合の有効なルートを使用するようにルーターが、BGP できます。 詳細については、次を参照してください。[RFC 4271](https://tools.ietf.org/html/rfc4271)します。  
  

  


