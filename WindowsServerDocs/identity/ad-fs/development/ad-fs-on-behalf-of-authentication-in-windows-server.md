---
ms.assetid: 5052f13c-ff35-471d-bff5-00b5dd24f8aa
title: On-Behalf-Of (OBO) の AD FS 2016 で OAuth を使用してを使用して、多層アプリケーションを構築します。
description: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 33d0bfa4139f16c90f3d79f5b61188b4d311538b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858943"
---
# <a name="build-a-multi-tiered-application-using-on-behalf-of-obo-using-oauth-with-ad-fs-2016"></a>On-Behalf-Of (OBO) の AD FS 2016 で OAuth を使用してを使用して、多層アプリケーションを構築します。

>適用先:Windows Server 2016

このチュートリアルではの-(OBO) の認証のため Windows Server 2016 TP5 で AD FS を使用して実装するための命令を提供します。 詳細についてお読みください OBO 認証は[開発者向けの AD FS のシナリオ](../../ad-fs/overview/AD-FS-Scenarios-for-Developers.md)

>警告:ここで作成できる例は、教育目的でのみです。 これらの手順では、モデルの必須の要素を公開する最も単純で最低限の実装です。 例では、エラー処理のすべての側面を含まない場合があり、その他の関連機能と OBO 認証の成功の取得にのみ焦点を当てています。

## <a name="overview"></a>概要

このサンプルでから作成していきます、認証フローを中間層の Web サービスにアクセスするクライアントと web サービスへのアクセス トークンを取得する認証済みのクライアントの代理として動作します。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO28.png)

認証フローが達成できる、サンプルを次に示します
1. クライアントが AD FS 承認エンドポイントに認証され、承認コード要求
2. 承認エンドポイントは、クライアントを認証コードを返します。
3. クライアントが認証コードを使用し、WebAPI としての中間層 Web サービスのアクセス トークンの要求に AD FS のトークン エンドポイントに表示します
4. AD FS では、中間層 Web サービスにアクセス トークンを返します。 中間層サービスを追加の機能のバックエンド web Api へのアクセスを必要があります。
5. クライアントは、中間層サービスを使用するのにアクセス トークンを使用します。
6. 中間層サービスは、AD FS のトークン エンドポイントにアクセス トークンを提供し、要求へのアクセス トークン - on-behalf-of のバックエンド web Api の認証されたユーザー
7. AD FS は、クライアントとして中間層サービス actiing にバックエンド web Api のアクセス トークンを返します
8. 中間層サービスでは、手順 7. で AD FS によって提供されるアクセス トークンを使用して、クライアントとして WebAPI バックエンドへのアクセスを必要な機能を実行します。

## <a name="sample-structure"></a>サンプルの構造

3 つのモジュールのサンプルを構成します。


モジュール | 説明
-------|------------
ToDoClient | ユーザーが対話するネイティブ クライアント
ToDoService | 中間層 web API バックエンド web Api 用のクライアントとして機能します。
WebAPIOBO | バックエンド web api ToDoService によってユーザーは、ToDoItem を追加するときに必要な操作を実行するために使用します。




## <a name="setting-up-the-development-box"></a>開発ボックスの設定

