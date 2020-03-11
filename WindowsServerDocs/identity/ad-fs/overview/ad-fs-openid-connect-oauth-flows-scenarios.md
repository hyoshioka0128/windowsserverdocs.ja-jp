---
ms.assetid: 8a64545b-16bd-4c13-a664-cdf4c6ff6ea0
title: AD FS OpenID 接続/OAuth フローとアプリケーション シナリオ
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 875edcf191596d181ec0d70a83f9f3c20f5d5f4a
ms.sourcegitcommit: a6ec589a39ef104ec2be958cd09d2f679816a5ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2020
ms.locfileid: "78261941"
---
# <a name="ad-fs-openid-connectoauth-flows-and-application-scenarios"></a>AD FS OpenID 接続/OAuth フローとアプリケーション シナリオ
AD FS 2016 以降に適用されます


|シナリオ|サンプルを使用したシナリオ チュートリアル|OAuth 2.0 OAuth 2.0 フロー/許可|クライアントの種類|
|-----|-----|-----|-----|
|単一ページのアプリ</br> | &bull; [ADAL を使用したサンプル](../development/Single-Page-Application-with-AD-FS.md)|[暗黙](#implicit-grant-flow)|パブリック| 
|ユーザーのサインインを行う Web アプリ</br> | &bull; [OWIN を使用したサンプル](../development/enabling-openid-connect-with-ad-fs.md)|[認証コード](#authorization-code-grant-flow)|パブリック、機密|  
|ネイティブ アプリが Web API を呼び出す</br>|&bull; [MSAL を使用したサンプル](../development/msal/adfs-msal-native-app-web-api.md)</br>&bull; [ADAL を使用したサンプル](../development/native-client-with-ad-fs.md)|[認証コード](#authorization-code-grant-flow)|パブリック|   
|Web アプリが Web API を呼び出す</br>|&bull; [MSAL を使用したサンプル](../development/msal/adfs-msal-web-app-web-api.md)</br>&bull; [ADAL を使用したサンプル](../development/enabling-oauth-confidential-clients-with-ad-fs.md)|[認証コード](#authorization-code-grant-flow)|機密| 
|Web API がユーザーの代わり (OBO) に別の Web API を呼び出す</br>|&bull; [MSAL を使用したサンプル](../development/msal/adfs-msal-web-api-web-api.md)</br>&bull; [ADAL を使用したサンプル](../development/ad-fs-on-behalf-of-authentication-in-windows-server.md)|[On-behalf-of](#on-behalf-of-flow)|Web アプリが機密として機能します| 
|デーモン アプリが Web API を呼び出す||[クライアント資格情報](#client-credentials-grant-flow)|機密| 
|Web アプリがユーザーの資格情報を使用して Web API を呼び出す||[リソース所有者のパスワード資格情報](#resource-owner-password-credentials-grant-flow-not-recommended)|パブリック、機密| 
|ブラウザレス アプリが Web API を呼び出す||[デバイス コード](#device-code-flow)|パブリック、機密| 

## <a name="implicit-grant-flow"></a>暗黙的な許可のフロー 
 
シングル ページ アプリケーション (AngularJS、Ember.js、React.js など) について、AD FS では OAuth 2.0 の暗黙的な許可のフローをサポートしています。 この暗黙的フローは、 [OAuth 2.0 仕様](https://tools.ietf.org/html/rfc6749#section-4.2)で説明されています。 その主な利点は、バックエンド サーバーとの資格情報の交換を実行しなくても、アプリが AD FS からトークンを取得できることです。 これにより、アプリは、ユーザーのサインイン、セッションの維持、他の Web API へのトークンの取得をすべてクライアント JavaScript コード内で実行できます。 特に [クライアント](https://tools.ietf.org/html/rfc6749#section-10.3)に関して暗黙的フローを使用する場合、検討すべきセキュリティ上の重要な考慮事項がいくつかあります。  
 
暗黙的フローと AD FS を使用して JavaScript アプリに認証を追加する場合は、以下の一般的な手順に従います。  
  
### <a name="protocol-diagram"></a>プロトコルの図

次の図は、暗黙的なサインイン フローの全体像を示しています。この後のセクションで、各手順について詳しく説明します。  

![暗黙的なサインイン](media/adfs-scenarios-for-developers/implicit.png)

### <a name="request-id-token-and-access-token"></a>ID トークンとアクセス トークンを要求する 
 
最初にユーザーをアプリにサインインさせるために、OpenID Connect 認証要求を送信し、AD FS エンドポイントから id_token とアクセス トークンを取得できます。  
 
```
// Line breaks for legibility only 
 
https://adfs.contoso.com/adfs/oauth2/authorize? 
client_id=6731de76-14a6-49ae-97bc-6eba6914391e 
&response_type=id_token+token 
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F 
&scope=openid 
&response_mode=fragment 
&state=12345 
```


|パラメーター|必須/オプション|説明| 
|-----|-----|-----|
|client_id|必須|AD FS がアプリに割り当てたアプリケーション (クライアント) ID。| 
|response_type|必須|OpenID Connect サインインでは  `id_token`  を含める必要があります。 response_type `token` が含まれる場合もあります。 ここでトークンを使用すると、アプリではトークン エンドポイントへ 2 度目の要求を行うことなく、承認エンドポイントからアクセス トークンをすぐに受け取ることができます。| 
|redirect_uri|必須|アプリの redirect_uri。ここでは、認証応答をアプリで送受信できます。 AD FS で構成した redirect_uris のいずれかと正確に一致する必要があります。| 
|nonce|必須|要求に含まれる、アプリによって生成される値。この値は、結果の id_token に要求として含まれます。 アプリはこの値を確認することにより、トークン リプレイ攻撃を緩和できます。 通常、この値はランダム化された一意の文字列であり、要求の送信元を特定する際に使用できます。 Id_token が要求される場合にのみ必須です。|
|scope|オプション|スペースで区切られたスコープのリスト。 OpenID Connect では、スコープ  `openid` を含める必要があります。|
|resource|オプション|Web API の URL。</br>注: MSAL クライアント ライブラリを使用している場合、resource パラメーターは送信されません。 代わりに、リソース URL が、次のようにスコープ パラメーターの一部として送信されます: `scope = [resource url]//[scope values e.g., openid]`</br>リソースがここで渡されない場合やスコープ内にない場合、ADFS は既定のリソース urn:microsoft:userinfo を使用します。 userinfo リソースのポリシー (MFA、発行、承認ポリシーなど) はカスタマイズできません。| 
|response_mode|オプション| 結果として得られたトークンをアプリに送り返す際に使用するメソッドを指定します。 既定値は、`fragment` です。| 
|state|オプション|要求に含まれ、かつトークンの応答でも返される値。 任意のコンテンツの文字列を指定できます。 クロスサイト リクエスト フォージェリ攻撃を防止するために、通常、ランダムに生成された一意の値が使用されます。 この状態は、認証要求が行われる前にアプリ内でユーザーの状態 (表示中のページやビューなど) に関する情報をエンコードする際にも使用されます。| 
|prompt|オプション|必要なユーザー操作の種類を示します。 現時点で有効な値は、login と none だけです。</br>- `prompt=login`  を指定すると、その要求でユーザーに強制的に資格情報を入力させ、シングル サインオンを無効にします。 </br>- `prompt=none`  はその反対であり、ユーザーにどのような対話型プロンプトも表示されないようにします。 シングル サインオンで確認なしで要求を完了できない場合、AD FS から interaction_required エラーが返されます。| 
|login_hint|オプション|ユーザー名が事前にわかっている場合に、これを使用して、ユーザーに代わってサインイン ページのユーザー名/電子メール アドレス フィールドに事前入力できます。 多くの場合、アプリは、`id_token` の  `upn`  要求を使用して前回のサインインからユーザー名を既に抽出した状態で、再認証時にこのパラメーターを使用します。| 
|domain_hint|オプション|これが含まれていると、ユーザーがサインイン ページで実行するドメイン ベースの検出プロセスがスキップされ、多少効率化されたユーザー エクスペリエンスが提供されます。| 

この時点で、ユーザーは資格情報を入力して、認証を完了することを求められます。 ユーザーが認証されると、AD FS 承認エンドポイントは、response_mode パラメーターで指定されたメソッドを使用して、指定された redirect_uri でアプリに応答を返します。  
 
### <a name="successful-response"></a>成功した応答 
 
 `response_mode=fragment and response_type=id_token+token`  を使用した成功した応答は次のようになります。  
 
```
// Line breaks for legibility only 
 
GET https://localhost/myapp/# 
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZEstZnl0aEV... 
&token_type=Bearer 
&expires_in=3599 
&scope=openid  
&id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZstZnl0aEV1Q... 
&state=12345 
```


|パラメーター|説明| 
|-----|-----|
|access_token|response_type に  `token` が含まれている場合に含まれます。|
|token_type|response_type に  `token` が含まれている場合に含まれます。 常に Bearer になります。| 
|expires_in| response_type に  `token` が含まれている場合に含まれます。 キャッシュ用にトークンが有効になっている秒数を示します。| 
|scope| access_token が有効なスコープを示します。|  
|id_token|response_type に  `id_token` が含まれている場合に含まれます。 署名付き JSON Web トークン (JWT)。 アプリは、このトークンのセグメントをデコードして、サインインしたユーザーに関する情報を要求することができます。 アプリはこの値をキャッシュして表示できますが、承認やセキュリティ境界のためにこの値を使用することはできません。| 
|state|要求に state パラメーターが含まれている場合、同じ値が応答にも表示されます。 アプリは、要求と応答の state 値が同じであることを検証します。|

### <a name="refresh-tokens"></a>更新トークン 
暗黙的な許可では、更新トークンは提供されません。  `id_tokens` と  `access_tokens` はどちらも短時間で期限切れになるため、これらのトークンを定期的に更新するようにアプリを準備しておく必要があります。 どちらの種類のトークンを更新する場合も、ID プラットフォームの動作を制御するための  `prompt=none`  パラメーターを使用して、上記と同じ非表示の iframe 要求を実行できます。 `new id_token` を受け取りたい場合は、必ず  `response_type=id_token` を使用してください。 

## <a name="authorization-code-grant-flow"></a>認証コード付与フロー 
 
OAuth 2.0 認証コード付与は、Web API など、保護されているリソースにアクセスできるようにするために Web アプリで使用できます。 OAuth 2.0 認証コード フローについては、 [OAuth 2.0 仕様のセクション 4.1](https://tools.ietf.org/html/rfc6749) で説明されています。 これは、Web アプリやネイティブにインストールされるアプリなど、大半のアプリの種類で認証と承認を行う際に使用されます。 このフローにより、アプリは、AD FS を信頼するリソースにアクセスする際に使用できる access_tokens を安全に取得できます。  
 
### <a name="protocol-diagram"></a>プロトコルの図 
 
大まかに言うと、ネイティブ アプリケーションの認証フローは次のようになります。

![認証コード付与フロー](media/adfs-scenarios-for-developers/authorization.png)

### <a name="request-an-authorization-code"></a>認証コードを要求する 
 
認証コード フローは、クライアントがユーザーを /authorize エンドポイントに移動させることから始まります。 この要求では、クライアントは、ユーザーから取得する必要のあるアクセス許可を示します。 
 
```
// Line breaks for legibility only 
 
https://adfs.contoso.com/adfs/oauth2/authorize? 
client_id=6731de76-14a6-49ae-97bc-6eba6914391e 
&response_type=code 
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F 
&response_mode=query 
&resource=https://webapi.com/ 
&scope=openid 
&state=12345 
```

|パラメーター|必須/オプション|説明|
|-----|-----|-----| 
|client_id|必須|AD FS がアプリに割り当てたアプリケーション (クライアント) ID。|  
|response_type|必須| 認証コード フローのコードを含める必要があります。| 
|redirect_uri|必須|アプリの `redirect_uri`。ここでは、認証応答をアプリで送受信できます。 クライアントの AD FS に登録した redirect_uri のいずれかと完全に一致する必要があります。|  
|resource|オプション|Web API の URL。</br>注: MSAL クライアント ライブラリを使用している場合、resource パラメーターは送信されません。 代わりに、リソース URL が、次のようにスコープ パラメーターの一部として送信されます: `scope = [resource url]//[scope values e.g., openid]`</br>リソースがここで渡されない場合やスコープ内にない場合、ADFS は既定のリソース urn:microsoft:userinfo を使用します。 userinfo リソースのポリシー (MFA、発行、承認ポリシーなど) はカスタマイズできません。| 
|scope|オプション|スペースで区切られたスコープのリスト。|
|response_mode|オプション|結果として得られたトークンをアプリに送り返す際に使用するメソッドを指定します。 次のいずれかを指定できます。 </br>- query </br>- fragment </br>- form_post</br>`query`  は、リダイレクト URI でクエリ文字列パラメーターとしてコードを提供します。 コードを要求する場合は、query、fragment、または form_post を使用できます。 `form_post`  は、リダイレクト URI に対するコードを含む POST を実行します。|
|state|オプション|要求に含まれ、かつトークンの応答でも返される値。 任意のコンテンツの文字列を指定できます。 クロスサイト リクエスト フォージェリ攻撃を防止するために、通常、ランダムに生成された一意の値が使用されます。 この値は、認証要求が行われる前にアプリ内でユーザーの状態 (表示中のページやビューなど) に関する情報をエンコードすることもできます。|
|prompt|オプション|必要なユーザー操作の種類を示します。 現時点で有効な値は、login と none だけです。</br>- `prompt=login`  を指定すると、その要求でユーザーに強制的に資格情報を入力させ、シングル サインオンを無効にします。 </br>- `prompt=none`  はその反対であり、ユーザーにどのような対話型プロンプトも表示されないようにします。 シングル サインオンで確認なしで要求を完了できない場合、AD FS から interaction_required エラーが返されます。|
|login_hint|オプション|ユーザー名が事前にわかっている場合に、これを使用して、ユーザーに代わってサインイン ページのユーザー名/電子メール アドレス フィールドに事前入力できます。 多くの場合、アプリは、`id_token` の  `upn` 要求を使用して前回のサインインからユーザー名を既に抽出した状態で、再認証時にこのパラメーターを使用します。|
|domain_hint|オプション|これが含まれていると、ユーザーがサインイン ページで実行するドメイン ベースの検出プロセスがスキップされ、多少効率化されたユーザー エクスペリエンスが提供されます。|
|code_challenge_method|オプション|code_challenge パラメーターの code_verifier をエンコードするために使用されるメソッド。 値は、次のいずれかです。 </br>- plain </br>- S256 </br>除外されている場合、 `code_challenge`  が含まれていると、code_challenge はプレーンテキストであると見なされます。 AD FS は、plain と S256 の両方をサポートしています。 詳細については、 [PKCE RFC](https://tools.ietf.org/html/rfc7636) を参照してください。|
|code_challenge|オプション| ネイティブ クライアントからの Proof Key for Code Exchange (PKCE) を使用して、認証コード付与をセキュリティ保護するために使用されます。  `code_challenge_method`  が含まれている場合は必須です。 詳細については、 [PKCE RFC](https://tools.ietf.org/html/rfc7636) を参照してください。|

この時点で、ユーザーは資格情報を入力して、認証を完了することを求められます。 ユーザーが認証されると、AD FS は、 `response_mode`  パラメーターで指定されたメソッドを使用して、指定された  `redirect_uri` でアプリに応答を返します。  
 
### <a name="successful-response"></a>成功した応答 
 
response_mode=query を使用した場合の成功応答は次のようになります。 
 
```
GET https://adfs.contoso.com/common/oauth2/nativeclient? 
code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq... 
&state=12345  
```


|パラメーター|説明|
|-----|-----|
|code|アプリが要求した `authorization_code`。 アプリは認証コードを使用して、ターゲット リソースのアクセス トークンを要求できます。 authorization_code は有効期間が短く、通常は約 10 分後に期限切れになります。|
|state|要求に `state` パラメーターが含まれている場合、同じ値が応答にも表示されます。 アプリは、要求と応答の state 値が同じであることを検証します。|

### <a name="request-an-access-token"></a>アクセス トークンを要求する 
 
`authorization_code` を取得し、ユーザーによってアクセス許可が付与されたので、目的のリソースに対して  `access_token`  のコードを使用できます。 これを行うには、以下のように POST 要求を /token エンドポイントに送信します。  
 
```
// Line breaks for legibility only 
 
POST /adfs/oauth2/token HTTP/1.1 
Host: https://adfs.contoso.com/ 
Content-Type: application/x-www-form-urlencoded 
 
client_id=6731de76-14a6-49ae-97bc-6eba6914391e 
&code=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq3n8b2JRLk4OxVXr... 
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F 
&grant_type=authorization_code 
&client_secret=JqQX2PNo9bpM0uEihUPzyrh    // NOTE: Only required for confidential clients (web apps)  
```

|パラメーター|必須/省略可能|説明|
|-----|-----|-----| 
|client_id|必須|AD FS がアプリに割り当てたアプリケーション (クライアント) ID。| 
|grant_type|必須|認証コード フローでは  `authorization_code`  を指定する必要があります。| 
|code|必須|フローの最初の段階で取得した `authorization_code`。| 
|redirect_uri|必須|`authorization_code` を取得するために使用されたものと同じ `redirect_uri` 値。| 
|client_secret|Web アプリの場合は必須|AD FS でアプリの登録時に作成したアプリケーション シークレット。 client_secret はデバイスに確実に保存することはできないため、ネイティブ アプリではアプリケーション シークレットは使用しないでください。 Web アプリや Web API では必須です。これらは、client_secret をサーバー側で安全に保存する機能を備えています。 クライアント シークレットは、送信前に URL エンコードする必要があります。 これらのアプリは、JWT に署名して、client_assertion パラメーターとして追加することによって、キー ベースの認証も使用できます。| 
|code_verifier|オプション|authorization_code を取得するために使用されたのと同じ `code_verifier`。 認証コード付与要求で PKCE が使用された場合は必須です。 詳細については、 [PKCE RFC](https://tools.ietf.org/html/rfc7636) を参照してください。</br>注: AD FS 2019 以降に適用されます| 

### <a name="successful-response"></a>成功した応答 
 
成功したトークン応答は次のようになります。 
 
```
{ 
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...", 
    "token_type": "Bearer", 
    "expires_in": 3599, 
    "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4...", 
    "refresh_token_expires_in": 28800, 
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctOD...", 
} 
```


|パラメーター|説明| 
|-----|-----|
|access_token|要求されたアクセス トークン。 アプリはこのトークンを使用して、保護されたリソース (Web API など) に対して認証できます。| 
|token_type|トークンの種類の値を示します。 AD FS でサポートされる種類は Bearer のみです。
|expires_in|アクセス トークンの有効期間 (秒)。
|refresh_token|OAuth 2.0 更新トークン。 アプリはこのトークンを使用して、現在のアクセス トークンの有効期限が切れた後に追加のアクセス トークンを取得できます。 refresh_token は有効期間が長く、リソースへのアクセスを長時間保持するときに使用できます。| 
|refresh_token_expires_in|更新トークンの有効期間 (秒)。| 
|id_token|JSON Web トークン (JWT)。 アプリは、このトークンのセグメントをデコードして、サインインしたユーザーに関する情報を要求することができます。 アプリはこの値をキャッシュして表示できますが、承認やセキュリティ境界のためにこの値を使用することはできません。|

### <a name="use-the-access-token"></a>アクセス トークンを使用する 
 
```
GET /v1.0/me/messages 
Host: https://webapi.com 
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q... 
 ```

### <a name="refresh-the-access-token"></a>アクセス トークンを更新する 
 
access_token は有効期間が短く、有効期限が切れた後もリソースにアクセスし続けるにはそのトークンを更新する必要があります。 これを行うには、もう一度 POST 要求を  `/token`  エンドポイントに送信します。このとき、コードの代わりに refresh_token を指定します。 更新トークンは、クライアントが既にアクセス トークンを受け取っているすべてのアクセス許可に対して有効です。 
 
更新トークンには、指定された有効期間はありません。 通常、更新トークンの有効期間は比較的長くなります。 ただし、更新トークンが期限切れになったり失効したりする場合や、必要な操作を行うための十分な特権がない場合があります。 アプリケーションでは、トークン発行エンドポイントから返されるエラーを正しく予想して処理する必要があります。  
 
新しいアクセス トークンを取得するために使用されたときに、更新トークンが失効していないにもかかわらず、古い更新トークンを破棄することを求められます。 OAuth 2.0 仕様に、次のように記載されています。"承認サーバーで新しい更新トークンが発行される場合があります。この場合、クライアントは古い更新トークンを破棄し、新しい更新トークンに置き換える必要があります。 承認サーバーは新しい更新トークンをクライアントに発行した後に、古い更新トークンを取り消す場合があります。" 
 
```
// Line breaks for legibility only 
 
POST /adfs/oauth2/token HTTP/1.1 
Host: https://adfs.contoso.com 
Content-Type: application/x-www-form-urlencoded 
 
client_id=6731de76-14a6-49ae-97bc-6eba6914391e 
&refresh_token=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq... 
&grant_type=refresh_token 
&client_secret=JqQX2PNo9bpM0uEihUPzyrh      // NOTE: Only required for confidential clients (web apps)  
```


|パラメーター|必須/オプション|説明| 
|-----|-----|-----|
|client_id|必須|AD FS がアプリに割り当てたアプリケーション (クライアント) ID。| 
|grant_type|必須|この段階の認証コード フローでは  `refresh_token`  を指定する必要があります。| 
|resource|オプション|Web API の URL。</br>注: MSAL クライアント ライブラリを使用している場合、resource パラメーターは送信されません。 代わりに、リソース URL が、次のようにスコープ パラメーターの一部として送信されます: `scope = [resource url]//[scope values e.g., openid]`</br>リソースがここで渡されない場合やスコープ内にない場合、ADFS は既定のリソース urn:microsoft:userinfo を使用します。 userinfo リソースのポリシー (MFA、発行、承認ポリシーなど) はカスタマイズできません。|
|scope|オプション|スペースで区切られたスコープのリスト。| 
|refresh_token|必須|フローの 2 番目の段階で取得した refresh_token。| 
|client_secret|Web アプリの場合は必須| アプリのアプリ登録ポータルで作成したアプリケーション シークレット。 client_secret はデバイスに確実に保存することはできないため、ネイティブ アプリでは使用しないでください。 Web アプリや Web API では必須です。これらは、client_secret をサーバー側で安全に保存する機能を備えています。 これらのアプリは、JWT に署名して、client_assertion パラメーターとして追加することによって、キー ベースの認証も使用できます。|

### <a name="successful-response"></a>成功した応答 
成功したトークン応答は次のようになります。 
 
```
{ 
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...", 
    "token_type": "Bearer", 
    "expires_in": 3599, 
    "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4...", 
    "refresh_token_expires_in": 28800, 
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctOD...", 
}  
```
|パラメーター|説明| 
|-----|-----|
|access_token|要求されたアクセス トークン。 アプリはこのトークンを使用して、Web API など、保護されたリソースに対して認証できます。| 
|token_type|トークンの種類の値を示します。 AD FS でサポートされる種類は Bearer のみです。|
|expires_in|アクセス トークンの有効期間 (秒)。|
|scope|access_token が有効であるスコープ。| 
|refresh_token|OAuth 2.0 更新トークン。 アプリはこのトークンを使用して、現在のアクセス トークンの有効期限が切れた後に追加のアクセス トークンを取得できます。 refresh_token は有効期間が長く、リソースへのアクセスを長時間保持するときに使用できます。| 
|refresh_token_expires_in|更新トークンの有効期間 (秒)。| 
|id_token|JSON Web トークン (JWT)。 アプリは、このトークンのセグメントをデコードして、サインインしたユーザーに関する情報を要求することができます。 アプリはこの値をキャッシュして表示できますが、承認やセキュリティ境界のためにこの値を使用することはできません。|

## <a name="on-behalf-of-flow"></a>On-Behalf-Of フロー 
 
OAuth 2.0 の On-Behalf-Of (OBO) フローは、アプリケーションがサービス/Web API を呼び出し、それがさらに別のサービス/Web API を呼び出す必要のあるユース ケースに対応します。 その目的は、委任されたユーザー ID とアクセス許可を要求チェーンを介して伝達することです。 中間層サービスが認証済み要求をダウンストリーム サービスに対して行うには、AD FS からのアクセス トークンをユーザーに代わってセキュリティ保護する必要があります。  
 
### <a name="protocol-diagram"></a>プロトコルの図 
前述の OAuth 2.0 認証コード付与フローを使用するアプリケーションでユーザーが認証されていることを前提とします。 この時点で、そのアプリケーションには、中間層 Web API (API A) にアクセスするためのユーザーの要求と同意を含む API A のアクセス トークン (トークン A) があります。 クライアントがトークンで user_impersonation スコープを要求していることを確認してください。 ここで、API A はダウンストリーム Web API (API B) に認証済み要求を行う必要があります。 

OBO フローを構成するための以下の手順について、次の図を使用して説明します。 

![On-Behalf-Of フロー](media/adfs-scenarios-for-developers/obo.png)

  1. クライアント アプリケーションは、トークン A を使用して API A に要求を発行します。  
  注: AD FS で OBO フローを構成する際、スコープ `user_impersonation` が選択されていること、およびクライアントが要求で `user_impersonation` スコープを要求していることを確認してください。 
  2. API A が AD FS トークン発行エンドポイントに対して認証を行い、API B にアクセスするためのトークンを要求します。注: AD FS でこのフローを構成する際、API A が、API A のリソース ID と同じ値の clientID を持つサーバー アプリケーションとしても登録されていることを確認してください。
  3. AD FS トークン発行エンドポイントは、トークン A を使用して API A の資格情報を検証し、API B (トークン B) のアクセス トークンを発行します。 
  4. API B への要求の承認ヘッダー内にトークン B が設定されます。 
  5. セキュリティで保護されたリソースからのデータが API B から返されます。 

### <a name="service-to-service-access-token-request"></a>サービス間のアクセス トークン要求 
 
アクセス トークンを要求するには、次のパラメーターを使用して、AD FS トークン エンドポイントへの HTTP POST を実行します。  


### <a name="first-case-access-token-request-with-a-shared-secret"></a>最初のケース: 共有シークレットによるアクセス トークン要求 
 
共有シークレットを使用する場合、サービス間のアクセス トークン要求には、以下のパラメーターが含まれています。 


|パラメーター|必須/オプション|説明|
|-----|-----|-----| 
|grant_type|必須|トークン要求の種類。 JWT を使用した要求では、この値は urn:ietf:params:oauth:grant-type:jwt-bearer にする必要があります。|  
|client_id|必須|最初の Web API をサーバー アプリ (中間層アプリ) として登録するときに構成するクライアント ID。 これは、最初の段階 (最初の Web API の URL) で使用されているリソース ID と同一である必要があります。| 
|client_secret|必須|AD FS でサーバー アプリの登録時に作成したアプリケーション シークレット。| 
|assertion|必須|要求で使用されるトークンの値。|  
|requested_token_use|必須|要求の処理方法を指定します。 OBO フローでは、この値は on_behalf_of に設定する必要があります| 
|resource|必須|最初の Web API をサーバーアプリ (中間層アプリ) として登録するときに指定されたリソース ID。 リソース ID は、中間層アプリがクライアントの代わりに呼び出す 2 番目の Web API の URL である必要があります。|
|scope|オプション|トークン要求のスコープのスペース区切りリスト。| 

#### <a name="example"></a>例 
 
次の `HTTP POST` は、アクセス トークンと更新トークンを要求します 
 
```
//line breaks for legibility only 
 
POST /adfs/oauth2/token HTTP/1.1 
Host: adfs.contoso.com  
Content-Type: application/x-www-form-urlencoded 
 
grant_type=urn:ietf:params:oauth:grant-type:jwt-bearer 
&client_id=https://webapi.com/ 
&client_secret=BYyVnAt56JpLwUcyo47XODd 
&assertion=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIm… 
&resource=https://secondwebapi.com/
&requested_token_use=on_behalf_of
&scope=openid    
```

### <a name="second-case-access-token-request-with-a-certificate"></a>2 番目のケース:証明書を使用したアクセス トークン要求 
 
証明書を使用したサービス間のアクセス トークン要求には、以下のパラメーターが含まれています。 


|パラメーター|必須/オプション|説明|
|-----|-----|-----| 
|grant_type|必須|トークン要求の種類。 JWT を使用した要求では、この値は urn:ietf:params:oauth:grant-type:jwt-bearer にする必要があります。 |
|client_id|必須|最初の Web API をサーバー アプリ (中間層アプリ) として登録するときに構成するクライアント ID。 これは、最初の段階 (最初の Web API の URL) で使用されているリソース ID と同一である必要があります。|  
|client_assertion_type|必須|値は urn:ietf:params:oauth:client-assertion-type:jwt-bearer である必要があります。| 
|client_assertion|必須|作成する必要があるアサーション (JSON Web トークン) です。このアサーションは、アプリケーションの資格情報として登録した証明書で署名する必要があります。|  
|assertion|必須|要求で使用されるトークンの値。| 
|requested_token_use|必須|要求の処理方法を指定します。 OBO フローでは、この値は on_behalf_of に設定する必要があります| 
|resource|必須|最初の Web API をサーバーアプリ (中間層アプリ) として登録するときに指定されたリソース ID。 リソース ID は、中間層アプリがクライアントの代わりに呼び出す 2 番目の Web API の URL である必要があります。|
|scope|オプション|トークン要求のスコープのスペース区切りリスト。|


パラメーターは、共有シークレットによる要求の場合とほぼ同じであることに注意してください。ただし、client_secret パラメーターが client_assertion_type と client_assertion の 2 つのパラメーターに置き換えられる点が異なります。 

#### <a name="example"></a>例 
次の HTTP POST は、証明書を使用して Web API のアクセス トークンを要求します。

``` 
// line breaks for legibility only 
 
POST /adfs/oauth2/token HTTP/1.1 
Host: https://adfs.contoso.com 
Content-Type: application/x-www-form-urlencoded 
 
grant_type=urn%3Aietf%3Aparams%3Aoauth%3Agrant-type%3Ajwt-bearer 
&client_id= https://webapi.com/ 
&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer 
&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNS… 
&resource=https://secondwebapi.com/
&requested_token_use=on_behalf_of
&scope= openid 
```    

### <a name="service-to-service-access-token-response"></a>サービス間のアクセス トークン応答 
 
成功応答は、以下のパラメーターを持つ JSON OAuth 2.0 応答です。 


|パラメーター|説明|
|-----|-----| 
|token_type|トークンの種類の値を示します。 AD FS でサポートされる種類は Bearer のみです。 | 
|scope|トークンで付与されるアクセスのスコープ。| 
|expires_in|アクセス トークンが有効である期間 (秒)。| 
|access_token|要求されたアクセス トークン。 呼び出し元のサービスは、このトークンを使用して受信側のサービスに対する認証を行うことができます。| 
|id_token|JSON Web トークン (JWT)。 アプリは、このトークンのセグメントをデコードして、サインインしたユーザーに関する情報を要求することができます。 アプリはこの値をキャッシュして表示できますが、承認やセキュリティ境界のためにこの値を使用することはできません。| 
|refresh_token|要求されたアクセス トークンの更新トークン。 呼び出し元のサービスは、現在のアクセス トークンの有効期限が切れた後に、このトークンを使用して別のアクセス トークンを要求できます。|
|Refresh_token_expires_in|更新トークンが有効になっている時間の長さ (秒)。 

### <a name="success-response-example"></a>成功応答の例 
 
次の例は、Web API 用のアクセス トークンの要求に対する成功応答を示しています。 

``` 
{ 
  "token_type": "Bearer", 
  "scope": openid, 
  "expires_in": 3269, 
  "access_token": "eyJ0eXAiOiJKV1QiLCJub25jZSI6IkFRQUJBQUFBQUFCbmZpRy1t" 
  "id_token": "aWRfdG9rZW49ZXlKMGVYQWlPaUpLVjFRaUxDSmhiR2NpT2lKU1V6STFOa" 
  "refresh_token": "OAQABAAAAAABnfiG…" 
  "refresh_token_expires_in": 28800, 
} 
```  
 
 
アクセス トークンを使用して、セキュリティ保護されたリソースにアクセスします。これで、中間層サービスは上で取得されたトークンを使用して、そのトークンを Authorization ヘッダーに設定することにより、ダウンストリーム Web API に対して認証済み要求を行うことができます。  

#### <a name="example"></a>例 
``` 
GET /v1.0/me HTTP/1.1 
Host: https://secondwebapi.com 
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJub25jZSI6IkFRQUJBQUFBQUFCbmZpRy1tQ… 
``` 

## <a name="client-credentials-grant-flow"></a>クライアント資格情報の付与フロー 
 
[RFC 6749](https://tools.ietf.org/html/rfc6749#section-4.4) に記述されている OAuth 2.0 クライアント資格情報の付与は、アプリケーションの ID を使用した Web ホスト リソースへのアクセスに使用できます。 通常、この種類の付与は、バックグラウンドでの実行が必要なサーバー間の相互作用に使用され、ユーザーとの即時のやり取りは必要ありません。 この種のアプリケーションは、多くの場合、デーモンまたはサービス アカウントと呼ばれます。 

OAuth 2.0 クライアント資格情報付与フローでは、Web サービス (機密クライアント) が別の Web サービスを呼び出すときに、ユーザーを偽装する代わりに、独自の資格情報を使用して認証することができます。 このシナリオでは、クライアントは通常、中間層の Web サービス、デーモン サービス、または Web サイトです。 より高いレベルの保証を行うために、AD FS では、呼び出し元サービスは資格情報として (共有シークレットではなく) 証明書を使用することもできます。 

### <a name="protocol-diagram"></a>プロトコルの図 

次の図は、クライアント資格情報の付与フローを示しています。 

![クライアント資格情報](media/adfs-scenarios-for-developers/credentials.png)

### <a name="request-a-token"></a>トークンの要求 
 
クライアント資格情報の付与を使用してトークンを取得するには、次のように /token AD FS エンドポイントに `POST` 要求を送信します。  
 
### <a name="first-case-access-token-request-with-a-shared-secret"></a>最初のケース: 共有シークレットによるアクセス トークン要求 
 
```
POST /adfs/oauth2/token HTTP/1.1            
//Line breaks for clarity 
 
Host: https://adfs.contoso.com 
Content-Type: application/x-www-form-urlencoded 
 
client_id=535fb089-9ff3-47b6-9bfb-4f1264799865 
&client_secret=qWgdYAmab0YSkuL1qKv5bPX 
&grant_type=client_credentials 
```

|パラメーター|必須/オプション|説明|
|-----|-----|-----| 
|client_id|必須|AD FS がアプリに割り当てたアプリケーション (クライアント) ID。| 
|scope|オプション|ユーザーに同意するよう求めるスコープのスペース区切りの一覧。| 
|client_secret|必須|アプリ登録ポータルでアプリ用に生成したクライアント シークレット。 クライアント シークレットは、送信前に URL エンコードする必要があります。| 
|grant_type|必須| `client_credentials` に設定する必要があります。|

### <a name="second-case-access-token-request-with-a-certificate"></a>2 番目のケース:証明書を使用したアクセス トークン要求 

``` 
POST /adfs/oauth2/token HTTP/1.1                
 
// Line breaks for clarity 
 
Host: https://adfs.contoso.com 
Content-Type: application/x-www-form-urlencoded 
 
&client_id=97e0a5b7-d745-40b6-94fe-5f77d35c6e05 
&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer 
&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg 
&grant_type=client_credentials  
```

|パラメーター|必須/オプション|説明| 
|-----|-----|-----|
|client_assertion_type|必須|値は urn:ietf:params:oauth:client-assertion-type:jwt-bearer に設定する必要があります。| 
|client_assertion|必須|作成する必要があるアサーション (JSON Web トークン) です。このアサーションは、アプリケーションの資格情報として登録した証明書で署名する必要があります。|  
|grant_type|必須| `client_credentials` に設定する必要があります。|
|client_id|オプション|AD FS がアプリに割り当てたアプリケーション (クライアント) ID。 これは client_assertion の一部であるため、ここで渡す必要はありません。| 
|scope|オプション|ユーザーに同意するよう求めるスコープのスペース区切りの一覧。| 

### <a name="use-a-token"></a>トークンを使用する 
 
トークンを取得したので、そのトークンを使用してリソースへの要求を行います。 トークンの有効期限が切れたときは、/token エンドポイントへの要求を繰り返し、新しいアクセス トークンを取得します。  
 
```
GET /v1.0/me/messages 
Host: https://webapi.com 
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...  
```

## <a name="resource-owner-password-credentials-grant-flow-not-recommended"></a>リソース所有者のパスワード資格情報の付与フロー (推奨されません) 
 
リソース所有者のパスワード資格情報 (ROPC) の付与により、アプリケーションはユーザーのパスワードを直接処理して、ユーザーをサインインさせることができます。 ROPC フローでは、高レベルの信頼性を必要とし、ユーザーがリスクにさらされる可能性が高くなります。このフローは、セキュリティが強化された他のフローを使用できない場合にのみ使用してください。  
 
### <a name="protocol-diagram"></a>プロトコルの図 
 
次の図は、ROPC フローを示しています。

![ROPC フロー](media/adfs-scenarios-for-developers/resource.png)

### <a name="authorization-request"></a>承認要求 
ROPC フローは単一の要求です。クライアント ID とユーザーの資格情報を IDP に送信し、返されたトークンを受信します。 クライアントでは、これを行う前に、ユーザーのメール アドレス (UPN) とパスワードを要求する必要があります。 クライアントでは、要求が成功した直後にユーザーの資格情報を安全な方法でメモリから解放する必要があります。 保存してはなりません。  

```
// Line breaks and spaces are for legibility only. 
 
POST /adfs/oauth2/token HTTP/1.1 
Host: https://adfs.contoso.com  
Content-Type: application/x-www-form-urlencoded 
 
client_id=6731de76-14a6-49ae-97bc-6eba6914391e 
&scope= openid  
&username=myusername@contoso.com 
&password=SuperS3cret 
&grant_type=password 
```


|パラメーター|必須/オプション|説明| 
|-----|-----|-----|
|client_id|必須|クライアント ID| 
|grant_type|必須|パスワードに設定する必要があります。| 
|username|必須|ユーザーの電子メール アドレス。| 
|password|必須|ユーザーのパスワード。| 
|scope|オプション|スペースで区切られたスコープのリスト。|

### <a name="successful-authentication-response"></a>成功した認証応答 
トークンの応答の成功例を次に示します。 

```
{ 
    "token_type": "Bearer", 
    "scope": "openid", 
    "expires_in": 3599, 
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIn...", 
    "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4...", 
    "refresh_token_expires_in": 28800, 
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDR..." 
}  
```


|パラメーター|説明| 
|-----|-----|
|token_type|常に Bearer に設定します。| 
|scope|アクセス トークンが返された場合、このパラメーターによって、アクセス トークンが有効なスコープが一覧表示されます。| 
|expires_in|含まれているアクセス トークンが有効である秒数。| 
|access_token|要求されたスコープに対して発行されます。| 
|id_token|JSON Web トークン (JWT)。 アプリは、このトークンのセグメントをデコードして、サインインしたユーザーに関する情報を要求することができます。 アプリはこの値をキャッシュして表示できますが、承認やセキュリティ境界のためにこの値を使用することはできません。| 
|refresh_token_expires_in|含まれている更新トークンが有効である秒数。| 
|refresh_token|元の scope パラメーターに offline_access が含まれている場合に発行されます。|

更新トークンを使用して、上記の「認証コード付与フロー」セクションで説明しているものと同じフローを使用して、新しいアクセス トークンと更新トークンを取得できます。   

## <a name="device-code-flow"></a>デバイス コード フロー 
 
デバイス コード付与を使用すると、ユーザーは、スマート TV、IoT デバイス、プリンターなどの入力制限のあるデバイスにサインインできます。 このフローを有効にするには、デバイスのユーザーが別のデバイス上のブラウザーで Web ページにアクセスしてサインインします。 ユーザーがサインインすると、デバイスは必要に応じてアクセス トークンと更新トークンを取得できます。 
 
### <a name="protocol-diagram"></a>プロトコルの図 
 
全体的なデバイス コード フローは、次の図のようになります。 それぞれの手順については、この記事で後述します。 
 
![デバイス コード フロー](media/adfs-scenarios-for-developers/device.png)

### <a name="device-authorization-request"></a>デバイス承認要求 
クライアントはまず、認証を開始するために使用されるデバイスとユーザー コードを認証サーバーで確認する必要があります。 クライアントは、この要求を /devicecode エンドポイントから収集します。 クライアントはこの要求内に、ユーザーから取得する必要のあるアクセス許可も含める必要があります。 ユーザーは、この要求が送信された時点から 15 分以内にサインインしなければならないため (expires_in の通常の値)、ユーザーがサインインする準備ができていることが示された場合にのみこの要求を行います。 

```
// Line breaks are for legibility only. 
 
POST https://adfs.contoso.com/adfs/oauth2/devicecode 
Content-Type: application/x-www-form-urlencoded 
 
client_id=6731de76-14a6-49ae-97bc-6eba6914391e 
scope=openid 
```


|パラメーター|条件|説明|
|-----|-----|-----| 
|client_id|必須|AD FS がアプリに割り当てたアプリケーション (クライアント) ID。| 
|scope|オプション|スペースで区切られたスコープのリスト。|

### <a name="device-authorization-response"></a>デバイス承認応答 
成功した応答は、ユーザーがサインインできるようにするために必要な情報が含まれた JSON オブジェクトです。 


|パラメーター|説明|
|-----|-----| 
|device_code|クライアントと承認サーバー間のセッションを検証するために使用される長い文字列。 クライアントはこのパラメーターを使用して、承認サーバーにアクセス トークンを要求します。| 
|user_code|セカンダリ デバイスでセッションを識別するために使用される、ユーザーに表示される短い文字列。| 
|verification_uri|ユーザーがサインインするために user_code を使用してアクセスする必要がある URI。| 
|verification_uri_complete|ユーザーがサインインするために user_code を使用してアクセスする必要がある URI。 ユーザーが user_code を入力しなくて済むように、これには user_code が事前に入力されています。| 
|expires_in|device_code と user_code の有効期限が切れるまでの秒数。| 
|interval|各ポーリング要求間にクライアントが待機する秒数。| 
|メッセージ|ユーザー用の指示が含まれている、人間が判読可能な文字列。 これは、?mkt=xx-XX という形式の要求にクエリ パラメーターを含め、適切な言語カルチャ コードを入力することによってローカライズできます。  

### <a name="authenticating-the-user"></a>ユーザーの認証 
クライアントは、user_code と verification_uri を受け取ると、これらをユーザーに表示して、携帯電話または PC のブラウザーを使ってサインインするよう指示します。 さらに、クライアントは、QR コードまたは同様のメカニズムを使用して verfication_uri_complete を表示できます。これにより、ユーザーの user_code を入力する手順が実行されます。 ユーザーが verification_uri で認証を行っている間、クライアントは device_code を使用して、要求されたトークンを取得するために /token エンドポイントをポーリングする必要があります。 

```
POST https://adfs.contoso.com /adfs/oauth2/token 
Content-Type: application/x-www-form-urlencoded 
 
grant_type: urn:ietf:params:oauth:grant-type:device_code 
client_id: 6731de76-14a6-49ae-97bc-6eba6914391e 
device_code: GMMhmHCXhWEzkobqIHGG_EnNYYsAkukHspeYUk9E8 
```


|パラメーター|必須|説明|
|-----|-----|-----| 
|grant_type|必須|urn:ietf:params:oauth:grant-type:device_code でなければなりません。| 
|client_id|必須|最初の要求で使用された client_id と一致する必要があります。| 
|code|必須|デバイス承認要求で返された device_code。|

### <a name="successful-authentication-response"></a>成功した認証応答 
成功したトークン応答は次のようになります。  


|パラメーター|説明|
|-----|-----| 
|token_type|常に "Bearer" です。| 
|scope|アクセス トークンが返された場合、アクセス トークンが有効なスコープが一覧表示されます。| 
|expires_in|含まれているアクセス トークンが有効になるまでの秒数。| 
|access_token|要求されたスコープに対して発行されます。| 
|id_token|元の scope パラメーターに openid スコープが含まれている場合に発行されます。| 
|refresh_token|元の scope パラメーターに offline_access が含まれている場合に発行されます。| 
|refresh_token_expires_in|含まれている更新トークンが有効になるまでの秒数。| 


## <a name="related-content"></a>関連するコンテンツ  
すべてのチュートリアル記事の一覧については、「[AD FS の開発](../AD-FS-Development.md)」を参照してください。これらの記事では、関連するフローの使用に関するステップバイステップの手順について説明しています。 
