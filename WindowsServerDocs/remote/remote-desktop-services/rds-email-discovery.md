---
title: RDS のフィードを購読するメールの検索を設定します。
description: Azure AD ドメイン サービスを RDS 展開に統合する方法について説明します。
ms.prod: windows-server-threshold
ms.technology: remote-desktop-services
ms.author: chrimo
ms.date: 3/27/2018
ms.localizationpriority: medium
ms.topic: article
author: christianmontoya
ms.openlocfilehash: 5b3f162b8eee70fbc452b7400b737454c3fffb59
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/01/2018
ms.locfileid: "1691671"
---
# <a name="set-up-email-discovery-to-subscribe-to-your-rds-feed"></a>RDS のフィードを購読するメールの検索を設定します。

したことがありますが、エンドユーザーは維持フィードに存在しない文字を 1 つの理由により、いずれか、フィード、発行された RDS が自分に接続されている問題が発生 URL または URL を使用してメールを失いですか? ほぼすべてのリモート デスクトップ クライアント アプリケーションでは、Remoteapp とデスクトップに接続されているユーザーの取得よりも簡単にできるように、電子メール アドレスを入力して、サブスクリプションの検索をサポートします。

>[!IMPORTANT]
>Microsoft ストアの Microsoft リモート デスクトップ アプリは、この時点でのメール アドレスの購読をサポートしていません。

検出のメールをセットアップする前に、次の操作を行います。

- メールに関連付けられているドメインに TXT レコードを追加する権限があることを確認します (たとえば、ユーザーがある場合@contoso.comメール アドレス、contoso.com のアクセス許可が必要と)
- フィードの URL を RD Web を作成する (https://\ < rdweb dns name\ >.domain/RDWeb/Feed/webfeed.aspx、次のようなhttps://rdweb.contoso.com/RDWeb/Feed/webfeed.aspx)

これで、次の手順を使用して、検出のメールを設定します。

1. ブラウザーで、自分のドメインが登録されているドメイン名レジストラーの web サイトに接続します。
2. 適切な表示、追加、および DNS レコードを編集が登録されているドメインのページに移動します。
3. 次のプロパティで新しい DNS レコードを入力します。
   - **Host]:** _msradc
   - **テキスト:** \ < RD Web フィードの URL\ >
   - **TTL:** 300

   DNS レコードのフィールドの名前が、ドメイン名レジストラーによって異なりますが、このプロセスと名付けられた _msradc TXT レコードを \ < domain_name\ > フル RD Web フィードの値を持つ (_msradc.contoso.com) など。

それです！ これで、デバイスでリモート デスクトップ アプリケーションを起動し、自分の購読を行います。