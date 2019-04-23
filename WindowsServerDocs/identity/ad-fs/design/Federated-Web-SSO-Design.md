---
ms.assetid: 09f335bb-896a-45dd-adc2-f215b8fba828
title: フェデレーション Web SSO 設計
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b85f49ac0556bf9b3542a23514d7fcbf82d2d88e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865143"
---
# <a name="federated-web-sso-design"></a>フェデレーション Web SSO 設計

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

フェデレーション Web シングル\-サインオン\-で\(SSO\) Active Directory フェデレーション サービスの設計\(AD FS\)にまたがる複数のファイアウォールでのセキュリティで保護された通信境界ネットワーク、および名前\-解決サーバー: インターネット ルーティング インフラストラクチャ全体だけでなく。  
  
この設計は通常、1 つの組織でユーザーを許可するフェデレーションの信頼関係を作成する 2 つの組織が同意するときに使用\(アカウント パートナー組織\)Web にアクセスする\-ベースのアプリケーションまたはサービス、他の組織内の AD FS によってセキュリティで保護されている\(リソース パートナー組織\)します。  
  
つまり、フェデレーションの信頼関係は、ビジネスの具体化\-レベルの合意またはパートナーシップを 2 つの組織との間。 その結果、最終的に、2 つの企業間のフェデレーションの信頼関係を確立するには、次の図に示すように\-に\-エンド フェデレーション シナリオ。  
  
![フェデレーション web sso](media/adfs2_FederatedWebSSODesign.gif)  
  
1 つ\-方向の矢印の図には、フェデレーションの方向を表して信頼-Windows 信頼の方向と同様、常にフォレストのアカウント側を指します。 これは、認証がアカウント パートナー組織からリソース パートナー組織に対して行われることを意味します。  
  
このフェデレーション Web SSO 設計で 2 つのフェデレーション サーバー \(Fabrikam および Contoso の他に 1 つずつ\)Fabrikam Web へのユーザー アカウントからの認証要求をルーティング\-ベースのアプリケーションまたはサービスでは Contoso。  
  
> [!NOTE]  
> 追加のセキュリティは、インターネットから直接アクセスできないフェデレーション サーバーに要求をリレーするフェデレーション サーバー プロキシを使用できます。  
  
この例では、Fabrikam は、ID (アカウント) プロバイダーになります。 フェデレーション Web SSO 設計の Fabrikam の部分では、次の AD FS 展開目標を使用します。  
  
-   [アプリケーションと他の組織のサービスに、Active Directory ユーザーのアクセスを提供します。](Provide-Your-Active-Directory-Users-Access-to-the-Applications-and-Services-of-Other-Organizations.md)  
  
Contoso はリソース プロバイダーになります。 フェデレーション Web SSO 設計の Contoso の部分では、次の AD FS 展開目標を実現します。  
  
-   [クレーム対応アプリケーションとサービスをユーザーに別の組織のアクセスを提供します。](Provide-Users-in-Another-Organization-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
-   [クレーム対応アプリケーションとサービスに、Active Directory ユーザーのアクセスを提供します。](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
計画およびフェデレーション Web SSO 設計を展開するのに使用できる詳細なタスクの一覧は、次を参照してください。[チェックリスト。フェデレーション Web SSO 設計を実装する](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md)します。  
  
## <a name="see-also"></a>関連項目
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)
