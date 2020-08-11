---
ms.assetid: acc9101b-841c-4540-8b3c-62a53869ef7a
title: AD FS の FAQ
description: AD FS に関してよく寄せられる質問
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 04/29/2020
ms.topic: article
ms.openlocfilehash: 50767d5b1941e397583f6c2bfa1d6b2ae3f253cf
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87949686"
---
# <a name="ad-fs-frequently-asked-questions-faq"></a>AD FS についてよく寄せられる質問 (FAQ)

以下のドキュメントでは、Active Directory フェデレーション サービス (AD FS) に関してよく寄せられる質問について説明します。  ドキュメントは、質問の種類に基づくグループに分かれています。

## <a name="deployment"></a>展開

### <a name="how-can-i-upgrademigrate-from-previous-versions-of-ad-fs"></a>以前のバージョンの AD FS からアップグレードまたは移行するにはどうすればよいですか?

次のいずれかを使用して AD FS をアップグレードできます。

- Windows Server 2012 R2 AD FS から Windows Server 2016 AD FS 以降。 方法は、Windows Server 2016 AD FS から Windows Server 2019 AD FS にアップグレードする場合と同じであることに注意してください。
    - [WID データベースを使用した、Windows Server 2016 での AD FS へのアップグレード](../deployment/upgrading-to-ad-fs-in-windows-server.md)
    - [SQL データベースを使用した、Windows Server 2016 での AD FS へのアップグレード](../deployment/upgrading-to-ad-fs-in-windows-server-sql.md)
- Windows Server 2012 AD FS から Windows Server 2012 R2 AD FS
    - [Windows Server 2012 R2 の AD FS に移行する](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn486815(v=ws.11))
- AD FS 2.0 から Windows Server 2012 AD FS
    - [Windows Server 2012 の AD FS に移行する](../deployment/migrate-ad-fs-role-services-to-windows-server-2012.md)
- AD FS 1.x から AD FS 2.0
    - [AD FS 1.x から AD FS 2.0 にアップグレードする](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff678035(v=ws.10))

AD FS 2.0 または 2.1 (Windows Server 2008 R2 または Windows Server 2012) からアップグレードする必要がある場合は、(C:\Windows\ADFS にある) インボックス スクリプトを使用する必要があります。

### <a name="why-does-ad-fs-installation-require-a-reboot-of-the-server"></a>AD FS をインストールするときにサーバーの再起動が必要なのはなぜですか?

HTTP/2 のサポートは Windows Server 2016 で追加されましたが、クライアント証明書認証に HTTP/2 を使用することはできません。  AD FS の多くのシナリオでクライアント証明書認証が使用されており、多数のクライアントでは HTTP/1.1 を使用した要求の再試行がサポートされていないため、AD FS ファームの構成では、ローカル サーバーの HTTP 設定が HTTP/1.1 に再構成されます。  これには、サーバーの再起動が必要です。

### <a name="is-using-windows-2016-wap-servers-to-publish-the-ad-fs-farm-to-the-internet-without-upgrading-the-back-end-ad-fs-farm-supported"></a>Windows 2016 WAP サーバーを使用して、バックエンド AD FS ファームをアップグレードせずに、AD FS ファームをインターネットに発行することはサポートされていますか?
はい。この構成はサポートされていますが、この構成では AD FS 2016 の新しい機能はサポートされません。  この構成は、AD FS 2012 R2 から AD FS 2016 への移行フェーズの間の一時的なものとして意図されており、長期間展開することはできません。

### <a name="is-it-possible-to-deploy-ad-fs-for-office-365-without-publishing-a-proxy-to-office-365"></a>Office 365 にプロキシを発行せずに、Office 365 用に AD FS を展開することはできますか?
はい、これはサポートされています。 ただし、次のような副作用があります

1. Azure AD ではフェデレーション メタデータにアクセスできないため、更新トークン署名証明書を手動で管理する必要があります。 トークン署名証明書の手動更新について詳しくは、「[Office 365 および Azure Active Directory 用のフェデレーション証明書の更新](/azure/active-directory/connect/active-directory-aadconnect-o365-certs)」をご覧ください
2. 従来の認証フロー (たとえば、ExO プロキシ認証フロー) を利用することはできません

### <a name="what-are-load-balancing-requirements-for-ad-fs-and-wap-servers"></a>AD FS と WAP サーバーにはどのような負荷分散要件がありますか?

AD FS はステートレス システムです。 したがって、ログインの負荷分散は非常に簡単です。 システムの負荷分散に関する主な推奨事項を次に示します。


- IP アフィニティを使用してロード バランサーを構成しないでください。 これを行うと、Exchange Online の特定のシナリオで、サーバーのサブセットに過度の負荷がかかる可能性があります。
- ロード バランサーで、AD FS サーバーへの HTTPS 接続を終了し、新しい接続を再開しないでください。
- ロード バランサーでは、AD FS に送信される HTTP パケットの送信元 IP として、接続している IP アドレスを変換する必要があります。 ロード バランサーで、HTTP パケットの送信元 IP を送信できない場合は、x-forwarded-for ヘッダーに IP アドレスを追加 (または、既にある場合は付加) する必要があります。 これは、特定の IP 関連機能 (禁止された IP、エクストラネット スマート ロックアウトなど) を正しく処理するために必要であり、正しく構成しないとセキュリティが低下する可能性があります。
- ロード バランサーでは、SNI をサポートする必要があります。 そうでない場合は、非 SNI 対応クライアントを処理するため、HTTPS バインドを作成するように AD FS が構成されていることを確認します。
- ロード バランサーでは、AD FS HTTP 正常性プローブ エンドポイントを使用して、AD FS または WAP サーバーが稼働しているかどうかを検出し、200 OK が返されない場合はそれらを除外する必要があります。

