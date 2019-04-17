---
ms.assetid: d282bb4e-38a0-4c7c-83d8-f6ea89278057
title: "AD FS 2016 で OpenID 接続を使用して Web アプリケーションを構築します。"
description: 
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f8040b19576ac9de4ced43e6313cad69276a3d27
ms.sourcegitcommit: c16a2bf1b8a48ff267e71ff29f18b5e5cda003e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/28/2018
---
# <a name="build-a-web-application-using-openid-connect-with-ad-fs-2016"></a>AD FS 2016 で OpenID 接続を使用して Web アプリケーションを構築します。

>Windows Server 2016 の適用対象:

Windows Server 2012 R2 で AD FS で初期の Oauth のサポートの構築、AD FS 2016 には、OpenId 接続サインオンを使用するためのサポートが導入されています。  
  
## <a name="pre-requisites"></a>前提条件  
このドキュメントを完了する前に必要な前提条件の一覧を次に示します。 このドキュメントは、AD FS がインストールされており、AD FS ファームが作成されたことを想定しています。  
  
-   Azure AD サブスクリプション (無料試用版で問題ありません)  
  
-   GitHub クライアント ツール  
  
-   Windows Server 2016 TP4 またはそれ以降の AD FS  
  
-   Visual Studio 2013 以降。  
  
## <a name="create-an-application-group-in-ad-fs-2016"></a>AD FS 2016 でアプリケーション グループを作成します。  
次のセクションでは、AD FS 2016 でアプリケーション グループを構成する方法について説明します。  
  
#### <a name="create-application-group"></a>アプリケーション グループを作成します。  
  
1.  AD FS の管理でアプリケーション グループを右クリックして**アプリケーション グループの追加**します。  
  
2.  アプリケーション グループ ウィザードで、名前を入力**ADFSSSO**し、[**スタンドアロン アプリケーション**選択、**サーバー アプリケーションまたは Web サイト**テンプレート。  をクリックして**次**します。  
  
    ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_1.PNG)  
  
3.  コピー、**クライアント識別子**値。  これは後で値として使用できる、ida: ClientId アプリケーションの Web.config ファイルでのします。  
  
4.  次の入力**URI のリダイレクト:** - **https://localhost:44320/**します。  をクリックして**追加**します。 をクリックして**次**します。  
  
    ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_2.PNG)  
  
5.  **アプリケーションの資格情報を構成する**画面で、チェック ボックスをオンに**共有シークレットを生成**シークレットをコピーします。 をクリックして**[次へ]**  
  
    ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_3.PNG)  
  
6.  **概要**画面で、[**次**します。  
  
7.  **Complete**画面で、[**閉じる**します。  
  
8.  現時点で新しいアプリケーション グループを右クリックし、**プロパティ**します。  
  
9. **ADFSSSO プロパティ**クリックして**アプリケーションの追加**します。  
  
10. **サンプル アプリケーションに新しいアプリケーションを追加**選択**Web API** ] をクリック**次**します。  
  
    ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_4.PNG)  
  
11. **構成 Web API**画面で、次の入力**識別子** - **https://contoso.com/WebApp**します。  をクリックして**追加**します。 をクリックして**次**します。  
  
    ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_7.PNG)  
  
12. **アクセス制御ポリシーの選択**画面で、**すべてのユーザーを許可**] をクリック**次**します。  
  
    ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_Confidential_7.PNG)  
  
13. **アプリケーション アクセス許可の構成**画面で、必ず**openid**が選択されているし] をクリックして**[次へ]**します。  
  
    ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_7.PNG)  
  
14. **概要**画面で、[**次**します。  
  
15. **Complete**画面で、[**閉じる**します。  
  
16. **サンプル アプリケーション プロパティ**] をクリックして**OK**します。  
  
## <a name="download-and-modify-mvp-app-to-authenticate-via-openid-connect-and-ad-fs"></a>ダウンロードして修正 MVP アプリ OpenId 経由での認証に接続し、AD FS  
このセクションでは、Web API のサンプルをダウンロードして、Visual Studio でそれを変更する方法について説明します。   私たちに使用する Azure AD のサンプルである[ここ](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)します。  
  
サンプル プロジェクトをダウンロードするには、次のように入力し、Git Bash を使用します。  
  
```  
git clone https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect  
```  
  
![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_8.PNG)  
  
#### <a name="to-modify-the-app"></a>アプリを変更するには  
  
1.  Visual Studio を使用してサンプルを開きます。  
  
2.  すべての不足している NuGets は復元できるように、アプリをコンパイルします。  
  
3.  Web.config ファイルを開きます。  次のように、[検索のため、次の値を変更します。  
  
    ```  
    <add key="ida:ClientId" value="8219ab4a-df10-4fbd-b95a-8b53c1d8669e" />  
    <add key="ida:ADFSDiscoveryDoc" value="https://adfs.contoso.com/adfs/.well-known/openid-configuration" />  
    <!--<add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" />      
    <add key="ida:ResourceID" value="https://contoso.com/WebApp"  
    <add key="ida:AADInstance" value="https://login.microsoftonline.com/{0}" />-->  
    <add key="ida:PostLogoutRedirectUri" value="https://localhost:44320/" />  
    ```  
  
    ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_9.PNG)  
  
4.  Startup.Auth.cs ファイルを開き、次を変更します。  
  
    -   コメント アウト次します。  
  
        ```  
        //public static readonly string Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);  
        ```  
  
    -   次の変更で OpenId 接続ミドルウェア初期化ロジックを調整します。  
  
        ```  
        private static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];  
        //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];  
        //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];  
        private static string metadataAddress = ConfigurationManager.AppSettings["ida:ADFSDiscoveryDoc"];  
        private static string postLogoutRedirectUri = ConfigurationManager.AppSettings["ida:PostLogoutRedirectUri"];  
        ```  
  
        ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_10.PNG)  
  
    -   遠く下矢印をオプションを変更して、OpenId 接続ミドルウェア次に示すようにします。  
  
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
  
        ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_11.PNG)  
  
        上記を変更することで、次の手順はしました。  
  
        -   信頼された発行元に関するデータを通信するため、権限を使用する代わりに MetadataAddress 経由で直接探索 doc 場所を指定しました  
  
        -   Azure AD は、要求内の redirect_uri の存在を強制しませんが、ADFS します。 そのため、ここで追加する必要があります。  
  
## <a name="verify-the-app-is-working"></a>アプリが動作していることを確認します。  
上記の変更が確立されると、F5 キーを押します。  サンプル ページが表示されます。  ログオン] をクリックします。  
  
![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_12.PNG)  
  
AD FS サインイン ページにリダイレクトできます。  ログインしてください。  
  
![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_13.PNG)  
  
これが成功した後ログインしていることが表示されます。  
  
![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_14.PNG)  
  
## <a name="next-steps"></a>次の手順
[AD FS の開発](../../ad-fs/AD-FS-Development.md)  

