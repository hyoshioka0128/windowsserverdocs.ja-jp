---
ms.assetid: 222e9f93-7c41-4527-8a98-8f7fbc7a58af
title: Windows Server 2012 R2 の AD FS でのフェデレーションサーバープロキシの展開
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: eaf33a1f5398adc1237eaed5c8b418ccbebed9fe
ms.sourcegitcommit: de8fea497201d8f3d995e733dfec1d13a16cb8fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87864170"
---
# <a name="deploying-federation-server-proxies"></a>フェデレーション サーバー プロキシの展開

\( \) Windows Server 2012 R2 の Active Directory フェデレーションサービス (AD FS) AD FS では、フェデレーションサーバープロキシの役割は、Web アプリケーションプロキシと呼ばれる新しいリモートアクセス役割サービスによって処理されます。 AD FS が企業ネットワークの外部からアクセスできるようにします。これは、Windows Server 2012 の AD FS 2.0 や AD FS など、AD FS のレガシバージョンでフェデレーションサーバープロキシを展開するためのものであり、Windows Server 2012 R2 で AD FS 用に1つ以上の web アプリケーションプロキシを展開することができます。  
  
AD FS のコンテキストでは、Web アプリケーションプロキシは AD FS フェデレーションサーバープロキシとして機能します。 さらに、Web アプリケーション プロキシには、企業ネットワーク内部の Web アプリケーション用のリバース プロキシ機能があり、ユーザーは任意のデバイスで企業ネットワーク外部から Web アプリケーションにアクセスできます。 Web アプリケーション プロキシの役割サービスの詳細については、「Web アプリケーション プロキシの概要」を参照してください。  
  
Web アプリケーション プロキシの展開を計画するには、次のトピックの情報を確認できます。  
  
-   [Web アプリケーションプロキシインフラストラクチャ (WAP) を計画する](/previous-versions/orphan-topics/ws.11/dn383648(v=ws.11))  
  
-   [Web アプリケーション プロキシ サーバーを計画する](/previous-versions/orphan-topics/ws.11/dn383647(v=ws.11))  
  
Web アプリケーション プロキシを展開するには、次のトピックの手順を実行できます。  
  
-   [Web アプリケーション プロキシ インフラストラクチャを構成する](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn383644(v=ws.11))  
  
-   [Web アプリケーション プロキシ サーバーをインストールし、構成する](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn383662(v=ws.11))  
  
 
## <a name="see-also"></a>参照 

[AD FS 展開](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS の展開ガイド](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[フェデレーション サーバー ファームの展開](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  
