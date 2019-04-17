---
ms.assetid: 97999892-29c6-4076-be19-5e5259d8ada6
title: "フェデレーション サーバーを展開します。"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: f80425b6f062040c51357353038fd07ff0a79ae6
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="interoperating-with-ad-fs-1x"></a>Interoperating with AD FS 1.x

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows Server® 2012 での Active Directory フェデレーション サービス \(AD FS\) と AD FS 1 の間の相互運用性。*x*、1 つ以上の組織のニーズに応じて、次のタスクを完了します。  
  
-   Windows Server 2012 で AD FS と AD FS の以前のバージョン間の相互運用性の計画し、詳細については、名前 ID 要求の種類について説明します。 詳細については、次を参照してください。[AD FS と相互運用性の計画 1.x](https://technet.microsoft.com/library/ff678040.aspx)します。  
  
-   AD FS 1 で消費可能な Windows Server 2012 で AD FS フェデレーション サービスからの信頼性情報が送信される場合。*x*フェデレーション サービスを参照してください[チェックリスト: Configuring AD FS to Send Claims to an AD FS 1.x Federation Service](Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Federation-Service.md)します。  
  
-   AD FS 1 を実行している Web サーバーによってホストされているアプリケーションで消費可能な Windows Server 2012 で AD FS フェデレーション サービスから信頼性情報が送信されます。場合、*x* claims\ 対応する Web エージェントを参照してください[チェックリスト: Configuring AD FS to Send Claims to an AD FS 1.x Claims-aware Web エージェント](Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Claims-Aware-Web-Agent.md)します。  
  
-   AD FS 1 から信頼性情報が送信される場合。*x*フェデレーション サービス、Windows Server 2012 で AD FS フェデレーション サービスで使用されるを参照してください[チェックリスト: AD FS からの信頼性情報を使用する AD FS を構成する 1.x](Checklist--Configuring-AD-FS--to-Consume-Claims-from-AD-FS-1.x.md)します。  
  
## <a name="differences-between-federation-service-settings"></a>フェデレーション サービスの設定の相違点  
ただし、AD FS 1 のほとんどします。*x*同様の方法として Windows Server 2012 の設定で AD FS フェデレーション サービスでフェデレーション サービスの設定の作業、いくつかの設定名が変更されました。 次の表は、AD FS 1 の設定の名前を示します。*x*フェデレーション サービスと Windows Server 2012 で AD FS フェデレーション サービスをそれと同等の名前。  
  
|AD FS 1.x のフェデレーション サービスの設定|Windows Server 2012 の設定でそれと同等の AD FS フェデレーション サービス  
|----------------------------------------|---------------------------------------------------------------------------------------------------------- 
|アカウント パートナー|要求プロバイダー信頼  
|リソース パートナー|証明書利用者の信頼 
|アプリケーション|証明書利用者の信頼  
|アプリケーションのプロパティ|証明書利用者信頼のプロパティをパーティー  
|アプリケーションの URL|証明書利用者の識別子と WS\ フェデレーション パッシブ エンドポイントの URL  
|フェデレーション サービスの URI|フェデレーション サービス識別子  
|フェデレーション サービスのエンドポイント URL|WS\ フェデレーション パッシブ エンドポイント URL  
  
## <a name="see-also"></a>参照してください。  
[AD FS と AD FS 1.x の相互運用性](https://go.microsoft.com/fwlink/?LinkId=200776)  
  

