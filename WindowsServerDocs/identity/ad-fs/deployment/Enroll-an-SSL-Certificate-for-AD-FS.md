---
ms.assetid: 3095e6a7-b562-4c6a-bf29-13b32c133cac
title: AD FS 用に SSL 証明書を登録する
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 6f7af40f23c3fa3bd0a31ecb74b11013133a4b32
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855435"
---
# <a name="enroll-an-ssl-certificate-for-ad-fs"></a>AD FS 用に SSL 証明書を登録する

Active Directory フェデレーションサービス (AD FS) \(AD FS\) には、フェデレーションサーバーファーム内の各フェデレーションサーバーで SSL \(サーバー認証に Secure Socket Layer の証明書が必要です。\) ファーム内の各フェデレーションサーバーで同じ証明書を使用できます。 証明書とその秘密キーの両方を使用可能にする必要があります。 たとえば、証明書と秘密キーが .pfx ファイルに保存されている場合は、そのファイルを Active Directory フェデレーション サービス構成ウィザードに直接インポートできます。 この SSL 証明書には次の情報が必要です。  
  
1.  サブジェクト名とサブジェクトの別名には、fs.contoso.com などのフェデレーションサービス名が含まれている必要があります。  
  
2.  サブジェクトの別名には、 **enterpriseregistration**の値が含まれている必要があります。その後に、組織のユーザープリンシパル名 \(UPN\) サフィックス (たとえば、 **enterpriseregistration.corp.contoso.com**) を指定します。  
  
    > [!WARNING]  
    > デバイス登録サービス \(DRS\) を Workplace Join に有効にする予定の場合は、サブジェクトの別名を指定します。  
  
> [!IMPORTANT]  
> 組織で複数の UPN サフィックスを使用していて、DRS を有効にする予定がある場合、SSL 証明書には各サフィックスのサブジェクト代替名のエントリが含まれている必要があります。  
  
## <a name="see-also"></a>参照
[AD FS 展開](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 展開ガイド](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[フェデレーション サーバー ファームの展開](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  
  

