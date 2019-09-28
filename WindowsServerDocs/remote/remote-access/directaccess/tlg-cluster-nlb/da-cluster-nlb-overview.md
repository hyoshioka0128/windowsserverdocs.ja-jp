---
title: DirectAccess クラスター/NLB テスト ラボのシナリオの概要
description: このトピックは、「windows Server 2016 用 Windows NLB を使用するクラスターでの DirectAccess のデモンストレーション」のテストラボガイドに含まれています。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cd1e9efd-19e9-49e7-8432-881f661c9792
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 487b85713d415cdda9ee40548091abdb5fe7fc2e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404832"
---
# <a name="overview-of-the-directaccess-cluster-nlb-test-lab-scenario"></a>DirectAccess クラスター/NLB テスト ラボのシナリオの概要

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このテスト ラボのシナリオでは、DirectAccess に展開されます。  
  
-   **DC1**- ドメイン コント ローラーとして構成されているサーバー、ドメイン ネーム システム (DNS) サーバー、および動的ホスト構成プロトコル (DHCP) サーバー。  
  
-   **EDGE1**- リモート アクセス サーバー クラスター内の最初のリモート アクセス サーバーとして構成されている内部ネットワーク上のサーバーです。 このサーバーには 2 つのネットワーク アダプターです。内部ネットワークに接続されているいずれかと、外部ネットワークに接続されている他のです。  
  
-   **EDGE2**- リモート アクセス サーバー クラスター内の 2 つ目のリモート アクセス サーバーとして構成されている内部ネットワーク上のサーバーです。 このサーバーには 2 つのネットワーク アダプターです。内部ネットワークに接続されているいずれかと、外部ネットワークに接続されている他のです。  
  
-   **APP1**- web サービスとファイル サーバー、およびエンタープライズ ルート証明機関 (CA) として構成されている内部ネットワーク上のサーバー  
  
-   **APP2**- IPv4 のみ web サービスとファイル サーバーとして構成されている内部ネットワーク上のコンピューターです。 このコンピューターは、nat64/dns64 機能を強調表示に使用されます。  
  
-   **INET1**- インターネット DNS と DHCP サーバーとして構成されているサーバーです。  
  
-   **NAT1**のインターネット接続の共有を使用して、ネットワーク アドレス変換器 (NAT) デバイスとして構成されているクライアント コンピューター。  
  
-   **CLIENT1**- 内部のネットワーク、シミュレートされたインターネットやホーム ネットワーク間を移動するときに、DirectAccess の接続をテストするために使用する DirectAccess クライアントとして構成されているクライアント コンピューター。  
  
テスト ラボは、次をシミュレートする 3 つのサブネットで構成されます。  
  
-   NAT でインターネットに接続されているホームネット (192.168.137.0/24) という名前のホーム ネットワーク  
  
-   インターネット サブネット (131.107.0.0/24) によって表される外部ネットワークです。  
  
-   Corpnet という名前の内部ネットワーク (10.0.0.0/24; 2001:db8:1::/64) リモート アクセス サーバーによって、インターネットから分離します。  
  
各サブネット上のコンピューターは、次の図に示すように、物理または仮想ハブまたはスイッチを使用して接続します。  
  
![テスト ラボの概要](../../../media/Overview-of-the-Test-Lab-Scenario_5/TLG_DA_Cluster.png)  
  


