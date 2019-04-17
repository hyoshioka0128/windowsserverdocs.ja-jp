---
title: "AD FS 2.0 フェデレーション サーバーを移行します。"
description: "Windows Server 2012 R2 への AD FS サーバーの移行についてを説明します。"
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 0a3e8e444f715fe2ae0f0ccd858d90e8664be00c
ms.sourcegitcommit: 03ce78a1624dbd7f4e6abf2ec1ef185b55de29a1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/12/2017
---
# <a name="verify-the-ad-fs-20-migration-to-windows-server-2012-r2"></a>確認、AD FS 2.0 に移行する Windows Server 2012 R2

Active Directory フェデレーション サービス (AD FS) ファームから Windows Server 2012 R2 の同じサーバーの移行を完了したら、ファーム内のフェデレーション サーバーが運用; であることを確認、次の手順を使用することができます。つまり、同じネットワーク上のどのクライアントが、federtation サーバーに到達できること。  
  
メンバーシップ**ユーザー**、 **Backup Operators**、 **Power Users**、**管理者**相当するもので、ローカル コンピューターでは、この手順を完了するために必要な最低限またはします。
  
### <a name="to-verify-that-a-federation-server-is-operational"></a>フェデレーション サーバーが動作可能であることを確認するには  
  
1.  ブラウザー ウィンドウを開くと、アドレス バーで、フェデレーション サーバー名を入力およびと追加`federationmetadata/2007-06/federationmetadata.xml`フェデレーション サービスのメタデータ エンドポイントを閲覧します。 たとえば、`https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml`します。  
  
ブラウザー ウィンドウには、SSL のエラーや警告なしのフェデレーション サーバーのメタデータを表示、された場合、フェデレーション サーバーは動作します。  
  
2.  AD FS サインイン ページを閲覧することもできます (、フェデレーション サービス名の末尾`adfs/ls/idpinitiatedsignon.htm`、たとえば、 `https://fs.contoso.com/adfs/ls/idpinitiatedsignon.htm`)。  AD FS サインイン ページのドメイン管理者の資格情報でサインインすることができますが表示されます。  
  
> [!IMPORTANT]
>  フェデレーション サービス名を追加することで、フェデレーション サーバーの役割を信頼するブラウザーの設定を構成することを確認 (たとえば、 `https://fs.contoso.com`)、ブラウザーのローカル イントラネット ゾーンにします。  
  
## <a name="next-steps"></a>次の手順
 [Windows Server 2012 R2 への Active Directory フェデレーション サービスの役割サービスを移行します。](migrate-ad-fs-service-role-to-windows-server-r2.md)   
 [AD FS フェデレーション サーバーの移行の準備](prepare-migrate-ad-fs-server-r2.md)  
 [AD FS フェデレーション サーバーの移行](migrate-ad-fs-fed-server-r2.md)   
 [AD FS フェデレーション サーバー プロキシの移行](migrate-fed-server-proxy-r2.md)   
