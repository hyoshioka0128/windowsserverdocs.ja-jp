---
ms.assetid: 5052f13c-ff35-471d-bff5-00b5dd24f8aa
title: AD FS 2016 以降で OAuth を使用して、の代理 (OBO) を使用して多層アプリケーションを構築する
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.openlocfilehash: c313754b315b48982342fe2797d1ed766ce354a9
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87965169"
---
# <a name="build-a-multi-tiered-application-using-on-behalf-of-obo-using-oauth-with-ad-fs-2016-or-later"></a>AD FS 2016 以降で OAuth を使用して、の代理 (OBO) を使用して多層アプリケーションを構築する

このチュートリアルでは、Windows Server 2016 TP5 以降の AD FS を使用して、の代理 (OBO) 認証を実装するための手順を示します。 OBO 認証の詳細については[AD FS OpenID connect/OAuth フローとアプリケーションシナリオ](../../ad-fs/overview/ad-fs-openid-connect-oauth-flows-scenarios.md)に関するページを参照してください。

> [!WARNING]
> ここで作成できる例は、学習のみを目的としています。 これらの手順は、モデルの必須要素を公開するために使用できる、最も単純で最小の実装用です。 この例には、エラー処理やその他の関連機能のすべての側面が含まれているわけではなく、OBO 認証を成功させるためだけに焦点を当てています。

## <a name="overview"></a>概要

このサンプルでは、クライアントが中間層の Web サービスにアクセスする認証フローを作成します。 web サービスは、認証されたクライアントの代わりに動作し、アクセストークンを取得します。

![AD FS の代表図](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO28.png)

次に、サンプルで実現する認証フローを示します。
1. クライアントが認証エンドポイントを AD FS に認証し、認証コードを要求する
2. 認証エンドポイントがクライアントに認証コードを返す
3. クライアントは認証コードを使用して AD FS トークンエンドポイントに提示し、中間層 Web サービスのアクセストークンを WebAPI として要求します。
4. AD FS は、アクセストークンを中間層 Web サービスに返します。 その他の機能については、中間層サービスはバックエンド WebAPI へのアクセスを必要とします。
5. クライアントは、アクセストークンを使用して中間層サービスを使用します。
6. 中間層サービスは、AD FS トークンエンドポイントへのアクセストークンを提供し、認証されたユーザーに代わってバックエンド WebAPI のアクセストークンを要求します。
7. バックエンド WebAPI のアクセストークンをクライアントとして中間層サービス actiing に返す AD FS
8. 中間層サービスは、手順 7. で AD FS によって提供されたアクセストークンを使用してバックエンド WebAPI にクライアントとしてアクセスし、必要な機能を実行します。

## <a name="sample-structure"></a>サンプルの構造

サンプルは3つのモジュールで構成されます

モジュール | 説明
-------|------------
ToDoClient | ユーザーが対話するネイティブクライアント
ToDoService | バックエンド WebAPI のクライアントとして機能する中間層 web API
WebAPIOBO | ユーザーが ToDoItem を追加したときに必要な操作を実行するために ToDoService によって使用されるバックエンド web api

## <a name="setting-up-the-development-box"></a>開発ボックスの設定

このチュートリアルでは、Visual Studio 2015 を使用します。 プロジェクトは、Active Directory 認証ライブラリ (ADAL) を頻繁に使用します。 ADAL の詳細については[Active Directory 認証ライブラリ .net](/dotnet/api/microsoft.identitymodel.clients.activedirectory?view=azure-dotnet)をご覧ください

このサンプルでは、SQL LocalDB v1.0 も使用されています。 サンプルで作業する前に、SQL LocalDB をインストールします。

## <a name="setting-up-the-environment"></a>環境のセットアップ
次の基本的なセットアップを使用します。

1. **DC**: AD FS がホストされるドメインのドメインコントローラー
2. **AD FS server**: ドメインの AD FS サーバー
3. **開発用コンピューター**: Visual Studio がインストールされていて、サンプルを開発しているコンピューター

必要に応じて、2台のコンピューターのみを使用できます。 1つは DC/ADFS 用で、もう1つはサンプルを開発するためのものです。

