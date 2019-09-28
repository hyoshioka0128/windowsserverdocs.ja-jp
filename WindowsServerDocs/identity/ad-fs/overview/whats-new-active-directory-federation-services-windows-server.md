---
ms.assetid: aa892a85-f95a-4bf1-acbb-e3c36ef02b0d
title: Windows Server 2016 の Active Directory フェデレーション サービス (AD FS) の新機能
description: ''
author: billmath
ms.author: billmath
manager: daveba
ms.date: 04/23/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 6294c7b6ead0a9fa338f8b2cc8134b750f7e3e8f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385550"
---
# <a name="whats-new-in-active-directory-federation-services"></a>Active Directory フェデレーション サービス (AD FS) の新機能


## <a name="whats-new-in-active-directory-federation-services-for-windows-server-2019"></a>Windows Server 2019 の Active Directory フェデレーションサービス (AD FS) の新機能

### <a name="protected-logins"></a>保護されたログイン
AD FS 2019 で使用できる保護されたログインの更新の概要を次に示します。
- **プライマリとしての外部認証プロバイダー** -最初の要素としてサードパーティの認証製品を使用できるようになり、最初の要因としてパスワードを公開しないようになりました。 外部認証プロバイダーが2つの要素を証明できる場合は、MFA を要求できます。 
- **追加の認証としてのパスワード認証**-最初の要素としてパスワードを使用しないオプションが使用された後に、追加の要素に対してのみパスワードを使用するように、完全にサポートされた受信トレイオプションがあります。 これにより、お客様は、としてサポートされている github アダプターをダウンロードする必要がある、ADFS 2016 からのカスタマーエクスペリエンスが向上します。 
- **プラグ可能なリスク評価モジュール**-事前認証段階で、顧客が独自のプラグインモジュールを作成して特定の種類の要求をブロックできるようになりました。 これにより、Identity protection などのクラウドインテリジェンスを使用して、リスクの高いユーザーや危険なトランザクションのログインをブロックすることが簡単になります。  詳細については、「 [AD FS 2019 のリスク評価モデルを使用したプラグインのビルド](../../ad-fs/development/ad-fs-risk-assessment-model.md)」を参照してください。 
- **Esl の改善**-次の機能を追加することにより、2016の ESL QFE を改善します。
    - ユーザーは、ADFS 2012R2 以降で使用可能な "従来の" エクストラネットロックアウト機能によって保護されているときに、監査モードにすることができます。 現在、2016のお客様は、監査モードでは保護されていません。 
    - 使い慣れた場所に対して、個別のロックアウトしきい値を有効にします。 これにより、共通のサービスアカウントで実行されているアプリの複数のインスタンスが、最小限の影響でパスワードをロールオーバーできるようになります。 

### <a name="additional-security-improvements"></a>追加のセキュリティ強化
AD FS 2019 では、次の追加のセキュリティ強化を利用できます。
- **スマートカードログインを使用したリモートの psh** -スマートカードを使用して、psh 経由で ADFS にリモート接続し、複数ノードの psh コマンドレットを使用してすべての psh 関数を管理できるようになりました。
- **Http ヘッダーのカスタマイズ**-ADFS 応答中に生成された http ヘッダーをカスタマイズできるようになりました。 これには次のヘッダーが含まれます。
     - HSTSこれにより、ADFS エンドポイントは、準拠ブラウザーの HTTPS エンドポイントでのみ使用できます。
     - x フレームオプション:Adfs 管理者は、特定の証明書利用者が ADFS 対話型ログインページに Iframe を埋め込むことを許可できます。 これは、HTTPS ホストでのみ使用してください。 
     - 今後のヘッダー:さらに、今後のヘッダーも構成できます。 

詳細については、「 [AD FS 2019 で HTTP セキュリティ応答ヘッダーをカスタマイズ](../../ad-fs/operations/customize-http-security-headers-ad-fs.md)する」を参照してください。 

### <a name="authenticationpolicy-capabilities"></a>認証/ポリシー機能
AD FS 2019 には、次の認証/ポリシー機能があります。
- **RP ごとに追加の認証に認証方法を指定し**ます。お客様は、要求規則を使用して、追加の認証プロバイダーに対して呼び出す追加の認証プロバイダーを決定できるようになりました。 これは2つのユースケースに便利です。
    - お客様は、1つの追加の認証プロバイダーから別の認証プロバイダーに移行しています。 これにより、ユーザーを新しい認証プロバイダーにオンボードすると、グループを使用して、どの追加の認証プロバイダーを呼び出すかを制御できるようになります。
    - お客様は、特定のアプリケーションに対して、特定の追加の認証プロバイダー (証明書など) を必要としています。 
