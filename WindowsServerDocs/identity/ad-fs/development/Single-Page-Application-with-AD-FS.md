---
title: "OAuth および ADAL.JS"
description: 
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: active-directory-federation-services
ms.openlocfilehash: 7b3d48e1e38baffeb84b1f236efb43cfda5048c0
ms.sourcegitcommit: c16a2bf1b8a48ff267e71ff29f18b5e5cda003e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/28/2018
---
# <a name="build-a-single-page-web-application-using-oauth-and-adaljs-with-ad-fs-2016"></a>OAuth および ADAL.JS

>Windows Server 2016 の適用対象:

このチュートリアルでは、AngularJS をセキュリティで保護する JavaScript 用 ADAL を使用して AD FS に対して認証するための命令ベースの 1 つのページのアプリケーション、ASP.NET Web API バックエンドを使って実装を提供します。

>警告: ここで構築する例は、教育用にのみです。 次に挙げる手順では、モデルの必須の要素を公開する最も簡単な最小限の実装のためです。 この例は、エラー処理のすべての側面を含まない場合があり、その他の関連機能します。

>[!NOTE]
>This walkthrough is applicable **only** to AD FS Server 2016 and higher 

## <a name="overview"></a>概要
このサンプルでは作成します、バックエンドで WebAPI リソースへのアクセスをセキュリティで保護する AD FS に対して 1 つのページ アプリケーション クライアントを認証は、認証フロー。 全体的な認証フローを次に示します


![AD FS の認証](media/Single-Page-Application-with-AD-FS/authenticationflow.PNG)

シングル ページ アプリケーションを使用する場合、ユーザーが元の場所にから開始ページと JavaScript ファイルのコレクションと HTML ビューが読み込まれます。 向けの AD FS を認証できるように、アプリケーション、つまり、AD FS のインスタンス、クライアント ID、に関する重要な情報を理解して Active Directory 認証ライブラリ (ADAL) を構成する必要があります。

ADAL 認証のためのトリガーが見つかると場合、は、アプリケーションによって提供される情報を使用してし、は、AD FS の STS を認証するように指示します。  暗黙的な付与フローは、AD FS でパブリック クライアントとして登録されるシングル ページ アプリケーションが自動的に構成します。 認証要求の結果、#fragment 経由でアプリケーションに返される ID トークン。 バックエンドそれ以降の呼び出し WebAPI はこの ID トークンを WebAPI にアクセスするヘッダーで bearer トークンとして実行します。

