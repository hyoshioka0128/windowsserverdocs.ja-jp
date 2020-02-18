---
ms.assetid: aa892a85-f95a-4bf1-acbb-e3c36ef02b0d
title: Windows Server 2016 の Active Directory フェデレーション サービス (AD FS) の新機能
description: ''
author: billmath
ms.author: billmath
manager: daveba
ms.date: 01/22/2020
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: adce37d8d06399d3a00221a12f3449244720ade7
ms.sourcegitcommit: 840d1d8851f68936db3934c80796fb8722d3c64a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519484"
---
# <a name="whats-new-in-active-directory-federation-services"></a>Active Directory フェデレーション サービス (AD FS) の新機能


## <a name="whats-new-in-active-directory-federation-services-for-windows-server-2019"></a>Windows Server 2019 の Active Directory フェデレーション サービス (AD FS) の新機能

### <a name="protected-logins"></a>保護されたログイン
AD FS 2019 で使用できる保護されたログインの更新の概要を次に示します。
- **プライマリとしての外部認証プロバイダー** - 1 つ目の要素としてパスワードを公開するのではなく、1 つ目の要素としてサード パーティの認証製品を使用できます。 外部認証プロバイダーで 2 つの要素を証明できる場合は、MFA が要求される可能性があります。 
- **追加認証としてのパスワード認証** - パスワードなしのオプションが 1 つ目の要素として使用された後、追加要素にのみパスワードを使用するという、完全にサポートされた受信トレイ オプションを使用できます。 これまではそのままの状態でサポートされている github アダプターをダウンロードする必要がありましたが、これにより、ADFS 2016 のユーザー エクスペリエンスが向上します。 
- **プラグ可能なリスク評価モジュール** - お客様は独自のプラグイン モジュールを作成して、事前認証段階で特定の種類の要求をブロックできるようになりました。 これにより、ID 保護などのクラウド インテリジェンスを使用して、危険なユーザーや危険なトランザクションのログインをブロックしやすくなります。  詳細については、「[AD FS 2019 のリスク評価モデルを使用してプラグインをビルドする](../../ad-fs/development/ad-fs-risk-assessment-model.md)」を参照してください。 
- **ESL の改善** - 次の機能を追加して 2016 の ESL QFE を改善します
    - 監査モード中も、ADFS 2012 R2 以降で使用できる "クラシック" エクストラネット ロックアウト機能で保護することができます。 現在 2016 をご利用の場合、監査モード中は保護されません。 
    - 使い慣れた場所に対して、個別のロックアウトしきい値を有効にします。 これにより、共通のサービス アカウントで実行されているアプリの複数のインスタンスが、最小限の影響でパスワードをロールオーバーできるようになります。 

### <a name="additional-security-improvements"></a>追加のセキュリティ強化
AD FS 2019 では、次の追加のセキュリティ強化を利用できます。
- **スマートカード ログインを使用したリモートの PSH** - スマートカードを使用して PSH 経由で ADFS にリモート接続し、それを使用してマルチノード PSH コマンドレットを含むすべての PSH 機能を管理できます。
- **HTTP ヘッダーのカスタマイズ** - ADFS の応答中に生成された HTTP ヘッダーをカスタマイズできるようになりました。 これには次のヘッダーが含まれます
     - HSTS:これは、準拠するブラウザーが適用する HTTPS エンドポイント上でのみ、ADFS エンドポイントを使用できることを示します
     - x-frame-options:ADFS 管理者は、特定の証明書利用者が ADFS 対話型ログイン ページに iFrame を埋め込むことを許可できます。 これは、HTTPS ホスト上でのみ、注意して使用してください。 
     - 将来的なヘッダー:さらに、将来的なヘッダーも構成できます。 

詳細については、「[AD FS 2019 で HTTP セキュリティ応答ヘッダーをカスタマイズする](../../ad-fs/operations/customize-http-security-headers-ad-fs.md)」を参照してください。 

