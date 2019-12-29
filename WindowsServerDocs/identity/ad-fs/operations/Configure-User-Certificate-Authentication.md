---
ms.assetid: 1ea2e1be-874f-4df3-bc9a-eb215002da91
title: ユーザー証明書認証の AD FS サポートを構成する
description: ''
author: jenfieldmsft
ms.author: billmath
manager: samueld
ms.date: 01/18/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 82d826d41e95be18fba689706025ce6f5195f726
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407661"
---
# <a name="configuring-ad-fs-for-user-certificate-authentication"></a>ユーザー証明書認証の AD FS の構成

ユーザー証明書の認証は主に2つのユースケースで使用されます。
* ユーザーは、スマートカードを使用して AD FS システムにサインインしています
* ユーザーがモバイルデバイスにプロビジョニングされた証明書を使用している


## <a name="prerequisites"></a>前提条件
1) [この記事](ad-fs-support-for-alternate-hostname-binding-for-certificate-authentication.md)で説明されているいずれかのモードを使用して、有効にする AD FS ユーザー証明書認証のモードを決定します。
2) ユーザー証明書信頼チェーンが、すべての AD FS および WAP サーバー (中間証明機関を含む) によって信頼されている & インストールされていることを確認します。 通常、これは AD FS/WAP サーバー上の GPO を使用して行われます。
3)  ユーザー証明書の信頼チェーンのルート証明書が、の NTAuth ストアにあることを確認し Active Directory
4) 代替証明書認証モードで AD FS を使用する場合は、AD FS および WAP サーバーに "certauth" (たとえば "certauth.fs.contoso.com") というプレフィックスの付いた AD FS hostname を含む SSL 証明書があり、このホスト名へのトラフィックが許可されていることを確認します。ファイアウォール経由
5) エクストラネットから証明書認証を使用する場合は、証明書に指定されている一覧から、少なくとも1つの AIA と1つ以上の CDP または OCSP の場所にインターネットからアクセスできることを確認してください。
6) また Azure AD 証明書認証の場合、Exchange ActiveSync クライアントの場合、クライアント証明書には、[サブジェクトの別名] フィールドのプリンシパル名または RFC822 名の値のいずれかで、Exchange online のユーザーのルーティング可能な電子メールアドレスが設定されている必要があります。 (Azure Active Directory は、RFC822 値をディレクトリ内のプロキシアドレス属性にマップします)。


## <a name="configure-ad-fs-for-user-certificate-authentication"></a>ユーザー証明書認証用に AD FS を構成する  

AD FS 管理コンソールまたは PowerShell コマンドレット`Set-AdfsGlobalAuthenticationPolicy`を使用して AD FS で、イントラネットまたはエクストラネットの認証方法としてユーザー証明書認証を有効にします。

