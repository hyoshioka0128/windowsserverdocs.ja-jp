---
ms.assetid: 3095e6a7-b562-4c6a-bf29-13b32c133cac
title: AD FS 用に SSL 証明書を登録する
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 2d24e5593af2d12359d4e2acd5fc93df334730b8
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87962826"
---
# <a name="enroll-an-ssl-certificate-for-ad-fs"></a>AD FS 用に SSL 証明書を登録する

Active Directory フェデレーションサービス (AD FS) \( AD FS に \) は、 \( \) フェデレーションサーバーファーム内の各フェデレーションサーバーで Secure sockets Layer SSL サーバー認証用の証明書が必要です。 ファーム内の各フェデレーションサーバーで同じ証明書を使用できます。 証明書と秘密キーが両方とも利用可能であることが必要です。 たとえば、証明書と秘密キーが .pfx ファイルに保存されている場合は、そのファイルを Active Directory フェデレーション サービス構成ウィザードに直接インポートできます。 この SSL 証明書には、以下が含まれている必要があります。

1.  サブジェクト名とサブジェクトの別名には、fs.contoso.com などのフェデレーションサービス名が含まれている必要があります。

2.  サブジェクトの別名には、enterpriseregistration.corp.contoso.com のように、組織のユーザープリンシパル名 UPN サフィックスが続く値**enterpriseregistration**が含まれている必要があり \( \) ます**enterpriseregistration.corp.contoso.com**。

    > [!WARNING]
    > デバイス登録サービス DRS を Workplace Join に有効にする予定の場合は、サブジェクトの別名を指定し \( \) ます。

> [!IMPORTANT]
> 組織で複数の UPN サフィックスを使用していて、DRS を有効にする予定がある場合、SSL 証明書には各サフィックスのサブジェクト代替名のエントリが含まれている必要があります。

## <a name="see-also"></a>参照
[AD FS 展開](../../ad-fs/AD-FS-Deployment.md)

[Windows Server 2012 R2 AD FS の展開ガイド](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)

[フェデレーション サーバー ファームの展開](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)



