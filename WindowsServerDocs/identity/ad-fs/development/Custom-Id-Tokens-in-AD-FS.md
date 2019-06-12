---
title: AD FS 2016 で OpenID Connect または OAuth を使用する場合は id_token で出力された以降にする要求をカスタマイズします。
description: AD FS 2016 以降でのカスタム id トークンの概念の技術概要
author: anandyadavmsft
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.reviewer: anandy
ms.technology: identity-adfs
ms.openlocfilehash: 04573aa13689a0e6744b01a0fbf8b11b622b2706
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445470"
---
# <a name="customize-claims-to-be-emitted-in-idtoken-when-using-openid-connect-or-oauth-with-ad-fs-2016-or-later"></a>AD FS 2016 で OpenID Connect または OAuth を使用する場合は id_token で出力された以降にする要求をカスタマイズします。

## <a name="overview"></a>概要
記事[ここ](native-client-with-ad-fs.md)OpenID Connect のサインオン用に AD FS を使用するアプリをビルドする方法を示します。 ただし、既定では、id_token で使用できる要求の固定セットだけです。 AD FS 2016 と以降のリリースには、OpenID Connect のシナリオで id_token をカスタマイズする機能が搭載されています。

## <a name="when-are-custom-id-token-used"></a>カスタム ID が場合に使用されるトークンですか?
特定のシナリオでは、クライアント アプリケーションにアクセスしようとするリソースがないことができます。 そのため、アクセス トークンは本当に必要ありません。 このような場合、クライアント アプリケーションには、のみ、ID トークンですがいくつか追加の要求のヘルプで、機能を本質的には必要があります。

## <a name="what-are-the-restrictions-on-getting-custom-claims-in-id-token"></a>ID でカスタム要求のトークンの取得に関する制限事項とは

### <a name="scenario-1"></a>例 1

![制限](media/Custom-Id-Tokens-in-AD-FS/res1.png)

1.  response_mode は form_post として設定します。
2.  パブリック クライアントのみで入手できますカスタム クレーム ID トークン
3.  証明書利用者のパーティ識別子 (Web API 識別子) をクライアント識別子と同じにする必要があります。

### <a name="scenario-2"></a>シナリオ 2

![制限](media/Custom-Id-Tokens-in-AD-FS/restrict2.png)