## <a name="setting-up-the-development-box"></a>開発のボックスを設定します。
このチュートリアルでは、Visual Studio 2015 を使用します。 プロジェクトが ADAL JS ライブラリを使用します。 お読みください ADAL について[Active Directory 認証ライブラリ .NET します。](https://msdn.microsoft.com/library/azure/mt417579.aspx)

## <a name="setting-up-the-environment"></a>環境のセットアップ
このチュートリアルでは、使用の基本設定。

1.  AD FS をホストするドメインの DC: ドメイン コントローラー
2.  AD FS サーバー: ドメインの AD FS のサーバー
3.  開発マシンの場合: Visual Studio のあるコンピューターがインストールされているし、サンプルを開発します。

2 つだけのマシンをする場合は、使用、できます。 DC/AD FS と他のサンプルを開発するための 1 つです。

ドメイン コントローラーと AD FS をセットアップする方法は、この記事の範囲外です。 追加の展開をご覧ください。

- [AD DS の展開](../../ad-ds/deploy/AD-DS-Deployment.md) 
- [AD FS の展開](../AD-FS-Deployment.md)



## <a name="clone-or-download-this-repository"></a>複製またはダウンロードこのリポジトリ
私たちに使用する AngularJS 1 つのページ アプリに Azure AD を統合して、変更、用に作成されたサンプル アプリケーションを代わりに AD FS を使用してバックエンド リソースをセキュリティで保護します。

シェルまたはコマンド ライン: から

    git clone https://github.com/Azure-Samples/active-directory-angularjs-singlepageapp.git

## <a name="about-the-code"></a>コードについて
認証ロジックが含まれているキー ファイル次に示します。

**App.js** - ADAL モジュールの依存関係を挿入し、およびこの AAD とプロトコルの相互作用を推進するために、ADAL によって使用されるアプリの構成値をルーティングする必要があります前の認証を使用せずにアクセスできませんを示します。

**index.html** -adal.js への参照が含まれています

**HomeController.js**-ADAL login() logOut() 方法のメリットを利用する方法について説明します。

**UserDataController.js** -キャッシュされた id_token からユーザー情報を抽出する方法について説明します。

**Startup.Auth.cs** -認証に使用する Active Directory フェデレーション サービス bearer WebAPI の構成が含まれています。

## <a name="registering-the-public-client-in-ad-fs"></a>AD FS での公開のクライアントを登録します。
サンプルでは、WebAPI は https://localhost:44326/ でリッスンするように構成されます。 アプリケーション グループ**Web アプリケーションにアクセスする Web ブラウザー**暗黙的な付与フローのアプリケーションを構成するために使用できます。

1. AD FS 管理コンソールを開き、をクリックして**アプリケーション グループの追加**します。 **アプリケーション グループの追加ウィザード**アプリケーション、説明、および選択の名前を入力、**Web アプリケーションにアクセスする Web ブラウザー**テンプレートから、**クライアント サーバー アプリケーション**以下に示すようにセクション
    <br>![新しいアプリケーション グループを作成します。](media/Single-Page-Application-with-AD-FS/appgroup_step1.png)

2. 次のページで**ネイティブ アプリケーション**アプリケーション クライアント識別子を提供し、以下に示す URI にリダイレクト、
    <br>![新しいアプリケーション グループを作成します。](media/Single-Page-Application-with-AD-FS/appgroup_step2.png)

3. 次のページで**アクセス制御ポリシーの適用**としてアクセス許可をそのまま使用*すべてのユーザーを許可*

4. [概要] ページに次のようななります
    <br>![新しいアプリケーション グループを作成します。](media/Single-Page-Application-with-AD-FS/appgroup_step3.png)

5. をクリックして**次**をアプリケーション グループの追加を完了し、ウィザードを閉じます。

## <a name="modifying-the-sample"></a>サンプルを変更します。
ADAL JS を構成します。

開いている、**app.js**ファイルし、変更、**adalProvider.init**を定義します。

    adalProvider.init(
        {
            instance: 'https://fs.contoso.com/', // your STS URL
            tenant: 'adfs',                      // this should be adfs
            clientId: 'https://localhost:44326/', // your client ID of the
            //cacheLocation: 'localStorage', // enable this for IE, as sessionStorage does not work for localhost.
        },
        $httpProvider
        );

|構成|説明
|--------|--------
|インスタンス|例: https://fs.contoso.com/、STS URL
|テナント|"Adfs"として維持すること
|clientID|これは、1 つのページのアプリケーションの公開のクライアントを構成するときに指定したクライアント ID です。

## <a name="configure-webapi-to-use-ad-fs"></a>AD FS を使って WebAPI を構成します。
開いている、**Startup.Auth.cs**サンプル ファイルを先頭に、次を追加します。 

    using System.IdentityModel.Tokens;

削除します。

                app.UseWindowsAzureActiveDirectoryBearerAuthentication(
    new WindowsAzureActiveDirectoryBearerAuthenticationOptions
    {
    Audience = ConfigurationManager.AppSettings["ida:Audience"],
    Tenant = ConfigurationManager.AppSettings["ida:Tenant"]
    });

追加します。

    app.UseActiveDirectoryFederationServicesBearerAuthentication(
    new ActiveDirectoryFederationServicesBearerAuthenticationOptions
    {
    MetadataEndpoint = ConfigurationManager.AppSettings["ida:AdfsMetadataEndpoint"],
    TokenValidationParameters = new TokenValidationParameters()
    {
    ValidAudience = ConfigurationManager.AppSettings["ida:Audience"],
    ValidIssuer = ConfigurationManager.AppSettings["ida:Issuer"]
    }
    }
    );

|パラメーター|説明
|--------|--------
|ValidAudience|これにより、構成 'オーディエンス' の値、トークンに照合するされます
|ValidIssuer|これにより、構成の値 ' トークンで照合発行者
|MetadataEndpoint|これは、STS のメタデータ情報を指します

## <a name="add-application-configuration-for-ad-fs"></a>AD FS のアプリケーションの構成を追加します。
次に示す appsettings を変更します。

    <appSettings>
    <add key="ida:Audience" value="https://localhost:44326/" />
    <add key="ida:AdfsMetadataEndpoint" value="https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml" />
    <add key="ida:Issuer" value="https://fs.contoso.com/adfs" />
      </appSettings>

## <a name="running-the-solution"></a>ソリューションを実行しています。
クリーン、ソリューションでは、ソリューションのリビルドし、それを実行します。 詳細なトレースを表示する場合は、Fiddler を起動し、HTTPS 復号化を有効にします。

ブラウザーは、SPA を読み込むし、次の画面が表示されます。

![クライアントを登録します。](media/Single-Page-Application-with-AD-FS/singleapp3.PNG)

ログイン時にクリックします。  ToDo リストが認証フローをトリガーして、ADAL JS は AD fs 認証を直接

![ログイン](media/Single-Page-Application-with-AD-FS/singleapp4a.PNG)

Fiddler で、# フラグメントで URL の一部として返されるトークンを確認できます。

![Fiddler](media/Single-Page-Application-with-AD-FS/singleapp5a.PNG)

今すぐバックエンド ログイン ユーザーの ToDo リスト項目を追加する API を呼び出すことができます。

![Fiddler](media/Single-Page-Application-with-AD-FS/singleapp6.PNG)

## <a name="next-steps"></a>次の手順
[AD FS の開発](../../ad-fs/AD-FS-Development.md)  
