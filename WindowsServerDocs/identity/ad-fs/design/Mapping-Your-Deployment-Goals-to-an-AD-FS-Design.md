---
ms.assetid: 68979914-8a1c-465a-bd37-08df30722d69
title: 展開目標の AD FS 設計への反映
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 048bce75c52895b2d9e215bdccef9cb13dc23533
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866823"
---
# <a name="mapping-your-deployment-goals-to-an-ad-fs-design"></a>展開目標の AD FS 設計への反映

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

既存の Active Directory フェデレーション サービスのレビューが完了したら\(AD FS\)展開の目標とする特定のデプロイに関係のある目標、特定の AD FS 設計へのそれらの目標をマップすることができます。 AD FS の詳細については、展開の目標を定義済みを参照してください。 [AD FS 展開目標の特定](Identifying-Your-AD-FS-Deployment-Goals.md)します。  
  
次の表を参照して、組織の展開の目標の AD FS の適切な組み合わせにマップされますが AD FS 設計を確認します。 このテーブルは、このガイドで説明したように、2 つのプライマリ AD FS 設計のみを指します。 ただし、組織のニーズを満たすために AD FS 展開の目標の任意の組み合わせを使用して、ハイブリッドまたはカスタムの AD FS 設計を作成できます。  
  
|AD FS 展開の目的|[Web SSO 設計](Web-SSO-Design.md)|[フェデレーション Web SSO 設計](Federated-Web-SSO-Design.md)|  
|---------------------------------------------------------------------------|----------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|  
|[クレーム対応アプリケーションとサービスに、Active Directory ユーザーのアクセスを提供します。](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)|X|はい、アカウント パートナーで|  
|[アプリケーションと他の組織のサービスに、Active Directory ユーザーのアクセスを提供します。](Provide-Your-Active-Directory-Users-Access-to-the-Applications-and-Services-of-Other-Organizations.md)|X|はい、アカウント パートナーでのオプション|  
|[クレーム対応アプリケーションとサービスをユーザーに別の組織のアクセスを提供します。](Provide-Users-in-Another-Organization-Access-to-Your-Claims-Aware-Applications-and-Services.md)|〇|〇|  

## <a name="see-also"></a>関連項目
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)
  

