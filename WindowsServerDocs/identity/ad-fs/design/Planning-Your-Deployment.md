---
ms.assetid: bb9b9e18-bf2f-4115-be77-9a165944db41
title: "展開の計画"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 5c7cec9ad92605f3dc98f8ce8fb7853a7ae61299
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="planning-your-deployment"></a>展開の計画

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Active Directory フェデレーション サービス \(AD FS\) を使用したクロス組織 \(federation\-based\) コラボレーションを計画する場合は、まず、組織は、インターネット経由で他の組織でアクセスする Web リソースをホストする場合、または、組織内従業員用の Web リソースへのアクセスを提供する場合を判断します。 この判断は、AD FS を展開する方法に影響し、AD FS インフラストラクチャの計画の基礎します。  
  
> [!NOTE]  
> 組織がフェデレーション契約で果たす役割をすべての当事者が明確に理解することを確認します。  
  
[Federated Web SSO Design](Federated-Web-SSO-Design.md)、AD FS の使用条件*アカウント パートナー* \ (とも呼ば*id プロバイダー*で AD FS 管理 snap\ 詳細な) と*リソース パートナー* \ (とも呼ば*証明書利用者*で AD FS 管理 snap\ 詳細な) アカウントをホストしている組織を区別しやすく \(the account partner\) Web ベース リソースをホストする組織から \(the resource partner\) します。  
  
[Web SSO 設計](Web-SSO-Design.md)、に対してアプリケーションへのアクセス権を持つユーザーを提供するため、組織がアカウント パートナーとリソース パートナーの両方の役割で動作します。  
  
次のトピックでは、パートナー組織で AD FS の一部について説明します。 設定して、アカウント パートナー組織と AD FS 展開目標に基づく、リソース パートナー組織の構成に関する情報が含まれている AD FS 展開ガイドのトピックへのリンクも含まれます。  
  
## <a name="in-this-section"></a>このセクションで  
  
-   [セキュリティで保護の計画と AD FS の展開のベスト プラクティス](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)  
  
-   [AD FS と相互運用性の計画 1.x](Planning-for-Interoperability-with-AD-FS-1.x.md)  
  
-   [Id 委任を使用する場合](When-to-Use-Identity-Delegation.md)  
  
-   [アカウント パートナー組織で AD FS の展開](Deploying-AD-FS-in-the-Account-Partner-Organization-2012.md)  
  
-   [リソース パートナー組織で AD FS の展開](Deploying-AD-FS-in-the-Resource-Partner-Organization-2012.md)  
  
## <a name="see-also"></a>参照してください。
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)


