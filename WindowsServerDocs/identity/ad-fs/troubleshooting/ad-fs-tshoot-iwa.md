---
title: AD FS トラブルシューティング-統合 Windows 認証
description: このドキュメントでは、統合 windows 認証のトラブルシューティングを行う方法について説明します。
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/21/2017
ms.topic: article
ms.openlocfilehash: 4c1823e1cbfc58e50c7231293b846c31480e01a6
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954158"
---
# <a name="ad-fs-troubleshooting---integrated-windows-authentication"></a>AD FS トラブルシューティング-統合 Windows 認証
統合 Windows 認証を使用すると、ユーザーは Windows 資格情報でログインし、Kerberos または NTLM を使用してシングルサインオン (SSO) を利用できます。

## <a name="reason-integrated-windows-authentication-fails"></a>統合 windows 認証が失敗する理由
統合 windows 認証が失敗する主な理由は3つあります。 これらは次のとおりです。
    - サービスプリンシパル名 (SPN) の構成の誤り
    - チャネルバインドトークン
    - Internet Explorer の構成

## <a name="spn-misconfiguration"></a>SPN の構成の誤り
サービスプリンシパル名 (SPN) は、サービスインスタンスの一意の識別子です。 Spn は、サービスインスタンスをサービスログオンアカウントに関連付けるために Kerberos 認証によって使用されます。 これにより、クライアントアプリケーションは、アカウント名がない場合でも、サービスがアカウントを認証するように要求できます。

SPN を AD FS と共に使用する方法の例を次に示します。
1. Web ブラウザーは、sts.contoso.com を実行しているサービスアカウントを特定するために Active Directory を照会します。
2. Active Directory は、AD FS サービスアカウントであることをブラウザーに伝えます。
3. ブラウザーは、AD FS サービスアカウントの Kerberos チケットを取得します。

AD FS サービスアカウントの構成が正しくない場合、または SPN が間違っている場合は、問題が発生する可能性があります。  ネットワークトレースを見ると、KRB Error: KRB5KDC_ERR_S_PRINCIPAL_UNKNOWN のようなエラーが表示される場合があります。

ネットワークトレース (Wireshark など) を使用して、ブラウザーが解決しようとしている SPN を特定し、コマンドラインツール setspn-Q を使用すると、 <spn> その spn で参照を行うことができます。  見つからないか、AD FS サービスアカウント以外の別のアカウントに割り当てられている可能性があります。

![済み](media/ad-fs-tshoot-iwa/iwa3.png)

SPN を確認するには、AD FS サービスアカウントのプロパティを参照します。

![済み](media/ad-fs-tshoot-iwa/iwa1.png)

## <a name="channel-binding-token"></a>チャネルバインドトークン
現在のところ、クライアント アプリケーションが HTTPS で Kerberos、Digest または NTLM を使用してサーバーに対する認証を実行する場合、最初にトランスポート レベルのセキュリティ (TLS) チャネルが構築され、このチャネルを使用して認証が行われます。

チャネルバインディングトークンは、TLS で保護された外部チャネルのプロパティであり、外部チャネルをクライアント認証の内部チャネルを介してメッセージ交換にバインドするために使用されます。

"Man-in-the-middle" 攻撃が発生し、SSL トラフィックを crypting して再暗号化した場合、キーは一致しませんが、この攻撃が行われます。  AD FS は、web 参照 r とそれ自体の中間にあるものがあることを確認します。  これにより、Kerberos 認証が失敗し、SSO エクスペリエンスではなく、ユーザーに401ダイアログが表示されます。

原因として、次のことが考えられます。
 - ブラウザーと AD FS の間にあるもの
 - Fiddler
 - SSL ブリッジングを実行するリバースプロキシ

既定では、AD FS は [許可] に設定されています。  この設定は、PowerShell のコマンドレットを使用して変更できます。`Set-ADFSProperties -ExtendProtectionTokenCheck`

詳細については[、「AD FS のセキュリティで保護された計画と展開のベストプラクティス](../../ad-fs/design/best-practices-for-secure-planning-and-deployment-of-ad-fs.md)」を参照してください。

## <a name="internet-explorer-configuration"></a>Internet Explorer の構成
既定では、Internet explorer は次のようになります。

1. Internet explorer は、ヘッダーに NEGOTIATE という単語の AD FS から401の応答を受け取ります。
2. これにより、web ブラウザーは AD FS に返信するために Kerberos または NTLM チケットを取得するように指示されます。
3. 既定では、IE は、ヘッダーに "NEGOTIATE" という単語が含まれている場合、ユーザーの操作なしでこの操作 (SPNEGO) を試みます。  これは、イントラネットサイトでのみ機能します。

これは、happeing によって妨げられる可能性がある主な点が2つあります。
   - IE のプロパティでは、[統合 Windows 認証を有効にする] はオンになっていません。  これは [インターネットオプション] の下にあります。詳細 > セキュリティ > ます。

   ![済み](media/ad-fs-tshoot-iwa/iwa4.png)

   - セキュリティゾーンが正しく構成されていません
       - Fqdn がイントラネットゾーンにありません
       - AD FS URL がイントラネットゾーンにありません。

      ![済み](media/ad-fs-tshoot-iwa/iwa5.png)
## <a name="next-steps"></a>次の手順

- [AD FS のトラブルシューティング](ad-fs-tshoot-overview.md)
