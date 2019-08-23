---
ms.assetid: acc9101b-841c-4540-8b3c-62a53869ef7a
title: AD FS FAQ
description: AD FS に関してよく寄せられる質問
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 04/17/2019
ms.topic: article
ms.custom: it-pro
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 7bc98a8c9a57b2b7f63523f0411d648ca82137aa
ms.sourcegitcommit: 2082335e1260826fcbc3dccc208870d2d9be9306
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69980338"
---
# <a name="ad-fs-frequently-asked-questions-faq"></a>AD FS に関してよく寄せられる質問 (FAQ)


次のドキュメントでは、Active Directory フェデレーションサービス (AD FS) に関してよく寄せられる質問とその回答を示します。  ドキュメントは、質問の種類に基づいてグループに分割されています。

## <a name="deployment"></a>展開

### <a name="how-can-i-upgrademigrate-from-previous-versions-of-ad-fs"></a>以前のバージョンの AD FS からアップグレードまたは移行する方法
次のいずれかを使用して AD FS をアップグレードできます。


- Windows Server 2012 R2 は、Windows Server 2016 AD FS 以降に AD FS ます。 方法は、Windows Server 2016 AD FS から Windows Server 2019 AD FS にアップグレードする場合と同じであることに注意してください。 
    - [WID データベースを使用した、Windows Server 2016 での AD FS へのアップグレード](../deployment/Upgrading-to-AD-FS-in-Windows-Server-2016.md)
    - [SQL データベースを使用した、Windows Server 2016 での AD FS へのアップグレード](../deployment/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL.md)
