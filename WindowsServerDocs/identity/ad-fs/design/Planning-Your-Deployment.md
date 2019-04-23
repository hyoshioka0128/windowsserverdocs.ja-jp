---
ms.assetid: bb9b9e18-bf2f-4115-be77-9a165944db41
title: 展開の計画
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 5c7cec9ad92605f3dc98f8ce8fb7853a7ae61299
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863693"
---
# <a name="planning-your-deployment"></a>展開の計画

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

計画するときクロス\-組織\(フェデレーション\-ベース\)Active Directory フェデレーション サービスを使用してコラボレーション\(AD FS\)、突き止める場合、組織他の組織がインターネット経由でアクセスする Web リソースをホストするか、組織内の従業員は Web リソースへのアクセスを提供します。 この決定は、AD FS を展開する方法に影響し、AD FS インフラストラクチャの計画の基本的なことをします。  
  
> [!NOTE]  
> 組織がフェデレーション契約で果たす役割をすべての当事者が明確に理解するようにしてください。  
  
[フェデレーション Web SSO 設計](Federated-Web-SSO-Design.md)、AD FS の使用条件*アカウント パートナー* \(とも呼ば*id プロバイダー* ADFS管理スナップインで\-で\)と*リソース パートナー* \(とも呼ば*証明書利用者*AD FS 管理スナップインで\-で\)にアカウントをホストしている組織を区別するために役立つ\(アカウント パートナー\) Web をホストする組織から\-ベースのリソース\(リソース パートナー\)します。  
  
[Web SSO Design](Web-SSO-Design.md)では、組織はユーザーに対してアプリケーションへのアクセスを提供するため、アカウント パートナーとリソース パートナー両方の役割を実行します。  
  
次のトピックでは、AD FS のいくつかのパートナーの組織の概念について説明します。 AD FS 展開ガイドを設定して、アカウント パートナー組織と AD FS 展開目標に基づいて、リソース パートナー組織の構成に関する情報が含まれているトピックへのリンクも含まれます。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [AD FS のセキュリティで保護された計画および展開のベスト プラクティス](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)  
  
-   [AD FS との相互運用の計画 1.x](Planning-for-Interoperability-with-AD-FS-1.x.md)  
  
-   [Id 委任を使用する場合](When-to-Use-Identity-Delegation.md)  
  
-   [アカウント パートナー組織で AD FS を展開します。](Deploying-AD-FS-in-the-Account-Partner-Organization-2012.md)  
  
-   [リソース パートナー組織で AD FS を展開します。](Deploying-AD-FS-in-the-Resource-Partner-Organization-2012.md)  
  
## <a name="see-also"></a>関連項目
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)


