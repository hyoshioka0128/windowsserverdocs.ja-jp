---
ms.assetid: f0464182-56a2-4bfa-a8c8-7e39c1bd62d3
title: "WID とプロキシを使用してフェデレーション サーバー ファーム"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e372f066fc82b9857d438234b491732a177e24fa
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="federation-server-farm-using-wid-and-proxies"></a>WID とプロキシを使用してフェデレーション サーバー ファーム

>適用対象: Windows Server 2016、Windows Server 2012 R2

Active Directory フェデレーション サービス \(AD FS\) の場合は、この展開トポロジが Windows Internal Database \(WID\) トポロジを使ってフェデレーション サーバー ファームと同じですが、外部ユーザーをサポートするために、境界ネットワークにプロキシ コンピューターを追加します。 このようなプロキシは、フェデレーション サーバー ファームに企業ネットワークの外側に起因するクライアントの認証要求をリダイレクトします。 AD FS の以前のバージョンでは、フェデレーション サーバー プロキシをこのプロキシが呼び出されました。  
  
> [!IMPORTANT]  
> Windows Server 2012 R2 で Active Directory フェデレーション サービス \(AD FS\) でフェデレーション サーバー プロキシの役割は、Web アプリケーション プロキシという新しいリモート アクセス役割サービスによって処理されます。 従来のバージョンの AD FS 2.0 と Windows Server 2012 の AD FS などの AD FS フェデレーション サーバー プロキシの展開の目的であった、企業ネットワークの外部からのアクセシビリティのための AD FS を有効にするには、Windows Server 2012 R2 の AD FS で 1 つまたは複数の Web アプリケーション プロキシを展開できます。  
>   
> AD FS のコンテキストでは、Web アプリケーション プロキシは、AD FS フェデレーション サーバー プロキシとして機能します。 さらに、Web アプリケーション プロキシは、任意のデバイスで企業ネットワークの外部からアクセスできるように、企業ネットワーク内に Web アプリケーションのリバース プロキシ機能を提供します。 詳細については、Web アプリケーション プロキシ役割サービスは、Web アプリケーション プロキシの概要を参照してください。  
>   
> Web アプリケーション プロキシの展開を計画するには、次のトピックの情報を確認できます。  
>   
> -   [インフラストラクチャを計画、Web アプリケーション プロキシ (WAP)](https://technet.microsoft.com/library/dn383648.aspx)  
> -   [Web アプリケーション プロキシ サーバーを計画します。](https://technet.microsoft.com/library/dn383647.aspx)  
  
## <a name="deployment-considerations"></a>展開に関する考慮事項  
このセクションでは、対象となるユーザー、利点、およびこの展開トポロジに関連付けられている制限事項についてさまざまな考慮事項について説明します。  
  
### <a name="who-should-use-this-topology"></a>このトポロジを使用している必要がありますか。  
  
-   内部ユーザーと外部ユーザーの両方を提供する必要がある 100 台以下の構成済みの信頼関係を持つ組織 \ (ユーザーがコンピューターにログオン物理的に企業ネットワークの外側にある) 1 つ sign\ で \(SSO\) アクセス権を持つ、フェデレーション アプリケーションまたはサービス  
  
-   Microsoft Office 365 SSO アクセス権を持つ内部ユーザーと外部ユーザーの両方を提供する必要がある組織  
  
-   外部ユーザーが存在し、冗長なでスケーラブルなサービスを必要とする小規模な組織  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>このトポロジを使用する利点は何ですか。  
  
-   一覧に表示されている同じメリット、[WID フェデレーション サーバー ファームを使用して](Federation-Server-Farm-Using-WID.md)トポロジと外部ユーザーの追加のアクセスを提供することの利点は、  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>このトポロジを使用する場合の制限事項とは何ですか。  
  
-   表示されていると同じ制限、[WID フェデレーション サーバー ファームを使用して](Federation-Server-Farm-Using-WID.md)トポロジ  

||1 \-100 RP 信頼|100 を超える RP 信頼 
| ----- |-----| ------ |
|1 \-30 AD FS ノード|WID のサポート|WID を使用してサポートされていません \-必要な SQL 
|複数の 30 AD FS ノード|WID を使用してサポートされていません \-必要な SQL|WID を使用してサポートされていません \-必要な SQL  
  
## <a name="server-placement-and-network-layout-recommendations"></a>サーバーの配置とネットワーク レイアウトの推奨事項  
このトポロジでは、次の 2 つの Web アプリケーション プロキシを追加するだけの展開には、境界ネットワークの場合、ドメイン ネーム システム \(DNS\) サーバーおよび 2 番目のネットワーク負荷分散 \(NLB\) ホストへのアクセスも提供を確認する必要があります。 NLB クラスターとは限らないからアクセス可能なクラスター IP アドレスを使用すると、2 番目の NLB ホストを構成する必要があり、企業ネットワーク \(fs.fabrikam.com\) で構成した前の NLB クラスターとして同じクラスター DNS 名の設定を使用する必要があります。 Web アプリケーション プロキシとは限らないからアクセス可能な IP アドレスを持つも構成する必要があります。  
  
同じクラスター DNS 名 \(fs.fabrikam.com\) と 2 番目の NLB ホストを追加する次の図は、WID トポロジ上記に記載されている架空の企業で Fabrikam, Inc. が境界 DNS サーバーへのアクセスを提供する方法と、既存のフェデレーション サーバー ファームし、2 つの Web アプリケーション プロキシを追加 \(wap1 and wap2\) 境界ネットワークにします。  
  
![WID ファームとプロキシ](media/WIDFarmADFSBlue.gif)  
  
フェデレーション サーバーまたは Web アプリケーション プロキシを使用するため、ネットワーク環境を構成する方法の詳細については、「名前解決の要件」を参照してください。セクション[AD FS の要件](AD-FS-Requirements.md)と[Web アプリケーション プロキシ インフラストラクチャ (WAP) を計画](https://technet.microsoft.com/library/dn383648.aspx)します。  
  
## <a name="see-also"></a>参照してください。  
[AD FS 展開トポロジを計画します。](Plan-Your-AD-FS-Deployment-Topology.md)  
[Windows Server 2012 R2 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

