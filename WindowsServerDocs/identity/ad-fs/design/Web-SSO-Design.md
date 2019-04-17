---
ms.assetid: eb778f63-f7be-438e-8c5e-1fd9b194b967
title: "Web SSO 設計"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 1b8344594c9fc477ed8424c716ec8d7f7fd91ef3
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="web-sso-design"></a>Web SSO 設計

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Active Directory フェデレーション サービス \(AD FS\) でシングル Sign\-で \(SSO\) 設計 Web ユーザー認証が必要 1 回だけに複数の AD FS\ で保護されたアプリケーションやサービスにアクセスします。 この設計ではすべてのユーザーが外部、およびフェデレーションの信頼が存在しないためパートナー組織ではありません。 通常、次の図に示すように、インターネット経由で 1 つ以上の AD FS で保護されたサービスまたはアプリケーションへの個々 の顧客または顧客アクセスを提供するときに、この設計を展開します。  
  
![web sso 設計](media/adfs2_WebSSODesign.gif)  
  
Web SSO 設計、通常 AD FS\ で保護されたアプリケーションをホストする組織または境界ネットワーク内のサービスは、顧客アカウントと従業員アカウントを分離しやすく境界ネットワーク内の顧客アカウントの独立したストアを管理できます。  
  
Active Directory Domain Services \(AD DS\)、SQL サーバー、またはカスタム属性ストアを使用して、境界ネットワーク内の顧客のローカル アカウントを管理できます。  
  
この設計の展開の目標と一致している[提供 Your Active Directory Users Access to Your Claims-aware Applications and Services](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)します。  
  
計画し、Web SSO 設計を展開するのに使用できる詳細なタスクの一覧は、次を参照してください。[チェックリスト: Web SSO 設計の実装](../../ad-fs/deployment/Checklist--Implementing-a-Web-SSO-Design.md)します。  
  
## <a name="see-also"></a>参照してください。
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)