- **Tls ベースのデバイス認証を、it を必要とするアプリケーションのみに制限**する-顧客は、デバイスベースの条件付きアクセスを実行するアプリケーションのみにクライアント tls ベースのデバイス認証を制限できるようになりました。 これにより、TLS ベースのデバイス認証を必要としないアプリケーションに対して、デバイス認証 (クライアントアプリケーションが処理できない場合はエラー) に対する不要なプロンプトが表示されなくなります。
- **MFA 鮮度のサポート**-AD FS は、2番目の要素の資格情報の鮮度に基づいて2要素の資格情報を再実行する機能をサポートするようになりました。 これにより、顧客は2つの要素を持つ初期トランザクションを実行し、定期的に2番目の要素を要求することができます。 これは、要求に追加のパラメーターを提供することができ、ADFS で構成可能な設定ではないアプリケーションにのみ使用できます。 このパラメーターは Azure AD でサポートされています。 [MFA を X 日間記憶する] が構成されていて、Azure AD のフェデレーションドメインの信頼設定で "supportsMFA" フラグが true に設定されている場合です。 

### <a name="sign-in-sso-improvements"></a>サインイン SSO の機能強化
AD FS 2019 では、次のサインイン SSO の機能強化が行われています。

- [中央のテーマを使用する改ページ調整](../operations/AD-FS-paginated-sign-in.md)された ux-adfs は、改ページ調整された ux フローに移行され、adfs はより円滑なサインインエクスペリエンスを提供できるようになりました。 ADFS では、(画面の右側ではなく) 中央の UI が使用されるようになりました。 このエクスペリエンスに合わせて、新しいロゴと背景画像が必要になる場合があります。 これは、Azure AD で提供される機能にも反映されます。
- **Bug fix:Win10 デバイスの永続 SSO 状態: PRT auth @ no__t-0 を実行すると、Windows 10 デバイスに対して PRT 認証を使用しているときに MFA 状態が永続化されていない問題が解決されます。 この問題の原因は、エンドユーザーが2要素資格情報 (MFA) を頻繁に要求することでした。 また、この修正により、デバイス認証がクライアント TLS および PRT 機構を使用して正常に実行されたときに、エクスペリエンスの一貫性も向上します。 


### <a name="suppport-for-building-modern-line-of-business-apps"></a>最新の基幹業務アプリを構築するためのつい
最新の LOB アプリをビルドするための次のサポートが AD FS 2019 に追加されました。

 - **Oauth デバイスフロー/プロファイル**-AD FS では、リッチログインエクスペリエンスをサポートするための UI 領域がないデバイスでのログインを実行するための oauth デバイスフロープロファイルがサポートされるようになりました。 これにより、ユーザーは別のデバイスでログインエクスペリエンスを完了できます。 この機能は、Azure Stack の Azure CLI エクスペリエンスに必要であり、他の場合にも使用できます。 
 - **' Resource ' パラメーター** -AD FS を削除すると、現在の Oauth 仕様に対応したリソースパラメーターを指定する必要がなくなりました。 クライアントは、要求されたアクセス許可に加えて、証明書利用者信頼の識別子をスコープパラメーターとして提供できるようになりました。 
 - **AD FS の応答での CORS ヘッダー** -お客様は、AD FS にある oidc discovery ドキュメントから署名キーを照会することによって、クライアント側 JS ライブラリが id_token の署名を検証できるようになりました。 
 - **Pkce のサポート**-AD FS は、OAuth 内で安全な認証コードフローを提供する pkce サポートを追加します。 これにより、このフローにセキュリティレイヤーが追加され、コードがハイジャックされ、別のクライアントから再生されるのを防ぐことができます。 
 - **Bug fix:Send x5t と kid 要求 @ no__t-0-これは軽微なバグ修正です。 さらに、AD FS は、署名を検証するためのキー id ヒントを示す "kid" 要求を送信します。 以前は AD FS これは ' x5t ' 要求としてのみ送信されていました。

