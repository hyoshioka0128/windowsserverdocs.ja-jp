---
ms.assetid: 8890ccc9-068d-4da2-bd51-8a2964173ff1
title: WID とプロキシを使用してフェデレーションサーバーファームを AD FS する
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: e70359b5a05fed8e7cfb467d3410e12939a1de1b
ms.sourcegitcommit: de8fea497201d8f3d995e733dfec1d13a16cb8fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87864053"
---
# <a name="federation-server-farm-using-wid-and-proxies"></a>WID とプロキシを使用するフェデレーション サーバー ファーム

Active Directory フェデレーションサービス (AD FS) AD FS のこの展開 \( トポロジ \) は、Windows Internal Database WID トポロジを持つフェデレーションサーバーファームと同じです \( \) が、外部ユーザーをサポートするために、フェデレーションサーバープロキシを境界ネットワークに追加します。 フェデレーションサーバープロキシは、企業ネットワークの外部からのクライアント認証要求をフェデレーションサーバーファームにリダイレクトします。  
  
## <a name="deployment-considerations"></a>デプロイに関する考慮事項  
このセクションでは、この展開トポロジに関連する対象ユーザー、利点、および制限事項に関するさまざまな考慮事項について説明します。  
  
### <a name="who-should-use-this-topology"></a>このトポロジを使用する必要がありますか。  
  
-   100またはそれよりも少数の信頼関係がある組織では、社内ユーザーと \( 、 \) \- \( \) フェデレーションアプリケーションまたはサービスへのシングルサインオン SSO アクセスを持つ企業ネットワークの外部にあるコンピューターにログオンしている外部ユーザーの両方を提供する必要があります。  
  
-   内部ユーザーと外部ユーザーの両方に Microsoft Office 365 への SSO アクセスを提供する必要がある組織  
  
-   外部ユーザーを持ち、冗長でスケーラブルなサービスを必要とする小規模の組織  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>このトポロジを使用する利点とは  
  
-   [WID トポロジを使用するフェデレーションサーバーファーム](Federation-Server-Farm-Using-WID-2012.md)と同じ利点に加えて、外部ユーザーに追加のアクセスを提供する利点もあります。  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>このトポロジを使用する場合の制限事項を挙げてください。  
  
-   [WID トポロジを使用したフェデレーションサーバーファーム](Federation-Server-Farm-Using-WID-2012.md)の一覧と同じ制限事項  
  
## <a name="server-placement-and-network-layout-recommendations"></a>サーバーの配置とネットワークレイアウトに関する推奨事項  
このトポロジを展開するには、2つのフェデレーションサーバープロキシを追加するだけでなく、境界ネットワークがドメインネームシステムの \( DNS \) サーバーと2番目のネットワーク負荷分散 NLB ホストにもアクセスできるようにする必要があり \( \) ます。 2番目の NLB ホストは、インターネットアクセス可能なクラスター IP アドレスを使用する NLB クラスタで構成する必要があり \- ます。また、企業ネットワーク fs.fabrikam.com で構成した前の nlb クラスタと同じクラスタ DNS 名設定を使用する必要があり \( \) ます。 フェデレーションサーバープロキシは、インターネットからアクセス可能な IP アドレスを使用して構成する必要もあり \- ます。  
  
次の図は、既に説明した WID トポロジを使用した既存のフェデレーションサーバーファームと、架空の Fabrikam, Inc. が境界 DNS サーバーへのアクセスを提供し、同じクラスター DNS 名 fs.fabrikam.com を持つ2番目の NLB ホストを追加 \( \) し、境界ネットワークに2つのフェデレーションサーバープロキシ fsp1 と fsp2 を追加する方法を示しています \( \) 。  
  
![WID を使用するサーバーファーム](media/FarmWIDProxies.gif)  
  
フェデレーションサーバーまたはフェデレーションサーバープロキシで使用するネットワーク環境を構成する方法の詳細については、「フェデレーションサーバー[の名前解決の要件](Name-Resolution-Requirements-for-Federation-Servers.md)」または「[フェデレーションサーバープロキシの名前解決の要件](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)」を参照してください。  
  
## <a name="see-also"></a>参照
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
