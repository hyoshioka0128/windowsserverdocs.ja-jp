---
title: OpenID Connect または OAuth を AD FS 2016 以降で使用するときに id_token で出力される要求をカスタマイズする
description: AD FS 2016 以降のカスタム id トークンの概念の技術的な概要
author: anandyadavmsft
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server
ms.reviewer: anandy
ms.technology: identity-adfs
ms.openlocfilehash: 88ae6837872c5a6cf6bb1d8533a0aa14b82ca573
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358913"
---
# <a name="customize-claims-to-be-emitted-in-id_token-when-using-openid-connect-or-oauth-with-ad-fs-2016-or-later"></a>OpenID Connect または OAuth を AD FS 2016 以降で使用するときに id_token で出力される要求をカスタマイズする

## <a name="overview"></a>概要
[この](native-client-with-ad-fs.md)記事では、OpenID connect サインオンで AD FS を使用するアプリを構築する方法について説明します。 ただし、既定では、id_token で利用可能な、固定された一連の要求のみが存在します。 AD FS 2016 以降のリリースには、OpenID Connect シナリオで id_token をカスタマイズする機能があります。

## <a name="when-are-custom-id-token-used"></a>カスタム ID トークンはいつ使用されますか?
特定のシナリオでは、クライアントアプリケーションにアクセスしようとしているリソースがない可能性があります。 そのため、実際にアクセストークンは必要ありません。 このような場合、クライアントアプリケーションは基本的に ID トークンのみを必要としますが、機能をサポートするために追加の要求がいくつか必要になります。

## <a name="what-are-the-restrictions-on-getting-custom-claims-in-id-token"></a>ID トークンでカスタム要求を取得する際の制限は何ですか?

### <a name="scenario-1"></a>例 1

![制限](media/Custom-Id-Tokens-in-AD-FS/res1.png)

1.  response_mode は form_post として設定されます。
2.  ID トークンでカスタム要求を取得できるのはパブリッククライアントのみです
3.  証明書利用者識別子 (Web API 識別子) はクライアント識別子と同じである必要があります

### <a name="scenario-2"></a>シナリオ 2

![制限](media/Custom-Id-Tokens-in-AD-FS/restrict2.png)

