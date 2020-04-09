---
ms.assetid: 5a64e790-6725-4099-aa08-8067d57c3168
title: AD FS 2016 以降の OAuth 機密クライアントを使用してサーバー側アプリケーションを構築する
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 8a8567a497e10df66f77fb996c937791b4aa9e08
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857565"
---
# <a name="build-a-server-side-application-using-oauth-confidential-clients-with-ad-fs-2016-or-later"></a>AD FS 2016 以降の OAuth 機密クライアントを使用してサーバー側アプリケーションを構築する


AD FS 2016 以降のリリースでは、web サーバーで実行されているアプリやサービスなど、独自のシークレットを保持できるクライアントがサポートされています。  これらのクライアントは、機密クライアントとして知られています。
次に示すのは、web サーバー上で実行され、AD FS するための機密クライアントとして機能する web アプリケーションの概略です。  

## <a name="pre-requisites"></a>前提条件  
このドキュメントを完了する前に必要な前提条件の一覧を次に示します。 このドキュメントでは、AD FS がインストールされていることを前提としています。  

-   GitHub クライアントツール  

-   Windows Server 2016 TP4 以降の AD FS  

-   Visual Studio 2013 以降。  

## <a name="create-an-application-group-in-ad-fs-2016-or-later"></a>AD FS 2016 以降でアプリケーショングループを作成する
次のセクションでは、AD FS 2016 以降でアプリケーショングループを構成する方法について説明します。  

#### <a name="create-the-application-group"></a>アプリケーショングループを作成する  

1.  AD FS 管理 で、アプリケーショングループ を右クリックし、**アプリケーショングループの追加** を選択します。  

2.  アプリケーショングループウィザードで、**名前**として「 **Adfsoauthcc** 」と入力し、 **[クライアント-サーバーアプリケーション]** で、 **Web API テンプレートにアクセスするサーバーアプリケーション**を選択します。  **[次へ]** をクリックします。  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_2.PNG)  

3.  **クライアント識別子**の値をコピーします。  この値は、アプリケーションの web.config ファイルの**ida: ClientId**の値として後で使用されます。  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_3.PNG)  

4.  **リダイレクト URI:**  -  **https://localhost:44323** には、次のように入力します。  **[追加]** をクリックします。 **[次へ]** をクリックします。  

5.  **[アプリケーション資格情報の構成]** 画面で、 **[共有シークレットを生成]** してシークレットをコピーする チェックボックスをオンにします。  この値は、アプリケーションの web.config ファイルの**ida: ClientSecret**の値として後で使用されます。  **[次へ]** をクリックします。  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_4.PNG)   

6. **[WEB API の構成]** 画面で、**識別子** -  **https://contoso.com/WebApp** に次のように入力します。  **[追加]** をクリックします。 **[次へ]** をクリックします。  この値は、アプリケーションの web.config ファイルの**ida: GraphResourceId**で後で使用されます。  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_9.PNG)  

7. **[Access Control ポリシーの適用]** 画面で、 **[すべてのユーザーを許可]** する を選択し、 **[次へ]** をクリックします。  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_7.PNG)  

8. **[アプリケーションのアクセス許可の構成]** 画面で、 **openid**と**user_impersonation**が選択されていることを確認し、 **[次へ]** をクリックします。  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_8.PNG)  

9. **[概要]** 画面で、 **[次へ]** をクリックします。  

10. **[完了]** 画面で、 **[閉じる]** をクリックします。  

## <a name="upgrade-the-database"></a>データベースをアップグレードする  
このチュートリアルの作成では、Visual Studio 2015 が使用されました。   この例を Visual Studio 2015 で使用するには、データベースファイルを更新する必要があります。  この場合、次の手順を実行します。  

このセクションでは、サンプル Web API をダウンロードし、Visual Studio 2015 でデータベースをアップグレードする方法について説明します。   [ここに記載](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity)されている Azure AD サンプルを使用します。  

サンプルプロジェクトをダウンロードするには、Git Bash を使用し、次のように入力します。  

```  
git clone https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity.git  
```  

![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_10.PNG)  

#### <a name="to-upgrade-the-database-file"></a>データベースファイルをアップグレードするには  

1.  Visual Studio でプロジェクトを開くと、アプリに 2012 Express SQL Server が必要であることを通知するポップアップが表示されるか、データベースをアップグレードする必要があります。  [OK] をクリックします。  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_12.PNG)  

2.  次に、上部にある [ビルド] > [ソリューションのビルド] の順に選択して、アプリケーションをコンパイルします。  これにより、すべての NuGet パッケージが復元されます。  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_13.PNG)  

3.  上部で、[ **View** -> **サーバーエクスプローラー**] を選択します。  このウィンドウが開いたら、 **[データ接続]** の **[defaultconnection]** を右クリックし、 **[接続の変更]** を選択します。  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_14.PNG)  

4.  **[接続の変更]** の **[データベースファイル名 (新規または既存)]** で、 **[参照]** を選択して**path\filename.mdf**を指定します。 ダイアログボックスで [**はい]** をクリックします。

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_6.PNG)

5.  **[接続の変更]** で **[詳細設定]** を選択します。  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_15.PNG)  