### <a name="supportability-improvements"></a>サポート性の向上
次のサポート性の向上は、AD FS 2019 には含まれていません。
- **AD FS の管理者にエラーの詳細を送信**する-管理者は、エンドユーザー認証の失敗に関連するデバッグログを送信するようにエンドユーザーを構成できます。これにより、使用しやすい zip 形式で保存することができます。 また、管理者は、無人設定の電子メールアカウントに対して zip 形式のファイルを自動で送信するように SMTP 接続を構成したり、電子メールに基づいてチケットを自動作成したりすることもできます。 

### <a name="deployment-updates"></a>展開の更新
AD FS 2019 には、次の展開の更新が含まれるようになりました。
- **ファームの動作レベル 2019** -AD FS 2016 と同様に、上で説明した新しい機能を有効にするために必要な新しいファーム動作レベルバージョンがあります。 これにより、次のことが可能になります。
    - 2012 R2-> 2019
    - 2016-> 2019   

### <a name="saml-updates"></a>SAML 更新
次の SAML 更新は AD FS 2019 にあります。
- **Bug fix:集計されたフェデレーション @ no__t のバグを修正しました-0-集約されたフェデレーションサポートに関するバグ修正が多数ありました (例: Common)。 修正は次のように行われています。 
  - 集計されたフェデレーションメタデータドキュメントに含まれる大規模なエンティティのスケーリングが向上しました。以前は、"ADMIN0017" エラーが発生すると失敗します。 
  - AdfsRelyingPartyTrustsGroup PSH コマンドレットを使用して ' ScopeGroupID ' パラメーターを使用してクエリを実行します。 
  - 重複する entityID に関するエラー状態の処理


### <a name="azure-ad-style-resource-specification-in-scope-parameter"></a>スコープパラメーターの Azure AD スタイルリソース仕様 
以前は、任意の認証要求で、必要なリソースとスコープが個別のパラメーターに含まれて AD FS 必要があります。 たとえば、一般的な oauth 要求は次のようになります。7 **https:&#47;&#47;fs.contoso.com/adfs/oauth2/authorize? </br>response_type = code & client_id = claimsxrayclient & resource = urn: microsoft: </br>adfs: claimsxray & scope = oauth & redirect_uri = https:&#47; &#47;adfshelp.microsoft.com/</br> ClaimsXray/TokenResponse & prompt = ログイン**
 
サーバー2019で AD FS を使用すると、スコープパラメーターに埋め込まれたリソース値を渡すことができます。 これは Azure AD に対して認証を行う方法と同じです。 

スコープパラメーターは、各エントリがリソース/スコープとして構成されるスペース区切りのリストとして構成できるようになりました。 次に例を示します。  

**有効なサンプル要求 > を作成 <**
> [!NOTE]
> 認証要求では、1つのリソースのみを指定できます。 要求に複数のリソースが含まれている場合、AD FS はエラーを返し、認証は失敗します。 

### <a name="proof-key-for-code-exchange-pkce-support-for-oauth"></a>コード交換 (PKCE) の oAuth サポートのための証明キー 
認証コードの付与を使用する OAuth パブリッククライアントは、認証コード傍受攻撃の影響を受けやすくなります。  この攻撃は、RFC 7636 で説明されています。 この攻撃を軽減するために、サーバー2019の AD FS では、OAuth 認証コード付与フロー用のコード交換 (PKCE) の証明キーがサポートされています。 
 
この仕様では、PKCE のサポートを活用するために、OAuth 2.0 認証およびアクセストークン要求に追加のパラメーターが追加されています。

![Proofkey](media/whats-new-in-active-directory-federation-services-for-windows-server-2016/adfs2019.png)

A. クライアントは、"code_verifier" という名前のシークレットを作成して記録し、変換されたバージョン "t (code_verifier)" ("code_challenge" と呼ばれます) を派生します。これは、変換メソッド "t_m" と共に OAuth 2.0 Authorization 要求で送信されます。 

B. 承認エンドポイントは通常どおり応答しますが、"t (code_verifier)" と変換メソッドを記録します。 

C. 次にクライアントは、通常どおりアクセストークン要求で認証コードを送信しますが、(A) で生成された "code_verifier" シークレットを含みます。 

D. AD FS によって "code_verifier" が変換され、(B) から "t (code_verifier)" と比較されます。  同じでない場合、アクセスは拒否されます。 