### <a name="authenticationpolicy-capabilities"></a>認証およびポリシーの機能
AD FS 2019 には、次の認証およびポリシーの機能があります。
- **RP ごとの追加認証に使う認証方法の指定** - 要求ルールを使用して、追加認証プロバイダーに対して呼び出す追加認証プロバイダーを決定できます。 これは 2 つのユース ケースに便利です
    - お客様は、ある追加認証プロバイダーから別の認証プロバイダーに移行しています。 このように、新しい認証プロバイダーにお客様をオンボードし、グループを使用して、どの追加の認証プロバイダーを呼び出すかを制御できます。
    - お客様には、特定のアプリケーション用の特定の追加認証プロバイダー (証明書など) が必要です。 
- **TLS ベースのデバイス認証を必要とするアプリケーションのみに制限する** - クライアントの TLS ベースのデバイス認証を、デバイス ベースの条件付きアクセスを実行するアプリケーションのみに制限できるようになりました。 これにより、TLS ベースのデバイス認証を必要としないアプリケーションのデバイス認証の不要なプロンプトが表示されなくなります (または、クライアント アプリケーションで処理できない場合は失敗します)。
- **MFA の更新間隔のサポート** - AD FS は、2 つ目の要素の資格情報の更新間隔に基づいて、2 つ目の要素の資格情報を再実行する機能をサポートするようになりました。 これにより、お客様は 2 つの要素を使用して最初のトランザクションを実行し、定期的にのみ 2 つ目の要素のプロンプトを表示することができます。 これは、要求で追加のパラメーターを指定できるアプリケーションでのみ使用できます。ADFS で構成可能な設定ではありません。 このパラメーターが Azure AD でサポートされるのは、"MFA を X 日間記憶する" が構成され、Azure AD でフェデレーション ドメインの信頼設定で 'supportsMFA' フラグが true に設定されている場合のみです。 

### <a name="sign-in-sso-improvements"></a>サインイン SSO の機能強化
AD FS 2019 では、次のサインイン SSO の機能強化が行われています。

- [中央のテーマを使用する改ページ調整された UX](../operations/AD-FS-paginated-sign-in.md) - ADFS は、改ページ調整された UX フローに移行し、よりスムーズなサインイン エクスペリエンスを ADFS で検証および提供できるようになりました。 ADFS では、(画面の右側ではなく) 中央の UI が使用されるようになりました。 このエクスペリエンスに合わせて、ロゴと背景画像の更新が必要になる可能性があります。 これは、Azure AD で提供される機能にも反映されます。
- **バグの修正: PRT 認証を行うときの Win10 デバイスの永続的な SSO 状態**   Windows 10 デバイスで PRT 認証を使用するときに MFA 状態が永続化されない問題を修正します。 この問題の結果、エンド ユーザーは 2 つ目の要素の資格情報 (MFA) の入力を頻繁に求められていました。 また、この修正により、デバイス認証がクライアント TLS および PRT メカニズムを介して正常に実行される場合のエクスペリエンスの一貫性も向上します。 