[KB4019472](https://support.microsoft.com/help/4019472/windows-10-update-kb4019472) AD FS サーバーにインストールされています。
1.  response_mode は form_post として設定します。
2.  パブリックと機密情報の両方のクライアントで取得できますカスタム クレーム ID トークン
3.  クライアント-RP ペアには、スコープ allatclaims を割り当てます。
次の例に示すように Grant ADFSApplicationPermission コマンドレットを使用して、スコープを割り当てることができます。

``` powershell
Grant-AdfsApplicationPermission -ClientRoleIdentifier "https://my/privateclient" -ServerRoleIdentifier "https://rp/fedpassive" -ScopeNames "allatclaims","openid"
```

## <a name="creating-and-configuring-an-oauth-application-to-handle-custom-claims-in-id-token"></a>作成して、ID トークンのカスタム要求を処理するために OAuth アプリケーションの構成
作成し、カスタム クレームと ID トークンを受信するための AD FS でアプリケーションを構成するのには、次の手順に従います。

### <a name="create-and-configure-an-application-group-in-ad-fs-2016-or-later"></a>作成し、AD FS 2016 以降でアプリケーション グループの構成

1. AD FS の管理、アプリケーション グループを右クリックし、選択**アプリケーション グループの追加**します。

2. アプリケーション グループ ウィザードで、名前の入力**ADFSSSO**クライアント サーバー アプリケーションを選択し、 **web アプリケーションにアクセスするネイティブ アプリケーション**テンプレート。 **[次へ]** をクリックします。

   ![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap1.png)

3. コピー、**クライアント識別子**値。  これは後で値として使用、ida: ClientId、アプリケーションの web.config ファイルでの。

4. 次の入力**リダイレクト URI:**  -  **https://localhost:44320/** します。  **[追加]** をクリックします。 **[次へ]** をクリックします。

   ![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap2.png)

5. **Web API の構成**画面で、次の入力**識別子** -  **https://contoso.com/WebApp** します。  **[追加]** をクリックします。 **[次へ]** をクリックします。  この値の後で使用する**ida: ResourceID**アプリケーションの web.config ファイルにします。

   ![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap3.png)

6. **へのアクセス制御ポリシーの選択**画面で、 **[のすべてのユーザーに許可]** をクリック**次**。

   ![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap4.png)

7. **アプリケーションのアクセス許可を構成する**確認画面で、 **openid**と**allatclaims**が選択されており、クリックして **[次へ]** 。

   ![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap5.png)

8. **概要**画面で、**次**します。  

   ![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap6.png)

9. **完了**画面で、**閉じる**します。

10. AD FS の管理には、すべてのアプリケーション グループの一覧を取得するアプリケーション グループをクリックします。 右クリックして**ADFSSSO**選択**プロパティ**します。 選択**ADFSSSO - Web API**  をクリック**を編集しています.**

    ![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap7.png)

11. **ADFSSSO - Web API プロパティ**画面で、 **[発行変換規則]** タブでをクリックし、**規則の追加.**

    ![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap8.png)

12. **変換要求規則追加ウィザード**画面で、**カスタム規則を使用して要求を送信する**ドロップダウン リストからをクリック**次へ**

    ![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap9.png)

13. **変換要求規則追加ウィザード**画面で、入力**ForCustomIDToken**で**要求規則名**次の要求の規則と**Custom rule**. **[Finish]** (完了) をクリックする

    ```  
    x:[]
    => issue(claim=x);  
    ```

    ![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap10.png)

```

>[!NOTE]
>You can also use PowerShell to assign the allatclaims and openid scopes
>``` powershell
Grant-AdfsApplicationPermission -ClientRoleIdentifier "[Client ID from #3 above]" -ServerRoleIdentifier "[Identifier from #5 above]" -ScopeNames "allatclaims","openid"
```

### <a name="download-and-modify-the-sample-application-to-emit-custom-claims-in-idtoken"></a>ダウンロードして、id_token に含まれるカスタムの要求を出力するサンプル アプリケーションの変更

このセクションでは、サンプル Web アプリをダウンロードして Visual Studio で変更する方法について説明します。   Azure AD のサンプルを使用する[ここ](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)します。  

サンプル プロジェクトをダウンロードし、Git Bash を使用して、次を入力します。  

```  
git clone https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect  
```  

![AD FS の OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_1.PNG)

#### <a name="to-modify-the-app"></a>アプリケーションを変更するには

1.  Visual Studio を使用してサンプルを開きます。  

2.  すべての不足している Nuget が復元されるように、アプリをリビルドします。  

3.  Web.config ファイルを開きます。  次のように、検索するため、次の値を変更します。  

    ```  
    <add key="ida:ClientId" value="[Replace this Client Id from #3 above under section Create and configure an Application Group in AD FS 2016 or later]" />  
    <add key="ida:ResourceID" value="[Replace this with the Web API Identifier from #5 above]"  />
    <add key="ida:ADFSDiscoveryDoc" value="https://[Your ADFS hostname]/adfs/.well-known/openid-configuration" />  
    <!--<add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" />      
    <add key="ida:AADInstance" value="https://login.microsoftonline.com/{0}" />-->  
    <add key="ida:PostLogoutRedirectUri" value="[Replace this with the Redirect URI from #4 above]" />  
    ```  

    ![AD FS の OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_2.PNG)  

4.  Startup.Auth.cs ファイルを開き、次の変更を行います。  

    -   次の変更と OpenId Connect ミドルウェアの初期化ロジックを調整します。  

        ```  
        private static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];  
        //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];  
        //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];  
        private static string metadataAddress = ConfigurationManager.AppSettings["ida:ADFSDiscoveryDoc"];
        private static string resourceId = ConfigurationManager.AppSettings["ida:ResourceID"];
        private static string postLogoutRedirectUri = ConfigurationManager.AppSettings["ida:PostLogoutRedirectUri"];  
        ```  

    -   コメントを以下の記事。  

            ```  
            //string Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);  
            ```

          ![AD FS の OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_3.PNG)

    -   さらに、下には、次のように OpenId Connect ミドルウェアのオプションを変更します。  

        ```  
        app.UseOpenIdConnectAuthentication(  
            new OpenIdConnectAuthenticationOptions  
            {  
                ClientId = clientId,  
                //Authority = authority,  
                Resource = resourceId,
                MetadataAddress = metadataAddress,  
                PostLogoutRedirectUri = postLogoutRedirectUri,
                RedirectUri = postLogoutRedirectUri
        ```  

        ![AD FS の OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_4.PNG)

5.  HomeController.cs ファイルを開き、次の変更を行います。  

    -   以下を追加します。  

            ```  
            using System.Security.Claims;  
            ```

    -   About() メソッドは、次に示すように更新します。  

        ```  
        [Authorize]
        public ActionResult About()
        {
            ClaimsPrincipal cp = ClaimsPrincipal.Current;
            string userName = cp.FindFirst(ClaimTypes.WindowsAccountName).Value;
            ViewBag.Message = String.Format("Hello {0}!", userName);
            return View();
        }
        ```  

        ![AD FS の OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_5.PNG)

### <a name="test-the-custom-claims-in-id-token"></a>ID トークン内のカスタム要求をテストします。

上記の変更が完了したら後、は、f5 キーを押します。 サンプルのページが表示されます。 サインインをクリックします。

![AD FS の OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_6.PNG)

AD FS サインイン ページにリダイレクトできます。 サインインしてください。

![AD FS の OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_7.PNG)

これが成功した後署名されたようになりましたことがわかります。

![AD FS の OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_8.PNG)

リンクをクリックします。 ID トークン内のユーザー名要求から取得されます。 こんにちは [Username] が表示されます。

![AD FS の OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_9.PNG)

## <a name="next-steps"></a>次の手順
[AD FS の開発](../../ad-fs/AD-FS-Development.md)  