ドメインコントローラーと AD FS のセットアップ方法については、この記事では説明しません。 デプロイの詳細については、次を参照してください。

- [AD DS 展開](../../ad-ds/deploy/AD-DS-Deployment.md)
- [AD FS 展開](../AD-FS-Deployment.md)

このサンプルは、Vittorio によって作成された Azure に対する既存の OBO サンプルに基づいており、[ここ](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof)で入手できます。 指示に従って、開発用コンピューター上のプロジェクトを複製し、サンプルのコピーを作成して作業を開始します。

## <a name="clone-or-download-this-repository"></a>このリポジトリをクローンまたはダウンロードする

シェルまたはコマンド ラインから:

```
git clone https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof.git
```

## <a name="modifying-the-sample"></a>サンプルの変更

ソリューション WebAPI-OnBehalfOf-DotNet を開くとすぐに、ソリューションに2つのプロジェクトがあることがわかります。

* **ToDoListClient**: これは、ユーザーが対話する OpenID クライアントとして機能します
* **ToDoListService**: これは、認証されたユーザーの別のバックエンド WebAPI obo と対話する中間層の WEB サーバーアプリ/サービスになります。

ご覧のように、後で別のプロジェクトを追加する必要があります。このプロジェクトは、中間層の ToDoListService によってアクセスされるリソースとして機能します。

### <a name="configuring-ad-fs-for-the-client-and-webserver-app"></a>クライアントおよび Web サーバーアプリの AD FS の構成

このサンプルの現在の形式では、認証は Azure AD に対して実行されるように構成されています。 認証メカニズムを変更し、オンプレミスにデプロイされた AD FS にダイレクトします。 そのためには、サンプルに含まれているクライアントと Web サーバーアプリを認識するように AD FS を構成する必要があります。

**アプリケーショングループの作成**

AD FS 管理 MMC を開き、新しいアプリケーショングループを追加します。 WebAPI テンプレートを選択します。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO2.PNG)

[次へ] をクリックすると、クライアントアプリに関する情報を提供するためのページが表示されます。 AD FS でクライアントアプリに適切な名前を付けます。 クライアント識別子をコピーし、後でアクセスできる場所に保存します。これは、visual studio のアプリケーション構成で必要になります。

>注: リダイレクト URI は、ネイティブクライアントの場合には実際には使用されないため、任意の URI にすることができます。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO11.PNG)

[次へ] をクリックすると、WebAPI に関する情報を提供するためのページが表示されます。 WebAPI の AD FS エントリに適切な名前を付け、ToDoListService に対して Visual Studio に表示される URI としてリダイレクト URI を入力します。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO16.PNG)

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO18.PNG)

[次へ] をクリックすると、[Access Control ポリシーの選択] ページが表示されます。 [ポリシー] セクションで、[everyone を許可する] が表示されていることを確認します。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO1.PNG)

[次へ] をクリックすると、[アプリケーションのアクセス許可の構成] ページが表示されます。 このページで、openid として許可されているスコープ (既定ではオン) と user_impersonation を選択します。 AD FS から代理アクセストークンを要求できるようにするには、スコープ ' user_impersonation ' が必要です。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO12.PNG)

[次へ] をクリックすると、概要ページが表示されます。 ウィザードの残りの部分を実行し、構成を完了します。

代理認証を有効にするには、AD FS がクライアントに対するスコープ user_impersonation のアクセストークンを返すことを確認する必要があります。 ToDoListServiceWebApi の要求発行を変更して、次の3つのカスタム規則を追加します。

```
@RuleName = "All claims"
c:[]
=> issue(claim = c);

@RuleName = "Issue user_impersonation scope"
=> issue(Type = "http://schemas.microsoft.com/identity/claims/scope", Value = "user_impersonation");
```

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO10.PNG)

**アプリケーショングループのクライアントとしての ToDoListService の追加**

この段階では、Web サーバーアプリがリソースとしてではなく、クライアントとして機能するために AD FS に追加のエントリを作成する必要があります。 先ほど作成したアプリケーショングループを開き、[アプリケーションの追加] をクリックします。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO15.PNG)

