---
title: AD FS 2.0 を Windows Server 2012 R2 に移行することを確認する
description: AD FS サーバーを Windows Server 2012 R2 に移行する方法について説明します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.openlocfilehash: 35216baafefc5b304e1fc27b48f99b3afcde32fc
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87940449"
---
# <a name="verify-the-ad-fs-20-migration-to-windows-server-2012-r2"></a>AD FS 2.0 を Windows Server 2012 R2 に移行することを確認する

Active Directory フェデレーションサービス (AD FS) ファームから Windows Server 2012 R2 への同じサーバーの移行を完了したら、次の手順を使用して、ファーム内のフェデレーションサーバーが動作していることを確認できます。つまり、同じネットワーク上のすべてのクライアントが、federtation サーバーに接続できます。

この手順を実行するには、少なくとも **Users**、**Backup Operators**、**Power Users**、または **Administrators** グループのメンバーであるか、そのメンバーと同等の権限が必要になります。

### <a name="to-verify-that-a-federation-server-is-operational"></a>フェデレーション サーバーが正常に動作していることを確認するには

1.  ブラウザーウィンドウを開き、アドレスバーにフェデレーションサーバーの名前を入力し、それをに追加して `federationmetadata/2007-06/federationmetadata.xml` 、フェデレーションサービスのメタデータエンドポイントを参照します。 たとえば、のように `https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml` なります。

ブラウザー ウィンドウでフェデレーション サーバーのメタデータを表示してみて、SSL のエラーや警告が表示されない場合、フェデレーション サーバーは正常に動作しています。

2. AD FS サインイン ページを閲覧することもできます (この場合には、フェデレーション サービス名の末尾に「`adfs/ls/idpinitiatedsignon.htm`」を付加して、たとえば「`https://fs.contoso.com/adfs/ls/idpinitiatedsignon.htm`」と入力します)。  このように入力すると、ドメイン管理者の資格情報を使用してサインインできる AD FS サインイン ページが表示されます。

> [!IMPORTANT]
>  ブラウザーのローカルイントラネットゾーンにフェデレーションサービス名 (など) を追加することによって、フェデレーションサーバーの役割を信頼するようにブラウザーの設定を構成し `https://fs.contoso.com` ます。

## <a name="next-steps"></a>次の手順
 [Active Directory フェデレーションサービス (AD FS) 役割サービスを Windows Server 2012 R2 に移行](migrate-ad-fs-service-role-to-windows-server-r2.md)[する AD FS フェデレーション AD FS サーバーの移行の準備](prepare-migrate-ad-fs-server-r2.md) [Migrating the AD FS Federation Server](migrate-ad-fs-fed-server-r2.md) [AD FS フェデレーション](migrate-fed-server-proxy-r2.md)サーバーを移行するフェデレーションサーバープロキシの移行