Azure AD 証明書認証の AD FS を構成する場合は、証明書の発行者とシリアル番号に必要な[Azure AD 設定](https://docs.microsoft.com/azure/active-directory/active-directory-certificate-based-authentication-get-started#step-2-configure-the-certificate-authorities)と[AD FS 要求規則](https://docs.microsoft.com/azure/active-directory/active-directory-certificate-based-authentication-ios#requirements)を構成していることを確認します。

また、いくつかのオプションの側面もあります。
- EKU (要求の種類 https://schemas.microsoft.com/2012/12/certificatecontext/extension/eku) ) に加えて、証明書のフィールドと拡張機能に基づく要求を使用する場合は、Active Directory 要求プロバイダー信頼の規則に従って追加の要求パスを構成します。  利用可能な証明書の要求の完全な一覧については、以下を参照してください。  
- 証明書の種類に基づいてアクセスを制限する必要がある場合は、アプリケーションの発行承認規則 AD FS で、証明書の追加のプロパティを使用できます。 一般的なシナリオは、"MDM プロバイダーによってプロビジョニングされた証明書のみを許可する" または "スマートカード証明書のみを許可する" です。
- [この記事](https://technet.microsoft.com/library/dn786429(v=ws.11).aspx)の「クライアント認証の信頼された発行者の管理」にあるガイダンスを使用して、クライアント証明書に対して許可されている発行証明機関を構成します。
- 証明書認証を行う場合は、エンドユーザーのニーズに合わせてサインインページを変更することをお勧めします。 一般的なケースとしては、(a) "X509 証明書によるサインイン" をエンドユーザーにとって使いやすいものに変更します。

## <a name="configure-seamless-certificate-authentication-for-chrome-browser-on-windows-desktops"></a>Windows デスクトップで Chrome ブラウザーのシームレスな証明書認証を構成する
クライアント認証の目的を満たす複数のユーザー証明書 (Wi-fi 証明書など) がコンピューター上に存在する場合、Windows デスクトップの Chrome ブラウザーによって、適切な証明書を選択するように求めるメッセージが表示されます。 これは、エンドユーザーの混乱を招く可能性があります。 このエクスペリエンスを最適化するために、Chrome のポリシーを設定して、適切な証明書を自動的に選択してユーザーエクスペリエンスを向上させることができます。 このポリシーを手動で設定するには、レジストリを変更するか、GPO を使用して自動的に構成する (レジストリキーを設定する) 必要があります。 これには、AD FS に対する認証にユーザークライアント証明書が必要です。これは、他のユースケースとは別の発行者になります。 

Chrome 用にこれを構成する方法の詳細については、こちらの[リンク](http://www.chromium.org/administrators/policy-list-3#AutoSelectCertificateForUrls)を参照してください。  


## <a name="troubleshoot-certificate-authentication"></a>証明書認証のトラブルシューティング
このドキュメントでは、ユーザーの証明書認証用に AD FS が構成されている場合の一般的な問題のトラブルシューティングに焦点を当てています。 

### <a name="check-if-certificate-trusted-issuers-is-configured-properly-in-all-the-ad-fswap-servers"></a>証明書の信頼された発行者がすべての AD FS/WAP サーバーで適切に構成されているかどうかを確認する
*一般的な症状:HTTP 204 "https\://certuath.adfs.contoso.com からのコンテンツはありません"*

AD FS は、基になる windows オペレーティングシステムを使用してユーザー証明書を所有していることを証明し、証明書信頼チェーン検証を行って信頼された発行者と一致していることを確認します。 信頼された発行者と一致させるには、すべてのルートと中間機関がローカルコンピューターの証明機関ストアの信頼された発行者として構成されていることを確認する必要があります。 これを自動的に検証するには、 [AD FS 診断アナライザーツール](https://adfshelp.microsoft.com/DiagnosticsAnalyzer/Analyze)を使用してください。 このツールはすべてのサーバーに対してクエリを行い、適切な証明書が正しくプロビジョニングされていることを確認します。 
1)  上記のリンクに記載されている手順に従って、ツールをダウンロードして実行します。
2)  結果をアップロードし、エラーがないか確認します

### <a name="check-if-certificate-authentication-is-enabled-in-the-ad-fs-authentication-policy"></a>AD FS 認証ポリシーで証明書認証が有効になっているかどうかを確認する
AD FS は、既定で証明書認証を有効にしません。 証明書認証を有効にする方法については、このドキュメントの冒頭を参照してください。 

### <a name="check-if-certificate-authentication-is-enabled-in-the-ad-fs-authentication-policy"></a>AD FS 認証ポリシーで証明書認証が有効になっているかどうかを確認する
AD FS は、AD FS と同じホスト名を持つポート49443で、既定でユーザー証明書の`adfs.contoso.com`認証を行います (例:)。 また、代替 SSL バインドを使用してポート 443 (既定の HTTPS ポート) を使用するように AD FS を構成することもできます。 ただし、この構成で使用される URL `certauth.<adfs-farm-name>`はです ( `certauth.contoso.com`例:)。 詳細については、こちらの[リンク](ad-fs-support-for-alternate-hostname-binding-for-certificate-authentication.md)を参照してください。 ネットワーク接続の最も一般的なケースは、ファイアウォールが正しく構成されていないこと、およびユーザー証明書の認証トラフィックがブロックまたは妨げになっていることです。 通常、この問題が発生すると、空の画面または500サーバーエラーが表示されます。 
1)  「」で構成したホスト名とポートに注意してください AD FS
2)  AD FS または Web アプリケーションプロキシ (WAP) の前にあるすべてのファイアウォールが、AD FS `hostname:port`ファームとの組み合わせを許可するように構成されていることを確認します。 この手順を実行するには、ネットワークエンジニアに参照する必要があります。 

### <a name="check-certificate-revocation-list-connectivity"></a>証明書失効リストの接続を確認する
証明書失効リスト (CRL) は、ランタイムの失効確認を実行するためにユーザー証明書にエンコードされるエンドポイントです。 たとえば、証明書を含むデバイスが盗まれた場合、管理者は失効した証明書の一覧に証明書を追加できます。 これまでにこの証明書を受け入れたエンドポイントは、認証に失敗します。

すべての AD FS および WAP サーバーは、提示された証明書がまだ有効であり、失効していないかどうかを検証するために、CRL エンドポイントに達している必要があります。 CRL 検証は、HTTPS、HTTP、LDAP、または OCSP (オンライン証明書状態プロトコル) 経由で実行できます。 AD FS/WAP サーバーがエンドポイントに接続できない場合、認証は失敗します。 トラブルシューティングを行うには、次の手順に従います。 
1) Pki システムからユーザー証明書を失効させるために使用する CRL エンドポイントを確認するには、PKI エンジニアに問い合わせてください。 
2)  各 AD FS/WAP サーバーで、使用されているプロトコル (通常は HTTPS または HTTP) を介して CRL エンドポイントに到達可能であることを確認します。
3)  高度な検証を行うには、各 AD FS/WAP サーバーで[CAPI2 イベントログを有効に](https://blogs.msdn.microsoft.com/benjaminperkins/2013/09/30/enable-capi2-event-logging-to-troubleshoot-pki-and-ssl-certificate-issues/)します。
4) CAPI2 操作ログでイベント ID 41 (失効の確認) を確認します。
5) 確認する対象`‘\<Result value="80092013"\>The revocation function was unable to check revocation because the revocation server was offline.\</Result\>'`

