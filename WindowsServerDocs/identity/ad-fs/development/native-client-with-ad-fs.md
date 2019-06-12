---
title: AD FS 2016 で OAuth パブリック クライアントを使用してアプリケーションまたはそれ以降のネイティブ クライアントを構築します。
description: OAuth パブリック クライアントと AD FS 2016 を使用してアプリケーションまたはそれ以降のネイティブ クライアントの作成手順について説明するチュートリアル
author: billmath
ms.author: billmath
ms.reviewer: anandy
manager: mtillman
ms.date: 07/17/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: active-directory-federation-services
ms.openlocfilehash: 15bb6f1e39f64ff19ebb5515188ee944e277d3b7
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445479"
---
# <a name="build-a-native-client-application-using-oauth-public-clients-with-ad-fs-2016-or-later"></a>AD FS 2016 で OAuth パブリック クライアントを使用してアプリケーションまたはそれ以降のネイティブ クライアントを構築します。

## <a name="overview"></a>概要

この記事では、AD FS 2016 によって保護されている、またはそれ以降は、Web API と連携するネイティブ アプリケーションを作成する方法を示します。

1. .Net TodoListClient WPF アプリケーションでは、Active Directory Authentication Library (ADAL) を使用して、Azure Active Directory (Azure AD) から OAuth 2.0 プロトコルを介して JWT アクセス トークンを取得
2. アクセス トークンは、ベアラー トークンとして TodoListService web API の/todolist エンドポイントを呼び出すときにユーザーの認証に使用されます。
 私たちは、Azure AD は、ここの例では、アプリケーションを使用してはし、for AD FS 2016 以降に変更します。

![アプリケーションの概要](media/native-client-with-ad-fs-2016/appoverview.png)

## <a name="pre-requisites"></a>前提条件
このドキュメントを完了する前に必要な前提条件の一覧を次に示します。 このドキュメントは、AD FS がインストールされており、AD FS ファームが作成されたことを想定しています。

* GitHub のクライアント ツール
* Windows Server 2016 以降の AD FS
* Visual Studio 2013 またはそれ以降

## <a name="creating-the-sample-walkthrough"></a>サンプルのチュートリアルを作成します。

### <a name="create-the-application-group-in-ad-fs"></a>AD FS でのアプリケーション グループを作成します。

1. AD FS の管理 を右クリックし**アプリケーション グループ**選択**アプリケーション グループの追加**します。

2. アプリケーション グループ ウィザードで、名前 NativeToDoListAppGroup など、必要に応じて名前を入力します。 選択、 **web API にアクセスするネイティブ アプリケーション**テンプレート。 **[次へ]** をクリックします。
 ![アプリケーション グループを追加します。](media/native-client-with-ad-fs-2016/addapplicationgroup1.png)