### <a name="what-multi-forest-configurations-are-supported-by-ad-fs"></a>AD FS では、どのようなマルチフォレスト構成がサポートされていますか?

AD FS では、複数のマルチフォレスト構成がサポートされており、基盤となる AD DS の信頼のネットワークに依存して、複数の信頼された領域でユーザーの認証が行われます。 比較的簡単なセットアップで、信頼サブシステムを問題なく正常に動作させることができるため、双方向のフォレストの信頼を強くお勧めします。 さらに、

- パートナー ID を含む DMZ フォレストなどの一方向のフォレストの信頼の場合は、CORP フォレストに ADFS を展開し、LDAP 経由で接続された別のローカル要求プロバイダー信頼として、DMZ フォレストを扱うことをお勧めします。 この場合、Windows 統合認証は DMZ フォレストのユーザーに対して機能しないので、LDAP 用にサポートされている唯一のメカニズムであるパスワード認証を実行する必要があります。 このオプションを使用できない場合は、DMZ フォレストに別の AD FS を設定し、CORP フォレストの AD FS に要求プロバイダー信頼として追加する必要があります。 ユーザーはホーム領域検出を行う必要がありますが、Windows 統合認証とパスワード認証の両方が機能します。 CORP フォレストの AD FS では DMZ フォレストからユーザーに関する追加の情報を取得できないため、DMZ フォレストの ADFS で、発行規則を適切に変更してください。
- ドメイン レベルの信頼はサポートされており、機能しますが、フォレスト レベルの信頼モデルに移行することを強くお勧めします。 また、UPN ルーティングおよび名前の NETBIOS 名前解決が正確に機能することを確認する必要があります。

>[!NOTE]
>双方向の信頼構成で選択的認証を使用する場合は、ターゲット サービス アカウントでの "認証許可" アクセス許可が呼び出し元ユーザーに付与されていることを確認します。

### <a name="does-ad-fs-extranet-smart-lockout-support-ipv6"></a>AD FS エクストラネット スマート ロックアウトでは IPv6 をサポートしていますか?
はい。IPv6 アドレスは、使い慣れた場所または不明な場所で考慮されます。


## <a name="design"></a>設計

### <a name="what-third-party-multi-factor-authentication-providers-are-available-for-ad-fs"></a>AD FS に使用できるサードパーティの多要素認証プロバイダーは何ですか?
AD FS では、サードパーティの MFA プロバイダーを統合するための拡張可能なメカニズムが提供されています。 このための設定された認定プログラムはありません。 ベンダーはリリース前に必要な検証を実行したものと想定されています。

Microsoft に通知したベンダーの一覧は、[AD FS 対応 MFA プロバイダー](../operations/Configure-Additional-Authentication-Methods-for-AD-FS.md)で公開されています。  Microsoft が把握していない利用可能なプロバイダーは常に存在する可能性があり、わかったら一覧を更新します。

### <a name="are-third-party-proxies-supported-with-ad-fs"></a>AD FS ではサードパーティのプロキシはサポートされていますか?
はい。サードパーティのプロキシを AD FS の前面に配置できますが、サードパーティのプロキシでは、Web アプリケーション プロキシの代わりに使用する [MS-ADFSPIP プロトコル](/openspecs/windows_protocols/ms-adfspip/76deccb1-1429-4c80-8349-d38e61da5cbb)がサポートされている必要があります。

Microsoft が把握しているサードパーティ プロバイダーの一覧を次に示します。  Microsoft が把握していない利用可能なプロバイダーは常に存在する可能性があり、わかったら一覧を更新します。

