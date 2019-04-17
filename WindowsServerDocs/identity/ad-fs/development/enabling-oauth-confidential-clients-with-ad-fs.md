---
ms.assetid: 5a64e790-6725-4099-aa08-8067d57c3168
title: "AD FS 2016 で OAuth 機密クライアントを使用してサーバー側のアプリケーションを構築します。"
description: 
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 175c683f9097aeba4c1f06e8671183476c98aa3f
ms.sourcegitcommit: c16a2bf1b8a48ff267e71ff29f18b5e5cda003e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/28/2018
---
# <a name="build-a-server-side-application-using-oauth-confidential-clients-with-ad-fs-2016"></a>AD FS 2016 で OAuth 機密クライアントを使用してサーバー側のアプリケーションを構築します。

>Windows Server 2016 の適用対象:

Windows Server 2012 R2 で AD FS で初期の Oauth のサポートの構築、AD FS 2016 には、アプリや Web サーバーで実行されているサービスなど、独自のシークレットを維持するための対応のクライアントのサポートが導入されています。  これらのクライアントは、機密クライアントと呼ばれます。    
以下の AD FS に機密性の高いクライアントとして機能して、Web サーバーで実行されている Web アプリケーションの概略図に示します。  
  
## <a name="pre-requisites"></a>前提条件  
このドキュメントを完了する前に必要な前提条件の一覧を次に示します。 このドキュメントは、AD FS がインストールされており、AD FS ファームが作成されたことを想定しています。  
  
-   Azure AD サブスクリプション (無料試用版で問題ありません)  
  
-   GitHub クライアント ツール  
  
-   Windows Server 2016 TP4 またはそれ以降の AD FS  
  
-   Visual Studio 2013 以降。  
  
## <a name="create-an-application-group-in-ad-fs-2016"></a>AD FS 2016 でアプリケーション グループを作成します。  
次のセクションでは、AD FS 2016 でアプリケーション グループを構成する方法について説明します。  
  
#### <a name="create-the-application-group"></a>アプリケーション グループを作成します。  
  
1.  AD FS の管理でアプリケーション グループを右クリックして**アプリケーション グループの追加**します。  
  
2.  アプリケーション グループ ウィザードで、名前を入力**ADFSOAUTHCC**し、[**スタンドアロン アプリケーション**選択、**サーバー アプリケーションまたは Web サイト**テンプレート。  をクリックして**次**します。  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_2.PNG)  
  
3.  コピー、**クライアント識別子**値。  値として後で使用される**ida: ClientId**アプリケーションの Web.config ファイルでします。  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_3.PNG)  
  
4.  次の入力**URI のリダイレクト:** - **https://localhost:44323**します。  をクリックして**追加**します。 をクリックして**次**します。  
  
5.  **アプリケーションの資格情報を構成する**画面で、チェック ボックスをオンに**共有シークレットを生成**シークレットをコピーします。  これは、後の値として使用されます**ida: AppKey**アプリケーションの Web.config ファイルでします。  をクリックして**次**します。  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_4.PNG)  
  
6.  **概要**画面で、[**次**します。  
  
7.  **Complete**画面で、[**閉じる**します。  
  
8.  現時点で新しいアプリケーション グループを右クリックし、**プロパティ**します。  
  
9. **ADFSOAUTHCC プロパティ**クリックして**アプリケーションの追加**します。  
  
10. **サンプル アプリケーションに新しいアプリケーションを追加**選択**Web API**] をクリック**次**します。  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_6.PNG)  
  
11. **構成 Web API**画面で、次の入力**識別子** - **https://contoso.com/WebApp**します。  をクリックして**追加**します。 をクリックして**次**します。  この値はの後で使用される**ida: GraphResourceId**アプリケーションの Web.config ファイルでします。  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_9.PNG)  
  
12. **アクセス制御ポリシーの選択**画面で、**すべてのユーザーを許可**] をクリック**次**します。  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_7.PNG)  
  
13. **アプリケーション アクセス許可の構成**画面で、必ず**user_impersonation**が選択されているし] をクリックして**[次へ]**します。  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_8.PNG)  
  
14. **概要**画面で、[**次**します。  
  
15. **Complete**画面で、[**閉じる**します。  
  
16. **ADFSOAUTHCC プロパティ**クリックして**OK**します。  
  
## <a name="upgrade-the-database"></a>データベースをアップグレードします。  
Visual Studio 2015 は、このチュートリアルの作成に使用されました。   Visual Studio 2015 の使用例を取得するためには、データベース ファイルを更新する必要があります。  これを行うには、次の手順を使用します。  
  
このセクションでは、Web API のサンプルをダウンロードして、Visual Studio 2015 でデータベースをアップグレードする方法について説明します。   私たちに使用する Azure AD のサンプルである[ここ](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity)します。  
  
サンプル プロジェクトをダウンロードするには、次のように入力し、Git Bash を使用します。  
  
```  
git clone https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity.git  
```  
  
![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_10.PNG)  
  
#### <a name="to-upgrade-the-database-file"></a>データベース ファイルをアップグレードするには  
  
1.  Visual Studio でプロジェクトを開く、アプリが SQL Server 2102 Express が必要であるを通知するポップアップがあります。またはデータベースをアップグレードする必要があります。  [OK] をクリックします。  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_12.PNG)  
  
2.  [次へ] のコンパイル ビルドを選択して、アプリケーションは、上部にあるソリューションのビルド]-> [します。  これは、すべての NuGet パッケージが復元されます。  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_13.PNG)  
  
