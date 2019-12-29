---
title: AD FS 2.0 フェデレーションプロキシサーバーを移行する
description: AD FS プロキシサーバーを Windows Server 2012 R2 に移行する方法について説明します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 57367cadd3c7ce3d031c6eb3a53c333422543dae
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359372"
---
# <a name="migrate-the-active-directory-federation-services-proxy-server-to-windows-server-2012-r2"></a>Active Directory フェデレーションサービス (AD FS) プロキシサーバーを Windows Server 2012 R2 に移行する

Windows Server 2012 R2 の Active Directory フェデレーションサービス (AD FS) (AD FS) では、フェデレーションサーバープロキシの役割は、Web アプリケーションプロキシと呼ばれる新しいリモートアクセス役割サービスによって処理されます。 Windows Server 2012 R2 では、企業ネットワークの外部からアクセスできるように AD FS を有効にするために、1つまたは複数の Web アプリケーションプロキシを展開できます。 ただし、windows server 2008 R2 または Windows Server 2012 で実行されているフェデレーションサーバープロキシを、Windows Server 2012 R2 で実行されている Web アプリケーションプロキシに移行することはできません。  
  
> [!IMPORTANT]
>  Windows server 2008、Windows Server 2008 R2、または Windows Server 2012 で実行されているフェデレーションサーバープロキシを、windows Server 2012 R2 で実行されている Web アプリケーションプロキシに移行することはサポートされていません。  
  
エクストラネットアクセス用に Windows Server 2012 R2 移行されたファームで AD FS を構成する場合は、AD FS インフラストラクチャの一部として1つ以上の Web アプリケーションプロキシコンピューターを新規に展開する必要があります。  
  
Web アプリケーション プロキシの展開を計画するには、次のトピックの情報を確認できます。  
  
- [Web アプリケーションプロキシインフラストラクチャを計画する](https://technet.microsoft.com/library/dn383648.aspx)  
  
- [Web アプリケーションプロキシサーバーを計画する](https://technet.microsoft.com/library/dn383647.aspx)  
  
  Web アプリケーション プロキシを展開するには、次のトピックの手順を実行できます。  
  
- [Web アプリケーションプロキシインフラストラクチャを構成する](https://technet.microsoft.com/library/dn383644.aspx)  
  
- [Web アプリケーションプロキシサーバーをインストールして構成する](https://technet.microsoft.com/library/dn383662.aspx)  
  
## <a name="next-steps"></a>次のステップ
 [Active Directory フェデレーションサービス (AD FS) の役割サービスを Windows Server 2012 R2  に移行する](migrate-ad-fs-service-role-to-windows-server-r2.md)  
 [AD FS フェデレーションサーバー  を移行する準備をしています](prepare-migrate-ad-fs-server-r2.md)  
 [AD FS フェデレーションサーバー   の移行](migrate-ad-fs-fed-server-r2.md)  
 [Windows Server 2012 R2 への AD FS 移行の検証](verify-ad-fs-migration.md)

