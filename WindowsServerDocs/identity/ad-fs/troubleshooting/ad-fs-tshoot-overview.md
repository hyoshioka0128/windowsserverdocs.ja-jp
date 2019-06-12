---
title: AD FS のトラブルシューティング
description: このドキュメントは、AD FS のさまざまな側面をトラブルシューティングする方法を説明します
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/12/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 6410d510085d1772ca6d8ced47226e00239a1a02
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66443902"
---
# <a name="troubleshooting-ad-fs"></a>AD FS のトラブルシューティング
AD FS は、多数の変動要素がある、さまざまなことに触れておよび多くのさまざまな依存関係があります。  当然ながら、さまざまな問題に上昇を与えることがこれです。  このドキュメントは、これらの問題のトラブルシューティングを開始するために設計されています。  このドキュメントでは、追加情報、および問題を追跡するために使用できるさまざまなツールの機能を有効にする方法に注意すべき一般的な領域に紹介します。  

>[!NOTE]
>追加情報を参照してください。 [ADFS ヘルプ](http://adfshelp.microsoft.com)ユーザーおよび管理者は迅速なペースでの認証の問題を解決するには簡単で 1 つの効果的なツールの配置を提供する使用します。 


## <a name="what-to-check-first"></a>最初のチェックの対象
詳細なトラブルシューティングに説明する前に最初に確認する必要がありますをいくつかの点があります。  それらは以下のとおりです。
- **DNS 構成**-フェデレーション サービスの名前を解決することができますか?  これは、いずれか、ロード バランサーの IP アドレスまたは AD FS サーバー ファーム内の 1 つの IP アドレスに解決する必要があります。  詳細については、次を参照してください。 [AD FS のトラブルシューティング - DNS](ad-fs-tshoot-dns.md)します。
- **AD FS エンドポイント**-AD FS のエンドポイントを参照することができますか?  これを参照して、AD FS web サーバーが要求に応答するかどうかを判断できます。  、このファイルを表示する場合、AD FS が要求を処理うまく 443 をしたがわかります。  詳細については、次を参照してください。 [AD FS エンドポイントのトラブルシューティング -](ad-fs-tshoot-endpoints.md)します。
- **Idp によって開始されたサインオン**-できるログインし、Idp-Initiated へのサインオン ページを使用して認証しますか?  既定で無効になっているため、このページが有効になっていることを確認する必要があります。  使用`Set-AdfsProperties -EnableIdPInitiatedSignOn $true`ページを有効にします。  サインインして認証する知ってこの領域で、AD FS が動作するいるとします。  詳細については、次を参照してください。 [AD FS のトラブルシューティング - サインオン](ad-fs-tshoot-initiatedsignon.md)します。
  ##  <a name="common-troubleshooting-areas"></a>トラブルシューティングの一般的な領域

|名前|説明|
|-----|-----|
|[イベント ログと監査](ad-fs-tshoot-logging.md)|Windows イベント ログを使用すると、高レベルと低レベルの情報管理とトレース ログを使用して表示できます。  セキュリティ監査を表示するのにも使用できます。|
|[SQL 接続](ad-fs-tshoot-sql.md)|AD FS サーバーとバックエンドの SQL データベース間の接続をテストするのには|
|[要求の発行](ad-fs-tshoot-claims-issuance.md)|AD FS で要求の発行が正常かどうかを決定する方法の詳細については説明します。|
|[ループの検出](ad-fs-tshoot-loop.md)|決定し、ユーザーが Idp と RP の間を行き来返送されていることを防止に関する情報です。|
|[証明書](ad-fs-tshoot-certs.md)|発生する可能性についてはこの使用証明書の問題|
|[Fiddler](ad-fs-tshoot-fiddler.md)|インストールする方法および Fiddler の使用に関する情報|
|[Fiddler で Ws-federation](ad-fs-tshoot-fiddler-ws-fed.md)|Ws-federation の相互作用の詳細な Fiddler のトレース|
|[要求規則](ad-fs-tshoot-claims-rules.md)|要求規則とその構文のトラブルシューティングに関する情報|
|[統合 Windows 認証](ad-fs-tshoot-iwa.md)|統合認証のトラブルシューティングに関する情報です。|
|[Azure AD](ad-fs-tshoot-azure.md)|Azure AD との対話を AD FS のトラブルシューティングに関する情報です。|
|[AD FS 診断アナライザー](ad-fs-diagnostics-analyzer.md)|AD FS ヘルプ診断アナライザーは、診断の PowerShell モジュールを使用して基本的な AD FS のチェックを実行できます。 