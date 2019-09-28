---
ms.assetid: 97999892-29c6-4076-be19-5e5259d8ada6
title: フェデレーション サーバーの展開
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: f2aaca5ffc846c41af82c276750c564db38b5020
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359513"
---
# <a name="interoperating-with-ad-fs-1x"></a>AD FS 1.x との相互運用

Active Directory フェデレーションサービス (AD FS) \(AD FS @ no__t-1 (Windows Server®2012および AD FS 1) の間の相互運用性。*x*では、組織のニーズに応じて、次の1つ以上のタスクを実行します。  
  
-   Windows Server 2012 と以前のバージョンの AD FS の AD FS 間の相互運用性を計画し、Name ID 要求の種類の詳細について説明します。 詳細については、「 [AD FS 1.x との相互運用性の計画](https://technet.microsoft.com/library/ff678040.aspx)」を参照してください。  
  
-   AD FS 1 で使用できる Windows Server 2012 の AD FS フェデレーションサービスから要求を送信する場合は。*x*フェデレーションサービス、「[ チェックリスト:AD FS 1.x フェデレーションサービス @ no__t に要求を送信するように AD FS を構成しています。  
  
-   AD FS 1 を実行している Web サーバーでホストされているアプリケーションで使用できる Windows Server 2012 の AD FS フェデレーションサービスから要求を送信する場合。*x*要求 @ no__t-1 対応 Web エージェント、「[ チェックリスト:AD FS 1. x 要求に対応する Web エージェント @ no__t に要求を送信するように AD FS を構成しています。  
  
-   AD FS 1 から要求を送信する場合は。Windows Server 2012 の AD FS フェデレーションサービスによって使用される*x*フェデレーションサービス、「[checklist リスト:AD FS 1.x @ no__t からの要求を使用するように AD FS を構成しています。  
  
## <a name="differences-between-federation-service-settings"></a>フェデレーションサービス設定の相違点  
ほとんどの AD FS 1 です。*x*フェデレーションサービス設定は、Windows Server 2012 設定の AD FS フェデレーションサービスと同様の方法で動作します。一部の設定名が変更されています。 次の表に、AD FS 1 の設定の名前を示します。Windows Server 2012 の AD FS フェデレーションサービスの*x*フェデレーションサービスとそれに相当する名前。  
  
|AD FS 1.x フェデレーションサービス設定|Windows Server 2012 の設定で AD FS フェデレーションサービスと同じです。  
|----------------------------------------|---------------------------------------------------------------------------------------------------------- 
|アカウントパートナー|要求プロバイダー信頼  
|リソースパートナー|証明書利用者信頼 
|アプリケーション|証明書利用者信頼  
|Application Properties|証明書利用者信頼のプロパティ  
|アプリケーションの URL|証明書利用者識別子と WS @ no__t-0Federation パッシブエンドポイント URL  
|フェデレーションサービス URI|フェデレーション サービスの識別子  
|フェデレーションサービスエンドポイント URL|WS @ no__t-0Federation パッシブエンドポイント URL  
  
## <a name="see-also"></a>関連項目  
[AD FS と AD FS 1. x 相互運用性](https://go.microsoft.com/fwlink/?LinkId=200776)  
  