3.  ここで、上部にある次のように選択します。**ビュー** -> **サーバー エクスプ ローラー**します。  開き、[1 回**データ接続**を右クリックして**両者**選択**接続の変更**します。  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_14.PNG)  
  
4.  **接続の変更**[**詳細**します。  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_15.PNG)  
  
5.  [詳細プロパティ] のデータ ソースを見つけてから変更をドロップダウン リストを使用して**(LocalDb\v11.0)**に**(LoaclDB) MSSQLLocalDB**します。  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_16.PNG)  
  
6.  [OK] をクリックします。 [OK] をクリックします。  データベースをアップグレードするには、[はい] をクリックします。  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_17.PNG)  
  
7.  これが完了したら、超える、右側の値をコピー、ボックスの横に**接続文字列。**  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_18.PNG)  
  
8.  を開き、Web.config ファイルを上にコピーした値を持つ connectionString 内にある値を置き換えます。  Web.config ファイルを保存します。  
  
    > [!NOTE]  
    > 新しい connectionString を実現できるように、上記の手順を実行する必要があります。  それ以外の場合、以下の Update-Database を実行するとエラーを出力します。  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_19.PNG)  
  
9. Visual Studio の上部には、次のように選択します。**ビュー** -> **その他の Windows** -> **パッケージ マネージャー コンソール**します。  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_20.PNG)  
  
10. 下部にあるパッケージ マネージャー コンソールで入力:`Enable-Migrations`とヒットを入力します。  
  
    > [!NOTE]  
    > コマンドレットとして Enable-Migrations が認識されていないことを示すエラーが発生した場合、EntityFramework を更新する Install-Package EntityFramework を入力します。  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_21.PNG)  
  
11. 下部にあるパッケージ マネージャー コンソールで入力:`Add-Migration <anynamehere>`とヒットを入力します。  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_22.PNG)  
  
12. 下部にあるパッケージ マネージャー コンソールで入力:`Update-Database`とヒットを入力します。  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_23.PNG)  
  
## <a name="modify-the-webapi-in-visual-studio"></a>Visual Studio で WebApi を変更します。  
  
#### <a name="to-modify-the-sample-web-api"></a>サンプルの Web API を変更するには  
  
1.  Visual Studio を使用してサンプルを開きます。  
  
2.  Web.config ファイルを開きます。  次の値を変更します。  
  
    -   ida: ClientId - 上記 3 から値を入力します。  
  
    -   ida: AppKey - 上記 5 から値を入力します。  
  
    -   ida: GraphResourceId - 上記 #11 から値を入力します。  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_24.PNG)  
  
3.  [App_Start Startup.Auth.cs ファイルを開き、次の変更します。  
  
    -   次の行をコメントにします。  
  
        ```  
        //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];  
        //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];  
        //public static readonly string Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);  
        ```  
  
        ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_25.PNG)  
  
    -   代わりに、次を追加します。  
  
        ```  
        public static readonly string Authority = "https://<your_fsname>/adfs";  
        ```  
  
        ここで < your_fsname > は、DNS の部分、フェデレーション サービスの url、たとえば adfs.contoso.com に置き換えられます。  
  
        ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_26.PNG)  
  
4.  UserProfileController.cs ファイルを開き、次を変更します。  
  
    -   コメント アウト次します。  
  
        ```  
        //authContext = new AuthenticationContext(Startup.Authority, new TokenDbCache(userObjectID));  
        ```  
  
    -   次のように両方の出現に置き換えてください。  
  
        ```  
        authContext = new AuthenticationContext(Startup.Authority, false, new TokenDbCache(userObjectID));  
        ```  
  
        ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_27.PNG)  
  
    -   コメント アウト次します。  
  
        ```  
        //authContext = new AuthenticationContext(Startup.Authority);  
        ```  
  
    -   次のように両方の出現に置き換えてください。  
  
        ```  
        authContext = new AuthenticationContext(Startup.Authority, false);  
        ```  
  
        ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_28.PNG)  
  
    -   今すぐをコメント アウト、次のすべてのインスタンス。  
  
        ```  
        Uri redirectUri = new Uri(Request.Url.GetLeftPart(UriPartial.Authority.ToString() + "/OAuth");  
        ```  
  
    -   次のようにすべての出現箇所に置き換えてください。  
  
        ```  
        Uri redirectUri = new Uri(Request.Url.GetLeftPart(UriPartial.Authority.ToString());  
        ```  
  
        ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_34.PNG)  
  
## <a name="test-the-solution"></a>ソリューションをテストします。  
このセクションでは、機密性の高いクライアント ソリューションをテストします。  ソリューションをテストするのにには、次の手順を使用します。  
  
#### <a name="testing-the-confidential-client-solution"></a>機密性の高いクライアント ソリューションをテストします。  
  
1.  Visual Studio の上部には、Internet Explorer が選択されているかどうかを確認し、緑の矢印をクリックします。  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_36.png)  
  
2.  ASP.Net ページが表示されて、1 回] をクリックして**登録**します。  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_31.PNG)  
  
3.  ユーザー名とパスワードを入力し、クリックして**登録**します。  これは、SQL データベースのローカル アカウントを作成します。  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_31.PNG)  
  
4.  通知、ASP.NET サイトになってこんにちはください。  をクリックして**プロファイル**します。  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_32.PNG)  
  
5.  これは、情報をせずページが表示し、ということお必要がありますここをクリックしてサインインします。  をクリックして**ここ**します。  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_33.PNG)  
  
6.  AD fs のサインインを求められますようになりました。  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_35.PNG)  
  
## <a name="next-steps"></a>次の手順
[AD FS の開発](../../ad-fs/AD-FS-Development.md)  

