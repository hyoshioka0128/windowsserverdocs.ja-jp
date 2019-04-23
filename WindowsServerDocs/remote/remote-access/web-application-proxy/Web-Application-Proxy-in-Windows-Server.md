---
ms.assetid: 0b3587b2-219f-43d8-88b4-1254eaa8b910
title: Windows Server の Web アプリケーション プロキシ
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.service: ''
ms.suite: na
ms.technology: web-app-proxy
ms.tgt_pltfrm: na
ms.topic: article
author: kgremban
ms.openlocfilehash: 056e833a2c030b2fdb96b00e7e55996656e2fec2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886043"
---
# <a name="web-application-proxy-in-windows-server"></a>Windows Server の Web アプリケーション プロキシ

>適用先:Windows Server&reg; 2016

**このコンテンツは、Web アプリケーション プロキシのオンプレミス バージョンに関連します。クラウドでオンプレミス アプリケーションに安全にアクセスを有効にするのを参照してください。、 [Azure AD アプリケーション プロキシのコンテンツ](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-get-started/)します。**  
  
このセクションの内容は、新機能と、Web アプリケーション プロキシの Windows Server 2016 での変更について説明します。 新機能とは、ここに記載されている変更は、大きな影響を及ぼすプレビューを使用する際に最も可能性の高いものです。  
  
## <a name="web-application-proxy-new-features"></a>Web アプリケーション プロキシの新機能  
  
-   HTTP 基本アプリケーションの発行の事前認証  
  
    HTTP 基本は、ActiveSync を含む、多くのプロトコルと、Exchange メールボックスのスマート フォンを含む、リッチ クライアントの接続に使用する承認プロトコルです。 Web アプリケーション プロキシは、従来のリダイレクトを使用して ActiveSync クライアントでサポートされていない AD FS と対話します。 この新しいバージョンの Web アプリケーション プロキシは、以外の要求を受信する HTTP アプリケーションを有効にすると、基本的な HTTP を使用してアプリを発行するサポートを提供します。 アプリケーションをフェデレーション サービスの証明書利用者信頼。  
  
    HTTP の基本的な発行の詳細については、次を参照してください[AD FS 事前認証を使用してアプリケーションの発行。](../web-application-proxy/../web-application-proxy/Publishing-Applications-using-AD-FS-Preauthentication.md)  
  
-   アプリケーションのワイルドカード ドメインの公開  
  
    SharePoint 2013 などのシナリオをサポートするために、アプリケーションの外部 URL にワイルドカード https://*.sp-apps.contoso.com など、特定のドメイン内から複数のアプリケーションを発行するためにできるようになりました。 これは、SharePoint アプリの発行を簡略化されます。  
  
-   HTTP HTTPS へのリダイレクトから  
  
    確認するために、ユーザーは、アプリにアクセスできる HTTPS URL を入力を怠ると、場合でも、Web アプリケーション プロキシは HTTP を HTTPS にリダイレクトするようになりましたサポートします。  
  
-   HTTP の公開  
  
    パススルー事前認証を使用する HTTP アプリケーションを発行することは今すぐ  
  
-   リモート デスクトップ ゲートウェイ アプリケーションの発行  
  
    Web アプリケーション プロキシで RDG の詳細については、次を参照してください[SharePoint、Exchange および RDG によるアプリケーションの発行。](../web-application-proxy/Publishing-Applications-with-SharePoint,-Exchange-and-RDG.md)  
  
-   トラブルシューティングに役立つ新しいデバッグ ログとサービスの向上のログに完全な監査証跡およびエラー処理の強化  
  
    トラブルシューティングの詳細については、次を参照してください[Web アプリケーション プロキシのトラブルシューティング。](https://technet.microsoft.com/library/dn770156.aspx)  
  
-   管理者コンソール UI の機能強化  
  
-   バックエンド アプリケーションへのクライアント IP アドレスの伝達  
  
## <a name="see-also"></a>関連項目  
  
-   [新機能 Windows Server 2016 の新機能](https://technet.microsoft.com/library/dn765472.aspx)  
  
-   [AD FS 事前認証を使用してアプリケーションの発行](../web-application-proxy/Publishing-Applications-using-AD-FS-Preauthentication.md)  
  
-   [Web アプリケーション プロキシのトラブルシューティング](https://technet.microsoft.com/library/dn770156.aspx)  
  


