---
ms.assetid: f0464182-56a2-4bfa-a8c8-7e39c1bd62d3
title: WID とプロキシを使用するフェデレーション サーバー ファーム
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 6a123afaebba002b8ee4fb98d5cee5aded286a96
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359133"
---
# <a name="federation-server-farm-using-wid-and-proxies"></a>WID とプロキシを使用するフェデレーション サーバー ファーム

Active Directory フェデレーションサービス (AD FS) \(AD FS @ no__t のこの展開トポロジは、Windows Internal Database \(WID @ no__t トポロジのフェデレーションサーバーファームと同じですが、サポートするために、境界ネットワークにプロキシコンピューターを追加します。外部ユーザー。 これらのプロキシは、企業ネットワークの外部からのクライアント認証要求をフェデレーションサーバーファームにリダイレクトします。 以前のバージョンの AD FS では、これらのプロキシはフェデレーションサーバープロキシと呼ばれていました。  
  
> [!IMPORTANT]  
> Windows Server 2012 R2 の Active Directory フェデレーションサービス (AD FS) \(AD FS @ no__t-1 では、フェデレーションサーバープロキシの役割は、Web アプリケーションプロキシと呼ばれる新しいリモートアクセス役割サービスによって処理されます。 AD FS AD FS のレガシバージョンでフェデレーションサーバープロキシを展開する目的であった企業ネットワークの外部からのアクセスを可能にするには (AD FS 2.0、Windows Server 2012 の AD FS など)、1つまたは複数の web アプリケーションプロキシを展開できます。Windows Server 2012 R2 の D FS。  
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
  
-   100以下の信頼関係を持つ組織では、社内のユーザーと外部ユーザーの両方を提供する必要があります。 @no__t は、物理的に企業ネットワークの外部にあるコンピューターにログオンしている場合は、シングルサイン @ no__t-2on を指定します。\(SSO @ no__t-4 フェデレーションアプリケーションまたはサービスへのアクセス  
  
-   内部ユーザーと外部ユーザーの両方に Microsoft Office 365 への SSO アクセスを提供する必要がある組織  
  
-   外部ユーザーを持ち、冗長でスケーラブルなサービスを必要とする小規模の組織  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>このトポロジを使用する利点とは  
  
-   [WID トポロジを使用するフェデレーションサーバーファーム](Federation-Server-Farm-Using-WID.md)と同じ利点に加えて、外部ユーザーに追加のアクセスを提供する利点もあります。  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>このトポロジを使用する場合の制限事項を挙げてください。  
  
-   [WID トポロジを使用したフェデレーションサーバーファーム](Federation-Server-Farm-Using-WID.md)の一覧と同じ制限事項  

||1 \- 100 RP 信頼|100を超える RP 信頼 
| ----- |-----| ------ |
|1 \-個の AD FS ノード|WID がサポートされる|WID \- SQL が必要な場合はサポートされません 
|30を超える AD FS ノード|WID \- SQL が必要な場合はサポートされません|WID \- SQL が必要な場合はサポートされません  
  
## <a name="server-placement-and-network-layout-recommendations"></a>サーバーの配置とネットワークレイアウトに関する推奨事項  
このトポロジを展開するには、2つの web アプリケーションプロキシを追加するだけでなく、境界ネットワークからドメインネームシステムへのアクセスも許可する必要があります。これには、@no__t 0DNS @ no__t サーバーと2番目のネットワーク負荷分散 \(NLB @ no__t ホストを指定します。 2番目の NLB ホストは、インターネット @ no__t からアクセス可能なクラスター IP アドレスを使用する NLB クラスターを使用して構成する必要があります。また、企業 @no__t ネットワークで構成した前の NLB クラスターと同じクラスター DNS 名設定を使用する必要があります。 Web アプリケーションプロキシは、Internet @ no__t にアクセス可能な IP アドレスで構成する必要もあります。  
  
次の図は、既に説明した WID トポロジを使用した既存のフェデレーションサーバーファームと、架空の Fabrikam を示しています。 Inc. は、境界 DNS サーバーへのアクセスを提供し、同じクラスター DNS 名を持つ2番目の NLB ホストを no__t @ に追加して、2つの web アプリケーションプロキシ \(wap1 と wap2 @no__t @ no__t を境界ネットワークに追加します。  
  
![WID ファームとプロキシ](media/WIDFarmADFSBlue.gif)  
  
フェデレーションサーバーまたは web アプリケーションプロキシで使用するためのネットワーク環境を構成する方法の詳細については、「AD FS の[要件](AD-FS-Requirements.md)」の「名前解決の要件」セクションを参照してください。 [(WAP)](https://technet.microsoft.com/library/dn383648.aspx)。  
  
## <a name="see-also"></a>関連項目  
[AD FS 展開トポロジの計画](Plan-Your-AD-FS-Deployment-Topology.md)  
[Windows Server 2012 R2 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

