---
title: AD FS 2.0 フェデレーション サーバーを移行します。
description: Windows Server 2012 R2 への AD FS サーバーの移行に関する情報を提供します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 38e44ab2f803d8ec8940dbba7574a9f37389112a
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444461"
---
# <a name="verify-the-ad-fs-20-migration-to-windows-server-2012-r2"></a>確認、AD FS 2.0 に移行する Windows Server 2012 R2

Windows Server 2012 R2 に Active Directory フェデレーション サービス (AD FS) ファームを同じサーバーの移行を完了すると、ファーム内のフェデレーション サーバーが運用; であることを確認、次の手順を使用することができます。つまり、同じネットワーク上のクライアントが、federtation サーバーに到達できることです。  
  
この手順を実行するには、少なくとも **Users**、 **Backup Operators**、 **Power Users**、または **Administrators** グループのメンバーであるか、そのメンバーと同等の権限が必要になります。
  
### <a name="to-verify-that-a-federation-server-is-operational"></a>フェデレーション サーバーが正常に動作していることを確認するには  
  
1.  ブラウザー ウィンドウを開いて、アドレス バーにフェデレーション サーバー名を入力し、追加`federationmetadata/2007-06/federationmetadata.xml`フェデレーション サービスのメタデータ エンドポイントを参照します。 たとえば、`https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml`します。  
  
ブラウザー ウィンドウでフェデレーション サーバーのメタデータを表示してみて、SSL のエラーや警告が表示されない場合、フェデレーション サーバーは正常に動作しています。  
  
2. AD FS サインイン ページを閲覧することもできます (この場合には、フェデレーション サービス名の末尾に「`adfs/ls/idpinitiatedsignon.htm`」を付加して、たとえば「`https://fs.contoso.com/adfs/ls/idpinitiatedsignon.htm`」と入力します)。  このように入力すると、ドメイン管理者の資格情報を使用してサインインできる AD FS サインイン ページが表示されます。  
  
> [!IMPORTANT]
>  ブラウザーのローカル インターネット ゾーンにフェデレーション サービス名 (`https://fs.contoso.com` など) を追加し、フェデレーション サーバーの役割を信頼するようにブラウザーの設定を変更してください。  
  
## <a name="next-steps"></a>次の手順
 [Windows Server 2012 R2 への Active Directory フェデレーション サービス役割サービスを移行します。](migrate-ad-fs-service-role-to-windows-server-r2.md)   
 [AD FS フェデレーション サーバーの移行の準備](prepare-migrate-ad-fs-server-r2.md)  
 [AD FS フェデレーション サーバーの移行](migrate-ad-fs-fed-server-r2.md)   
 [AD FS フェデレーション サーバー プロキシの移行](migrate-fed-server-proxy-r2.md)   
