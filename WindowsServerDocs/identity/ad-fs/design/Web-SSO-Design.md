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

Active Directory フェデレーションサービス (AD FS) \(AD FS @ no__t-5 で \(SSO @ no__t design の Web Single @ no__t-0Sign @ no__t-1On 認証する必要があります。ユーザーは、複数の AD FS @ no__t-6secured アプリケーションまたはサービスにアクセスするために1回だけ認証する必要があります。 この設計では、すべてのユーザーが外部ユーザーであり、パートナー組織が存在しないため、フェデレーションの信頼はありません。 通常、次の図に示すように、1つまたは複数の AD FS セキュリティで保護されたサービスまたはアプリケーションに対して、個々のコンシューマーまたは顧客のアクセスをインターネット経由で提供する場合は、この設計をデプロイします。  
  
![web sso の設計](media/adfs2_WebSSODesign.gif)  
  
Web SSO 設計では、通常、境界ネットワークで AD FS @ no__t で保護されたアプリケーションまたはサービスをホストする組織は、境界ネットワーク内に顧客アカウントを個別に格納することができます。これにより、顧客アカウントの分離が容易になります。従業員アカウント。  
  
境界ネットワーク内の顧客のローカルアカウントは、Active Directory Domain Services \(AD DS @ no__t-1、SQL Server、またはカスタム属性ストアのいずれかを使用して管理できます。  
  
この設計は、 [Provide Your Active Directory Users Access to Your Claims-Aware Applications and Services](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)のデプロイ目標と同じです。  
  
Web SSO 設計を計画してデプロイするために使用できる詳細なタスクの一覧については、「@no__t」チェックリストを参照してください。Web SSO デザイン @ no__t を実装します。  
  
## <a name="see-also"></a>関連項目
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
