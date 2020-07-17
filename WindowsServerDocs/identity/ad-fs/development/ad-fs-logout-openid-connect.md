---
title: AD FS での OpenID 接続のシングル ログアウト
author: billmath
ms.author: billmath
manager: femila
ms.date: 11/17/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: fe176af74ebabb5cb56d8aa74d755c4e35ec94a3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857315"
---
#  <a name="single-log-out-for-openid-connect-with-ad-fs"></a>AD FS での OpenID 接続のシングル ログアウト

## <a name="overview"></a>概要
Windows Server 2012 R2 の AD FS での最初の Oauth サポートを基にした AD FS 2016 では、OpenId Connect サインオンのサポートが導入されました。 [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801)では、AD FS 2016 で OpenId connect シナリオでのシングルログアウトがサポートされるようになりました。 この記事では、OpenId Connect シナリオのシングルログアウトの概要について説明し、AD FS で OpenId Connect アプリケーションで使用する方法についてのガイダンスを提供します。


## <a name="discovery-doc"></a>探索ドキュメント
OpenID Connect は、"探索ドキュメント" と呼ばれる JSON ドキュメントを使用して、構成に関する詳細を提供します。  これには、認証、トークン、userinfo、およびパブリックエンドポイントの Uri が含まれます。  探索ドキュメントの例を次に示します。

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



フロントチャネルログアウトのサポートを示すために、次の追加の値が探索ドキュメントで使用できるようになります。

- frontchannel_logout_supported: 値は ' true ' になります
- frontchannel_logout_session_supported: 値は ' true ' になります。
- end_session_endpoint: これは、クライアントがサーバーでログアウトを開始するために使用できる OAuth logout URI です。


## <a name="ad-fs-server-configuration"></a>AD FS サーバーの構成
既定では、AD FS プロパティ EnableOAuthLogout が有効になります。  このプロパティは、クライアントでログアウトを開始するための SID を使用して URL (LogoutURI) を参照するように AD FS サーバーに指示します。 [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801)がインストールされていない場合は、次の PowerShell コマンドを使用できます。

```PowerShell
Set-ADFSProperties -EnableOAuthLogout $true
```

>[!NOTE]
> [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801)をインストールした後、`EnableOAuthLogout` パラメーターは不使用とマークされます。 `EnableOAUthLogout` は常に true になり、ログアウト機能には影響しません。

>[!NOTE]
>frontchannel_logout は[KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801)の vcredist の後で**のみ**サポートされます。

## <a name="client-configuration"></a>クライアント構成
クライアントは、ログインしているユーザーを "ログオフ" する url を実装する必要があります。 管理者は、次の PowerShell コマンドレットを使用して、クライアント構成で LogoutUri を構成できます。 


- `(Add | Set)-AdfsNativeApplication`
- `(Add | Set)-AdfsServerApplication`
- `(Add | Set)-AdfsClient`

```PowerShell
Set-AdfsClient -LogoutUri <url>
```

`LogoutUri` は、ユーザーを "ログオフ" するために AF FS によって使用される url です。 `LogoutUri`を実装するには、クライアントは、アプリケーションでユーザーの認証の状態をクリアする必要があります。たとえば、クライアントは、含まれている認証トークンを削除します。 AD FS は、この URL を参照し、クエリパラメーターとして SID を使用して、ユーザーからログオフするように証明書利用者/アプリケーションに通知します。 

![](media/ad-fs-logout-openid-connect/adfs_single_logout2.png)


1.  **セッション id を持つ oauth トークン**: AD FS id_token トークンの発行時に、oauth トークンにセッション id が含まれます。 これは、ユーザーに対してクリーンアップする関連 SSO cookie を特定するために後で AD FS によって使用されます。
2.  **ユーザー**は、ログに記録された任意のアプリケーションからログアウトを開始できます。 この例のシナリオでは、ユーザーは、[ユーザー] からログアウトを開始します。
3.  **アプリケーションがログアウト要求を AD FS に送信する**: ユーザーがログアウトを開始した後、アプリケーションは GET 要求を AD FS の end_session_endpoint に送信します。 アプリケーションでは、必要に応じて、この要求のパラメーターとして id_token_hint を含めることができます。 Id_token_hint が存在する場合、AD FS はセッション ID と共に使用して、ログアウト後にクライアントがリダイレクトされる必要がある URI を判別します (post_logout_redirect_uri)。  Post_logout_redirect_uri は、RedirectUris パラメーターを使用して AD FS に登録されている有効な uri である必要があります。
4.  AD FS は、ログインしている**クライアントにサインアウトを送信**します。 AD FS は、セッション識別子の値を使用して、ユーザーがログインしている関連クライアントを検索します。 識別されたクライアントは、AD FS に登録されている LogoutUri で要求を送信し、クライアント側でログアウトを開始します。

## <a name="faqs"></a>FAQ
**Q:** 探索ドキュメントに frontchannel_logout_supported と frontchannel_logout_session_supported のパラメーターが表示されません。</br>
**A:** すべての AD FS サーバーに[KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801)がインストールされていることを確認します。 [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801)を使用したサーバー2016でのシングルログアウトを参照してください。

**Q:** 転送済みとしてシングルログアウトを構成しましたが、ユーザーは他のクライアントにログインしたままにします。</br>
**A:** ユーザーがログインしているすべてのクライアントに対して `LogoutUri` が設定されていることを確認します。 また、AD FS は、登録されている `LogoutUri`にサインアップ要求を送信しようとしています。 クライアントは、要求を処理し、アプリケーションからユーザーをサインアウトするアクションを実行するロジックを実装する必要があります。</br>

**Q:** ログアウト後に、クライアントの1つが有効な更新トークンを使用して AD FS に戻った場合、アクセストークン AD FS 発行されますか?</br>
**A:** はい。 登録された `LogoutUri`でサインアウト要求を受信した後、すべての認証済みアイテムを削除するのは、クライアントアプリケーションの役割です。


## <a name="next-steps"></a>次の手順
[AD FS の開発](../../ad-fs/AD-FS-Development.md)  
