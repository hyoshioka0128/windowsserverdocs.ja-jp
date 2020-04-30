---
title: OAuth と ADAL を使用して単一ページの web アプリケーションを構築します。AD FS 2016 以降を使用した JS
description: AngularJS ベースのシングルページアプリケーションをセキュリティで保護する JavaScript 用 ADAL を使用して AD FS に対して認証するための手順を提供するチュートリアルです。
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 06/13/2018
ms.topic: article
ms.prod: windows-server
ms.technology: active-directory-federation-services
ms.openlocfilehash: f62b6ad288e2733083d535260f0b3f5ffb5b50bf
ms.sourcegitcommit: f829a48b9b0c7b9ed6e181b37be828230c80fb8a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2020
ms.locfileid: "82173627"
---
# <a name="build-a-single-page-web-application-using-oauth-and-adaljs-with-ad-fs-2016-or-later"></a>OAuth と ADAL を使用して単一ページの web アプリケーションを構築します。AD FS 2016 以降を使用した JS

このチュートリアルでは、ASP.NET Web API バックエンドで実装された AngularJS ベースのシングルページアプリケーションをセキュリティで保護する JavaScript 用の ADAL を使用して AD FS に対して認証するための手順を示します。

このシナリオでは、ユーザーがサインインすると、JavaScript フロントエンドが [Active Directory Authentication Library for JavaScript (ADAL.JS)](https://github.com/AzureAD/azure-activedirectory-library-for-js) と暗黙的な認証付与を使用して、Azure AD から ID トークン (id_token) を取得します。 トークンがキャッシュされ、クライアントは、OWIN ミドルウェアを使用して保護された Web API バックエンドを呼び出すときに、トークンをベアラー トークンとして要求に添付します。

>[!IMPORTANT]
>ここで作成できる例は、学習のみを目的としています。 これらの手順は、モデルの必須要素を公開するために使用できる、最も単純で最小の実装用です。 この例には、エラー処理やその他の関連機能のすべての側面を含めることはできません。

>[!NOTE]
>このチュートリアルは AD FS Server 2016 以降に**のみ**適用されます。 

## <a name="overview"></a>概要
このサンプルでは、バックエンドの WebAPI リソースへのアクセスをセキュリティで保護するために、単一ページアプリケーションクライアントが AD FS に対して認証を行う認証フローを作成します。 全体の認証フローを次に示します。


![AD FS 承認](media/Single-Page-Application-with-AD-FS/authenticationflow.PNG)

シングルページアプリケーションを使用する場合、ユーザーは、開始ページと、JavaScript ファイルと HTML ビューのコレクションが読み込まれる開始位置に移動します。 Active Directory 認証ライブラリ (ADAL) を構成して、アプリケーションに関する重要な情報 (つまり、AD FS インスタンス、クライアント ID) を把握し、AD FS に認証を送信できるようにする必要があります。

ADAL が認証用のトリガーを確認すると、アプリケーションによって提供される情報が使用され、認証が AD FS STS に送られます。  AD FS にパブリッククライアントとして登録されているシングルページアプリケーションは、暗黙的な許可フローに対して自動的に構成されます。 承認要求は、#fragment を介してアプリケーションに返される ID トークンになります。 さらに、バックエンド WebAPI を呼び出すと、この ID トークンがヘッダーのベアラートークンとして処理され、WebAPI にアクセスできるようになります。

## <a name="setting-up-the-development-box"></a>開発ボックスの設定
このチュートリアルでは、Visual Studio 2015 を使用します。 プロジェクトは ADAL JS ライブラリを使用します。 ADAL の詳細については[Active Directory 認証ライブラリ .net](https://msdn.microsoft.com/library/azure/mt417579.aspx)をご覧ください。

## <a name="setting-up-the-environment"></a>環境のセットアップ
このチュートリアルでは、次の基本的なセットアップを使用します。

1.    DC: AD FS がホストされるドメインのドメインコントローラー
2.    AD FS Server: ドメインの AD FS サーバー
3.    開発用コンピューター: Visual Studio がインストールされていて、サンプルを開発しているコンピューター

必要に応じて、2台のコンピューターのみを使用できます。 DC/AD FS 用、もう1つはサンプルを開発しています。

ドメインコントローラーと AD FS のセットアップ方法については、この記事では説明しません。 デプロイの詳細については、次を参照してください。

- [AD DS 展開](../../ad-ds/deploy/AD-DS-Deployment.md)
- [AD FS 展開](../AD-FS-Deployment.md)



## <a name="clone-or-download-this-repository"></a>このリポジトリをクローンまたはダウンロードする
ここでは、Azure AD を AngularJS シングルページアプリに統合するために作成されたサンプルアプリケーションを使用し、AD FS を使用してバックエンドリソースをセキュリティで保護するように変更します。

シェルまたはコマンド ラインから:

    git clone https://github.com/Azure-Samples/active-directory-angularjs-singlepageapp.git

## <a name="about-the-code"></a>コードについて
認証ロジックを含むキーファイルは次のとおりです。

**App.config** : adal モジュールの依存関係が挿入され、adal によって使用されるアプリ構成値が提供されます。これにより、AAD とのプロトコルの対話が促進され、以前の認証なしにアクセスする必要のあるルートが示されます。

**index .html** -adal への参照が含まれています。

**HomeController**-ADAL で login () メソッドと logOut () メソッドを活用する方法を示します。

**UserDataController** -キャッシュされた id_token からユーザー情報を抽出する方法を示します。

**Startup.Auth.cs** -ベアラー認証に Active Directory フェデレーションサービスを使用するための構成が含まれています。

## <a name="registering-the-public-client-in-ad-fs"></a>AD FS にパブリッククライアントを登録しています
このサンプルでは、WebAPI はでhttps://localhost:44326/リッスンするように構成されています。 **Web アプリケーションにアクセス**するアプリケーショングループ web ブラウザーは、暗黙的な許可フローアプリケーションを構成するために使用できます。

1. AD FS 管理コンソールを開き、[**アプリケーショングループの追加**] をクリックします。 **アプリケーショングループの追加ウィザード**で、アプリケーションの名前と説明を入力し、次に示すように、[**クライアント-サーバーアプリケーション**] セクションから**web アプリケーションテンプレートにアクセスする web ブラウザー**を選択します。

    ![新しいアプリケーショングループの作成](media/Single-Page-Application-with-AD-FS/appgroup_step1.png)

2. 次のページの**ネイティブアプリケーション**で、次に示すように、アプリケーションクライアント識別子とリダイレクト URI を指定します。

    ![新しいアプリケーショングループの作成](media/Single-Page-Application-with-AD-FS/appgroup_step2.png)

3. 次のページで**Access Control ポリシーを適用**します。アクセス許可は [*すべて許可*] のままにします。

4. 概要ページは次のようになります。

    ![新しいアプリケーショングループの作成](media/Single-Page-Application-with-AD-FS/appgroup_step3.png)

5. [**次**へ] をクリックして、アプリケーショングループの追加を完了し、ウィザードを閉じます。

## <a name="modifying-the-sample"></a>サンプルの変更
ADAL JS の構成

**App.config**ファイルを開き、 **adalProvider**定義を次のように変更します。

    adalProvider.init(
        {
            instance: 'https://fs.contoso.com/', // your STS URL
            tenant: 'adfs',                      // this should be adfs
            clientId: 'https://localhost:44326/', // your client ID of the
            //cacheLocation: 'localStorage', // enable this for IE, as sessionStorage does not work for localhost.
        },
        $httpProvider
    );

|構成|説明|
|--------|--------|
|instance|STS の URL (例:https://fs.contoso.com/|
|tenant|' Adfs ' として保持する|
|clientID|これは、シングルページアプリケーションのパブリッククライアントを構成するときに指定したクライアント ID です。|

## <a name="configure-webapi-to-use-ad-fs"></a>AD FS を使用するように WebAPI を構成する
サンプルの**Startup.Auth.cs**ファイルを開き、先頭に次のコードを追加します。

    using System.IdentityModel.Tokens;

から

    app.UseWindowsAzureActiveDirectoryBearerAuthentication(
        new WindowsAzureActiveDirectoryBearerAuthenticationOptions
        {
            Audience = ConfigurationManager.AppSettings["ida:Audience"],
            Tenant = ConfigurationManager.AppSettings["ida:Tenant"]
        }
    );

およびを追加します。

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

|パラメーター|[説明]|
|--------|--------|
|ValidAudience|これにより、トークン内で照合される "audience" の値が構成されます。|
|ValidIssuer|これにより、トークン内でチェックされる "issuer" の値が構成されます。|
|MetadataEndpoint|これは、STS のメタデータ情報を指します。|

## <a name="add-application-configuration-for-ad-fs"></a>AD FS のアプリケーション構成の追加
Appsettings を次のように変更します。
```xml
    <appSettings>
        <add key="ida:Audience" value="https://localhost:44326/" />
        <add key="ida:AdfsMetadataEndpoint" value="https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml" />
        <add key="ida:Issuer" value="https://fs.contoso.com/adfs" />
    </appSettings>
    ```

## Running the solution
Clean the solution, rebuild the solution and run it. If you want to see detailed traces, launch Fiddler and enable HTTPS decryption.

The browser (use Chrome browser) will load the SPA and you will be presented with the following screen:

![Register the client](media/Single-Page-Application-with-AD-FS/singleapp3.PNG)

Click on Login.  The ToDo List will trigger the authentication flow and ADAL JS will direct the authentication to AD FS

![Login](media/Single-Page-Application-with-AD-FS/singleapp4a.PNG)

In Fiddler you can see the token being returned as part of the URL in the # fragment.

![Fiddler](media/Single-Page-Application-with-AD-FS/singleapp5a.PNG)

You will be able to now call the backend API to add ToDo List items for the logged-in user:

![Fiddler](media/Single-Page-Application-with-AD-FS/singleapp6.PNG)

## Next Steps
[AD FS Development](../../ad-fs/AD-FS-Development.md)  
