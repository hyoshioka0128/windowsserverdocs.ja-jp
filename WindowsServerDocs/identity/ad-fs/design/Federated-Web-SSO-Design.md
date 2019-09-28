---
ms.assetid: 09f335bb-896a-45dd-adc2-f215b8fba828
title: フェデレーション Web SSO 設計
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 6a3e7eb6c42c8190da799c88c1e947e6aef1c29f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408106"
---
# <a name="federated-web-sso-design"></a>フェデレーション Web SSO 設計

フェデレーション Web Single @ no__t-0Sign @ no__t On \(SSO @ no__t design on Active Directory フェデレーションサービス (AD FS) \(AD FS @ no__t-5 では、複数のファイアウォール、境界ネットワーク、および名前 @ no__t-6resolution にまたがるセキュリティで保護された通信が必要です。サーバー-インターネットルーティングインフラストラクチャ全体に加えて、  
  
通常、この設計は、2つの組織がフェデレーションの信頼関係を作成することに同意し、1つの @no__t 組織内のユーザーが、アカウントパートナー組織 @ no__t を使用して、Web @ no__t ベースのアプリケーションまたはサービスにアクセスできるようにするときに使用されます。AD FS、もう一方の組織では、リソースパートナー組織 @ no__t-4 @no__t ます。  
  
言い換えると、フェデレーションの信頼関係は、2つの組織間での business @ no__t 具現化レベルアグリーメントまたはパートナーシップの一部です。 次の図に示すように、2つの企業間にフェデレーションの信頼関係を確立すると、@ no__t-0to @ no__t-1end フェデレーションシナリオが終了します。  
  
![フェデレーション web sso](media/adfs2_FederatedWebSSODesign.gif)  
  
図の1つの @ no__t-0way 矢印は、フェデレーションの信頼の方向を示しています。これは、Windows の信頼の方向と同様に、常にフォレストのアカウント側を指します。 これは、認証がアカウント パートナー組織からリソース パートナー組織に対して行われることを意味します。  
  
このフェデレーション Web SSO 設計では、Fabrikam の2つのフェデレーションサーバー @no__t と Contoso @ no__t の他のサーバーが、Contoso の Web @ no__t ベースのアプリケーションまたはサービスである Fabrikam のユーザーアカウントからの認証要求をルーティングします。  
  
> [!NOTE]  
> セキュリティを強化するために、フェデレーションサーバープロキシを使用して、インターネットから直接アクセスできないフェデレーションサーバーに要求をリレーできます。  
  
この例では、Fabrikam は、ID (アカウント) プロバイダーになります。 フェデレーション Web SSO 設計の Fabrikam の部分では、次の AD FS 展開の目的を使用します。  
  
-   [Active Directory ユーザーに他の組織のアプリケーションとサービスへのアクセスを提供する](Provide-Your-Active-Directory-Users-Access-to-the-Applications-and-Services-of-Other-Organizations.md)  
  
Contoso はリソース プロバイダーになります。 フェデレーション Web SSO 設計の Contoso の部分では、次の AD FS 展開の目標を達成します。  
  
-   [要求に対応するアプリケーションやサービスへのアクセスを別の組織のユーザーに提供する](Provide-Users-in-Another-Organization-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
-   [Active Directory ユーザーに要求に対応するアプリケーションとサービスへのアクセスを提供する](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
フェデレーション Web SSO 設計の計画と展開に使用できる詳細なタスクの一覧については、「@no__t」を参照してください。フェデレーション Web SSO デザイン @ no__t-0 を実装します。  
  
## <a name="see-also"></a>関連項目
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
