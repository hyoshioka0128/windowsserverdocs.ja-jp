---
title: OpenID Connect または OAuth を AD FS 2016 以降で使用する場合に id_token で出力される要求をカスタマイズする
description: AD FS 2016 以降のカスタム id トークンの概念の技術的な概要
author: anandyadavmsft
ms.author: billmath
manager: mtillman
ms.date: 04/29/2020
ms.topic: article
ms.prod: windows-server
ms.reviewer: anandy
ms.technology: identity-adfs
ms.openlocfilehash: 331e5ff2dbe7f172488543d1d1f5ed0f757cd584
ms.sourcegitcommit: 2cc251eb5bc3069bf09bc08e06c3478fcbe1f321
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/03/2020
ms.locfileid: "84333953"
---
# <a name="customize-claims-to-be-emitted-in-id_token-when-using-openid-connect-or-oauth-with-ad-fs-2016-or-later"></a>OpenID Connect または OAuth を AD FS 2016 以降で使用する場合に id_token で出力される要求をカスタマイズする

## <a name="overview"></a>概要

[この](native-client-with-ad-fs.md)記事では、OpenID connect サインオンで AD FS を使用するアプリを構築する方法について説明します。 ただし、既定では、id_token で使用できるのは固定されたクレームセットのみです。 AD FS 2016 以降のリリースには、OpenID Connect シナリオで id_token をカスタマイズする機能があります。

## <a name="when-are-custom-id-tokens-used"></a>カスタム ID トークンはいつ使用されますか?

特定のシナリオでは、クライアントアプリケーションにアクセスしようとしているリソースがない可能性があります。 そのため、実際にアクセストークンは必要ありません。 このような場合、クライアントアプリケーションは基本的に ID トークンのみを必要としますが、機能をサポートするために追加のクレームが必要になります。

## <a name="what-are-the-restrictions-on-getting-custom-claims-in-id-token"></a>ID トークンでカスタム要求を取得する際の制限は何ですか?

### <a name="scenario-1"></a>シナリオ 1

![制限](media/Custom-Id-Tokens-in-AD-FS/res1.png)

1. `response_mode`がに設定されている`form_post`
2. ID トークンでカスタム要求を取得できるのはパブリッククライアントのみです
3. 証明書利用者識別子 (Web API 識別子) はクライアント識別子と同じである必要があります

### <a name="scenario-2"></a>シナリオ 2

![制限](media/Custom-Id-Tokens-in-AD-FS/restrict2.png)

AD FS サーバーに[KB4019472](https://support.microsoft.com/help/4019472/windows-10-update-kb4019472)がインストールされている
1. `response_mode`が form_post として設定されています
2. パブリックと機密の両方のクライアントが ID トークンでカスタム要求を取得できます。
3. `allatclaims`クライアント– RP ペアにスコープを割り当てます。

次の例に示すように、コマンドレットを使用してスコープを割り当てることができ `Grant-ADFSApplicationPermission` ます。

```powershell
Grant-AdfsApplicationPermission -ClientRoleIdentifier "https://my/privateclient" -ServerRoleIdentifier "https://rp/fedpassive" -ScopeNames "allatclaims","openid"
```

## <a name="creating-and-configuring-an-oauth-application-to-handle-custom-claims-in-id-token"></a>ID トークン内のカスタム要求を処理する OAuth アプリケーションの作成と構成

次の手順に従って、カスタム要求で ID トークンを受信するための AD FS でアプリケーションを作成し、構成します。

### <a name="create-and-configure-an-application-group-in-ad-fs-2016-or-later"></a>AD FS 2016 以降でアプリケーショングループを作成および構成する

1. AD FS 管理] で、[アプリケーショングループ] を右クリックし、[**アプリケーショングループの追加**] を選択します。
2. アプリケーショングループウィザードの [名前] に「 **ADFSSSO** 」と入力し、[クライアント-サーバーアプリケーション] で、 **web アプリケーションテンプレートにアクセスするネイティブアプリケーション**を選択します。 **[次へ]** をクリックします。

   ![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap1.png)

3. [**クライアント識別子**の値をコピーします。  この値は、アプリケーションの web.config ファイルの ida: ClientId の値として後で使用されます。
4. **リダイレクト URI**には、次のように入力し  -  **https://localhost:44320/** ます。  **[追加]** をクリックします。 **[次へ]** をクリックします。

   ![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap2.png)

5. [ **WEB API の構成**] 画面で、[**識別子**] に次のように入力し  -  **https://contoso.com/WebApp** ます。  **[追加]** をクリックします。 **[次へ]** をクリックします。  この値は、アプリケーションの web.config ファイルの**ida: ResourceID**で後で使用されます。

   ![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap3.png)

6. [ **Access Control ポリシーの選択**] 画面で、[**すべてのユーザーを許可**する] を選択し、[**次へ**] をクリックします。

   ![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap4.png)

7. [**アプリケーションのアクセス許可の構成**] 画面で、 **openid**と**allatclaims**が選択されていることを確認し、[**次へ**] をクリックします。

   ![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap5.PNG)

8. [**概要**] 画面で、[**次へ**] をクリックします。

   ![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap6.PNG)

9. [**完了**] 画面で、[**閉じる**] をクリックします。
10. AD FS 管理] で [アプリケーショングループ] をクリックして、すべてのアプリケーショングループの一覧を取得します。 **ADFSSSO**を右クリックし、[**プロパティ**] を選択します。 [ **ADFSSSO-WEB API** ] を選択し、[**編集...** ] をクリックします。

    ![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap7.PNG)

