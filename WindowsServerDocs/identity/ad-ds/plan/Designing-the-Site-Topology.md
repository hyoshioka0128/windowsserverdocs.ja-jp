---
ms.assetid: eeb919de-e21e-48d8-8186-e42adec6933f
title: サイト トポロジの設計
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: d3ebc3bd764a8ed44e201d0fca5f85b06df8be9d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408892"
---
# <a name="designing-the-site-topology"></a>サイト トポロジの設計

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

ディレクトリサービスサイトのトポロジは、物理ネットワークを論理的に表したものです。 Active Directory Domain Services (AD DS) 用のサイトトポロジの設計には、ドメインコントローラーの配置の計画、サイト、サブネット、サイトリンク、およびサイトリンクブリッジの設計が含まれます。これにより、クエリとレプリケーションのトラフィックを効率的にルーティングすることができます。  
  
サイトトポロジを設計すると、クライアントクエリを効率的にルーティングし、レプリケーショントラフィックを Active Directory できます。 適切に設計されたサイトトポロジを使用すると、組織は次のような利点を得ることができます。  
  
-   Active Directory データをレプリケートするコストを最小限に抑えます。  
  
-   サイトトポロジを維持するために必要な管理作業を最小限に抑えます。  
  
-   低速またはダイヤルアップネットワークリンクがある場所で、ピーク時以外の時間帯に Active Directory データをレプリケートするようにレプリケーションをスケジュールします。  
  
-   クライアントコンピューターがドメインコントローラーや分散ファイルシステム (DFS) サーバーなど、最も近いリソースを見つける機能を最適化します。 これにより、低速のワイドエリアネットワーク (WAN) リンクを介したネットワークトラフィックを削減し、ログオンとログオフのプロセスを改善し、ファイルのダウンロード操作を高速化できます。  
  
サイトトポロジの設計を開始する前に、物理ネットワークの構造を理解しておく必要があります。 また、まず、管理階層、フォレスト計画、および各フォレストのドメイン計画を含む Active Directory の論理構造を設計する必要があります。 また、AD DS については、ドメインネームシステム (DNS) インフラストラクチャの設計も完了している必要があります。 Active Directory 論理構造と DNS インフラストラクチャの設計の詳細については、「 [Windows Server 2008 AD DS の論理構造の設計](https://technet.microsoft.com/library/cc770806.aspx)」を参照してください。  
  
サイトトポロジの設計が完了したら、ドメインコントローラーが Windows Server 2008 Standard、Windows Server 2008 Enterprise、および Windows Server 2008 Datacenter のハードウェア要件を満たしていることを確認する必要があります。  
  
## <a name="in-this-guide"></a>このガイドについて  
  
-   [Active Directory サイト トポロジとは](../../ad-ds/plan/Understanding-Active-Directory-Site-Topology.md)  
  
-   [ネットワーク情報の収集](../../ad-ds/plan/Collecting-Network-Information.md)  
  
-   [ドメイン コントローラー配置の計画](../../ad-ds/plan/Planning-Domain-Controller-Placement.md)  
  
-   [サイト設計の作成](../../ad-ds/plan/Creating-a-Site-Design.md)  
  
-   [サイト リンク設計の作成](../../ad-ds/plan/Creating-a-Site-Link-Design.md)  
  
-   [サイト リンク ブリッジ設計の作成](../../ad-ds/plan/Creating-a-Site-Link-Bridge-Design.md)  
  
-   [Windows Server 2008 Active Directory サイトトポロジの設計に関するその他のリソースの検索](../../ad-ds/plan/Finding-Additional-Resources-for-Windows-Server-2008-Active-Directory-Site-Topology-Design.md)  
  


