---
title: OAuth を使用し、AD FS 2016 以降の ADAL.JS で単一ページ web アプリケーションを構築する
description: AngularJS ベースのシングルページアプリケーションをセキュリティで保護する JavaScript 用 ADAL を使用して AD FS に対して認証するための手順を提供するチュートリアルです。
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 06/13/2018
ms.topic: article
ms.openlocfilehash: c615bd6426098e00854e873d3e1eb2cfbfaa0734
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87970939"
---
# <a name="build-a-single-page-web-application-using-oauth-and-adaljs-with-ad-fs-2016-or-later"></a>OAuth を使用し、AD FS 2016 以降の ADAL.JS で単一ページ web アプリケーションを構築する

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
このチュートリアルでは、Visual Studio 2015 を使用します。 プロジェクトは ADAL JS ライブラリを使用します。 ADAL の詳細については[Active Directory 認証ライブラリ .net](/dotnet/api/microsoft.identitymodel.clients.activedirectory?view=azure-dotnet)をご覧ください。

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

```
git clone https://github.com/Azure-Samples/active-directory-angularjs-singlepageapp.git
```

## <a name="about-the-code"></a>コードについて
認証ロジックを含むキーファイルは次のとおりです。

**App.js** -adal モジュールの依存関係が挿入され、adal によって使用されるアプリ構成値が提供されます。これにより、AAD とのプロトコルの対話が促進され、以前の認証なしにアクセスする必要のあるルートが示されます。

**index.html** -への参照が含まれて adal.js

**HomeController.js**-ADAL で login () メソッドと logOut () メソッドを活用する方法について説明します。

**UserDataController.js** -キャッシュされた id_token からユーザー情報を抽出する方法について説明します。

**Startup.Auth.cs** -ベアラー認証に Active Directory フェデレーションサービスを使用するための構成が含まれています。

## <a name="registering-the-public-client-in-ad-fs"></a>AD FS にパブリッククライアントを登録しています
このサンプルでは、WebAPI はでリッスンするように構成されてい https://localhost:44326/ ます。 **Web アプリケーションにアクセス**するアプリケーショングループ web ブラウザーは、暗黙的な許可フローアプリケーションを構成するために使用できます。

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

**app.js**ファイルを開き、 **adalProvider.init**定義を次のように変更します。

```
    adalProvider.init(
        {
            instance: 'https://fs.contoso.com/', // your STS URL
            tenant: 'adfs',                      // this should be adfs
            clientId: 'https://localhost:44326/', // your client ID of the
            //cacheLocation: 'localStorage', // enable this for IE, as sessionStorage does not work for localhost.
        },
        $httpProvider
    );
```

|構成|説明|
|--------|--------|
|instance|STS の URL (例:https://fs.contoso.com/|
|tenant|' Adfs ' として保持する|
|clientID|これは、シングルページアプリケーションのパブリッククライアントを構成するときに指定したクライアント ID です。|

## <a name="configure-webapi-to-use-ad-fs"></a>AD FS を使用するように WebAPI を構成する
サンプルの**Startup.Auth.cs**ファイルを開き、先頭に次のコードを追加します。

```
    using System.IdentityModel.Tokens;

remove:

    app.UseWindowsAzureActiveDirectoryBearerAuthentication(
        new WindowsAzureActiveDirectoryBearerAuthenticationOptions
        {
            Audience = ConfigurationManager.AppSettings["ida:Audience"],
            Tenant = ConfigurationManager.AppSettings["ida:Tenant"]
        }
    );

and add:

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
```

|パラメーター|説明|
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

## <a name="running-the-solution"></a>ソリューションの実行
ソリューションをクリーンアップし、ソリューションをリビルドして実行します。 詳細なトレースを表示する場合は、Fiddler を起動し、HTTPS の暗号化解除を有効にします。

ブラウザー (Chrome ブラウザーを使用) によって SPA が読み込まれ、次の画面が表示されます。

![クライアントを登録する](media/Single-Page-Application-with-AD-FS/singleapp3.PNG)

[ログイン] をクリックします。  ToDo リストは認証フローをトリガーし、ADAL JS は認証をに送信し AD FS

![ログイン](media/Single-Page-Application-with-AD-FS/singleapp4a.PNG)

Fiddler では、# fragment の URL の一部として返されるトークンを確認できます。

![Fiddler](media/Single-Page-Application-with-AD-FS/singleapp5a.PNG)

バックエンド API を呼び出して、ログインしているユーザーの ToDo リスト項目を追加できるようになりました。

![Fiddler](media/Single-Page-Application-with-AD-FS/singleapp6.PNG)

## <a name="next-steps"></a>次の手順
[AD FS の開発](../../ad-fs/AD-FS-Development.md)
