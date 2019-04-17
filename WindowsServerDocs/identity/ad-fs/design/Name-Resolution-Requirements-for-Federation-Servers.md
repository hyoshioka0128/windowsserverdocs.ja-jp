---
ms.assetid: 74ef34c8-e13f-499b-b2bb-952ad7036622
title: "フェデレーション サーバーの名前解決の要件"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 74701cbaa403611b081942f016b21db1c0b3ff70
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="name-resolution-requirements-for-federation-servers"></a>フェデレーション サーバーの名前解決の要件

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

企業ネットワーク上のクライアント コンピューターは、アプリケーションまたは Active Directory フェデレーション サービス \(AD FS\) によって保護されている Web サービスにアクセスするときに、最初のフェデレーション サーバーを認証する必要があります。 認証方法の 1 つは、企業ネットワーク クライアントが Windows 統合認証を通じて、ローカルのフェデレーション サーバーにアクセスします。  
  
## <a name="configure-corporate-dns"></a>企業 DNS を構成します。  
ローカルのフェデレーション サーバーで Windows 統合認証を通じて正常な名前解決が発生することができるように、アカウント パートナーの企業ネットワーク内のドメイン ネーム システム \(DNS\) をフェデレーション サーバー クラスターの IP アドレスにフェデレーション サーバーの完全修飾ドメイン名 \(FQDN\) ホスト名を解決する新しいホスト \(A\) リソース レコードの構成する必要があります。  
  
次の図では、特定のシナリオでは、このタスクを実現する方法を確認できます。 このシナリオでは、Microsoft Network Load Balancing \(NLB\) は、既存のフェデレーション サーバー ファームの 1 つのクラスター FQDN 名と 1 つのクラスター IP アドレスを提供します。  
  
![名の要件](media/adfs2_deploy_single_fs.gif)  
  
NLB を使用する FQDN をクラスターまたはクラスター IP アドレスを構成する方法については、次を参照してください。[クラスター パラメーターを指定して](https://go.microsoft.com/fwlink/?LinkId=75282)します。  
  
企業 DNS をフェデレーション サーバーを構成する方法については、次を参照してください[ホスト (&) #40; を追加。A & #41 です。リソース レコードを会社の DNS にフェデレーション サーバーに](../../ad-fs/deployment/Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md)します。  
  
境界ネットワーク内のフェデレーション サーバー プロキシを構成する方法については、次を参照してください。[フェデレーション サーバー プロキシの名前解決要件](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)します。  
  

## <a name="see-also"></a>参照してください。
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)
