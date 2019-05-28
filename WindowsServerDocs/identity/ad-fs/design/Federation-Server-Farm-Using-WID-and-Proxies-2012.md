---
ms.assetid: 8890ccc9-068d-4da2-bd51-8a2964173ff1
title: WID とプロキシを使用するフェデレーション サーバー ファーム
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 19e73e43a863ec60fbc9da09b24173220bb331ed
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191357"
---
# <a name="federation-server-farm-using-wid-and-proxies"></a>WID とプロキシを使用するフェデレーション サーバー ファーム

Active Directory フェデレーション サービスの場合は、この配置トポロジ\(AD FS\)が Windows Internal Database のフェデレーション サーバー ファームと同じ\(WID\)がトポロジでは、フェデレーション サーバー プロキシを追加します。外部ユーザーをサポートするために境界ネットワーク。 フェデレーション サーバー プロキシは、フェデレーション サーバー ファームに、企業ネットワーク外から取得したクライアントの認証要求をリダイレクトします。  
  
## <a name="deployment-considerations"></a>展開に関する考慮事項  
このセクションでは、対象となるユーザー、利点、およびこの配置トポロジに関連付けられている制限事項についてさまざまな考慮事項について説明します。  
  
### <a name="who-should-use-this-topology"></a>このトポロジを使用する必要がありますか。  
  
-   組織の内部ユーザーと外部ユーザーの両方を指定する必要がある 100 以下の構成済みの信頼関係を持つ\(企業ネットワークの外部に物理的に配置されているコンピューターにログオンしたユーザーは\)1 回サインオン\-で\(SSO\)フェデレーション アプリケーションまたはサービスへのアクセス  
  
-   Microsoft Office 365 に SSO アクセス権を持つ、内部ユーザーと外部ユーザーの両方を提供する必要がある組織  
  
-   外部ユーザーが、重複した、スケーラブルなサービスを必要とする小規模な組織  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>このトポロジを使用する利点とは  
  
-   場合と同じメリットがあります、 [WID フェデレーション サーバー ファームを使用して](Federation-Server-Farm-Using-WID-2012.md)トポロジ、および外部ユーザーを追加のアクセスを提供するための特典  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>このトポロジを使用する場合の制限事項を挙げてください。  
  
-   表示されていると同じ制限、 [WID フェデレーション サーバー ファームを使用して](Federation-Server-Farm-Using-WID-2012.md)トポロジ  
  
## <a name="server-placement-and-network-layout-recommendations"></a>サーバーの配置とネットワーク レイアウトの推奨事項  
2 つのフェデレーション サーバー プロキシを追加するだけでなく、このトポロジをデプロイする必要がありますを確認することを境界ネットワークもにアクセスできるように、ドメイン ネーム システム\(DNS\)サーバーと、2 つ目ネットワーク負荷分散に\(NLB\)ホスト。 2 番目の NLB ホストは、インターネットを使用する NLB クラスターを構成する必要があります\-企業ネットワーク上に構成されて以前の NLB クラスターと同じクラスター DNS 名の設定を使用する必要がありますアクセス可能なクラスター IP アドレス、およびその\(fs.fabrikam.com\)します。 フェデレーション サーバー プロキシはインターネットと構成も必要があります\-アクセス可能な IP アドレス。  
  
次の図は、以前に説明した WID トポロジと架空の会社の Fabrikam, Inc. が境界の DNS サーバーへのアクセスを提供する方法は、既存のフェデレーション サーバー ファームを同じクラスター DNS 名2番目のNLBホストを追加します\(fs.fabrikam.com\)、2 つのフェデレーション サーバー プロキシの追加と\(fsp1 および fsp2\)境界ネットワークにします。  
  
![WID を使用して、サーバー ファーム](media/FarmWIDProxies.gif)  
  
フェデレーション サーバーまたはフェデレーション サーバー プロキシを使用するため、ネットワーク環境を構成する方法の詳細については、のいずれかの操作を参照して[フェデレーション サーバーの名前解決要件](Name-Resolution-Requirements-for-Federation-Servers.md)または[名フェデレーション サーバー プロキシの解決の要件](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)します。  
  
## <a name="see-also"></a>関連項目
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