#### <a name="faq"></a>FAQ 
**Q..** Azure AD に対する要求の実行方法など、スコープの値の一部としてリソース値を渡すことはできますか。 
</br>**ある.** サーバー2019で AD FS を使用すると、スコープパラメーターに埋め込まれたリソース値を渡すことができます。 スコープパラメーターは、各エントリがリソース/スコープとして構成されるスペース区切りのリストとして構成できるようになりました。 次に例を示します。  
**有効なサンプル要求 > を作成 <**

**Q..** PKCE 拡張機能はサポートさ AD FS ますか?
</br>**ある.** サーバー2019の AD FS では、OAuth 認証コード付与フロー用のコード交換 (PKCE) の証明キーがサポートされています 

## <a name="whats-new-in-active-directory-federation-services-for-windows-server-2016"></a>Windows Server 2016 の Active Directory フェデレーション サービス (AD FS) の新機能   
以前のバージョンの AD FS に関する情報を探している場合は、次の記事を参照してください。  
 [Windows Server 2012 または 2012 R2 の ADFS](https://technet.microsoft.com/library/hh831502.aspx)と[AD FS 2.0](https://technet.microsoft.com/library/adfs2.aspx)  

 Active Directory フェデレーションサービス (AD FS) は、Office 365、クラウドベースの SaaS アプリケーション、企業ネットワーク上のアプリケーションなど、さまざまなアプリケーションでアクセス制御とシングルサインオンを提供します。  
* IT 組織では、同じ資格情報とポリシーのセットに基づいて、オンプレミスとクラウドの両方で、最新のアプリケーションとレガシアプリケーションの両方にサインオンとアクセス制御を提供できます。    
* ユーザーは、同じ使い慣れたアカウント資格情報を使用してシームレスなサインオンを提供します。  
* 開発者にとっては、id が組織のディレクトリに存在するユーザーを認証し、認証や id ではなくアプリケーションに専念できるようにするための簡単な方法を提供します。  

この記事では、Windows Server 2016 (AD FS 2016) の AD FS の新機能について説明します。  

## <a name="eliminate-passwords-from-the-extranet"></a>エクストラネットからパスワードを削除する  
AD FS 2016 では、パスワードを使用せずにサインオンするための3つの新しいオプションが有効になるため、組織はフィッシング、漏洩、または盗難されたパスワードからのネットワーク侵害のリスクを回避できます。 

### <a name="sign-in-with-azure-multi-factor-authentication"></a>Azure Multi-factor Authentication でサインインする
AD FS 2016 は、最初にユーザー名とパスワードを入力しなくても、Azure MFA コードのみを使用してサインオンできるようにすることで、Windows Server 2012 R2 の AD FS の multi-factor authentication (MFA) 機能に基づいて構築されます。

* プライマリ認証方法として Azure MFA を使用すると、ユーザー名と Azure Authenticator アプリからの OTP コードを入力するように求められます。  
* Azure MFA をセカンダリまたは追加の認証方法として使用すると、ユーザーはプライマリ認証資格情報を提供します (Windows 統合認証、ユーザー名とパスワード、スマートカード、またはユーザーまたはデバイスの証明書を使用)。次に、テキストの入力を求めるプロンプトが表示されます。音声、または OTP ベースの Azure MFA ログイン。  
* 新しい組み込みの Azure MFA アダプターを使用すると、AD FS を使用した Azure MFA のセットアップと構成がかつてないほど簡単になりました。
* 組織は、オンプレミスの Azure MFA server を必要とせずに Azure MFA を利用できます。
* Azure MFA は、イントラネットまたはエクストラネット用に構成することも、アクセス制御ポリシーの一部として構成することもできます。

Azure MFA の詳細については AD FS を参照してください。
*  [AD FS 2016 と Azure MFA を構成する](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configure-ad-fs-and-azure-mfa)  

### <a name="password-less-access-from-compliant-devices"></a>準拠デバイスからのパスワードを使用しないアクセス
AD FS 2016 は、デバイスの準拠状態に基づいてサインオンとアクセス制御を有効にするために、以前のデバイス登録機能を基盤としています。 ユーザーはデバイスの資格情報を使用してサインオンでき、デバイスの属性が変更されるとコンプライアンスが再評価されるので、ポリシーが強制的に適用されるようにすることができます。  これにより、次のようなポリシーが有効になります。

* 管理されているデバイスまたは準拠しているデバイスからのみアクセスを有効にする  
* 管理されているデバイスまたは準拠しているデバイスからのみエクストラネットアクセスを有効にする  
* 管理されていない、または準拠していないコンピューターに対して多要素認証を要求する  

AD FS では、ハイブリッド シナリオで条件付きアクセス ポリシーに内部設置型コンポーネントを提供します。 クラウドリソースへの条件付きアクセスのために Azure AD にデバイスを登録すると、デバイス id を AD FS ポリシーにも使用できます。

![新しいもの](media/whats-new-in-active-directory-federation-services-for-windows-server-2016/ADFS_ITPRO4.png)  

 クラウドでデバイスベースの条件付きアクセスを使用する方法の詳細については、   
 *  [条件付きアクセスの Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access/)

デバイスベースの条件付きアクセスを AD FS で使用する方法の詳細については、
*  [AD FS を使用したデバイスベースの条件付きアクセスの計画](../../ad-fs/deployment/Plan-Device-based-Conditional-Access-on-Premises.md)  
* [AD FS の Access Control ポリシー](../../ad-fs/operations/Access-Control-Policies-in-AD-FS.md)  

### <a name="sign-in-with-windows-hello-for-business"></a>Windows Hello for Business でサインイン   
Windows 10 デバイスでは、Windows Helloと Windows Hello for Business、ユーザーのパスワードに置き換えて、ユーザーのジェスチャ (PIN、指紋、顔認識などの生体認証ジェスチャ) によって保護されている強力なデバイス主体ユーザー資格情報を紹介します。 AD FS 2016 では、これらの新しい Windows 10 機能がサポートされているため、ユーザーはパスワードを指定しなくても、イントラネットまたはエクストラネットから AD FS アプリケーションにサインインできるようになります。

詳細については、Microsoft Windows Hello for Business 組織で使用します。
*  [Windows Hello for Business の組織で有効化にします。](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-passport-deployment/)

## <a name="secure-access-to-applications"></a>アプリケーションへのアクセスをセキュリティで保護する

### <a name="modern-authentication"></a>先進認証
AD FS 2016 は、最新の iOS および Android デバイスとアプリだけでなく、Windows 10 のユーザーエクスペリエンスを向上させる最新のプロトコルをサポートしています。  

詳細については、「[開発者向けの AD FS シナリオ](../../ad-fs/overview/ad-fs-openid-connect-oauth-flows-scenarios.md)」を参照してください。  


### <a name="configure-access-control-policies-without-having-to-know-claim-rules-language"></a>要求規則言語を知らなくてもアクセス制御ポリシーを構成する  
以前は、AD FS 管理者は、AD FS 要求規則言語を使用してポリシーを構成する必要があり、ポリシーの構成と管理が困難になっていました。 アクセス制御ポリシーを使用すると、管理者は組み込みのテンプレートを使用して、などの一般的なポリシーを適用できます。
* イントラネットアクセスのみを許可する
* すべてのユーザーを許可し、エクストラネットから MFA を要求する
* すべてのユーザーを許可し、特定のグループから MFA を要求する

テンプレートは、ウィザードを使用して例外や追加のポリシー規則を追加することで簡単にカスタマイズでき、ポリシーを一貫して適用するために1つまたは複数のアプリケーションに適用できます。

詳細については[、「AD FS のアクセス制御ポリシー](../../ad-fs/operations/Access-Control-Policies-in-AD-FS.md) 」を参照してください。  

### <a name="enable-sign-on-with-non-ad-ldap-directories"></a>AD 以外の LDAP ディレクトリでのサインオンを有効にする  
多くの組織は、Active Directory とサードパーティのディレクトリを組み合わせています。 LDAP v3 準拠のディレクトリに格納されているユーザーを認証するための AD FS サポートが追加され、AD FS を次の対象に使用できるようになりました。
* サードパーティのユーザー、LDAP v3 に準拠したディレクトリ
* Active Directory 双方向の信頼が構成されていない Active Directory フォレスト内のユーザー
* Active Directory ライトウェイトディレクトリサービスのユーザー (AD LDS)

詳細については、「 [LDAP ディレクトリに格納されたユーザーを認証するための AD FS の構成」を](../../ad-fs/operations/Configure-AD-FS-to-authenticate-users-stored-in-LDAP-directories.md)参照してください。  

## <a name="better-sign-in-experience"></a>サインインエクスペリエンスの向上
### <a name="customize-sign-in-experience-for-ad-fs-applications"></a>AD FS アプリケーションのサインインエクスペリエンスをカスタマイズする  
各アプリケーションのログオンエクスペリエンスをカスタマイズする機能は、特に、複数の異なる企業やブランドを表すアプリケーションのサインオンを提供する組織にとっては、優れたユーザビリティ向上を実現しています。  

以前は、Windows Server 2012 R2 の AD FS では、すべての証明書利用者アプリケーションに共通のサインオンエクスペリエンスが提供され、アプリケーションごとにテキストベースのコンテンツのサブセットをカスタマイズできるようになりました。 Windows Server 2016 では、アプリケーションごとにメッセージだけでなく、画像、ロゴ、web テーマをカスタマイズすることもできます。 また、新しいカスタム web テーマを作成し、証明書利用者ごとに適用することもできます。  

詳細については、「 [AD FS ユーザーサインインのカスタマイズ](../../ad-fs/operations/AD-FS-user-sign-in-customization.md)」を参照してください。  



## <a name="manageability-and-operational-enhancements"></a>管理の容易性と操作の機能強化  
次のセクションでは、Windows Server 2016 の Active Directory フェデレーションサービス (AD FS) で導入された改善された運用シナリオについて説明します。  

### <a name="streamlined-auditing-for-easier-administrative-management"></a>管理を容易にするための効率的な監査  
Windows Server 2012 R2 の AD FS では、1つの要求に対して多数の監査イベントが生成され、ログインまたはトークンの発行アクティビティに関する関連情報が存在しない (一部のバージョンの AD FS) か、複数の監査イベントに分散しています。 既定では、AD FS 監査イベントは、詳細な性質のために無効になっています。  
AD FS 2016 のリリースにより、監査が効率化され、詳細が少なくなりました。  

詳細については、「 [Windows Server 2016 での AD FS の監査の強化](../../ad-fs/technical-reference/auditing-enhancements-to-ad-fs-in-windows-server.md)」を参照してください。  

### <a name="improved-interoperability-with-saml-20-for-participation-in-confederations"></a>SAML 2.0 との相互運用性の向上と confederations への参加  
AD FS 2016 には、複数のエンティティを含むメタデータに基づいて信頼をインポートするためのサポートなど、追加の SAML プロトコルサポートが含まれています。 これにより、InCommon フェデレーションや、eGov 2.0 標準に準拠するその他の実装など、confederations に参加するように AD FS を構成することができます。  

詳細については、「 [SAML 2.0 との相互運用性の向上](../../ad-fs/operations/Improved-interoperability-with-SAML-2.0.md)」を参照してください。  

### <a name="simplified-password-management-for-federated-o365-users"></a>フェデレーション O365 ユーザーのパスワード管理の簡素化  
AD FS によって保護されている証明書利用者信頼 (アプリケーション) にパスワードの有効期限要求を送信するように Active Directory フェデレーションサービス (AD FS) (AD FS) を構成することができます。 これらの要求がどのように使用されるかは、アプリケーションによって異なります。 たとえば、Office 365 を証明書利用者として使用する場合、更新プログラムは、間もなく期限切れになったパスワードをフェデレーションユーザーに通知するために Exchange と Outlook に実装されています。  

詳細については、「[パスワードの有効期限要求を送信するための AD FS の構成」を](../../ad-fs/operations/Configure-AD-FS-to-Send-Password-Expiry-Claims.md)参照してください。  

### <a name="moving-from-ad-fs-in-windows-server-2012-r2-to-ad-fs-in-windows-server-2016-is-easier"></a>Windows server 2012 R2 の AD FS から Windows Server 2016 の AD FS への移行は簡単です。  
以前は、新しいバージョンの AD FS に移行するには、以前のファームから構成をエクスポートし、新しい並列ファームにインポートする必要があります。  

これで、windows server 2012 R2 の AD FS から Windows Server 2016 上の AD FS に移行する作業が非常に簡単になりました。 Windows server 2012 R2 ファームに新しい Windows Server 2016 サーバーを追加するだけで、ファームは windows server 2012 R2 ファームの動作レベルで動作するため、Windows Server の 2012 R2 ファームと同じように動作します。  

次に、新しい Windows Server 2016 サーバーをファームに追加し、機能を確認して、ロードバランサーから古いサーバーを削除します。 すべてのファームノードで Windows Server 2016 が実行されると、ファームの動作レベルを2016にアップグレードし、新しい機能の使用を開始できます。  

詳細については、「 [Windows Server 2016 での AD FS へのアップグレード」を](../../ad-fs/deployment/Upgrading-to-AD-FS-in-Windows-Server-2016.md)参照してください。  
