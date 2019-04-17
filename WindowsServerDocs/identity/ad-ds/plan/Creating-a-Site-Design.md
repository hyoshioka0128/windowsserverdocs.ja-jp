---
ms.assetid: 83f746e5-81db-4610-9977-1d5c57699f50
title: "サイト設計の作成"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 2bcbf30159721e1fc2e12af103ca6f3e79f3ec97
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="creating-a-site-design"></a>サイト設計の作成

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サイトの設計を作成するには、サイトにする場所を決定する、サイト オブジェクトの作成、サブネット オブジェクトを作成する、およびサイトとサブネットを関連付けることが必要があります。  
  
## <a name="deciding-which-locations-will-become-sites"></a>サイトにする場所を決定します。  
次のようにサイトを作成する場所を決定します。  
  
-   ドメイン コントローラーを配置を計画しているすべての場所のサイトを作成します。 ドメイン コントローラーが含まれる場所を識別する「ドメイン コントローラー配置」(DSSTOPO_4.doc) ワークシートに記載されている情報を参照してください。  
  
-   サイトを作成できるを必要とするアプリケーションを実行しているサーバーが含まれるこれらの場所のサイトを作成します。 など分散ファイル システム名前空間 (DFSN) を特定のアプリケーションでは、サイト オブジェクトを使用して、クライアントに最も近いサーバーを検索します。  
  
    > [!NOTE]  
    > 組織に複数のネットワークで高速で信頼性の高い接続の近くにある場合は、単一の Active Directory サイトでそれらのネットワークのサブネットのすべてを含めることができます。 たとえば、ネットワーク別の 2 つのサーバー間での待機時間のラウンド トリップを返す場合サブネットが 10 ms または以下の場合、同じ Active Directory サイトで両方のサブネットを含めることができます。 次の 2 つの場所の間でネットワーク待ち時間が 10 ms を超える場合は、単一の Active Directory サイト、サブネットを含めないでください。 でもと待機時間が 10 ms または以下の場合、Active Directory ベース アプリケーション用のサイト間のトラフィックのセグメント化する場合は、個別のサイトを展開することもできます。  
  
-   サイトが必要な場所でない場合は、最大のワイド エリア ネットワーク (WAN) の速度と利用可能な帯域幅を場所には、サイトに、場所のサブネットを追加します。  
  
サイトとネットワーク アドレスとサブネット マスク内の各場所になる場所を文書化します。 サイトを文書化するためのワークシートで、ジョブ エイドの Windows Server 2003 導入ガイドを参照してください ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558))、Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip、およびオープン「に関連付けるサブネットとサイト」(DSSTOPO_6.doc) します。  
  
## <a name="creating-a-site-object-design"></a>サイト オブジェクト設計を作成します。  
サイトを作成するが決まったら場所ごとに、Active Directory ドメイン サービス (AD DS) でサイト オブジェクトを作成する計画します。 サイト「に関連付けるサブネットとサイト」ワークシートにドキュメントの場所。  
  
サイト オブジェクトを作成する方法の詳細については、サイトの作成を参照してください ([https://go.microsoft.com/fwlink/?LinkId=107067](https://go.microsoft.com/fwlink/?LinkId=107067))。  
  
## <a name="creating-a-subnet-object-design"></a>サブネット オブジェクト設計を作成します。  
すべての IP サブネットとそれぞれの場所に関連付けられたサブネット マスク、サイト内のすべての IP アドレスを表す AD DS のサブネット オブジェクトを作成する計画します。  
  
Active Directory サブネット オブジェクトを作成すると、ネットワークの IP サブネットとサブネット マスクに関する情報が自動的にネットワーク プレフィックス長表記形式に変換<IP address>/<prefix length>します。 たとえば、ネットワーク IP バージョン 4 (IPv4) アドレス 172.16.4.0 とサブネット マスク 255.255.252.0 172.16.4.0/22 が表示されます。 IPv4 アドレスだけでなく Windows Server 2008 もサポートしている IP version 6 (IPv6) のサブネット プレフィックスをたとえば、3ffe:ffff:0:c 000::/64 します。 詳細については、それぞれの場所にある IP サブネットで「場所およびサブネット」(DSSTOPO_2.doc) ワークシートを参照してください。[ネットワーク情報の収集](../../ad-ds/plan/Collecting-Network-Information.md)と[付録 a: 場所とサブネットのプレフィックス](Appendix-A--Locations-and-Subnet-Prefixes.md)します。  
  
どのサイトに関連付けるはサブネットを決定する「を決定する場所になるサイト」セクションでは「に関連付けるサブネットとサイト」(DSSTOPO_6.doc) ワークシートを参照して、サイト オブジェクトには、各サブネット オブジェクトを関連付けるです。 「サイトに関連付けるサブネット」(DSSTOPO_6.doc) ワークシートで各場所に関連付けられている Active Directory のサブネット オブジェクトを文書化します。  
  
サブネット オブジェクトを作成する方法の詳細については、サブネットを作成するを参照してください ([https://go.microsoft.com/fwlink/?LinkId=107068](https://go.microsoft.com/fwlink/?LinkId=107068))。  
  


