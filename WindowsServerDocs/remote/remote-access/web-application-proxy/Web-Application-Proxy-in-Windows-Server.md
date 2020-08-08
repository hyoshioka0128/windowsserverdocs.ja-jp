---
ms.assetid: 0b3587b2-219f-43d8-88b4-1254eaa8b910
title: Windows Server の Web アプリケーション プロキシ
ms.topic: article
ms.author: kgremban
author: eross-msft
ms.openlocfilehash: 433ab4825ff23526b656949c0df94befd892e29e
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87939743"
---
# <a name="web-application-proxy-in-windows-server"></a>Windows Server の Web アプリケーション プロキシ

>適用対象: Windows Server&reg; 2016

**このコンテンツは、オンプレミスバージョンの Web アプリケーションプロキシに関連しています。クラウド経由でオンプレミスアプリケーションへの安全なアクセスを実現するには、 [Azure AD アプリケーションプロキシのコンテンツ](/azure/active-directory/manage-apps/application-proxy)を参照してください。**

このセクションの内容では、Windows Server 2016 用の Web アプリケーションプロキシの新機能と変更された機能について説明します。 ここに記載されている新機能と変更点は、プレビューを操作するときに最も大きな影響を与える可能性の高いものです。

## <a name="web-application-proxy-new-features"></a>Web アプリケーションプロキシの新機能

- HTTP 基本アプリケーションの発行の事前認証

  HTTP Basic は、多数のプロトコル (ActiveSync など) によって使用される認証プロトコルで、スマートフォンなどのリッチクライアントを Exchange メールボックスに接続します。 従来、Web アプリケーションプロキシは、ActiveSync クライアントでサポートされていないリダイレクトを使用して AD FS とやり取りします。 この新しいバージョンの Web アプリケーションプロキシでは、http アプリがアプリケーションの要求されていない証明書利用者信頼をフェデレーションサービスに受信できるようにすることで、HTTP basic を使用してアプリを発行するためのサポートを提供します。

  HTTP 基本発行の詳細については、「 [AD FS 事前認証を使用してアプリケーションを公開する](../web-application-proxy/../web-application-proxy/Publishing-Applications-using-AD-FS-Preauthentication.md)」を参照してください。

- ワイルドカードによるアプリケーションのドメイン公開

  SharePoint 2013 のようなシナリオをサポートするために、アプリケーションの外部 URL にワイルドカードを含めることができるようになりました。これにより、https://*. sp-アプリなど、特定のドメイン内から複数のアプリケーションを発行できます。 これにより、SharePoint アプリの発行が簡単になります。

- HTTP から HTTPS へのリダイレクト

  URL に HTTPS を入力しない場合でも、ユーザーがアプリにアクセスできるようにするために、Web アプリケーションプロキシで HTTP から HTTPS へのリダイレクトがサポートされるようになりました。

- HTTP 発行

  パススルー事前認証を使用して HTTP アプリケーションを公開できるようになりました

- リモートデスクトップゲートウェイアプリの発行

  Web アプリケーションプロキシの RDG の詳細については、「 [SharePoint、Exchange、および RDG を使用したアプリケーションの発行](../web-application-proxy/Publishing-Applications-with-SharePoint,-Exchange-and-RDG.md)」を参照してください。

- 詳細なトラブルシューティングと改善されたサービスログを記録し、完全な監査証跡を作成し、エラー処理を改善します。

  トラブルシューティングの詳細については、「 [Web アプリケーションプロキシのトラブルシューティング](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn770156(v=ws.11))」を参照してください。

- 管理コンソール UI の機能強化

- バックエンドアプリケーションへのクライアント IP アドレスの伝達

## <a name="see-also"></a>参照

-   [Windows Server 2016 の新機能](../../../get-started/whats-new-in-windows-server-2016.md)

-   [AD FS 事前認証を使用してアプリケーションを公開する](../web-application-proxy/Publishing-Applications-using-AD-FS-Preauthentication.md)

-   [Web アプリケーション プロキシのトラブルシューティング](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn770156(v=ws.11))