### <a name="suppport-for-building-modern-line-of-business-apps"></a>最新の基幹業務アプリを構築するためのサポート
最新の LOB アプリを構築するための次のサポートが AD FS 2019 に追加されました。

 - **Oauth デバイス フローとプロファイル** - AD FS は、OAuth デバイス フロー プロファイルをサポートし、UI 領域を持たないデバイス上でログインを実行して豊富なログイン エクスペリエンスをサポートするようになりました。 これにより、ユーザーは別のデバイス上でログイン エクスペリエンスを完了できるようになります。 この機能は、Azure Stack での Azure CLI のエクスペリエンスに必要であり、他の場合に使用できます。 
 - **'Resource' パラメーターの削除** - AD FS では、現在の Oauth 仕様に沿ったリソース パラメーターを指定する要件を削除しました。 クライアントでは、要求されたアクセス許可に加えて、スコープ パラメーターとして証明書利用者信頼の識別子を指定できるようになりました。 
 - **AD FS 応答の CORS ヘッダー** - AD FS の OIDC 検出ドキュメントから署名キーを照会することにより、クライアント側の JS ライブラリから id_token の署名を検証できるシングル ページ アプリケーションを構築できるようになりました。 
 - **PKCE のサポート** - AD FS では、OAuth 内でセキュリティで保護された認証コード フローを提供するために、PKCE のサポートを追加します。 これにより、別のクライアントからのコードのハイジャックとリプレイを防止するセキュリティのレイヤーがこのフローに追加されます。 
 - **バグの修正: x5t と kid 要求の送信** - これは軽微なバグ修正です。 AD FS からは、署名を検証するためのキー ID ヒントを示すために、'kid' 要求が追加で送信されます。 以前の AD FS では、'x5t' 要求としてのみこれが送信されていました。

### <a name="supportability-improvements"></a>サポート性の向上
次のサポート性の向上は、AD FS 2019 には含まれていません。
- **AD FS 管理者にエラーの詳細を送信する** - 管理者は、エンド ユーザー認証の失敗に関するデバッグ ログを送信するようにエンド ユーザーを構成し、簡単に使用できるように圧縮ファイルとして保存できます。 管理者は、zip 形式のファイルをトリアージ メール アカウントにメールを自動送信したり、メールに基づいてチケットを自動作成したりするように SMTP 接続を構成することもできます。 

### <a name="deployment-updates"></a>デプロイの更新
AD FS 2019 には、次のデプロイの更新が追加されました。
- **ファーム動作レベル 2019** - AD FS 2016 と同様に、前述の新しい機能を有効にするために必要な新しいファーム動作レベル バージョンがあります。 これにより、以下が可能になります。
    - 2012 R2-> 2019
    - 2016 -> 2019   

### <a name="saml-updates"></a>SAML の更新
次の SAML の更新は AD FS 2019 に含まれています。
- **バグの修正: 集計されたフェデレーションのバグの修正** - 集計されたフェデレーションのサポートに関するバグ修正が多数ありました (例: InCommon)。 以下に関する修正が行われました。 
  - 集計されたフェデレーション メタデータ ドキュメントに含まれる多数のエンティティのスケーリングが向上しました。以前は、"ADMIN0017" エラーが発生するとこれは失敗していました。 
  - Get-AdfsRelyingPartyTrustsGroup PSH コマンドレットを介し、'ScopeGroupID' パラメーターを使用してクエリを実行します。 
  - 重複する entityID に関するエラー条件の処理


### <a name="azure-ad-style-resource-specification-in-scope-parameter"></a>スコープ パラメーターの Azure AD スタイル リソース仕様 
以前は、AD FS では、認証要求の別のパラメーターに目的のリソースとスコープが必要でした。 たとえば、一般的な oauth 要求は次のようになります。7 **https:&#47;&#47;fs.contoso.com/adfs/oauth2/authorize?</br>response_type=code&client_id=claimsxrayclient&resource=urn:microsoft:</br>adfs:claimsxray&scope=oauth&redirect_uri=https:&#47;&#47;adfshelp.microsoft.com/</br> ClaimsXray/TokenResponse&prompt=login**
 
Server 2019 の AD FS では、リソース値をスコープ パラメーターに埋め込んで渡すことができます。 これは Azure AD に対して認証を行う方法と同じです。 

スコープ パラメーターは、各エントリがリソース/スコープとして構成された、スペース区切りのリストとして作成できるようになりました。 

> [!NOTE]
> 認証要求では、1 つのリソースのみを指定できます。 要求に複数のリソースが含まれている場合、AD FS からエラーが返され、認証は失敗します。 