このチュートリアルでは、Visual Studio 2015 を使用します。 プロジェクトは、頻度の高い Active Directory Authentication Library (ADAL) を使用します。 ADAL をお読みくださいについて[Active Directory 認証ライブラリ .NET](https://msdn.microsoft.com/library/azure/mt417579.aspx)

このサンプルでは、SQL LocalDB v11.0 も使用します。 サンプルを操作する前に、SQL LocalDB をインストールします。

## <a name="setting-up-the-environment"></a>環境のセットアップ
私たちの基本的なセットアップで使用されます。

1. **DC**:AD FS をホストするドメインのドメイン コント ローラー
2. **AD FS サーバー**:ドメインの AD FS サーバー
3. **開発用コンピューター**:マシンがある Visual Studio がインストールされているし、サンプルを開発します。

2 つのマシンをする場合は、使用できます。 DC/ADFS と他のサンプルを開発するための 1 つです。

ドメイン コント ローラーと AD FS をセットアップする方法は、この記事の範囲外です。 追加の配置情報を参照してください。

- [AD DS の展開](../../ad-ds/deploy/AD-DS-Deployment.md)
- [AD FS の展開](../AD-FS-Deployment.md)

このサンプルは、Vittorio Bertocci によって作成された Azure に対する既存の OBO サンプルに基づいており、使用可能な[ここ](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof)します。 開発用コンピューターにプロジェクトを複製して、操作を開始するサンプルのコピーを作成する手順に従います。

## <a name="clone-or-download-this-repository"></a>複製するか、このリポジトリをダウンロード

シェルまたはコマンド ライン: から

    git clone https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof.git

## <a name="modifying-the-sample"></a>このサンプルを変更します。

WebAPI-OnBehalfOf-DotNet.sln ソリューションを開くとすぐに、ソリューションに 2 つのプロジェクトがあることがわかります

* **ToDoListClient**:これは、ユーザーが対話する OpenID クライアントとして機能します。
* **ToDoListService**:中間層の web サーバー アプリケーション/サービスがこれは、認証されたユーザーに別のバックエンド WebAPI OBO で対話が

ご覧のように、中間層 ToDoListService によってアクセスされるリソースとして機能するを後でもう 1 つのプロジェクトに追加する必要になります。

### <a name="configuring-ad-fs-for-the-client-and-webserver-app"></a>クライアントと web サーバー アプリの AD FS を構成します。

サンプルの現在のフォームでは、認証は、Azure AD に対して構成されます。 認証メカニズムを変更して、オンプレミスでデプロイ、AD FS に直接します。 そのために、サンプルのクライアントを認識する AD FS と web サーバー アプリがあるを構成する必要があります。

**アプリケーション グループを作成します。**

AD FS の管理 MMC を開き、新しいアプリケーション グループを追加します。 ネイティブのアプリケーションの web Api テンプレートを選択します。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO2.PNG)

[次へ] をクリックして、クライアント アプリに関する情報を提供するページが表示されます。 適切な名前をクライアントの AD FS でのアプリ クライアント識別子をコピーし、これは、visual studio でアプリケーションの構成で必要になります、後で使用する場所に保存します。

>注:実際に使用されていないネイティブ クライアントが発生した場合に、リダイレクト URI は、任意の URI を指定できます。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO11.PNG)

[次へ] をクリックして、WebAPI についての情報を提供するページが表示されます。 WebAPI の AD FS のエントリの適切な名前を入力し、ToDoListService 用 Visual Studio で参照する URI としてリダイレクト URI を入力します

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO16.PNG)

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO18.PNG)

次へ をクリックして、アクセス制御のポリシーの選択 ページが表示されます。 「許可するすべてのユーザー」ポリシー セクションで表示を確認します。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO1.PNG)

次へ をクリックして、アプリケーションのアクセス許可の構成 ページに表示されます。 このページでは、(既定でオン) openid と user_impersonation として許可されているスコープを選択します。 "User_impersonation"スコープでは、正常に AD FS からの on-behalf-of アクセス トークンを要求したりする必要があります。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO12.PNG)

次へ をクリックは、概要 ページが表示されます。 ウィザードの残りの部分と構成を完了します。

On-behalf-of 認証を有効にするためには、AD FS がクライアントにスコープ user_impersonation でアクセス トークンを返すことを確認する必要があります。 次の 3 つのカスタム規則を含める ToDoListServiceWebApi の要求の発行を変更します。

    @RuleName = "All claims"
    c:[]
    => issue(claim = c);

    @RuleName = "Issue open id scope"
    => issue(Type = "https://schemas.microsoft.com/identity/claims/scope", Value = "openid");

    @RuleName = "Issue user_impersonation scope"
    => issue(Type = "https://schemas.microsoft.com/identity/claims/scope", Value = "user_impersonation");

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO10.PNG)