[MySampleGroup への新しいアプリケーションの追加] ページが表示されます。 このページで、スタンドアロンアプリケーションとして [サーバーアプリケーションまたは Web サイト] を選択します。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO19.PNG)

[次へ] をクリックすると、アプリケーションの詳細を指定するためのページが表示されます。 [名前] セクションで、構成エントリに適切な名前を指定します。 クライアント識別子が ToDoListServiceWebAPI の識別子と同じであることを確認します。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO20.PNG)

[次へ] をクリックすると、アプリケーションの資格情報を構成するためのページが表示されます。 [共有シークレットの生成] をクリックします。 自動的に生成されたシークレットが表示されます。 ToDoListService を visual studio で構成するときに必要になるので、シークレットをどこかにコピーします。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO17.PNG)

[次へ] をクリックして、ウィザードを完了します。

### <a name="modifying-the-todolistclient-code"></a>ToDoListClient コードの変更

#### <a name="modify-the-application-config"></a>アプリケーション構成の変更

WebAPI-DotNet ソリューションの ToDoListClient プロジェクトにアクセスします。 App.config ファイルを開き、次のように変更します。

* Ida: テナントキーのエントリをコメント化します。
* Ida: RedirectURI には、AD FS で MySampleGroup_ClientApplication を構成するときに指定した任意の URI を入力します。
* Ida: ClientID キーには、MySampleGroup_ClientApplication の構成時に指定 AD FS れるクライアント ID 識別子を指定します。
* Ida: ToDoListResourceID の場合は、ToDoListServiceWebApi の構成時に指定したリソース ID を指定し AD FS
* キー ida: AADInstance をコメント化します。
* Ida: ToDoListBaseAddress の場合、ToDoListServiceWebApi のリソース ID を入力します。 これは、ToDoList WebAPI の呼び出し中に使用されます。
* キー ida: Authority を追加し、AD FS の URI として値を指定します。

App.Config の**appSettings**は次のようになります。

```
<appSettings>
    <!--<add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" />-->
    <add key="ida:ClientId" value="c7f7b85c-497c-4589-877f-b17a0bd13398" />
    <add key="ida:RedirectUri" value="https://arbitraryuri.com/" />
    <add key="ida:TodoListResourceId" value="https://localhost:44321/" />
    <!--<add key="ida:AADInstance" value="https://login.microsoftonline.com/{0}" />-->
    <add key="ida:TodoListBaseAddress" value="https://localhost:44321" />
    <add key="ida:Authority" value="https://fs.anandmsft.com/adfs/"/>
</appSettings>
```

#### <a name="modifying-the-code"></a>コードの変更

**MainWindow.xaml.cs**

アプリケーション構成からテナント情報を読み取る行をコメント化します

```
//private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];
//private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];
```

String authority の値をに変更します。

```
private static string authority = ConfigurationManager.AppSettings["ida:Authority"];
```

ToDoListResourceId と ToDoListBaseAddress の正しい値を読み取るようにコードを変更します。

```
private static string todoListResourceId = ConfigurationManager.AppSettings["ida:TodoListResourceId"];
private static string todoListBaseAddress = ConfigurationManager.AppSettings["ida:TodoListBaseAddress"];
```

関数 Mainwindow.xaml () で、authcontext の初期化を次のように変更します。

```
authContext = new AuthenticationContext(authority, false);
```

### <a name="adding-the-backend-resource"></a>バックエンドリソースの追加

代理フローを完了するには、認証されたユーザーの代理として ToDoListService がアクセスするバックエンドリソースを作成する必要があります。 バックエンドリソースの選択は要件によって異なる場合がありますが、このサンプルでは基本的な WebAPI を作成できます。

* ソリューションエクスプローラーでソリューション ' WebAPI-DotNet ' を右クリックし、[> 追加]、[新しいプロジェクト] の順に選択します。
* ASP.NET Web アプリケーションテンプレートの選択

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO4.PNG)

