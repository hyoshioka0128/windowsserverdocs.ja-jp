---
ms.assetid: d282bb4e-38a0-4c7c-83d8-f6ea89278057
title: AD FS 2016 以降で OpenID Connect を使用して web アプリケーションを構築する
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 49d952a49cf474708f57a0ae2a7760d2470af607
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857495"
---
# <a name="build-a-web-application-using-openid-connect-with-ad-fs-2016-and-later"></a>AD FS 2016 以降で OpenID Connect を使用して web アプリケーションを構築する

## <a name="pre-requisites"></a>前提条件  
このドキュメントを完了する前に必要な前提条件の一覧を次に示します。 このドキュメントでは、AD FS がインストールされ、AD FS ファームが作成されていることを前提としています。  

-   GitHub クライアントツール  

-   Windows Server 2016 TP4 以降の AD FS  

-   Visual Studio 2013 以降。  

## <a name="create-an-application-group-in-ad-fs-2016-and-later"></a>AD FS 2016 以降でアプリケーショングループを作成する
次のセクションでは、AD FS 2016 以降でアプリケーショングループを構成する方法について説明します。  

#### <a name="create-application-group"></a>アプリケーショングループの作成  

1.  AD FS 管理 で、アプリケーショングループ を右クリックし、**アプリケーショングループの追加** を選択します。  

2.  アプリケーショングループウィザードの [名前] に「 **ADFSSSO** 」と入力し、 **[クライアント-サーバーアプリケーション]** で、web**アプリケーションテンプレートにアクセスする web ブラウザー**を選択します。  **[次へ]** をクリックします。

    ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_1.PNG)  

3.  **クライアント識別子**の値をコピーします。  この値は、アプリケーションの web.config ファイルの ida: ClientId の値として後で使用されます。  

4.  **リダイレクト URI:**  -  **https://localhost:44320/** には、次のように入力します。  **[追加]** をクリックします。 **[次へ]** をクリックします。  

    ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_2.PNG)  

5.  **[概要]** 画面で、 **[次へ]** をクリックします。  

    ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_3.PNG)

6.  **[完了]** 画面で、 **[閉じる]** をクリックします。  

## <a name="download-and-modify-sample-application-to-authenticate-via-openid-connect-and-ad-fs"></a>OpenID Connect と AD FS を使用して認証するサンプルアプリケーションをダウンロードして変更する  
このセクションでは、サンプル Web アプリをダウンロードし、Visual Studio で変更する方法について説明します。   [ここに記載](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)されている Azure AD サンプルを使用します。  

サンプルプロジェクトをダウンロードするには、Git Bash を使用し、次のように入力します。  

```  
git clone https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect  
```  

![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_8.PNG)  

#### <a name="to-modify-the-app"></a>アプリを変更するには  

1.  Visual Studio を使用してサンプルを開きます。  

2.  不足しているすべての Nuget が復元されるように、アプリをリビルドします。  

3.  Web.config ファイルを開きます。  次のように、次の値を変更します。  

    ```  
    <add key="ida:ClientId" value="[Replace this Client Id from #3 in above section]" />  
    <add key="ida:ADFSDiscoveryDoc" value="https://[Your ADFS hostname]/adfs/.well-known/openid-configuration" />  
    <!--<add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" />      
    <add key="ida:AADInstance" value="https://login.microsoftonline.com/{0}" />-->  
    <add key="ida:PostLogoutRedirectUri" value="[Replace this with Redirect URI from #4 in the above section]" />  
    ```  

    ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_9.PNG)  

4.  Startup.Auth.cs ファイルを開き、次のように変更します。  

    -   次のことをコメントアウトします。  

        ```  
        //string Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);  
        ```  

    -   次の変更を加えて、OpenId Connect ミドルウェア初期化ロジックを調整します。  

        ```  
        private static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];  
        //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];  
        //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];  
        private static string metadataAddress = ConfigurationManager.AppSettings["ida:ADFSDiscoveryDoc"];  
        private static string postLogoutRedirectUri = ConfigurationManager.AppSettings["ida:PostLogoutRedirectUri"];  
        ```  

        ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_10.PNG)  

    -   さらに、次のように OpenId Connect ミドルウェアのオプションを変更します。  

        ```  
        app.UseOpenIdConnectAuthentication(  
            new OpenIdConnectAuthenticationOptions  
            {  
                ClientId = clientId,  
                //Authority = authority,  
                MetadataAddress = metadataAddress,  
                PostLogoutRedirectUri = postLogoutRedirectUri,
                RedirectUri = postLogoutRedirectUri
        ```  

        ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_11.PNG)  

        上記を変更することで、次の操作を実行します。  

        -   信頼された発行者に関するデータの通信に証明機関を使用する代わりに、MetadataAddress を使用して探索ドキュメントの場所を直接指定します。  

        -   Azure AD では、要求に redirect_uri の存在は強制されませんが、ADFS では実行されます。 そのため、ここに追加する必要があります。  

## <a name="verify-the-app-is-working"></a>アプリが動作していることを確認する  
上記の変更が加えられたら、F5 キーを押します。  これにより、サンプルページが表示されます。  [サインイン] をクリックします。  

![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_12.PNG)  

AD FS サインインページにリダイレクトされます。  さあ、サインインします。  

![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_13.PNG)  

これが成功すると、サインインしたことがわかります。  

![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_14.PNG)  

## <a name="next-steps"></a>次の手順
[AD FS の開発](../../ad-fs/AD-FS-Development.md)  
