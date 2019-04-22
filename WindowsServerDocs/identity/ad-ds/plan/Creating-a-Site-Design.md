---
ms.assetid: 83f746e5-81db-4610-9977-1d5c57699f50
title: サイト設計の作成
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: f6d896213708f8c3ec5de44a1f85fb4ebd86b8c0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819073"
---
# <a name="creating-a-site-design"></a>サイト設計の作成

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

サイトの設計を作成するには、サイトにするどの場所を決定する、サイト オブジェクトを作成する、サブネット オブジェクトを作成する、およびサイトとサブネットの関連付けが含まれます。  
  
## <a name="deciding-which-locations-will-become-sites"></a>サイトにする場所を決定します。

次のようにサイトを作成する場所を決定します。  
  
- ドメイン コント ローラーを配置するすべての場所のサイトを作成します。 ドメイン コント ローラーが含まれている場所を識別するために、「ドメイン コント ローラー配置」(DSSTOPO_4.doc) ワークシートに記載されている情報を参照してください。  
- サイトの作成を必要とするアプリケーションを実行しているサーバーを含む場所に対してサイトを作成します。 など分散ファイル システム名前空間 (DFSN)、特定のアプリケーションでは、サイト オブジェクトを使用して、クライアントに最も近いサーバーを探します。  

   > [!NOTE]  
   > 高速で信頼性の高い接続での近接の組織に複数のネットワークした場合、1 つの Active Directory サイトでこれらのネットワークのサブネットのすべてを含めることができます。 たとえば、ラウンドト リップの戻り値が異なる 2 つのサーバー間の待機時間をネットワーク サブネットが 10 ミリ秒か、以下の場合、同じ Active Directory サイトで両方のサブネットを含めることができます。 2 つの場所間のネットワーク待機時間が 10 ミリ秒よりも大きい場合は、1 つの Active Directory サイト内のサブネットを含めないでください。 でもと待機時間は 10 ミリ秒または以下の場合、Active Directory ベースのアプリケーション用にサイト間のトラフィックを分割する場合は、個別のサイトをデプロイすることもできます。  

- サイトでの場所に必要ない場合は、場所が、最大のワイド エリア ネットワーク (WAN) の速度と利用可能な帯域幅をサイトに場所のサブネットを追加します。  
  
サイトとのネットワーク アドレスとサブネット マスクそれぞれの場所となる場所を文書化します。 サイトを文書化するために、ワークシートでは、次を参照してください[ジョブ エイドの Windows Server 2003 展開キット](https://go.microsoft.com/fwlink/?LinkID=102558)、Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip をダウンロードして"関連付けサブネットでを開きます。サイト"(DSSTOPO_6.doc)。  
  
## <a name="creating-a-site-object-design"></a>サイト オブジェクト設計の作成

サイトを作成することが決定されました、すべての場所には、Active Directory Domain Services (AD DS) にサイト オブジェクトを作成する予定です。 「に関連付けるサブネットをサイト」ワークシート内のサイトになるドキュメントの場所。  
  
サイト オブジェクトを作成する方法の詳細については、記事を参照してください。[サイトを作成する](https://go.microsoft.com/fwlink/?LinkId=107067)します。  
  
## <a name="creating-a-subnet-object-design"></a>サブネット オブジェクト設計の作成

すべての IP サブネットと各場所に関連付けられたサブネット マスクを使用してには、サイト内のすべての IP アドレスを表す AD DS にサブネット オブジェクトを作成する予定です。  
  
ネットワークの IP サブネットとサブネット マスクに関する情報がネットワーク プレフィックス長表記形式に変換が自動的に Active Directory サブネット オブジェクトを作成するときに<IP address> /<prefix length>します。 たとえば、ネットワーク IP バージョン 4 (IPv4) アドレス 172.16.4.0 サブネット 255.255.252.0 の 172.16.4.0/22 として表示されます。 IPv4 アドレスだけでなく Windows Server 2008 もサポートしている IP version 6 (IPv6) のサブネット プレフィックス、たとえば、3ffe:ffff:0:c 000::/64 です。 各場所の IP サブネットの詳細については、「場所とサブネット」(DSSTOPO_2.doc) のワークシートを参照してください[ネットワーク情報の収集](../../ad-ds/plan/Collecting-Network-Information.md)と[付録 a:。場所とサブネットのプレフィックス](Appendix-A--Locations-and-Subnet-Prefixes.md)します。  
  
サブネットを決定する「を決定する場所になるサイト」セクションでは「に関連付けるサブネットをサイト」(DSSTOPO_6.doc) ワークシートを参照して、サイト オブジェクトの場合は、各サブネット オブジェクトがどのサイトと関連付ける関連付けします。 Active Directory サブネット オブジェクトを「に関連付けるサブネットをサイト」(DSSTOPO_6.doc) ワークシート内の各場所に関連付けられているドキュメントです。  
  
サブネット オブジェクトを作成する方法の詳細については、記事を参照してください。[サブネットを作成する](https://go.microsoft.com/fwlink/?LinkId=107068)します。
