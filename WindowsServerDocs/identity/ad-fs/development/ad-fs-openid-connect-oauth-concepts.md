---
title: AD FS OpenID Connect/OAuth の概念
description: 最新の認証の概念 AD FS について説明します。
author: billmath
ms.author: billmath
manager: daveba
ms.date: 08/09/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 0e680e07ce1ee27a73791e310a71b85ad76d6318
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358759"
---
# <a name="ad-fs-openid-connectoauth-concepts"></a>AD FS OpenID Connect/OAuth の概念
AD FS 2016 以降に適用されます
 
## <a name="modern-authentication-actors"></a>先進認証アクター 

|Actor| 説明|
|-----|-----|
|エンド ユーザー|これは、リソースへのアクセスを必要とするセキュリティプリンシパル (ユーザー、アプリケーション、サービス、およびグループ) です。|  
|クライアント|これは、クライアント ID によって識別される web アプリケーションです。 クライアントは、通常、エンドユーザーが操作するパーティであり、承認サーバーからのトークンを要求します。
|承認サーバー/Id プロバイダー (IdP)| これは AD FS サーバーです。 組織のディレクトリに存在するセキュリティプリンシパルの id を確認する役割があります。 セキュリティプリンシパルが正常に認証されると、セキュリティトークン (ベアラーアクセストークン、ID トークン、更新トークン) が発行されます。
|リソースサーバー/リソースプロバイダー/証明書利用者| これは、リソースまたはデータが存在する場所です。 クライアントを安全に認証および承認するために承認サーバーを信頼し、ベアラーアクセストークンを使用してリソースへのアクセスを許可できるようにします。

次の図は、アクター間の最も基本的な関係を示しています。

![先進認証アクター](media/adfs-modern-auth-concepts/concept1.png)

## <a name="application-types"></a>アプリケーションの種類 
 

|アプリケーションの種類|説明|ロール|
|-----|-----|-----|
|ネイティブアプリケーション|**パブリッククライアント**とも呼ばれ、これは、ユーザーが操作する pc またはデバイスで実行されるクライアントアプリとして使用することを目的としています。|リソースへのユーザーアクセスのために、承認サーバー (AD FS) からのトークンを要求します。 Http ヘッダーとしてトークンを使用して、保護されたリソースに HTTP 要求を送信します。| 
|サーバーアプリケーション (Web アプリ)|サーバー上で実行され、一般にブラウザーを介してユーザーがアクセスできる web アプリケーション。 独自のクライアント "シークレット" または資格情報を維持できるため、**機密クライアント**と呼ばれることもあります。 |リソースへのユーザーアクセスのために、承認サーバー (AD FS) からのトークンを要求します。 トークンを要求する前に、クライアント (Web アプリ) はそのシークレットを使用して認証する必要があります。 | 
|Web API|ユーザーがアクセスしている終了リソース。 これらは、"証明書利用者" の新しい表現と考えてください。|クライアントによって取得されたベアラーアクセストークンを消費します| 

## <a name="application-group"></a>アプリケーショングループ 
 
AD FS で構成されたすべての OAuth クライアント (ネイティブまたは web アプリ) またはリソース (web api) は、アプリケーショングループに関連付けられている必要があります。 アプリケーショングループ内のクライアントは、同じグループ内のリソースにアクセスするように構成できます。 アプリケーショングループには、複数のクライアントとリソースを含めることができます。  

## <a name="security-tokens"></a>セキュリティトークン 
 
先進認証では、次のトークンの種類を使用します。 
- **id_token**: 承認サーバー (AD FS) によって発行され、クライアントによって使用される JWT トークン。 ID トークン内の要求には、クライアントがそれを使用できるように、ユーザーに関する情報が含まれます。  
- **access_token**: 承認サーバー (AD FS) によって発行され、リソースによって使用されることを意図した JWT トークン。 このトークンの ' aud ' または対象ユーザーの要求は、リソースまたは Web API の識別子と一致している必要があります。  
- **refresh_token**: これは、id_token および access_token を更新する必要がある場合にクライアントが使用する AD FS によって発行されたトークンです。 トークンはクライアントに対して非透過的であり、AD FS によってのみ使用できます。  

## <a name="scopes"></a>スコープ 
 
AD FS にリソースを登録するときに、AD FS が特定のアクションを実行できるようにスコープを構成できます。 スコープの構成に加えて、アクションを実行するために AD FS 要求でもスコープの値を送信する必要があります。 たとえば、管理者はリソースの登録時に openid としてスコープを構成する必要があります。また、アプリケーション (クライアント) が ID トークンを発行するには、AD FS の認証要求で scope = openid を送信する必要があります。 AD FS で使用できるスコープの詳細については、以下を参照してください。 
 
