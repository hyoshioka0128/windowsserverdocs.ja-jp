---
ms.assetid: acc9101b-841c-4540-8b3c-62a53869ef7a
title: "AD FS 2016 に関する FAQ"
description: "AD FS 2016 についてよく寄せられる質問"
author: jenfieldmsft
ms.author: billmath
manager: femila
ms.date: 03/06/2018
ms.topic: article
ms.custom: it-pro
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 313447d2c92c15505434ec5c39898ca84aef46db
ms.sourcegitcommit: 556361fe7c73c75d6cdc46a67dc88679fbe89c61
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2018
---
# <a name="ad-fs-frequently-asked-questions-faq"></a>AD FS のよく寄せられる質問 (FAQ)

>Windows Server 2016 の適用対象:

次のドキュメントは、Active Directory フェデレーション サービスに関してよく寄せられる質問へのホームです。  ドキュメントの質問の種類に基づくグループに分割されました。

## <a name="deployment"></a>展開 

### <a name="how-can-i-upgrademigrate-from-previous-versions-of-ad-fs"></a>移行する方法をアップグレード/AD FS の以前のバージョンから
AD FS を使用して、次のいずれかをアップグレードすることができます。


- Windows Server 2016 の AD FS を Windows Server 2012 R2 AD FS
    - [WID データベースを使用して Windows Server 2016 での AD FS へのアップグレード](../deployment/Upgrading-to-AD-FS-in-Windows-Server-2016.md)
    - [SQL データベースを使用して Windows Server 2016 での AD FS へのアップグレード](../deployment/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL.md)
