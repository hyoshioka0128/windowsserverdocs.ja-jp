---
ms.assetid: aa892a85-f95a-4bf1-acbb-e3c36ef02b0d
title: Windows Server 2016 の Active Directory フェデレーション サービス (AD FS) の新機能
description: ''
author: billmath
ms.author: billmath
manager: daveba
ms.date: 04/23/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: fbb289c16d82da79aded49e3af4134ac7f6df325
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188697"
---
# <a name="whats-new-in-active-directory-federation-services"></a>Active Directory フェデレーション サービス (AD FS) の新機能


## <a name="whats-new-in-active-directory-federation-services-for-windows-server-2019"></a>Active Directory フェデレーション サービスの Windows Server 2019 の新機能新機能

### <a name="protected-logins"></a>保護されたログイン
保護されたログインの AD FS 2019 で使用可能な更新プログラムの簡単な概要を次に示します。
- **プライマリと外部認証プロバイダー** -顧客が最初の要素としてサード パーティの認証製品を使用するようになりましたし、最初の要素としてのパスワードは表示されません。 外部認証プロバイダーが 2 つの要因を証明できる場合は、MFA を要求にできます。 
- **追加の認証としてパスワード認証**-顧客だけ少ないオプション、パスワードの後に、追加の考慮が最初の要素として使用されるパスワードを使用する受信トレイを完全にサポートされているオプションがあります。 これにより、お客様が現状サポートされている github アダプターをダウンロードしなければ ADFS 2016 のカスタマー エクスペリエンスが向上します。 
- **プラグ可能なリスクの評価モジュール**-顧客が事前認証段階中に特定の種類の要求をブロックするモジュールが独自のプラグインを構築できます。 これにより、簡単に Identity protection などのクラウド インテリジェンスを使用して、リスクの高いユーザーやリスクの高いトランザクションのログインをブロックします。  詳細については、次を参照してください[プラグインを AD FS 2019 リスク評価のモデルの構築。](../../ad-fs/development/ad-fs-risk-assessment-model.md) 
- **ESL 改善**-は次の機能を追加することで、2016年で ESL QFE の向上
    - 監査モードでは ADFS 2012R2 以降で使用可能 'クラシック' のエクストラネット ロックアウト機能によって保護されているができます。 現在 2016 顧客がない監査モードで保護します。 
    - 場所の独立したロックアウトのしきい値を有効にします。 これにより、ロール オーバー、最小限の影響では、パスワードに共通のサービス アカウントで実行されているアプリの複数のインスタンス。 

### <a name="additional-security-improvements"></a>追加のセキュリティの機能強化
次の追加のセキュリティ機能強化は AD FS 2019 で使用できます。
- **スマート カードのログインを使用してリモートの PSH** - 顧客が今使用スマートをリモートの PSH 経由で ad FS に接続し、使用して、すべての PSH を管理する機能が複数ノードの PSH コマンドレットを含めます。
- **HTTP ヘッダーのカスタマイズ**-顧客が ADFS の応答中に生成された HTTP ヘッダーをカスタマイズできます。 これにより、次のヘッダーが含まれます。
     - HSTS:ADFS のエンドポイント使用できることのみの準拠しているブラウザーの HTTPS エンドポイントに適用するに伝える
     - x-フレーム オプション:ADFS 管理者は、ADFS の対話型ログイン ページの Iframe を埋め込むには特定の証明書利用者のパーティを許可できます。 これは、HTTPS のホストでのみ、慎重に使用する必要があります。 
     - 将来のヘッダー。追加のヘッダーを今後も構成できます。 

詳細については、次を参照してください[と AD FS 2019 カスタマイズ HTTP セキュリティ応答ヘッダー。](../../ad-fs/operations/customize-http-security-headers-ad-fs.md) 

### <a name="authenticationpolicy-capabilities"></a>認証ポリシー/機能
次の認証/ポリシー機能は、ad FS 2019 を。
- **RP あたり追加の認証用の認証方法を指定**-顧客の追加の認証プロバイダーを起動する追加の認証プロバイダーを決定する規則に要求を使用できます。 これは、2 のユース ケースに便利です。
    - 顧客は別に 1 つ追加の認証プロバイダーから移行します。 新しい認証プロバイダーにユーザーを追加するには、この方法を制御する追加の認証プロバイダーが呼び出されるグループを使用できます。
    - お客様は、特定のアプリケーション固有の追加の認証プロバイダー (例: 証明書) のニーズを持ちます。 
