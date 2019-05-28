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
ms.openlocfilehash: 13d8ae8b8f3e4c8160f61284e5fb97e21b6a51b6
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191247"
---
# <a name="mapping-your-deployment-goals-to-an-ad-fs-design"></a>展開目標の AD FS 設計への反映


既存の Active Directory フェデレーション サービスのレビューが完了したら\(AD FS\)展開の目標とする特定のデプロイに関係のある目標、特定の AD FS 設計へのそれらの目標をマップすることができます。 AD FS の詳細については、展開の目標を定義済みを参照してください。 [AD FS 展開目標の特定](Identifying-Your-AD-FS-Deployment-Goals.md)します。  
  
次の表を参照して、組織の展開の目標の AD FS の適切な組み合わせにマップされますが AD FS 設計を確認します。 このテーブルは、このガイドで説明したように、2 つのプライマリ AD FS 設計のみを指します。 ただし、組織のニーズを満たすために AD FS 展開の目標の任意の組み合わせを使用して、ハイブリッドまたはカスタムの AD FS 設計を作成できます。  
  
|AD FS 展開の目的|[Web SSO 設計](Web-SSO-Design.md)|[フェデレーション Web SSO 設計](Federated-Web-SSO-Design.md)|  
|---------------------------------------------------------------------------|----------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|  
|[Active Directory ユーザーに要求に対応するアプリケーションとサービスへのアクセスを提供する](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)|X|はい、アカウント パートナーで|  
|[Active Directory ユーザーに他の組織のアプリケーションとサービスへのアクセスを提供する](Provide-Your-Active-Directory-Users-Access-to-the-Applications-and-Services-of-Other-Organizations.md)|X|はい、アカウント パートナーでのオプション|  
|[要求に対応するアプリケーションやサービスへのアクセスを別の組織のユーザーに提供する](Provide-Users-in-Another-Organization-Access-to-Your-Claims-Aware-Applications-and-Services.md)|〇|〇|  

## <a name="see-also"></a>関連項目
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
  

