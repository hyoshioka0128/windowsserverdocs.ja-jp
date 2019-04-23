---
ms.assetid: d282bb4e-38a0-4c7c-83d8-f6ea89278057
title: AD FS 2016 で OpenID Connect を使用して web アプリケーションを作成します。
description: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 74a493e6568b71a05116140ec67586d36f439aa8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882663"
---
# <a name="build-a-web-application-using-openid-connect-with-ad-fs-2016"></a>AD FS 2016 で OpenID Connect を使用して web アプリケーションを作成します。

>適用先:Windows Server 2016

Windows Server 2012 R2 で AD FS での初期の Oauth サポートに基づき、AD FS 2016 には、OpenId Connect サインオンを使用するためのサポートが導入されています。  
  
## <a name="pre-requisites"></a>前提条件  
このドキュメントを完了する前に必要な前提条件の一覧を次に示します。 このドキュメントは、AD FS がインストールされており、AD FS ファームが作成されたことを想定しています。  
  
-   GitHub のクライアント ツール  
  
-   Windows Server 2016 TP4 以降の AD FS  
  
-   Visual Studio 2013 またはそれ以降。  
  
## <a name="create-an-application-group-in-ad-fs-2016"></a>AD FS 2016 でのアプリケーション グループを作成します。  
次のセクションでは、AD FS 2016 でのアプリケーション グループを構成する方法について説明します。  
  
#### <a name="create-application-group"></a>アプリケーション グループを作成します。  
  
1.  AD FS の管理、アプリケーション グループを右クリックし、選択**アプリケーション グループの追加**します。  
  
2.  アプリケーション グループ ウィザードで、名前の入力**ADFSSSO** **スタンドアロン アプリケーション**選択、**サーバー アプリケーションまたは web サイト**テンプレート。  **[次へ]** をクリックします。  
  
    ![AD FS の OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_1.PNG)  
  
3.  コピー、**クライアント識別子**値。  これは後で値として使用、ida: ClientId、アプリケーションの web.config ファイルでの。  
  
4.  次の入力**リダイレクト URI:** - **https://localhost:44320/** します。  **[追加]** をクリックします。 **[次へ]** をクリックします。  
  
    ![AD FS の OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_2.PNG)  
  
5.  **アプリケーション資格情報の構成**画面で、チェック ボックスをオンに**共有シークレットを生成**し、シークレットをコピーします。  **[次へ]** をクリックします。  
  
    ![AD FS の OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_3.PNG)  
  
6.  **概要**画面で、**次**します。  
  
7.  **完了**画面で、**閉じる**します。  
  
8.  ここでは、新しいアプリケーション グループを右クリックで、および選択**プロパティ**します。  
  
9. **ADFSSSO プロパティ**クリックして**アプリケーションを追加**します。  
  
10. **サンプル アプリケーションに新しいアプリケーションを追加**選択**Web API**  をクリック**次**。  
  
    ![AD FS の OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_4.PNG)  
  
11. **Web API の構成**画面で、次の入力**識別子** - **https://contoso.com/WebApp**します。  **[追加]** をクリックします。 **[次へ]** をクリックします。  
  
    ![AD FS の OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_7.PNG) 
    
12. **へのアクセス制御ポリシーの選択**画面で、**[のすべてのユーザーに許可]** をクリック**次**。  
  
    ![AD FS の OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_Confidential_7.PNG)  
  
13. **アプリケーション アクセス許可の構成**確認画面で、 **openid**が選択されているし、をクリックして**次**。  
  
    ![AD FS の OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_7.PNG)  
  
14. **概要**画面で、**次**します。  
  
15. **完了**画面で、**閉じる**します。  
  
16. **サンプル アプリケーションのプロパティ**クリックして**OK**。  
  
## <a name="download-and-modify-mvp-app-to-authenticate-via-openid-connect-and-ad-fs"></a>MVP アプリ OpenId での認証の変更をダウンロードして接続し、AD FS  
このセクションでは、Web API のサンプルをダウンロードして Visual Studio で変更する方法について説明します。   Azure AD のサンプルを使用する[ここ](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)します。  
  
サンプル プロジェクトをダウンロードし、Git Bash を使用して、次を入力します。  
  
```  
git clone https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect  
```  
  
![AD FS の OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_8.PNG)  
  
#### <a name="to-modify-the-app"></a>アプリケーションを変更するには  
  
1.  Visual Studio を使用してサンプルを開きます。  
  
2.  すべての不足している Nuget が復元されるように、アプリをコンパイルします。  
  
3.  Web.config ファイルを開きます。  次のように、検索するため、次の値を変更します。  
  
    ```  
    <add key="ida:ClientId" value="8219ab4a-df10-4fbd-b95a-8b53c1d8669e" />  
    <add key="ida:ADFSDiscoveryDoc" value="https://adfs.contoso.com/adfs/.well-known/openid-configuration" />  
    <!--<add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" />      
    <add key="ida:ResourceID" value="https://contoso.com/WebApp"  
    <add key="ida:AADInstance" value="https://login.microsoftonline.com/{0}" />-->  
    <add key="ida:PostLogoutRedirectUri" value="https://localhost:44320/" />  
    ```  
  
    ![AD FS の OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_9.PNG)  
  
4.  Startup.Auth.cs ファイルを開き、次の変更を行います。  
  
    -   コメントを以下の記事。  
  
        ```  
        //public static readonly string Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);  
        ```  
  
    -   次の変更と OpenId Connect ミドルウェアの初期化ロジックを調整します。  
  
        ```  
        private static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];  
        //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];  
        //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];  
        private static string metadataAddress = ConfigurationManager.AppSettings["ida:ADFSDiscoveryDoc"];  
        private static string postLogoutRedirectUri = ConfigurationManager.AppSettings["ida:PostLogoutRedirectUri"];  
        ```  
  
        ![AD FS の OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_10.PNG)  
  
    -   遠くダウン、次のように OpenId Connect ミドルウェアのオプションを変更します。  
  
        ```  
        app.UseOpenIdConnectAuthentication(  
            new OpenIdConnectAuthenticationOptions  
            {  
                ClientId = clientId,  
                //Authority = authority,  
                MetadataAddress = metadataAddress,  
                RedirectUri = postLogoutRedirectUri,  
                PostLogoutRedirectUri = postLogoutRedirectUri 
        ```  
  
        ![AD FS の OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_11.PNG)  
  
        上記の変更によっては、次の操作を行っています。  
  
        -   信頼された発行者に関するデータを通信するための権限を使用せずに MetadataAddress 経由で直接検出ドキュメントの場所を指定します  
  
        -   Azure AD では、要求での redirect_uri の存在は強制されませんが、ADFS は。 そのため、ここに追加する必要があります。  
  
## <a name="verify-the-app-is-working"></a>アプリが動作を確認します。  
上記の変更が完了したら後、は、f5 キーを押します。  サンプルのページが表示されます。  サインインをクリックします。  
  
![AD FS の OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_12.PNG)  
  
AD FS サインイン ページにリダイレクトできます。  サインインしてください。  
  
![AD FS の OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_13.PNG)  
  
これが成功した後署名されたようになりましたことがわかります。  
  
![AD FS の OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_14.PNG)  
  
## <a name="next-steps"></a>次の手順
[AD FS の開発](../../ad-fs/AD-FS-Development.md)  

