---
ms.assetid: eeb919de-e21e-48d8-8186-e42adec6933f
title: サイト トポロジの設計
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: e1d9323ceda478369973f959687d46c9ca3cb88f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888493"
---
# <a name="designing-the-site-topology"></a>サイト トポロジの設計

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

ディレクトリ サービスのサイト トポロジは、物理ネットワークの論理表現です。 Active Directory Domain services (AD DS) サイトのトポロジを設計するには、ドメイン コント ローラーの配置と設計のサイト、サブネット、サイト リンク、およびクエリし、レプリケーション トラフィックの効率的なルーティングを確認するサイト リンク ブリッジを計画する必要があります。  
  
サイト トポロジの設計では、クライアントのクエリと Active Directory レプリケーションのトラフィックを効率的にルーティングできます。 適切に設計されたサイト トポロジでは、組織は、次の利点の実現を支援します。  
  
-   Active Directory データをレプリケートするコストを最小限に抑えます。  
  
-   サイトのトポロジを維持するために必要な管理作業を最小限に抑えます。  
  
-   場所で、低速またはダイヤルアップ ネットワークへのリンクをオフピーク時間中に Active Directory データをレプリケートできるようにするためのレプリケーションをスケジュールします。  
  
-   ドメイン コント ローラーと分散ファイル システム (DFS) サーバーなど、最も近いリソースを検索するクライアント コンピューターの機能を最適化します。 低速ワイド エリア ネットワーク トラフィックを削減するには、これによりネットワーク (WAN) リンクするには、ログオンおよびログオフのプロセスを改善およびファイルのダウンロード操作を高速化します。  
  
サイト トポロジの設計を開始する前に、物理ネットワーク構造を理解する必要があります。 さらに、まず管理階層、フォレストの計画、および各フォレストのドメインのプランを含む、Active Directory 論理構造を設計する必要があります。 AD DS のドメイン ネーム システム (DNS) インフラストラクチャの設計を行う必要があります。 Active Directory 論理構造と DNS インフラストラクチャを設計の詳細については、次を参照してください。 [、論理構造の Windows Server 2008 AD DS の設計](https://technet.microsoft.com/library/cc770806.aspx)します。  
  
サイト トポロジの設計を完了した後は、ドメイン コント ローラーが Windows Server 2008 Standard、Windows Server 2008 の Enterprise、および Windows Server 2008 Datacenter のハードウェア要件を満たしていることを確認する必要があります。  
  
## <a name="in-this-guide"></a>このガイドについて  
  
-   [Active Directory サイト トポロジを理解します。](../../ad-ds/plan/Understanding-Active-Directory-Site-Topology.md)  
  
-   [ネットワーク情報の収集](../../ad-ds/plan/Collecting-Network-Information.md)  
  
-   [ドメイン コント ローラーの配置の計画](../../ad-ds/plan/Planning-Domain-Controller-Placement.md)  
  
-   [サイト設計の作成](../../ad-ds/plan/Creating-a-Site-Design.md)  
  
-   [サイト リンク設計の作成](../../ad-ds/plan/Creating-a-Site-Link-Design.md)  
  
-   [サイト リンク ブリッジ設計の作成](../../ad-ds/plan/Creating-a-Site-Link-Bridge-Design.md)  
  
-   [Windows Server 2008 の Active Directory サイト トポロジ設計に関するその他のリソースの検索](../../ad-ds/plan/Finding-Additional-Resources-for-Windows-Server-2008-Active-Directory-Site-Topology-Design.md)  
  


