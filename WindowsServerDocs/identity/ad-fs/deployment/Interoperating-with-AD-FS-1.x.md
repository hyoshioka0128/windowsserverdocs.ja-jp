---
ms.assetid: 97999892-29c6-4076-be19-5e5259d8ada6
title: フェデレーション サーバーの展開
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: f80425b6f062040c51357353038fd07ff0a79ae6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812173"
---
# <a name="interoperating-with-ad-fs-1x"></a>AD FS 1.x との相互運用

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

Active Directory フェデレーション サービスの相互運用性\(AD FS\) Windows Server® 2012 および AD FS 1 *。x*、1 つ以上の組織のニーズに応じて、次のタスクを完了します。  
  
-   Windows Server 2012 で AD FS と AD FS の以前のバージョン間の相互運用性の計画し、要求の種類の名前 ID の詳細について説明します。 詳細については、次を参照してください。 [AD FS との相互運用の計画 1.x](https://technet.microsoft.com/library/ff678040.aspx)します。  
  
-   場合は、AD fs 1 使用できる Windows Server 2012 で AD FS フェデレーション サービスから要求が送信されます。*x*フェデレーション サービスを参照してください[チェックリスト。AD FS 1.x のフェデレーション サービスに対するクレームを送信する AD FS を構成する](Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Federation-Service.md)します。  
  
-   場合は、AD FS 1 を実行している Web サーバーによってホストされているアプリケーションで使用できる Windows Server 2012 で AD FS フェデレーション サービスから要求が送信されます。*x*クレーム\-、対応する Web エージェントを参照してください[チェックリスト。AD FS 1.x Claims-aware Web エージェントを要求を送信する AD FS を構成する](Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Claims-Aware-Web-Agent.md)します。  
  
-   場合は、AD FS 1 から要求が送信されます。*x* Windows Server 2012 の AD FS フェデレーション サービスで使用するフェデレーション サービスを参照してください[チェックリスト。Configuring AD FS からの要求を使用する AD FS 1.x](Checklist--Configuring-AD-FS--to-Consume-Claims-from-AD-FS-1.x.md)します。  
  
## <a name="differences-between-federation-service-settings"></a>フェデレーション サービスの設定の相違点  
ほとんどの AD FS 1。*x*同様の方法として Windows Server 2012 の設定では、AD FS フェデレーション サービスでフェデレーション サービスの設定作業をいくつかの設定名が変更されました。 次の表は、AD FS 1 の設定の名前を一覧表示します。*x*フェデレーション サービスと Windows Server 2012 で AD FS フェデレーション サービスの名前と同じです。  
  
|AD FS 1.x Federation Service の設定|Windows Server 2012 の設定で AD FS のフェデレーション サービスと同じです。  
|----------------------------------------|---------------------------------------------------------------------------------------------------------- 
|アカウント パートナー|要求プロバイダー信頼  
|リソース パートナー|証明書利用者信頼 
|アプリケーション|証明書利用者信頼  
|Application Properties|証明書利用者信頼のプロパティをパーティ  
|アプリケーションの URL|証明書利用者のパーティの識別子と WS\-フェデレーション パッシブ エンドポイント URL  
|フェデレーション サービス URI|フェデレーション サービスの識別子  
|フェデレーション サービス エンドポイントの URL|WS\-フェデレーション パッシブ エンドポイント URL  
  
## <a name="see-also"></a>関連項目  
[AD FS と AD FS 1.x の相互運用性](https://go.microsoft.com/fwlink/?LinkId=200776)  
  