- aza- [Broker クライアントに OAuth 2.0 プロトコル拡張](https://docs.microsoft.com/openspecs/windows_protocols/ms-oapxbc/2f7d8875-0383-4058-956d-2fb216b44706)を使用している場合  and スコープパラメーターにスコープ "aza" が含まれていると、サーバーは新しいプライマリ更新トークンを発行し、refresh_ を設定するだけでなく、応答の refresh_token フィールドに設定します。token_expires_in フィールドが適用されている場合は、新しいプライマリ更新トークンの有効期間を設定します。 
- openid-アプリケーションが OpenID Connect 承認プロトコルの使用を要求できるようにします。 
- logon_cert-logon_cert スコープを使用すると、アプリケーションはログオン証明書を要求することができます。これは、認証されたユーザーを対話的にログオンするために使用できます。 AD FS サーバーは、応答から access_token パラメーターを除外し、代わりに base64 でエンコードされた CMS 証明書チェーンまたは CMC 完全 PKI 応答を提供します。 詳細について [は、こちら](https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-oapx/32ce8878-7d33-4c02-818b-6c9164cc731e)を参照してください。
- user_impersonation-user_impersonation スコープは、AD FS からの代理アクセストークンを正常に要求するために必要です。 このスコープを使用する方法の詳細については、 [AD FS 2016 で OAuth を使用して、(OBO) を使用して多層アプリケーションを構築](ad-fs-on-behalf-of-authentication-in-windows-server.md)する方法に関する説明を参照してください。 
- allatclaims – allatclaims スコープを使用すると、アプリケーションはアクセストークン内の要求を ID トークンにも追加するように要求できます。   
- vpn_cert-vpn_cert スコープは、アプリケーションが VPN 証明書を要求できるようにします。この証明書は、eap-tls 認証を使用して VPN 接続を確立するために使用できます。 これはサポートされなくなりました。 
- 電子メール-アプリケーションは、サインインしたユーザーの電子メール要求を要求できます。  
- プロファイル-アプリケーションがサインインユーザーのプロファイル関連の要求を要求できるようにします。  

## <a name="claims"></a>信頼性情報 
 
AD FS によって発行されたセキュリティトークン (アクセストークンと ID トークン) には、要求、または認証されたサブジェクトに関する情報のアサーションが含まれます。 アプリケーションでは、次のようなさまざまなタスクに対して要求を使用できます。 
- トークンを検証する 
- サブジェクトのディレクトリテナントを識別する 
- ユーザー情報の表示 
- 指定されたセキュリティトークンに存在する要求は、トークンの種類、ユーザーの認証に使用される資格情報の種類、およびアプリケーション構成によって決まります。  
 
## <a name="high-level-ad-fs-authentication-flow"></a>高レベル AD FS 認証フロー 

![AD FS 認証フロー](media/adfs-modern-auth-concepts/adfsauthflow.png)


 1. AD FS は、クライアントから認証要求を受信します。  
 
 2. AD FS は、AD FS でクライアントとリソースの登録時に取得したクライアント ID を使用して、認証要求のクライアント ID を検証します。 機密クライアントを使用している場合は、AD FS 認証要求で提供されたクライアントシークレットも検証します。 また AD FS クライアントのリダイレクト uri も検証します。 
 
 3. AD FS は、認証要求で渡されたリソースパラメーターを介してクライアントがアクセスするリソースを識別します。 MSAL クライアントライブラリを使用している場合、resource パラメーターは送信されません。 代わりに、リソース url はスコープパラメーターの一部として送信されます。*スコープ = [リソース url]//[スコープ値 (openid など*)。 

    リソースがリソースまたはスコープパラメーターを使用して渡されない場合、ADFS は既定のリソース urn を使用します。 microsoft: userinfo ポリシー (MFA、発行、または承認ポリシーなど) を構成することはできません。 
 
 4. 次の AD FS は、クライアントがリソースにアクセスするためのアクセス許可を持っているかどうかを検証します。 また AD FS は、認証要求で渡されるスコープが、リソースの登録時に構成されたスコープと一致するかどうかを検証します。 クライアントにアクセス許可がない場合、または適切なスコープが auth 要求で送信されない場合は、認証フローが終了します。   
 
 5. アクセス許可とスコープが検証されると、AD FS は、構成された[認証方法](../operations/configure-authentication-policies.md)を使用してユーザーを認証します。   

 6. リソースポリシーまたはグローバル認証ポリシーに従って[追加の認証方法](../operations/configure-additional-authentication-methods-for-ad-fs.md)が必要な場合は、AD FS によって追加の認証がトリガーされます。 

 7. AD FS は、 [AZURE mfa](../operations/configure-ad-fs-and-azure-mfa.md)または[サードパーティの mfa](../operations/additional-authentication-methods-ad-fs.md)を使用して認証を実行します。   
 
 8. ユーザーが認証されると、AD FS によって[要求規則](../deployment/configuring-claim-rules.md)が適用され (セキュリティトークンの一部としてリソースに送信される要求が決定されます)、[アクセス制御ポリシー](../operations/ad-fs-client-access-policies.md) (ユーザーがリソースにアクセスするために必要な条件を満たしていることが判断されます)。   

 9. 次に、AD FS によってアクセストークンと更新トークンが生成されます。 

 10. AD FS は、ID トークンも生成します。 
 
 11. スコープ = allatclaims が auth 要求に含まれている場合、定義された要求規則に基づいてアクセストークンに要求が含まれるように、 [ID トークンがカスタマイズされ](custom-id-tokens-in-ad-fs.md)ます。 
    
 12. 必要なトークンが生成され、カスタマイズされると、AD FS はトークンを含むクライアントに応答します。 認証要求に scope = openid が含まれている場合にのみ、ID トークンが応答に含まれます。 クライアントは、トークンエンドポイントを使用して、認証後に常に ID トークンを取得できます。 

## <a name="types-of-libraries"></a>ライブラリの種類 
  
AD FS では、次の2種類のライブラリが使用されます。 
- **クライアントライブラリ**:ネイティブクライアントとサーバーアプリは、クライアントライブラリを使用して、Web API などのリソースを呼び出すためのアクセストークンを取得します。 Microsoft Authentication Library (MSAL) は、AD FS 2019 を使用する場合の最新の推奨されるクライアントライブラリです。 AD FS 2016 には Active Directory 認証ライブラリ (ADAL) を使用することをお勧めします。  

- **サーバーミドルウェアライブラリ**:Web アプリでは、ユーザーのサインインにサーバーミドルウェアライブラリを使用します。 Web Api は、サーバーミドルウェアライブラリを使用して、ネイティブクライアントまたは他のサーバーによって送信されたトークンを検証します。 推奨されるミドルウェアライブラリは OWIN (Open Web Interface for .NET) です。 

## <a name="customize-id-token-additional-claims-in-id-token"></a>ID トークンをカスタマイズする (ID トークンの追加の要求)
 
特定のシナリオでは、Web アプリ (クライアント) が機能を利用するために ID トークンに追加の要求を必要とする可能性があります。 これは、次のいずれかのオプションを使用して実現できます。 

**選択肢 1:** パブリッククライアントを使用していて、web アプリにアクセスしようとしているリソースがない場合は、を使用する必要があります。 オプションにはが必要です。 
1.  form_post として設定される response_mode 
2.  証明書利用者識別子 (Web API identifier) はクライアント識別子と同じです

![AD FS カスタマイズトークンオプション1](media/adfs-modern-auth-concepts/option1.png)

**選択肢 2:** Web アプリにアクセスしようとしているリソースがあり、ID トークンを介して追加の要求を渡す必要がある場合は、を使用する必要があります。 パブリックと機密の両方のクライアントを使用できます。 オプションにはが必要です。 
1.  form_post として設定される response_mode 
2.  KB4019472 が AD FS サーバーにインストールされている 
3.  クライアント– RP ペアに割り当てられている allatclaims のスコープ。 次の例に示すように、ADFSApplicationPermission を使用してスコープを割り当てることができます (既に一度付与されている場合は AdfsApplicationPermission を使用します)。 

    ``` powershell
    Grant-AdfsApplicationPermission -ClientRoleIdentifier "https://my/privateclient" -ServerRoleIdentifier "https://rp/fedpassive" -ScopeNames "allatclaims","openid"
    ```

![AD FS カスタマイズトークンオプション2](media/adfs-modern-auth-concepts/option2.png)

カスタマイズされた ID トークンを取得するために ADFS で Web アプリを構成する方法について理解を深めるには、「 [OpenID connect または OAuth を使用する場合に id_token で出力される要求をカスタマイズ](Custom-Id-Tokens-in-AD-FS.md)する」を参照してください。 AD FS 2016 以降

## <a name="single-log-out"></a>単一のログアウト

シングルログアウトでは、セッション id を使用してすべてのクライアントセッションが終了します。AD FS 2016 以降では、OpenID Connect/OAuth のシングルログアウトがサポートされています。 詳細については、「 [AD FS を使用した OpenID connect のシングルログアウト](ad-fs-logout-openid-connect.md)」を参照してください。


## <a name="ad-fs-endpoints"></a>AD FS エンドポイント

|AD FS エンドポイント|説明|
|-----|-----|
|/authorize|AD FS は、アクセストークンを取得するために使用できる認証コードを返します。|
|/token|AD FS は、リソース (Web API) へのアクセスに使用できるアクセストークンを返します|
|/userinfo|AD FS は、認証されたユーザーに関する要求を返します。|
|/devicecode|デバイスコードとユーザーコードを返す AD FS|
|/ログアウト|ユーザーをログアウト AD FS|
|/キー|応答の署名に使用される公開キーの AD FS|
|/.well-known/openid-configuration|AD FS が OAuth/OpenID Connect メタデータを返す|