### <a name="proof-key-for-code-exchange-pkce-support-for-oauth"></a>oAuth の Proof Key for Code Exchange (PKCE) のサポート 
認証コードの付与を使用する OAuth パブリック クライアントは、認証コードの傍受攻撃の影響を受けやすくなります。  この攻撃の詳細については、RFC 7636 を参照してください。 この攻撃を軽減するために、Server 2019 の AD FS では、OAuth 認証コード付与フロー用の Proof Key for Code Exchange (PKCE) がサポートされています。 
 
この仕様では、PKCE のサポートを活用するために、OAuth 2.0 認証およびアクセス トークン要求にパラメーターが追加されています。

![Proofkey](media/whats-new-in-active-directory-federation-services-for-windows-server-2016/adfs2019.png)

A. クライアントでは、"code_verifier" という名前のシークレットが作成および記録され、変換されたバージョンの "t(code_verifier)" ("code_challenge" と呼ばれます) が導出されます。これは、OAuth 2.0 承認要求で変換メソッド "t_m" と共に送信されます。 

B. 承認エンドポイントは通常どおり応答しますが、"t(code_verifier)" と変換メソッドが記録されます。 

C. クライアントからは通常どおりアクセス トークン要求で認証コードが送信されますが、(A) で生成された "code_verifier" シークレットが含められます。 

D. AD FS によって "code_verifier" が変換され、(B) の "t(code_verifier)" と比較されます。  同じでない場合、アクセスは拒否されます。 

#### <a name="faq"></a>FAQ 
**Q.** Azure AD に対する要求方法のように、スコープ値の一部としてリソース値を渡すことはできますか? 
</br>**A.** Server 2019 の AD FS では、リソース値をスコープ パラメーターに埋め込んで渡すことができます。 スコープ パラメーターは、各エントリがリソース/スコープとして構成された、スペース区切りのリストとして作成できるようになりました。 例  
**<有効なサンプル要求を作成する>**

**Q.** AD FS では PKCE 拡張機能はサポートされていますか?
</br>**A.** Server 2019 の AD FS では、OAuth 認証コード付与フロー用の Proof Key for Code Exchange (PKCE) がサポートされています 