* 次のプロンプトで、[認証の変更] をクリックします。
* [職場と学校のアカウント] を選択し、右側のドロップダウンリストで [オンプレミス] を選択します。
* AD FS デプロイの federationmetadata.xml パスを入力し、アプリの URI を指定します (ここでは URI を指定し、後で変更します)。その後、[Ok] をクリックしてプロジェクトをソリューションに追加します。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO9.PNG)

* ソリューションエクスプローラーで、作成した新しいプロジェクトの下にある [コントローラー] を右クリックします。 [Add-> Controller] を選択します。
* テンプレートの選択で、[Web API 2 コントローラー-空] を選択し、[Ok] をクリックします。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO3.PNG)

* コントローラーに適切な名前を付けます。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO13.PNG)

* コントローラーに次のコードを追加します。

    ```cs
        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Net;
        using System.Net.Http;
        using System.Web.Http;
        namespace WebAPIOBO.Controllers
        {
            [Authorize]
            public class WebAPIOBOController : ApiController
            {
                public IHttpActionResult Get()
                {
                    return Ok($"WebAPI via OBO (user: {User.Identity.Name}");
                }
            }
        }
    ```

このコードは、誰かが WebAPI WebAPIOBO に Get 要求を行ったときに、単に文字列を返します。

### <a name="adding-the-new-backend-webapi-to-ad-fs"></a>AD FS に新しいバックエンド WebAPI を追加する

MySampleGroup アプリケーショングループを開きます。 [アプリケーションの追加] をクリックし、[Web API テンプレート] を選択し、[次へ] をクリックします。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO6.PNG)

[Web API の構成] ページで、WebAPI エントリと識別子に適切な名前を指定します。 識別子は、visual studio の WebAPIOBO プロジェクトの [SSL URL] の値にする必要があります (BackendWebAPIAdfsAdd の場合と同様)。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO8.PNG)

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO7.PNG)

ToDoListService WebAPI を構成したときと同じように、ウィザードの残りの部分を続行します。 最後に、アプリケーショングループは次のようになります。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO5.PNG)

### <a name="modifying-the-todolistservice-code"></a>ToDoListService コードの変更

#### <a name="modifying-the-application-config"></a>アプリケーション構成の変更

* Web.config ファイルを開きます。
* 次のキーを変更する

| キー | 値 |
|:-|:-|
| ida: 対象ユーザー | ToDoListService WebAPI の構成中に AD FS に指定された ToDoListService の ID (例:)https://localhost:44321/ |
| ida: ClientID | ToDoListService WebAPI の構成中に AD FS に指定された ToDoListService の ID (例:)<https://localhost:44321/> </br>**Ida: Audience と ida: ClientID が相互に一致することが非常に重要です。** |
| ida:ClientSecret | これは、で ToDoListService クライアントを構成したときに生成されたシークレット AD FS AD FS |
| ida: AdfsMetadataEndpoint | これは AD FS メタデータの URL です。例:https://fs.anandmsft.com/federationmetadata/2007-06/federationmetadata.xml |
| ida: OBOWebAPIBase | これは、バックエンド API の呼び出しに使用するベースアドレスです。たとえば、https://localhost:44300 |
| ida:Authority | これは、AD FS サービスの URL です。例を次に示します。https://fs.anandmsft.com/adfs/ |

**Appsettings**ノード内の他のすべての IDA: XXXXXXX キーをコメントアウトまたは削除できます。

#### <a name="change-authentication-from-azure-ad-to-ad-fs"></a>認証を Azure AD から AD FS に変更する

* Startup.Auth.cs ファイルを開きます。
* 次のコードを削除します

    ```
    app.UseWindowsAzureActiveDirectoryBearerAuthentication(
    new WindowsAzureActiveDirectoryBearerAuthenticationOptions
    {
        Audience = ConfigurationManager.AppSettings["ida:Audience"],
        Tenant = ConfigurationManager.AppSettings["ida:Tenant"],
        TokenValidationParameters = new TokenValidationParameters{ SaveSigninToken = true }
    });
    ```

    with

    ```
    app.UseActiveDirectoryFederationServicesBearerAuthentication(
    new ActiveDirectoryFederationServicesBearerAuthenticationOptions
    {
        MetadataEndpoint = ConfigurationManager.AppSettings["ida:AdfsMetadataEndpoint"],
        TokenValidationParameters = new TokenValidationParameters()
    {
        SaveSigninToken = true,
        ValidAudience = ConfigurationManager.AppSettings["ida:Audience"]
    }
    });
    ```

