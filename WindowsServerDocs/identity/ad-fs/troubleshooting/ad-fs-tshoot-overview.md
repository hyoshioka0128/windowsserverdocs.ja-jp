---
title: AD FS のトラブルシューティング
description: このドキュメントでは、AD FS のさまざまな側面をトラブルシューティングする方法について説明します。
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/12/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 5fc5c2384a6d8d13f807a1ce99c5db78bee5b108
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2020
ms.locfileid: "75950135"
---
# <a name="troubleshooting-ad-fs"></a>AD FS のトラブルシューティング
AD FS には多くのさまざまな要素があり、さまざまな依存関係があります。  当然、これによって各種の問題が生じると考えられます。  このドキュメントは、これらの問題のトラブルシューティングを開始できるようにすることを目的としています。  このドキュメントでは、注目すべき一般的な領域、追加情報のために機能を有効にする方法、および問題を追跡するために使用できるさまざまなツールについて紹介します。  

>[!NOTE]
>詳細については、「 [ADFS ヘルプ](https://adfshelp.microsoft.com)」を参照してください。これにより、ユーザーおよび管理者は、より迅速に認証の問題を簡単に解決できるようになります。 


## <a name="what-to-check-first"></a>最初に確認する内容
詳細なトラブルシューティングに進む前に、まず、確認する必要がある点がいくつかあります。  以下の説明を参照してください。
- **DNS 構成**-フェデレーションサービスの名前を解決できますか。  これは、ロードバランサーの IP アドレスか、ファーム内のいずれかの AD FS サーバーの IP アドレスに解決されます。  詳細については[、「AD FS のトラブルシューティング-DNS](ad-fs-tshoot-dns.md)」を参照してください。
- **AD FS エンド**ポイント-AD FS エンドポイントを参照できますか。  これを参照することによって、AD FS web サーバーが要求に応答しているかどうかを判断できます。  このファイルにアクセスできる場合は、443以上の要求を正常に処理 AD FS ことがわかっています。  詳細については[、「AD FS のトラブルシューティング-エンドポイント](ad-fs-tshoot-endpoints.md)」を参照してください。
- **Idp によって開始**されるサインオン-Idp で開始されたサインオンページを使用してログインおよび認証を行うことができますか。  既定では無効になっているため、このページが有効になっていることを確認する必要があります。  `Set-AdfsProperties -EnableIdPInitiatedSignOn $true` を使用してページを有効にします。  サインインして認証できる場合は、AD FS がこの領域で動作していることがわかります。  詳細については[、「AD FS トラブルシューティング-サイン](ad-fs-tshoot-initiatedsignon.md)オン」を参照してください。
  ##  <a name="common-troubleshooting-areas"></a>一般的なトラブルシューティング領域

|名前|説明|
|-----|-----|
|[イベントのログ記録と監査](ad-fs-tshoot-logging.md)|Windows イベントログを使用して、管理ログとトレースログを使用して、概要レベルおよび低レベルの情報を表示します。  また、セキュリティ監査の表示にも使用できます。|
|[SQL 接続](ad-fs-tshoot-sql.md)|AD FS サーバーとバックエンド SQL データベース間の接続のテストに関する情報|
|[要求の発行](ad-fs-tshoot-claims-issuance.md)|AD FS が要求を正しく発行しているかどうかを判断するための情報。|
|[ループの検出](ad-fs-tshoot-loop.md)|Idp と RP の間でのユーザーによるバウンスの特定と防止について説明します。|
|[証明書](ad-fs-tshoot-certs.md)|Typcial 証明書の問題が発生する可能性があります|
|[Fiddler](ad-fs-tshoot-fiddler.md)|Fiddler をインストールして使用する方法に関する情報|
|[Fiddler との WS-FEDERATION](ad-fs-tshoot-fiddler-ws-fed.md)|WS-FEDERATION の相互作用の詳細な Fiddler トレース|
|[要求規則](ad-fs-tshoot-claims-rules.md)|要求規則とその構文のトラブルシューティングに関する情報|
|[統合 Windows 認証](ad-fs-tshoot-iwa.md)|統合認証のトラブルシューティングについて説明します。|
|[Azure AD](ad-fs-tshoot-azure.md)|Azure AD との AD FS の相互作用に関するトラブルシューティングについて説明します。|
|[AD FS Diagnostics Analyzer](ad-fs-diagnostics-analyzer.md)|AD FS Help Diagnostics Analyzer は、診断 PowerShell モジュールを使用して基本的な AD FS チェックを実行するのに役立ちます。 