---
title: "AD FS 2.0 フェデレーション プロキシ サーバーを移行します。"
description: "Windows Server 2012 R2 への AD FS プロキシ サーバーの移行について説明します。"
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 33ab29fd5efdb0bdd1fe25580e3f4434071e1c7d
ms.sourcegitcommit: 03ce78a1624dbd7f4e6abf2ec1ef185b55de29a1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/12/2017
---
# <a name="migrate-the-active-directory-federation-services-proxy-server-to-windows-server-2012-r2"></a>Windows Server 2012 R2 への Active Directory フェデレーション サービス プロキシ サーバーを移行します。

Windows Server 2012 R2 では、Active Directory フェデレーション サービス (AD FS) でフェデレーション サーバー プロキシの役割は、Web アプリケーション プロキシという新しいリモート アクセス役割サービスによって処理されます。 企業のネットワークの外部からのアクセシビリティのための AD FS を有効にする Windows Server 2012 R2 で 1 つまたは複数の Web アプリケーション プロキシを展開できます。 ただし、Windows Server 2012 R2 で実行されている Web アプリケーション プロキシには、Windows Server 2008 R2 または Windows Server 2012 で実行されているフェデレーション サーバー プロキシを移行することはできません。  
  
> [!IMPORTANT]
>  Windows Server 2012 R2 で実行されている Web アプリケーション プロキシには、Windows Server 2008、Windows Server 2008 R2、または Windows Server 2012 で実行されているフェデレーション サーバー プロキシの移行がサポートされていません。  
  
Windows Server 2012 R2 の移行されたファームでエクストラネット アクセス用に AD FS を構成する場合、AD FS インフラストラクチャの一部として 1 つまたは複数の Web アプリケーション プロキシ コンピューターの新しい展開を行う必要があります。  
  
Web アプリケーション プロキシの展開を計画するには、次のトピックの情報を確認できます。  
  
-   [Web アプリケーション プロキシ インフラストラクチャを計画します。](https://technet.microsoft.com/en-us/library/dn383648.aspx)  
  
-   [Web アプリケーション プロキシ サーバーを計画します。](https://technet.microsoft.com/en-us/library/dn383647.aspx)  
  
 Web アプリケーション プロキシを展開するには、ことができます、次のトピックの手順に従います。  
  
-   [Web アプリケーション プロキシ インフラストラクチャを構成します。](https://technet.microsoft.com/en-us/library/dn383644.aspx)  
  
-   [インストールして Web アプリケーション プロキシ サーバーを構成します。](https://technet.microsoft.com/en-us/library/dn383662.aspx)  
  
## <a name="next-steps"></a>次の手順
 [Windows Server 2012 R2 への Active Directory フェデレーション サービスの役割サービスを移行します。](migrate-ad-fs-service-role-to-windows-server-r2.md)   
 [AD FS フェデレーション サーバーの移行の準備](prepare-migrate-ad-fs-server-r2.md)   
 [AD FS フェデレーション サーバーの移行](migrate-ad-fs-fed-server-r2.md)    
 [Windows Server 2012 R2 への AD FS の移行の検証](verify-ad-fs-migration.md)

