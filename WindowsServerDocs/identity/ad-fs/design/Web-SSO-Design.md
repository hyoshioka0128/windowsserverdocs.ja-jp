---
ms.assetid: eb778f63-f7be-438e-8c5e-1fd9b194b967
title: Web SSO 設計
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 7112fe6983a6292c57fc489c959b1edeb0c13c7b
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87949856"
---
# <a name="web-sso-design"></a>Web SSO 設計

\- \- Active Directory フェデレーションサービス (AD FS) AD FS の Web シングルサインオン \( SSO 設計では \) \( \) 、ユーザーは、セキュリティで保護された AD FS 複数のアプリケーションまたはサービスにアクセスするために1回だけ認証する必要があり \- ます。 この設計では、すべてのユーザーが外部ユーザーであり、パートナー組織が存在しないため、フェデレーションの信頼はありません。 通常、次の図に示すように、1つまたは複数の AD FS セキュリティで保護されたサービスまたはアプリケーションに対して、個々のコンシューマーまたは顧客のアクセスをインターネット経由で提供する場合は、この設計をデプロイします。

![web sso の設計](media/adfs2_WebSSODesign.gif)

Web SSO 設計では、通常、 \- 境界ネットワークでセキュリティで保護されたアプリケーションまたはサービス AD FS をホストする組織は、境界ネットワーク内に顧客アカウントを個別に格納することができます。これにより、従業員アカウントから顧客アカウントを分離しやすくなります。

境界ネットワーク内の顧客のローカルアカウントは \( 、Active Directory Domain Services AD DS \) 、SQL Server、またはカスタム属性ストアのいずれかを使用して管理できます。

この設計は、 [Provide Your Active Directory Users Access to Your Claims-Aware Applications and Services](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)のデプロイ目標と同じです。

Web SSO 設計を計画してデプロイするために使用できる詳細なタスクの一覧については、「 [Checklist: Implementing a Web SSO Design](../../ad-fs/deployment/Checklist--Implementing-a-Web-SSO-Design.md)」を参照してください。

## <a name="see-also"></a>参照
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