## <a name="whats-new-in-active-directory-federation-services-for-windows-server-2016"></a>Windows Server 2016 の Active Directory フェデレーション サービス (AD FS) の新機能   
以前のバージョンの AD FS に関する情報を探している場合は、  
 [Windows Server 2012 または 2012 R2 の ADFS](https://technet.microsoft.com/library/hh831502.aspx) と [AD FS 2.0](https://technet.microsoft.com/library/adfs2.aspx) に関する記事を参照してください  

 Active Directory フェデレーション サービス (AD FS) は、Office 365、クラウド ベースの SaaS アプリケーション、社内ネットワーク上のアプリケーションなど、さまざまなアプリケーションにアクセス制御とシングル サインオンを提供します。  
* IT 組織の場合、同じ資格情報とポリシーのセットに基づいて、オンプレミスとクラウドの両方で、最新のアプリケーションとレガシ アプリケーションの両方にサインオンとアクセス制御を提供できます。    
* ユーザーの場合、同じ使い慣れたアカウント資格情報を使用したシームレスなサインオンが提供されます。  
* 開発者の場合、組織のディレクトリに ID が存在するユーザーを簡単に認証できるため、認証や ID ではなく、アプリケーションに集中できます。  

この記事では、Windows Server 2016 (AD FS 2016) の AD FS の新機能について説明します。  

## <a name="eliminate-passwords-from-the-extranet"></a>エクストラネットからパスワードを削除する  
AD FS 2016 では、パスワードなしでサインオンするための 3 つの新しいオプションが有効になりました。これにより、組織はパスワードのフィッシング、漏えい、盗難によるネットワーク侵害のリスクを回避できます。 

### <a name="sign-in-with-azure-multi-factor-authentication"></a>Azure 多要素認証を使用してサインインする
AD FS 2016 は、Windows Server 2012 R2 の AD FS の多要素認証 (MFA) 機能に基づいて構築されており、最初にユーザー名とパスワードを入力することなく、Azure MFA コードのみを使用してサインオンすることができます。

* プライマリ認証方法として Azure MFA を使用している場合、ユーザーは、Azure Authenticator アプリからユーザー名と OTP コードの入力を求められます。  
* Azure MFA をセカンダリまたは追加の認証方法として使用すると、ユーザーが (Windows 統合認証、ユーザー名とパスワード、スマート カード、またはユーザーまたはデバイス証明書を使用する) プライマリ認証資格情報を指定すると、テキスト、音声、または OTP ベースの Azure MFA ログインのプロンプトが表示されます。  
* 新しく組み込まれた Azure MFA アダプターにより、AD FS を使用した Azure MFA の設定と構成がこれまでよりも簡単になりました。
* 組織は、オンプレミスの Azure MFA サーバーを必要とすることなく Azure MFA を利用できます。
* イントラネット用またはエクストラネット用として、またはアクセス制御ポリシーの一部として Azure MFA を構成できます。

Azure MFA と AD FS の詳細を確認してください
*  [AD FS 2016 と Azure MFA を構成する](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configure-ad-fs-and-azure-mfa)  

### <a name="password-less-access-from-compliant-devices"></a>準拠デバイスからのパスワードを使用しないアクセス
AD FS 2016 は、以前のデバイス登録機能に基づいて構築されており、デバイス コンプライアンス状態に基づいたサインオンとアクセス制御を使用できます。 ユーザーはデバイス資格情報を使用してサインオンできます。また、デバイスの属性が変更されたときにコンプライアンスは再評価されるため、常にポリシーが適用されていることを確認できます。  これにより、次のようなポリシーが可能になります

* マネージド デバイスまたは準拠しているデバイスからのアクセスのみを有効にする  
* マネージド デバイスまたは準拠しているデバイスからのエクストラネット アクセスのみを有効にする  
* 管理対象ではないコンピューターまたは準拠していないコンピューターに対して多要素認証を要求する  

AD FS では、ハイブリッド シナリオで条件付きアクセス ポリシーに内部設置型コンポーネントを提供します。 クラウド リソースへの条件付きアクセスのために Azure AD にデバイスを登録すると、そのデバイス ID は AD FS ポリシーにも使用できます。

![新機能](media/whats-new-in-active-directory-federation-services-for-windows-server-2016/ADFS_ITPRO4.png)  

 クラウドでのデバイス ベースの条件付きアクセスの使用の詳細情報   
 *  [Azure Active Directory の条件付きアクセス](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access/)

AD FS でのデバイス ベースの条件付きアクセスの使用の詳細情報
*  [AD FS を使用したデバイス ベースの条件付きアクセスの計画](../../ad-fs/deployment/Plan-Device-based-Conditional-Access-on-Premises.md)  
* [AD FS のアクセス制御ポリシー](../../ad-fs/operations/Access-Control-Policies-in-AD-FS.md)  

### <a name="sign-in-with-windows-hello-for-business"></a>Windows Hello for Business でサインインする  

> [!NOTE]
> 現在、Google Chrome と [Chromium オープン ソース プロジェクト ブラウザーに基づいて構築された新しい Microsoft Edge](https://www.microsoft.com/edge?form=MB110A&OCID=MB110A) は、Microsoft Windows Hello for Business でのブラウザー ベースのシングルサインオン (SSO) ではサポートされていません。 Internet Explorer または以前のバージョンの Microsoft Edge を使用してください。  

Windows 10 デバイスでは、Windows Hello および Windows Hello for Business が導入され、ユーザーのパスワードは、ユーザーのジェスチャー (PIN、指紋などの生体認証ジェスチャー、または顔認識) で保護された強力なデバイスバインド ユーザー資格情報に置き換えられました。 AD FS 2016 は、これらの新しい Windows 10 機能をサポートしているため、ユーザーはパスワードを入力しなくてもイントラネットまたはエクストラネットから AD FS アプリケーションにサインインできます。

組織での Microsoft Windows Hello for Business の使用の詳細情報
*  [組織で Windows Hello for Business を有効にする](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-passport-deployment/)

## <a name="secure-access-to-applications"></a>アプリケーションへのアクセスをセキュリティで保護する

### <a name="modern-authentication"></a>先進認証
AD FS 2016 は、Windows 10 および最新の iOS および Android デバイスとアプリのユーザー エクスペリエンスを向上させる最新の先進プロトコルをサポートしています。  

詳細については、[開発者向けの AD FS シナリオ](../../ad-fs/overview/ad-fs-openid-connect-oauth-flows-scenarios.md)に関する記事を参照してください  


### <a name="configure-access-control-policies-without-having-to-know-claim-rules-language"></a>要求規則言語の知識なしでアクセス制御ポリシーを構成する  
以前は、AD FS 管理者は AD FS の要求規則言語を使用してポリシーを構成する必要があり、ポリシーの構成と保守が困難でした。 アクセス制御ポリシーを使用すると、管理者は組み込みのテンプレートを使用して、次のような一般的なポリシーを適用できます
* イントラネット アクセスのみを許可する
* エクストラネットのすべてのユーザーを許可し、MFA を要求する
* 特定のグループのすべてのユーザーを許可し、MFA を要求する

テンプレートは、ウィザードによるプロセスを使って簡単にカスタマイズし、例外または新しいポリシー規則を追加できます。また、1 つまたは複数のアプリケーションに適用することで、ポリシーを一貫して適用できます。

詳細については、[AD FS でのアクセス制御ポリシー](../../ad-fs/operations/Access-Control-Policies-in-AD-FS.md)に関する記事を参照してください。  

### <a name="enable-sign-on-with-non-ad-ldap-directories"></a>AD 以外の LDAP ディレクトリでのサインオンを有効にする  
多くの組織は、Active Directory とサードパーティのディレクトリを組み合わせています。 LDAP v3 準拠のディレクトリに保存されているユーザーを認証する AD FS のサポートが追加され、AD FS を次の用途に使用できるようになりました。
* サード パーティの LDAP v3 に準拠したディレクトリのユーザー
* Active Directory の双方向の信頼が構成されていない Active Directory フォレスト内のユーザー
* Active Directory ライトウェイト ディレクトリ サービス (AD LDS) のユーザー

詳細については、「[LDAP ディレクトリに保存されたユーザーを認証するように AD FS を構成する](../../ad-fs/operations/Configure-AD-FS-to-authenticate-users-stored-in-LDAP-directories.md)」を参照してください。  

## <a name="better-sign-in-experience"></a>サインイン エクスペリエンスの向上
### <a name="customize-sign-in-experience-for-ad-fs-applications"></a>AD FS アプリケーションのサインイン エクスペリエンスをカスタマイズする  
各アプリケーションのログオン エクスペリエンスをカスタマイズする機能によって使いやすさが大幅に向上するというご意見をお客様からいただいています。特に、複数の異なる企業またはブランドを表すアプリケーションへのサインオンを提供する組織の場合は特にそうです。  

以前の Windows Server 2012 R2 の AD FS では、すべての証明書利用者アプリケーションに共通のサインオン エクスペリエンスを提供し、アプリケーションごとにテキスト ベースのコンテンツのサブセットをカスタマイズする機能を備えていました。 Windows Server 2016 では、メッセージだけでなく、アプリケーションごとに画像、ロゴ、および Web テーマをカスタマイズできます。 さらに、新しいカスタム Web テーマを作成し、証明書利用者ごとに適用することができます。  

詳細については、「[AD FS のユーザー サインインのカスタマイズ](../../ad-fs/operations/AD-FS-user-sign-in-customization.md)」を参照してください。  



## <a name="manageability-and-operational-enhancements"></a>管理の容易性と操作の機能強化  
次のセクションでは、Windows Server 2016 の Active Directory フェデレーション サービス (AD FS) で導入された運用シナリオの改善について説明します。  

### <a name="streamlined-auditing-for-easier-administrative-management"></a>管理を容易にするための効率的な監査  
Windows Server 2012 R2 の AD FS では、1 つの要求に対して多数の監査イベントが生成されていたため、ログインまたはトークン発行アクティビティに関する関連情報が存在しないか (AD FS の一部のバージョンの場合)、複数の監査イベントに分散します。 既定で、AD FS 監査イベントは冗長な性質のために無効になっています。  
AD FS 2016 のリリースにより、監査が効率化され、冗長性が低くなりました。  

詳細については、「[Windows Server 2016 での AD FS の監査機能の強化](../../ad-fs/technical-reference/auditing-enhancements-to-ad-fs-in-windows-server.md)」を参照してください。  

### <a name="improved-interoperability-with-saml-20-for-participation-in-confederations"></a>コンフェデレーションに参加するための SAML 2.0 との相互運用性の改善  
AD FS 2016 には、複数のエンティティを含むメタデータに基づいた信頼のインポートのサポートなど、追加の SAML プロトコルのサポートが含まれています。 これにより、InCommon フェデレーションや、eGov 2.0 標準に準拠する他の実装など、コンフェデレーションに参加するように AD FS を構成できます。  

詳細については、「[SAML 2.0 との相互運用性の向上](../../ad-fs/operations/Improved-interoperability-with-SAML-2.0.md)」を参照してください。  

### <a name="simplified-password-management-for-federated-o365-users"></a>フェデレーション O365 ユーザーのパスワード管理の簡素化  
AD FS で保護されている証明書利用者信頼 (アプリケーション) にパスワードの有効期限要求を送信するように Active Directory フェデレーション サービス (AD FS) を構成することができます。 これらの要求がどのように使用されるかは、アプリケーションによって異なります。 たとえば、証明書利用者として Office 365 を使用している場合、間もなく期限切れになるパスワードをフェデレーション ユーザーに通知できる更新プログラムが Exchange および Outlook に実装されました。  

詳細については、「[パスワードの有効期限クレームを送信するように AD FS を構成する](../../ad-fs/operations/Configure-AD-FS-to-Send-Password-Expiry-Claims.md)」を参照してください。  

### <a name="moving-from-ad-fs-in-windows-server-2012-r2-to-ad-fs-in-windows-server-2016-is-easier"></a>Windows Server 2012 R2 の AD FS から Windows Server 2016 の AD FS への移行が簡単になりました  
以前は、AD FS の新しいバージョンに移行するには、古いファームから構成をエクスポートし、新しい並列ファームにインポートする必要がありました。  

現在は、Windows Server 2012 R2 の AD FS から Windows Server 2016 の AD FS への移行がはるかに簡単になりました。 新しい Windows Server 2016 サーバーを Windows Server 2012 R2 ファームに追加するだけで、ファームは Windows Server 2012 R2 ファーム動作レベルで動作し、外観と動作が Windows Server 2012 R2 ファームのようになります。  

次に、新しい Windows Server 2016 サーバーをファームに追加し、機能を確認し、以前のサーバーをロード バランサーから削除します。 すべてのファーム ノードで Windows Server 2016 が動作したら、ファーム動作レベルを 2016 にアップグレードして、新しい機能を使い始める準備は完了です。  

詳細については、[Windows Server 2016 での AD FS へのアップグレード](../../ad-fs/deployment/Upgrading-to-AD-FS-in-Windows-Server-2016.md)に関する記事を参照してください。  
