---
title: AD FS 2.0 フェデレーション プロキシ サーバーを移行します。
description: Windows Server 2012 R2 への AD FS プロキシ サーバーの移行に関する情報を提供します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 18ce084ec7d1b602dfca913372d6a0e279671a6e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867413"
---
# <a name="migrate-the-active-directory-federation-services-proxy-server-to-windows-server-2012-r2"></a>Windows Server 2012 R2 への Active Directory フェデレーション サービス プロキシ サーバーを移行します。

Windows Server 2012 R2 で、Active Directory フェデレーション サービス (AD FS) でのフェデレーション サーバー プロキシの役割は、Web アプリケーション プロキシという新しいリモート アクセス役割サービスによって処理されます。 AD FS に企業のネットワークの外部からのアクセスを有効にするには、Windows Server 2012 R2 では、1 つまたは複数の Web アプリケーション プロキシをデプロイできます。 ただし、Windows Server 2012 R2 で実行されている Web アプリケーション プロキシには、Windows Server 2008 R2 または Windows Server 2012 で実行されているフェデレーション サーバー プロキシに移行することはできません。  
  
> [!IMPORTANT]
>  Windows Server 2012 R2 で実行されている Web アプリケーション プロキシには、Windows Server 2008、Windows Server 2008 R2、または Windows Server 2012 で実行されているフェデレーション サーバー プロキシの移行がサポートされていません。  
  
エクストラネット アクセス用の Windows Server 2012 R2 の移行されたファーム内の AD FS を構成する場合は、AD FS インフラストラクチャの一部として 1 つまたは複数の Web アプリケーション プロキシ コンピューターの新規に展開を行う必要があります。  
  
Web アプリケーション プロキシの展開を計画するには、次のトピックの情報を確認できます。  
  
-   [Web アプリケーション プロキシ インフラストラクチャを計画します。](https://technet.microsoft.com/library/dn383648.aspx)  
  
-   [Web アプリケーション プロキシ サーバーを計画します。](https://technet.microsoft.com/library/dn383647.aspx)  
  
 Web アプリケーション プロキシを展開するには、次のトピックの手順を実行できます。  
  
-   [Web アプリケーション プロキシ インフラストラクチャを構成します。](https://technet.microsoft.com/library/dn383644.aspx)  
  
-   [インストールして、Web アプリケーション プロキシ サーバーの構成](https://technet.microsoft.com/library/dn383662.aspx)  
  
## <a name="next-steps"></a>次の手順
 [Windows Server 2012 R2 への Active Directory フェデレーション サービス役割サービスを移行します。](migrate-ad-fs-service-role-to-windows-server-r2.md)   
 [AD FS フェデレーション サーバーの移行の準備](prepare-migrate-ad-fs-server-r2.md)   
 [AD FS フェデレーション サーバーの移行](migrate-ad-fs-fed-server-r2.md)    
 [Windows Server 2012 R2 への AD FS の移行の検証](verify-ad-fs-migration.md)

