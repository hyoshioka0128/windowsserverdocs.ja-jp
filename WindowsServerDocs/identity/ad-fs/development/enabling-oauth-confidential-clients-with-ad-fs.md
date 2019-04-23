---
ms.assetid: 5a64e790-6725-4099-aa08-8067d57c3168
title: AD FS 2016 で OAuth 機密クライアントを使用してサーバー側アプリケーションを構築します。
description: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 175c683f9097aeba4c1f06e8671183476c98aa3f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869583"
---
# <a name="build-a-server-side-application-using-oauth-confidential-clients-with-ad-fs-2016"></a>AD FS 2016 で OAuth 機密クライアントを使用してサーバー側アプリケーションを構築します。

>適用先:Windows Server 2016

Windows Server 2012 R2 で AD FS での初期の Oauth サポートに基づき、AD FS 2016 には、アプリや web サーバーで実行されているサービスなどの独自のシークレットを維持できるクライアントのサポートが導入されています。  これらのクライアントは、confidential クライアントと呼ばれます。    
Web サーバーで実行し、AD FS に機密性の高いクライアントとして使用される web アプリケーションの概略図を次に示します。  
  
## <a name="pre-requisites"></a>前提条件  
このドキュメントを完了する前に必要な前提条件の一覧を次に示します。 このドキュメントは、AD FS がインストールされており、AD FS ファームが作成されたことを想定しています。  
  
-   Azure AD サブスクリプション (無料試用版では問題ありません)  
  
-   GitHub のクライアント ツール  
  
-   Windows Server 2016 TP4 以降の AD FS  
  
-   Visual Studio 2013 またはそれ以降。  
  
## <a name="create-an-application-group-in-ad-fs-2016"></a>AD FS 2016 でのアプリケーション グループを作成します。  
次のセクションでは、AD FS 2016 でのアプリケーション グループを構成する方法について説明します。  
  
#### <a name="create-the-application-group"></a>アプリケーション グループを作成します。  
  
1.  AD FS の管理、アプリケーション グループを右クリックし、選択**アプリケーション グループの追加**します。  
  
2.  アプリケーション グループ ウィザードで、名前の入力**ADFSOAUTHCC** **スタンドアロン アプリケーション**選択、**サーバー アプリケーションまたは web サイト**テンプレート。  **[次へ]** をクリックします。  
  
    ![AD FS の Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_2.PNG)  
  
3.  コピー、**クライアント識別子**値。  後の値として使用する**ida: ClientId**アプリケーションの web.config ファイルにします。  
  
    ![AD FS の Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_3.PNG)  
  
4.  次の入力**リダイレクト URI:** - **https://localhost:44323**します。  **[追加]** をクリックします。 **[次へ]** をクリックします。  
  
5.  **アプリケーション資格情報の構成**画面で、チェック ボックスをオンに**共有シークレットを生成**し、シークレットをコピーします。  これは、後の値として使用されます**ida: AppKey**アプリケーションの web.config ファイルにします。  **[次へ]** をクリックします。  
  
    ![AD FS の Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_4.PNG)  
  
6.  **概要**画面で、**次**します。  
  
7.  **完了**画面で、**閉じる**します。  
  
8.  ここでは、新しいアプリケーション グループを右クリックで、および選択**プロパティ**します。  
  
9. **ADFSOAUTHCC プロパティ**クリックして**アプリケーションを追加**します。  
  
10. **サンプル アプリケーションに新しいアプリケーションを追加**選択**Web API** をクリック**次**。  
  
    ![AD FS の Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_6.PNG)  
  
11. **Web API の構成**画面で、次の入力**識別子** - **https://contoso.com/WebApp**します。  **[追加]** をクリックします。 **[次へ]** をクリックします。  この値の後で使用する**ida: GraphResourceId**アプリケーションの web.config ファイルにします。  
  
    ![AD FS の Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_9.PNG)  
  
12. **へのアクセス制御ポリシーの選択**画面で、**[のすべてのユーザーに許可]** をクリック**次**。  
  
    ![AD FS の Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_7.PNG)  
  
