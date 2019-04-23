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
ms.openlocfilehash: 1b8344594c9fc477ed8424c716ec8d7f7fd91ef3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852803"
---
# <a name="web-sso-design"></a>Web SSO 設計

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

Web シングル\-サインオン\-で\(SSO\) Active Directory フェデレーション サービスの設計\(AD FS\)、ユーザーは複数の AD FS にアクセスするには 1 回だけ認証する必要があります\-セキュリティで保護されたアプリケーションまたはサービス。 この設計では、すべてのユーザーが外部ユーザーであり、パートナー組織が存在しないため、フェデレーションの信頼はありません。 通常、次の図に示すように、インターネット経由で 1 つ以上の AD FS で保護されたサービスまたはアプリケーションを個々 の顧客または顧客のアクセスを提供する場合に、この設計を展開します。  
  
![web sso 設計](media/adfs2_WebSSODesign.gif)  
  
Web SSO 設計で組織通常をホストする AD FS\-セキュリティで保護されたアプリケーションまたは境界ネットワーク内のサービスがお客様を分離しやすくなる境界ネットワーク内の顧客アカウントの独立したストアを維持従業員のアカウントのアカウントです。  
  
境界ネットワーク内の顧客のローカル アカウントを管理するには、Active Directory Domain Services を使用して\(AD DS\)、SQL Server、またはカスタム属性ストアです。  
  
この設計は、 [Provide Your Active Directory Users Access to Your Claims-Aware Applications and Services](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)のデプロイ目標と同じです。  
  
計画および Web SSO 設計を展開するのに使用できる詳細なタスクの一覧は、次を参照してください。[チェックリスト。Web SSO 設計を実装する](../../ad-fs/deployment/Checklist--Implementing-a-Web-SSO-Design.md)します。  
  
## <a name="see-also"></a>関連項目
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)
