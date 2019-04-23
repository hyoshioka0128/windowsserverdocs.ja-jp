---
ms.assetid: d8adcb68-18e0-41bf-a817-d57344bf2e7d
title: Windows Server 2016 における Web アプリケーション プロキシ
description: ''
author: kgremban
manager: femila
ms.date: 07/13/2016
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: web-app-proxy
ms.openlocfilehash: 2f24e1b8605503d338b15f385017bbeacce682fb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872213"
---
# <a name="web-application-proxy-in-windows-server-2016"></a>Windows Server 2016 における Web アプリケーション プロキシ

>適用先:Windows Server 2016

**このコンテンツは、Web アプリケーション プロキシのオンプレミス バージョンに関連します。クラウドでオンプレミス アプリケーションに安全にアクセスを有効にするのを参照してください。、 [Azure AD アプリケーション プロキシのコンテンツ](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-get-started/)します。**  
  
このセクションの内容は、新機能と、Web アプリケーション プロキシの Windows Server 2016 での変更について説明します。 新機能とは、ここに記載されている変更は、大きな影響を及ぼすプレビューを使用する際に最も可能性の高いものです。  
  
## <a name="web-application-proxy-new-features-in-windows-server-2016"></a>Windows Server 2016 で web アプリケーション プロキシの新機能
  
-   HTTP 基本アプリケーションの発行の事前認証  
  
    HTTP 基本は、ActiveSync を含む、多くのプロトコルと、Exchange メールボックスのスマート フォンを含む、リッチ クライアントの接続に使用する承認プロトコルです。 Web アプリケーション プロキシは、従来のリダイレクトを使用して ActiveSync クライアントでサポートされていない AD FS と対話します。 この新しいバージョンの Web アプリケーション プロキシは、以外の要求を受信する HTTP アプリケーションを有効にすると、基本的な HTTP を使用してアプリを発行するサポートを提供します。 アプリケーションをフェデレーション サービスの証明書利用者信頼。  
  
    HTTP の基本的な発行の詳細については、次を参照してください[AD FS 事前認証を使用してアプリケーションの発行。](Publishing-Applications-using-AD-FS-Preauthentication.md#publish-an-application-that-uses-http-basic)  
  
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
  