**アプリケーション グループ内のクライアントとして ToDoListService を追加します。**

この段階では、クライアントとは、リソースとしてだけでなく動作する web サーバー アプリ用に AD FS の追加エントリを作成する必要があります。 作成したアプリケーション グループを開き、[アプリケーションの追加] をクリックします。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO15.PNG)

"MySampleGroup に新しいアプリケーションの追加 ページが表示されます。 そのページで、スタンドアロン アプリケーションとして「サーバーのアプリケーションまたは web サイト」を選択します。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO19.PNG)

[次へ] をクリックして、アプリケーションの詳細を提供するページが表示されます。 [名前] セクションの構成エントリの適切な名前を提供します。 クライアント識別子が、ToDoListServiceWebAPI の識別子と同じであることを確認します。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO20.PNG)

[次へ] をクリックして、アプリケーションの資格情報を構成するページが表示されます。 「共有シークレットを生成する」をクリックします。 自動的に生成されたシークレットが表示されます。 Visual studio で、ToDoListService 構成中には、必要これには、いくつかの場所にシークレットをコピーします。


![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO17.PNG)

[次へ] をクリックし、ウィザードを完了します。

### <a name="modifying-the-todolistclient-code"></a>ToDoListClient コードを変更します。

#### <a name="modify-the-application-config"></a>アプリケーション構成を変更します。

移動先では、WebAPI OnBehalfOf-DotNet ソリューションで、ToDoListClient プロジェクトしています。 App.config ファイルを開き、次の変更

* コメント ida: テナント キーのエントリ
* Ida: RedirectURI には、AD FS で、MySampleGroup_ClientApplication を構成するときに指定した任意の URI が」と入力します。
* Ida: ClientID キーの場合、クライアント ID です。 AD FS は、MySampleGroup_ClientApplication を構成するときに指定を提供します。
* AD FS で、ToDoListServiceWebApi を構成するときに指定した ida: ToDoListResourceID の場合は、リソース ID
* コメント キー ida: AADInstance
* Ida: ToDoListBaseAddress、ToDoListServiceWebApi のリソース ID を入力します。 これは、ToDoList web Api の呼び出し中に使用されます。
* キーの ida: 機関を追加し、AD FS の URI として値を指定します。

**AppSettings** App.Config では次のように検索する必要があります。

    <appSettings>
    <!--<add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" />-->
    <add key="ida:ClientId" value="c7f7b85c-497c-4589-877f-b17a0bd13398" />
    <add key="ida:RedirectUri" value="https://arbitraryuri.com/" />
    <add key="ida:TodoListResourceId" value="https://localhost:44321/" />
    <!--<add key="ida:AADInstance" value="https://login.microsoftonline.com/{0}" />-->
    <add key="ida:TodoListBaseAddress" value="https://localhost:44321" />
    <add key="ida:Authority" value="https://fs.anandmsft.com/adfs/"/>
    </appSettings>

#### <a name="modifying-the-code"></a>コードを変更します。

**MainWindow.xaml.cs**

アプリケーション構成からテナント情報を読み取る行をコメントします。

    //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];
    //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];

変更する権限を文字列の値

    private static string authority = ConfigurationManager.AppSettings["ida:Authority"];

ToDoListResourceId と ToDoListBaseAddress の正しい値を読み取るコードを変更します。

    private static string todoListResourceId = ConfigurationManager.AppSettings["ida:TodoListResourceId"];
    private static string todoListBaseAddress = ConfigurationManager.AppSettings["ida:TodoListBaseAddress"];

関数では、MainWindow() として authcontext 初期化を変更します。

    authContext = new AuthenticationContext(authority, false);

### <a name="adding-the-backend-resource"></a>バックエンド リソースを追加します。

