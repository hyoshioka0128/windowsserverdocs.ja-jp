---
ms.assetid: 09f335bb-896a-45dd-adc2-f215b8fba828
title: "フェデレーション Web SSO 設計"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b85f49ac0556bf9b3542a23514d7fcbf82d2d88e
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="federated-web-sso-design"></a>フェデレーション Web SSO 設計

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Active Directory フェデレーション サービス \(AD FS\) でフェデレーション Web Single\-Sign\-On \(SSO\) 設計では、複数のファイアウォール、境界ネットワーク、およびサーバーの名前 \/解像度にまたがるセキュリティで保護された通信-インターネット ルーティング インフラストラクチャ全体に加えします。  
  
この設計は、通常、2 つの組織の同意を 1 つの組織でユーザーを許可するようにフェデレーションの信頼関係を作成する場合に使用 \ (、アカウント パートナー organization\) Web ベースのアプリケーションやサービスで、他の組織内の AD FS によって保護されたアクセスを \ (リソース パートナー organization\)。  
  
つまり、フェデレーションの信頼関係は business\ レベルの合意またはパートナーシップを 2 つの組織間での具現化したものです。 次の図に示すように、その結果、エンド ツー エンドのフェデレーションのシナリオでは、2 つの企業間にフェデレーション信頼関係を確立できます。  
  
![フェデレーション Web sso](media/adfs2_FederatedWebSSODesign.gif)  
  
図の特定方法の矢印はフェデレーションの方向を表して信頼 — などの Windows の信頼の方向-常に、フォレストのアカウント側をポイントします。 つまり、その認証フローは、アカウント パートナー組織からリソース パートナー組織。  
  
このフェデレーション Web SSO 設計で 2 台のフェデレーション サーバー \ (Fabrikam の 1 つと、他方 Contoso\) のユーザー アカウントからの認証要求でルーティング Fabrikam Contoso で Web ベース アプリケーションまたはサービスにします。  
  
> [!NOTE]  
> セキュリティを高めるため、インターネットから直接アクセスされているフェデレーション サーバーに要求をリレーするフェデレーション サーバー プロキシを使用することができます。  
  
この例では、Fabrikam は、id、またはアカウント、プロバイダーです。 フェデレーション Web SSO 設計の Fabrikam の部分では、次の AD FS 展開目標を使用します。  
  
-   [アプリケーションや他の組織のサービスに、Active Directory ユーザーのアクセスを提供します。](Provide-Your-Active-Directory-Users-Access-to-the-Applications-and-Services-of-Other-Organizations.md)  
  
Contoso は、リソース プロバイダーです。 フェデレーション Web SSO 設計の Contoso の部分では、次の AD FS 展開目標を達成します。  
  
-   [要求対応のアプリケーションとサービスをユーザーに他の組織がアクセスを提供します。](Provide-Users-in-Another-Organization-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
-   [Active Directory ユーザー アクセスを提供する、クレーム対応アプリケーションとサービス](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
計画およびフェデレーション Web SSO 設計の展開に使用できる詳細なタスクの一覧は、次を参照してください。[チェックリスト: Implementing a Federated Web SSO Design](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md)します。  
  
## <a name="see-also"></a>参照してください。
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)
