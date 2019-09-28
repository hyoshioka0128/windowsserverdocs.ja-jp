---
title: RDS フィードに登録するために電子メールの検出を設定する
description: ご自身の RDS 展開に Azure AD Domain Services を統合する方法について説明します。
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: chrimo
ms.date: 3/27/2018
ms.localizationpriority: medium
ms.topic: article
author: christianmontoya
ms.openlocfilehash: c56a233adf28270aac809dc960e32b5363e4b8ab
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71387509"
---
# <a name="set-up-email-discovery-to-subscribe-to-your-rds-feed"></a>RDS フィードに登録するために電子メールの検出を設定する

フィード URL 内の単一の文字が不足している、または URL が含まれる電子メールを紛失したという理由で、エンドユーザーが各自に発行された RDS フィードに接続できないというトラブルを経験したことがありますか。 ほぼすべてのリモート デスクトップ クライアント アプリケーションでは、電子メール アドレスの入力によるサブスクリプションの検索をサポートして、ユーザーが各自の RemoteApp とデスクトップに簡単に接続できるようにしています。

>[!IMPORTANT]
>Microsoft Store の Microsoft リモート デスクトップ アプリでは、現時点では電子メール アドレスのサブスクリプションはサポートされていません。

電子メールの検出を設定する前に、以下を行います。

- 電子メールに関連付けられているドメインに TXT レコードを追加する権限があるかどうかを確認します (たとえば、ユーザーの電子メール アドレスに @contoso.com が含まれている場合は、contoso.com ドメインへのアクセス許可が必要です)。
- RD Web フィード URL (https://\<rdweb-dns-name\>.domain/RDWeb/Feed/webfeed.aspx) を作成します。例: https://rdweb.contoso.com/RDWeb/Feed/webfeed.aspx)

次に、以下の手順を使用して、電子メールの検出を設定します。

1. ブラウザーで、ドメインが登録されているドメイン名レジストラーの Web サイトに接続します。
2. DNS レコードを表示、追加、および編集できる登録済みのドメイン用の適切なページに移動します.
3. 次のプロパティを持つ新しい DNS レコードを入力します。
   - **ホスト:** _msradc
   - **テキスト:** \<RD Web フィード URL\>
   - **TTL:** 300

   DNS レコードのフィールドの名前はドメイン名レジストラーによって異なりますが、このプロセスでは、RD Web フィード全体の値を持つ _msradc.\<domain_name\> (_msradc.contoso.com など) という名前の TXT レコードになります。

以上で作業は終了です。 ここでデバイス上のリモート デスクトップ アプリケーションを起動して、ご自身を登録してください。