- **TLS ベースのデバイス認証を必要とするアプリケーションにのみ制限**-顧客は、クライアントは TLS ベースのデバイス認証ベースの条件付きアクセスのデバイスを実行するアプリケーションのみを制限できますようになりました。 これには、TLS ベースのデバイス認証を必要としないアプリケーションのデバイスの認証 (または失敗したクライアント アプリケーションで処理できない場合) のすべての不要なプロンプトができないようにします。
- **MFA の鮮度サポート**-AD FS 機能をサポートするようになりましたに 2 番目の要素の資格情報の鮮度に基づく 2 つ目の要素の資格情報を再実行します。 これにより、お客様は 2 つの要因と定期的に第 2 の要素の入力を求めるだけで、最初のトランザクションを実行できます。 これは、要求に追加のパラメーターを指定あり、ADFS で構成可能な設定ではないアプリケーションで使用できるのみです。 このパラメーターが「X 日間、MFA を記憶する」が構成されているし、'supportsMFA' フラグに設定されて、Azure AD によってサポートされている Azure AD でフェデレーション ドメインの信頼設定の場合は true。 

### <a name="sign-in-sso-improvements"></a>SSO の機能強化でサインイン
Ad FS 2019、次でサインイン SSO の機能強化が加えられました。

- [中央のテーマでの UX を改ページ調整された](../operations/AD-FS-paginated-sign-in.md)-ADFS は、検証しより滑らかなサインイン エクスペリエンスを提供する ADFS を使用する改ページ調整された UX フローに移動しましたようになりました。 ADFS は、(画面の右側にある) ではなく中央揃えの UI を使用します。 このエクスペリエンスの連携を新しいロゴと背景のイメージを要求することがあります。 これには、Azure AD で提供される機能もミラー化します。
- **バグの修正:Win10 デバイス PRT 認証を行う場合の SSO の状態を永続的な**これで MFA の状態は保存されていない Windows 10 デバイス用 PRT 認証を使用する場合問題に対処します。 問題の結果は、2 番目の係数資格情報 (MFA) のエンドユーザーを頻繁に求められるはことでした。 修正プログラムも、エクスペリエンスの一貫性のある場合にクライアント TLS および PRT メカニズムを使用して、デバイス認証が正常に実行します。 


### <a name="suppport-for-building-modern-line-of-business-apps"></a>最新の基幹業務アプリを構築するためのによるサポート
AD FS 2019 に最新の LOB アプリを構築するための次のサポートが追加されました。

 - **デバイスの Oauth フロー/プロファイル**-AD FS が豊富なログイン エクスペリエンスをサポートするために、UI サーフェイス領域がないデバイスでのログインを実行するには、OAuth デバイス フロー プロファイルになりました。 これにより、ユーザーが別のデバイスでのログイン エクスペリエンスを完了できます。 この機能は、Azure Stack での Azure CLI エクスペリエンスのために必要なは、それ以外の場合に使用できます。 
 - **'Resource' パラメーターの削除**-AD FS が現在の Oauth 仕様に合わせてリソース パラメーターを指定する必要があるされました。 クライアントできますようになりました証明書利用者信頼の識別子パラメーターとして指定スコープさらに要求されたアクセス許可をします。 
 - **AD FS の応答の CORS ヘッダー** -顧客が AD FS の OIDC 探索ドキュメントからの署名キーを照会して id_token の署名を検証する側の JS ライブラリをクライアントに許可するシングル ページ アプリケーションを構築できますようになりました。 
 - **PKCE のサポート**-AD FS 内での OAuth のセキュリティで保護された認証コード フローを提供する PKCE のサポートを追加します。 このフローをハイジャック コードや別のクライアントから再生することを防ぐために、追加のセキュリティ層が追加されます。 
 - **バグの修正:X5t と子供の要求を送信**-これは、小さなバグ修正。 AD FS さらに送信するように、署名の検証キー id のヒントを示すために 'kid' 要求。 既に AD FS のみ送信されますこの 'x5t' の要求として。

### <a name="supportability-improvements"></a>サポートの機能強化
次のサポートの機能強化は、AD FS 2019 の一部ではないです。
- **エラーの詳細を送信するために AD FS 管理者**-管理者が簡単に使用、zip 形式のフィールドとして格納されるエンドユーザー認証でエラーに関連するデバッグ ログを送信するエンドユーザーを構成することを許可します。 管理者は、automail zip 形式のファイルを自動またはトリアージの電子メール アカウントには、電子メールに基づくチケットを作成する SMTP 接続を構成できます。 

