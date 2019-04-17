---
ms.assetid: 5052f13c-ff35-471d-bff5-00b5dd24f8aa
title: "On-Behalf-Of (OBO) AD FS 2016 で OAuth を使用してを使用して、多層アプリケーションを構築します。"
description: 
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 8940cde2b78ce3ead499263e6fba0fbe28aae695
ms.sourcegitcommit: c16a2bf1b8a48ff267e71ff29f18b5e5cda003e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/28/2018
---
# <a name="build-a-multi-tiered-application-using-on-behalf-of-obo-using-oauth-with-ad-fs-2016"></a>On-Behalf-Of (OBO) AD FS 2016 で OAuth を使用してを使用して、多層アプリケーションを構築します。

>Windows Server 2016 の適用対象:

このチュートリアルでは、上のため (OBO) 認証では、Windows Server 2016 TP5 AD FS を使用して実装するための命令を提供します。  O についてお読みください OBO 認証[開発者向けの AD FS のシナリオ](../../ad-fs/overview/AD-FS-Scenarios-for-Developers.md)

>警告: ここで構築する例は、教育用にのみです。 次に挙げる手順では、モデルの必須の要素を公開する最も簡単な最小限の実装のためです。 この例は、エラー処理のすべての側面を含まない場合がありますおよびその他の関連機能 OBO 認証が成功したの取得にのみ重点を置いています。

## <a name="overview"></a>概要

このサンプルでは作成します、中間層 Web サービスは、クライアントにアクセスして、Web サービスが認証されたアクセス トークンを取得するクライアントに代わって動作し、認証フロー。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO28.PNG)

サンプルを反映した認証フローを次に示します
1. クライアントが AD FS 認証の終点に認証され、認証コードを要求します。
2. エンドポイントの authorization がクライアントに認証コードを返します
3. クライアントが認証コードを使用して、WebAPI として中間層 Web サービスのアクセス トークンの要求に AD FS トークン エンドポイントに表示
4. AD FS では、中間層 Web サービスへのアクセス トークンを返します。 中間層サービスは、追加の機能のバックエンド WebAPI へのアクセスに必要があります。
5. クライアントは、中間層サービスを使用するのにアクセス トークンを使用します。
6. 中間層サービスは、AD FS トークン エンドポイントにアクセス トークンを提供し、要求アクセス トークンのバックエンド WebAPI 上のための認証されたユーザー
7. AD FS は、中間層サービス actiing をバックエンド WebAPI のアクセス トークンをクライアントとして返します
8. 中間層サービスは手順 7 での AD FS によって提供されたアクセス トークンを使用してクライアントとして WebAPI バックエンドにアクセスし、必要な機能を実行するには

## <a name="sample-structure"></a>サンプルの構造

サンプルを次の 3 つのモジュールを構成します。


モジュール | 説明
-------|------------
ToDoClient | ユーザーが対話するネイティブ クライアント
ToDoService | 中央層 Web バックエンド WebAPI 用のクライアントとして動作する API
WebAPIOBO | バックエンド Web ToDoService によってユーザーが、ToDoItem を追加するときに必要な操作を実行するために使用する api




## <a name="setting-up-the-development-box"></a>開発のボックスを設定します。

