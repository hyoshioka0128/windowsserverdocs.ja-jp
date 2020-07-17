---
ms.assetid: 97999892-29c6-4076-be19-5e5259d8ada6
title: フェデレーション サーバーの展開
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 800c7fc23c9b126a17e54311fc6df0d3dcf36b4c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855365"
---
# <a name="interoperating-with-ad-fs-1x"></a>AD FS 1.x との相互運用

Active Directory フェデレーションサービス (AD FS) \(間の相互運用性のために、Windows Server&reg; 2012 および AD FS 1 で\) AD FS ます。*x*では、組織のニーズに応じて、次の1つ以上のタスクを実行します。  
  
-   Windows Server 2012 と以前のバージョンの AD FS の AD FS 間の相互運用性を計画し、Name ID 要求の種類の詳細について説明します。 詳細については、「 [AD FS 1.x との相互運用性の計画](https://technet.microsoft.com/library/ff678040.aspx)」を参照してください。  
  
-   AD FS 1 で使用できる Windows Server 2012 の AD FS フェデレーションサービスから要求を送信する場合は。*x*フェデレーションサービス、「[チェックリスト: AD FS 1.X フェデレーションサービスに要求を送信するための AD FS の構成](Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Federation-Service.md)」を参照してください。  
  
-   AD FS 1 を実行している Web サーバーでホストされているアプリケーションで使用できる Windows Server 2012 の AD FS フェデレーションサービスから要求を送信する場合。*x*要求\-対応 web エージェント、「[チェックリスト: AD FS 1.X 要求に対応する Web エージェントに要求を送信するための AD FS の構成](Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Claims-Aware-Web-Agent.md)」を参照してください。  
  
-   AD FS 1 から要求を送信する場合は。*x*フェデレーションサービス Windows Server 2012 の AD FS フェデレーションサービスによって使用される場合は、「[チェックリスト: AD FS 1.X からの要求を使用するように AD FS を構成](Checklist--Configuring-AD-FS--to-Consume-Claims-from-AD-FS-1.x.md)する」を参照してください。  
  
## <a name="differences-between-federation-service-settings"></a>フェデレーションサービス設定の相違点  
ほとんどの AD FS 1 です。*x*フェデレーションサービス設定は、Windows Server 2012 設定の AD FS フェデレーションサービスと同様の方法で動作します。一部の設定名が変更されています。 次の表に、AD FS 1 の設定の名前を示します。Windows Server 2012 の AD FS フェデレーションサービスの*x*フェデレーションサービスとそれに相当する名前。  
  
|AD FS 1.x フェデレーションサービス設定|Windows Server 2012 の設定で AD FS フェデレーションサービスと同じです。  
|----------------------------------------|---------------------------------------------------------------------------------------------------------- 
|アカウントパートナー|要求プロバイダー信頼  
|リソースパートナー|証明書利用者の信頼 
|アプリケーション|証明書利用者の信頼  
|アプリケーションのプロパティ|証明書利用者信頼のプロパティ  
|アプリケーションの URL|証明書利用者識別子と WS\-フェデレーションパッシブエンドポイント URL  
|フェデレーションサービス URI|フェデレーション サービスの識別子  
|フェデレーションサービスエンドポイント URL|WS\-フェデレーションパッシブエンドポイント URL  
  
## <a name="see-also"></a>参照  
[AD FS と AD FS 1. x 相互運用性](https://go.microsoft.com/fwlink/?LinkId=200776)  
  

