---
ms.assetid: 3095e6a7-b562-4c6a-bf29-13b32c133cac
title: "AD FS の SSL 証明書を登録します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 12f544ad0d037c4ae7a9789238186b7ded311bdf
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="enroll-an-ssl-certificate-for-ad-fs"></a>AD FS の SSL 証明書を登録します。

>適用対象: Windows Server 2016、Windows Server 2012 R2

Active Directory フェデレーション サービス \(AD FS\) では、フェデレーション サーバー ファーム内の各フェデレーション サーバーで Secure Socket Layer \(SSL\) サーバー認証証明書が必要です。 同じ証明書は、ファーム内の各フェデレーション サーバーで使用できます。 証明書とその秘密キーを使用できる両方が必要です。 たとえば、.pfx ファイルである場合、証明書とその秘密キーは、Active Directory フェデレーション サービス構成ウィザードに直接ファイルをインポートできます。 この SSL 証明書を次に含める必要があります。  
  
1.  サブジェクト名とサブジェクトの別名 fs.contoso.com など、フェデレーション サービス名を含める必要があります。  
  
2.  サブジェクトの別名は値を含める必要があります**enterpriseregistration**その後ろに、組織のユーザー プリンシパル名 \(UPN\) サフィックスなど**enterpriseregistration.corp.contoso.com**します。  
  
    > [!WARNING]  
    > ワークプ レース ジョイン、デバイス登録サービス \(DRS\) を有効にする予定の場合は、サブジェクト代替名を指定します。  
  
> [!IMPORTANT]  
> 組織で複数の UPN サフィックスを使用すると、DRS を有効にする、SSL 証明書は、各サフィックスに対するサブジェクト代替名エントリを含める必要があります。  
  
## <a name="see-also"></a>参照してください。
[AD FS の展開](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 展開ガイドします。](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[フェデレーション サーバー ファームを展開します。](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  
  