このチュートリアルでは、Visual Studio 2015 を使用します。 頻度の高いプロジェクトが Active Directory 認証ライブラリ (ADAL) を使用します。 お読みください ADAL について[Active Directory 認証ライブラリ .NET](https://msdn.microsoft.com/library/azure/mt417579.aspx)

このサンプルでは、SQL LocalDB v11.0 も使用します。 サンプルで作業する前に SQL LocalDB をインストールします。

## <a name="setting-up-the-environment"></a>環境のセットアップ
おについては、基本設定を作成します。

1. **DC**: AD FS をホストするドメインのドメイン コントローラー
2. **AD FS サーバー**: ドメインの AD FS サーバー
3. **開発マシン**: マシンお Visual Studio がインストールされている、サンプルを開発します。

2 つだけのマシンをする場合は、使用、できます。 DC/ADFS と他のサンプルを開発するための 1 つです。

ドメイン コントローラーと AD FS をセットアップする方法は、この記事の範囲外です。 追加の展開をご覧ください。

- [AD DS の展開](../../ad-ds/deploy/AD-DS-Deployment.md)
- [AD FS の展開](../AD-FS-Deployment.md)

このサンプルは、Azure Vittorio Bertocci によって作成されたに対して既存の OBO サンプルに基づいており、利用可能な[ここ](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof)します。 開発用コンピューターで、プロジェクトの複製操作を開始するサンプルのコピーを作成するための手順に従います。

## <a name="clone-or-download-this-repository"></a>複製またはダウンロードこのリポジトリ

シェルまたはコマンド ライン: から

    git clone https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof.git

## <a name="modifying-the-sample"></a>サンプルを変更します。

ソリューション WebAPI-OnBehalfOf-DotNet.sln を開くとすぐにわかりますソリューション - に 2 つのプロジェクトがあること

* **ToDoListClient**: これは、ユーザーは対話 OpenID クライアントとして動作
* **ToDoListService**: これは、中間層 WebServer アプリである/service を認証されたユーザーに別のバックエンド WebAPI OBO と対話は

ご覧のように、おは中間層 ToDoListService によってアクセスされるリソースとして機能し、後でもう 1 つのプロジェクトを追加する必要があります。

### <a name="configuring-ad-fs-for-the-client-and-webserver-app"></a>クライアントと Web サーバー アプリの AD FS を構成します。

サンプルの現在のフォーム認証が Azure AD に対して実行するように構成します。 認証メカニズムを変更して、オンプレミス展開されている AD FS に向けて、ダイレクトします。 これを行うためには、サンプルで、クライアントを認識するように AD FS と Web サーバーのアプリがあるを構成する必要があります。

**アプリケーション グループを作成します。**

[AD FS 管理] mmc スナップインを開き、新しいアプリケーション グループを追加します。 WebAPI-ネイティブ-アプリケーション テンプレートを選択します。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO2.PNG)

[次へ] をクリックして、クライアント アプリに関する情報を提供するためのページに表示されます。 クライアントの AD FS でのアプリに適切な名前を提供します。 クライアントの識別子をコピーし、これは、visual studio でアプリケーションの構成に必要がありますに応じて後でアクセスできる場所に保存します。

>注: URI にリダイレクトすることができます、任意の URI 実際に使用されていないネイティブ クライアントが発生した場合

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO11.PNG)

[次へ] をクリックし、WebAPI に関する情報を提供するためのページに表示されます。 WebAPI の AD FS のエントリに対して適切な名前を付けるし、ToDoListService の Visual Studio で「URI としてリダイレクト URI を入力してください

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO16.PNG)

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO18.PNG)

[次へ] をクリックし、アクセス制御のポリシーの選択] ページが表示されます。 「許可 everyone」[ポリシー] セクションに表示されることを確認します。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO1.PNG)

[次へ] をクリックし、アプリケーションのアクセス許可の構成] ページに表示されます。 このページでは、(既定で選択) openid や user_impersonation として、許可されているスコープを選択します。 スコープ 'user_impersonation' ができるように正常に AD FS からでのためのアクセス トークンを要求する必要があります。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO12.PNG)

[次へ] をクリックは、[概要] ページが表示されます。 ウィザードの残りの部分を通過し、構成を完了します。

上のための認証を有効にするためには、AD FS に、クライアントにスコープ user_impersonation でアクセス トークンが返されることを確認する必要があります。 次の 3 つのカスタム規則を含める ToDoListServiceWebApi の信頼性情報の発行を変更します。

    @RuleName = "All claims"
    c:[]
    => issue(claim = c);

    @RuleName = "Issue open id scope"
    => issue(Type = "https://schemas.microsoft.com/identity/claims/scope", Value = "openid");

    @RuleName = "Issue user_impersonation scope"
    => issue(Type = "https://schemas.microsoft.com/identity/claims/scope", Value = "user_impersonation");

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO10.PNG)

**アプリケーション グループ内のクライアントとして ToDoListService を追加する方法**

この段階では、AD fs とリソースとしてだけでなく、クライアントとして動作する Web サーバー アプリの追加エントリを作成する必要があります。 作成したアプリケーション グループを開き、[アプリケーションの追加] をクリックします。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO15.PNG)

"MySampleGroup に新しいアプリケーションの追加] ページが表示されます。 そのページで、スタンドアロン アプリケーションとして「サーバーのアプリケーションまたは Web サイト」を選択します

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO19.PNG)

[次へ] をアプリケーションの詳細を提供するページが表示されます。 [名前] セクションで構成のエントリの名前を適切なを指定します。 クライアント識別子、ToDoListServiceWebAPI の識別子と同じであることを確認します。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO20.PNG)

[次へ] をクリックしするアプリケーションの資格情報の構成] ページが表示されます。 "共有シークレットを生成する] をクリックします。 自動的に生成されたシークレットが表示されます。 するため、必要な visual studio で、ToDoListService 設定中には、いくつかの場所にシークレットをコピーします。


