---
ms.assetid: eb778f63-f7be-438e-8c5e-1fd9b194b967
title: Web SSO 設計
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 29d50a4d1855e609b6ac9ee627256201074a5033
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190723"
---
# <a name="web-sso-design"></a>Web SSO 設計

Web シングル\-サインオン\-で\(SSO\) Active Directory フェデレーション サービスの設計\(AD FS\)、ユーザーは複数の AD FS にアクセスするには 1 回だけ認証する必要があります\-セキュリティで保護されたアプリケーションまたはサービス。 この設計では、すべてのユーザーが外部ユーザーであり、パートナー組織が存在しないため、フェデレーションの信頼はありません。 通常、次の図に示すように、インターネット経由で 1 つ以上の AD FS で保護されたサービスまたはアプリケーションを個々 の顧客または顧客のアクセスを提供する場合に、この設計を展開します。  
  
![web sso 設計](media/adfs2_WebSSODesign.gif)  
  
Web SSO 設計で組織通常をホストする AD FS\-セキュリティで保護されたアプリケーションまたは境界ネットワーク内のサービスがお客様を分離しやすくなる境界ネットワーク内の顧客アカウントの独立したストアを維持従業員のアカウントのアカウントです。  
  
境界ネットワーク内の顧客のローカル アカウントを管理するには、Active Directory Domain Services を使用して\(AD DS\)、SQL Server、またはカスタム属性ストアです。  
  
この設計は、 [Provide Your Active Directory Users Access to Your Claims-Aware Applications and Services](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)のデプロイ目標と同じです。  
  
計画および Web SSO 設計を展開するのに使用できる詳細なタスクの一覧は、次を参照してください。[チェックリスト。Web SSO 設計を実装する](../../ad-fs/deployment/Checklist--Implementing-a-Web-SSO-Design.md)します。  
  
## <a name="see-also"></a>関連項目
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
