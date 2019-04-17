---
ms.assetid: 8890ccc9-068d-4da2-bd51-8a2964173ff1
title: "WID とプロキシを使用してフェデレーション サーバー ファーム"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4bd815daccdd72a8c612b9b728ce12378c1926e7
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="federation-server-farm-using-wid-and-proxies"></a>WID とプロキシを使用してフェデレーション サーバー ファーム

>適用対象: Windows Server 2012

Active Directory フェデレーション サービス \(AD FS\) の場合は、この展開トポロジが Windows Internal Database \(WID\) トポロジを使ってフェデレーション サーバー ファームと同じですが、外部ユーザーをサポートするために、境界ネットワークにフェデレーション サーバー プロキシを追加します。 フェデレーション サーバー プロキシは、フェデレーション サーバー ファームに企業ネットワークの外側に起因するクライアントの認証要求をリダイレクトします。  
  
## <a name="deployment-considerations"></a>展開に関する考慮事項  
このセクションでは、対象となるユーザー、利点、およびこの展開トポロジに関連付けられている制限事項についてさまざまな考慮事項について説明します。  
  
### <a name="who-should-use-this-topology"></a>このトポロジを使用している必要がありますか。  
  
-   内部ユーザーと外部ユーザーの両方を提供する必要がある 100 台以下の構成済みの信頼関係を持つ組織 \ (ユーザーがコンピューターにログオン物理的に企業ネットワークの外側にある) 1 つ sign\ で \(SSO\) アクセス権を持つ、フェデレーション アプリケーションまたはサービス  
  
-   Microsoft Office 365 SSO アクセス権を持つ内部ユーザーと外部ユーザーの両方を提供する必要がある組織  
  
-   外部ユーザーが存在し、冗長なでスケーラブルなサービスを必要とする小規模な組織  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>このトポロジを使用する利点は何ですか。  
  
-   一覧に表示されている同じメリット、[WID フェデレーション サーバー ファームを使用して](Federation-Server-Farm-Using-WID-2012.md)トポロジと外部ユーザーの追加のアクセスを提供することの利点は、  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>このトポロジを使用する場合の制限事項とは何ですか。  
  
-   表示されていると同じ制限、[WID フェデレーション サーバー ファームを使用して](Federation-Server-Farm-Using-WID-2012.md)トポロジ  
  
## <a name="server-placement-and-network-layout-recommendations"></a>サーバーの配置とネットワーク レイアウトの推奨事項  
2 台のフェデレーション サーバー プロキシを追加するだけでなく、このトポロジを展開するには、境界ネットワークの場合、ドメイン ネーム システム \(DNS\) サーバーおよび 2 番目のネットワーク負荷分散 \(NLB\) ホストへのアクセスも提供を確認する必要があります。 NLB クラスターとは限らないからアクセス可能なクラスター IP アドレスを使用すると、2 番目の NLB ホストを構成する必要があり、企業ネットワーク \(fs.fabrikam.com\) で構成した前の NLB クラスターとして同じクラスター DNS 名の設定を使用する必要があります。 フェデレーション サーバー プロキシとは限らないからアクセス可能な IP アドレスを持つも構成する必要があります。  
  
同じクラスター DNS 名 \(fs.fabrikam.com\) と 2 番目の NLB ホストを追加する次の図は、WID トポロジ上記に記載されている架空の企業で Fabrikam, Inc. が境界 DNS サーバーへのアクセスを提供する方法と、既存のフェデレーション サーバー ファームし、2 台のフェデレーション サーバー プロキシを追加 \(fsp1 and fsp2\) 境界ネットワークにします。  
  
![サーバー ファームが WID を使用します。](media/FarmWIDProxies.gif)  
  
フェデレーション サーバーまたはフェデレーション サーバー プロキシで使用するため、ネットワーク環境を構成する方法の詳細については、いずれかを参照して[フェデレーション サーバーの名前解決要件](Name-Resolution-Requirements-for-Federation-Servers.md)または[フェデレーション サーバー プロキシの名前解決要件](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)します。  
  
## <a name="see-also"></a>参照してください。
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)
