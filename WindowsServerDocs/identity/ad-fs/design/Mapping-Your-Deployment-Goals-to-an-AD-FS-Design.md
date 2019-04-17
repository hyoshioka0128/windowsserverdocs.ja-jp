---
ms.assetid: 68979914-8a1c-465a-bd37-08df30722d69
title: "AD FS 設計への展開目標のマッピング"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 048bce75c52895b2d9e215bdccef9cb13dc23533
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="mapping-your-deployment-goals-to-an-ad-fs-design"></a>AD FS 設計への展開目標のマッピング

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

既存の Active Directory フェデレーション サービス \(AD FS\) 展開の目標の確認が終了すると、デプロイに関係のある目標を決定する、これらの目標を特定の AD FS 設計にマップできます。 AD FS の詳細については、展開の目標を定義済みを参照してください[AD FS 展開目標の特定](Identifying-Your-AD-FS-Deployment-Goals.md)します。  
  
AD FS の適切な組み合わせ、組織の展開の目標にマップする AD FS 設計を決定するのにには、次の表を使用します。 次の表は、このガイドで説明するように、2 つのプライマリ AD FS 設計のみを指します。 ただし、組織のニーズを満たすために、AD FS 展開目標の任意の組み合わせを使用してハイブリッドまたはカスタム AD FS 設計を作成することができます。  
  
|AD FS 展開目標|[Web SSO 設計](Web-SSO-Design.md)|[フェデレーション Web SSO 設計](Federated-Web-SSO-Design.md)|  
|---------------------------------------------------------------------------|----------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|  
|[Active Directory ユーザー アクセスを提供する、クレーム対応アプリケーションとサービス](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)|違います|アカウント パートナーで、[はい]|  
|[アプリケーションや他の組織のサービスに、Active Directory ユーザーのアクセスを提供します。](Provide-Your-Active-Directory-Users-Access-to-the-Applications-and-Services-of-Other-Organizations.md)|違います|[はい、アカウント パートナーでは省略可能]|  
|[要求対応のアプリケーションとサービスをユーザーに他の組織がアクセスを提供します。](Provide-Users-in-Another-Organization-Access-to-Your-Claims-Aware-Applications-and-Services.md)|うん|うん|  

## <a name="see-also"></a>参照してください。
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)
  

