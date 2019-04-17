---
ms.assetid: 1b3a03c0-5558-4177-9b2f-e9d6ce3271cd
title: "アカウント パートナー内のフェデレーション サーバー プロキシの役割を確認します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: d2b60ce593c2ca7eb902595ee6a42850cb7605d9
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="review-the-role-of-the-federation-server-proxy-in-the-account-partner"></a>アカウント パートナー内のフェデレーション サーバー プロキシの役割を確認します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Active Directory フェデレーション サービス \(AD FS\) 内のアカウント パートナー組織の境界ネットワーク内のフェデレーション サーバー プロキシの主な役割は、インターネット経由でログオンしているクライアント コンピューターから認証資格情報を収集して、アカウント パートナー組織の企業ネットワーク内に配置されたフェデレーション サーバーにそれらの資格情報を渡すにです。 クライアント コンピューターのアカウントは、アカウント パートナーの属性ストアに格納されます。  
  
フェデレーション サーバー プロキシは、アカウント パートナー組織のニーズを満たすように構成方法に応じて、次の役割の 1 つ以上のも動作できます。  
  
-   セキュリティ トークンをリレー: フェデレーション サーバーがクライアント コンピューターにトークンがリレーし、フェデレーション サーバー プロキシにセキュリティ トークンを発行します。 セキュリティ トークンを使用すると、そのクライアント コンピューターの特定の証明書利用者のパーティへのアクセスを提供します。  
  
-   資格情報を収集、フェデレーション サーバー プロキシを使って既定クライアント ログオン Web フォーム \(clientlogon.aspx\) forms\ ベースの認証を通じて password\ ベースの資格情報を収集します。 ただし、このフォーム認証は、Secure Sockets Layer \(SSL\) クライアント認証などのサポートされているその他の種類を受け入れるようにカスタマイズできます。 このページをカスタマイズする方法の詳細については、カスタマイズのクライアント ログオンおよびホーム領域検出のページを参照して \ ([http:///\/go.microsoft.com\/fwlink\/ ですか?LinkId\ = 104275](https://go.microsoft.com/fwlink/?LinkId=104275)\)。 フェデレーション サーバー プロキシは、Windows 統合認証を通じて資格情報を受け付けません。  
  
要約すると、アカウント パートナーのフェデレーション サーバー プロキシは、企業ネットワークに配置されているフェデレーション サーバーへのクライアント ログオン用のプロキシとして機能します。 フェデレーション サーバー プロキシには、インターネットのクライアント証明書利用者宛てにセキュリティ トークンの配布も容易になります。  
  
> [!CAUTION]  
> アカウント パートナーのエクストラネット上のフェデレーション サーバー プロキシを公開するクライアント ログオン インターネットとのすべてのユーザーがアクセスできる Web フォームにアクセスします。 これは、できる可能性のある組織を去る辞書攻撃やブルート フォース攻撃が企業の Active Directory Domain Services \(AD DS\) に格納されているユーザー アカウントのアカウント ロックアウトが発生するなど、一部の password\ ベース攻撃に対して脆弱になります。  
  

## <a name="see-also"></a>参照してください。
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)