On-behalf-of フローを完了するには - on-behalf-of ToDoListService がアクセスするためのバックエンド リソースを作成する必要があります。 認証されたユーザー。 バックエンド リソースの選択、必要に応じて変わります。 ただしこのサンプルの目的は、基本的な web Api を作成することができます。

* ソリューション エクスプ ローラーでソリューション ' WebAPI OnBehalfOf DotNet' を右クリックし、[追加] 新しいプロジェクト
* ASP.NET Web アプリケーション テンプレートを選択します。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO4.PNG)

* '認証の変更' で次のプロンプトのクリックで
* '職場と学校のアカウント を選択し、右のドロップダウン リストで「オンプレミス」を選択します。
* AD FS の展開に federationmetadata.xml パスを入力して、アプリの URI を入力して (ここでは、任意の URI を提供および後で変更されます)、プロジェクトをソリューションに追加するのには、[ok] をクリックします。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO9.PNG)

* 右は、作成した新しいプロジェクトの下の ソリューション エクスプ ローラーで、コント ローラーをクリックします。 コント ローラー-> 追加 を選択
* テンプレートの選択で、'Web API 2 コント ローラー - 空' を選択し、[ok] をクリックします。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO3.PNG)

* 適切なコント ローラーの名前を付けます

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO13.PNG)

* コント ローラーで、次のコードを追加します。


        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Net;
        using System.Net.Http;
        using System.Web.Http;
        namespace WebAPIOBO.Controllers
        {
            public class WebAPIOBOController : ApiController
            {
                public IHttpActionResult Get()
                {
                    return Ok("WebAPI via OBO");
                }
            }
        }

WebAPI WebAPIOBO の Get 要求は、すべてのユーザーとは、このコードは、文字列を戻ります。

### <a name="adding-the-new-backend-webapi-to-ad-fs"></a>AD FS に、新しいバックエンド web Api を追加します。

MySampleGroup アプリケーション グループを開きます。 追加のアプリケーションと Web API テンプレートの選択 をクリックし、次へ をクリックします。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO6.PNG)

Web API の構成 ページでは、WebAPI エントリと、識別子の適切な名前を指定します。 識別子 (BackendWebAPIAdfsAdd に対して実行したものに類似) が visual studio で SSL URL WebAPIOBO プロジェクトからの値があります。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO8.PNG)

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO7.PNG)

ウィザードの残りの部分で同じとして継続 ToDoListService web Api を構成するときにします。 最後に、アプリケーション グループは以下のようになる必要があります。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO5.PNG)


### <a name="modifying-the-todolistservice-code"></a>ToDoListService コードを変更します。

#### <a name="modifying-the-application-config"></a>アプリケーション構成の変更

* Web.config ファイルを開く
* 次のキーを変更します。

| Key | 値 |
|:-----|:-------|
|ida:Audience| ToDoListService WebAPI を構成するときに AD FS に渡されると ToDoListService の ID https://localhost:44321/|
|ida: ClientID| ToDoListService WebAPI を構成するときに AD FS に渡されると ToDoListService の ID https://localhost:44321/ </br>**Ida: 対象ユーザーと ida: ClientID が互いに一致することが重要です。**|
|ida:ClientSecret| これは AD FS で、ToDoListService クライアントを構成するときに AD FS が生成したシークレットです。|
|ida: ADFSMetadata| これは、AD FS のメタデータの URL の例です。 https://fs.anandmsft.com/federationmetadata/2007-06/federationmetadata.xml|
|ida: OBOWebAPIBase| これは、基本のアドレスなどをバックエンド API を呼び出すために使用します。 https://localhost:44300|
|ida 機関:| これは、AD FS サービスの URL の例 https://fs.anandmsft.com/adfs/|


キーを他のすべての ida: XXXXXXX、 **appsettings**ノードをコメント アウトまたは削除できます

