---
title: AD FS 2016 以降の OAuth パブリッククライアントを使用してネイティブクライアントアプリケーションを構築する
description: OAuth パブリッククライアントを使用してネイティブクライアントアプリケーションを構築する手順を示すチュートリアルと AD FS 2016 以降
author: billmath
ms.author: billmath
ms.reviewer: anandy
manager: mtillman
ms.date: 07/17/2018
ms.topic: article
ms.prod: windows-server
ms.technology: active-directory-federation-services
ms.openlocfilehash: cecffe6ae789c4a7c8c9ff382e83d84ade8ef018
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2020
ms.locfileid: "87519851"
---
# <a name="build-a-native-client-application-using-oauth-public-clients-with-ad-fs-2016-or-later"></a>AD FS 2016 以降の OAuth パブリッククライアントを使用してネイティブクライアントアプリケーションを構築する

## <a name="overview"></a>概要

この記事では、AD FS 2016 以降で保護されている Web API と対話するネイティブアプリケーションを構築する方法について説明します。

1. .Net TodoListClient WPF アプリケーションは、Active Directory 認証ライブラリ (ADAL) を使用して Azure Active Directory (Azure AD) から OAuth 2.0 プロトコルを介して JWT アクセストークンを取得します。
2. アクセストークンは、TodoListService web API の/todolist エンドポイントを呼び出すときにユーザーを認証するためのベアラートークンとして使用されます。
 ここでは Azure AD のアプリケーションの例を使用し、AD FS 2016 以降に変更します。

![アプリケーションの overivew](media/native-client-with-ad-fs-2016/appoverview.png)

## <a name="pre-requisites"></a>前提条件
このドキュメントを完了する前に必要な前提条件の一覧を次に示します。 このドキュメントでは、AD FS がインストールされ、AD FS ファームが作成されていることを前提としています。

* GitHub クライアントツール
* Windows Server 2016 以降の AD FS
* Visual Studio 2013 以降

## <a name="creating-the-sample-walkthrough"></a>サンプルチュートリアルの作成

### <a name="create-the-application-group-in-ad-fs"></a>AD FS でアプリケーショングループを作成します。

1. AD FS 管理] で、[**アプリケーショングループ**] を右クリックし、[**アプリケーショングループの追加**] を選択します。

2. アプリケーショングループウィザードで、[名前] に任意の名前 (例: NativeToDoListAppGroup) を入力します。 **WEB API テンプレートにアクセスするネイティブアプリケーション**を選択します。 **[次へ]** をクリックします。
 ![アプリケーショングループの追加](media/native-client-with-ad-fs-2016/addapplicationgroup1.png)

