---
title: DirectAccess クラスター/NLB テスト ラボのシナリオの概要
description: このトピックは、「windows Server 2016 用 Windows NLB を使用するクラスターでの DirectAccess のデモンストレーション」のテストラボガイドに含まれています。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: cd1e9efd-19e9-49e7-8432-881f661c9792
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 7394562ce7a5c08a81fb3c243fb8671d281d8370
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80819045"
---
# <a name="overview-of-the-directaccess-cluster-nlb-test-lab-scenario"></a>DirectAccess クラスター/NLB テスト ラボのシナリオの概要

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

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
  


