---
ms.assetid: f0464182-56a2-4bfa-a8c8-7e39c1bd62d3
title: WID とプロキシを使用するフェデレーション サーバー ファーム
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e372f066fc82b9857d438234b491732a177e24fa
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860393"
---
# <a name="federation-server-farm-using-wid-and-proxies"></a>WID とプロキシを使用するフェデレーション サーバー ファーム

>適用先:Windows Server 2016、Windows Server 2012 R2

Active Directory フェデレーション サービスの場合は、この配置トポロジ\(AD FS\)が Windows Internal Database のフェデレーション サーバー ファームと同じ\(WID\)トポロジをプロキシ コンピューターを追加します、。外部ユーザーをサポートするために境界ネットワーク。 これらのプロキシでは、フェデレーション サーバー ファームに、企業ネットワーク外から取得したクライアントの認証要求をリダイレクトします。 AD FS の以前のバージョンでこれらのプロキシにフェデレーション サーバー プロキシが呼び出されました。  
  
> [!IMPORTANT]  
> Active Directory フェデレーション サービスで\(AD FS\)で Windows Server 2012 R2 では、フェデレーション サーバー プロキシの役割は、Web アプリケーション プロキシという新しいリモート アクセス役割サービスによって処理されます。 AD FS の以前のバージョンの AD FS 2.0 および Windows Server 2012 の AD FS などの AD FS でフェデレーション サーバー プロキシの展開の目的であった、企業ネットワークの外部からのアクセスを有効にするには、A の 1 つまたは複数の web アプリケーション プロキシをデプロイすることができます。Windows Server 2012 R2 の D FS します。  
>   
> AD FS のコンテキストでは、Web アプリケーション プロキシは、AD FS フェデレーション サーバー プロキシとして機能します。 さらに、Web アプリケーション プロキシには、企業ネットワーク内部の Web アプリケーション用のリバース プロキシ機能があり、ユーザーは任意のデバイスで企業ネットワーク外部から Web アプリケーションにアクセスできます。 Web アプリケーション プロキシの役割サービスの詳細については、「Web アプリケーション プロキシの概要」を参照してください。  
>   
> Web アプリケーション プロキシの展開を計画するには、次のトピックの情報を確認できます。  
>   
> -   [インフラストラクチャを計画する Web アプリケーション プロキシ (WAP)](https://technet.microsoft.com/library/dn383648.aspx)  
> -   [Web アプリケーション プロキシ サーバーを計画します。](https://technet.microsoft.com/library/dn383647.aspx)  
  
## <a name="deployment-considerations"></a>展開に関する考慮事項  
このセクションでは、対象となるユーザー、利点、およびこの配置トポロジに関連付けられている制限事項についてさまざまな考慮事項について説明します。  
  
### <a name="who-should-use-this-topology"></a>このトポロジを使用する必要がありますか。  
  
-   組織の内部ユーザーと外部ユーザーの両方を指定する必要がある 100 以下の構成済みの信頼関係を持つ\(企業ネットワークの外部に物理的に配置されているコンピューターにログオンしたユーザーは\)1 回サインオン\-で\(SSO\)フェデレーション アプリケーションまたはサービスへのアクセス  
  
-   Microsoft Office 365 に SSO アクセス権を持つ、内部ユーザーと外部ユーザーの両方を提供する必要がある組織  
  
-   外部ユーザーが、重複した、スケーラブルなサービスを必要とする小規模な組織  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>このトポロジを使用する利点とは  
  
-   場合と同じメリットがあります、 [WID フェデレーション サーバー ファームを使用して](Federation-Server-Farm-Using-WID.md)トポロジ、および外部ユーザーを追加のアクセスを提供するための特典  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>このトポロジを使用する場合の制限事項を挙げてください。  
  
-   表示されていると同じ制限、 [WID フェデレーション サーバー ファームを使用して](Federation-Server-Farm-Using-WID.md)トポロジ  

||1 \- 100 の RP 信頼|100 を超える RP 信頼 
| ----- |-----| ------ |
|1 \- 30年の AD FS ノード|WID のサポート|WID を使用してサポートされていません\-のために必要な SQL 
|複数の 30年の AD FS ノード|WID を使用してサポートされていません\-のために必要な SQL|WID を使用してサポートされていません\-のために必要な SQL  
  
## <a name="server-placement-and-network-layout-recommendations"></a>サーバーの配置とネットワーク レイアウトの推奨事項  
2 つの web アプリケーション プロキシを追加するだけでなく、このトポロジをデプロイする必要がありますを確認することを境界ネットワークもにアクセスできるように、ドメイン ネーム システム\(DNS\)サーバーと 2 番目ネットワーク負荷分散に\(NLB\)ホスト。 2 番目の NLB ホストは、インターネットを使用する NLB クラスターを構成する必要があります\-企業ネットワーク上に構成されて以前の NLB クラスターと同じクラスター DNS 名の設定を使用する必要がありますアクセス可能なクラスター IP アドレス、およびその\(fs.fabrikam.com\)します。 インターネットと web アプリケーション プロキシを構成する必要があることも\-アクセス可能な IP アドレス。  
  
次の図は、以前に説明した WID トポロジと架空の会社の Fabrikam, Inc. が境界の DNS サーバーへのアクセスを提供する方法は、既存のフェデレーション サーバー ファームを同じクラスター DNS 名2番目のNLBホストを追加します\(fs.fabrikam.com\)、2 つの web アプリケーション プロキシを追加および\(wap1 と wap2\)境界ネットワークにします。  
  
![Wid とプロキシ](media/WIDFarmADFSBlue.gif)  
  
フェデレーション サーバーまたは web アプリケーション プロキシを使用するため、ネットワーク環境を構成する方法の詳細については、「名前解決の要件」を参照してください。 セクション[AD FS の要件](AD-FS-Requirements.md)と[Web の計画アプリケーション プロキシ インフラストラクチャ (WAP)](https://technet.microsoft.com/library/dn383648.aspx)します。  
  
## <a name="see-also"></a>関連項目  
[AD FS 展開トポロジを計画します。](Plan-Your-AD-FS-Deployment-Topology.md)  
[Windows Server 2012 R2 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