6.  [詳細プロパティ] で [データソース] を見つけ、ドロップダウンを使用して、 **(Localdb\ V11.0)** から **(LocalDb) \MSSQLLocalDB**に変更します。  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_16.PNG)  

7.  [OK] をクリックします。 [OK] をクリックします。  [はい] をクリックしてデータベースをアップグレードします。  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_17.PNG)  

8.  この処理が完了したら、右側にある [接続文字列] の横にあるボックスの値をコピーし**ます。**  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_18.PNG)  

9.  次に、web.config ファイルを開き、connectionString 内の値を上記でコピーした値に置き換えます。  Web.config ファイルを保存します。  

    > [!NOTE]  
    > 上記の手順は、新しい connectionString を取得できるようにするために必要です。  それ以外の場合は、以下のように Update データベースを実行すると、エラーが発生します。  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_19.PNG)  

10. Visual Studio の上部で、[ -> **その他の Windows** -> **パッケージマネージャーコンソール**を**表示**する] を選択します。  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_20.PNG)  

11. 下部にあるパッケージマネージャーコンソールで、次のように入力して、enter キーを押し `Enable-Migrations` ます。  

    > [!NOTE]  
    > コマンドレットとして "有効/移行" が認識されないというエラーが表示された場合は、「Install-Package EntityFramework」と入力して EntityFramework を更新します。  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_21.PNG)  

12. 下部にあるパッケージマネージャーコンソールで、次のように入力して、enter キーを押し `Add-Migration <anynamehere>` ます。  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_22.PNG)  

13. 下部にあるパッケージマネージャーコンソールで、次のように入力して、enter キーを押し `Update-Database` ます。  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_23.PNG)  

## <a name="modify-the-webapi-in-visual-studio"></a>Visual Studio での WebApi の変更  

#### <a name="to-modify-the-sample-web-api"></a>サンプル Web API を変更するには  

1.  Visual Studio を使用してサンプルを開きます。  

2.  Web.config ファイルを開きます。  次の値を変更します。  

    -   ida: ClientId-上の「アプリケーショングループの作成」セクションの #3 から値を入力します。  

    -   ida: ClientSecret-前の「アプリケーショングループの作成」セクションの #5 から値を入力します。  

    -   ida: GraphResourceId-上の「アプリケーショングループの作成」セクションの #6 から値を入力します。  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_24.PNG)  

3.  App_Start で Startup.Auth.cs ファイルを開き、次のように変更します。  

    -   次の行をコメントアウトします。  

        ```  
        //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];  
        //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];  
        //public static readonly string Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);  
        ```  

    -   その場所に次のものを追加します。  

        ```  
        public static readonly string Authority = "https://<your_fsname>/adfs";  
        ```  

        < your_fsname > は、フェデレーションサービスの url の DNS 部分 (adfs.contoso.com など) に置き換えられます。  

        ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_25.PNG)  

4.  UserProfileController.cs ファイルを開き、次のように変更します。  

    -   次のことをコメントアウトします。  

        ```  
        //authContext = new AuthenticationContext(Startup.Authority, new TokenDbCache(userObjectID));  
        ```  

    -   両方のオカレンスを次のように置き換えます。  

        ```  
        authContext = new AuthenticationContext(Startup.Authority, false, new TokenDbCache(userObjectID));  
        ```  

        ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_27.PNG)  

    -   次のことをコメントアウトします。  

        ```  
        //authContext = new AuthenticationContext(Startup.Authority);  
        ```  

    -   両方のオカレンスを次のように置き換えます。  

        ```  
        authContext = new AuthenticationContext(Startup.Authority, false);  
        ```  

        ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_28.PNG)  

    -   次のすべてのインスタンスをコメントアウトします。  

        ```  
        Uri redirectUri = new Uri(Request.Url.GetLeftPart(UriPartial.Authority).ToString() + "/OAuth");  
        ```  

    -   すべての出現箇所を次のように置き換えます。  

        ```  
        Uri redirectUri = new Uri(Request.Url.GetLeftPart(UriPartial.Authority).ToString());  
        ```  

        ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_34.PNG)  

## <a name="test-the-solution"></a>ソリューションのテスト  
このセクションでは、confidential クライアントソリューションをテストします。  ソリューションをテストするには、次の手順に従います。  

#### <a name="testing-the-confidential-client-solution"></a>Confidential クライアントソリューションのテスト  

1. Visual Studio の上部で、Internet Explorer が選択されていることを確認し、緑色の矢印をクリックします。  

   ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_36.png)  

2. ASP.Net ページが起動したら、ページの右上にある **[登録]** をクリックします。  ユーザー名とパスワードを入力し、 **[登録]** ボタンをクリックします。  これにより、SQL データベースにローカルアカウントが作成されます。  

   ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_31.PNG)  

3. ASP.NET サイトで Hello abby@contoso.com! と表示されるようになりました。  **[プロファイル]** をクリックします。  

   ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_32.PNG)  

4. これにより、情報のないページが表示され、サインインするにはここをクリックする必要があります。  **ここ**をクリックしてください。  

   ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_33.PNG)  

5. AD FS にサインインするように求められます。  

   ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_35.PNG)  

## <a name="next-steps"></a>次の手順
[AD FS の開発](../../ad-fs/AD-FS-Development.md)  