- Windows Server 2012 に AD FS を Windows Server 2012 R2 AD FS
    - [Windows Server 2012 R2 で AD FS への移行します。](https://technet.microsoft.com/library/dn486815.aspx)
- Windows Server 2012 AD FS には、AD FS 2.0
    - [Windows Server 2012 で AD FS への移行します。](https://technet.microsoft.com/library/jj647765.aspx)
- AD FS 1.x と AD FS 2.0 
    - [AD FS からのアップグレードに AD FS 2.0 1.x](https://technet.microsoft.com/library/ff678035.aspx)

AD FS 2.0 または 2.1 (Windows Server 2008 R2 または Windows Server 2012) からアップグレードする場合は、(C:\Windows\ADFS にある) ボックスでスクリプトを使用する必要があります。

### <a name="why-does-ad-fs-installation-require-a-reboot-of-the-server"></a>AD FS のインストールでサーバーの再起動が必要なはなぜですか。

Windows Server 2016 で HTTP/2 のサポートが追加されましたが、HTTP/2 は、クライアント証明書の認証には使用できません。  多くの AD FS シナリオ再試行をサポートしていませんクライアント証明書の認証の使用とクライアント操作の数が多いために要求 http/1.1、AD FS ファーム構成再構成を使用して http/1.1 にローカル サーバーの HTTP 設定します。  これには、サーバーの再起動が必要です。  

### <a name="is-using-windows-2016-wap-servers-to-publish-the-ad-fs-farm-to-the-internet-without-upgrading-the-back-end-ad-fs-farm-supported"></a>Windows 2016 WAP サーバーを使用して、サポートされているバックエンドの AD FS ファームをアップグレードすることがなく、AD FS ファームをインターネットに公開しますか。
はい、この構成はサポートされて、ただし、この構成での AD FS 2016 の新機能はサポートされません。  この構成では、AD FS 2016 には、AD FS 2012 R2 から移行フェーズ中に一時的なものでは、長期間のない展開されている必要があります。

## <a name="design"></a>設計

### <a name="what-third-party-multi-factor-authentication-providers-are-available-for-ad-fs"></a>どのようなサード パーティの多要素認証プロバイダーは、AD FS の使用可能ないますか。 
以下は、対応のサード パーティ プロバイダーの一覧に示します。  おについて把握していないことと、それらについて学習一覧を更新しましたが、使用可能なプロバイダー常にあります。

- [Gemalto アイデンティティ & セキュリティ サービス](http://www.gemalto.com/identity)
- [inWebo エンタープライズ認証サービス](http://www.inwebo.com/)
- [ログイン People MFA API コネクタ](https://www.loginpeople.com)
- [Microsoft Active Directory フェデレーション サービスの RSA SecurID 認証エージェント](http://www.emc.com/security/rsa-securid/rsa-authentication-agents/microsoft-ad-fs.htm)
- [AD FS の SafeNet Authentication サービス (SAS) エージェント](http://www.safenet-inc.com/resources/integration-guide/data-protection/Safenet_Authentication_Service/SafeNet_Authentication_Service__AD_FS_Agent_Configuration_Guide/?langtype=1033)
- [Swisscom 社 Mobile ID 認証サービス](http://swisscom.ch/mid)
- [Symantec の検証と ID Protection Service (VIP)](http://www.symantec.com/vip-authentication-service) 

### <a name="are-third-party-proxies-supported-with-ad-fs"></a>サード パーティ製プロキシは、AD FS でサポートされますか。
はい、サード パーティ製プロキシは、Web アプリケーション プロキシは、前に配置することができますが、任意のサード パーティ製プロキシをサポートする必要があります、[MS ADFSPIP プロトコル](https://msdn.microsoft.com/library/dn392811.aspx)Web アプリケーション プロキシの代わりに使用します。

### <a name="what-third-party-proxies-are-available-for-ad-fs-that-support-ms-adfspip"></a>どのようなサード パーティ製プロキシは、MS ADFSPIP をサポートするための AD FS の使用可能ないますか。

以下は、対応のサード パーティ プロバイダーの一覧に示します。  おについて把握していないことと、それらについて学習一覧を更新しましたが、使用可能なプロバイダー常にあります。

- [F5 キーを押してアクセス ポリシー マネージャー](https://support.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-third-party-integration-13-1-0/12.html#guid-1ee8fbb3-1b33-4982-8bb3-05ae6868d9ee)

### <a name="where-is-the-capacity-planning-sizing-spreadsheet-for-ad-fs-2016"></a>ここでは、キャパシティ プランニング サイジング スプレッドシート AD FS 2016 ですか。
スプレッドシートの AD FS 2016 バージョンをダウンロードできます[ここ](http://adfsdocs.blob.core.windows.net/adfs/ADFSCapacity2016.xlsx)します。
これは、Windows Server 2012 R2 の AD FS で使用できます。

### <a name="how-can-i-ensure-my-ad-fs-and-wap-servers-support-apples-atp-requirements"></a>どうすれば確認できます、AD FS と WAP サーバーがサポート Apple の ATP 要件ですか。

Apple には、AD FS に対して認証する iOS アプリからの呼び出しに影響を与える可能性アプリ トランスポート セキュリティ (ATS) と呼ばれる要件のセットをリリースしました。  おくと、AD FS と WAP サーバーがサポートしていることを確認することによって準拠、[ATS を使用して接続するための要件](https://developer.apple.com/library/prerelease/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW57)します。  
具体的には、AD FS と WAP サーバーで TLS 1.2 をサポートし、TLS 接続のネゴシエートされた暗号スイートが最適な前方の機密性をサポートすることを確認する必要があります。

有効にして、SSL 2.0、3.0、TLS バージョン 1.0、1.1、1.2 を無効にすることができますを使用して[AD FS での SSL プロトコルの管理](../operations/Manage-SSL-Protocols-in-AD-FS.md)します。

AD FS と WAP ことを確認するにはサーバー ATP をサポートする唯一の TLS 暗号スイートをネゴシエートするに追加されていないすべての暗号スイートを無効にすることができます、[ATP 準拠の暗号スイートのリスト](https://developer.apple.com/library/prerelease/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW57)します。  これを行うを使用して、[Windows TLS PowerShell コマンドレット](https://technet.microsoft.com/itpro/powershell/windows/tls/index)します。 


## <a name="operations"></a>操作

### <a name="how-do-i-replace-the-ssl-certificate-for-ad-fs"></a>AD FS の SSL 証明書を交換する方法 
AD FS の SSL 証明書は、AD FS 管理スナップインで見つかった AD FS サービス通信証明書と同じではないです。  AD FS の SSL 証明書を変更するには、PowerShell を使用する必要があります。 以下の記事のガイダンスに従います。

[AD FS と WAP 2016 で SSL 証明書の管理](../operations/Manage-SSL-Certificates-AD-FS-WAP-2016.md)

### <a name="how-can-i-enable-or-disable-tlsssl-settings-for-ad-fs"></a>または方法は有効にする AD FS の TLS と SSL の設定を無効にします。
無効にし、SSL プロトコルを有効にするか、暗号スイート、次の手順に従います。

[AD FS での SSL プロトコルを管理します。](../operations/Manage-SSL-Protocols-in-AD-FS.md)

### <a name="does-the-proxy-ssl-certificate-have-to-be-the-same-as-the-ad-fs-ssl-certificate"></a>プロキシの SSL 証明書は、AD FS の SSL 証明書と同じにするか。  
プロキシの SSL 証明書および AD FS の SSL 証明書に関する次のガイダンスを使用します。


- 統合 Windows 認証、プロキシの SSL 証明書を使用する AD FS プロキシ要求が (同じキーを使用) と同じフェデレーション サーバーの SSL 証明書をする必要があります、プロキシを使用する場合
- プロキシの SSL 証明書が (同じキーを使用) と同じフェデレーション サーバーの SSL 証明書をする必要があります"ExtendedProtectionTokenCheck"は、AD FS プロパティには、(既定の AD FS で設定) が有効な場合、
- それ以外の場合、プロキシの SSL 証明書は、AD FS の SSL 証明書から別のキーを持つことができますが、同じを満たす必要があります[要件](../overview/AD-FS-2016-Requirements.md)

### <a name="how-can-i-configure-promptlogin-behavior-for-ad-fs"></a>プロンプトを構成する方法の AD FS のログインの動作を = ですか?
プロンプトを構成する方法について = ログイン時を参照してください[Active Directory フェデレーション サービスのプロンプト ログイン パラメーターのサポートを =](../operations/AD-FS-Prompt-Login.md)します。

### <a name="how-can-i-configure-browsers-to-use-windows-integrated-authentication-wia-with-ad-fs"></a>AD FS に Windows 統合認証 (WIA) を使用するようにブラウザーを構成する方法

ブラウザーを構成する方法については、次を参照してください。[AD FS に Windows 統合認証 (WIA) を使用するようにブラウザーを構成する](../operations/Configure-AD-FS-Browser-WIA.md)します。


### <a name="how-long-are-ad-fs-tokens-valid"></a>有効な AD FS トークンはどのくらいの期間のですか。

多くの場合この質問は、' 時間の長さはユーザーを取得するシングル サインオン (SSO) を新しい資格情報を入力しなくても方法制御できますか。管理者ですか?"  この動作し、それを制御する構成設定が、記事で説明されている[ここ](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/operations/ad-fs-2016-single-sign-on-settings)します。

さまざまな Cookie とトークンの既定の有効期間は、(このパラメーターは、有効期間を制御する) と同様、以下に示します。

**登録済みデバイス**

- PRT と SSO の Cookie: PSSOLifeTimeMins の対象となる、最大 90 日間です。 (提供されているデバイスを使用には、少なくとも 14 日に、DeviceUsageWindow で制御されている)

- 更新トークン: 一貫した動作を提供するには、上記のに基づいて計算

- access_token: 証明書利用者のパーティに基づいて、既定では、1 時間

- id_token: アクセス トークンと同じ

**デバイスを登録解除**

- SSO Cookie: 既定では、8 時間が SSOLifetimeMins によって左右されます。  (KMSI) に記録 Me 保持が有効な場合、既定では 24 時間と KMSILifetimeMins を使用して構成できます。


- トークンを更新します。既定では 8 時間です。 24 時間で有効になっている KMSI

- access_token: 証明書利用者のパーティに基づいて、既定では、1 時間

- id_token: アクセス トークンと同じ

### <a name="does-ad-fs-support-http-strict-transport-security-hsts"></a>AD FS は HTTP Strict Transport Security (HSTS) をサポートしますか。  

HTTP Strict Transport Security (HSTS) は、ダウン グレード攻撃のプロトコルと HTTP と HTTPS の両方のエンドポイントのサービスの Cookie ハイジャックを軽減するのに役立ちます Web セキュリティ ポリシー メカニズムです。 Web サーバーを Web ブラウザー (または complying 他のユーザー エージェント) する必要がありますのみとやり取りする HTTPS を使用して HTTP プロトコル経由でないを宣言できます。

Web 認証トラフィックのすべての AD FS エンドポイントが HTTPS 経由で排他的で開きます。  その結果、AD FS を効率的に軽減 HTTP Strict Transport Security ポリシーのメカニズムを提供する脅威 (仕様ではありません HTTP にダウン グレードで HTTP リスナーはないため)。 さらに、AD FS では、セキュリティで保護されたフラグを使用してすべての Cookie をマークすることによって、HTTP プロトコルのエンドポイントで別のサーバーに送信されることから、Cookie ができないようにします。

そのため、AD FS サーバーに HSTS を実装する必要はありませんができることはありませんダウン グレードするためです。  コンプライアンスのために、AD FS サーバーは HTTP を使用できることはありませんし、すべての Cookie がセキュリティで保護されたマークされているためにこれらの要件を満たしています。

### <a name="x-ms-forwarded-client-ip-does-not-contain-the-ip-of-the-client-but-contains-ip-of-the-firewall-in-front-of-the-proxy-where-can-i-get-the-right-ip-of-the-client"></a>X-ms-転送-クライアントの ip アドレスは、クライアントの ip アドレスが含まれていないが、プロキシの前に、ファイアウォールの ip アドレスが含まれています。 クライアントの正しい IP はどこで入手できますか。
WAP する前に、SSL ターミネーションを行うには推奨されません。 場合に、WAP の前に、SSL ターミネーション機能が完了したら、X-ms-転送-クライアントの ip アドレスには WAP の前に、ネットワーク デバイスの ip アドレスが含まれます。 AD FS でサポートされている要求を関連するさまざまな IP の簡単な説明を次に示します。
 - X ms クライアント ip: ネットワーク、STS へ接続するデバイスの ip アドレスです。  エクストラネットの要求の場合は常に、WAP の ip アドレスが表示されます。
 - x-ms-転送-クライアントの ip アドレス: Exchange Online と WAP に接続されているデバイスの IP アドレスによって ADFS に転送されるすべての値が含まれる複数値の要求。
 - Userip: エクストラネットの要求のこの要求が含まれます x-ms-転送-クライアントの ip アドレスの値。  この要求では、イントラネットの要求の x ms クライアント ip と同じ値が含まれます。

### <a name="i-am-trying-to-get-additional-claims-on-the-user-info-endpoint-but-its-only-returning-subject-how-can-i-get-additional-claims"></a>ユーザー情報のエンドポイントでの他の信頼性情報を取得しようとしていますが、件名のみを返します。 その他の信頼性情報を取得する方法
ADFS ユーザー情報のエンドポイントは、常に、OpenID 標準で指定されている件名要求を返します。 AD FS では、ユーザー情報エンドポイント経由で要求されたその他の信頼性情報は提供されません。 ID トークンで信頼性情報を追加する場合を参照してください。[AD FS でのカスタム ID トークン](../development/custom-id-tokens-in-ad-fs.md)します。

### <a name="why-do-i-see-alot-of-1021-errors-on-my-ad-fs-servers"></a>Why do I see alot of 1021 errors on my AD FS servers?
This event is logged usually for an invalid resource access on AD FS for resource 00000003-0000-0000-c000-000000000000. This error is caused by an erroneous behavior of the client where it tries to get an access token for the Azure AD Graph service. Since the resource is not present on AD FS, this results in event ID 1021 on the AD FS servers. It’s safe to ignore any warnings or errors for resource 00000003-0000-0000-c000-000000000000 on AD FS. 

### <a name="why-am-i-seeing-a-warning-for-failure-to-add-the-ad-fs-service-account-to-the-enterprise-key-admins-group"></a>Why am I seeing a warning for failure to add the AD FS service account to the Enterprise Key Admins group?
This group is only created when a Windows 2016 Domain Controller with the FSMO PDC role exists in the Domain. To resolve the error, you can create the Group manually and follow the below to give the required permission after adding the service account as member of the group.
1.  Open **Active Directory Users and Computers**. 
2.  **Right-click** your domain name from the navigation pane and **click** Properties.
3.  **Click** Security (if the Security tab is missing, turn on Advanced Features from the View menu).
4.  **Click** Advanced. **Click** Add. **Click** Select a principal.
5.  The Select User, Computer, Service Account, or Group dialog box appears.  In the Enter the object name to select text box, type Key Admin Group.  [Ok] をクリックします。
6.  In the Applies to list box, select **Descendant User objects**.
7.  Using the scroll bar, scroll to the bottom of the page and **click** Clear all.
8.  In the **Properties** section, select **Read msDS-KeyCredentialLink** and **Write msDS-KeyCrendentialLink**.

### <a name="why-does-modern-authentication-from-android-devices-fail-if-the-server-does-not-send-all-the-intermediate-certificates-in-the-chain-with-the-ssl-cert"></a>Why does modern authentication from Android devices fail if the server does not send all the intermediate certificates in the chain with the SSL cert?

Federated users may experience authentication to Azure AD for apps that use the Android ADAL library failing. The app will get an **AuthenticationException** when it tries to show the login page. In chrome the AD FS login page might be called out as unsafe.

Android - across all versions and all devices - does not support downloading additional certificates from the **authorityInformationAccess** field of the certificate. This is true of the Chrome browser as well. Any Server Authentication certificate that’s missing intermediate certificates will result in this error if the entire certificate chain is not passed from AD FS. 

A proper solution to this problem is to configure the AD FS and WAP servers to send the necessary intermediate certificates along with the SSL certificate. 

When exporting the SSL certificate, from one machine, to be imported to the computer’s personal store, of the AD FS and WAP server(s), make sure to export the Private key and select **Personal Information Exchange - PKCS #12**. 

It is important that the check box to **Include all certificates in the certificate path if possible** is checked, as well as **Export all extended properties**. 

Run certlm.msc on the Windows servers and import the *.PFX into the Computer’s Personal Certificate store. This will cause the server to pass the entire certificate chain to the ADAL library. 

>[!NOTE]
> The certificate store of Network Load Balancers should also be updated to include the entire certificate chain if present

### <a name="does-ad-fs-support-head-requests"></a>Does AD FS support HEAD requests?
AD FS does not support HEAD requests.  Applications should not be using HEAD requests against AD FS endpoints.  This may cause HTTP error responses that are unexpected and/or delayed.  Additionally, you may see unexpected error events in the AD FS event log.

### <a name="why-am-i-not-seeing-a-refresh-token-when-i-am-logging-in-with-a-remote-idp"></a>理由は確認できない更新トークンはリモート IdP でログインしているときにしますか。
IdP によって発行されたトークンには、validty 1 時間未満の場合、更新トークンが発行されません。 更新トークンが発行されることを確認するには、1 時間以上の IdP によって発行されたトークンの有効性を増やします。