- Windows server 2012 AD FS Windows Server 2012 R2 AD FS
    - [Windows Server 2012 R2 の AD FS への移行](https://technet.microsoft.com/library/dn486815.aspx)
- AD FS 2.0 から Windows Server 2012 AD FS
    - [Windows Server 2012 の AD FS への移行](https://technet.microsoft.com/library/jj647765.aspx)
- AD FS 1.x AD FS 2.0
    - [AD FS 1.x から AD FS 2.0 にアップグレードします。](https://technet.microsoft.com/library/ff678035.aspx)

AD FS 2.0 または 2.1 (Windows Server 2008 R2 または Windows Server 2012) からアップグレードする必要がある場合は、(C:\Windows\ADFS にある) インボックススクリプトを使用する必要があります。

### <a name="why-does-ad-fs-installation-require-a-reboot-of-the-server"></a>AD FS のインストールにサーバーの再起動が必要なのはなぜですか。

Windows Server 2016 で HTTP/2 のサポートが追加されましたが、クライアント証明書の認証に HTTP/2 を使用することはできません。  多くの AD FS シナリオではクライアント証明書認証が使用され、多数のクライアントが HTTP/1.1 を使用した要求の再試行をサポートしていないため、AD FS ファーム構成によってローカルサーバーの HTTP 設定が HTTP/1.1 に再構成されます。  これには、サーバーの再起動が必要です。  

### <a name="is-using-windows-2016-wap-servers-to-publish-the-ad-fs-farm-to-the-internet-without-upgrading-the-back-end-ad-fs-farm-supported"></a>Windows 2016 WAP サーバーを使用して、バックエンド AD FS ファームをアップグレードせずに AD FS ファームをインターネットに発行していますか。
はい。この構成はサポートされていますが、この構成では新しい AD FS 2016 機能はサポートされません。  この構成は、AD FS 2012 R2 から AD FS 2016 への移行フェーズ中に一時的なものとして、長時間にわたって展開すべきではありません。

### <a name="is-it-possible-to-deploy-ad-fs-for-office-365-without-publishing-a-proxy-to-office-365"></a>Office 365 にプロキシを発行せずに、Office 365 の AD FS を展開することはできますか。
はい、これはサポートされています。 ただし、副作用として

1. Azure AD がフェデレーションメタデータにアクセスできないため、更新トークン署名証明書を手動で管理する必要があります。 トークン署名証明書を手動で更新する方法の詳細については[、「Office 365 用フェデレーション証明書を更新する」および Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-o365-certs)を参照してください。
2. レガシ認証フロー (例: ExO プロキシ認証フロー) を利用することはできません。

### <a name="what-are-load-balancing-requirements-for-ad-fs-and-wap-servers"></a>AD FS と WAP サーバーの負荷分散の要件は何ですか。

AD FS はステートレスシステムです。 そのため、負荷分散はログインには非常に簡単です。 負荷分散システムの主な推奨事項を次に示します。


- ロードバランサーは、IP アフィニティを使用して構成しないでください。 このため、特定の Exchange Online のシナリオでは、サーバーのサブセットに過度の負荷がかかる可能性があります。
- ロードバランサーは、HTTPS 接続を終了して、ADFS サーバーへの新しい接続を再開することはできません。
- ロードバランサーは、ADFS に送信されるときに、接続する IP アドレスを HTTP パケットの送信元 IP として変換する必要があります。 ロードバランサーが HTTP パケットでソース IP を送信できない場合、ロードバランサーは、IP アドレスを x 転送ヘッダーに追加 (または、既存のものを追加) する必要があります。 これは、特定の IP 関連機能 (禁止された IP、エクストラネットのスマートロックアウト,...) を正しく処理するために必要であり、正しく構成されていない場合、セキュリティが低下する可能性があります。
- ロードバランサーは SNI をサポートする必要があります。 そうでない場合は、AD FS が、非 SNI 対応クライアントを処理する HTTPS バインドを作成するように構成されていることを確認します。
- ロードバランサーは、AD FS HTTP 正常性プローブエンドポイントを使用して、AD FS または WAP サーバーが稼働しているかどうかを検出し、200 OK が返されない場合は除外します。

### <a name="what-multi-forest-configurations-are-supported-by-ad-fs"></a>AD FS では、どのようなマルチフォレスト構成がサポートされていますか。

AD FS は複数のフォレスト構成をサポートしており、基盤となる AD DS 信頼ネットワークに依存して、複数の信頼された領域でユーザーを認証します。 双方向のフォレストの信頼を確保することを強くお勧めします。これは、信頼されたサブシステムが問題なく正常に動作するようにするための簡単なセットアップです。 かつ

- パートナー id を含む DMZ フォレストなど一方向のフォレストの信頼がある場合は、corp フォレストに ADFS を展開し、LDAP 経由で接続された別のローカル要求プロバイダー信頼として DMZ フォレストを扱うことをお勧めします。 この場合、Windows 統合認証は、DMZ フォレストのユーザーに対しては機能しません。また、LDAP でサポートされている唯一のメカニズムであるため、パスワード認証を実行する必要があります。 このオプションを追求することができない場合は、DMZ フォレストで別の ADFS を設定し、corp フォレストの ADFS で要求プロバイダー信頼として追加する必要があります。 ユーザーはホーム領域検出を行う必要がありますが、Windows 統合認証とパスワード認証の両方が機能します。 Corp フォレストの ADFS が、DMZ フォレストからユーザーに関する追加のユーザー情報を取得できないようにするため、DMZ フォレストの ADFS で、発行規則に適切な変更を加えてください。
- ドメインレベルの信頼はサポートされており、機能しますが、フォレストレベルの信頼モデルに移行することを強くお勧めします。 また、名前の UPN ルーティングおよび NETBIOS 名前解決を正確に機能させる必要があります。



## <a name="design"></a>設計

### <a name="what-third-party-multi-factor-authentication-providers-are-available-for-ad-fs"></a>AD FS に使用できるサードパーティ製の multi-factor authentication プロバイダーは何ですか。
AD FS は、サードパーティの MFA プロバイダーを統合するための拡張メカニズムを提供します。 このための設定された認定プログラムはありません。 リリース前に、ベンダーが必要な検証を実行したことを前提としています。 

Microsoft に通知されたベンダーの一覧は、 [AD FS のために MFA プロバイダー](..\operations\Configure-Additional-Authentication-Methods-for-AD-FS.md)で公開されています。  提供されていないプロバイダーが常に利用可能であり、その内容について学習するためにリストが更新されます。

### <a name="are-third-party-proxies-supported-with-ad-fs"></a>サードパーティのプロキシは AD FS でサポートされていますか。
はい。サードパーティのプロキシは Web アプリケーションプロキシの前に配置できますが、サードパーティのプロキシでは、Web アプリケーションプロキシの代わりに使用するために、 [MS ADFSPIP プロトコル](https://msdn.microsoft.com/library/dn392811.aspx)をサポートする必要があります。

認識しているサードパーティプロバイダーの一覧を次に示します。  提供されていないプロバイダーが常に利用可能であり、その内容について学習するためにリストが更新されます。

- [F5 キーアクセスポリシーマネージャー](https://support.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-third-party-integration-13-1-0/12.html#guid-1ee8fbb3-1b33-4982-8bb3-05ae6868d9ee)


### <a name="where-is-the-capacity-planning-sizing-spreadsheet-for-ad-fs-2016"></a>AD FS 2016 の容量計画のサイジングスプレッドシートはどこにありますか?
スプレッドシートの AD FS 2016 バージョンは、[ここで](http://adfsdocs.blob.core.windows.net/adfs/ADFSCapacity2016.xlsx)ダウンロードできます。
これは、Windows Server 2012 R2 の AD FS にも使用できます。

### <a name="how-can-i-ensure-my-ad-fs-and-wap-servers-support-apples-atp-requirements"></a>AD FS と WAP サーバーが Apple の ATP 要件をサポートするようにするにはどうすればよいですか。

Apple は、AD FS に認証する iOS アプリからの呼び出しに影響する可能性がある App Transport Security (ATS) と呼ばれる一連の要件をリリースしました。  AD FS と WAP サーバーは、 [ATS を使用した接続の要件](https://developer.apple.com/library/prerelease/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW57)を確実に満たしていることを確認できます。  
特に、AD FS と WAP サーバーが TLS 1.2 をサポートしていること、および TLS 接続のネゴシエートされた暗号スイートが完全な転送機密性をサポートすることを確認する必要があります。

[AD FS の [Ssl プロトコルの管理](../operations/Manage-SSL-Protocols-in-AD-FS.md)] を使用して、ssl 2.0 および3.0 と TLS バージョン1.0、1.1、および1.2 を有効または無効にすることができます。

AD FS と WAP サーバーが ATP をサポートする TLS 暗号スイートのみをネゴシエートするように、 [atp 準拠の暗号スイートの一覧](https://developer.apple.com/library/prerelease/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW57)に含まれていないすべての暗号スイートを無効にすることができます。  これを行うには、 [WINDOWS TLS PowerShell コマンドレット](https://technet.microsoft.com/itpro/powershell/windows/tls/index)を使用します。

## <a name="developer"></a>Developer

### <a name="when-generating-an-id_token-with-adfs-for-a-user-authenticated-against-ad-how-is-the-sub-claim-generated-in-the-id_token"></a>AD に対して認証されたユーザーの ADFS を使用して id_token を生成する場合、id_token で "sub" 要求がどのように生成されますか?
"Sub" 要求の値は、クライアント ID + アンカー要求の値のハッシュです。

### <a name="what-is-the-lifetime-of-the-refresh-tokenaccess-token-when-the-user-logs-in-via-a-remote-claims-provider-trust-over-ws-fedsaml-p"></a>ユーザーが WS フィード/SAML でリモート要求プロバイダー信頼を使用してログインした場合、更新トークン/アクセストークンの有効期間はどのくらいですか?
更新トークンの有効期間は、ADFS がリモート要求プロバイダー信頼から受け取ったトークンの有効期間です。 アクセストークンの有効期間は、アクセストークンが発行されている証明書利用者のトークンの有効期間になります。

### <a name="i-need-to-return-profile-and-email-scopes-as-well-in-addition-to-the-openid-scope-can-i-obtain-additional-information-using-scopes-how-to-do-it-in-ad-fs"></a>OpenId スコープに加えて、プロファイルと電子メールのスコープも返す必要があります。 スコープを使用して追加情報を取得できますか。 AD FS で実行する方法
カスタマイズした id_token を使用して、id_token 自体に関連情報を追加できます。 詳細については、「 [id_token で出力される要求をカスタマイズする](../development/Custom-Id-Tokens-in-AD-FS.md)」を参照してください。

### <a name="how-to-issue-json-blobs-inside-jwt-tokens"></a>JWT トークン内で json blob を発行する方法
このに対する特殊な<http://www.w3.org/2001/XMLSchema#json>ValueType ("") とエスケープ文字 (\x22) が AD FS 2016 で追加されました。 発行規則と、アクセストークンからの最終的な出力については、次のサンプルを参照してください。

発行規則の例:

    => issue(Type = "array_in_json", ValueType = "http://www.w3.org/2001/XMLSchema#json", Value = "{\x22Items\x22:[{\x22Name\x22:\x22Apple\x22,\x22Price\x22:12.3},{\x22Name\x22:\x22Grape\x22,\x22Price\x22:3.21}],\x22Date\x22:\x2221/11/2010\x22}");

アクセストークンで発行された要求:

    "array_in_json":{"Items":[{"Name":"Apple","Price":12.3},{"Name":"Grape","Price":3.21}],"Date":"21/11/2010"}

### <a name="can-i-pass-resource-value-as-part-of-the-scope-value-like-how-requests-are-done-against-azure-ad"></a>Azure AD に対する要求の実行方法など、スコープの値の一部としてリソース値を渡すことはできますか。
サーバー2019で AD FS を使用すると、スコープパラメーターに埋め込まれたリソース値を渡すことができます。 スコープパラメーターは、各エントリがリソース/スコープとして構成されるスペース区切りのリストとして構成できるようになりました。 次に例を示します。  
**有効なサンプル要求 > を作成 <**

### <a name="does-ad-fs-support-pkce-extension"></a>PKCE 拡張機能はサポートさ AD FS ますか?
サーバー2019の AD FS では、OAuth 認証コード付与フロー用のコード交換 (PKCE) の証明キーがサポートされています

### <a name="what-permitted-scopes-are-supported-by-ad-fs"></a>AD FS では、許可されるスコープは何ですか。
- aza-[ブローカークライアントに OAuth 2.0 プロトコル拡張](https://docs.microsoft.com/openspecs/windows_protocols/ms-oapxbc/2f7d8875-0383-4058-956d-2fb216b44706)を使用していて、スコープパラメーターにスコープ "aza" が含まれている場合、サーバーは新しいプライマリ更新トークンを発行し、それを応答の refresh_token フィールドに設定し、refresh_token_ を設定します。expires_in フィールドが適用されている場合は、新しいプライマリ更新トークンの有効期間を設定します。
- openid-アプリケーションが OpenID Connect 承認プロトコルの使用を要求できるようにします。
- logon_cert-logon_cert スコープを使用すると、アプリケーションはログオン証明書を要求することができます。これは、認証されたユーザーを対話的にログオンするために使用できます。 AD FS サーバーは、応答から access_token パラメーターを除外し、代わりに base64 でエンコードされた CMS 証明書チェーンまたは CMC 完全 PKI 応答を提供します。 詳細について[は、こちら](https://docs.microsoft.com/openspecs/windows_protocols/ms-oapx/32ce8878-7d33-4c02-818b-6c9164cc731e)を参照してください。 
- user_impersonation-user_impersonation スコープは、AD FS からの代理アクセストークンを正常に要求するために必要です。 このスコープを使用する方法の詳細については[、AD FS 2016 で OAuth を使用して、(OBO) を使用して多層アプリケーションを構築](../../ad-fs/development/ad-fs-on-behalf-of-authentication-in-windows-server.md)する方法に関する説明を参照してください。
- vpn_cert-vpn_cert スコープは、アプリケーションが VPN 証明書を要求できるようにします。この証明書は、eap-tls 認証を使用して VPN 接続を確立するために使用できます。 これはサポートされなくなりました。
- 電子メール-アプリケーションは、サインインしたユーザーの電子メール要求を要求できます。 これはサポートされなくなりました。 
- プロファイル-アプリケーションがサインインユーザーのプロファイル関連の要求を要求できるようにします。 これはサポートされなくなりました。 


## <a name="operations"></a>操作

### <a name="how-do-i-replace-the-ssl-certificate-for-ad-fs"></a>AD FS の SSL 証明書操作方法置き換えますか?
AD FS SSL 証明書が、AD FS 管理スナップインで見つかった AD FS サービス通信証明書と同じではありません。  AD FS SSL 証明書を変更するには、PowerShell を使用する必要があります。 次の記事のガイダンスに従ってください。

[AD FS と WAP 2016で SSL 証明書を管理する](../operations/Manage-SSL-Certificates-AD-FS-WAP-2016.md)

### <a name="how-can-i-enable-or-disable-tlsssl-settings-for-ad-fs"></a>AD FS の TLS/SSL 設定を有効または無効にする方法はありますか
SSL プロトコルと暗号スイートを無効または有効にするには、次のようにします。

[AD FS での SSL プロトコルの管理](../operations/Manage-SSL-Protocols-in-AD-FS.md)

### <a name="does-the-proxy-ssl-certificate-have-to-be-the-same-as-the-ad-fs-ssl-certificate"></a>プロキシの SSL 証明書は AD FS SSL 証明書と同じである必要がありますか。  
プロキシ SSL 証明書と AD FS SSL 証明書に関しては、次のガイダンスを参考にしてください。


- プロキシを使用して Windows 統合認証を使用する AD FS 要求をプロキシする場合、プロキシ SSL 証明書はフェデレーションサーバーの SSL 証明書と同じである必要があります (同じキーを使用します)。
- AD FS プロパティ "ExtendedProtectionTokenCheck" が有効になっている場合 (AD FS の既定の設定)、プロキシ SSL 証明書はフェデレーションサーバーの SSL 証明書と同じである必要があります (同じキーを使用します)。
- それ以外の場合、プロキシ SSL 証明書は AD FS SSL 証明書とは異なるキーを持つことができますが、同じ[要件](../overview/AD-FS-2016-Requirements.md)を満たしている必要があります。

### <a name="why-do-i-only-see-a-password-login-on-ad-fs-and-not-my-other-authentication-methods-that-i-have-configured"></a>AD FS のパスワードログインのみが表示され、構成したその他の認証方法が表示されないのはなぜですか。 
アプリケーションで、構成済みで有効な認証方法にマップされる特定の認証 URI が明示的に要求されている場合、AD FS はログイン画面に1つの認証方法のみを表示します。 これは、WS-FEDERATION 要求の ' wauth ' パラメーターと、SAML プロトコル要求の ' RequestedAuthnCtxRef ' パラメーターに示されます。 その結果、要求された認証方法 (パスワードログインなど) のみが表示されます。

Azure AD で AD FS を使用する場合、アプリケーションは prompt = login パラメーターを Azure AD に送信するのが一般的です。 既定では Azure AD は、AD FS に対して新しいパスワードベースのログインを要求するように変換します。 これは、ネットワーク内の AD FS でパスワードのログインを確認する場合、または証明書を使用してログインするオプションが表示されない場合に最も一般的な理由です。 これは、Azure AD でフェデレーションドメインの設定を変更することによって簡単に解決できます。 

これを構成する方法の詳細については、「 [Active Directory フェデレーションサービス (AD FS) prompt = login parameter support](../operations/AD-FS-Prompt-Login.md)」を参照してください。

### <a name="how-can-i-change-the-ad-fs-service-account"></a>AD FS サービスアカウントを変更する方法はありますか
AD FS サービスアカウントを変更するには、[AD FS ツールボックス[サービスアカウント] Powershell モジュール](https://github.com/Microsoft/adfsToolbox/tree/master/serviceAccountModule)を使用した手順に従います。

### <a name="how-can-i-configure-browsers-to-use-windows-integrated-authentication-wia-with-ad-fs"></a>AD FS で Windows 統合認証 (WIA) を使用するようにブラウザーを構成する方法はありますか

ブラウザーを構成する方法の詳細については[、「AD FS で Windows 統合認証 (WIA) を使用するようにブラウザーを構成](../operations/Configure-AD-FS-Browser-WIA.md)する」を参照してください。

### <a name="can-i-turn-off-browserssoenabled"></a>Browserの有効化を無効にすることはできますか。
Adfs を使用したデバイスに基づくアクセス制御ポリシーがない場合、または Windows Hello for Business 証明書を登録している場合は、Browserの有効化を無効にすることができます。 Browserの有効化が有効になっていると、ADFS は、デバイス情報を格納しているクライアントから PRT (プライマリ更新トークン) を収集できます。 そのデバイスを使用しない場合、ADFS の認証は Windows 10 デバイスで機能しません。

### <a name="how-long-are-ad-fs-tokens-valid"></a>AD FS トークンはどのくらいの期間有効ですか?

多くの場合、この質問は、新しい資格情報を入力しなくても、ユーザーがシングルサインオン (SSO) を取得するのにどのくらいの時間がかかりますか。また、管理者がこれを管理するにはどうすればよいでしょうか。  この動作、およびそれを制御する構成設定については AD FS 「[シングルサインオンの設定](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/ad-fs-2016-single-sign-on-settings)」を参照してください。

さまざまな cookie とトークンの既定の有効期間 (および有効期間を制御するパラメーター) を以下に示します。

**登録済みデバイス**

- PRT と SSO cookie:PSSOLifeTimeMins によって管理される最大90日。 (指定されたデバイスは、少なくとも14日ごとに使用されます。これは Deviceon ウィンドウによって制御されます)

- 更新トークン: 一貫性のある動作を提供するために、上記の基準に基づいて計算されます。

- access_token:既定では、証明書利用者に基づいて1時間

- id_token: アクセストークンと同じ

**登録されていないデバイス**

- SSO cookie:既定では、SSOLifetimeMins によって管理される8時間です。  [サインインしたままにする (KMSI)] が有効になっている場合、既定値は24時間で、KMSILifetimeMins を使用して構成できます。


- 更新トークン:既定では8時間。 KMSI が有効になっている24時間

- access_token:既定では、証明書利用者に基づいて1時間

- id_token: アクセストークンと同じ

### <a name="does-ad-fs-support-http-strict-transport-security-hsts"></a>HTTP Strict Transport Security (HSTS) はサポート AD FS ですか。  

HTTP Strict Transport Security (HSTS) は、HTTP と HTTPS の両方のエンドポイントを持つサービスのプロトコルダウングレード攻撃や cookie ハイジャックを軽減するのに役立つ web セキュリティポリシーメカニズムです。 これにより、web サーバーは、web ブラウザー (または他の準拠ユーザーエージェント) が HTTPS を使用してのみ対話し、HTTP プロトコル経由では通信しないように宣言できます。

Web 認証トラフィックのすべての AD FS エンドポイントは、HTTPS 経由で排他的に開かれます。  その結果、http Strict Transport セキュリティポリシーメカニズムによって提供される脅威を効果的に軽減 AD FS ます (http にリスナーが存在しないため、http にダウングレードすることはできません)。 また、セキュリティで保護されたフラグを使用してすべての cookie をマークすることによって、HTTP プロトコルエンドポイントを使用する別のサーバーにクッキーが送信されないように AD FS ます。

そのため、AD FS サーバーに HSTS を実装する必要はありません。ダウングレードすることはできません。  コンプライアンスを確保するために、AD FS サーバーは HTTP を使用することはできず、すべての cookie は安全としてマークされるため、これらの要件を満たしています。

さらに、AD FS 2016 (最新の更新プログラムが適用されています) を使用し、AD FS 2019 で HSTS ヘッダーの生成をサポートしています。 これを構成するには[、「AD FS で HTTP セキュリティ応答ヘッダーをカスタマイズ](../operations/customize-http-security-headers-ad-fs.md)する」を参照してください。

### <a name="x-ms-forwarded-client-ip-does-not-contain-the-ip-of-the-client-but-contains-ip-of-the-firewall-in-front-of-the-proxy-where-can-i-get-the-right-ip-of-the-client"></a>-Ms-chap-クライアント ip にはクライアントの IP は含まれませんが、プロキシの前にファイアウォールの IP が格納されます。 クライアントの適切な IP はどこで入手できますか。
WAP の前に SSL を終了することはお勧めしません。 WAP の前に SSL ターミネーションが行われた場合は、WAP の前にネットワークデバイスの IP アドレスが含まれます (例:)。 AD FS によってサポートされる IP 関連のさまざまな要求の簡単な説明を次に示します。
 - クライアント ip アドレス:STS に接続されているデバイスのネットワーク IP。  エクストラネット要求の場合、これには常に WAP の IP が含まれます。
 - -ms-chap-クライアント-ip:複数値の要求。これには、Exchange Online によって ADFS に転送されるすべての値と、WAP に接続されているデバイスの IP アドレスが含まれます。
 - Userip:エクストラネット要求の場合、この要求には、---転送されたクライアント ip の値が含まれます。  イントラネット要求の場合、この要求には、x.y と同じ値が含まれます。

 さらに、AD FS 2016 (最新の更新プログラムが適用されています) では、より高いバージョンでは、x の転送ヘッダーのキャプチャもサポートしています。 レイヤー 3 (IP が保持されている) で転送されないすべてのロードバランサーまたはネットワークデバイスは、受信クライアント IP を業界標準の x 転送ヘッダーに追加する必要があります。 

### <a name="i-am-trying-to-get-additional-claims-on-the-user-info-endpoint-but-its-only-returning-subject-how-can-i-get-additional-claims"></a>ユーザー情報エンドポイントに対して追加の要求を取得しようとしていますが、そのサブジェクトのみが返されます。 追加の要求を取得するにはどうすればよいですか。
AD FS userinfo エンドポイントは、OpenID 標準で指定されているように常にサブジェクト要求を返します。 AD FS は、UserInfo エンドポイントを介して要求された追加の要求を提供しません。 ID トークンに追加の要求が必要な場合は、 [AD FS のカスタム ID トークン](../development/custom-id-tokens-in-ad-fs.md)を参照してください。

### <a name="why-do-i-see-a-lot-of-1021-errors-on-my-ad-fs-servers"></a>AD FS サーバーで1021のエラーが多数表示されるのはなぜですか。
このイベントは、通常、リソース 00000003-0000-0000-c000-000000000000 の AD FS で無効なリソースへのアクセスが発生した場合にログに記録されます。 このエラーは、Azure AD Graph サービスのアクセストークンを取得しようとするクライアントの動作が正しくないことが原因で発生します。 AD FS にリソースが存在しないため、AD FS サーバーでイベント ID 1021 が生成されます。 AD FS のリソース 00000003-0000-0000-c000-000000000000 の警告やエラーを無視しても安全です。

### <a name="why-am-i-seeing-a-warning-for-failure-to-add-the-ad-fs-service-account-to-the-enterprise-key-admins-group"></a>AD FS サービスアカウントを Enterprise Key Admins グループに追加できないという警告が表示されるのはなぜですか。
このグループは、ドメイン内に FSMO PDC 役割を持つ Windows 2016 ドメインコントローラーが存在する場合にのみ作成されます。 このエラーを解決するには、グループを手動で作成し、以下の手順に従って、サービスアカウントをグループのメンバーとして追加した後に必要なアクセス許可を付与します。
1.  **[Active Directory ユーザーとコンピューター]** を開きます。
2.  ナビゲーションウィンドウでドメイン名を**右クリック**し、 **[プロパティ] をクリック**します。
3.  **クリック**セキュリティ ([セキュリティ] タブが表示されていない場合は、[表示] メニューの [高度な機能] をオンにします)。
4.  **クリック**進め. **クリック**アドイン. **クリック**プリンシパルを選択します。
5.  [ユーザー、コンピューター、サービスアカウントまたはグループの選択] ダイアログボックスが表示されます。  [選択するオブジェクト名を入力してください] テキストボックスに、「キー管理者グループ」と入力します。  [OK] をクリックします。
6.  適用先 ボックスの一覧で、**子孫ユーザーオブジェクト** を選択します。
7.  スクロール バーを使用して、ページの下部までスクロールし、 **をクリックして** すべてクリアします。
8.  **[プロパティ]** セクションで、 **[キーの取得]** を選択して、"キーの入力" リンクを**書き込み**ます。

### <a name="why-does-modern-authentication-from-android-devices-fail-if-the-server-does-not-send-all-the-intermediate-certificates-in-the-chain-with-the-ssl-cert"></a>サーバーが SSL 証明書を使用してチェーン内のすべての中間証明書を送信しない場合、Android デバイスからの先進認証が失敗するのはなぜですか。

Android ADAL ライブラリを使用しているアプリでは、フェデレーションユーザーが Azure AD の認証を経験する場合があります。 ログインページを表示しようとすると、アプリケーションは**Authenticationexception**を受け取ります。 Chrome では、AD FS ログインページが unsafe として呼び出される場合があります。

Android-すべてのバージョンとすべてのデバイスで-証明書の**authorityInformationAccess**フィールドから追加の証明書をダウンロードすることはできません。 これは Chrome ブラウザーにも当てはまります。 中間証明書が欠落しているサーバー認証証明書では、証明書チェーン全体が AD FS から渡されなかった場合、このエラーが発生します。

この問題を解決するには、必要な中間証明書を SSL 証明書と共に送信するように AD FS と WAP サーバーを構成します。

1台のコンピューターから、AD FS および WAP サーバーのコンピューターの個人用ストアにインポートする SSL 証明書をエクスポートする場合は、必ず秘密キーをエクスポートし、 **[Personal Information Exchange-PKCS #12]** を選択します。

**[可能な場合は証明書のパスにすべての証明書を含める]** チェックボックスをオンにし、すべての**拡張プロパティをエクスポート**することが重要です。  

Windows サーバーで certlm .msc を実行し、* をインポートします。コンピューターの個人証明書ストアに PFX を格納します。 これにより、サーバーは証明書チェーン全体を ADAL ライブラリに渡します。

>[!NOTE]
> ネットワークロードバランサーの証明書ストアは、証明書チェーン全体を含めるようにも更新する必要があります (存在する場合)。

### <a name="does-ad-fs-support-head-requests"></a>HEAD 要求をサポート AD FS。
AD FS は、HEAD 要求をサポートしていません。  アプリケーションでは、AD FS エンドポイントに対してヘッド要求を使用しないでください。  これにより、予期しない、または遅延している HTTP エラー応答が発生する可能性があります。  また、AD FS イベントログに予期しないエラーイベントが表示される場合があります。

### <a name="why-am-i-not-seeing-a-refresh-token-when-i-am-logging-in-with-a-remote-idp"></a>リモート IdP でログインしているときに更新トークンが表示されないのはなぜですか。
IdP によって発行されたトークンの有効期間が1時間未満の場合、更新トークンは発行されません。 更新トークンが確実に発行されるようにするには、IdP によって発行されたトークンの有効性を1時間以上に増やします。

### <a name="do-we-have-any-way-to-change-rp-token-encryption-algorithm"></a>RP トークン暗号化アルゴリズムを変更する方法はありますか。
既定では、RP トークンの暗号化は AES256 に設定されており、それ以外の値には変更できません。

### <a name="on-a-mixed-mode-farm-i-get-error-when-trying-to-set-the-new-ssl-certificate-using-set-adfssslcertificate--thumbprint-how-can-i-update-the-ssl-certificate-in-a-mixed-mode-ad-fs-farm"></a>混合モードのファームでは、Set-adfssslcertificate-Thumbprint を使用して新しい SSL 証明書を設定しようとするとエラーが発生します。 ファーム AD FS 混在モードで SSL 証明書を更新する方法はありますか
混在モード AD FS ファームは transitionary の状態になります。 アップグレードプロセスの前に SSL 証明書をロールオーバーするか、プロセスを完了し、SSL 証明書を更新する前にファームの動作レベルを上げることを計画する際にお勧めします。 これが行われなかった場合は、以下の手順に従って SSL 証明書を更新することができます。 

WAP サーバーでは、WebApplicationProxySslCertificate を引き続き使用できます。 ADFS サーバーでは、netsh を使用する必要があります。 次の手順に従います。

1. メンテナンスのために ADFS 2016 サーバーのサブセットを選択する (例: ロードバランサーから削除する)
2. #1 で選択したサーバーで、MMC を使用して新しい証明書をインポートします。
3. 既存の証明書を削除する

    a. netsh http delete sslcert hostnameport = fs. contoso .com: 443 b. netsh http delete sslcert hostnameport = localhost: 443 c。 netsh http delete sslcert hostnameport = fs. contoso .com: 49443

4.  新しい証明書を追加する

    a. netsh http add sslcert hostnameport = fs. contoso .com: 443 certhash = CERTTHUMBPRINT appid = {5d89a20cx beab4-388-71-324788 ebcertstorename 4a} = MY sslctlstorename = AdfsTrustedDevices

    b. netsh http add sslcert hostnameport = localhost: 443 certhash = CERTTHUMBPRINT appid = {5d89a20cx beab47 38388 8-324788 eb71 4a} certstorename = MY sslctlstorename = AdfsTrustedDevices

    c. netsh http add sslcert hostnameport = fs. contoso .com: 49443 certhash = CERTTHUMBPRINT appid = {5d89a20c beab4-388-71-324788 eb・ 4a} certstorename = MY sslctlstorename = AdfsTrustedDevices

5. 選択したサーバーで ADFS サービスを再起動します
6. メンテナンスのために WAP サーバーのサブセットを削除する
7. 選択した WAP サーバーで、MMC を使用して新しい証明書をインポートします。
8. コマンドレットを使用して、WAP に新しい証明書を設定する

    a. WebApplicationProxySslCertificate-Thumbprint "CERTTHUMBPRINT"

9. 選択した WAP サーバーでサービスを再起動します
10. 選択した WAP と AD FS サーバーを運用環境に戻します。

同様の方法で、AD FS と WAP サーバーの残りの部分で更新を実行します。

### <a name="is-adfs-supported-when-web-application-proxy-wap-servers-are-behind-azure-web-application-firewallwaf"></a>Web アプリケーションプロキシ (WAP) サーバーが Azure Web アプリケーションファイアウォール (WAF) の内側にある場合、ADFS はサポートされますか?
ADFS と Web アプリケーションサーバーは、エンドポイントで SSL 終了を実行しないすべてのファイアウォールをサポートします。 さらに、ADFS/WAP サーバーには、クロスサイトスクリプティング、ADFS プロキシ、 [MS ADFSPIP プロトコル](https://msdn.microsoft.com/library/dn392811.aspx)で定義されているすべての要件を満たす一般的な web 攻撃を防ぐためのメカニズムが組み込まれています。

### <a name="i-am-seeing-an-event-441-a-token-with-a-bad-token-binding-key-was-found-what-should-i-do-to-resolve-this"></a>"イベント 441:トークンのバインドキーが正しくないトークンが見つかりました。 " これを解決するにはどうすればよいですか。
AD FS 2016 では、トークンのバインドが自動的に有効になり、プロキシとフェデレーションのシナリオで複数の既知の問題が発生し、このエラーが発生します。 これを解決するには、次の Powershell コマンドを実行し、トークンのバインディングサポートを削除します。

`Set-AdfsProperties -IgnoreTokenBinding $true`

### <a name="i-have-upgraded-my-farm-from-ad-fs-in-windows-server-2016-to-ad-fs-in-windows-server-2019-the-farm-behavior-level-for-the-ad-fs-farm-has-been-successfully-raised-to-2019-but-the-web-application-proxy-configuration-is-still-displayed-as-windows-server-2016"></a>Windows server 2016 の AD FS から Windows Server 2019 の AD FS にファームをアップグレードしました。 AD FS ファームのファームの動作レベルは正常に2019になりましたが、Web アプリケーションプロキシの構成は Windows Server 2016 として表示されていますか?
Windows Server 2019 へのアップグレード後、Web アプリケーションプロキシの構成バージョンは、Windows Server 2016 として引き続き表示されます。 Web アプリケーションプロキシには、Windows Server 2019 向けの新バージョン固有の機能がありません。 AD FS でファームの動作レベルが正常に発生した場合、Web アプリケーションプロキシは、設計上、Windows Server 2016 として引き続き表示されます。 
