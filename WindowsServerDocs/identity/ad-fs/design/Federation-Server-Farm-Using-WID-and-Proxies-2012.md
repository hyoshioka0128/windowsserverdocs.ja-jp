---
ms.assetid: 8890ccc9-068d-4da2-bd51-8a2964173ff1
title: WID とプロキシを使用するフェデレーション サーバー ファーム
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 60072037aea4ecd81376e1334f3a89b7bb2ff851
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408085"
---
# <a name="federation-server-farm-using-wid-and-proxies"></a>WID とプロキシを使用するフェデレーション サーバー ファーム

Active Directory フェデレーションサービス (AD FS) \(AD FS @ no__t のこの展開トポロジは、Windows Internal Database \(WID @ no__t トポロジのフェデレーションサーバーファームと同じですが、フェデレーションサーバープロキシを境界ネットワークに追加します。外部ユーザーをサポートします。 フェデレーションサーバープロキシは、企業ネットワークの外部からのクライアント認証要求をフェデレーションサーバーファームにリダイレクトします。  
  
## <a name="deployment-considerations"></a>展開に関する考慮事項  
このセクションでは、この展開トポロジに関連する対象ユーザー、利点、および制限事項に関するさまざまな考慮事項について説明します。  
  
### <a name="who-should-use-this-topology"></a>このトポロジを使用する必要がありますか。  
  
-   100以下の信頼関係を持つ組織では、社内のユーザーと外部ユーザーの両方を提供する必要があります。 @no__t は、物理的に企業ネットワークの外部にあるコンピューターにログオンしている場合は、シングルサイン @ no__t-2on を指定します。\(SSO @ no__t-4 フェデレーションアプリケーションまたはサービスへのアクセス  
  
-   内部ユーザーと外部ユーザーの両方に Microsoft Office 365 への SSO アクセスを提供する必要がある組織  
  
-   外部ユーザーを持ち、冗長でスケーラブルなサービスを必要とする小規模の組織  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>このトポロジを使用する利点とは  
  
-   [WID トポロジを使用するフェデレーションサーバーファーム](Federation-Server-Farm-Using-WID-2012.md)と同じ利点に加えて、外部ユーザーに追加のアクセスを提供する利点もあります。  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>このトポロジを使用する場合の制限事項を挙げてください。  
  
-   [WID トポロジを使用したフェデレーションサーバーファーム](Federation-Server-Farm-Using-WID-2012.md)の一覧と同じ制限事項  
  
## <a name="server-placement-and-network-layout-recommendations"></a>サーバーの配置とネットワークレイアウトに関する推奨事項  
このトポロジを展開するには、2つのフェデレーションサーバープロキシを追加するだけでなく、境界ネットワークからドメインネームシステムへのアクセスも許可する必要があります。これには、@no__t 0DNS @ no__t サーバーと2番目のネットワーク負荷分散 \(NLB @ no__t ホストを指定します。 2番目の NLB ホストは、インターネット @ no__t からアクセス可能なクラスター IP アドレスを使用する NLB クラスターを使用して構成する必要があります。また、企業 @no__t ネットワークで構成した前の NLB クラスターと同じクラスター DNS 名設定を使用する必要があります。 フェデレーションサーバープロキシは、Internet @ no__t にアクセス可能な IP アドレスで構成する必要もあります。  
  
次の図は、既に説明した WID トポロジを使用した既存のフェデレーションサーバーファームと、架空の Fabrikam, Inc. が境界 DNS サーバーへのアクセスを提供する方法、同じクラスター DNS @no__t 名を持つ2番目の NLB ホストを追加する方法を示しています。 no__t @ 2fsp1、境界ネットワークに2つのフェデレーションサーバー @no__t プロキシを追加し、  
  
![WID を使用するサーバーファーム](media/FarmWIDProxies.gif)  
  
フェデレーションサーバーまたはフェデレーションサーバープロキシで使用するためのネットワーク環境を構成する方法の詳細については、「フェデレーション[サーバーの名前解決の要件](Name-Resolution-Requirements-for-Federation-Servers.md)」または「[フェデレーションの名前解決の要件」を参照してください。サーバープロキシ](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)。  
  
## <a name="see-also"></a>関連項目
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