3. [**ネイティブアプリケーション**] ページで、AD FS によって生成された識別子を確認します。 これは、AD FS がパブリッククライアントアプリを認識する id です。 [**クライアント識別子**の値をコピーします。 この値は、アプリケーションコードで**ida: ClientId**の値として後で使用されます。 必要に応じて、ここで任意のカスタム識別子を指定できます。 リダイレクト URI は任意の値です。たとえば、 https://ToDoListClient ![ ネイティブアプリを配置します。](media/native-client-with-ad-fs-2016/addapplicationgroup2.png)

4. [ **WEB api の構成**] ページで、web api の識別子の値を設定します。 この例では、これは Web アプリが実行されていると考えられる**SSL URL**の値にする必要があります。 この値を取得するには、ソリューション内の TooListServer プロジェクトのプロパティをクリックします。 これは、ネイティブクライアントアプリケーションの**App.config**ファイルの**todo: TodoListResourceId**値として、また**todo: TodoListBaseAddress**として後で使用されます。
![Web API](media/native-client-with-ad-fs-2016/addapplicationgroup3.png)

5. [ **Access Control ポリシーの適用**] を実行し、既定値を設定した状態で**アプリケーションのアクセス許可を構成**します。 [概要] ページは次のようになります。
![まとめ](media/native-client-with-ad-fs-2016/addapplicationgroupsummary.png)

[次へ] をクリックし、ウィザードを完了します。

### <a name="add-the-nameidentifier-claim-to-the-list-of-claims-issued"></a>発行された要求の一覧に NameIdentifier 要求を追加します。
デモアプリケーションでは、さまざまな場所で NameIdentifier claim の値を使用します。 Azure AD とは異なり、AD FS は既定で NameIdentifier 要求を発行しません。 そのため、NameIdentifier 要求を発行する要求規則を追加して、アプリケーションが正しい値を使用できるようにする必要があります。 この例では、指定されたユーザー名が、トークン内のユーザーの NameIdentifier 値として発行されます。
要求規則を構成するには、先ほど作成したアプリケーショングループを開き、Web API をダブルクリックします。 [発行変換規則] タブを選択し、[規則の追加] ボタンをクリックします。 要求規則の種類で、[カスタム要求規則] を選択し、次のように要求規則を追加します。

```
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"]
 => issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier"), query = ";givenName;{0}", param = c.Value);
```

![NameIdentifier 要求規則](media/native-client-with-ad-fs-2016/addnameidentifierclaimrule.png)

### <a name="modify-the-application-code"></a>アプリケーション コードの変更

このセクションでは、サンプル Web API をダウンロードし、Visual Studio で変更する方法について説明します。   [ここに記載](https://github.com/Azure-Samples/active-directory-dotnet-native-desktop)されている Azure AD サンプルを使用します。

サンプルプロジェクトをダウンロードするには、Git Bash を使用し、次のように入力します。

```
git clone https://github.com/Azure-Samples/active-directory-dotnet-native-desktop
```

#### <a name="modify-todolistclient"></a>ToDoListClient の変更

ソリューション内のこのプロジェクトは、ネイティブクライアントアプリケーションを表します。 クライアントアプリケーションが次のことを認識していることを確認する必要があります。

1. 必要に応じてユーザーを認証するには、どこに移動すればよいですか。
2. クライアントが認証機関 (AD FS) に提供する必要がある ID は何ですか。
3. アクセストークンを要求しているリソースの ID は何ですか。
4. Web API のベースアドレスとは何ですか。

ネイティブクライアントアプリケーションに上記の情報を取得するには、次のコード変更が必要です。

**App.config**

* AD FS サービスを表す値を持つキー **ida: Authority**を追加します。 たとえば、https://fs.contoso.com/adfs/ のように指定します。
* AD FS でのアプリケーショングループの作成時に、**ネイティブアプリケーション**ページで [**クライアント識別子**] の値を使用して**ida: ClientId**キーを変更します。 たとえば、3f07368b-6efd-4f50-a330-d93853f4c855 のようになります。
* AD FS でアプリケーショングループを作成するときに、[ **WEB API の構成**] ページの [**識別子**] の値を使用して**todo: todo: TodoListResourceId**を変更します。 たとえば、https://localhost:44321/ のように指定します。
* AD FS でアプリケーショングループを作成するときに、[ **WEB API の構成**] ページの [**識別子**] の値を使用して**todo: TodoListBaseAddress**を変更します。 たとえば、https://localhost:44321/ のように指定します。
* AD FS でのアプリケーショングループの作成時に、**ネイティブアプリケーション**ページの [**リダイレクト uri** ] の値を使用して**ida: redirecturi**の値を設定します。 たとえば、https://ToDoListClient のように指定します。
* 読みやすくするために、 **ida: Tenant**と**ida: AADInstance**のキーを削除/コメントすることができます。

  ![アプリの構成](media/native-client-with-ad-fs-2016/app_configfile.PNG)

**MainWindow.xaml.cs**

* 次のように aadInstance の行をコメント化します。

    `// private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];`

* 次のように authority の値を追加します。

    `private static string authority = ConfigurationManager.AppSettings["ida:Authority"];`

* AadInstance とテナントから**機関**の値を作成するための行を削除します。

    `private static string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);`

* 関数**mainwindow.xaml**で、authcontext のインスタンス化をに変更します。

   `authContext = new AuthenticationContext(authority,false);`

    ADAL は、authority AD FS の検証をサポートしていないため、validateAuthority パラメーターに false 値フラグを渡す必要があります。

  ![メイン ウィンドウ](media/native-client-with-ad-fs-2016/mainwindow.PNG)

#### <a name="modify-todolistservice"></a>TodoListService の変更
このプロジェクトには、Web.config と Startup.Auth.cs という2つのファイルが必要です。 パラメーターの正しい値を取得するには、Web.Config の変更が必要です。 Azure AD ではなく AD FS に対して認証するように WebAPI を設定するには、Startup.Auth.cs の変更が必要です。

**Web.config**

* 必要ではないため、キー **ida: テナント**にコメントを付けます
* フェデレーションサービスの FQDN (例:) を示す値を持つ**ida: Authority**のキーを追加します。https://fs.contoso.com/adfs/
* キー **ida:** [アプリケーショングループの追加] の [ **Web api の構成**] ページで指定した web api 識別子の値を AD FS に変更します。
* AD FS サービスのフェデレーションメタデータ URL に対応する値を持つキー **ida: AdfsMetadataEndpoint**を追加します。次に例を示します。https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml

![Web 構成](media/native-client-with-ad-fs-2016/webconfig.PNG)

**Startup.Auth.cs**

ConfigureAuth 関数を次のように変更します。

```
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
```

基本的には、AD FS を使用し、AD FS メタデータに関する情報をさらに提供するように認証を構成し、トークンを検証するために、Web API によって想定される値を対象ユーザー要求にする必要があります。
アプリケーションの実行

1. ソリューション DotNet で、右クリックし、[プロパティ] にアクセスします。 次に示すように、スタートアッププロジェクトを複数のスタートアッププロジェクトに変更し、TodoListClient と TodoListService の両方を Start に設定します。
![ソリューションのプロパティ](media/native-client-with-ad-fs-2016/solutionproperties.png)

2.  F5 キーを押すか、メニューバーの [デバッグ > 続行] を選択します。 これにより、ネイティブアプリケーションと WebAPI の両方が起動されます。 ネイティブアプリケーションの [サインイン] ボタンをクリックすると、AD AL からの対話型ログオンがポップアップ表示され、AD FS サービスにリダイレクトされます。 有効なユーザーの資格情報を入力してください。
![サインイン](media/native-client-with-ad-fs-2016/sign-in.png)

この手順では、ネイティブアプリケーションが AD FS にリダイレクトされ、Web API の ID トークンとアクセストークンが返されます。

3. テキストボックスに to do アイテムを入力し、[アイテムの追加] をクリックします。 この手順では、アプリケーションが Web API に到達して to do 項目を追加します。そのために、AD FS から取得した WebAPI にアクセストークンを提示します。 Web API は、対象ユーザーの値と照合して、トークンが想定されていることを確認し、フェデレーションメタデータからの情報を使用してトークンの署名を検証します。

![サインイン](media/native-client-with-ad-fs-2016/clienttodoadd.png)

## <a name="next-steps"></a>次の手順
[AD FS の開発](../../ad-fs/AD-FS-Development.md)