13. **アプリケーション アクセス許可の構成**確認画面で、**user_impersonation**が選択されているし、をクリックして**次**。  
  
    ![AD FS の Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_8.PNG)  
  
14. **概要**画面で、**次**します。  
  
15. **完了**画面で、**閉じる**します。  
  
16. **ADFSOAUTHCC プロパティ**クリックして**OK**。  
  
## <a name="upgrade-the-database"></a>データベースをアップグレードします。  
Visual Studio 2015 は、このチュートリアルの作成に使用されました。   Visual Studio 2015 の使用例を取得するためには、データベース ファイルを更新する必要があります。  この場合、次の手順を実行します。  
  
このセクションでは、Web API のサンプルをダウンロードし、Visual Studio 2015 でのデータベースをアップグレードする方法について説明します。   Azure AD のサンプルを使用する[ここ](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity)します。  
  
サンプル プロジェクトをダウンロードし、Git Bash を使用して、次を入力します。  
  
```  
git clone https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity.git  
```  
  
![AD FS の Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_10.PNG)  
  
#### <a name="to-upgrade-the-database-file"></a>データベース ファイルをアップグレードするには  
  
1.  Visual Studio でプロジェクトを開く、アプリが SQL Server 2012 Express が必要であることを示すポップアップがあります。 またはデータベースをアップグレードする必要があります。  [Ok] をクリックします。  
  
    ![AD FS の Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_12.PNG)  
  
2.  次のコンパイル ビルドを選択して、アプリケーションでは、上部にあるソリューションのビルドを -> します。  これは、すべての NuGet パッケージが復元されます。  
  
    ![AD FS の Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_13.PNG)  
  
3.  これで、上部にある次のように選択します。**ビュー** -> **サーバー エクスプ ローラー**します。  を開くと**データ接続**、右クリック**DefaultConnection**選択と**接続の変更**します。  
  
    ![AD FS の Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_14.PNG)  
  
4.  **接続の変更**を選択します**詳細**します。  
  
    ![AD FS の Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_15.PNG)  
  
5.  高度なプロパティのデータ ソースを特定およびから変更する、ドロップダウンを使用して **(LocalDb\v11.0)** に **(LoaclDB) MSSQLLocalDB**します。  
  
    ![AD FS の Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_16.PNG)  
  
6.  [Ok] をクリックします。 [Ok] をクリックします。  データベースをアップグレードするには、[はい] をクリックします。  
  
    ![AD FS の Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_17.PNG)  
  
7.  これが完了したら、以上、右側の値をコピー、ボックスの横に**接続文字列。**  
  
    ![AD FS の Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_18.PNG)  
  
8.  次に、Web.config ファイルを開きは上記でコピーした値を持つ接続文字列の値を置き換えます。  Web.config ファイルを保存します。  
  
    > [!NOTE]  
    > 上記の手順は、新しい接続文字列を取得できるように必要です。  それ以外の場合、以下の更新プログラム-データベースを実行するとエラーが発生をされます。  
  
    ![AD FS の Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_19.PNG)  
  
9. Visual Studio の上部にある次のように選択します。**ビュー** -> **その他の Windows** -> **パッケージ マネージャー コンソール**します。  
  
    ![AD FS の Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_20.PNG)  
  
10. 下部で、パッケージ マネージャー コンソールで入力します:`Enable-Migrations`し、enter キーを押します。  
  
    > [!NOTE]  
    > 表示された場合は、Enable-migrations ことを示すエラーは、コマンドレットとしては認識されません、EntityFramework を更新するのには、"Install-package entityframework"を入力します。  
  
    ![AD FS の Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_21.PNG)  
  
11. 下部で、パッケージ マネージャー コンソールで入力します:`Add-Migration <anynamehere>`し、enter キーを押します。  
  
    ![AD FS の Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_22.PNG)  
  
12. 下部で、パッケージ マネージャー コンソールで入力します:`Update-Database`し、enter キーを押します。  
  
    ![AD FS の Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_23.PNG)  
  
