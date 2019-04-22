---
title: AD FS での OpenID 接続のシングル ログアウト
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 11/17/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3af10ec139edbc72e75bf80f544ac5b4f1cf9222
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825773"
---
#  <a name="single-log-out-for-openid-connect-with-ad-fs"></a>AD FS での OpenID 接続のシングル ログアウト

## <a name="overview"></a>概要
Windows Server 2012 R2 で AD FS での初期の Oauth サポートに基づき、AD FS 2016 には、OpenId Connect サインオンのサポートが導入されました。 [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801)、AD FS 2016 ようになりましたが OpenId Connect のシナリオでのシングル ログアウトをサポートします。 この記事では、シナリオの OpenId Connect のシングル ログアウトの概要を説明し、AD FS で OpenId Connect のアプリケーションの使用方法に関するガイダンスを示します。


## <a name="discovery-doc"></a>探索ドキュメント
「探索ドキュメント」と呼ばれる JSON ドキュメントを使用して OpenID Connect の構成の詳細を指定します。  これには、認証、トークン、ユーザー情報、およびパブリック エンドポイントの Uri が含まれます。  次は、探索ドキュメントの例です。

```
{
"issuer":"https://fs.fabidentity.com/adfs",
"authorization_endpoint":"https://fs.fabidentity.com/adfs/oauth2/authorize/",
"token_endpoint":"https://fs.fabidentity.com/adfs/oauth2/token/",
"jwks_uri":"https://fs.fabidentity.com/adfs/discovery/keys",
"token_endpoint_auth_methods_supported":["client_secret_post","client_secret_basic","private_key_jwt","windows_client_authentication"],
"response_types_supported":["code","id_token","code id_token","id_token token","code token","code id_token token"],
"response_modes_supported":["query","fragment","form_post"],
"grant_types_supported":["authorization_code","refresh_token","client_credentials","urn:ietf:params:oauth:grant-type:jwt-bearer","implicit","password","srv_challenge"],
"subject_types_supported":["pairwise"],
"scopes_supported":["allatclaims","email","user_impersonation","logon_cert","aza","profile","vpn_cert","winhello_cert","openid"],
"id_token_signing_alg_values_supported":["RS256"],
"token_endpoint_auth_signing_alg_values_supported":["RS256"],
"access_token_issuer":"http://fs.fabidentity.com/adfs/services/trust",
"claims_supported":["aud","iss","iat","exp","auth_time","nonce","at_hash","c_hash","sub","upn","unique_name","pwd_url","pwd_exp","sid"],
"microsoft_multi_refresh_token":true,
"userinfo_endpoint":"https://fs.fabidentity.com/adfs/userinfo",
"capabilities":[],
"end_session_endpoint":"https://fs.fabidentity.com/adfs/oauth2/logout",
"as_access_token_token_binding_supported":true,
"as_refresh_token_token_binding_supported":true,
"resource_access_token_token_binding_supported":true,
"op_id_token_token_binding_supported":true,
"rp_id_token_token_binding_supported":true,
"frontchannel_logout_supported":true,
"frontchannel_logout_session_supported":true
} 
 
```



次の追加の値は前面チャネル ログアウトのサポートを示すための探索ドキュメントで利用できます。

- frontchannel_logout_supported: 値は 'true' になります
- frontchannel_logout_session_supported: 値は 'true' になります。
- end_session_endpoint: これは、OAuth ログアウト URI をサーバー上のログアウトを開始するクライアントで使用できます。


## <a name="ad-fs-server-configuration"></a>AD FS サーバーの構成
既定では、AD FS プロパティ EnableOAuthLogout を有効になります。  このプロパティは、クライアントでログアウトを開始する SID を持つ URL (LogoutURI) を参照する AD FS サーバーを指示します。 ない場合[KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801)インストールの次の PowerShell コマンドを使用することができます。

```PowerShell
Set-ADFSProperties -EnableOAuthLogout $true
```