#### <a name="change-authentication-from-azure-ad-to-ad-fs"></a>Azure AD への AD FS からの認証の変更

* Startup.Auth.cs ファイルを開く
* 次のコードを削除します。

        app.UseWindowsAzureActiveDirectoryBearerAuthentication(
            new WindowsAzureActiveDirectoryBearerAuthenticationOptions
            {
                Audience = ConfigurationManager.AppSettings["ida:Audience"],
                Tenant = ConfigurationManager.AppSettings["ida:Tenant"],
                TokenValidationParameters = new TokenValidationParameters{ SaveSigninToken = true }
            });

を、次のように置き換えます。

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

#### <a name="modifying-the-todolistcontroller"></a>変更、ToDoListController

System.Web.Extensions への参照を追加します。 次のコードを置き換えることにより、クラスのメンバーを変更します。

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

を、次のように置き換えます。

    //
    // The Client ID is used by the application to uniquely identify itself to Azure AD.
    // The client secret is the credentials for the WebServer Client

    private static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];
    private static string clientSecret = ConfigurationManager.AppSettings["ida:ClientSecret"];
    private static string authority = ConfigurationManager.AppSettings["ida:Authority"];

    // Base address of the WebAPI
    private static string OBOWebAPIBase = ConfigurationManager.AppSettings["ida:OBOWebAPIBase"];

**名に使用される、要求を変更します。**

AD FS から Nmae 要求を発行しましたが、NameIdentifier 要求を発行していないこと。 このサンプルでは、NameIdentifier を使用して、ToDo 項目のキーを一意にします。 わかりやすくするため、コードで名前クレームに NameIdentifier を安全に削除できます。 検索し、NameIdentifier のすべての出現箇所を名前に置き換えます。

**Post および CallGraphAPIOnBehalfOfUser() を変更します。**

コピーし ToDoListController.cs で次のコードを貼り付けるし、Post および CallGraphAPIOnBehalfOfUser のコードに置き換えます

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
        //      The Resource ID of the service we want to call.
        //      The current user's access token, from the current request's authorization header.
        //      The credentials of this application.
        //      The username (UPN or email) of the user calling the API
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
                result = await authContext.AcquireTokenAsync(...);
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

## <a name="running-the-solution"></a>ソリューションの実行


既定では、visual studio はデバッグを実行するに達した場合に、1 つのプロジェクトを実行する構成します。

* ソリューションと [プロパティ] を右クリックします。
* [プロパティ] ページで複数のスタートアップ プロジェクトを選択し、3 つすべてのエントリを起動するアクションを変更します。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO14.PNG)

F5 キーを押すし、ソリューションの実行

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO24.PNG)

サインイン ボタンをクリックします。 AD FS を使用してサインインを求められます

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO25.PNG)

後でサインイン、一覧で、ToDo 項目を追加します。 バック グラウンドでの ToDoListService WebAPIOBO web API へのポストをさらに実行する Post 操作を行うにはでしょう。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO26.PNG)

成功した操作では、OBO 承認のフローを使用してアクセスされた Web API のバックエンドから、項目が追加のメッセージを使用してリストに追加されたことがわかります。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO27.PNG)

Fiddler の詳細なトレースを確認できます。 Fiddler を起動し、HTTPS の復号化を有効にします。 /Adfs/oautincludes エンドポイントに 2 つの要求を行ったことを確認できます。
最初の相互作用の トークン エンドポイントへのアクセス コードし、アクセスのトークンを取得しました https://localhost:44321/ ![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO22.PNG)

トークン エンドポイントに 2 つ目の操作であることを確認できます**requested_token_use**として設定**on_behalf_of** つまり、中間層のwebサービスの取得したアクセストークンを使用していることと https://localhost:44321/ - on-behalf-of トークンを取得するアサーションとして。
![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO23.PNG)

## <a name="next-steps"></a>次の手順
[AD FS の開発](../../ad-fs/AD-FS-Development.md)  