#### <a name="modifying-the-todolistcontroller"></a>Todolistcontroller.cs の変更

System.web 拡張子への参照を追加します。 次のコードを置き換えて、クラスのメンバーを変更します。

```
//
// The Client ID is used by the application to uniquely identify itself to Azure AD.
// The App Key is a credential used by the application to authenticate to Azure AD.
// The Tenant is the name of the Azure AD tenant in which this application is registered.
// The AAD Instance is the instance of Azure, for example public Azure or Azure China.
// The Authority is the sign-in URL of the tenant.
//
private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];
private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];
private static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];
private static string appKey = ConfigurationManager.AppSettings["ida:AppKey"];

//
// To authenticate to the Graph API, the app needs to know the Grah API's App ID URI.
// To contact the Me endpoint on the Graph API we need the URL as well.
//
private static string graphResourceId = ConfigurationManager.AppSettings["ida:GraphResourceId"];
private static string graphUserUrl = ConfigurationManager.AppSettings["ida:GraphUserUrl"];
private const string TenantIdClaimType = "https://schemas.microsoft.com/identity/claims/tenantid";
```

with

```
//
// The Client ID is used by the application to uniquely identify itself to Azure AD.
// The client secret is the credentials for the WebServer Client

private static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];
private static string clientSecret = ConfigurationManager.AppSettings["ida:ClientSecret"];
private static string authority = ConfigurationManager.AppSettings["ida:Authority"];

// Base address of the WebAPI
private static string OBOWebAPIBase = ConfigurationManager.AppSettings["ida:OBOWebAPIBase"];
```

**名前に使用される要求を変更する**

AD FS は、Nmae 要求を発行していますが、NameIdentifier 要求を発行していません。 このサンプルでは、NameIdentifier を使用して、ToDo 項目に一意のキーを使用します。 わかりやすくするために、コードで Name 要求を使用して NameIdentifier を安全に削除することができます。 NameIdentifier のすべての出現箇所を検索し、名前に置き換えます。

**Post ルーチンと CallGraphAPIOnBehalfOfUser () の変更**

次のコードをコピーして ToDoListController.cs に貼り付け、Post と CallGraphAPIOnBehalfOfUser のコードを置き換えます。

