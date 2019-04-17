---
ms.assetid: eeb919de-e21e-48d8-8186-e42adec6933f
title: "サイト トポロジの設計"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 3f16b5b941ef9c3bd8f4bf742d432afc1b3f559a
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="designing-the-site-topology"></a>サイト トポロジの設計

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ディレクトリ サービス サイトのトポロジは、物理ネットワークの論理表現です。 Active Directory ドメイン サービス (AD DS) のサイト トポロジの設計には、ドメイン コントローラーの配置と設計サイト、サブネット、サイト リンク、およびクエリとレプリケーションのトラフィックの効果的なルーティングすることを確認するサイト リンク ブリッジの計画が含まれます。  
  
サイト トポロジの設計と、クライアントのクエリと Active Directory レプリケーションのトラフィックを効率的にルーティングするのに役立ちます。 適切に設計されたサイトのトポロジでは、組織は、次の利点を得ることができます。  
  
-   Active Directory データをレプリケートするコストを最小限に抑えます。  
  
-   サイト トポロジを維持するために必要な管理作業を最小限に抑えます。  
  
-   ピーク時以外に Active Directory データをレプリケートする低速またはダイヤルアップ ネットワークへのリンクの場所を実現するレプリケーションをスケジュールします。  
  
-   ドメイン コントローラーと分散ファイル システム (DFS) サーバーなど、最も近いリソースを検索するクライアント コンピューターの機能を最適化します。 低速のワイド エリア経由でネットワーク トラフィックを削減するには、これによりネットワーク (WAN) リンクするには、ログオンおよびログオフのプロセスを改善し、ファイル ダウンロードの操作を高速化します。  
  
サイト トポロジの設計を開始する前に、物理ネットワークの構造を理解する必要があります。 さらに、まず管理階層、フォレストの計画、各フォレストのドメインの計画など、Active Directory 論理構造を設計する必要があります。 AD DS のドメイン ネーム システム (DNS) インフラストラクチャの設計を行う必要があります。 詳細については、Active Directory 論理構造と DNS インフラストラクチャの設計について、次を参照してください。[、論理構造の Windows Server 2008 AD DS の設計](https://technet.microsoft.com/library/cc770806.aspx)します。  
  
サイト トポロジの設計を完了した後、ドメイン コントローラーが Windows Server 2008 Standard、Windows Server 2008 Enterprise、および Windows Server 2008 Datacenter のハードウェア要件を満たしていることを確認する必要があります。  
  
## <a name="in-this-guide"></a>このガイドで  
  
-   [Active Directory サイト トポロジを理解します。](../../ad-ds/plan/Understanding-Active-Directory-Site-Topology.md)  
  
-   [ネットワーク情報の収集](../../ad-ds/plan/Collecting-Network-Information.md)  
  
-   [ドメイン コントローラーの配置を計画します。](../../ad-ds/plan/Planning-Domain-Controller-Placement.md)  
  
-   [サイト設計の作成](../../ad-ds/plan/Creating-a-Site-Design.md)  
  
-   [サイト リンク設計を作成します。](../../ad-ds/plan/Creating-a-Site-Link-Design.md)  
  
-   [サイト リンク ブリッジ設計を作成します。](../../ad-ds/plan/Creating-a-Site-Link-Bridge-Design.md)  
  
-   [Windows Server 2008 の Active Directory サイト トポロジの設計の他のリソース](../../ad-ds/plan/Finding-Additional-Resources-for-Windows-Server-2008-Active-Directory-Site-Topology-Design.md)  
  