## <a name="modify-the-webapi-in-visual-studio"></a>Visual Studio で web Api を変更します。  
  
#### <a name="to-modify-the-sample-web-api"></a>サンプル Web API を変更するには  
  
1.  Visual Studio を使用してサンプルを開きます。  
  
2.  Web.config ファイルを開きます。  次の値を変更します。  
  
    -   ClientId: ida - 上記 3 から値を入力します。  
  
    -   ida: AppKey - 5 から値を入力します。  
  
    -   ida: GraphResourceId - 上記 11 から値を入力します。  
  
    ![AD FS の Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_24.PNG)  
  
3.  App_Start Startup.Auth.cs ファイルを開き、次の変更を行います。  
  
    -   次の行をコメント化します。  
  
        ```  
        //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];  
        //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];  
        //public static readonly string Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);  
        ```  
  
        ![AD FS の Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_25.PNG)  
  
    -   代わりに、次を追加します。  
  
        ```  
        public static readonly string Authority = "https://<your_fsname>/adfs";  
        ```  
  
        < your_fsname > は、フェデレーション サービスの url、adfs.contoso.com などの DNS 部分を置き換え  
  
        ![AD FS の Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_26.PNG)  
  
4.  UserProfileController.cs ファイルを開き、次の変更を行います。  
  
    -   コメントを以下の記事。  
  
        ```  
        //authContext = new AuthenticationContext(Startup.Authority, new TokenDbCache(userObjectID));  
        ```  
  
    -   次のように両方の出現箇所を置き換えます。  
  
        ```  
        authContext = new AuthenticationContext(Startup.Authority, false, new TokenDbCache(userObjectID));  
        ```  
  
        ![AD FS の Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_27.PNG)  
  
    -   コメントを以下の記事。  
  
        ```  
        //authContext = new AuthenticationContext(Startup.Authority);  
        ```  
  
    -   次のように両方の出現箇所を置き換えます。  
  
        ```  
        authContext = new AuthenticationContext(Startup.Authority, false);  
        ```  
  
        ![AD FS の Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_28.PNG)  
  
    -   次のすべてのインスタンスを今すぐコメント:  
  
        ```  
        Uri redirectUri = new Uri(Request.Url.GetLeftPart(UriPartial.Authority.ToString() + "/OAuth");  
        ```  
  
    -   次のように、すべての出現箇所を置き換えます。  
  
        ```  
        Uri redirectUri = new Uri(Request.Url.GetLeftPart(UriPartial.Authority.ToString());  
        ```  
  
        ![AD FS の Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_34.PNG)  
  
## <a name="test-the-solution"></a>ソリューションをテストします。  
このセクションでは秘密のクライアント ソリューションがテストされます。  ソリューションをテストするのにには、次の手順を使用します。  
  
#### <a name="testing-the-confidential-client-solution"></a>Confidential クライアント ソリューションをテストします。  
  
1.  Visual Studio の上部にある Internet Explorer が選択されているかどうかを確認し、緑色の矢印をクリックします。  
  
    ![AD FS の Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_36.png)  
  
2.  をクリックすると、ASP.Net ページが表示されたら、**登録**します。  
  
    ![AD FS の Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_31.PNG)  
  
3.  ユーザー名とパスワードを入力し、クリックして**登録**します。  これは、SQL database で、ローカル アカウントを作成します。  
  
    ![AD FS の Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_31.PNG)  
  
4.  通知 ASP.NET サイト、として bsimon でこんにちはの質問です。  クリックして**プロファイル**します。  
  
    ![AD FS の Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_32.PNG)  
  
5.  これにより、情報なしのページが表示され、ということする必要がありますここをクリックしてサインインします。  クリックして**ここ**します。  
  
    ![AD FS の Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_33.PNG)  
  
6.  AD FS にサインインを求め。  
  
    ![AD FS の Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_35.PNG)  
  
## <a name="next-steps"></a>次の手順
[AD FS の開発](../../ad-fs/AD-FS-Development.md)  

