---
title: SDN の RAS ゲートウェイ
description: このトピックでは、Windows Server 2016 のソフトウェアベース、マルチテナント、Border Gateway Protocol (BGP) 対応ルーターである RAS ゲートウェイについて説明します。
manager: grcusanz
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: article
ms.assetid: a32357a5-ab1a-4a4c-848a-7a4ed65b1921
ms.author: anpaul
author: AnirbanPaul
ms.openlocfilehash: 3059da769e8ab5719be657c82d3f075a686f6691
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859595"
---
# <a name="ras-gateway-for-sdn"></a>SDN の RAS ゲートウェイ

>適用対象: Windows Server (半期チャネル)、Windows Server 2016 # # SDN 用 RAS ゲートウェイ  


RAS ゲートウェイは、クラウドサービスプロバイダー (Csp) および Hyper-v ネットワーク仮想化を使用して複数のテナント仮想ネットワークをホストする企業向けに設計された、ソフトウェアベースのマルチテナントの Border Gateway Protocol (BGP) 対応ルーターです。 RAS ゲートウェイは、場所に関係なく、物理ネットワークと VM ネットワークリソース間のネットワークトラフィックをルーティングします。 ネットワークトラフィックは、同じ物理的な場所またはさまざまな場所でルーティングできます。   

マルチテナント機能は、複数のテナントの仮想マシンワークロードをサポートするクラウドインフラストラクチャの機能であり、すべてのワークロードが同じインフラストラクチャ上で実行されている間は相互に分離されています。 個別のテナントの複数のワークロードは相互接続でき、リモートで管理できますが、これらのシステムが他のテナントのワークロードと相互接続したり、他のテナントがこれらをリモートで管理したりすることはできません。

  
> [!NOTE]  
> このトピックに加えて、次の RAS ゲートウェイのトピックも参照してください。  
>   
> -   [RAS ゲートウェイの新機能](../../../sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md)  
> -   [RAS ゲートウェイの展開アーキテクチャ](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-Deployment-Architecture.md)  
> -   [RAS ゲートウェイの高可用性](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-High-Availability.md)  
> -   [Border Gateway Protocol &#40;BGP&#41;](../../../../remote/remote-access/bgp/Border-Gateway-Protocol-BGP.md)  
> -   [BGP Windows PowerShell コマンド リファレンス](../../../../remote/remote-access/bgp/BGP-Windows-PowerShell-Command-Reference.md)  
  
    
## <a name="prerequisites-for-installing-ras-gateway-for-sdn"></a>SDN 用 RAS ゲートウェイをインストールするための前提条件  
SDN で使用するために RAS ゲートウェイをマルチテナントモードで展開する場合は、Windows インターフェイスを使用してリモートアクセスをインストールすることはできません。 代わりに、Windows PowerShell を使用する必要があります。  
  
ただし、Windows PowerShell を使用して RAS ゲートウェイをインストールするには、Windows PowerShell を使用して、 **RemoteAccess** windows 機能を追加する必要があります。 これを行うには、Windows PowerShell プロンプトで次のコマンドを実行します。  
  
`Add-WindowsFeature -Name RemoteAccess -IncludeAllSubFeature -IncludeManagementTools`  
  
このコマンドでは、機能の**RemoteAccess**機能と Windows PowerShell コマンドを追加します。  
  
サーバーに**RemoteAccess**を追加した後、リモートアクセスをマルチテナントモードと BORDER GATEWAY PROTOCOL (BGP) を使用した RAS ゲートウェイとしてインストールできます。  
  
詳細については、Windows PowerShell のリファレンストピック「 [Install-RemoteAccess](https://technet.microsoft.com/library/hh918408.aspx)」を参照してください。  
  
## <a name="ras-gateway-features"></a>RAS ゲートウェイの機能  
Windows Server 2016 の RAS ゲートウェイの機能を次に示します。 これらすべての機能を一度に使用する高可用性プールに RAS ゲートウェイを展開できます。  
  
-   **サイト間 VPN**。 この RAS ゲートウェイ機能を使用すると、サイト間 VPN 接続を使用して、インターネット経由で異なる物理的な場所にある2つのネットワークを接続することができます。 データセンター内の多数のテナントをホストする Csp の場合、RAS ゲートウェイはマルチテナントゲートウェイソリューションを提供します。これにより、テナントはリモートサイトからのサイト間 VPN 接続を介してリソースにアクセスして管理できるようになり、ネットワークトラフィックフローが可能になります。データセンターとその物理ネットワーク内の仮想リソース。  
  
-   **ポイント対サイト VPN**。 この RAS ゲートウェイ機能を使用すると、組織の従業員または管理者は、リモートの場所から組織のネットワークに接続できます。  マルチテナント展開の場合、テナントネットワーク管理者は、ポイント対サイト VPN 接続を使用して、CSP データセンターの仮想ネットワークリソースにアクセスできます。  
  
-   **GRE トンネリング**。 汎用ルーティングカプセル化 (GRE) ベースのトンネルにより、テナント仮想ネットワークと外部ネットワーク間の接続が可能になります。 GRE プロトコルは軽量であるため、GRE のサポートはほとんどのネットワーク デバイスで利用でき、データの暗号化を必要としないトンネリングに最適な選択肢です。 サイト間 (S2S) トンネルの GRE サポートは、このトピックで後述するように、マルチテナントゲートウェイを使用して、テナント仮想ネットワークとテナント外部ネットワーク間の転送の問題を解決します。  
  
-   **Border Gateway Protocol (BGP) を使用した動的ルーティング**。 BGP を使用するとルーター上で手動でルートを構成する必要性が減ります。それは、BGP が動的ルーティング プロトコルであり、サイト間 VPN 接続を使用して接続されているサイト間のルートが自動的に学習されるためです。 RAS ゲートウェイなどの BGP 対応ルーターを使用して接続されている複数のサイトが組織にある場合、BGP では、ネットワークの中断や障害が発生した場合に、ルーターが有効なルートを自動的に計算して使用することができます。 詳細については、 [RFC 4271](https://tools.ietf.org/html/rfc4271)を参照してください。  
  

  


