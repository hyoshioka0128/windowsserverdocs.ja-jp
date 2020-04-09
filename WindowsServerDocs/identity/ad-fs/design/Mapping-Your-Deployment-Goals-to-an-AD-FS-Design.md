---
ms.assetid: 68979914-8a1c-465a-bd37-08df30722d69
title: 展開目標の AD FS 設計への反映
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 4154f46bdb1a7b3a2c81eba6882a6a095a16ee45
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853055"
---
# <a name="mapping-your-deployment-goals-to-an-ad-fs-design"></a>展開目標の AD FS 設計への反映


既存の Active Directory フェデレーションサービス (AD FS) AD FS \(を確認し\) デプロイの目標を確認した後、配置に関連する目標を決定したら、それらの目標を特定の AD FS 設計にマップできます。 定義済みの展開の目標 AD FS の詳細については、「 [AD FS の展開目標の特定](Identifying-Your-AD-FS-Deployment-Goals.md)」を参照してください。  
  
次の表を使用して、組織の AD FS の展開目標の適切な組み合わせに対応する AD FS 設計を決定します。 次の表は、このガイドで説明されている2つの主要な AD FS デザインのみを示しています。 ただし、組織のニーズを満たすために、AD FS 展開目標の任意の組み合わせを使用して、ハイブリッドまたはカスタムの AD FS 設計を作成することができます。  
  
|AD FS 展開の目標|[Web SSO 設計](Web-SSO-Design.md)|[フェデレーション Web SSO 設計](Federated-Web-SSO-Design.md)|  
|---------------------------------------------------------------------------|----------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|  
|[Active Directory ユーザーに要求に対応するアプリケーションとサービスへのアクセスを提供する](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)|いいえ|はい、アカウント パートナーで|  
|[Active Directory ユーザーに他の組織のアプリケーションとサービスへのアクセスを提供する](Provide-Your-Active-Directory-Users-Access-to-the-Applications-and-Services-of-Other-Organizations.md)|いいえ|はい、アカウント パートナーでのオプション|  
|[要求に対応するアプリケーションやサービスへのアクセスを別の組織のユーザーに提供する](Provide-Users-in-Another-Organization-Access-to-Your-Claims-Aware-Applications-and-Services.md)|はい|はい|  

## <a name="see-also"></a>参照
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
  

