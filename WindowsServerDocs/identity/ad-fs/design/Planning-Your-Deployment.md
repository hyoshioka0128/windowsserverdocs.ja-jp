---
ms.assetid: bb9b9e18-bf2f-4115-be77-9a165944db41
title: 展開の計画
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 607dc34c8f44d8d96a8dc0c9d1ed004edc799167
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407997"
---
# <a name="planning-your-deployment"></a>展開の計画

クロス\-組織 \(フェデレーション\-、Active Directory フェデレーションサービス (AD FS) \(AD FS を使用して\) コラボレーションを計画している場合は、まず、組織がインターネット経由で他の組織からアクセスする Web リソースをホストするか、組織内の従業員の Web リソースへのアクセスを提供するかを決定します。\) この決定は AD FS の展開方法に影響し、AD FS インフラストラクチャの計画の基礎となります。  
  
> [!NOTE]  
> 組織がフェデレーション契約で果たす役割をすべての当事者が明確に理解するようにしてください。  
  
[フェデレーション WEB SSO 設計](Federated-Web-SSO-Design.md)では、AD FS は、\) の AD FS 管理スナップ\-で*id プロバイダー*とも呼ばれる*アカウントパートナー* \(のような用語を*使用し、* \(の AD FS 管理スナップ\-で*証明書利用者*と呼ばれることもあり\) アカウントをホストする組織を、Web \(ベースのリソースをホストしている組織から区別するのに役立ち\)リソースパートナー\)。\-\(  
  
[Web SSO Design](Web-SSO-Design.md)では、組織はユーザーに対してアプリケーションへのアクセスを提供するため、アカウント パートナーとリソース パートナー両方の役割を実行します。  
  
次のトピックでは、AD FS パートナー組織の概念について説明します。 また、AD FS の展開目標に基づいてアカウントパートナー組織およびリソースパートナー組織のセットアップと構成に関する情報が記載されている、AD FS 展開ガイドのトピックへのリンクも含まれています。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [AD FS のセキュリティを考慮した設計と展開のベスト プラクティス](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)  
  
-   [AD FS 1.x との相互運用性の計画](Planning-for-Interoperability-with-AD-FS-1.x.md)  
  
-   [Id 委任を使用する場合](When-to-Use-Identity-Delegation.md)  
  
-   [アカウント パートナー組織での AD FS の展開](Deploying-AD-FS-in-the-Account-Partner-Organization-2012.md)  
  
-   [リソース パートナー組織での AD FS の展開](Deploying-AD-FS-in-the-Resource-Partner-Organization-2012.md)  
  
## <a name="see-also"></a>参照
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)