![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO17.PNG)

[次へ] をクリックし、ウィザードを完了します。

### <a name="modifying-the-todolistclient-code"></a>ToDoListClient コードを変更します。

#### <a name="modify-the-application-config"></a>アプリケーション構成を変更します。

[移動先には、ToDoListClient ソリューションのプロジェクトに WebAPI-な-DotNet ができました。 App.config ファイルを開き、次の変更

* コメント ida: テナント キー エントリ
* Ida: RedirectURI が AD FS で、MySampleGroup_ClientApplication を構成するときに提供されている任意の URI を入力します。
* Ida: ClientID キー ID の識別子、MySampleGroup_ClientApplication の構成中に AD FS がなったクライアントを提供します。
* AD FS で、ToDoListServiceWebApi を構成するときに指定した ida: ToDoListResourceID リソース ID を提供するため
* コメント キー ida: AADInstance
* Ida: ToDoListBaseAddress、ToDoListServiceWebApi のリソースの ID を入力します。 これは、ToDoList WebAPI を呼び出すときに使用されます。
* Ida: 機関キーを追加し、AD FS の URI と値を提供します。

**AppSettings** App.Config は次のように確認する必要があります。

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

アプリケーション構成からテナント情報を読み取って、行のコメント

    //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];
    //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];

権限を文字列の値を変更します。

    private static string authority = ConfigurationManager.AppSettings["ida:Authority"];

ToDoListResourceId と ToDoListBaseAddress の正しい値を読み取るためのコードを変更します。

    private static string todoListResourceId = ConfigurationManager.AppSettings["ida:TodoListResourceId"];
    private static string todoListBaseAddress = ConfigurationManager.AppSettings["ida:TodoListBaseAddress"];

関数では、MainWindow() として authcontext 初期化を変更します。

    authContext = new AuthenticationContext(authority, false);

### <a name="adding-the-backend-resource"></a>バックエンドのリソースを追加します。

上のためのフローを完了するためには、上のため、ToDoListService にアクセスするバックエンド リソースを作成する必要があります、認証されたユーザー。 バックエンドのリソースの選択は、要件に従った異なりますが、このサンプルの目的は、基本的な WebAPI を作成することができます。

* ソリューション エクスプ ローラーでソリューション ' WebAPI な DotNet' を右クリックし、[追加] の新しいプロジェクト
* ASP.NET Web アプリケーション テンプレートを選択します。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO4.PNG)

* '変更認証' のプロンプトをクリックして、[次へ] の
* 作業学校のアカウントを選択し、[' オンプレミス ' 右ドロップ ダウン リスト
* AD FS 展開の federationmetadata.xml パスを入力し、アプリの URI を入力して (現時点では、任意の URI を入力して、後で変更されます)、プロジェクトをソリューションに追加するのには、[OK] をクリックします。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO9.PNG)

* 右クリック コントローラーで新しいプロジェクトの作成 [ソリューション エクスプ ローラーでします。 コントローラー]-> [追加] を選択
* テンプレートの選択で、"コントローラーの空の Web API 2"を選択し、[OK] をクリックします。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO3.PNG)

* 適切なコントローラーの名前を付ける

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO13.PNG)

* コントローラーで、次のコードを追加します。


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

このコードは単に返す文字列 WebAPI WebAPIOBO の Get 要求は、すべてのユーザーとき

### <a name="adding-the-new-backend-webapi-to-ad-fs"></a>AD FS に、新しいバックエンド WebAPI を追加します。

MySampleGroup アプリケーション グループを開きます。 追加のアプリケーションや Web API のテンプレートの選択] をクリックし、[次へ] をクリックします。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO6.PNG)

[Web API の構成] ページで、WebAPI エントリと識別子の適切な名前を提供します。 識別子は、visual studio (BackendWebAPIAdfsAdd を行ったに似ています) で WebAPIOBO プロジェクトから SSL URL の値をする必要があります。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO8.PNG)

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO7.PNG)

ウィザードの残りの部分を同じとして継続 ToDoListService WebAPI お構成されている場合。 最後に、アプリケーション グループは次のようになります必要があります。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO5.PNG)


### <a name="modifying-the-todolistservice-code"></a>ToDoListService コードを変更します。

#### <a name="modifying-the-application-config"></a>アプリケーション構成の変更

* Web.config ファイルを開く
* 次のキーを変更します。

