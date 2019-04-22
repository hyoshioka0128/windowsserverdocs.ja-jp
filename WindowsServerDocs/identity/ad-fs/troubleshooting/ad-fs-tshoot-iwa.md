---
title: 統合 Windows 認証の AD FS のトラブルシューティング
description: このドキュメントは、統合 windows 認証のトラブルシューティングを行う方法を説明します
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/21/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 91f252f5b0eca0f4c44e0b1a4564037298bf023c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814063"
---
# <a name="ad-fs-troubleshooting---integrated-windows-authentication"></a>統合 Windows 認証の AD FS のトラブルシューティング
統合 Windows 認証では、エクスペリエンス シングル サインオン (SSO)、Kerberos または NTLM を使用して、Windows 資格情報でログインすることができます。

## <a name="reason-integrated-windows-authentication-fails"></a>理由の統合 windows 認証が失敗しました。
次の 3 つの主な理由は、統合 windows 認証の失敗理由があります。 それらは以下のとおりです。
    - サービス プリンシパル Name(SPN) 構成が正しくないです。
    - チャネル バインディング トークン
    - Internet Explorer の構成

## <a name="spn-misonfiguration"></a>SPN misonfiguration
サービス プリンシパル名 (SPN) は、サービス インスタンスの一意の識別子です。 Spn は、サービスのログオン アカウントにサービス インスタンスを関連付けるの Kerberos 認証で使用されます。 これにより、クライアントは、アカウント名を持っていない場合でも、サービスがアカウントを認証することを要求するクライアント アプリケーションができます。

方法の例で、SPN が使用されます AD FS のとおりです。
1. Web ブラウザー sts.contoso.com を実行しているサービス アカウントを確認する Active Directory のクエリします。
2. Active Directory、AD FS サービス アカウントであるブラウザーに指示します。
3. AD FS サービス アカウントの Kerberos チケットがブラウザーに表示されます。

AD FS サービス アカウントがある、正しく構成されていない、または間違った SPN である場合は、問題が発生このことができます。  ネットワーク トレースを見ると、KRB エラーなどのエラーが発生する可能性があります。KRB5KDC_ERR_S_PRINCIPAL_UNKNOWN.

Wireshark) などのネットワーク トレースを使用してどのような SPN を解決しようとして、ブラウザーとコマンドラインを使用して、ツール、setspn - Q を調べる<spn>、その SPN に対する参照を行うことができます。  見つからない可能性があります。 またはそれを AD FS サービス アカウント以外の別のアカウントに割り当てることができます。

![統合](media/ad-fs-tshoot-iwa/iwa3.png)

SPN は、AD FS サービス アカウントのプロパティを調べることで確認できます。

![統合](media/ad-fs-tshoot-iwa/iwa1.png)

## <a name="channel-binding-token"></a>チャネル バインディング トークン
現時点では、クライアント アプリケーションでは、Kerberos、Digest、または HTTPS を使用して NTLM を使用してサーバーが認証自体、最初にトランスポート レベル セキュリティ (TLS) チャネルが構築されると認証が行われるこのチャネルを使用しています。 

チャネル バインディング トークン TLS で保護された外部チャネルのプロパティであるし、メッセージ交換に、クライアント認証の内部チャネル経由で外部チャネルをバインドするために使用します。

ある場合は、de 暗号化と、SSL トラフィックを再暗号化には、「- the-中間」攻撃が発生し、し、キーは一致しません。  AD FS は、web 参照の r と自体の間の中間にある何かが決まります。  これにより、Kerberos 認証に失敗して、sso ではなく、401 のダイアログ ボックスで、ユーザーが求められます。

原因があります。 このことができます。
 - ブラウザーと AD FS の間に何か
 - Fiddler
 - リバース プロキシの SSL ブリッジングを実行します。

既定では AD FS が「許可」に設定します。  PowerShell コマンドレットを使用してこの設定を変更することができます。 `Set-ADFSProperties -ExtendProtectionTokenCheck`

この参照の詳細については[をセキュリティで保護の計画と AD FS のデプロイのベスト プラクティス](../../ad-fs/design/best-practices-for-secure-planning-and-deployment-of-ad-fs.md)します。

## <a name="internet-explorer-configuration"></a>Internet Explorer の構成
既定では、次のように Internet explorer があるします。

1. Internet explorer では、ヘッダーに、ネゴシエートと AD FS から、401 の応答を受け取ります。
2. AD FS に返送する Kerberos または NTLM チケットを取得する web ブラウザーに指示します。
3. 既定では、IE を単語ネゴシエートがヘッダーにある場合、ユーザーの介入なし (SPNEGO) を実行を試みます。  イントラネット サイトにのみ機能します。

Happeing からこれを妨げる可能性のある 2 つの主な点があります。
   - 統合 Windows 認証を有効には、IE のプロパティではチェックされません。  [詳細設定]-> [インターネット オプション] の下にあるこのセキュリティ]-> [です。
![integrated](media/ad-fs-tshoot-iwa/iwa4.png)
   
   - セキュリティ ゾーンが正しく構成されていません
       - Fqdn はイントラネット ゾーンではありません。
       - AD FS の URL は、イントラネット ゾーンではありません。

![統合](media/ad-fs-tshoot-iwa/iwa5.png)
## <a name="next-steps"></a>次の手順

- [AD FS のトラブルシューティング](ad-fs-tshoot-overview.md)