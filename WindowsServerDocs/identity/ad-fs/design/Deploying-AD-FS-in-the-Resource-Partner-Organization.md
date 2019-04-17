---
ms.assetid: 41d6b897-1e72-4522-aad6-eece1154a154
title: "リソース パートナー組織で AD FS の展開"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4a556c07e7d6e0bec4c947ea9d1a75eef9964cef
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="deploying-ad-fs-in-the-resource-partner-organization"></a>リソース パートナー組織で AD FS の展開

>適用対象: Windows Server 2016、Windows Server 2012 R2

The resource partner organization in Active Directory Federation Services \(AD FS\) represents the organization whose Web servers may be protected by a resource\-side federation server. The federation server at the resource partner uses the security tokens that are produced by the account partner to provide claims to the Web servers that are located in the resource partner.  
  
In scenarios in which you need to provide access to federated services or applications to many different users—when some users reside in different organizations—you can configure the resource federation server so that you can deploy multiple account partners.  
  
For more information about how to set up and configure a resource partner organization, see [Checklist: Configuring the Resource Partner Organization](../../ad-fs/deployment/Checklist--Configuring-the-Resource-Partner-Organization.md).  
  
## <a name="in-this-section"></a>このセクションで  
  
-   [リソース パートナーのフェデレーション サーバーの役割を確認します。](Review-the-Role-of-the-Federation-Server-in-the-Resource-Partner.md)  
  
-   [リソース パートナーのフェデレーション サーバー プロキシの役割を確認します。](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Resource-Partner.md)  
  
-   [リソース パートナーのフェデレーション アプリケーション戦略を決定します。](Determine-Your-Federated-Application-Strategy-in-the-Resource-Partner.md)  
  

## <a name="see-also"></a>参照してください。
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)
