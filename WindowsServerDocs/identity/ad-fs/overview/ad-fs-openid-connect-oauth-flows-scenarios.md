---
ms.assetid: 8a64545b-16bd-4c13-a664-cdf4c6ff6ea0
title: OpenID Connect/OAuth フローとアプリケーションシナリオの AD FS
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: d7ed8f7976116ab245fa730a5a050e7ec46cebea
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70869492"
---
# <a name="ad-fs-openid-connectoauth-flows-and-application-scenarios"></a>OpenID Connect/OAuth フローとアプリケーションシナリオの AD FS
AD FS 2016 以降に適用されます


|シナリオ|サンプルを使用したシナリオのチュートリアル|OAuth 2.0 フロー/許可|クライアントの種類|
|-----|-----|-----|-----|
|シングルページアプリ</br> | &bull;[ADAL を使用したサンプル](../development/Single-Page-Application-with-AD-FS.md)|[順序](#implicit-grant-flow)|パブリック| 
|ユーザーがサインインする Web アプリ</br> | &bull;[OWIN を使用したサンプル](../development/enabling-openid-connect-with-ad-fs.md)|[認証コード](#authorization-code-grant-flow)|パブリック、社外秘|  
|ネイティブアプリ呼び出し Web API</br>|&bull;[MSAL を使用したサンプル](../development/msal/adfs-msal-native-app-web-api.md)</br>&bull;[ADAL を使用したサンプル](../development/native-client-with-ad-fs.md)|[認証コード](#authorization-code-grant-flow)|パブリック|   
|Web アプリが Web API を呼び出します</br>|&bull;[MSAL を使用したサンプル](../development/msal/adfs-msal-web-app-web-api.md)</br>&bull;[ADAL を使用したサンプル](../development/enabling-oauth-confidential-clients-with-ad-fs.md)|[認証コード](#authorization-code-grant-flow)|部外| 
|Web API は、ユーザーの代わりに別の web API を呼び出します (OBO)。</br>|&bull;[MSAL を使用したサンプル](../development/msal/adfs-msal-web-api-web-api.md)</br>&bull;[ADAL を使用したサンプル](../development/ad-fs-on-behalf-of-authentication-in-windows-server.md)|[代理](#on-behalf-of-flow)|Web アプリは社外秘として機能します| 
|デーモンアプリが Web API を呼び出します||[クライアント資格情報](#client-credentials-grant-flow)|部外| 
|Web アプリがユーザーの資格情報を使用して Web API を呼び出す||[リソース所有者のパスワード資格情報](#resource-owner-password-credentials-grant-flow-not-recommended)|パブリック、社外秘| 
|Browserless アプリ呼び出し Web API||[デバイスコード](#device-code-flow)|パブリック、社外秘| 

## <a name="implicit-grant-flow"></a>暗黙的な許可フロー 
 
シングルページアプリケーション (AngularJS、Ember.js、応答など) の場合、AD FS では OAuth 2.0 の暗黙的な許可フローがサポートされます。 暗黙のフローは、 [OAuth 2.0 仕様](https://tools.ietf.org/html/rfc6749#section-4.2)で説明されています。 主な利点は、バックエンドサーバーの資格情報の交換を実行せずに、アプリが AD FS からトークンを取得できるようにすることです。 これにより、アプリケーションは、クライアントの JavaScript コード内で、ユーザーのサインイン、セッションの管理、および他の web Api へのトークンの取得を行うことができます。  [クライアント](https://tools.ietf.org/html/rfc6749#section-10.3)に特化した暗黙のフローを使用する場合は、セキュリティに関する重要な考慮事項がいくつかあります。  
 
暗黙のフローと AD FS を使用して JavaScript アプリに認証を追加する場合は、次の一般的な手順に従います。  
  
### <a name="protocol-diagram"></a>プロトコルダイアグラム

次の図は、暗黙的なサインインフロー全体がどのように表示されるかを示しています。以降のセクションでは、各手順について詳しく説明しています。  

![暗黙的なサインイン](media/adfs-scenarios-for-developers/implicit.png)

### <a name="request-id-token-and-access-token"></a>要求 ID トークンとアクセストークン 
 
最初にユーザーをアプリにサインインさせるには、OpenID Connect 認証要求を送信し、AD FS エンドポイントから id_token とアクセストークンを取得します。  
 
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
|client_id|required|AD FS アプリに割り当てられているアプリケーション (クライアント) ID。| 
|response_type|required|OpenID connect `id_token`サインインにはを含める 必要があります。 Response_type `token`が含まれている場合もあります。 ここでトークンを使用すると、トークンエンドポイントに対して2番目の要求を行うことなく、アプリが承認エンドポイントからすぐにアクセストークンを受信できるようになります。| 
|redirect_uri|required|アプリの redirect_uri。アプリで認証応答を送受信できます。 AD FS で構成した redirect_uris の1つと完全に一致している必要があります。| 
|nonce|required|要求に含まれる、アプリによって生成される値。この値は、結果の id_token に要求として含まれます。 その後、アプリはこの値を検証して、トークン再生攻撃を軽減できます。 通常、この値はランダム化された一意の文字列であり、要求の発生元を識別するために使用できます。 Id_token が要求された場合にのみ必要です。|
|スコープ (scope)|オプション|スペースで区切られたスコープのリスト。 OpenID Connect には、スコープ `openid`が含まれている必要があります。|
|resource|オプション|Web API の url。</br>注: MSAL クライアントライブラリを使用している場合、resource パラメーターは送信されません。 代わりに、リソース url はスコープパラメーターの一部として送信されます。`scope = [resource url]//[scope values e.g., openid]`</br>リソースがここで渡されない場合、またはスコープ内にある場合、ADFS は既定のリソース urn: microsoft: userinfo を使用します。 MFA、発行、承認ポリシーなどの userinfo リソースポリシーはカスタマイズできません。| 
|response_mode|オプション| 生成されたトークンをアプリに返すために使用するメソッドを指定します。 デフォルトは `fragment` です。| 
|state|オプション|要求に含まれる値。トークンの応答でも返されます。 任意のコンテンツの文字列を指定できます。 ランダムに生成された一意の値は、通常、クロスサイト要求偽造攻撃を防止するために使用されます。 また、状態は、認証要求が発生する前にアプリ内でユーザーの状態に関する情報をエンコードするためにも使用されます (ページやビューなど)。| 
|prompt|オプション|必要なユーザー操作の種類を示します。 現時点で有効な値は、login と none だけです。</br>- `prompt=login` では、ユーザーは、シングルサインオンを否定して、その要求に対して資格情報を入力するように強制されます。 </br>- `prompt=none` は反対です。ユーザーには、対話的なプロンプトが表示されないようにします。 シングルサインオンを使用して要求をサイレントモードで完了できない場合、AD FS は interaction_required エラーを返します。| 
|login_hint|オプション|を使用すると、ユーザー名が事前にわかっている場合に、ユーザーのサインインページのユーザー名/電子メールアドレスフィールドに事前に入力できます。 多くの場合、アプリでは再認証時にこのパラメーターが使用され、からの `upn`  `id_token`要求を使用して以前のサインインからユーザー名が既に抽出されています。| 
|domain_hint|オプション|含まれている場合は、サインインページでユーザーが実行するドメインベースの検出プロセスがスキップされ、ユーザーエクスペリエンスが少し簡素化されます。| 

この時点で、ユーザーは資格情報の入力を求められ、認証が完了します。 ユーザーが認証されると、AD FS 承認エンドポイントは、response_mode パラメーターで指定されたメソッドを使用して、指定された redirect_uri でアプリに応答を返します。  
 
### <a name="successful-response"></a>成功した応答 
 
を使用し `response_mode=fragment and response_type=id_token+token` た正常な応答は次のようになります。  
 
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
|access_token|Response_type にが含ま `token`れる場合に含まれます。|
|token_type|Response_type にが含ま `token`れる場合に含まれます。 は常にベアラーです。| 
|expires_in| Response_type にが含ま `token`れる場合に含まれます。 キャッシュのためにトークンが有効である秒数を示します。| 
|スコープ (scope)| Access_token が有効になるスコープを示します。|  
|id_token|Response_type にが含ま `id_token`れる場合に含まれます。 署名された JSON Web トークン (JWT)。 アプリは、このトークンのセグメントをデコードして、サインインしたユーザーに関する情報を要求することができます。 アプリは値をキャッシュして表示できますが、承認やセキュリティの境界に依存することはできません。| 
|state|状態パラメーターが要求に含まれている場合、同じ値が応答に表示されます。 アプリでは、要求と応答の状態値が同一であることを確認する必要があります。|

### <a name="refresh-tokens"></a>トークンの更新 
暗黙的な許可は、更新トークンを提供しません。  `id_tokens` と `access_tokens`はどちらも短時間で期限切れになるため、アプリはこれらのトークンを定期的に更新するように準備する必要があります。 どちらの種類のトークンを更新する場合でも、 `prompt=none` パラメーターを使用して、上記と同じ非表示の iframe 要求を実行して、id プラットフォームの動作を制御することができます。 を受信`new id_token`する場合は、必ずを使用 `response_type=id_token`してください。 

## <a name="authorization-code-grant-flow"></a>認証コード付与フロー 
 
Web アプリで OAuth 2.0 認証コード付与を使用して、web Api などの保護されたリソースにアクセスできます。 OAuth 2.0 認証コードフローは、 [oauth 2.0 仕様のセクション 4.1](https://tools.ietf.org/html/rfc6749)で説明されています。 Web アプリやネイティブにインストールされているアプリなど、大部分のアプリの種類で認証と承認を実行するために使用されます。 このフローにより、アプリケーションは、AD FS を信頼するリソースにアクセスするために使用できる access_tokens を安全に取得できます。  
 
### <a name="protocol-diagram"></a>プロトコルダイアグラム 
 
大まかに言えば、ネイティブアプリケーションの認証フローは次のようになります。

![認証コード付与フロー](media/adfs-scenarios-for-developers/authorization.png)

### <a name="request-an-authorization-code"></a>認証コードを要求する 
 
承認コードフローは、ユーザーを承認エンドポイントに誘導するクライアントから始まります。 この要求では、クライアントは、ユーザーから取得する必要のあるアクセス許可を示します。 
 
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
|client_id|required|AD FS アプリに割り当てられているアプリケーション (クライアント) ID。|  
|response_type|required| 承認コードフローのコードを含める必要があります。| 
|redirect_uri|required|アプリ`redirect_uri`の。アプリで認証応答を送受信することができます。 クライアントの AD FS に登録した redirect_uris の1つと完全に一致している必要があります。|  
|resource|オプション|Web API の url。</br>注: MSAL クライアントライブラリを使用している場合、resource パラメーターは送信されません。 代わりに、リソース url はスコープパラメーターの一部として送信されます。`scope = [resource url]//[scope values e.g., openid]`</br>リソースがここで渡されない場合、またはスコープ内にある場合、ADFS は既定のリソース urn: microsoft: userinfo を使用します。 MFA、発行、承認ポリシーなどの userinfo リソースポリシーはカスタマイズできません。| 
|スコープ (scope)|オプション|スペースで区切られたスコープのリスト。|
|response_mode|オプション|生成されたトークンをアプリに返すために使用するメソッドを指定します。 次のいずれかになります。 </br>-クエリ </br>-fragment </br>- form_post</br>`query` コードをリダイレクト URI のクエリ文字列パラメーターとして提供します。 コードを要求している場合は、query、fragment、または form_post を使用できます。 `form_post`コードを含む投稿をリダイレクトURIに対し て実行します。|
|state|オプション|要求に含まれる値。トークンの応答でも返されます。 任意のコンテンツの文字列を指定できます。 ランダムに生成された一意の値は、通常、クロスサイト要求偽造攻撃を防止するために使用されます。 この値は、認証要求が発生する前にアプリ内でユーザーの状態に関する情報をエンコードすることもできます (ページやビューなど)。|
|prompt|オプション|必要なユーザー操作の種類を示します。 現時点で有効な値は、login と none だけです。</br>- `prompt=login` では、ユーザーは、シングルサインオンを否定して、その要求に対して資格情報を入力するように強制されます。 </br>- `prompt=none` は反対です。ユーザーには、対話的なプロンプトが表示されないようにします。 シングルサインオンを使用して要求をサイレントモードで完了できない場合、AD FS は interaction_required エラーを返します。|
|login_hint|オプション|を使用すると、ユーザー名が事前にわかっている場合に、ユーザーのサインインページのユーザー名/電子メールアドレスフィールドに事前に入力できます。 多くの場合、アプリでは再認証時にこのパラメーターが使用され、からの `upn` `id_token`要求を使用して以前のサインインからユーザー名が既に抽出されています。|
|domain_hint|オプション|含まれている場合は、サインインページでユーザーが実行するドメインベースの検出プロセスがスキップされ、ユーザーエクスペリエンスが少し簡素化されます。|
|code_challenge_method|オプション|Code_challenge パラメーターの code_verifier をエンコードするために使用されるメソッド。 次の値のいずれかです。 </br>-plain </br>- S256 </br>除外されている場合、code_challenge は、 `code_challenge`が含まれている場合 はプレーンテキストと見なされます。 AD FS は、plain と S256 の両方をサポートしています。 詳細については、「 [Pkce RFC](https://tools.ietf.org/html/rfc7636)」を参照してください。|
|code_challenge|オプション| ネイティブクライアントからのコード交換 (PKCE) の証明キーを使用して承認コードの付与をセキュリティで保護するために使用されます。 が含ま `code_challenge_method`れている場合 は必須です。 詳細については、「 [Pkce RFC](https://tools.ietf.org/html/rfc7636) 」を参照してください。|

この時点で、ユーザーは資格情報の入力を求められ、認証が完了します。 ユーザーが認証されると、AD FS は、 `redirect_uri` パラメーター `response_mode`に指定されたメソッドを使用して、指定されたでアプリに応答を返します。  
 
### <a name="successful-response"></a>成功した応答 
 
Response_mode = query を使用した正常な応答は次のようになります。 
 
```
GET https://adfs.contoso.com/common/oauth2/nativeclient? 
code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq... 
&state=12345  
```


|パラメーター|説明|
|-----|-----|
|code|`authorization_code`アプリが要求した。 アプリは承認コードを使用して、ターゲットリソースのアクセストークンを要求できます。 Authorization_codes は有効期間が短いため、通常は約10分後に期限切れになります。|
|state|要求に`state`パラメーターが含まれている場合は、同じ値が応答に表示されます。 アプリでは、要求と応答の状態値が同一であることを確認する必要があります。|

### <a name="request-an-access-token"></a>アクセストークンを要求する 
 
を取得`authorization_code`し、ユーザーによるアクセス許可が付与されたので、 `access_token` のコードを目的のリソースに利用できます。 これを行うには、/トークンエンドポイントに POST 要求を送信します。  
 
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
|client_id|required|AD FS アプリに割り当てられているアプリケーション (クライアント) ID。| 
|grant_type|required|承認コード `authorization_code`フローの場合は、で ある必要があります。| 
|code|required|`authorization_code`フローの最初の区間で取得した。| 
|redirect_uri|required|`redirect_uri` を`authorization_code`取得するために使用したものと同じ値。| 
|client_secret|web アプリに必要|AD FS でのアプリの登録時に作成したアプリケーションシークレット。 デバイスに client_secrets を確実に格納することはできないため、ネイティブアプリではアプリケーションシークレットを使用しないでください。 これは web apps と web Api に必要であり、client_secret をサーバー側に安全に格納する機能を備えています。 クライアントシークレットは、送信する前に URL エンコードする必要があります。 これらのアプリでは、JWT に署名し、それを client_assertion パラメーターとして追加することで、キーベースの認証を使用することもできます。| 
|code_verifier|オプション|Authorization_code を`code_verifier`取得するために使用されたものと同じです。 認証コード付与要求で PKCE が使用されている場合は必須です。 詳細については、「 [Pkce RFC](https://tools.ietf.org/html/rfc7636)」を参照してください。</br>注– AD FS 2019 以降に適用されます。| 

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
|access_token|要求されたアクセストークン。 アプリは、このトークンを使用して、セキュリティで保護されたリソース (Web API) に対する認証を行うことができます。| 
|token_type|トークンの種類の値を示します。 AD FS がサポートする型はベアラーだけです。
|expires_in|アクセストークンの有効期間 (秒単位)。
|refresh_token|OAuth 2.0 更新トークン。 アプリは、このトークンを使用して、現在のアクセストークンの有効期限が切れた後に追加のアクセストークンを取得できます。 Refresh_tokens は有効期間が長く、リソースへのアクセスを長期間保持するために使用できます。| 
|refresh_token_expires_in|更新トークンの有効期間 (秒単位)。| 
|id_token|JSON Web トークン (JWT)。 アプリは、このトークンのセグメントをデコードして、サインインしたユーザーに関する情報を要求することができます。 アプリは値をキャッシュして表示できますが、承認やセキュリティの境界に依存することはできません。|

### <a name="use-the-access-token"></a>アクセストークンを使用する 
 
```
GET /v1.0/me/messages 
Host: https://webapi.com 
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q... 
 ```

### <a name="refresh-the-access-token"></a>アクセストークンを更新する 
 
Access_tokens は有効期間が短いため、リソースへのアクセスを継続するには、有効期限が切れた後で更新する必要があります。 これを行うには、 `/token` エンドポイントに別の POST 要求を送信します。今度は、コードの代わりに refresh_token を指定します。 更新トークンは、クライアントが既にのアクセストークンを受信しているすべてのアクセス許可に対して有効です。 
 
更新トークンには、有効期間が指定されていません。 通常、更新トークンの有効期間は比較的長くなります。 ただし、場合によっては、更新トークンの有効期限が切れたか、失効しているか、必要な操作に必要な特権が不足しています。 アプリケーションでは、トークン発行エンドポイントから返されたエラーを正しく処理し、処理する必要があります。  
 
新しいアクセストークンを取得するために更新トークンを使用しても、更新トークンは取り消されませんが、古い更新トークンを破棄する必要があります。 OAuth 2.0 仕様では、次のことが示されます。"承認サーバーが新しい更新トークンを発行する可能性があります。この場合、クライアントは古い更新トークンを破棄し、新しい更新トークンで置き換える必要があります。 承認サーバーは、クライアントに新しい更新トークンを発行した後に、古い更新トークンを失効させることができます。 
 
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
|client_id|required|AD FS アプリに割り当てられているアプリケーション (クライアント) ID。| 
|grant_type|required|承認コード `refresh_token`フローのこの区間では、で ある必要があります。| 
|resource|オプション|Web API の url。</br>注: MSAL クライアントライブラリを使用している場合、resource パラメーターは送信されません。 代わりに、リソース url はスコープパラメーターの一部として送信されます。`scope = [resource url]//[scope values e.g., openid]`</br>リソースがここで渡されない場合、またはスコープ内にある場合、ADFS は既定のリソース urn: microsoft: userinfo を使用します。 MFA、発行、承認ポリシーなどの userinfo リソースポリシーはカスタマイズできません。|
|スコープ (scope)|オプション|スペースで区切られたスコープのリスト。| 
|refresh_token|required|フローの2番目の段階で取得した refresh_token。| 
|client_secret|web アプリに必要| アプリのアプリ登録ポータルで作成したアプリケーションシークレット。 デバイスに client_secrets を確実に格納することはできないため、ネイティブアプリでは使用しないでください。 これは web apps と web Api に必要であり、client_secret をサーバー側に安全に格納する機能を備えています。 これらのアプリでは、JWT に署名し、それを client_assertion パラメーターとして追加することで、キーベースの認証を使用することもできます。|

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
|access_token|要求されたアクセストークン。 アプリは、このトークンを使用して、セキュリティで保護されたリソース (web API など) に対する認証を行うことができます。| 
|token_type|トークンの種類の値を示します。 AD FS がサポートする型はベアラーだけです。|
|expires_in|アクセストークンの有効期間 (秒単位)。|
|スコープ (scope)|Access_token が有効なスコープ。| 
|refresh_token|OAuth 2.0 更新トークン。 アプリは、このトークンを使用して、現在のアクセストークンの有効期限が切れた後に追加のアクセストークンを取得できます。 Refresh_tokens は有効期間が長く、リソースへのアクセスを長期間保持するために使用できます。| 
|refresh_token_expires_in|更新トークンの有効期間 (秒単位)。| 
|id_token|JSON Web トークン (JWT)。 アプリは、このトークンのセグメントをデコードして、サインインしたユーザーに関する情報を要求することができます。 アプリは値をキャッシュして表示できますが、承認やセキュリティの境界に依存することはできません。|

## <a name="on-behalf-of-flow"></a>代理フロー 
 
OAuth 2.0 の代理フロー (OBO) は、アプリケーションがサービス/web API を呼び出し、その後、別のサービス/web API を呼び出す必要があるユースケースに対応します。 この考え方は、委任されたユーザーの id とアクセス許可を要求チェーンによって伝達することです。 中間層サービスがダウンストリームサービスに対して認証された要求を行うには、ユーザーの代わりに、AD FS からアクセストークンをセキュリティで保護する必要があります。  
 
### <a name="protocol-diagram"></a>プロトコルダイアグラム 
前述の OAuth 2.0 認証コード付与フローを使用して、ユーザーがアプリケーションで認証されていることを前提としています。 この時点で、アプリケーションは、中間層の web API (API A) にアクセスするためのユーザーの要求と同意を持つ API A (トークン A) 用のアクセストークンを持っています。 クライアントがトークンの user_impersonation スコープを要求していることを確認します。 現在、API A では、ダウンストリーム web API (API B) に対して認証された要求を行う必要があります。 

次の手順では、OBO フローを構成します。次の図では、その方法について説明します。 

![代理フロー](media/adfs-scenarios-for-developers/obo.png)

  1. クライアントアプリケーションは、トークン A を使用して API A に要求を行います。  
  注:AD FS で obo フローを構成している`user_impersonation`ときに、スコープが選択`user_impersonation`されていること、およびクライアントが要求でスコープを要求していることを確認してください。 
  2. API A は AD FS トークン発行エンドポイントに対して認証を行い、API B にアクセスするためのトークンを要求します。注:AD FS でこのフローを構成するときに、api A も API A のリソース ID と同じ値を持つ clientID を使用してサーバーアプリケーションとして登録されていることを確認します。詳細については、こちらの「リンクの追加」を参照してください。  
  3. AD FS トークン発行エンドポイントは、トークン A を使用して API A の資格情報を検証し、API B (トークン B) のアクセストークンを発行します。 
  4. トークン B は、API B に対する要求の authorization ヘッダーに設定されます。 
  5. セキュリティで保護されたリソースからのデータが API B によって返されます。 

### <a name="service-to-service-access-token-request"></a>サービス間のアクセストークン要求 
 
アクセストークンを要求するには、次のパラメーターを使用して、AD FS トークンエンドポイントに HTTP POST を実行します。  


### <a name="first-case-access-token-request-with-a-shared-secret"></a>最初のケース:共有シークレットを使用したアクセストークン要求 
 
共有シークレットを使用する場合、サービス間のアクセストークン要求には次のパラメーターが含まれます。 


|パラメーター|必須/オプション|説明|
|-----|-----|-----| 
|grant_type|required|トークン要求の種類。 JWT を使用する要求の場合、値は urn: ietf: params: oauth: grant: JWT-ベアラーである必要があります。|  
|client_id|required|最初の Web API をサーバーアプリ (中間層アプリ) として登録するときに構成するクライアント ID。 これは、1番目のレッグ (最初の Web API の url) で使用されているリソース ID と同じである必要があります。| 
|client_secret|required|AD FS でのサーバーアプリの登録時に作成したアプリケーションシークレット。| 
|主張|required|要求で使用されるトークンの値。|  
|requested_token_use|required|要求の処理方法を指定します。 OBO フローでは、値を on_behalf_of に設定する必要があります。| 
|resource|required|最初の Web API をサーバーアプリとして登録するときに指定されたリソース ID (中間層アプリ)。 リソース ID は、中間層アプリがクライアントの代わりに呼び出す2番目の Web API の url である必要があります。|
|スコープ (scope)|オプション|トークン要求のスコープのスペース区切りリスト。| 

#### <a name="example"></a>例 
 
次`HTTP POST`のは、アクセストークンと更新トークンを要求します。 
 
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

### <a name="second-case-access-token-request-with-a-certificate"></a>2番目のケース:証明書を使用したアクセストークン要求 
 
証明書を使用したサービス間アクセストークン要求には、次のパラメーターが含まれています。 


|パラメーター|必須/省略可能|説明|
|-----|-----|-----| 
|grant_type|required|トークン要求の種類。 JWT を使用する要求の場合、値は urn: ietf: params: oauth: grant: JWT-ベアラーである必要があります。 |
|client_id|required|最初の Web API をサーバーアプリ (中間層アプリ) として登録するときに構成するクライアント ID。 これは、1番目のレッグ (最初の Web API の url) で使用されているリソース ID と同じである必要があります。|  
|client_assertion_type|required|値は urn: ietf: params: oauth: client-assertion: jwt-ベアラーである必要があります。| 
|client_assertion|required|アプリケーションの資格情報として登録した証明書を作成して署名する必要があるアサーション (JSON web トークン)。|  
|主張|required|要求で使用されるトークンの値。| 
|requested_token_use|required|要求の処理方法を指定します。 OBO フローでは、値を on_behalf_of に設定する必要があります。| 
|resource|required|最初の Web API をサーバーアプリとして登録するときに指定されたリソース ID (中間層アプリ)。 リソース ID は、中間層アプリがクライアントの代わりに呼び出す2番目の Web API の url である必要があります。|
|スコープ (scope)|オプション|トークン要求のスコープのスペース区切りリスト。|


パラメーターは、共有シークレットによる要求の場合とほぼ同じです。ただし、client_secret パラメーターは client_assertion_type と client_assertion の2つのパラメーターに置き換えられます。 

#### <a name="example"></a>例 
次の HTTP POST は、証明書を使用して Web API のアクセストークンを要求します。

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

### <a name="service-to-service-access-token-response"></a>サービス間のアクセストークン応答 
 
成功応答は、次のパラメーターを持つ JSON OAuth 2.0 応答です。 


|パラメーター|説明|
|-----|-----| 
|token_type|トークンの種類の値を示します。 AD FS がサポートする型はベアラーだけです。 | 
|スコープ (scope)|トークンで付与されるアクセスのスコープ。| 
|expires_in|アクセストークンが有効である時間の長さ (秒単位)。| 
|access_token|要求されたアクセストークン。 呼び出し元のサービスは、このトークンを使用して受信側のサービスに対する認証を行うことができます。| 
|id_token|JSON Web トークン (JWT)。 アプリは、このトークンのセグメントをデコードして、サインインしたユーザーに関する情報を要求することができます。 アプリは値をキャッシュして表示できますが、承認やセキュリティの境界に依存することはできません。| 
|refresh_token|要求されたアクセストークンの更新トークン。 呼び出し元のサービスは、このトークンを使用して、現在のアクセストークンの有効期限が切れた後に別のアクセストークンを要求できます。|
|Refresh_token_expires_in|更新トークンが有効な時間の長さ (秒単位)。 

### <a name="success-response-example"></a>成功応答の例 
 
次の例は、web API のアクセストークンの要求に対する成功応答を示しています。 

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
 
 
アクセストークンを使用してセキュリティで保護されたリソースにアクセスする現在、中間層のサービスでは、前に取得したトークンを使用して、ダウンストリーム web API に認証済みの要求を行うことができます。そのためには、Authorization ヘッダーでトークンを設定します。  

#### <a name="example"></a>例 
``` 
GET /v1.0/me HTTP/1.1 
Host: https://secondwebapi.com 
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJub25jZSI6IkFRQUJBQUFBQUFCbmZpRy1tQ… 
``` 

## <a name="client-credentials-grant-flow"></a>クライアント資格情報付与フロー 
 
[RFC 6749](https://tools.ietf.org/html/rfc6749#section-4.4)に指定されている OAuth 2.0 クライアント資格情報付与を使用して、アプリケーションの id を使用して web ホストリソースにアクセスできます。 この種類の許可は、通常、ユーザーとの直接の対話を行わずに、バックグラウンドで実行する必要があるサーバー間の対話に使用されます。 この種のアプリケーションは、多くの場合、デーモンまたはサービスアカウントと呼ばれます。 

OAuth 2.0 クライアント資格情報付与フローでは、web サービス (confidential クライアント) が、別の web サービスを呼び出すときに認証のために、ユーザーを偽装するのではなく、独自の資格情報を使用することが許可されます。 このシナリオでは、クライアントは通常、中間層の web サービス、デーモンサービス、または web サイトです。 さらに高い保証を行うために、AD FS では、呼び出し元のサービスが (共有シークレットではなく) 証明書を資格情報として使用することもできます。 

### <a name="protocol-diagram"></a>プロトコルダイアグラム 

次の図は、クライアント資格情報の付与フローを示しています。 

![クライアント資格情報](media/adfs-scenarios-for-developers/credentials.png)

### <a name="request-a-token"></a>トークンの要求 
 
クライアント資格情報の付与を使用してトークンを取得する`POST`には、/トークン AD FS エンドポイントに要求を送信します。  
 
### <a name="first-case-access-token-request-with-a-shared-secret"></a>最初のケース:共有シークレットを使用したアクセストークン要求 
 
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
|client_id|required|AD FS アプリに割り当てられているアプリケーション (クライアント) ID。| 
|スコープ (scope)|オプション|ユーザーに同意させるスコープのスペース区切りの一覧。| 
|client_secret|required|アプリ登録ポータルでアプリ用に生成したクライアントシークレット。 クライアントシークレットは、送信する前に URL エンコードする必要があります。| 
|grant_type|required|をに `client_credentials`設定する必要があります。|

### <a name="second-case-access-token-request-with-a-certificate"></a>2番目のケース:証明書を使用したアクセストークン要求 

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
|client_assertion_type|required|この値は urn: ietf: params: oauth: クライアントアサーションの種類: jwt-ベアラーに設定する必要があります。| 
|client_assertion|required|アプリケーションの資格情報として登録した証明書を作成して署名する必要があるアサーション (JSON web トークン)。|  
|grant_type|required|をに `client_credentials`設定する必要があります。|
|client_id|オプション|AD FS アプリに割り当てられているアプリケーション (クライアント) ID。 これは client_assertion の一部であるため、ここで渡す必要はありません。| 
|スコープ (scope)|オプション|ユーザーに同意させるスコープのスペース区切りの一覧。| 

### <a name="use-a-token"></a>トークンを使用する 
 
トークンを取得したので、トークンを使用してリソースへの要求を行います。 トークンの有効期限が切れたら、トークンエンドポイントに対して要求を繰り返し、新しいアクセストークンを取得します。  
 
```
GET /v1.0/me/messages 
Host: https://webapi.com 
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...  
```

## <a name="resource-owner-password-credentials-grant-flow-not-recommended"></a>リソース所有者のパスワード資格情報の付与フロー (推奨されません) 
 
リソース所有者のパスワード資格情報 (ROPC) の付与により、アプリケーションはユーザーのパスワードを直接処理してサインインできます。 ROPC フローには高い信頼性とユーザーの露出が必要です。このフローは、他のセキュリティが強化されたフローを使用できない場合にのみ使用してください。  
 
### <a name="protocol-diagram"></a>プロトコルダイアグラム 
 
次の図は、ROPC フローを示しています。

![ROPC フロー](media/adfs-scenarios-for-developers/resource.png)

### <a name="authorization-request"></a>承認要求 
ROPC フローは単一の要求であり、クライアント id とユーザーの資格情報を IDP に送信し、返されたトークンを受信します。 クライアントは、その前に、ユーザーの電子メールアドレス (UPN) とパスワードを要求する必要があります。 要求が成功すると、クライアントは、ユーザーの資格情報をメモリから安全に解放する必要があります。 保存することはできません。  

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
|client_id|required|クライアント ID| 
|grant_type|required|Password に設定する必要があります。| 
|username|required|ユーザーの電子メール アドレス。| 
|password|required|ユーザーのパスワード。| 
|スコープ (scope)|オプション|スペースで区切られたスコープのリスト。|

### <a name="successful-authentication-response"></a>成功した認証応答 
次の例は、正常なトークン応答を示しています。 

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
|token_type|常にベアラーに設定します。| 
|スコープ (scope)|アクセストークンが返された場合、このパラメーターは、アクセストークンが有効なスコープの一覧を表示します。| 
|expires_in|含まれているアクセストークンが有効である秒数。| 
|access_token|要求されたスコープに対して発行されます。| 
|id_token|JSON Web トークン (JWT)。 アプリは、このトークンのセグメントをデコードして、サインインしたユーザーに関する情報を要求することができます。 アプリは値をキャッシュして表示できますが、承認やセキュリティの境界に依存することはできません。| 
|refresh_token_expires_in|含まれている更新トークンが有効な秒数。| 
|refresh_token|元のスコープパラメーターに offline_access が含まれている場合に発行されます。|

更新トークンを使用して、前の「認証コード付与フロー」で説明されているものと同じフローを使用して、新しいアクセストークンを取得し、トークンを更新することができます。   

## <a name="device-code-flow"></a>デバイスコードフロー 
 
デバイスコード付与を使用すると、ユーザーは、スマート TV、IoT デバイス、プリンターなどの入力に制約のあるデバイスにサインインできます。 このフローを有効にするために、デバイスはユーザーが別のデバイス上のブラウザーで web ページにアクセスしてサインインできるようにします。 ユーザーがサインインすると、デバイスは必要に応じてアクセストークンを取得し、トークンを更新できます。 
 
### <a name="protocol-diagram"></a>プロトコルダイアグラム 
 
デバイスコードフロー全体は、次の図のようになります。 各手順については、この記事の後半で説明します。 
 
![デバイスコードフロー](media/adfs-scenarios-for-developers/device.png)

### <a name="device-authorization-request"></a>デバイスの承認要求 
クライアントは、まず認証サーバーで認証を開始するために使用されるデバイスとユーザーコードを確認する必要があります。 クライアントは、この要求を/devicecode エンドポイントから収集します。 この要求では、クライアントには、ユーザーから取得する必要のあるアクセス許可も含める必要があります。 この要求が送信された時点から、ユーザーがサインインできるのは15分 (expires_in の通常の値) であるため、ユーザーがサインインの準備ができていることを示す場合にのみ、この要求を行います。 

```
// Line breaks are for legibility only. 
 
POST https://adfs.contoso.com/adfs/oauth2/devicecode 
Content-Type: application/x-www-form-urlencoded 
 
client_id=6731de76-14a6-49ae-97bc-6eba6914391e 
scope=openid 
```


|パラメーター|条件|説明|
|-----|-----|-----| 
|client_id|required|AD FS アプリに割り当てられているアプリケーション (クライアント) ID。| 
|スコープ (scope)|オプション|スペースで区切られたスコープのリスト。|

### <a name="device-authorization-response"></a>デバイス承認応答 
成功した応答は、ユーザーにサインインを許可するために必要な情報を含む JSON オブジェクトになります。 


|パラメーター|説明|
|-----|-----| 
|device_code|クライアントと承認サーバー間のセッションを検証するために使用される長い文字列。 クライアントはこのパラメーターを使用して、承認サーバーからアクセストークンを要求します。| 
|user_code|セカンダリデバイスでセッションを識別するために使用される、ユーザーに表示される短い文字列。| 
|verification_uri|サインインするためにユーザーが user_code を使用してアクセスする必要がある URI。| 
|verification_uri_complete|サインインするためにユーザーが user_code を使用してアクセスする必要がある URI。 これは、ユーザーが user_code を入力する必要がないように user_code に事前ます。| 
|expires_in|Device_code と user_code の有効期限が切れるまでの秒数。| 
|定期的|クライアントがポーリング要求の間に待機する秒数。| 
|メッセージ|ユーザーに指示がある、ユーザーが判読できる文字列。 これは、適切な言語のカルチャコードを入力するという形式の要求にクエリパラメーターを含めることでローカライズできます。  

### <a name="authenticating-the-user"></a>ユーザーの認証 
User_code と verification_uri を受信すると、クライアントはこれらをユーザーに表示し、携帯電話または PC ブラウザーを使用してサインインするように指示します。 さらに、クライアントは、QR コードまたは同様のメカニズムを使用して verfication_uri_complete を表示できます。これにより、ユーザーの user_code が入力されます。 ユーザーが verification_uri で認証を行っている間、クライアントは、device_code を使用して、要求されたトークンのトークンエンドポイントをポーリングする必要があります。 

```
POST https://adfs.contoso.com /adfs/oauth2/token 
Content-Type: application/x-www-form-urlencoded 
 
grant_type: urn:ietf:params:oauth:grant-type:device_code 
client_id: 6731de76-14a6-49ae-97bc-6eba6914391e 
device_code: GMMhmHCXhWEzkobqIHGG_EnNYYsAkukHspeYUk9E8 
```


|パラメーター|required|説明|
|-----|-----|-----| 
|grant_type|required|Urn: ietf: params: oauth: grant type: device_code である必要があります。| 
|client_id|required|最初の要求で使用された client_id と一致する必要があります。| 
|code|required|デバイスの承認要求で device_code が返されました。|

### <a name="successful-authentication-response"></a>成功した認証応答 
成功したトークン応答は次のようになります。  


|パラメーター|説明|
|-----|-----| 
|token_type|常に "ベアラー"。| 
|スコープ (scope)|アクセストークンが返された場合は、アクセストークンが有効なスコープが一覧表示されます。| 
|expires_in|含まれているアクセストークンが有効になるまでの秒数。| 
|access_token|要求されたスコープに対して発行されます。| 
|id_token|元のスコープパラメーターに openid スコープが含まれている場合に発行されます。| 
|refresh_token|元のスコープパラメーターに offline_access が含まれている場合に発行されます。| 
|refresh_token_expires_in|含まれている更新トークンが有効になるまでの秒数。| 


## <a name="related-content"></a>関連コンテンツ  
関連するフローの使用方法についての詳細な手順については、「 [AD FS 開発](../AD-FS-Development.md)」を参照してください。 
