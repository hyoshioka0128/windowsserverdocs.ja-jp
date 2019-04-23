---
title: SDN の RAS ゲートウェイ
description: このトピックを使用すると、マルチ テナントとボーダー ゲートウェイ プロトコル (BGP) Windows Server 2016 での対応のルーターにはソフトウェア ベースで、RAS ゲートウェイについて説明します。
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
ms.openlocfilehash: 4f1ad0b3f0b5921a53faa8a45baae9f0b8711873
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856273"
---
# <a name="ras-gateway-for-sdn"></a>SDN の RAS ゲートウェイ

>適用対象:Windows Server (半期チャネル) SDN の Windows Server 2016 ## RAS ゲートウェイ  


RAS ゲートウェイはソフトウェア ベースのマルチ テナント、ボーダー ゲートウェイ プロトコル (BGP) 対応のルーター用に設計されたクラウド サービス プロバイダー (Csp) や企業をホストする複数のテナント仮想ネットワークが、HYPER-V ネットワーク仮想化を使用します。 RAS ゲートウェイは、場所に関係なく、物理ネットワークと VM ネットワークのリソースの間のネットワーク トラフィックをルーティングします。 物理的に同じ場所またはさまざまな場所でネットワーク トラフィックをルーティングすることができます。   

マルチ テナント機能は、複数のテナントの仮想マシンのワークロードをサポートするには、まだそれらを分離、その他のすべてのワークロードを同じインフラストラクチャで実行中にクラウド インフラストラクチャの機能です。 個別のテナントの複数のワークロードは相互接続でき、リモートで管理できますが、これらのシステムが他のテナントのワークロードと相互接続したり、他のテナントがこれらをリモートで管理したりすることはできません。

  
> [!NOTE]  
> このトピックに加え、次のトピックの RAS ゲートウェイを利用できます。  
>   
> -   [RAS ゲートウェイの新機能新機能](../../../sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md)  
> -   [RAS ゲートウェイ展開アーキテクチャ](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-Deployment-Architecture.md)  
> -   [RAS ゲートウェイの高可用性](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-High-Availability.md)  
> -   [ボーダー ゲートウェイ プロトコル&#40;BGP&#41;](../../../../remote/remote-access/bgp/Border-Gateway-Protocol-BGP.md)  
> -   [BGP Windows PowerShell コマンド リファレンス](../../../../remote/remote-access/bgp/BGP-Windows-PowerShell-Command-Reference.md)  
  
    
## <a name="prerequisites-for-installing-ras-gateway-for-sdn"></a>SDN の RAS ゲートウェイをインストールするための前提条件  
Windows インターフェイスを使用して SDN で使用するためのマルチ テナント モードで RAS ゲートウェイを展開するときに、リモート アクセスをインストールすることはできません。 代わりに、Windows PowerShell を使用する必要があります。  
  
RAS ゲートウェイをインストールするには、Windows PowerShell を使用して、前に追加する Windows PowerShell を使用する必要がありますが、 **RemoteAccess** Windows の機能です。 これを行うには、Windows PowerShell プロンプトで次のコマンドを実行します。  
  
`Add-WindowsFeature -Name RemoteAccess -IncludeAllSubFeature -IncludeManagementTools`  
  
このコマンドを追加、 **RemoteAccess**機能と機能の Windows PowerShell コマンド。  
  
追加した後**RemoteAccess**をサーバーには、マルチ テナント モードでは、RAS ゲートウェイとボーダー ゲートウェイ プロトコル (BGP) とリモート アクセスをインストールできます。  
  
詳細については、Windows PowerShell のリファレンス トピックを参照してください。 [Install-remoteaccess](https://technet.microsoft.com/library/hh918408.aspx)します。  
  
## <a name="ras-gateway-features"></a>RAS ゲートウェイの機能  
Windows Server 2016 で RAS ゲートウェイの機能を次に示します。 これらすべての機能を同時に使用する高可用性プール RAS ゲートウェイをデプロイできます。  
  
-   **サイト対サイト VPN**します。 この RAS ゲートウェイの機能を使用すると、サイト対サイト VPN 接続を使用して、インターネット経由で物理的に異なる場所にある 2 つのネットワークを接続できます。 RAS ゲートウェイはデータ センターで複数のテナントをホストする csp の場合にアクセスしてリモート サイトからサイト対サイト VPN 接続経由でそのリソースを管理するテナントを使用して、間のネットワーク トラフィック フローを許可するマルチ テナント ゲートウェイ ソリューションを提供しますデータ センターと物理ネットワーク内の仮想リソース。  
  
-   **ポイント対サイト VPN**します。 この RAS ゲートウェイの機能は、リモートの場所から、組織のネットワークに接続するには、組織の従業員または管理者を使用できます。  マルチ テナント展開では、テナント ネットワーク管理者は、CSP データ センターで仮想ネットワーク リソースにアクセスするのにポイント対サイト VPN 接続を使用することができます。  
  
-   **GRE トンネリング**します。 Generic Routing Encapsulation (GRE) ベースのテナントの仮想ネットワークと外部ネットワーク間のトンネル有効にする接続。 GRE プロトコルは軽量であるため、GRE のサポートはほとんどのネットワーク デバイスで利用でき、データの暗号化を必要としないトンネリングに最適な選択肢です。 サイト間 (S2S) トンネルで GRE がサポートは、このトピックの後半の説明に従って、テナントの仮想ネットワークと、マルチ テナント ゲートウェイを使用してテナントの外部ネットワーク間の転送の問題を解決します。  
  
-   **ボーダー ゲートウェイ プロトコル (BGP) を動的にルーティング**します。 BGP を使用するとルーター上で手動でルートを構成する必要性が減ります。それは、BGP が動的ルーティング プロトコルであり、サイト間 VPN 接続を使用して接続されているサイト間のルートが自動的に学習されるためです。 お客様の組織は、RAS ゲートウェイなどの BGP 対応ルーターを使用して接続されている複数のサイトがある、自動的に計算し、相互にネットワークの中断または障害が発生した場合の有効なルートを使用するようにルーターを BGP ができます。 詳細については、次を参照してください。 [RFC 4271](https://tools.ietf.org/html/rfc4271)します。  
  

  