```
// POST api/todolist
public async Task Post(TodoItem todo)
{
    if (!ClaimsPrincipal.Current.FindFirst("https://schemas.microsoft.com/identity/claims/scope").Value.Contains("user_impersonation"))
        {
        throw new HttpResponseException(new HttpResponseMessage { StatusCode = HttpStatusCode.Unauthorized, ReasonPhrase = "The Scope claim does not contain 'user_impersonation' or scope claim not found" });
        }

//
// Call the WebAPIOBO On Behalf Of the user who called the To Do list web API.
//

    string augmentedTitle = null;
    string custommessage = await CallGraphAPIOnBehalfOfUser();

    if (custommessage != null)
        {
            augmentedTitle = String.Format("{0}, Message: {1}", todo.Title, custommessage);
        }
        else
        {
            augmentedTitle = todo.Title;
        }

      if (null != todo && !string.IsNullOrWhiteSpace(todo.Title))
        {
            db.TodoItems.Add(new TodoItem { Title = augmentedTitle, Owner = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Name).Value });
            db.SaveChanges();
        }
      }

      public static async Task<string> CallGraphAPIOnBehalfOfUser()
      {
        string accessToken = null;
        AuthenticationResult result = null;
        AuthenticationContext authContext = null;
        HttpClient httpClient = new HttpClient();
        string custommessage = "";

//
// Use ADAL to get a token On Behalf Of the current user.  To do this we will need:
// The Resource ID of the service we want to call.
// The current user's access token, from the current request's authorization header.
// The credentials of this application.
// The username (UPN or email) of the user calling the API
//

        ClientCredential clientCred = new ClientCredential(clientId, clientSecret);
        var bootstrapContext = ClaimsPrincipal.Current.Identities.First().BootstrapContext as System.IdentityModel.Tokens.BootstrapContext;
        string userName = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Upn) != null ? ClaimsPrincipal.Current.FindFirst(ClaimTypes.Upn).Value : ClaimsPrincipal.Current.FindFirst(ClaimTypes.Email).Value;
        string userAccessToken = bootstrapContext.Token;
        UserAssertion userAssertion = new UserAssertion(bootstrapContext.Token, "urn:ietf:params:oauth:grant-type:jwt-bearer", userName);

        string userId = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Name).Value;
        authContext = new AuthenticationContext(authority, false);

        // In the case of a transient error, retry once after 1 second, then abandon.
        // Retrying is optional.  It may be better, for your application, to return an error immediately to the user and have the user initiate the retry.
        bool retry = false;
        int retryCount = 0;

        do
          {
              retry = false;
              try
                {
                    result = await authContext.AcquireTokenAsync(OBOWebAPIBase, clientCred, userAssertion);
                    //result = await authContext.AcquireTokenAsync(...);
                    accessToken = result.AccessToken;
                }
              catch (AdalException ex)
                {
                    if (ex.ErrorCode == "temporarily_unavailable")
                    {
                        // Transient error, OK to retry.
                        retry = true;
                        retryCount++;
                        Thread.Sleep(1000);
                    }
                }
          } while ((retry == true) && (retryCount < 1));

        if (accessToken == null)
          {
              // An unexpected error occurred.
              return (null);
          }

        // Once the token has been returned by ADAL, add it to the http authorization header, before making the call to access the To Do list service.
        httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

        // Call the WebAPIOBO.
        HttpResponseMessage response = await httpClient.GetAsync(OBOWebAPIBase + "/api/WebAPIOBO");


        if (response.IsSuccessStatusCode)
          {
              // Read the response and databind to the GridView to display To Do items.
              string s = await response.Content.ReadAsStringAsync();
              JavaScriptSerializer serializer = new JavaScriptSerializer();
              custommessage = serializer.Deserialize<string>(s);
              return custommessage;
          }
        else
          {
              custommessage = "Unsuccessful OBO operation : " + response.ReasonPhrase;
          }
        // An unexpected error occurred calling the Graph API.  Return a null profile.
        return (null);
    }
```

## <a name="running-the-solution"></a>ソリューションの実行

既定では、visual studio はデバッグにヒットしたときに1つのプロジェクトを実行するように構成されています。

* ソリューションを右クリックし、[プロパティ] を選択します。
* [プロパティ] ページで、[マルチスタートアッププロジェクト] を選択し、3つのエントリすべてについてアクションを [開始] に変更します。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO14.PNG)

F5 キーを押してソリューションを実行します

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO24.PNG)

[サインイン] ボタンをクリックします。 を使用してサインインするように求められ AD FS

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO25.PNG)

サインインした後、リストに ToDo 項目を追加します。 バックグラウンドで、ToDoListService に対して Post 操作を実行します。これにより、WebAPIOBO web API への投稿が行われます。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO26.PNG)

操作が正常に完了すると、項目がリストに追加され、OBO 認証フローを使用してアクセスされたバックエンド Web API からの追加のメッセージが表示されます。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO27.PNG)

Fiddler で詳細なトレースを確認することもできます。 Fiddler を起動し、HTTPS の暗号化解除を有効にします。 /Adfs/oautincludes エンドポイントに対して2つの要求が実行されていることがわかります。
最初の相互作用では、アクセスコードをトークンエンドポイントに提示し、 https://localhost:44321/ AD FS OBO のアクセストークンを取得します。 ![](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO22.PNG)

トークンエンドポイントとの2つ目のやり取りでは、 **on_behalf_of**として設定されている**requested_token_use** 、中間層 web サービス用に取得したアクセストークンを使用していることがわかり https://localhost:44321/ ます。
![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO23.PNG)

## <a name="next-steps"></a>次の手順
[AD FS の開発](../../ad-fs/AD-FS-Development.md)
