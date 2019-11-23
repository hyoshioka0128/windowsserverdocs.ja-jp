---
ms.assetid: eb778f63-f7be-438e-8c5e-1fd9b194b967
title: Web SSO 設計
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: d7f52cd36588a1e5de4536a760c38c147dd1e003
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407836"
---
# <a name="web-sso-design"></a>Web SSO 設計

Active Directory フェデレーションサービス (AD FS) \(AD FS\)の SSO\) 設計 \(の Web シングル\-署名\-では、ユーザーは1回だけ認証して、セキュリティで保護された複数のアプリケーションやサービスにアクセスする必要があります。\- この設計では、すべてのユーザーが外部ユーザーであり、パートナー組織が存在しないため、フェデレーションの信頼はありません。 通常、次の図に示すように、1つまたは複数の AD FS セキュリティで保護されたサービスまたはアプリケーションに対して、個々のコンシューマーまたは顧客のアクセスをインターネット経由で提供する場合は、この設計をデプロイします。  
  
![web sso の設計](media/adfs2_WebSSODesign.gif)  
  
Web SSO 設計では、通常、セキュリティで保護されたアプリケーションや境界ネットワーク内のサービス\-AD FS をホストする組織は、境界ネットワーク内に顧客アカウントの個別のストアを保持できます。これにより、従業員アカウントから顧客アカウントを簡単に分離できます。  
  
境界ネットワーク内の顧客のローカルアカウントを管理するには、Active Directory Domain Services \(AD DS\)、SQL Server、またはカスタム属性ストアを使用します。  
  
この設計は、 [Provide Your Active Directory Users Access to Your Claims-Aware Applications and Services](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)のデプロイ目標と同じです。  
  
Web SSO 設計を計画してデプロイするために使用できる詳細なタスクの一覧については、「 [Checklist: Implementing a Web SSO Design](../../ad-fs/deployment/Checklist--Implementing-a-Web-SSO-Design.md)」を参照してください。  
  
## <a name="see-also"></a>参照
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
