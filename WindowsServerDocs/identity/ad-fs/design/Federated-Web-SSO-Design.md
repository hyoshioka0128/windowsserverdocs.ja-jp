---
ms.assetid: 09f335bb-896a-45dd-adc2-f215b8fba828
title: フェデレーション Web SSO デザイン
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: f3f34aca7f7a316ff714b88209e3bf81de420ecb
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87942766"
---
# <a name="federated-web-sso-design"></a>フェデレーション Web SSO デザイン

Active Directory フェデレーションサービス (AD FS) AD FS でのフェデレーション Web シングル \- サイン \- オン SSO 設計では、 \( \) \( \) \- インターネットルーティングインフラストラクチャ全体に加えて、複数のファイアウォール、境界ネットワーク、および名前解決サーバーにまたがるセキュリティで保護された通信が行われます。

通常、この設計は、2つの組織がフェデレーションの信頼関係の作成に同意するときに使用されます。これにより、ある組織のユーザー \( が、 \) リソースパートナー組織の \- 他の組織で AD FS によって保護された Web ベースのアプリケーションまたはサービスにアクセスできるように \( \) なります。

つまり、フェデレーションの信頼関係は、 \- 2 つの組織間のビジネスレベルアグリーメントまたはパートナーシップの具現化です。 次の図に示すように、2つの企業間のフェデレーションの信頼関係を確立すると、エンドツー \- \- エンドのフェデレーションシナリオになります。

![フェデレーション web sso](media/adfs2_FederatedWebSSODesign.gif)

図の一方向の矢印は、 \- フェデレーションの信頼の方向を示しています。これは、Windows の信頼の方向と同様に、常にフォレストのアカウント側を指します。 これは、認証がアカウント パートナー組織からリソース パートナー組織に対して行われることを意味します。

このフェデレーション Web SSO 設計では、Fabrikam の2つのフェデレーションサーバーと Contoso の別のフェデレーションサーバーが、 \( \) fabrikam のユーザーアカウントから \- contoso の Web ベースのアプリケーションまたはサービスに対する認証要求をルーティングします。

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