AD FS サーバーに[KB4019472](https://support.microsoft.com/help/4019472/windows-10-update-kb4019472)がインストールされている
1.  response_mode は form_post として設定されます。
2.  パブリックと機密の両方のクライアントが ID トークンでカスタム要求を取得できます。
3.  スコープ allatclaims をクライアント– RP ペアに割り当てます。
次の例に示すように、ADFSApplicationPermission コマンドレットを使用してスコープを割り当てることができます。

``` powershell
Grant-AdfsApplicationPermission -ClientRoleIdentifier "https://my/privateclient" -ServerRoleIdentifier "https://rp/fedpassive" -ScopeNames "allatclaims","openid"
```

## <a name="creating-and-configuring-an-oauth-application-to-handle-custom-claims-in-id-token"></a>ID トークン内のカスタム要求を処理する OAuth アプリケーションの作成と構成
次の手順に従って、カスタム要求で ID トークンを受信するための AD FS でアプリケーションを作成し、構成します。

### <a name="create-and-configure-an-application-group-in-ad-fs-2016-or-later"></a>AD FS 2016 以降でアプリケーショングループを作成および構成する

1. AD FS 管理 で、アプリケーショングループ を右クリックし、**アプリケーショングループの追加** を選択します。

2. アプリケーショングループウィザードの [名前] に「 **ADFSSSO** 」と入力し、[クライアント-サーバーアプリケーション] で、 **web アプリケーションテンプレートにアクセスするネイティブアプリケーション**を選択します。 **[次へ]** をクリックします。

   ![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap1.png)

3. **クライアント識別子**の値をコピーします。  この値は、アプリケーションの web.config ファイルの ida: ClientId の値として後で使用されます。

4. **リダイレクト URI** - には、次のよう **https://localhost:44320/** に入力します。  **[追加]** をクリックします。 **[次へ]** をクリックします。

   ![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap2.png)

5. **[WEB API の構成]** 画面で、[**識別子** -  **https://contoso.com/WebApp** ] に次のように入力します。  **[追加]** をクリックします。 **[次へ]** をクリックします。  この値は、アプリケーションの web.config ファイルの**ida: ResourceID**で後で使用されます。

   ![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap3.png)

6. **[Access Control ポリシーの選択]** 画面で、 **[すべてのユーザーを許可]** する を選択し、 **[次へ]** をクリックします。

   ![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap4.png)

7. **[アプリケーションのアクセス許可の構成]** 画面で、 **openid**と**allatclaims**が選択されていることを確認し、 **[次へ]** をクリックします。

   ![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap5.png)

8. **[概要]** 画面で、 **[次へ]** をクリックします。  

   ![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap6.png)

9. **[完了]** 画面で、 **[閉じる]** をクリックします。

10. AD FS 管理 で アプリケーショングループ をクリックして、すべてのアプリケーショングループの一覧を取得します。 **ADFSSSO**を右クリックし、 **[プロパティ]** を選択します。 **[ADFSSSO-WEB API]** を選択し、 **[編集...]** をクリックします。

    ![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap7.png)

11. **[ADFSSSO-WEB API のプロパティ]** 画面で、 **[発行変換規則]** タブを選択し、 **[規則の追加...]** をクリックします。

    ![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap8.png)

12. **変換要求規則の追加ウィザード**画面で、ドロップダウンから **[カスタム規則を使用して要求を送信]** する を選択し、 **[次へ]** をクリックします。

    ![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap9.png)

13. **変換要求規則の追加ウィザード**画面で、 **[要求規則名]** に**forcustomidtoken**を入力し、 **[カスタム規則]** に次の要求規則を入力します。 **[Finish]** (完了) をクリックする

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

### <a name="download-and-modify-the-sample-application-to-emit-custom-claims-in-id_token"></a>Id_token でカスタム要求を出力するサンプルアプリケーションをダウンロードして変更する

このセクションでは、サンプル Web アプリをダウンロードし、Visual Studio で変更する方法について説明します。   [ここに記載](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)されている Azure AD サンプルを使用します。  

サンプルプロジェクトをダウンロードするには、Git Bash を使用し、次のように入力します。  

```  
git clone https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect  
```  

![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_1.PNG)

#### <a name="to-modify-the-app"></a>アプリを変更するには

1.  Visual Studio を使用してサンプルを開きます。  

2.  不足しているすべての Nuget が復元されるように、アプリをリビルドします。  

3.  Web.config ファイルを開きます。  次のように、次の値を変更します。  

    ```  
    <add key="ida:ClientId" value="[Replace this Client Id from #3 above under section Create and configure an Application Group in AD FS 2016 or later]" />  
    <add key="ida:ResourceID" value="[Replace this with the Web API Identifier from #5 above]"  />
    <add key="ida:ADFSDiscoveryDoc" value="https://[Your ADFS hostname]/adfs/.well-known/openid-configuration" />  
    <!--<add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" />      
    <add key="ida:AADInstance" value="https://login.microsoftonline.com/{0}" />-->  
    <add key="ida:PostLogoutRedirectUri" value="[Replace this with the Redirect URI from #4 above]" />  
    ```  

    ![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_2.PNG)  

4.  Startup.Auth.cs ファイルを開き、次のように変更します。  

    -   次の変更を加えて、OpenId Connect ミドルウェア初期化ロジックを調整します。  

        ```  
        private static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];  
        //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];  
        //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];  
        private static string metadataAddress = ConfigurationManager.AppSettings["ida:ADFSDiscoveryDoc"];
        private static string resourceId = ConfigurationManager.AppSettings["ida:ResourceID"];
        private static string postLogoutRedirectUri = ConfigurationManager.AppSettings["ida:PostLogoutRedirectUri"];  
        ```  

    -   次のことをコメントアウトします。  

            ```  
            //string Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);  
            ```

          ![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_3.PNG)

    -   さらに、次のように OpenId Connect ミドルウェアのオプションを変更します。  

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

        ![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_4.PNG)

5.  HomeController.cs ファイルを開き、次のように変更します。  

    -   以下を追加します。  

            ```  
            using System.Security.Claims;  
            ```

    -   次に示すように、About () メソッドを更新します。  

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

        ![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_5.PNG)

### <a name="test-the-custom-claims-in-id-token"></a>ID トークンでカスタム要求をテストする

上記の変更が加えられたら、F5 キーを押します。 これにより、サンプルページが表示されます。 [サインイン] をクリックします。

![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_6.PNG)

AD FS サインインページにリダイレクトされます。 さあ、サインインします。

![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_7.PNG)

これが成功すると、サインインしたことがわかります。

![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_8.PNG)

[About] リンクをクリックします。 ID トークンのユーザー名要求から取得された Hello [Username] が表示されます。

![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_9.PNG)

## <a name="next-steps"></a>次の手順
[AD FS の開発](../../ad-fs/AD-FS-Development.md)  
