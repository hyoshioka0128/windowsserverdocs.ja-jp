---
title: フィード、RDS を購読する電子メール discovery のセットアップします。
description: RDS のデプロイに Azure AD Domain Services を統合する方法について説明します。
ms.prod: windows-server-threshold
ms.technology: remote-desktop-services
ms.author: chrimo
ms.date: 3/27/2018
ms.localizationpriority: medium
ms.topic: article
author: christianmontoya
ms.openlocfilehash: 5b3f162b8eee70fbc452b7400b737454c3fffb59
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878323"
---
# <a name="set-up-email-discovery-to-subscribe-to-your-rds-feed"></a>フィード、RDS を購読する電子メール discovery のセットアップします。

経験はあるトラブルの維持、フィードで不足している単一の文字があるか、フィード、パブリッシュされた RDS が自分に接続されているエンドユーザー URL または URL を使用して電子メールを紛失したためでしょうか。 ほぼすべてのリモート デスクトップ クライアント アプリケーションをサポートして、これまでに、Remoteapp とデスクトップに接続されているユーザーを取得するよりも簡単に電子メール アドレスを入力して、サブスクリプションを検索します。

>[!IMPORTANT]
>Microsoft Store での Microsoft リモート デスクトップ アプリは、この時点で電子メール アドレスのサブスクリプションをサポートしていません。

電子メールの検出をセットアップする前に、次の操作を行います。

- TXT レコードを電子メールに関連付けられているドメインに追加する権限があるかどうかを確認 (ユーザーがある場合など、@contoso.comの電子メール アドレスに、contoso.com ドメインのアクセス許可を必要があります)
- フィード URL、RD Web の作成 (https://\<rdweb の dns 名\>.domain/RDWeb/Feed/webfeed.aspx など https://rdweb.contoso.com/RDWeb/Feed/webfeed.aspx)

ここで、次の手順を使用して、電子メールの検出を設定します。

1. ブラウザーでは、ドメインが登録されているドメイン名レジストラーの web サイトに接続します。
2. 表示、追加、および DNS レコードの編集をする登録済みドメインの適切なページに移動します。
3. 次のプロパティで新しい DNS レコードを入力します。
   - **ホスト:** _msradc
   - **テキスト:**\<RD Web フィード URL\>
   - **TTL:** 300

   ドメイン名レジストラーによって DNS レコードのフィールドの名前が異なりますが、_msradc という名前の TXT レコードでこのプロセスになります。\<domain_name\> (_msradc.contoso.com) など、すべての RD Web フィードの値を持ちます。

これで完了です。 ここで、デバイス上のリモート デスクトップ アプリケーションを起動し、自分でサブスクライブ!