3. **ネイティブ アプリケーション**] ページの [AD FS によって生成される id に注意してください。 これは、AD FS がパブリック クライアント アプリを認識する id です。 コピー、**クライアント識別子**値。 後の値として使用する**ida: ClientId**アプリケーション コードにします。 する場合は、ここで、カスタムの識別子を指定できます。 リダイレクト URI は、任意の値、例では、配置 https://ToDoListClient![ネイティブ アプリ](media/native-client-with-ad-fs-2016/addapplicationgroup2.png)

4. **Web API の構成** ページで、Web API の識別子の値を設定します。 この例での値があります、 **SSL URL** Web アプリが実行されているはずです。 ソリューションの TooListServer プロジェクトのプロパティをクリックして、この値を取得できます。 これは後で使用されますとして、 **todo:TodoListResourceId**値**App.config**ネイティブ クライアント アプリケーションとも、ファイル、 **todo:TodoListBaseAddress**します。
![Web API](media/native-client-with-ad-fs-2016/addapplicationgroup3.png)

5. 通し、**アクセス制御ポリシーの適用**と**アプリケーションのアクセス許可を構成する**場所に既定値で。 [概要] ページを以下のようになります。
![概要](media/native-client-with-ad-fs-2016/addapplicationgroupsummary.png)

[次へ] をクリックし、ウィザードを完了します。

### <a name="add-the-nameidentifier-claim-to-the-list-of-claims-issued"></a>発行された要求の一覧に NameIdentifier 要求を追加します。
デモ アプリケーションでは、さまざまな場所で NameIdentifier 要求の値を使用します。 Azure AD とは異なり AD FS は、既定で NameIdentifier 要求を発行しません。 そのため、アプリケーションは、適切な値を使用できるように、NameIdentifier 要求を発行する要求規則を追加する必要があります。 この例では、トークン内のユーザーの NameIdentifier 値として、ユーザーの指定した名前が発行されます。
要求規則を構成するに先ほど作成したアプリケーション グループを開き、Web API をダブルクリックします。 発行変換規則 タブを選択し、規則の追加 ボタンをクリックします。 で要求規則の種類では、カスタム要求規則を選択し、次に示すように、要求規則を追加します。

```  
c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"]
 => issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier"), query = ";givenName;{0}", param = c.Value);
```

![NameIdentifier 要求の規則](media/native-client-with-ad-fs-2016/addnameidentifierclaimrule.png)

### <a name="modify-the-application-code"></a>アプリケーション コードを変更します。

このセクションでは、Web API のサンプルをダウンロードして Visual Studio で変更する方法について説明します。   Azure AD のサンプルを使用する[ここ](https://github.com/Azure-Samples/active-directory-dotnet-native-desktop)します。  

サンプル プロジェクトをダウンロードし、Git Bash を使用して、次を入力します。  

```  
git clone https://github.com/Azure-Samples/active-directory-dotnet-native-desktop  
```  

#### <a name="modify-todolistclient"></a>ToDoListClient を変更します。

このプロジェクトをソリューションには、ネイティブ クライアント アプリケーションを表します。 クライアント アプリケーションを知っていることを確認する必要があります。

1. 必要な場合に認証されたユーザーを取得する場所ですか。
2. そのクライアント ID は認証機関 (AD FS) を提供する必要がありますか。
3. アクセス トークンは要求したリソースの ID とは何ですか。
4. Web API のベース アドレスとは何ですか。

ネイティブ クライアント アプリケーションには、上記の情報を取得するには、次のコード変更が必要です。

**App.config**

* キーを追加**ida: 機関**AD FS サービスを示す値を使用します。 たとえば、 https://fs.contoso.com/adfs/ と記述します。
* 変更**ida: ClientId**キーから値を**クライアント識別子**で、**ネイティブ アプリケーション**AD FS でアプリケーション グループの作成中にページ。 たとえば、3f07368b-6efd-4f50-a330-d93853f4c855
* 変更、 **todo:todo:TodoListResourceId**から値を持つ**識別子**で、 **Web API の構成**AD FS でアプリケーション グループの作成中にページ。 たとえば、 https://localhost:44321/ と記述します。
* 変更、 **todo:TodoListBaseAddress**から値を持つ**識別子**で、 **Web API の構成**AD FS でアプリケーション グループの作成中にページ。 たとえば、 https://localhost:44321/ と記述します。
* 値を設定**ida: RedirectUri**から値を持つ**リダイレクト URI**で、**ネイティブ アプリケーション**AD FS でアプリケーション グループの作成中にページ。 たとえば、 https://ToDoListClient と記述します。
* 読みやすさの削除/コメントのキー **ida: テナント**と**ida: AADInstance**します。

  ![アプリの構成](media/native-client-with-ad-fs-2016/app_configfile.PNG)


**MainWindow.xaml.cs**

* 行を次に示すよう aadInstance をコメントします。

        // private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];

* 次に示すように機関の値を追加します。

        private static string authority = ConfigurationManager.AppSettings["ida:Authority"];

* 作成するための行を削除、**機関**aadInstance とテナントからの値

        private static string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);

* 関数で**MainWindow**に authContext インスタンス化の変更

        authContext = new AuthenticationContext(authority,false);

    ADAL は機関として AD FS の検証をサポートしていませんし、validateAuthority パラメーターの値の false のフラグを渡す必要がそのためです。

  ![メイン ウィンドウ](media/native-client-with-ad-fs-2016/mainwindow.PNG)

#### <a name="modify-todolistservice"></a>TodoListService を変更します。
2 つのファイルには、web.config ファイルと Startup.Auth.cs – このプロジェクト内の変更が必要があります。 パラメーターの正しい値を取得するには、Web.Config の変更が必要です。 Azure AD ではなく、AD FS に対して認証する WebAPI を設定するのには、Startup.Auth.cs 変更が必要です。

**Web.config**

* キーをコメント**ida: テナント**必要があると
* キーを追加します**ida: 機関**フェデレーションの FQDN を示す値を持つサービス、例では、 https://fs.contoso.com/adfs/
* キーを変更**ida: Audience**で指定した Web API 識別子の値を持つ、 **Web API の構成**AD FS でアプリケーション グループの追加中にページ。
* キーを追加**ida: AdfsMetadataEndpoint** AD FS のフェデレーション メタデータ URL に対応する値を持つサービスでは、ex: https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml

![Web の構成](media/native-client-with-ad-fs-2016/webconfig.PNG)


**Startup.Auth.cs**

次に示すよう ConfigureAuth 関数を変更します。

    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseActiveDirectoryFederationServicesBearerAuthentication(
            new ActiveDirectoryFederationServicesBearerAuthenticationOptions
            {
                MetadataEndpoint = ConfigurationManager.AppSettings["ida:AdfsMetadataEndpoint"],
                TokenValidationParameters = new TokenValidationParameters()
                {
                    SaveSigninToken = true,
                    ValidAudience = ConfigurationManager.AppSettings["ida:Audience"]
                }

            });
    }

基本的には、AD FS を使用して、さらに、AD FS のメタデータに関する情報を提供し、トークンを検証する認証を構成しています、audience クレームは、Web API で想定されている値である必要があります。
アプリケーションの実行

1. Nativeclient-dotnet ソリューションを右クリックし、プロパティに移動します。 複数のスタートアップ プロジェクトに次のようにスタートアップ プロジェクトを変更し、開始する、TodoListClient と TodoListService の両方を設定します。
![ソリューションのプロパティ](media/native-client-with-ad-fs-2016/solutionproperties.png)

2.  F5 キーを押してボタンを押すか、デバッグを選択 > メニュー バーで続行します。 これには、ネイティブ クライアント アプリケーションと、web Api の両方が起動します。 ネイティブ アプリケーションにサインイン ボタンをクリックし、AD AL から対話型ログオンをポップアップ ウィンドウには、AD FS サービスにリダイレクトします。 有効なユーザーの資格情報を入力します。
![サインイン](media/native-client-with-ad-fs-2016/sign-in.png)

この手順で、ネイティブ アプリケーションが AD FS にリダイレクトされ、Web API の ID トークンとアクセス トークンを取得しました

3. 入力、項目のテキスト ボックスに行い、[項目の追加] をクリックします。 この手順でアプリケーションへの到達追加する Web API の todo 項目をそのためは、AD FS から取得した web Api にアクセス トークンを提示します。 Web API では、トークンのためのものし、フェデレーション メタデータから情報を使用してトークンの署名を検証するかどうかを確認する対象ユーザーの値と一致します。

![サインイン](media/native-client-with-ad-fs-2016/clienttodoadd.png)

## <a name="next-steps"></a>次の手順
[AD FS の開発](../../ad-fs/AD-FS-Development.md)  