11. [ **ADFSSSO-WEB API のプロパティ**] 画面で、[**発行変換規則**] タブを選択し、[**規則の追加...** ] をクリックします。

    ![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap8.PNG)

12. **変換要求規則の追加ウィザード**画面で、ドロップダウンから [**カスタム規則を使用して要求を送信**する] を選択し、[**次へ**] をクリックします。

    ![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap9.PNG)

13. **変換要求規則の追加ウィザード**画面で、[**要求規則名**] に「 **Forcustomidtoken** 」、**カスタム規則**に次の要求規則を入力します。 [**完了**] をクリック

    ```
    x:[]
    => issue(claim=x);
    ```

    ![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap10.PNG)

    > [!NOTE]
    > PowerShell を使用して、スコープとスコープを割り当てることもでき `allatclaims` `openid` ます。

    ``` powershell
    Grant-AdfsApplicationPermission -ClientRoleIdentifier "[Client ID from #3 above]" -ServerRoleIdentifier "[Identifier from #5 above]" -ScopeNames "allatclaims","openid"
    ```

### <a name="download-and-modify-the-sample-application-to-emit-custom-claims-in-id_token"></a>サンプルアプリケーションをダウンロードして変更し、id_token でカスタム要求を出力する

このセクションでは、サンプル Web アプリをダウンロードし、Visual Studio で変更する方法について説明します。 [ここ](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/tree/master/1-WebApp-OIDC)に記載されている Azure AD サンプルを使用します。

サンプルプロジェクトをダウンロードするには、Git Bash を使用し、次のように入力します。

```
git clone https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/tree/master/1-WebApp-OIDC
```

![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_1.PNG)

#### <a name="to-modify-the-app"></a>アプリを変更するには

1. Visual Studio を使用してサンプルを開きます。
2. 不足しているすべての Nuget が復元されるように、アプリをリビルドします。
3. Web.config ファイルを開きます。  次のように、次の値を変更します。

   ```xml
   <add key="ida:ClientId" value="[Replace this Client Id from #3 above under section Create and configure an Application Group in AD FS 2016 or later]" />
   <add key="ida:ResourceID" value="[Replace this with the Web API Identifier from #5 above]"  />
   <add key="ida:ADFSDiscoveryDoc" value="https://[Your ADFS hostname]/adfs/.well-known/openid-configuration" />
   <!--<add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" />
   <add key="ida:AADInstance" value="https://login.microsoftonline.com/{0}" />-->
   <add key="ida:PostLogoutRedirectUri" value="[Replace this with the Redirect URI from #4 above]" />
   ```

   ![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_2.png)

4. Startup.Auth.cs ファイルを開き、次のように変更します。

   - 次の変更を加えて、OpenId Connect ミドルウェア初期化ロジックを調整します。

      ```cs
      private static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];
      //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];
      //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];
      private static string metadataAddress = ConfigurationManager.AppSettings["ida:ADFSDiscoveryDoc"];
      private static string resourceId = ConfigurationManager.AppSettings["ida:ResourceID"];
      private static string postLogoutRedirectUri = ConfigurationManager.AppSettings["ida:PostLogoutRedirectUri"];
      ```

   - 次のことをコメントアウトします。

      ```cs
      //string Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);
      ```

      ![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_3.png)

   - さらに、次のように OpenId Connect ミドルウェアのオプションを変更します。

      ```cs
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

      ![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_4.png)

5. HomeController.cs ファイルを開き、次のように変更します。

   - 以下を追加します。

      ```cs
      using System.Security.Claims;
      ```

   - `About()`次に示すように、メソッドを更新します。

      ```cs
      [Authorize]
      public ActionResult About()
      {
          ClaimsPrincipal cp = ClaimsPrincipal.Current;
          string userName = cp.FindFirst(ClaimTypes.WindowsAccountName).Value;
          ViewBag.Message = String.Format("Hello {0}!", userName);
          return View();
      }
      ```

      ![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_5.png)

### <a name="test-the-custom-claims-in-id-token"></a>ID トークンでカスタム要求をテストする

上記の変更が加えられたら、F5 キーを押します。 これにより、サンプルページが表示されます。 [サインイン] をクリックします。

![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_6.PNG)

AD FS サインインページにリダイレクトされます。 要求に従ってサインインしてください。

![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_7.PNG)

これが成功すると、サインインしたことがわかります。

![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_8.png)

[About] リンクをクリックします。 ID トークンのユーザー名要求から取得される "Hello [Username]" が表示されます。

![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_9.png)

## <a name="next-steps"></a>次の手順

[AD FS の開発](../../ad-fs/AD-FS-Development.md)