### <a name="deployment-updates"></a>配置の更新
次の展開の更新プログラムは ad FS 2019 含まれるようになりました。
- **ファーム動作レベル 2019** - ad FS 2016 では、上で説明した新しい機能を有効にするために必要な新しいファーム動作レベル バージョン。 これによりから。
    - 2012 R2-> 2019
    - 2016 -> 2019   

### <a name="saml-updates"></a>SAML の更新プログラム
次の SAML の更新プログラムでは、ad FS 2019 です。
- **バグの修正:集計されたフェデレーションでバグを修正**-集計のフェデレーションのサポートに関する多くのバグ修正があった (例: InCommon)。 修正プログラムが、次をされています。 
  - 大規模な集約されたフェデレーション メタデータ ドキュメント内のエンティティ数のスケールが向上します。以前は、これは"ADMIN0017"エラーで失敗します。 
  - Get AdfsRelyingPartyTrustsGroup PSH コマンドレットを使用して 'ScopeGroupID' パラメーターを使用するクエリ。 
  - 重複する entityID 周囲のエラー状態の処理


### <a name="azure-ad-style-resource-specification-in-scope-parameter"></a>スコープのパラメーターでの azure AD のスタイル リソース仕様 
以前は、AD FS には、目的のリソースとの認証要求に個別のパラメーターになるようにスコープが必要です。 たとえば、一般的な oauth 要求は以下ようになります。7 **https:&#47;&#47;fs.contoso.com/adfs/oauth2/authorize?</br>response_type = コード & client_id = claimsxrayclient & リソース = urn: microsoft:</br>adfs:claimsxray & スコープ oauth と redirect_uri を = = https:&#47;&#47;adfshelp.microsoft.com/</br> ClaimsXray/TokenResponse & prompt = login**
 
2019 のサーバーで AD FS、スコープのパラメーターに埋め込まれたリソースの値を渡すことができますようになりました。 これはも Azure AD に対して認証を行ういずれかの方法と一致します。 

スコープのパラメーターは、リソース/スコープとして構造体の各エントリのスペースで区切られた一覧としてここで整理できます。 次に例を示します。  

**< サンプルの有効な要求の作成 >**
> [!NOTE]
> 1 つだけのリソースは、認証要求で指定できます。 要求で 1 つ以上のリソースが含まれる、AD FS は、エラーと認証は成功しませんを返します。 

### <a name="proof-key-for-code-exchange-pkce-support-for-oauth"></a>OAuth サポート コード Exchange (PKCE) の証明キー 
認証コード付与を使用して OAuth パブリック クライアントは承認コードの傍受攻撃を受けやすくなります。  攻撃は RFC 7636 でも説明します。 この攻撃を軽減するために AD FS サーバー 2019年の証明キーをコード Exchange (による PKCE) のサポート OAuth 承認コード付与フロー。 
 
PKCE のサポートを活用するには、この仕様は、OAuth 2.0 承認とアクセス トークン要求に追加のパラメーターを追加します。

![Proofkey](media/whats-new-in-active-directory-federation-services-for-windows-server-2016/adfs2019.png)

A. クライアントは、作成し"code_verifier"という名前のシークレットを記録し、変換後のバージョン"t(code_verifier)"("code_challenge"と呼ばれます) では、OAuth 2.0 承認要求と共に"t_m"変換メソッドに送信された派生します。 

B. 承認エンドポイントは、レコード"t(code_verifier)"と、変換メソッドが通常どおり応答します。 

C. クライアントは、通常どおりアクセス トークンの要求の承認コードを送信しますが、(A) で生成された"code_verifier"シークレットが含まれています。 

D. AD FS では、"code_verifier"を変換し、(B) から"t(code_verifier)"を比較します。  等しくない場合は、アクセスが拒否されました。 

#### <a name="faq"></a>FAQ 
**Q。** Azure AD に対して要求を実行する方法のように、スコープの値の一部としてリソースの値を渡すか。 
</br>**します。** 2019 のサーバーで AD FS、スコープのパラメーターに埋め込まれたリソースの値を渡すことができますようになりました。 スコープのパラメーターは、リソース/スコープとして構造体の各エントリのスペースで区切られた一覧としてここで整理できます。 次に例を示します。  
**< サンプルの有効な要求の作成 >**

