---
ms.assetid: 8890ccc9-068d-4da2-bd51-8a2964173ff1
title: WID とプロキシを使用するフェデレーション サーバー ファーム
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 9c6dba880b80de43bb713d1b4495f0e03d56a695
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853095"
---
# <a name="federation-server-farm-using-wid-and-proxies"></a>WID とプロキシを使用するフェデレーション サーバー ファーム

Active Directory フェデレーションサービス (AD FS) \(AD FS\) のこの展開トポロジは、Windows Internal Database \(WID\) トポロジを持つフェデレーションサーバーファームと同じですが、外部ユーザーをサポートするために、フェデレーションサーバープロキシを境界ネットワークに追加します。 フェデレーションサーバープロキシは、企業ネットワークの外部からのクライアント認証要求をフェデレーションサーバーファームにリダイレクトします。  
  
## <a name="deployment-considerations"></a>展開に関する考慮事項  
このセクションでは、この展開トポロジに関連する対象ユーザー、利点、および制限事項に関するさまざまな考慮事項について説明します。  
  
### <a name="who-should-use-this-topology"></a>このトポロジを使用する必要がありますか。  
  
-   100以下の信頼関係を持つ組織は、企業ネットワークの外部に物理的に配置されているコンピューターにログオンしているコンピューター \(\-\) 内部ユーザーと外部ユーザーの両方を提供する必要があります。 \(SSO\) フェデレーションアプリケーションまたはサービスへのアクセス  
  
-   内部ユーザーと外部ユーザーの両方に Microsoft Office 365 への SSO アクセスを提供する必要がある組織  
  
-   外部ユーザーを持ち、冗長でスケーラブルなサービスを必要とする小規模の組織  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>このトポロジを使用する利点とは  
  
-   [WID トポロジを使用するフェデレーションサーバーファーム](Federation-Server-Farm-Using-WID-2012.md)と同じ利点に加えて、外部ユーザーに追加のアクセスを提供する利点もあります。  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>このトポロジを使用する場合の制限事項を挙げてください。  
  
-   [WID トポロジを使用したフェデレーションサーバーファーム](Federation-Server-Farm-Using-WID-2012.md)の一覧と同じ制限事項  
  
## <a name="server-placement-and-network-layout-recommendations"></a>サーバーの配置とネットワークレイアウトに関する推奨事項  
このトポロジを展開するには、2つのフェデレーションサーバープロキシを追加するだけでなく、境界ネットワークがドメインネームシステム \(DNS\) サーバーにアクセスし、2番目のネットワーク負荷分散 \(NLB\) ホストにもアクセスできるようにする必要があります。 2番目の NLB ホストは、インターネット\-アクセス可能なクラスター IP アドレスを使用する NLB クラスターを使用して構成する必要があります。また、企業ネットワーク \(fs.fabrikam.com\)で構成した前の NLB クラスターと同じクラスター DNS 名設定を使用する必要があります。 フェデレーションサーバープロキシは、インターネット\-のアクセス可能な IP アドレスで構成する必要もあります。  
  
次の図は、既に説明した WID トポロジを使用した既存のフェデレーションサーバーファームと、架空の Fabrikam, Inc. が境界 DNS サーバーへのアクセスを提供する方法を示しています。また、fs.fabrikam.com\)と同じクラスター DNS \(名を持つ2番目の NLB ホストを追加し、境界ネットワークに2つのフェデレーションサーバープロキシ\) \(追加します  
  
![WID を使用するサーバーファーム](media/FarmWIDProxies.gif)  
  
フェデレーションサーバーまたはフェデレーションサーバープロキシで使用するネットワーク環境を構成する方法の詳細については、「フェデレーションサーバー[の名前解決の要件](Name-Resolution-Requirements-for-Federation-Servers.md)」または「[フェデレーションサーバープロキシの名前解決の要件](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)」を参照してください。  
  
## <a name="see-also"></a>参照
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