| キー | 値 |
|:-----|:-------|
|ida: 対象ユーザー| ように指定された AD fs ToDoListService WebAPI を構成するときに https://localhost:44321/ ToDoListService ID|
|ida: ClientID| ように指定された AD fs ToDoListService WebAPI を構成するときに https://localhost:44321/ ToDoListService ID </br>**Ida: 対象者と ida: ClientID が互いに一致することが非常に重要します。**|
|ida: ClientSecret| これは、AD FS で ToDoListService クライアントを構成していたときに生成された AD FS シークレット|
|ida: ADFSMetadata| これは、AD FS のメタデータ、https://fs.anandmsft.com/federationmetadata/2007-06/federationmetadata.xml などの URL|
|ida: OBOWebAPIBase| これは、アドレスが、基本 https://localhost:44300 などのバックエンド API を呼び出すを使用します。|
|ida: 機関| これは、例 https://fs.anandmsft.com/adfs/、AD FS サービスの URL|


その他のすべての ida: XXXXXXX キー、**appsettings**ノードをコメント アウトまたは削除されたことができます

#### <a name="change-authentication-from-azure-ad-to-ad-fs"></a>Azure AD に AD FS からの認証を変更します。

* Startup.Auth.cs ファイルを開く
* 次のコードを削除します。

        app.UseWindowsAzureActiveDirectoryBearerAuthentication(
            new WindowsAzureActiveDirectoryBearerAuthenticationOptions
            {
                Audience = ConfigurationManager.AppSettings["ida:Audience"],
                Tenant = ConfigurationManager.AppSettings["ida:Tenant"],
                TokenValidationParameters = new TokenValidationParameters{ SaveSigninToken = true }
            });

で

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

#### <a name="modifying-the-todolistcontroller"></a>ToDoListController を変更します。

System.Web への参照を追加します。拡張機能です。 次のコードを置き換えることにより、クラスのメンバーを変更します。

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

で

    //
    // The Client ID is used by the application to uniquely identify itself to Azure AD.
    // The client secret is the credentials for the WebServer Client

    private static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];
    private static string clientSecret = ConfigurationManager.AppSettings["ida:ClientSecret"];
    private static string authority = ConfigurationManager.AppSettings["ida:Authority"];

    // Base address of the WebAPI
    private static string OBOWebAPIBase = ConfigurationManager.AppSettings["ida:OBOWebAPIBase"];

**名で使用して信頼性情報を変更します。**

Nmae の要求を発行しました AD FS からが NameIdentifier 要求を発行していないしました。 サンプルでは、ToDo 項目に一意にキーに NameIdentifier を使用します。 わかりやすくするため、コードで名要求の NameIdentifier を安全に削除できます。 検索し、NameIdentifier のすべての出現を名で置き換えてください。

**Post および CallGraphAPIOnBehalfOfUser() を変更します。**

コピーおよび ToDoListController.cs で次のコードを貼り付けます Post および CallGraphAPIOnBehalfOfUser コードに置き換えます

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
                result = authContext.AcquireToken(OBOWebAPIBase, clientCred, userAssertion);
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

## <a name="running-the-solution"></a>ソリューションを実行しています。


既定で visual studio を実行するデバッグをヒットしたときに、1 つのプロジェクトを実行するように構成します。

* ソリューション、[プロパティ] を右クリックします。
* [プロパティ] ページで複数のスタートアップ プロジェクトを選択し、次の 3 つのすべてのエントリを開始するアクションを変更します。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO14.PNG)

F5 キーを押すし、ソリューションを実行します。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO24.PNG)

[サインイン] ボタンをクリックします。 AD FS を使用してサインインするように求められます

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO25.PNG)

後でサインイン、ToDo 項目を一覧に追加します。 バック グラウンドしようとしてこの WebAPIOBO Web API への Post 操作は、さらに ToDoListService に Post 操作を実行します。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO26.PNG)

正常な操作で、項目がバックエンド OBO 認証フローを使用してアクセスされた Web API から、その他のメッセージの一覧に追加されたことが表示されます。

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO27.PNG)

Fiddler で詳細なトレースを表示できます。 Fiddler を起動し、HTTPS 復号化を有効にします。 /Adfs/oautincludes エンドポイントに 2 つの要求を行うことを確認できます。
最初の操作でトークン エンドポイントにアクセス コードを提示して https://localhost:44321/ のアクセス トークンを取得![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO22.PNG)

トークンのエンドポイントと 2 つ目の相互作用であることを確認できます**requested_token_use**として設定**on_behalf_of**上のためのトークンを取得するアサーションとして https://localhost:44321/ すなわち、中間層 Web サービスの取得したアクセス トークンを使用するとします。
![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO23.PNG)

## <a name="next-steps"></a>次の手順
[AD FS の開発](../../ad-fs/AD-FS-Development.md)  
