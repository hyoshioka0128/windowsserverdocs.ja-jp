---
title: AD FS 2.0 フェデレーションプロキシサーバーを移行する
description: AD FS プロキシサーバーを Windows Server 2012 R2 に移行する方法について説明します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.openlocfilehash: a8345f587e7fe4119e46dc390e9240dee6071ce6
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87940835"
---
# <a name="migrate-the-active-directory-federation-services-proxy-server-to-windows-server-2012-r2"></a>Active Directory フェデレーションサービス (AD FS) プロキシサーバーを Windows Server 2012 R2 に移行する

Windows Server 2012 R2 の Active Directory フェデレーションサービス (AD FS) (AD FS) では、フェデレーションサーバープロキシの役割は、Web アプリケーションプロキシと呼ばれる新しいリモートアクセス役割サービスによって処理されます。 Windows Server 2012 R2 では、企業ネットワークの外部からアクセスできるように AD FS を有効にするために、1つまたは複数の Web アプリケーションプロキシを展開できます。 ただし、windows server 2008 R2 または Windows Server 2012 で実行されているフェデレーションサーバープロキシを、Windows Server 2012 R2 で実行されている Web アプリケーションプロキシに移行することはできません。

> [!IMPORTANT]
>  Windows server 2008、Windows Server 2008 R2、または Windows Server 2012 で実行されているフェデレーションサーバープロキシを、windows Server 2012 R2 で実行されている Web アプリケーションプロキシに移行することはサポートされていません。

エクストラネットアクセス用に Windows Server 2012 R2 移行されたファームで AD FS を構成する場合は、AD FS インフラストラクチャの一部として1つ以上の Web アプリケーションプロキシコンピューターを新規に展開する必要があります。

Web アプリケーション プロキシの展開を計画するには、次のトピックの情報を確認できます。

- [Web アプリケーション プロキシ インフラストラクチャを計画する](/previous-versions/orphan-topics/ws.11/dn383648(v=ws.11))

- [Web アプリケーション プロキシ サーバーを計画する](/previous-versions/orphan-topics/ws.11/dn383647(v=ws.11))

  Web アプリケーション プロキシを展開するには、次のトピックの手順を実行できます。

- [Web アプリケーション プロキシ インフラストラクチャを構成する](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn383644(v=ws.11))

- [Web アプリケーション プロキシ サーバーをインストールし、構成する](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn383662(v=ws.11))

## <a name="next-steps"></a>次の手順
 [Active Directory フェデレーションサービス (AD FS) 役割サービスを Windows server 2012 R2 に移行](migrate-ad-fs-service-role-to-windows-server-r2.md)[する AD FS フェデレーションサーバーの移行の準備](prepare-migrate-ad-fs-server-r2.md) [AD FS フェデレーションサーバーの移行](migrate-ad-fs-fed-server-r2.md) [Windows Server 2012 R2 への AD FS の移行の検証](verify-ad-fs-migration.md)
