---
ms.assetid: 09f335bb-896a-45dd-adc2-f215b8fba828
title: フェデレーション Web SSO 設計
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 9915a2942c9336d5aeb7776169d2e51491c22909
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853145"
---
# <a name="federated-web-sso-design"></a>フェデレーション Web SSO 設計

Active Directory フェデレーションサービス (AD FS) \(AD FS のフェデレーション Web シングル\-署名\-は \(SSO\) 設計において、インターネットルーティングインフラストラクチャ全体に加えて、複数のファイアウォール、境界ネットワーク、および名前\) 解決サーバーにまたがるセキュリティで保護された通信を必要とします。\-  
  
通常、この設計は、2つの組織がフェデレーションの信頼関係の作成に同意するときに使用されます。これにより、1つの組織内のユーザーは、リソースパートナー組織 \(\)他の組織の AD FS によって保護されている Web\-ベースのアプリケーションまたはサービスにアクセス\) \(できます。  
  
つまり、フェデレーションの信頼関係は、2つの組織間のビジネス\-レベルアグリーメントまたはパートナーシップの具現化です。 次の図に示すように、2つの企業間にフェデレーションの信頼関係を確立すると、\-エンドフェデレーションシナリオにエンド\-が生じます。  
  
![フェデレーション web sso](media/adfs2_FederatedWebSSODesign.gif)  
  
図の1つの\-方向の矢印は、フェデレーションの信頼の方向を示します。これは、Windows の信頼の方向と同様に、常にフォレストのアカウント側を指します。 これは、認証はアカウント パートナー組織からリソース パートナー組織の方向に向かうことを示します。  
  
このフェデレーション Web SSO 設計では、2つのフェデレーションサーバー (Fabrikam 内) と Contoso の別のフェデレーションサーバー \(、Fabrikam のユーザーアカウントから Contoso の Web\-ベースのアプリケーションまたはサービスに対する認証要求をルーティング\) ます。  
  
> [!NOTE]  
> セキュリティを強化するために、フェデレーションサーバープロキシを使用して、インターネットから直接アクセスできないフェデレーションサーバーに要求をリレーできます。  
  
この例では、Fabrikam は、ID (アカウント) プロバイダーになります。 フェデレーション Web SSO 設計の Fabrikam の部分では、次の AD FS 展開の目的を使用します。  
  
-   [Active Directory ユーザーに他の組織のアプリケーションとサービスへのアクセスを提供する](Provide-Your-Active-Directory-Users-Access-to-the-Applications-and-Services-of-Other-Organizations.md)  
  
Contoso はリソース プロバイダーになります。 フェデレーション Web SSO 設計の Contoso の部分では、次の AD FS 展開の目標を達成します。  
  
-   [要求に対応するアプリケーションやサービスへのアクセスを別の組織のユーザーに提供する](Provide-Users-in-Another-Organization-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
-   [Active Directory ユーザーに要求に対応するアプリケーションとサービスへのアクセスを提供する](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
フェデレーション Web SSO 設計を計画してデプロイするために使用できる詳細なタスクの一覧については、「 [Checklist: Implementing a Federated Web SSO Design](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md)」を参照してください。  
  
## <a name="see-also"></a>参照
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
