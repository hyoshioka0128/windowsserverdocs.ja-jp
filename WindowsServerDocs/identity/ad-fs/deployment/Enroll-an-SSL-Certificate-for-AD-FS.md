---
ms.assetid: 3095e6a7-b562-4c6a-bf29-13b32c133cac
title: AD FS 用に SSL 証明書を登録する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: efa7c7aee848a5bbb68d3ce7140e135d37c2161d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408361"
---
# <a name="enroll-an-ssl-certificate-for-ad-fs"></a>AD FS 用に SSL 証明書を登録する

Active Directory フェデレーションサービス (AD FS) \(AD FS @ no__t には、フェデレーションサーバーファーム内の各フェデレーションサーバーで、Secure Socket Layer \(SSL @ no__t サーバー認証用の証明書が必要です。 ファーム内の各フェデレーションサーバーで同じ証明書を使用できます。 証明書と秘密キーが両方とも利用可能であることが必要です。 たとえば、証明書と秘密キーが .pfx ファイルに保存されている場合は、そのファイルを Active Directory フェデレーション サービス構成ウィザードに直接インポートできます。 この SSL 証明書には、以下が含まれている必要があります。  
  
1.  サブジェクト名とサブジェクトの別名には、fs.contoso.com などのフェデレーションサービス名が含まれている必要があります。  
  
2.  サブジェクトの別名には、 **enterpriseregistration**の値が含まれている必要があります。その後にユーザープリンシパル名 \(upn @ no__t-2 サフィックス (たとえば、 **enterpriseregistration.corp.contoso.com**) を指定します。  
  
    > [!WARNING]  
    > デバイス登録サービスを有効にする予定の場合は、サブジェクトの別名を指定します \(DRS @ no__t-1 Workplace Join。  
  
> [!IMPORTANT]  
> 組織で複数の UPN サフィックスを使用していて、DRS を有効にする予定がある場合、SSL 証明書には各サフィックスのサブジェクト代替名のエントリが含まれている必要があります。  
  
## <a name="see-also"></a>関連項目
[AD FS 展開](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 展開ガイド](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[フェデレーション サーバー ファームの展開](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  
  