***ヒント***:特定のサーバーを指すように DNS 解決 (Windows 上の HOSTS ファイル) を構成することで、トラブルシューティングを容易にするために1つの AD FS または WAP サーバーを対象にすることができます。 これにより、サーバーを対象とするトレースを有効にすることができます。 

### <a name="check-if-this-is-a-server-name-indication-sni-issue"></a>これが Server Name Indication (SNI) の問題かどうかを確認する
AD FS では、クライアントデバイス (またはブラウザー) とロードバランサーが SNI をサポートする必要があります。 一部のクライアントデバイス (通常、古いバージョンの Android) は SNI をサポートしていない可能性があります。 また、ロードバランサーが SNI をサポートしていないか、SNI 用に構成されていない可能性があります。 これらのインスタンスでは、ユーザーの認証エラーが発生する可能性があります。 
1)  ネットワークエンジニアと協力して、AD FS/WAP の Load Balancer が SNI をサポートしていることを確認する
2)  SNI がサポートされない場合 AD FS 次の手順に従って対処できます。
    *   プライマリ AD FS サーバーで管理者特権でのコマンドプロンプトウィンドウを開く
    *   入力```Netsh http show sslcert```
    *   フェデレーションサービスの ' アプリケーション GUID ' と ' certificate hash ' をコピーする
    *   入力`netsh http add sslcert ipport=0.0.0.0:{your_certauth_port} certhash={your_certhash} appid={your_applicaitonGUID}`

### <a name="check-if-the-client-device-has-been-provisioned-with-the-certificate-correctly"></a>クライアントデバイスに証明書が正しくプロビジョニングされているかどうかを確認する
一部のデバイスは正常に機能していますが、他のデバイスは動作していません。 この場合、通常、クライアントデバイスにユーザー証明書が正しくプロビジョニングされていないことが原因です。 次の手順に従います。 
1)  この問題が Android デバイスに固有のものである場合、最も一般的な問題は、証明書チェーンが Android デバイスで完全に信頼されていないことです。  MDM ベンダーに問い合わせて、証明書が正しくプロビジョニングされており、チェーン全体が Android デバイスで完全に信頼されていることを確認します。 
2)  この問題が Windows デバイスに固有のものである場合は、ログインしているユーザーの Windows 証明書ストア (システム/コンピューターではありません) を確認して、証明書が正しくプロビジョニングされているかどうかを確認します。
3)  クライアントユーザー証明書を .cer ファイルにエクスポートし、コマンド "certutil-f-urlfetch-verify certificatefilename .cer" を実行します。


### <a name="check-if-the-tls-version-is-compatible-between-ad-fswap-servers-and-the-client-device"></a>TLS のバージョンが AD FS/WAP サーバーとクライアントデバイス間で互換性があるかどうかを確認します。
まれに、クライアントデバイス (通常はモバイルデバイス) は、より新しいバージョンの TLS のみをサポートするように更新されます (たとえば、1.3)。または、AD FS/WAP サーバーが更新され、より高い TLS バージョンのみが使用され、クライアントデバイスでサポートされていない場合もあります。 オンライン SSL ツールを使用して、AD FS/WAP サーバーを確認し、デバイスと互換性があるかどうかを確認できます。 TLS のバージョンを制御する方法の詳細については、こちらの[リンク](manage-ssl-protocols-in-ad-fs.md)を参照してください。

