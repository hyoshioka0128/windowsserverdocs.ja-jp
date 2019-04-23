---
ms.assetid: acc9101b-841c-4540-8b3c-62a53869ef7a
title: AD FS 2016 に関する FAQ
description: AD FS 2016 のよく寄せられる質問
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 12/07/2018
ms.topic: article
ms.custom: it-pro
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: d8014cd72e66642ea9200afd6cd4266cbccba30c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826813"
---
# <a name="ad-fs-frequently-asked-questions-faq"></a>AD FS のよく寄せられる質問 (FAQ)

>適用先:Windows Server 2016

次のドキュメントは、Active Directory フェデレーション サービスに関してよく寄せられる質問へのホームです。  ドキュメントは、質問の種類に基づくグループに分割されています。

## <a name="deployment"></a>展開 

### <a name="how-can-i-upgrademigrate-from-previous-versions-of-ad-fs"></a>移行する方法をアップグレード/AD FS の以前のバージョンから
次のいずれかを使用して AD FS をアップグレードすることができます。


- Windows Server 2016 AD FS を Windows Server 2012 R2 AD FS
    - [AD FS WID データベースを使用して Windows Server 2016 にアップグレードします。](../deployment/Upgrading-to-AD-FS-in-Windows-Server-2016.md)
    - [SQL database を使用して Windows Server 2016 での AD FS へのアップグレード](../deployment/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL.md)
