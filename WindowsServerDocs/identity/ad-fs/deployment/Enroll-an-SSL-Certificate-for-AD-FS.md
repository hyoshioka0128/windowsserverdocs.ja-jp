---
ms.assetid: 3095e6a7-b562-4c6a-bf29-13b32c133cac
title: AD FS 用に SSL 証明書を登録する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e80927f2670614d2949f4e67cc158319f05c5fa0
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192153"
---
# <a name="enroll-an-ssl-certificate-for-ad-fs"></a>AD FS 用に SSL 証明書を登録する

Active Directory フェデレーション サービス\(AD FS\)の Secure Socket Layer 証明書が必要\(SSL\)フェデレーション サーバー ファーム内の各フェデレーション サーバーでのサーバー認証。 同じ証明書は、ファーム内の各フェデレーション サーバーで使用できます。 証明書と秘密キーが両方とも利用可能であることが必要です。 たとえば、証明書と秘密キーが .pfx ファイルに保存されている場合は、そのファイルを Active Directory フェデレーション サービス構成ウィザードに直接インポートできます。 この SSL 証明書には、以下が含まれている必要があります。  
  
1.  サブジェクト名とサブジェクト代替名には、fs.contoso.com など、フェデレーション サービス名を含める必要があります。  
  
2.  サブジェクトの別名は、値を含める必要があります**enterpriseregistration**ですが、ユーザー プリンシパル名に続く\(UPN\) 、組織のサフィックス**enterpriseregistration.corp.contoso.com**します。  
  
    > [!WARNING]  
    > デバイス登録サービスを有効にする場合、サブジェクト代替名を指定\(DRS\)ワークプ レース ジョインします。  
  
> [!IMPORTANT]  
> 組織で複数の UPN サフィックスを使用して、DRS を有効にする場合は、SSL 証明書は、各サフィックスに対するサブジェクト代替名エントリを含める必要があります。  
  
## <a name="see-also"></a>関連項目
[AD FS 展開](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 展開ガイドします。](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[フェデレーション サーバー ファームの展開](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  
  

