---
title: AD FS トラブルシューティング-統合 Windows 認証
description: このドキュメントでは、統合 windows 認証のトラブルシューティングを行う方法について説明します。
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/21/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 98f6c2e39b2a5eeab76103c1ae477dde785a0e04
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385394"
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

AD FS サービスアカウントの構成が正しくない場合、または SPN が間違っている場合は、問題が発生する可能性があります。  ネットワークトレースを見ると、KRB エラーなどのエラーが表示される場合があります。KRB5KDC_ERR_S_PRINCIPAL_UNKNOWN.

ネットワークトレース (Wireshark など) を使用して、ブラウザーが解決しようとしている SPN を特定し、コマンドラインツール setspn-Q <spn> を使用して、その SPN で参照を行うことができます。  見つからないか、AD FS サービスアカウント以外の別のアカウントに割り当てられている可能性があります。

![済み](media/ad-fs-tshoot-iwa/iwa3.png)

SPN を確認するには、AD FS サービスアカウントのプロパティを参照します。

![済み](media/ad-fs-tshoot-iwa/iwa1.png)

## <a name="channel-binding-token"></a>チャネルバインドトークン
現在、クライアントアプリケーションが HTTPS を使用して Kerberos、ダイジェスト、または NTLM を使用してサーバーに対して自身を認証する場合、トランスポートレベルセキュリティ (TLS) チャネルが最初に確立され、このチャネルを使用して認証が行われます。 

チャネルバインディングトークンは、TLS で保護された外部チャネルのプロパティであり、外部チャネルをクライアント認証の内部チャネルを介してメッセージ交換にバインドするために使用されます。

"Man-in-the-middle" 攻撃が発生し、SSL トラフィックを crypting して再暗号化した場合、キーは一致しませんが、この攻撃が行われます。  AD FS は、web 参照 r とそれ自体の中間にあるものがあることを確認します。  これにより、Kerberos 認証が失敗し、SSO エクスペリエンスではなく、ユーザーに401ダイアログが表示されます。

原因として、次のことが考えられます。
 - ブラウザーと AD FS の間にあるもの
 - Fiddler
 - SSL ブリッジングを実行するリバースプロキシ

既定では、AD FS は [許可] に設定されています。  PowerShell コマンドレット `Set-ADFSProperties -ExtendProtectionTokenCheck` を使用して、この設定を変更できます。

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
