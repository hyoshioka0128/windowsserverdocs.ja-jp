---
title: OAuth および ADAL を使用して 1 つのページの web アプリケーションをビルドします。AD FS 2016 と JS
description: AngularJS をセキュリティで保護する JavaScript 用 ADAL を使用して AD FS に対して認証を行うための手順を提供するチュートリアル ベースのシングル ページ アプリケーション
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 06/12/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: active-directory-federation-services
ms.openlocfilehash: 78ab9f5d7c3e75650a4efb171d3b9281c56c63d3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865303"
---
# <a name="build-a-single-page-web-application-using-oauth-and-adaljs-with-ad-fs-2016"></a>OAuth および ADAL を使用して 1 つのページの web アプリケーションをビルドします。AD FS 2016 と JS

>適用先:Windows Server 2016

このチュートリアルでは、AngularJS をセキュリティで保護する JavaScript 用 ADAL を使用して AD FS に対して認証するための命令ベースのシングル ページ アプリケーション、ASP.NET Web API バックエンドで実装を提供します。

このシナリオで、ユーザーがサインインするときに、JavaScript フロント エンドは[Active の Directory Authentication Library for JavaScript (ADAL します。JS)](https://github.com/AzureAD/azure-activedirectory-library-for-js)と Azure AD から ID トークン (id_token) を取得する暗黙的な認証付与します。 トークンがキャッシュ クライアントに接続されると、要求、ベアラー トークンとして OWIN ミドルウェアを使用して保護されているバックエンド Web API を呼び出すとき。

>警告:ここで作成できる例は、教育目的でのみです。 これらの手順では、モデルの必須の要素を公開する最も単純で最低限の実装です。 例では、エラー処理のすべての側面を含まない場合があり、その他の機能に関連します。

>[!NOTE]
>このチュートリアルでは、該当する**のみ**2016 以降の AD FS サーバー 

## <a name="overview"></a>概要
このサンプルでは作成します、バックエンド web Api リソースへのアクセスをセキュリティで保護する AD FS に対してシングル ページ アプリケーションのクライアントを認証は、認証フロー。 全体的な認証フローを次に示します


![AD FS の承認](media/Single-Page-Application-with-AD-FS/authenticationflow.PNG)

シングル ページ アプリケーションを使用する場合、ユーザーが、開始の場所にからページや JavaScript ファイルのコレクションを開始する場所と、HTML ビューが読み込まれます。 AD FS の認証を直接そのように、アプリケーション、つまり AD FS インスタンス クライアントの ID に関する重要な情報を把握する Active Directory Authentication Library (ADAL) を構成する必要があります。

ADAL は、認証するためのトリガーを見て場合、アプリケーションによって提供される情報を使用して、AD FS STS に認証を指示します。  暗黙的な許可フローは、AD FS では、パブリック クライアントとして登録されるシングル ページ アプリケーションが自動的に構成します。 #Fragment を使用して、アプリケーションに返される ID トークンの承認要求の結果。 バックエンドへの呼び出し WebAPI は、この ID トークンを web Api にアクセスするヘッダーにベアラー トークンとして実行します。

## <a name="setting-up-the-development-box"></a>開発ボックスの設定
このチュートリアルでは、Visual Studio 2015 を使用します。 プロジェクトでは、ADAL JS ライブラリを使用します。 ADAL をお読みくださいについて[Active Directory 認証ライブラリ .NET。](https://msdn.microsoft.com/library/azure/mt417579.aspx)

## <a name="setting-up-the-environment"></a>環境のセットアップ
このチュートリアルでは、使用の基本設定。

1.  DC:AD FS をホストするドメインのドメイン コント ローラー
2.  AD FS サーバー:ドメインの AD FS サーバー
3.  開発用コンピューター:マシンがある Visual Studio がインストールされているし、サンプルを開発します。

2 つのマシンをする場合は、使用できます。 DC/AD FS と他のサンプルを開発するための 1 つです。

ドメイン コント ローラーと AD FS をセットアップする方法は、この記事の範囲外です。 追加の配置情報を参照してください。

- [AD DS の展開](../../ad-ds/deploy/AD-DS-Deployment.md) 
- [AD FS の展開](../AD-FS-Deployment.md)



## <a name="clone-or-download-this-repository"></a>複製するか、このリポジトリをダウンロード
使用する AngularJS シングル ページ アプリへの Azure AD の統合およびそれを変更するために作成したサンプル アプリケーションを代わりに、AD FS を使用して、バックエンド リソースをセキュリティで保護します。

シェルまたはコマンド ライン: から

    git clone https://github.com/Azure-Samples/active-directory-angularjs-singlepageapp.git

## <a name="about-the-code"></a>コードについて
キー ファイル認証ロジックを含む次のとおりです。

**App.js** - ADAL モジュールの依存関係の挿入、ADAL によって AAD とプロトコルの対話を推進するために使用されるアプリの構成値を提供およびルーティングする必要があります前の認証を使用せずにアクセスできませんを示します。

**index.html** -adal.js への参照が含まれています

**HomeController.js**-ADAL で login() と logOut() メソッドの活用方法を示しています。

**UserDataController.js** -キャッシュされた id_token からユーザー情報を抽出する方法を示します。

**Startup.Auth.cs** -ベアラー認証に Active Directory フェデレーション サービスを使用する web Api の構成が含まれています。

## <a name="registering-the-public-client-in-ad-fs"></a>AD FS でのパブリック クライアントの登録
サンプルでは、WebAPI はでリッスンする構成 https://localhost:44326/します。 アプリケーション グループ**web アプリケーションにアクセスする Web ブラウザー**暗黙的な許可フローのアプリケーションを構成するために使用できます。

1. AD FS 管理コンソールを開き、をクリックして**アプリケーション グループの追加**します。 **アプリケーション グループの追加ウィザード**アプリケーション、説明、および select の名前を入力、 **web アプリケーションにアクセスする Web ブラウザー**テンプレートから、**クライアント サーバーアプリケーション**次に示すセクション  <br>![新しいアプリケーション グループを作成します。](media/Single-Page-Application-with-AD-FS/appgroup_step1.png)

2. 次のページで**ネイティブ アプリケーション**アプリケーション クライアント id を指定し、リダイレクト URI を次に示すよう、  <br>![新しいアプリケーション グループを作成します。](media/Single-Page-Application-with-AD-FS/appgroup_step2.png)

3. 次のページで**アクセス制御ポリシーの適用**とアクセス許可のままに*のすべてのユーザーを許可*

4. [概要] ページに次のようになります  <br>![新しいアプリケーション グループを作成します。](media/Single-Page-Application-with-AD-FS/appgroup_step3.png)

5. をクリックして**次**をアプリケーション グループの追加を完了し、ウィザードを閉じます。

## <a name="modifying-the-sample"></a>このサンプルを変更します。
ADAL JS を構成します。

開く、 **app.js**ファイルし、変更、 **adalProvider.init**定義。

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
|インスタンス (instance)|お客様の STS URL では、例。 https://fs.contoso.com/
|テナント (tenant)|"Adfs"のまま
|クライアント Id|これは、シングル ページ アプリケーションのパブリック クライアントを構成するときに指定したクライアント ID です。

## <a name="configure-webapi-to-use-ad-fs"></a>AD FS を使用する web Api を構成します。
開く、 **Startup.Auth.cs**サンプル ファイルを開き、先頭に次のコードを追加します。 

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
|ValidAudience|これは、'audience' の値を構成しますトークンに対して確認されます。
|ValidIssuer|これが構成の値 ' に対してチェックされるトークンの発行者
|MetadataEndpoint|これは、STS のメタデータ情報を指します

## <a name="add-application-configuration-for-ad-fs"></a>AD FS の構成をアプリケーションを追加します。
次に示すよう appsettings を変更します。

    <appSettings>
    <add key="ida:Audience" value="https://localhost:44326/" />
    <add key="ida:AdfsMetadataEndpoint" value="https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml" />
    <add key="ida:Issuer" value="https://fs.contoso.com/adfs" />
      </appSettings>

## <a name="running-the-solution"></a>ソリューションの実行
ソリューションのクリーンで、ソリューションをリビルドして実行します。 詳細なトレースを表示するには、Fiddler を起動し、HTTPS 復号化を有効にします。

ブラウザーは、SPA を読み込むし、次の画面が表示されます。

![クライアントを登録します。](media/Single-Page-Application-with-AD-FS/singleapp3.PNG)

ログインをクリックします。  ToDo リストは、認証フローをトリガーして、ADAL JS で AD fs 認証を指示します。

![Login](media/Single-Page-Application-with-AD-FS/singleapp4a.PNG)

Fiddler では、# フラグメント内の URL の一部として返されるトークンを確認できます。

![Fiddler](media/Single-Page-Application-with-AD-FS/singleapp5a.PNG)

これで、バックエンドでは、ログインのユーザーの ToDo リスト項目を追加する API を呼び出してできます。

![Fiddler](media/Single-Page-Application-with-AD-FS/singleapp6.PNG)

## <a name="next-steps"></a>次の手順
[AD FS の開発](../../ad-fs/AD-FS-Development.md)  
