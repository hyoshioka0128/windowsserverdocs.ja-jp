---
ms.assetid: f0464182-56a2-4bfa-a8c8-7e39c1bd62d3
title: WID とプロキシを使用するフェデレーション サーバー ファーム
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 523e076ad9593f09ac2f9db5c45fa8c2e82f05bb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853105"
---
# <a name="federation-server-farm-using-wid-and-proxies"></a>WID とプロキシを使用するフェデレーション サーバー ファーム

Active Directory フェデレーションサービス (AD FS) \(AD FS\) のこの展開トポロジは、Windows Internal Database \(WID\) トポロジを持つフェデレーションサーバーファームと同じですが、外部ユーザーをサポートするために、境界ネットワークにプロキシコンピューターを追加します。 これらのプロキシは、企業ネットワークの外部からのクライアント認証要求をフェデレーションサーバーファームにリダイレクトします。 以前のバージョンの AD FS では、これらのプロキシはフェデレーションサーバープロキシと呼ばれていました。  
  
> [!IMPORTANT]  
> Windows Server 2012 R2 の Active Directory フェデレーションサービス (AD FS) \(AD FS\) では、フェデレーションサーバープロキシの役割は、Web アプリケーションプロキシと呼ばれる新しいリモートアクセス役割サービスによって処理されます。 AD FS が企業ネットワークの外部からアクセスできるようにします。これは、Windows Server 2012 の AD FS 2.0 や AD FS など、AD FS のレガシバージョンでフェデレーションサーバープロキシを展開するためのものであり、Windows Server 2012 R2 で AD FS 用に1つ以上の web アプリケーションプロキシを展開することができます。  
>   
> AD FS のコンテキストでは、Web アプリケーションプロキシは AD FS フェデレーションサーバープロキシとして機能します。 さらに、Web アプリケーション プロキシには、企業ネットワーク内部の Web アプリケーション用のリバース プロキシ機能があり、ユーザーは任意のデバイスで企業ネットワーク外部から Web アプリケーションにアクセスできます。 Web アプリケーション プロキシの役割サービスの詳細については、「Web アプリケーション プロキシの概要」を参照してください。  
>   
> Web アプリケーション プロキシの展開を計画するには、次のトピックの情報を確認できます。  
>   
> -   [Web アプリケーションプロキシインフラストラクチャ (WAP) を計画する](https://technet.microsoft.com/library/dn383648.aspx)  
> -   [Web アプリケーションプロキシサーバーを計画する](https://technet.microsoft.com/library/dn383647.aspx)  
  
## <a name="deployment-considerations"></a>展開に関する考慮事項  
このセクションでは、この展開トポロジに関連する対象ユーザー、利点、および制限事項に関するさまざまな考慮事項について説明します。  
  
### <a name="who-should-use-this-topology"></a>このトポロジを使用する必要がありますか。  
  
-   100以下の信頼関係を持つ組織は、企業ネットワークの外部に物理的に配置されているコンピューターにログオンしているコンピューター \(\-\) 内部ユーザーと外部ユーザーの両方を提供する必要があります。 \(SSO\) フェデレーションアプリケーションまたはサービスへのアクセス  
  
-   内部ユーザーと外部ユーザーの両方に Microsoft Office 365 への SSO アクセスを提供する必要がある組織  
  
-   外部ユーザーを持ち、冗長でスケーラブルなサービスを必要とする小規模の組織  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>このトポロジを使用する利点とは  
  
-   [WID トポロジを使用するフェデレーションサーバーファーム](Federation-Server-Farm-Using-WID.md)と同じ利点に加えて、外部ユーザーに追加のアクセスを提供する利点もあります。  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>このトポロジを使用する場合の制限事項を挙げてください。  
  
-   [WID トポロジを使用したフェデレーションサーバーファーム](Federation-Server-Farm-Using-WID.md)の一覧と同じ制限事項  

||1 \- 100 RP 信頼|100を超える RP 信頼 
| ----- |-----| ------ |
|1 \- 30 AD FS ノード|WID でサポートされる|WID を使用してサポートされていません \- SQL が必要です 
|30を超える AD FS ノード|WID を使用してサポートされていません \- SQL が必要です|WID を使用してサポートされていません \- SQL が必要です  
  
## <a name="server-placement-and-network-layout-recommendations"></a>サーバーの配置とネットワークレイアウトに関する推奨事項  
このトポロジを展開するには、2つの web アプリケーションプロキシを追加するだけでなく、境界ネットワークがドメインネームシステム \(DNS\) サーバーにアクセスし、2番目のネットワーク負荷分散 \(NLB\) ホストにもアクセスできるようにする必要があります。 2番目の NLB ホストは、インターネット\-アクセス可能なクラスター IP アドレスを使用する NLB クラスターを使用して構成する必要があります。また、企業ネットワーク \(fs.fabrikam.com\)で構成した前の NLB クラスターと同じクラスター DNS 名設定を使用する必要があります。 Web アプリケーションプロキシは、インターネット\-のアクセス可能な IP アドレスで構成する必要もあります。  
  
次の図は、既に説明した WID トポロジを持つ既存のフェデレーションサーバーファームと、架空の Fabrikam, Inc. が境界 DNS サーバーへのアクセスを提供する方法を示しています。また、fs.fabrikam.com\)と同じクラスター DNS \(名を持つ2つ目の NLB ホストを追加し、境界ネットワークに2つの web アプリケーションプロキシ\) \(追加します。  
  
![WID ファームとプロキシ](media/WIDFarmADFSBlue.gif)  
  
フェデレーションサーバーまたは web アプリケーションプロキシで使用するためのネットワーク環境を構成する方法の詳細については、「AD FS の[要件](AD-FS-Requirements.md)」の「名前解決の要件」セクションを参照して、 [Web アプリケーションプロキシインフラストラクチャ (WAP) を計画](https://technet.microsoft.com/library/dn383648.aspx)してください。  
  
## <a name="see-also"></a>参照  
[AD FS 展開トポロジの計画](Plan-Your-AD-FS-Deployment-Topology.md)  
[Windows Server 2012 R2 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