- Windows Server 2012 AD FS を Windows Server 2012 R2 AD FS
    - [Windows Server 2012 R2 で AD FS への移行します。](https://technet.microsoft.com/library/dn486815.aspx)
- Windows Server 2012 の AD FS には、AD FS 2.0
    - [Windows Server 2012 で AD FS への移行します。](https://technet.microsoft.com/library/jj647765.aspx)
- AD FS 1.x と AD FS 2.0 
    - [AD FS からのアップグレードに AD FS 2.0 1.x](https://technet.microsoft.com/library/ff678035.aspx)

AD FS 2.0 または 2.1 (Windows Server 2008 R2 または Windows Server 2012) からアップグレードする必要がある場合は、(C:\Windows\ADFS にある) ボックスにスクリプトを使用する必要があります。

### <a name="why-does-ad-fs-installation-require-a-reboot-of-the-server"></a>AD FS のインストールで、サーバーの再起動が必要なはなぜですか。

Windows Server 2016 で http/2 サポートが追加されましたが、クライアント証明書認証の http/2 を使用することはできません。  多くの AD FS のシナリオには、クライアント証明書の認証の使用と多数のクライアントは再試行をサポートしていませんので、使用して要求を http/1.1、AD FS ファームの構成が再構成されます http/1.1 するローカル サーバーの HTTP 設定。  これには、サーバーの再起動が必要です。  

### <a name="is-using-windows-2016-wap-servers-to-publish-the-ad-fs-farm-to-the-internet-without-upgrading-the-back-end-ad-fs-farm-supported"></a>Windows 2016 の WAP サーバーを使用して、サポートされているバックエンドの AD FS ファームをアップグレードすることがなく、AD FS ファームをインターネットに公開しますか。
はい、この構成はサポートされて、ただし、この構成で AD FS 2016 の新機能はサポートしません。  この構成では、AD FS 2016 には、AD FS 2012 R2 から移行フェーズ中に一時するものではあり、長期間にはデプロイされません。

### <a name="is-it-possible-to-deploy-ad-fs-for-office-365-without-publishing-a-proxy-to-office-365"></a>Office 365 へのプロキシを公開せず、Office 365 の AD FS をデプロイすることはできますか。
はい、これはサポートされています。 ただし、副作用として

1. Azure AD は、フェデレーション メタデータにアクセスできないために、トークン署名証明書の更新を手動で管理する必要があります。 トークン署名証明書を手動で更新の詳細については、読み取る[Office 365 と Azure Active Directory のフェデレーション証明書の更新](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-o365-certs)
2. レガシー認証フロー (例: ExO プロキシ認証フロー) を利用することはできません。

### <a name="what-are-load-balancing-requirements-for-ad-fs-and-wap-servers"></a>AD FS および WAP サーバーの負荷分散の要件とは 

AD FS は、ステートレスなシステムです。 そのため、負荷分散はログインの非常に単純です。 負荷分散システムの主な推奨事項を次に示します。 


- ロード バランサーは、IP アフィニティを使用して構成されていない必要があります。 過度の負荷を配置すると、Exchange Online の特定のシナリオで、サーバーのサブセットにこの可能性があります。
- ロード バランサーは必要がありますいない HTTPS 接続を終了し、ADFS サーバーへの新しい接続を再実行します。 
- ロード バランサーは、ADFS に送信されるときに、接続元 IP アドレスが HTTP パケットのソース ip アドレスと変換することを確認してください。 ロード バランサーは、HTTP パケットで送信元 ip アドレスを送信することはできません、こと、ロード バランサーする必要があります追加 (または既存が発生した場合の追加)、x のヘッダーに IP アドレス。 これは、機能は、特定の IP の適切な処理が関連機能 (IP の禁止されているため、エクストラネット スマート ロックアウト、...) と、正しく構成されていない場合、セキュリティが低下する可能性が必要です。 
- ロード バランサーには、SNI をサポートする必要があります。 イベントのそうでない、SNI が非対応クライアントを処理するために HTTPS バインドを作成する AD FS が構成されていることを確認します。
- ロード バランサーでは、AD FS WAP サーバーが稼働して、200 OK が返されない場合にそれらを除外するかどうかを検出するために、AD FS の HTTP の正常性プローブのエンドポイントを使用する必要があります。 

### <a name="what-multi-forest-configurations-are-supported-by-ad-fs"></a>AD FS によっては、どのような複数フォレスト構成がサポートされていますか。 

AD FS では、複数のマルチ フォレスト構成をサポートしているし、複数の信頼領域間のユーザーを認証する基礎となる AD DS 信頼ネットワークに依存しています。 双方向のフォレストの信頼は、これは問題なく信頼サブシステムが正しく動作するために単純なセットアップ強く推奨します。 かつ 

- パートナー id を格納している DMZ フォレストなど方法の 1 つのフォレストの信頼が発生した場合は、corp フォレスト内の ad FS を展開して、LDAP 経由で接続されている別のローカルの要求プロバイダー信頼と DMZ フォレストを扱うことを勧めします。 このオプションを追求することはできません、イベントには、「信頼」、"信頼されているフォレスト"を「信頼」フォレスト内のユーザーへのフル アクセスを持つサービス アカウントを使用してフォレストで ad FS を実行する必要があります。
- ドメイン レベルの信頼はサポートされており、操作できるは、フォレスト レベルの信頼モデルに移行することを強くお勧めします。 さらに、UPN がルーティングと名の NETBIOS 名前解決が正確にさせる必要があることを確認する必要があります。 



## <a name="design"></a>設計

### <a name="what-third-party-multi-factor-authentication-providers-are-available-for-ad-fs"></a>AD FS の使用可能などのようなサード パーティの多要素認証プロバイダー 
認識しています、サード パーティ プロバイダーの一覧を次に示します。  についてわからないことと、それらについて説明します一覧を更新しましたが、使用可能なプロバイダー常にあります。

- [Gemalto アイデンティティ & セキュリティ サービス](http://www.gemalto.com/identity)
- [inWebo エンタープライズ認証サービス](http://www.inwebo.com/)
- [Login People MFA API コネクタ](https://www.loginpeople.com)
- [Microsoft Active Directory フェデレーション サービス用には、RSA SecurID 認証エージェント](http://www.emc.com/security/rsa-securid/rsa-authentication-agents/microsoft-ad-fs.htm)
- [SafeNet Authentication Service (SAS) エージェント for AD FS](http://www.safenet-inc.com/resources/integration-guide/data-protection/Safenet_Authentication_Service/SafeNet_Authentication_Service__AD_FS_Agent_Configuration_Guide/?langtype=1033)
- [Swisscom 社 Mobile ID 認証サービス](http://swisscom.ch/mid)
- [Symantec の検証と ID 保護サービス (VIP)](http://www.symantec.com/vip-authentication-service) 

### <a name="are-third-party-proxies-supported-with-ad-fs"></a>サード パーティ製プロキシは、AD FS でサポートされますか。
はい、サード パーティ製プロキシは、Web アプリケーション プロキシは、前に配置することができますが、任意のサード パーティ製プロキシをサポートする必要があります、 [MS ADFSPIP プロトコル](https://msdn.microsoft.com/library/dn392811.aspx)Web アプリケーション プロキシの代わりに使用されます。

### <a name="what-third-party-proxies-are-available-for-ad-fs-that-support-ms-adfspip"></a>どのようなサード パーティ製プロキシ MS ADFSPIP をサポートする AD FS の利用ですか。

認識しています、サード パーティ プロバイダーの一覧を次に示します。  についてわからないことと、それらについて説明します一覧を更新しましたが、使用可能なプロバイダー常にあります。

- [F5 キーを押して Access Policy Manager](https://support.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-third-party-integration-13-1-0/12.html#guid-1ee8fbb3-1b33-4982-8bb3-05ae6868d9ee)

### <a name="where-is-the-capacity-planning-sizing-spreadsheet-for-ad-fs-2016"></a>場所は、キャパシティ プランニング サイジング スプレッドシート AD FS 2016 でしょうか。
スプレッドシートの AD FS 2016 バージョンをダウンロードできます[ここ](http://adfsdocs.blob.core.windows.net/adfs/ADFSCapacity2016.xlsx)します。
これは、Windows Server 2012 R2 の AD FS で使用できます。

### <a name="how-can-i-ensure-my-ad-fs-and-wap-servers-support-apples-atp-requirements"></a>確保すれば、AD FS と WAP サーバーがサポート Apple の ATP の要件ですか。

Apple では、一連の AD FS に対して認証する iOS アプリからの呼び出しに影響を与える可能性 App Transport Security (ATS) と呼ばれる要件がリリースされました。  おくと、AD FS と WAP サーバーをサポートするかどうかを確実に遵守、 [ATS を使用して接続するための要件](https://developer.apple.com/library/prerelease/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW57)します。  
具体的には、AD FS と WAP サーバーが TLS 1.2 をサポートし、TLS 接続のネゴシエートされた暗号スイートが完璧な前方 secrecy をサポートすることを確認する必要があります。

有効にして、SSL 2.0、3.0、TLS バージョン 1.0、1.1、1.2 を無効にすることができますを使用して[AD FS での SSL プロトコルの管理](../operations/Manage-SSL-Protocols-in-AD-FS.md)します。

AD FS と WAP サーバーが ATP をサポートする唯一の TLS 暗号スイートをネゴシエート、されていないすべての暗号スイートを無効にすることができます、 [ATP 準拠の暗号スイートの一覧](https://developer.apple.com/library/prerelease/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW57)します。  これを行うには、使用、 [Windows TLS の PowerShell コマンドレット](https://technet.microsoft.com/itpro/powershell/windows/tls/index)します。 

## <a name="developer"></a>Developer

### <a name="when-generating-an-idtoken-with-adfs-for-a-user-authenticated-against-ad-how-is-the-sub-claim-generated-in-the-idtoken"></a>AD に対して認証されたユーザーには、ADFS を使用した id_token を生成するときに、"sub"要求の生成方法、id_token に含まれるでしょうか。
"Sub"要求の値は、クライアント ID のハッシュ + アンカー要求の値。

### <a name="what-is-the-lifetime-of-the-refresh-tokenaccess-token-when-the-user-logs-in-via-a-remote-claims-provider-trust-over-ws-fedsaml-p"></a>更新トークンやアクセス トークンの有効期間は、ユーザーがログインすると、リモートの要求プロバイダー信頼を使用して WS Fed/SAML-P 経由で何ですか。 
更新トークンの有効期間は、ADFS をリモート要求プロバイダー信頼から取得したトークンの有効期間になります。 アクセス トークンの有効期間は、アクセス トークンを発行する証明書利用者のトークンの有効期間になります。

### <a name="i-need-to-return-profile-and-email-scopes-as-well-in-addition-to-the-openid-scope-can-i-obtain-additional-information-using-scopes-how-to-do-it-in-ad-fs"></a>OpenId スコープだけでなくもプロファイルと電子メールのスコープを返す必要があります。 スコープを使用して追加の情報を入手できますか。 AD FS で行う方法は?
カスタマイズされた id_token を使用すると、自体 id_token に含まれる関連情報を追加します。 詳細については、この記事を参照してください。 [id_token に出力する要求をカスタマイズ](../development/Custom-Id-Tokens-in-AD-FS.md)します。

### <a name="how-to-issue-json-blobs-inside-jwt-tokens"></a>JWT トークン内の json blob を発行する方法でしょうか。
特殊な値型 ("http://www.w3.org/2001/XMLSchema#json") と AD FS 2016 で追加されたこの character(\x22) をエスケープします。 発行規則とアクセス トークンから最終的な出力の下のサンプルをしてください。

サンプルの発行ルール:

    => issue(Type = "array_in_json", ValueType = "http://www.w3.org/2001/XMLSchema#json", Value = "{\x22Items\x22:[{\x22Name\x22:\x22Apple\x22,\x22Price\x22:12.3},{\x22Name\x22:\x22Grape\x22,\x22Price\x22:3.21}],\x22Date\x22:\x2221/11/2010\x22}");

アクセス トークンで発行された要求。

    "array_in_json":{"Items":[{"Name":"Apple","Price":12.3},{"Name":"Grape","Price":3.21}],"Date":"21/11/2010"}

### <a name="can-i-pass-resource-value-as-part-of-the-scope-value-like-how-requests-are-done-against-azure-ad"></a>Azure AD に対して要求を実行する方法のように、スコープの値の一部としてリソースの値を渡すか。 
2019 のサーバーで AD FS、スコープのパラメーターに埋め込まれたリソースの値を渡すことができますようになりました。 スコープのパラメーターは、リソース/スコープとして構造体の各エントリのスペースで区切られた一覧としてここで整理できます。 次に例を示します。  
**< サンプルの有効な要求の作成 >**

### <a name="does-ad-fs-support-pkce-extension"></a>AD FS は PKCE の拡張機能をサポートしますか。
AD FS サーバー 2019年の Proof Key for コード Exchange (による PKCE) のサポート OAuth 承認コード付与フロー 

## <a name="operations"></a>操作

### <a name="how-do-i-replace-the-ssl-certificate-for-ad-fs"></a>AD FS の SSL 証明書を交換する方法 
AD FS SSL 証明書は、AD FS 管理スナップインで見つかった AD FS サービス通信証明書と同じではありません。  AD FS SSL 証明書を変更するには、PowerShell を使用する必要があります。 以下の記事のガイダンスに従います。

[AD FS と WAP 2016 での SSL 証明書の管理](../operations/Manage-SSL-Certificates-AD-FS-WAP-2016.md)

### <a name="how-can-i-enable-or-disable-tlsssl-settings-for-ad-fs"></a>または方法は有効にする AD FS の TLS または SSL の設定を無効にします。
無効にするか、SSL プロトコルを有効にして暗号スイートを次の手順に従います。

[AD FS での SSL プロトコルを管理します。](../operations/Manage-SSL-Protocols-in-AD-FS.md)

### <a name="does-the-proxy-ssl-certificate-have-to-be-the-same-as-the-ad-fs-ssl-certificate"></a>プロキシの SSL 証明書に AD FS SSL 証明書と同じであるか。  
プロキシの SSL 証明書と AD FS SSL 証明書に関して次のガイダンスを使用します。


- プロキシを使用する場合、プロキシの SSL 証明書、Windows 統合認証を使用する AD FS プロキシ要求する必要がありますと同じである (同じキーを使用して) フェデレーション サーバーの SSL 証明書
- プロキシの SSL 証明書が (同じキーを使用) と同じフェデレーション サーバーの SSL 証明書をする必要があります (既定の AD FS で設定) が"ExtendedProtectionTokenCheck"は、AD FS プロパティに有効な場合
- それ以外の場合、プロキシの SSL 証明書は AD FS SSL 証明書から別のキーを持つことができますが、同じを満たす必要があります[要件](../overview/AD-FS-2016-Requirements.md)

### <a name="how-can-i-configure-promptlogin-behavior-for-ad-fs"></a>プロンプトを構成する方法の AD FS ログインの動作を = ですか?
プロンプトを構成する方法については、ログイン = を参照してください[Active Directory フェデレーション サービスの要求パラメーターのログインのサポートを =](../operations/AD-FS-Prompt-Login.md)します。

### <a name="how-can-i-configure-browsers-to-use-windows-integrated-authentication-wia-with-ad-fs"></a>AD FS で Windows 統合認証 (WIA) を使用するブラウザーを構成する方法はありますか

ブラウザーを構成する方法については、次を参照してください。 [AD FS で Windows 統合認証 (WIA) を使用するブラウザーを構成する](../operations/Configure-AD-FS-Browser-WIA.md)します。

### <a name="can-i-trun-off-browserssoenabled"></a>BrowserSsoEnabled の電源を切りますをできますか。
ADFS; を使用してビジネスの証明書登録用の ADFS や Windows こんにちはデバイスに基づいてアクセス制御ポリシーがあるない場合BrowserSsoEnabled オフにすることができます。 BrowserSsoEnabled は、デバイス情報を含むクライアントから PRT (プライマリ更新トークン) を収集する ADFS を使用できます。 そのデバイスがなくても ADFS の認証は、Windows 10 デバイスでは機能しません。

### <a name="how-long-are-ad-fs-tokens-valid"></a>有効な AD FS トークンは、どのくらいの時間のでしょうか。

多くの場合、この質問は、' どのくらいの期間はユーザーの取得シングル サインオン (SSO) を新しい資格情報を入力しなくても管理者の管理方法をでしょうか。 '  この動作では、およびそれを制御する構成設定が、この記事で説明されている[AD のシングル サインオン設定](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/ad-fs-2016-single-sign-on-settings)します。

さまざまな cookie とトークンの既定の有効期間は、(有効期間を制御するパラメーター) および以下に示します。

**登録済みデバイス**

- PRT と SSO cookie:90 日間の最大値は、PSSOLifeTimeMins によって管理されます。 (指定されたデバイスが使用される、少なくとも 14 日間、DeviceUsageWindow で制御されます)

- 更新トークン: 一貫性のある動作を提供するには、上記のに基づいて計算されます

- access_token:証明書利用者をに基づいて、既定では、1 時間

- id_token: アクセス トークンと同じ

**デバイスの登録解除**

- SSO cookie:既定では、8 時間は、SSOLifetimeMins によって管理されます。  (KMSI) の保持にサインインを有効にすると、既定では 24 時間と KMSILifetimeMins を使用して構成できます。


- 更新トークン。既定では 8 時間です。 KMSI を有効になっていると、24 時間

- access_token:証明書利用者をに基づいて、既定では、1 時間

- id_token: アクセス トークンと同じ

### <a name="does-ad-fs-support-http-strict-transport-security-hsts"></a>AD FS は、HTTP Strict Transport Security (HSTS) をサポートしますか。  

HTTP Strict Transport Security (HSTS) は、web セキュリティのポリシー メカニズムのプロトコルのダウン グレード攻撃や cookie のハイジャックを HTTP と HTTPS の両方のエンドポイントを持つサービスを軽減するのに役立ちます。 Web サーバーは、web ブラウザー (またはその他の complying ユーザー エージェント) のみの対話で HTTPS を使用して、HTTP プロトコルを使用することはありませんを宣言できます。

Web 認証トラフィックのすべての AD FS のエンドポイントは https のみを使って開かれます。  その結果、AD FS で効果的に HTTP Strict Transport Security ポリシー メカニズムを提供する脅威が軽減 (デザインではありません HTTP へのダウン グレードで HTTP リスナーが存在しないため)。 さらに、AD FS では、すべての cookie をセキュリティで保護されたフラグでマークすることで、HTTP プロトコルのエンドポイントを持つ別のサーバーに送信されない cookie をできないようにします。

そのため、HSTS を実装する AD FS サーバーでは必要ありません、決してダウン グレードできるためです。  コンプライアンスのために、AD FS サーバーは、HTTP が使用できないと、すべての cookie がセキュリティで保護されたマークされているため、これらの要件を満たします。

### <a name="x-ms-forwarded-client-ip-does-not-contain-the-ip-of-the-client-but-contains-ip-of-the-firewall-in-front-of-the-proxy-where-can-i-get-the-right-ip-of-the-client"></a>X-ms-転送-クライアントの ip は、クライアントの ip アドレスが含まれていないが、プロキシの前に、ファイアウォールの ip アドレスが含まれています。 クライアントの適切な IP を見いだすことのできるでしょうか。
WAP の前に、SSL 終了を行うには推奨されません。 場合は、WAP の前に、SSL 終了が終了したら、X-ms-転送-クライアントの ip アドレスには WAP の前に、ネットワーク デバイスの ip アドレスが含まれます。 関連する AD FS でサポートされている要求のさまざまな IP の簡単な説明を次に示します。
 - x-ms-client-ip :ネットワークを STS に接続されているデバイスの IP。  エクストラネットの要求の場合は常に、WAP の ip アドレスを含みます。
 - x-ms-forwarded-client-ip :Exchange Online と WAP に接続されているデバイスの IP アドレスによって、ADFS に転送されるすべての値が含まれる複数値の要求。
 - Userip:エクストラネット要求にはこの要求には x-ms-転送-クライアントの ip の値が含まれます。  この要求では、イントラネットの要求について x ms クライアント ip と同じ値が含まれます。

### <a name="i-am-trying-to-get-additional-claims-on-the-user-info-endpoint-but-its-only-returning-subject-how-can-i-get-additional-claims"></a>件名がユーザー情報エンドポイントがそののみを返す追加の要求の取得を試してみます。 その他の要求を取得する方法はありますか
ADFS の userinfo エンドポイントは、OpenID 標準で指定されているサブジェクト要求を常に返します。 AD FS では、UserInfo エンドポイント経由で要求される追加の要求は提供されません。 ID トークン内の他の要求が必要な場合を参照してください[AD FS でのカスタム ID トークン](../development/custom-id-tokens-in-ad-fs.md)します。

### <a name="why-do-i-see-a-lot-of-1021-errors-on-my-ad-fs-servers"></a>自分の AD FS サーバーで、多くの 1021 のエラーが参照する理由
このイベントは、通常はリソース 00000003-0000-0000-c000-000000000000 の AD FS での無効なリソース アクセス用に記録されます。 このエラーは、Azure AD Graph サービスのアクセス トークンを取得しようとする、クライアントのエラー動作によって発生します。 リソースが AD FS に存在しないために、この AD FS サーバーでイベント ID 1021 の結果します。 警告または AD fs リソース 00000003-0000-0000-c000-000000000000 のエラーを無視しても安全になります。 

### <a name="why-am-i-seeing-a-warning-for-failure-to-add-the-ad-fs-service-account-to-the-enterprise-key-admins-group"></a>エンタープライズ Key Admins グループに、AD FS サービス アカウントを追加するエラーの警告が表示されるはなぜですか。
このグループが作成されるは、PDC の FSMO の役割を持つ Windows 2016 のドメイン コント ローラーがドメインに存在する場合のみです。 エラーを解決するには、グループを手動で作成およびに従って、サービス アカウント グループのメンバーとして追加した後は必要なアクセス許可を与える以下。
1.  **[Active Directory ユーザーとコンピューター]** を開きます。 
2.  **右クリック**ナビゲーション ウィンドウから、ドメイン名と**クリックして**プロパティ。
3.  **クリックして**セキュリティ (セキュリティ タブがない場合に高度な機能の表示 メニューから)。
4.  **クリックして**高度な。 **クリックして**を追加します。 **クリックして**プリンシパルを選択します。
5.  [ユーザー、コンピューター、サービス アカウントまたはグループ] ダイアログ ボックスが表示されます。  テキスト ボックスに入力オブジェクトの名前、キーの管理グループを入力します。  [OK] をクリックします。
6.  [適用先] ボックスの一覧で選択**子孫ユーザー オブジェクト**します。
7.  スクロール バーを使用して、ページの下部までスクロールし、 ** をクリックして**すべてクリアします。
8.  **プロパティ**セクションで、 **msDS KeyCredentialLink を読み取る**と**書き込み msDS KeyCredentialLink**します。

### <a name="why-does-modern-authentication-from-android-devices-fail-if-the-server-does-not-send-all-the-intermediate-certificates-in-the-chain-with-the-ssl-cert"></a>Android デバイスからの最新の認証が失敗する理由、サーバーが SSL 証明書チェーン内すべての中間証明書を送信しない場合ですか。

Android ADAL ライブラリ失敗を使用するアプリの Azure AD 認証をフェデレーション ユーザーがあります。 アプリが表示されます、 **AuthenticationException**ログイン ページを表示しようとします。 Chrome の場合、AD FS ログイン ページという危険とします。

Android - すべてのバージョンとのすべてのデバイス間ではサポートしていませんから追加の証明書のダウンロード、 **authorityInformationAccess**証明書のフィールド。 これは、Chrome ブラウザーを同様の場合は true。 中間証明書が不足している任意のサーバー認証証明書は、AD FS からは、全体の証明書チェーンが渡されない場合もこのエラーになります。 

この問題を適切なソリューションでは、必要な中間証明書と SSL 証明書を送信する AD FS と WAP サーバーを構成します。 

コンピューターの個人用ストア、AD FS と WAP サーバーの場合にインポートする 1 つのマシンから SSL 証明書をエクスポートする秘密キーと選択をエクスポートすることを確認して**Personal Information Exchange - PKCS #12**します。 

チェック ボックスをする重要な**可能であれば、証明書のパスにすべての証明書を含む**がチェックされ、だけでなく**すべての拡張プロパティをエクスポート**します。 

Windows サーバー上で certlm.msc を実行し、インポート、*。コンピューターの個人証明書ストアに PFX です。 これをサーバー全体の証明書チェーンを ADAL ライブラリに渡すとなります。 

>[!NOTE]
> 証明書ストアのネットワーク ロード バランサーは、存在する場合は、全体の証明書チェーンを含めるも更新する必要があります。

### <a name="does-ad-fs-support-head-requests"></a>AD FS は HEAD 要求をサポートしますか。
AD FS では、HEAD 要求はサポートされていません。  アプリケーションで AD FS のエンドポイントに対して HEAD 要求が使用していない必要があります。  予期しないや遅延が HTTP エラー応答がある可能性があります。  さらに、AD FS イベント ログで予期しないエラー イベントを表示可能性があります。

### <a name="why-am-i-not-seeing-a-refresh-token-when-i-am-logging-in-with-a-remote-idp"></a>なぜいないが発生する更新トークンはいるリモートの IdP にログインする場合ですか。
IdP によって発行されたトークンがある、validty 1 時間未満の場合は、更新トークンは発行されません。 更新トークンが発行されたことを確認するには、するには、1 時間以上に、IdP によって発行されたトークンの有効性を増やします。

### <a name="do-we-have-any-way-to-change-rp-token-encryption-algorithm"></a>RP のトークンの暗号化アルゴリズムを変更する方法をいらっしゃいますか。
既定では、RP のトークン暗号化は AES256 を設定し、その他の値を変更することはできません。

### <a name="on-a-mixed-mode-farm-i-get-error-when-trying-to-set-the-new-ssl-certificate-using-set-adfssslcertificate--thumbprint-how-can-i-update-the-ssl-certificate-in-a-mixed-mode-ad-fs-farm"></a>混合モードのファームでエラーが発生 Set-adfssslcertificate を使用して新しい SSL 証明書を設定しようとするときの拇印。 混在モードの AD FS ファームの SSL 証明書を更新する方法は?
WAP サーバーのセット WebApplicationProxySslCertificate を引き続き使用できます。 ADFS サーバーでは、netsh を使用する必要があります。 以下に指定されている手順に従います。

1. メンテナンスのための ADFS 2016 サーバーのサブセットを選択します (例: ロード バランサーから削除)
2. 1 で選択されているサーバー、MMC を使用して新しい証明書をインポートします。
3. 既存の証明書を削除します。

    a.  netsh http delete sslcert hostnameport=fs.contoso.com:443 b。 netsh http delete sslcert hostnameport = localhost:443 c。 netsh http delete sslcert hostnameport=fs.contoso.com:49443

4.  新しい証明書を追加します。

    a.  netsh http 追加 sslcert hostnameport=fs.contoso.com:443 certhash CERTTHUMBPRINT appid = {5d89a20c-beab-4389-9447-324788eb944a} certstorename = MY sslctlstorename = AdfsTrustedDevices を =
    
    b.  netsh http 追加 sslcert hostnameport localhost:443 certhash = CERTTHUMBPRINT appid = {5d89a20c-beab-4389-9447-324788eb944a} certstorename = MY sslctlstorename = AdfsTrustedDevices を =
    
    c. netsh http 追加 sslcert hostnameport=fs.contoso.com:49443 certhash CERTTHUMBPRINT appid = {5d89a20c-beab-4389-9447-324788eb944a} certstorename = MY sslctlstorename = AdfsTrustedDevices を =

5. 選択したサーバーでの ADFS サービスを再起動します。
6. メンテナンスの WAP サーバーのサブセットを削除します。
7. 選択した WAP サーバー MMC を使用して新しい証明書をインポートします。
8. コマンドレットを使用して WAP での新しい証明書を設定します。

    a.  Set-WebApplicationProxySslCertificate -Thumbprint " CERTTHUMBPRINT"

9. 選択の WAP サーバー上でサービスを再起動します。
10. 運用環境に戻り、選択した WAP と AD FS サーバーを配置します。 
    
AD FS の残りの部分と同様に、WAP サーバーの更新プログラムを実行します。 

### <a name="is-adfs-supported-when-web-application-proxy-wap-servers-are-behind-azure-web-application-firewallwaf"></a>Web アプリケーション プロキシ (WAP) サーバーが Azure の Web アプリケーションの Firewall(WAF) の背後にあるときに ADFS がサポートされますか。
ADFS と Web アプリケーション サーバーは、エンドポイントで SSL 終了を実行しないすべてのファイアウォールをサポートします。 さらに、ad FS/WAP サーバーがクロスサイト スクリプティング、ADFS プロキシなどの一般的な web 攻撃を防止しで定義されているすべての要件を満たすためのメカニズムに構築された、 [MS ADFSPIP プロトコル](https://msdn.microsoft.com/library/dn392811.aspx)します。