- [F5 Access Policy Manager](https://support.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-third-party-integration-13-1-0/12.html#guid-1ee8fbb3-1b33-4982-8bb3-05ae6868d9ee)


### <a name="where-is-the-capacity-planning-sizing-spreadsheet-for-ad-fs-2016"></a>AD FS 2016 用のキャパシティ プランニング サイズ決定スプレッドシートはどこにありますか?
AD FS 2016 バージョンのスプレッドシートは、[こちらから](https://adfsdocs.blob.core.windows.net/adfs/ADFSCapacity2016.xlsx)ダウンロードできます。
これは、Windows Server 2012 R2 の AD FS にも使用できます。

### <a name="how-can-i-ensure-my-ad-fs-and-wap-servers-support-apples-atp-requirements"></a>AD FS と WAP サーバーで Apple の ATP 要件をサポートするにはどうすればよいですか?

Apple からは App Transport Security (ATS) と呼ばれる一連の要件がリリースされており、AD FS に対する認証を行う iOS アプリからの呼び出しに影響する可能性があります。  AD FS と WAP サーバーでは、[ATS を使用する接続に関する要件](https://developer.apple.com/library/prerelease/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW57)をサポートすることで、それに準拠することができます。
具体的には、AD FS と WAP サーバーで TLS 1.2 がサポートされていること、および TLS 接続のネゴシエートされた暗号スイートで完全な転送機密性がサポートされることを、確認する必要があります。

[AD FS での SSL プロトコルの管理](../operations/Manage-SSL-Protocols-in-AD-FS.md)に関する記事に従って、SSL 2.0 と 3.0 および TLS バージョン 1.0、1.1、1.2 を有効または無効にできます。

ATP をサポートする TLS 暗号スイートのみが AD FS と WAP サーバーでネゴシエートされるようにするには、[ATP に準拠する暗号スイートの一覧](https://developer.apple.com/library/prerelease/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW57)に含まれていないすべての暗号スイートを無効にします。  これを行うには、[Windows TLS PowerShell コマンドレット](/powershell/module/tls/?view=win10-ps)を使用します。

## <a name="developer"></a>Developer

### <a name="when-generating-an-id_token-with-adfs-for-a-user-authenticated-against-ad-how-is-the-sub-claim-generated-in-the-id_token"></a>AD に対して認証されたユーザー用の id_token を ADFS で生成するとき、"sub" 要求は id_token でどのように生成されますか?
"sub" 要求の値は、クライアント ID とアンカー要求の値のハッシュです。

### <a name="what-is-the-lifetime-of-the-refresh-tokenaccess-token-when-the-user-logs-in-via-a-remote-claims-provider-trust-over-ws-fedsaml-p"></a>ユーザーが WS-Fed/SAML-P を使用してリモート要求プロバイダー信頼経由でログインした場合、更新トークンとアクセス トークンの有効期間はどのくらいですか?
更新トークンの有効期間は、AD FS がリモート要求プロバイダー信頼から取得したトークンの有効期間です。 アクセス トークンの有効期間は、アクセス トークンの発行対象である証明書利用者のトークンの有効期間になります。

### <a name="i-need-to-return-profile-and-email-scopes-as-well-in-addition-to-the-openid-scope-can-i-obtain-additional-information-using-scopes-how-to-do-it-in-ad-fs"></a>OpenId スコープに加えて、プロファイルとメールのスコープも返す必要があります。 スコープを使用して追加情報を取得できますか? AD FS ではどのようにすればよいですか?
カスタマイズされた id_token を使用して、id_token 自体に関連情報を追加できます。 詳しくは、[id_token で出力されるように要求をカスタマイズする方法](../development/Custom-Id-Tokens-in-AD-FS.md)に関する記事をご覧ください。

### <a name="how-to-issue-json-blobs-inside-jwt-tokens"></a>JWT トークン内で Json BLOB を発行するにはどうすればよいですか?
これのための特殊な ValueType ("<http://www.w3.org/2001/XMLSchema#json>") とエスケープ文字 (\x22) が、AD FS 2016 で追加されました。 発行規則と、アクセス トークンからの最終的な出力については、次のサンプルを参照してください。

発行規則の例:

```
=> issue(Type = "array_in_json", ValueType = "http://www.w3.org/2001/XMLSchema#json", Value = "{\x22Items\x22:[{\x22Name\x22:\x22Apple\x22,\x22Price\x22:12.3},{\x22Name\x22:\x22Grape\x22,\x22Price\x22:3.21}],\x22Date\x22:\x2221/11/2010\x22}");
```

アクセス トークンで発行された要求:

```
"array_in_json":{"Items":[{"Name":"Apple","Price":12.3},{"Name":"Grape","Price":3.21}],"Date":"21/11/2010"}
```

### <a name="can-i-pass-resource-value-as-part-of-the-scope-value-like-how-requests-are-done-against-azure-ad"></a>Azure AD に対する要求方法のように、スコープ値の一部としてリソース値を渡すことはできますか?
Server 2019 の AD FS では、リソース値をスコープ パラメーターに埋め込んで渡すことができます。 スコープ パラメーターは、各エントリがリソース/スコープとして構成された、スペース区切りのリストとして作成できるようになりました。 例: **<有効なサンプル要求を作成する>**

### <a name="does-ad-fs-support-pkce-extension"></a>AD FS では PKCE 拡張機能はサポートされていますか?
Server 2019 の AD FS では、OAuth 認証コード付与フロー用の Proof Key for Code Exchange (PKCE) がサポートされています

### <a name="what-permitted-scopes-are-supported-by-ad-fs"></a>AD FS でサポートされている許可されたスコープは何ですか?
- aza - [ブローカー クライアント用 OAuth 2.0 プロトコル拡張](/openspecs/windows_protocols/ms-oapxbc/2f7d8875-0383-4058-956d-2fb216b44706)を使用していて、スコープ パラメーターにスコープ "aza" が含まれている場合、サーバーでは、新しいプライマリ更新トークンが発行されて、応答の refresh_token フィールドに設定され、新しいプライマリ更新トークンに有効期間が適用される場合は refresh_token_expires_in フィールドに設定されます。
- openid - アプリケーションで OpenID Connect 承認プロトコルの使用を要求できるようにします。
- logon_cert - logon_cert スコープを使用すると、アプリケーションでログオン証明書を要求できます。この証明書を使用して、認証されたユーザーを対話的にログオンさせることができます。 AD FS サーバーでは、応答から access_token パラメーターが除去され、代わりに base64 でエンコードされた CMS 証明書チェーンまたは CMC 完全 PKI 応答が提供されます。 詳しくは、[こちら](/openspecs/windows_protocols/ms-oapx/32ce8878-7d33-4c02-818b-6c9164cc731e)をご覧ください。
- user_impersonation - AD FS に On-Behalf-Of アクセス トークンを正常に要求するには、user_impersonation スコープが必要です。 このスコープを使用する方法について詳しくは、「[AD FS 2016 以降で OAuth を使用して、の代理 (OBO) を使用して多層アプリケーションを構築する](../../ad-fs/development/ad-fs-on-behalf-of-authentication-in-windows-server.md)」をご覧ください。
- vpn_cert - vpn_cert スコープを使用すると、アプリケーションで VPN 証明書を要求できます。VPN 証明書を使用すると、EAP-TLS 認証を使用して VPN 接続を確立できます。 これはサポートされなくなっています。
- email - アプリケーションで、サインインしたユーザーの電子メール要求を要求できます。 これはサポートされなくなっています。
- profile - アプリケーションで、サインインしたユーザーのプロファイル関連の要求を要求できます。 これはサポートされなくなっています。


## <a name="operations"></a>運用

### <a name="how-do-i-replace-the-ssl-certificate-for-ad-fs"></a>AD FS 用の SSL 証明書を置き換えるにはどうすればよいですか?
AD FS SSL 証明書は、AD FS 管理スナップインで見つかる AD FS サービス通信証明書と同じものではありません。  AD FS SSL 証明書を変更するには、PowerShell を使用する必要があります。 次の記事のガイダンスに従ってください。

[AD FS と WAP 2016で SSL 証明書を管理する](../operations/manage-ssl-certificates-ad-fs-wap.md)

### <a name="how-can-i-enable-or-disable-tlsssl-settings-for-ad-fs"></a>AD FS の TLS/SSL の設定を有効または無効にするにはどうすればよいですか?
SSL プロトコルと暗号スイートを無効または有効にするには、次のようにします。

[AD FS で SSL プロトコルを管理する](../operations/Manage-SSL-Protocols-in-AD-FS.md)

### <a name="does-the-proxy-ssl-certificate-have-to-be-the-same-as-the-ad-fs-ssl-certificate"></a>プロキシ SSL 証明書は AD FS SSL 証明書と同じである必要がありますか?
プロキシ SSL 証明書と AD FS SSL 証明書に関しては、次のガイダンスを参考にしてください。


- プロキシを使用して Windows 統合認証を使用する AD FS 要求をプロキシする場合、プロキシ SSL 証明書はフェデレーション サーバーの SSL 証明書と同じである (同じキーを使用している) 必要があります
- AD FS プロパティ "ExtendedProtectionTokenCheck" が有効な場合 (AD FS の既定の設定)、プロキシ SSL 証明書はフェデレーション サーバーの SSL 証明書と同じである (同じキーを使用している) 必要があります
- それ以外の場合、プロキシ SSL 証明書は AD FS SSL 証明書とは異なるキーを持つことができますが、同じ[要件](./ad-fs-requirements.md)を満たす必要があります。

### <a name="why-do-i-only-see-a-password-login-on-ad-fs-and-not-my-other-authentication-methods-that-i-have-configured"></a>AD FS のパスワード ログインのみが表示され、構成した他の認証方法が表示されないのはなぜですか?
アプリケーションで明示的に要求されている特定の認証 URI が構成済みで有効な認証方法にマップされる場合、AD FS のログイン画面には 1 つの認証方法のみが表示されます。 これは、WS-Federation 要求の "wauth" パラメーターと、SAML プロトコル要求の "RequestedAuthnCtxRef" パラメーターで伝達されます。 その結果、要求された認証方法 (パスワード ログインなど) のみが表示されます。

AD FS が Azure AD と共に使用されていると、アプリケーションでは prompt=login パラメーターを Azure AD に送信するのが一般的です。 既定では、これは、Azure AD によって、AD FS に対する新しいパスワードに基づくログインの要求に変換されます。 これは、ネットワーク内の AD FS でパスワードのログインが表示される、または証明書でログインするためのオプションが表示されない、最も一般的な理由です。 これは、Azure AD でフェデレーション ドメインの設定を変更することによって、簡単に解決できます。

これを構成する方法については、「[Active Directory フェデレーション サービス (AD FS) での prompt=login パラメーターのサポート](../operations/AD-FS-Prompt-Login.md)」をご覧ください。

### <a name="how-can-i-change-the-ad-fs-service-account"></a>AD FS のサービス アカウントを変更するにはどうすればよいですか?
AD FS のサービス アカウントを変更するには、AD FS ツールボックスの[サービス アカウント Powershell モジュール](https://github.com/Microsoft/adfsToolbox/tree/master/serviceAccountModule)を使用した手順に従います。

### <a name="how-can-i-configure-browsers-to-use-windows-integrated-authentication-wia-with-ad-fs"></a>AD FS で Windows 統合認証 (WIA) が使用されるようにブラウザーを構成するにはどうすればよいですか?

ブラウザーを構成する方法については、「[AD FS で Windows 統合認証 (WIA) を使用するようにブラウザーを構成する](../operations/Configure-AD-FS-Browser-WIA.md)」をご覧ください。

### <a name="can-i-turn-off-browserssoenabled"></a>BrowserSsoEnabled を無効にすることはできますか?
AD FS 上のデバイス、または AD FS を使用する Windows Hello for Business 証明書の登録に基づくアクセス制御ポリシーがない場合、BrowserSsoEnabled を無効にすることができます。 BrowserSsoEnabled を使用すると、AD FS で、デバイス情報が格納されているクライアントから PRT (プライマリ更新トークン) を収集できます。 そのデバイスがない場合、AD FS の認証は Windows 10 デバイスで機能しません。

### <a name="how-long-are-ad-fs-tokens-valid"></a>AD FS トークンの期間有効はどのくらいですか?

多くの場合、この質問は、"ユーザーが新しい資格情報を入力しないでシングル サインオン (SSO) を利用できる期間、および管理者がそれを管理する方法" を意味します。  この動作、およびそれを制御する構成設定については、「[AD FS のシングル サインオンの設定](../operations/ad-fs-single-sign-on-settings.md)」をご覧ください。

さまざまな Cookie とトークンの既定の有効期間 (および有効期間を制御するパラメーター) を以下に示します。

**登録済みデバイス**

- PRT と SSO Cookie: 最大 90 日で、PSSOLifeTimeMins によって管理されます。 (デバイスが少なくとも 14 日ごとに使用されること。これは DeviceUsageWindow によって制御されます)

- 更新トークン: 一貫性のある動作を提供するために、上記に基づいて計算されます

- access_token: 既定では 1 時間、証明書利用者に基づきます

- id_token: アクセス トークンと同じ

**未登録デバイス**

- SSO Cookie: 既定では 8 時間で、SSOLifetimeMins によって管理されます。  サインアウトしない (KMSI) が有効になっている場合の既定値は 24 時間で、KMSILifetimeMins を使用して構成できます。


- 更新トークン: 既定では 8 時間。 KMSI が有効になっている場合は 24 時間

- access_token: 既定では 1 時間、証明書利用者に基づきます

- id_token: アクセス トークンと同じ

### <a name="does-ad-fs-support-http-strict-transport-security-hsts"></a>AD FS では HTTP Strict Transport Security (HSTS) がサポートされますか?

HTTP Strict Transport Security (HSTS) は Web セキュリティ ポリシー メカニズムであり、HTTP と HTTPS の両方のエンドポイントを持つサービスに対するプロトコル ダウングレード攻撃や Cookie ハイジャックを緩和するのに役立ちます。 それを使用すると、Web サーバーで、Web ブラウザー (または他の準拠ユーザー エージェント) は HTTPS のみを使用して対話し、HTTP プロトコルを使用してはならないことを宣言できます。

Web 認証トラフィック用のすべての AD FS エンドポイントは、HTTPS 経由専用に開かれます。  その結果、AD FS では HTTP Strict Transport Security ポリシー メカニズムによって提供される脅威が効果的に軽減されます (設計上、HTTP にリスナーが存在しないため、HTTP にダウングレードできません)。 また、AD FS では、すべての Cookie をセキュリティで保護されたフラグでマークすることにより、HTTP プロトコル エンドポイントで別のサーバーに Cookie が送信されないようにできます。

したがって、ダウングレードすることはできないため、AD FS サーバーに HSTS を実装する必要はありません。  コンプライアンスに関しては、AD FS サーバーは、HTTP を使用できず、すべての Cookie が安全としてマークされるため、これらの要件を満たしています。

さらに、AD FS 2016 (最新の修正プログラムを適用) と AD FS 2019 では、HSTS ヘッダーの生成がサポートされています。 これを構成するには、「[AD FS 2019 で HTTP セキュリティ応答ヘッダーをカスタマイズする](../operations/customize-http-security-headers-ad-fs.md)」をご覧ください

### <a name="x-ms-forwarded-client-ip-does-not-contain-the-ip-of-the-client-but-contains-ip-of-the-firewall-in-front-of-the-proxy-where-can-i-get-the-right-ip-of-the-client"></a>X-ms-forwarded-client-ip には、クライアントの IP は含まれず、プロキシの前にあるファイアウォールの IP が含まれます。 クライアントの適切な IP はどこで入手できますか?
WAP の前に SSL を終了することはお勧めしません。 WAP の前面で SSL が終了された場合、X-ms-forwarded-client-ip には WAP の前にあるネットワーク デバイスの IP アドレスが含まれます。 AD FS によってサポートされている IP 関連のさまざまな要求の簡単な説明を次に示します。
 - x-ms-client-ip: STS に接続されているデバイスのネットワーク IP。  エクストラネット要求の場合、これには常に WAP の IP が含まれます。
 - x-ms-forwarded-client-ip: 複数値の要求。これには、Exchange Online によって AD FS に転送されるすべての値と、WAP に接続されているデバイスの IP アドレスが含まれます。
 - Userip: エクストラネット要求の場合、この要求には x-ms-forwarded-client-ip の値が含まれます。  イントラネット要求の場合、この要求には x-ms-client-ip と同じ値が含まれます。

 さらに、AD FS 2016 (最新の修正プログラムが適用されたもの) 以降のバージョンでは、x-forwarded-for ヘッダーのキャプチャもサポートされています。 レイヤー 3 (IP が保持される) での転送が行われないすべてのロード バランサーまたはネットワーク デバイスでは、受信したクライアント IP を業界標準の x-forwarded-for ヘッダーに追加する必要があります。

### <a name="i-am-trying-to-get-additional-claims-on-the-user-info-endpoint-but-its-only-returning-subject-how-can-i-get-additional-claims"></a>ユーザー情報エンドポイントで追加の要求を取得しようとしていますが、サブジェクトのみが返されます。 追加の要求を取得するにはどうすればよいですか?
AD FS の userinfo エンドポイントでは、常に、OpenID 標準で指定されているようにサブジェクト要求が返されます。 AD FS では、UserInfo エンドポイントを介して要求された追加の要求は提供されません。 ID トークンで追加の要求が必要な場合は、「[AD FS のカスタム ID トークン](../development/custom-id-tokens-in-ad-fs.md)」をご覧ください。

### <a name="why-do-i-see-a-lot-of-1021-errors-on-my-ad-fs-servers"></a>AD FS サーバーで 1021 エラーが多数表示されるのはなぜですか?
このイベントは、通常、リソース 00000003-0000-0000-c000-000000000000 に対して AD FS 上のリソース アクセスが無効である場合にログに記録されます。 このエラーは、Azure AD Graph サービスのアクセス トークンを取得しようとするクライアントの動作が正しくないことが原因で発生します。 AD FS にリソースが存在しないため、AD FS サーバーでイベント ID 1021 が発生します。 AD FS でのリソース 00000003-0000-0000-c000-000000000000 に対する警告やエラーは、無視しても安全です。

### <a name="why-am-i-seeing-a-warning-for-failure-to-add-the-ad-fs-service-account-to-the-enterprise-key-admins-group"></a>Enterprise Key Admins グループに AD FS サービス アカウントを追加できないという警告が表示されるのはなぜですか?
このグループは、FSMO PDC の役割を持つ Windows 2016 ドメイン コントローラーがドメイン内に存在する場合にのみ作成されます。 このエラーを解決するには、グループを手動で作成し、以下の手順に従って、サービス アカウントをグループのメンバーとして追加した後、必要なアクセス許可を付与します。
1.    **[Active Directory ユーザーとコンピューター]** を開きます。
2.    ナビゲーション ペインでドメイン名を**右クリック**し、[プロパティ] を**クリック**します。
3.    [セキュリティ] を**クリック**します ([セキュリティ] タブが表示されない場合は、[表示] メニューから [高度な機能] をオンにします)。
4.    [詳細設定] を**クリック**します。 [追加] を**クリック**します。 [プリンシパルの選択] を**クリック**します。
5.    [ユーザー、コンピューター、サービス アカウントまたはグループの選択] ダイアログ ボックスが表示されます。  [選択するオブジェクト名を入力してください] ボックスに「Key Admin Group」と入力します。  ［OK］をクリックします。
6.    [適用先] ボックスで、 **[Descendant User objects]\(子ユーザー オブジェクト\)** を選択します。
7.    スクロール バーを使用してページの下部までスクロールし、[すべてクリア] を**クリック**します。
8.    **[プロパティ]** セクションで、 **[Read msDS-KeyCredentialLink]\(msDS-KeyCredentialLink の読み取り\)** および **[Write msDS-KeyCredentialLink]\(msDS-KeyCredentialLink の書き込み\)** を選択します。

### <a name="why-does-modern-authentication-from-android-devices-fail-if-the-server-does-not-send-all-the-intermediate-certificates-in-the-chain-with-the-ssl-cert"></a>サーバーが SSL 証明書と共にチェーン内のすべての中間証明書を送信しない場合、Android デバイスからの先進認証が失敗するのはなぜですか?

フェデレーション ユーザーは、Android ADAL ライブラリを使用するアプリの Azure AD に対する認証が失敗する場合があります。 アプリでログイン ページを表示しようとすると、**AuthenticationException** を受け取ります。 Chrome では、AD FS ログイン ページが安全ではないと表示される場合があります。

Android のすべてのバージョンとすべてのデバイスでは、証明書の **authorityInformationAccess** フィールドから追加の証明書をダウンロードすることはサポートされていません。 これは Chrome ブラウザーにも当てはまります。 中間証明書が欠落しているサーバー認証証明書では、AD FS から証明書チェーン全体が渡されなかった場合、このエラーが発生します。

この問題の適切な解決策は、SSL 証明書と共に必要な中間証明書が送信されるように、AD FS と WAP サーバーを構成することです。

AD FS および WAP サーバーの SSL 証明書を 1 台のコンピューターからエクスポートし、コンピューターの個人用ストアにインポートするときは、必ず秘密キーをエクスポートし、**Personal Information Exchange - PKCS #12** を選択してください。

**[証明のパスにある証明書を可能であればすべて含む]** および **[すべての拡張プロパティをエクスポートする]** チェック ボックスをオンにすることが重要です。

Windows サーバーで certlm.msc を実行し、コンピューターの個人証明書ストアに *.PFX をインポートします。 これにより、サーバーで証明書チェーン全体が ADAL ライブラリに渡されるようになります。

>[!NOTE]
> ネットワーク ロード バランサーの証明書ストアも、証明書チェーン全体を含むように更新する必要があります (存在する場合)。

### <a name="does-ad-fs-support-head-requests"></a>AD FS では HEAD 要求はサポートされていますか?
AD FS では HEAD 要求はサポートされていません。  アプリケーションでは、AD FS エンドポイントに対して HEAD 要求を使用しないようにする必要があります。  これにより、予期しない、または遅延する HTTP エラー応答が発生する可能性があります。  また、AD FS イベント ログに予期しないエラー イベントが記録される場合があります。

### <a name="why-am-i-not-seeing-a-refresh-token-when-i-am-logging-in-with-a-remote-idp"></a>リモート IDP でログインしたときに、更新トークンが表示されないのはなぜですか?
IDP によって発行されたトークンの有効期間が 1 時間未満の場合、更新トークンは発行されません。 更新トークンが確実に発行されるようにするには、IDP によって発行されるトークンの有効期間を 1 時間以上に増やします。

### <a name="do-we-have-any-way-to-change-rp-token-encryption-algorithm"></a>RP トークン暗号化アルゴリズムを変更する方法はありますか?
RP トークンの暗号化は既定で AES256 に設定され、それ以外の値には変更できません。

### <a name="on-a-mixed-mode-farm-i-get-error-when-trying-to-set-the-new-ssl-certificate-using-set-adfssslcertificate--thumbprint-how-can-i-update-the-ssl-certificate-in-a-mixed-mode-ad-fs-farm"></a>混合モードのファームで、Set-AdfsSslCertificate -Thumbprint を使用して新しい SSL 証明書を設定しようとすると、エラーが発生します。 混合モードの AD FS ファームで SSL 証明書を更新する方法はありますか?
混合モードの AD FS ファームは、過渡状態が意図されています。 アップグレード プロセスの前に SSL 証明書をロールオーバーするか、プロセスを完了してから SSL 証明書を更新する前にファームの動作レベルを上げることを計画するようお勧めします。 これを行わなかった場合は、以下の手順に従って SSL 証明書を更新することができます。

WAP サーバーでは、Set-WebApplicationProxySslCertificate を引き続き使用できます。 AD FS サーバーでは、netsh を使用する必要があります。 次の手順のようにします。

1. メンテナンスする AD FS 2016 サーバーのサブセットを選択します (例: ロード バランサーから削除する)
2. ステップ 1 で選択したサーバーで、MMC を使用して新しい証明書をインポートします
3. 既存の証明書を削除します

    a。 netsh http delete sslcert hostnameport=fs.contoso.com:443 b. netsh http delete sslcert hostnameport=localhost:443 c. netsh http delete sslcert hostnameport=fs.contoso.com:49443

4.  新しい証明書を追加します

    a。 netsh http add sslcert hostnameport=fs.contoso.com:443 certhash=CERTTHUMBPRINT appid={5d89a20c-beab-4389-9447-324788eb944a} certstorename=MY sslctlstorename=AdfsTrustedDevices

    b. netsh http add sslcert hostnameport=localhost:443 certhash=CERTTHUMBPRINT appid={5d89a20c-beab-4389-9447-324788eb944a} certstorename=MY sslctlstorename=AdfsTrustedDevices

    c. netsh http add sslcert hostnameport=fs.contoso.com:49443 certhash=CERTTHUMBPRINT appid={5d89a20c-beab-4389-9447-324788eb944a} certstorename=MY sslctlstorename=AdfsTrustedDevices

5. 選択したサーバーで AD FS サービスを再起動します
6. メンテナンスする WAP サーバーのサブセットを削除します
7. 選択した WAP サーバーで、MMC を使用して新しい証明書をインポートします
8. コマンドレットを使用して、WAP で新しい証明書を設定します

    a。 Set-WebApplicationProxySslCertificate -Thumbprint " CERTTHUMBPRINT"

9. 選択した WAP サーバーでサービスを再起動します
10. 選択した WAP サーバーと AD FS サーバーを運用環境に戻します。

同じ方法で、残りの AD FS サーバーと WAP サーバーを更新します。

### <a name="is-adfs-supported-when-web-application-proxy-wap-servers-are-behind-azure-web-application-firewallwaf"></a>Web アプリケーション プロキシ (WAP) サーバーが Azure Web アプリケーション ファイアウォール (WAF) の内側にある場合、AD FS はサポートされますか?
AD FS と Web アプリケーション サーバーでは、エンドポイントで SSL 終了を実行しないすべてのファイアウォールがサポートされます。 さらに、AD FS サーバーと WAP サーバーには、クロスサイト スクリプティングや AD FS プロキシなどの一般的な Web 攻撃を防止し、[MS-ADFSPIP プロトコル](/openspecs/windows_protocols/ms-adfspip/76deccb1-1429-4c80-8349-d38e61da5cbb)で定義されているすべての要件を満たすためのメカニズムが組み込まれています。

### <a name="i-am-seeing-an-event-441-a-token-with-a-bad-token-binding-key-was-found-what-should-i-do-to-resolve-this"></a>"イベント 441: 誤ったトークンのバインド キーを持つトークンが見つかりました" と表示されます。 これを解決するにはどうすればよいですか?
AD FS 2016 では、トークンのバインドが自動的に有効になり、プロキシとフェデレーションのシナリオでの複数の既知の問題のため、このエラーが発生します。 これを解決するには、次の PowerShell コマンドを実行して、トークンのバインドのサポートを削除します。

`Set-AdfsProperties -IgnoreTokenBinding $true`

### <a name="i-have-upgraded-my-farm-from-ad-fs-in-windows-server-2016-to-ad-fs-in-windows-server-2019-the-farm-behavior-level-for-the-ad-fs-farm-has-been-successfully-raised-to-2019-but-the-web-application-proxy-configuration-is-still-displayed-as-windows-server-2016"></a>Windows Server 2016 の AD FS から Windows Server 2019 の AD FS にファームをアップグレードしました。 AD FS ファームのファーム動作レベルを 2019 に上げることはできましたが、Web アプリケーション プロキシの構成がまだ Windows Server 2016 と表示されるのはなぜですか?
Windows Server 2019 にアップグレードした後も、Web アプリケーション プロキシの構成バージョンは、引き続き Windows Server 2016 と表示されます。 Web アプリケーション プロキシには、Windows Server 2019 向けの新バージョン固有の機能はありません。AD FS でファーム動作レベルを正常に引き上げた場合でも、Web アプリケーション プロキシでは、設計上、Windows Server 2016 と引き続き表示されます。

### <a name="can-i-estimate-the-size-of-the-adfsartifactstore-before-enabling-esl"></a>ESL を有効にする前に、ADFSArtifactStore のサイズを見積もることはできますか?
ESL を有効にすると、AD FS では、ADFSArtifactStore データベースでユーザーのアカウント アクティビティと既知の場所が追跡されます。 このデータベースのサイズは、追跡されるユーザーと既知の場所の数に比例してスケーリングされます。 ESL の有効化を計画するとき、ADFSArtifactStore データベースのサイズは、10 万ユーザーあたり最大 1 GB の割合で増加すると見積もることができます。 AD FS ファームで Windows Internal Database (WID) が使用されている場合、データベース ファイルの既定の場所は C:\Windows\WID\Data です。 このドライブがいっぱいにならないよう、ESL を有効にする前に、少なくとも 5 GB の空き記憶域があることを確認してください。 ESL を有効にした後は、ディスク記憶域に加えて、プロセス メモリの総量も、50 万人以下のユーザーに対して、最大 1 GB の RAM が追加されるものとして計画します。

### <a name="i-am-seeing-event-570-active-directory-trust-enumeration-was-unable-to-enumerate-one-of-more-domains-due-to-the-following-error-enumeration-will-continue-but-the-active-directory-identifier-list-may-not-be-correct-validate-that-all-expected-active-directory-identifiers-are-present-by-running-get-adfsdirectoryproperties-on-ad-fs-2019-what-is-the-mitigation-for-this-event"></a>AD FS 2019 でイベント 570 が表示されます (Active Directory trust enumeration was unable to enumerate one of more domains due to the following error. Enumeration will continue but the Active Directory identifier list may not be correct. Validate that all expected Active Directory identifiers are present by running Get-ADFSDirectoryProperties/(Active Directory 信頼列挙で、次のエラーのため、ドメインの 1 つを列挙できませんでした。列挙は続行されますが Active Directory 識別子の一覧が正しくない可能性があります。Get-ADFSDirectoryProperties を実行して、予期されるすべての Active Directory 識別子が存在することを確認してください/))。 このイベントの軽減策は何ですか?
このイベントは、AD FS が信頼されているフォレストのチェーン内のすべてのフォレストを列挙し、すべてのフォレスト全体で接続しようとして、フォレストが信頼されていない場合に発生します。 たとえば、AD FS フォレスト A とフォレスト B が信頼されていて、フォレスト B とフォレスト C が信頼されている場合、AD FS は 3 つのすべてのフォレストを列挙し、フォレスト A と C の間の信頼を検出しようとします。失敗したフォレストのユーザーを AD FS によって認証する必要がある場合は、AD FS フォレストと、失敗しているフォレストとの間に信頼関係を設定します。 失敗したフォレストのユーザーを AD FS によって認証すべきでない場合は、このエラーは無視してください。

### <a name="i-am-seeing-an-event-id-364-microsoftidentityserverauthenticationfailedexception-msis5015-authentication-of-the-presented-token-failed-token-binding-claim-in-token-must-match-the-binding-provided-by-the-channel-what-should-i-do-to-resolve-this"></a>"Event ID 364:Microsoft.IdentityServer.AuthenticationFailedException:MSIS5015:Authentication of the presented token failed. Token Binding claim in token must match the binding provided by the channel."\(イベント ID 364: Microsoft.IdentityServer.AuthenticationFailedException: MSIS5015: 提示されたトークンの認証に失敗しました。トークンのトークン バインド要求は、チャネルによって提供されたバインドと一致している必要があります。\)" と表示されます。 これを解決するにはどうすればよいですか?
AD FS 2016 では、トークンのバインドが自動的に有効になり、プロキシとフェデレーションのシナリオでの複数の既知の問題のため、このエラーが発生します。 これを解決するには、次の PowerShell コマンドを実行して、トークンのバインドのサポートを削除します。

`Set-AdfsProperties -IgnoreTokenBinding $true`