### <a name="check-if-azure-ad-promptloginbehavior-is-configured-correctly-on-your-federated-domain-settings"></a>Azure AD PromptLoginBehavior がフェデレーションドメインの設定で正しく構成されているかどうかを確認します。
多くの Office 365 アプリケーションは、prompt = login を Azure AD に送信します。 Azure AD、既定では、AD FS するために新しいパスワードログインに変換します。 その結果、AD FS で証明書の認証を構成した場合でも、エンドユーザーにはパスワードのログインのみが表示されます。 
1)  ' Set-msoldomainfederationsettings ' コマンドレットを使用してフェデレーションドメイン設定を取得します
2)  PromptLoginBehavior パラメーターが ' Disabled ' または ' NativeSupport ' のいずれかに設定されていることを確認してください

詳細については、こちらの[リンク](ad-fs-prompt-login.md)を参照してください。 

### <a name="additional-troubleshooting"></a>その他のトラブルシューティング
これはまれなことです。
1)  CRL の一覧が非常に長い場合は、ダウンロードを試行したときにタイムアウトになることがあります。 その場合は、' MaxFieldLength ' と ' Maxfieldlength ' を更新する必要があります。 https://support.microsoft.com/en-us/help/820129/http-sys-registry-settings-for-windows




## <a name="reference-complete-list-of-user-certificate-claim-types-and-example-values"></a>参照 :ユーザー証明書の要求の種類と値の例の完全な一覧

|                                         要求の種類                                         |                              値の例                               |
|--------------------------------------------------------------------------------------------|--------------------------------------------------------------------------|
|         https://schemas.microsoft.com/2012/12/certificatecontext/field/x509version         |                                    3                                     |
|     https://schemas.microsoft.com/2012/12/certificatecontext/field/signaturealgorithm      |                                sha256RSA                                 |
|           https://schemas.microsoft.com/2012/12/certificatecontext/field/issuer            |                 CN = entca、DC = domain、DC = contoso、DC = com                  |
|         https://schemas.microsoft.com/2012/12/certificatecontext/field/issuername          |                 CN = entca、DC = domain、DC = contoso、DC = com                  |
|          https://schemas.microsoft.com/2012/12/certificatecontext/field/notbefore          |                           12/05/2016 20:50:18                            |
|          https://schemas.microsoft.com/2012/12/certificatecontext/field/notafter           |                           12/05/2017 20:50:18                            |
|           https://schemas.microsoft.com/2012/12/certificatecontext/field/subject           |   E =user@contoso.com、CN = user、CN = Users、dc = domain、dc = contoso、dc = com   |
|         https://schemas.microsoft.com/2012/12/certificatecontext/field/subjectname         |   E =user@contoso.com、CN = user、CN = Users、dc = domain、dc = contoso、dc = com   |
|           https://schemas.microsoft.com/2012/12/certificatecontext/field/rawdata           |                {Base64 でエンコードされたデジタル証明書データ}                 |
|        https://schemas.microsoft.com/2012/12/certificatecontext/extension/keyusage         |                             Digitalsignature ビット                             |
|        https://schemas.microsoft.com/2012/12/certificatecontext/extension/keyusage         |                             KeyEncipherment                              |
|  https://schemas.microsoft.com/2012/12/certificatecontext/extension/subjectkeyidentifier   |                 9D11941EC06FACCCCB1B116B56AA97F3987D620A                 |
| https://schemas.microsoft.com/2012/12/certificatecontext/extension/authoritykeyidentifier  |    キー Id = d6 13 e3 6b bc e5 d8 15 52 0a fd 36 6a d5 0b 51 f3 0b 25 7f     |
| https://schemas.microsoft.com/2012/12/certificatecontext/extension/certificatetemplatename |                                   User                                   |
|           https://schemas.microsoft.com/2012/12/certificatecontext/extension/san           | その他の名前: プリンシパルuser@contoso.com名 =、RFC822 名 =user@contoso.com |
|           https://schemas.microsoft.com/2012/12/certificatecontext/extension/eku           |                          1.3.6.1.4.1.311.10.3.4                          |

## <a name="related-links"></a>関連リンク
* [AD FS 証明書認証の代替ホスト名バインドを構成する](ad-fs-support-for-alternate-hostname-binding-for-certificate-authentication.md)
* [Azure AD で証明機関を構成する](https://docs.microsoft.com/azure/active-directory/active-directory-certificate-based-authentication-get-started#step-2-configure-the-certificate-authorities)