>[!NOTE]
> `EnableOAuthLogout` パラメーターがある不使用とマークをインストールした後[KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801)します。 `EnableOAUthLogout` 常に true に、影響がないログアウト機能で。

>[!NOTE]
>frontchannel_logout がサポートされている**のみ**のインストール後に[KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801)

## <a name="client-configuration"></a>クライアントの構成
クライアントは、'ログオフ' ログオンしたユーザーで url を実装する必要があります。 管理者は、次の PowerShell コマンドレットを使用して、クライアントの構成で、LogoutUri を構成できます。 


- `(Add | Set)-AdfsNativeApplication`
- `(Add | Set)-AdfsServerApplication`
- `(Add | Set)-AdfsClient`

```PowerShell
Set-AdfsClient -LogoutUri <url>
```

`LogoutUri`は、ユーザーを「ログオフ」AF FS で使用される url です。 実装するため、`LogoutUri`アプリケーション内のユーザーの認証状態をクリアすることを確認するクライアントのニーズがあるなど、認証を削除するトークンします。 AD FS 証明書利用者のシグナリング、クエリのパラメーターとしての SID を持つ、その URL を参照します/アプリケーション、ユーザーをログオフします。 

![](media/ad-fs-logout-openid-connect/adfs_single_logout2.png)


1.  **セッション ID の OAuth トークン**:AD FS には、id_token のトークンの発行時に、OAuth トークンでセッション id が含まれています。 これは使用後で AD FS によってユーザーのクリーンアップする SSO の関連クッキーを識別するためにします。
2.  **ユーザーは、App1 でログアウトを開始します**:。ユーザーがログインしているアプリケーションのいずれかから、ユーザーがログアウトを開始できます。 このシナリオの例では、ユーザーは、App1 からのログアウトを開始します。
3.  **アプリケーションは、AD FS にログアウト要求を送信します**:。ユーザーがログアウトを開始すた後、アプリケーションは、AD FS の end_session_endpoint に GET 要求を送信します。 必要に応じて、アプリケーションは、この要求のパラメーターとして id_token_hint を含めることができます。 Id_token_hint が存在する場合は、AD FS は組み合わせて使用セッション ID を持つ図にする URI をクライアントをリダイレクトするログアウト (post_logout_redirect_uri) 後にします。  Post_logout_redirect_uri RedirectUris パラメーターを使用して AD FS に登録されている有効な uri があります。
4.  **AD FS にログインしているクライアント送信サインアウト**:AD FS では、セッション識別子の値を使用して、ユーザーにログインして関連するクライアントを検索します。 識別されたクライアントは、クライアント側で、ユーザーがログアウトを開始する AD FS に登録されている LogoutUri で要求が送信されます。

## <a name="faqs"></a>よく寄せられる質問
**Q:** 探索ドキュメントで frontchannel_logout_supported と frontchannel_logout_session_supported パラメーターは表示されません。</br>
**A:** いる[KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801)すべての AD FS サーバーにインストールされています。 シングル ログアウト Server 2016 を参照してください[KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801)します。

**Q:**、指示に従ってシングル ログアウトを構成しましたが、ユーザーがそのまま保持記録の他のクライアントで。</br>
**A:** いることを確認`LogoutUri`すべてのクライアント設定は、ユーザーがログインしています。 また、AD FS には、登録済みのサインアウト要求を送信する最良の試行`LogoutUri`します。 クライアントは、要求を処理し、ユーザー アプリケーションからサインアウトするアクションを実行するためのロジックを実装する必要があります。</br>

**Q:** 場合は、ログアウトした後、クライアントのいずれかに戻る有効な更新トークンを使用して AD FS、AD FS はアクセス トークンが発行されますか。</br>
**A:**[はい]。 サインアウト要求を受信した後、認証されたすべての成果物を削除するクライアント アプリケーションの役割は、登録済みで`LogoutUri`します。


## <a name="next-steps"></a>次の手順
[AD FS の開発](../../ad-fs/AD-FS-Development.md)  