**Q。** AD FS は PKCE の拡張機能をサポートしますか。
</br>**します。** AD FS サーバー 2019年の Proof Key for コード Exchange (による PKCE) のサポート OAuth 承認コード付与フロー 

## <a name="whats-new-in-active-directory-federation-services-for-windows-server-2016"></a>Windows Server 2016 の Active Directory フェデレーション サービス (AD FS) の新機能   
AD FS の以前のバージョンに関する情報を探している場合は、次の記事をご覧ください。  
 [Windows Server 2012 または 2012 R2 で ADFS](https://technet.microsoft.com/library/hh831502.aspx)と[AD FS 2.0](https://technet.microsoft.com/library/adfs2.aspx)  

 Active Directory フェデレーション サービスがアクセス制御を提供し、SaaS アプリケーション、および企業ネットワーク上のアプリケーション ベースのさまざまな Office 365、クラウドを含むアプリケーション間でシングル サインオンします。  
* IT 組織のできますでサインインを提供し、アクセス制御を最新と従来の両方のアプリケーションに、クラウド内やオンプレミスの資格情報とポリシーの同じセットに基づいています。    
* ユーザーは、同じでなじみのあるアカウントの資格情報を使用してシームレスなサインインを提供します。  
* 開発者は、id は、アプリケーション、いない認証または id に、作業に取り組めるように組織のディレクトリに live ユーザーを認証する簡単な方法を提供します。  

この記事では、新機能 Windows Server 2016 (AD FS 2016) で AD FS の新機能について説明します。  

## <a name="eliminate-passwords-from-the-extranet"></a>エクストラネットからのパスワードを削除します。  
フィッシング、漏洩したまたは盗まれたパスワードから危険にさらす AD FS 2016 により次の 3 つの新しいオプション ネットワークのリスクを回避するために組織を有効にすると、パスワードを使用せずにサインオンします。 

### <a name="sign-in-with-azure-multi-factor-authentication"></a>Azure multi-factor Authentication を使用してサインイン
AD FS 2016 磨き多要素認証 (MFA) 機能の Windows Server 2012 R2 で AD FS により、ユーザー名とパスワードを最初に入力しなくても、Azure MFA コードのみを使用してサインオンします。

* プライマリ認証方法として、Azure MFA で、ユーザー名と、Azure Authenticator アプリからの OTP コードを求められます。  
* セカンダリまたは追加の認証方法として、Azure MFA、ユーザーは、プライマリ認証が (Windows 統合認証、ユーザー名とパスワード、スマート カード、またはユーザーまたはデバイスの証明書を使用) の資格情報をテキストを入力するプロンプトが表示されます。音声、または OTP は、Azure MFA のログインに基づいています。  
* 新しい組み込みの Azure MFA アダプターを使用した AD FS での Azure MFA のセットアップと構成がこれまで簡単です。
* 組織は、Azure MFA オンプレミス Azure MFA サーバーに必要とせずに利用にかかります。
* イントラネットまたはエクストラネット、またはすべてのアクセス制御ポリシーの一部として、azure MFA を構成することができます。

AD FS での Azure MFA の詳細については
*  [AD FS 2016 と Azure MFA を構成する](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configure-ad-fs-and-azure-mfa)  

### <a name="password-less-access-from-compliant-devices"></a>準拠しているデバイスからのパスワードのないアクセス
AD FS 2016 はサインオンを有効にする前のデバイス登録機能を基盤し、アクセス制御ベースのデバイス コンプライアンスの状態。 ユーザーがデバイスの資格情報を使用してサインオンでき、コンプライアンスが再評価されてデバイスの属性を変更するときにポリシーの適用を常に確認できるようにします。  ポリシーを行うこの

* 管理対象であるか、または準拠しているデバイスからのみアクセスを有効にします。  
* 管理対象であるか、または準拠しているデバイスからのみ、エクストラネット アクセスを有効にします。  
* 管理対象または非準拠ではないコンピューターの多要素認証を要求します。  

AD FS では、ハイブリッド シナリオで条件付きアクセス ポリシーに内部設置型コンポーネントを提供します。 クラウド リソースへの条件付きアクセス用に Azure AD にデバイスを登録するときは、AD FS のポリシーのデバイス id を使用できます。

![新しい機能](media/whats-new-in-active-directory-federation-services-for-windows-server-2016/ADFS_ITPRO4.png)  

 デバイスを使用しての詳細については、クラウドでの条件付きアクセスをベース   
 *  [Azure Active Directory の条件付きアクセス](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access/)

デバイスを使用しての詳細については、AD FS による条件付きアクセスをベース
*  [AD FS による条件付きアクセスをベースのデバイスの計画](../../ad-fs/deployment/Plan-Device-based-Conditional-Access-on-Premises.md)  
* [AD FS でのアクセス制御ポリシー](../../ad-fs/operations/Access-Control-Policies-in-AD-FS.md)  

### <a name="sign-in-with-windows-hello-for-business"></a>Windows こんにちは for Business でサインイン   
Windows 10 デバイスでは、Windows こんにちはと Windows こんにちは for Business、ユーザーのパスワードに置き換えて、ユーザーのジェスチャ (PIN、指紋、顔認識などの生体認証ジェスチャ) によって保護されている強力なデバイス主体ユーザー資格情報を紹介します。 AD FS 2016 では、これらの新しい Windows 10 機能をサポートするため、ユーザーにサインインできる AD FS アプリケーションから、イントラネットまたはエクストラネットのパスワードを入力する必要はありません。

詳細については、Microsoft Windows こんにちは for Business 組織で使用します。
*  [Windows こんにちは for Business の組織で有効化にします。](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-passport-deployment/)

## <a name="secure-access-to-applications"></a>アプリケーションへのアクセスをセキュリティで保護します。

### <a name="modern-authentication"></a>最新の認証
AD FS 2016 では、Windows 10 だけでなく、最新の iOS および Android デバイスとアプリの優れたユーザー エクスペリエンスを提供する最新の最新のプロトコルをサポートします。  

詳細については、次を参照してください[開発者向けの AD FS のシナリオ。](../../ad-fs/overview/AD-FS-Scenarios-for-Developers.md)  


### <a name="configure-access-control-policies-without-having-to-know-claim-rules-language"></a>知らなくてもアクセス制御ポリシーを構成する要求規則言語  
以前は、AD FS 管理者が AD FS の要求規則言語を使用してポリシーを構成する構成し、ポリシーの管理が難しくなります。 アクセス制御ポリシーとに、管理者は、組み込みのテンプレートを使用してなどの一般的なポリシーの適用
* イントラネット アクセスのみを許可します。
* すべてのユーザーを許可し、MFA をエクストラネットからの要求
* すべてのユーザーを許可し、特定のグループから MFA を要求

テンプレートは、簡単に、例外、またはその他のポリシー ルールを追加するプロセスを駆動するウィザードを使用してカスタマイズして、一貫性のあるポリシーの適用の 1 つまたは複数のアプリケーションに適用することができます。

詳細については、次を参照してください。 [AD FS でのアクセス制御ポリシー。](../../ad-fs/operations/Access-Control-Policies-in-AD-FS.md)  

### <a name="enable-sign-on-with-non-ad-ldap-directories"></a>AD 以外の LDAP ディレクトリでのサインインを有効にします。  
多くの組織では、Active Directory とサードパーティ製のディレクトリの組み合わせを保持します。 LDAP v3 に準拠しているディレクトリに格納されているユーザーを認証するための AD FS サポートの追加により、AD FS はこれの使用します。
* サード パーティ、v3 の LDAP 準拠ディレクトリ内のユーザー
* Active Directory 双方向の信頼が構成されていない Active Directory フォレスト内のユーザー
* Active Directory ライトウェイト ディレクトリ サービス (AD LDS) 内のユーザー

詳細については、次を参照してください。 [LDAP ディレクトリに格納されているユーザーの認証に AD FS を構成します。](../../ad-fs/operations/Configure-AD-FS-to-authenticate-users-stored-in-LDAP-directories.md)  

## <a name="better-sign-in-experience"></a>サインイン エクスペリエンス向上
### <a name="customize-sign-in-experience-for-ad-fs-applications"></a>AD FS アプリケーションのサインイン エクスペリエンスをカスタマイズします。  
いることを確認してからアプリケーションごとに、ログオン エクスペリエンスをカスタマイズする機能が複数の異なる会社またはブランドを表すアプリケーションのサインインを提供する組織に対して特に、優れた使いやすさの向上であります。  

以前は、Windows Server 2012 R2 で AD FS は、エクスペリエンスのすべての証明書利用者アプリケーションの一般的な記号を指定、ベース アプリケーションごとのコンテンツのテキストの一部をカスタマイズすることができます。 Windows Server 2016 では、だけでなく、メッセージが、イメージ、1 つのアプリケーションのロゴと web テーマをカスタマイズできます。 また、新しいカスタム web テーマを作成し、これら証明書利用者ごとに適用パーティです。  

詳細については、次を参照してください。 [AD FS のユーザーのサインインにカスタマイズします。](../../ad-fs/operations/AD-FS-user-sign-in-customization.md)  



## <a name="manageability-and-operational-enhancements"></a>管理の容易性と運用の機能強化  
次のセクションでは、Windows Server 2016 での Active Directory フェデレーション サービスで導入された、強化された運用のシナリオについて説明します。  

### <a name="streamlined-auditing-for-easier-administrative-management"></a>監査を容易に管理用の管理を簡素化  
Ad FS を Windows Server 2012 R2 がありますが、1 つの要求と、ログ内の関連情報が生成された多数の監査イベントまたはトークンの発行アクティビティが存在しないか、(でいくつかのバージョンの AD FS) または複数のイベントの監査に分散します。 AD FS の既定で、詳細な性質により、イベントの監査が無効になっています。  
AD FS 2016 のリリースでは、監査は効率となりに少なくなります。  

詳細については、次を参照してください。[の AD FS を Windows Server 2016 の機能強化を監査します。](../../ad-fs/technical-reference/auditing-enhancements-to-ad-fs-in-windows-server.md)  

### <a name="improved-interoperability-with-saml-20-for-participation-in-confederations"></a>Confederations に参加するための SAML 2.0 を使用した相互運用性の向上  
AD FS 2016 では、複数のエンティティが格納されたメタデータに基づく信頼をインポートするためのサポートを含むその他の SAML プロトコルのサポートが含まれています。 これにより、confederations InCommon フェデレーションと eGov 2.0 標準に準拠している他の実装などに参加する AD FS を構成することができます。  

詳細については、次を参照してください。 [SAML 2.0 を使用した相互運用性が向上します。](../../ad-fs/operations/Improved-interoperability-with-SAML-2.0.md)  

### <a name="simplified-password-management-for-federated-o365-users"></a>管理を簡略化されたパスワードが O365 のユーザーをフェデレーション  
AD FS によって保護されている証明書利用者のパーティ信頼 (アプリケーション) には、Active Directory フェデレーション サービス (AD FS) のパスワードの有効期限クレームを送信するを構成できます。 これらの要求を使用する方法は、アプリケーションによって異なります。 たとえば、証明書利用者として Office 365 を更新プログラムが実装されましたがすぐに-する-有効期限切れのパスワードのフェデレーション ユーザーに通知するには、Exchange と Outlook に。  

詳細については、次を参照してください。[パスワードの有効期限クレームを送信する AD FS を構成します。](../../ad-fs/operations/Configure-AD-FS-to-Send-Password-Expiry-Claims.md)  

### <a name="moving-from-ad-fs-in-windows-server-2012-r2-to-ad-fs-in-windows-server-2016-is-easier"></a>Windows Server 2012 R2 で AD FS から Windows Server 2016 での AD FS への移行が簡単  
以前は、AD FS の新しいバージョンに移行すると、以前のファームから構成をエクスポートし、新しいか、並列のファームへのインポートが必要です。  

ここで、Windows Server 2016 での AD FS を Windows Server 2012 R2 で AD FS からの移行ははるかに簡単なりました。 単に、Windows Server 2012 R2 ファームに新しい Windows Server 2016 サーバーを追加し、ファームが、Windows Server 2012 R2 ファーム動作レベルで機能するため、外観し、動作に Windows Server 2012 R2 ファームと同じようにします。  

次に、Windows Server 2016 の新しいサーバーをファームに追加、機能を検証およびロード バランサーから古いサーバーを削除します。 すべてのファーム ノードで Windows Server 2016 を実行するいるとファーム動作レベルを 2016年にアップグレードしての新機能の使用を開始する準備が整いました。  

詳細については、次を参照してください。[の AD FS を Windows Server 2016 にアップグレードします。](../../ad-fs/deployment/Upgrading-to-AD-FS-in-Windows-Server-2016.md)  
