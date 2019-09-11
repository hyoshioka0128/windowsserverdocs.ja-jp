---
title: AD FS MSAL Web アプリ (サーバーアプリ) web Api の呼び出し
description: AD FS 2019 によって認証される web アプリのサインインユーザーを構築する方法について説明します。
author: billmath
ms.author: billmath
manager: daveba
ms.date: 08/09/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 03328ff8c94d96fcf34dcef29ac1a1daefc9d14a
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70867491"
---
# <a name="scenario-web-app-server-app-calling-web-api"></a>シナリオ:Web アプリ (サーバーアプリ) Web API の呼び出し 
>適用先:AD FS 2019 以降 
 
AD FS 2019 によって認証される web アプリのサインインユーザーを構築し、 [Msal ライブラリ](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet/wiki)を使用してトークンを取得して web api を呼び出す方法について説明します。  
 
この記事を読む前に、 [AD FS の概念](../ad-fs-openid-connect-oauth-concepts.md)と[認証コード付与フロー](../../overview/ad-fs-openid-connect-oauth-flows-scenarios.md#authorization-code-grant-flow)について理解しておく必要があります。
 
## <a name="overview"></a>概要 
 
![Web アプリ呼び出し web api の概要](media/adfs-msal-web-app-web-api/webapp1.png)

このフローでは、Web アプリ (サーバーアプリ) に認証を追加します。これにより、ユーザーはサインインして web API を呼び出すことができます。 Web アプリから Web API を呼び出すには、MSAL の[AcquireTokenByAuthorizationCode](https://docs.microsoft.com/en-us/dotnet/api/microsoft.identity.client.acquiretokenbyauthorizationcodeparameterbuilder?view=azure-dotnet) token の取得方法を使用します。 認証コードフローを使用して、取得したトークンをトークンキャッシュに格納します。 その後、コントローラーは必要に応じてキャッシュからトークンをサイレントに取得します。 必要に応じて、MSAL によってトークンが更新されます。 

Web Api を呼び出す Web Apps: 


- は、機密クライアントアプリケーションです。 
- そのため、AD FS でシークレット (アプリケーションの共有シークレット、証明書、または AD アカウント) が登録されています。 このシークレットは、トークンを取得するために AD FS の呼び出し時に渡されます。  

ADFS で Web アプリを登録する方法と、Web API を呼び出すトークンを取得するように構成する方法について理解を深めるには、[こちら](https://github.com/microsoft/adfs-sample-msal-dotnet-webapp-to-webapi)で入手できるサンプルを使用し、アプリの登録とコードの構成の手順について説明します。  

 
## <a name="pre-requisites"></a>前提条件 

- GitHub クライアントツール 
- AD FS 2019 以降が構成され、実行されています 
- Visual Studio 2013 以降 
 
## <a name="app-registration-in-ad-fs"></a>AD FS でのアプリの登録 
このセクションでは、Web アプリを機密クライアントおよび Web API として AD FS で証明書利用者 (RP) として登録する方法について説明します。 

  1. AD FS 管理 で、**アプリケーショングループ** を右クリックし、**アプリケーショングループの追加** を選択します。  
  2. アプリケーショングループウィザードの **[名前]** に「 **WebAppToWebApi** 」と入力し、 **[クライアント-サーバーアプリケーション]** で、 **Web API テンプレートにアクセスするサーバーアプリケーション**を選択します。 **[次へ]** をクリックします。  
  
      ![アプリケーショングループの追加](media/adfs-msal-web-app-web-api/webapp2.png)
  
  3. **クライアント識別子**の値をコピーします。 この値は、アプリケーションの**web.config**ファイルの**ida: ClientId**の値として後で使用されます。 **リダイレクト URI** - には、次のよう https://localhost:44326 に入力します。 [追加] をクリックします。 **[次へ]** をクリックします。 
  
      ![アプリケーショングループの追加](media/adfs-msal-web-app-web-api/webapp3.png)
  
  4. [アプリケーション資格情報の構成] 画面で、[**共有シークレットを生成**してシークレットをコピーする] チェックボックスをオンにします。 この値は、アプリケーションの**web.config**ファイルの**Ida: clientsecret**の値として後で使用されます。 **[次へ]** をクリックします。  
  
      ![アプリケーショングループの追加](media/adfs-msal-web-app-web-api/webapp4.png)
  
  5. [Web API の構成] 画面で、**識別子** https://webapi として「」を入力します。 **[追加]** をクリックします。 **[次へ]** をクリックします。 この値は、アプリケーションの**web.config**ファイルの**Ida: graphresourceid**で後で使用されます。 
  
      ![アプリケーショングループの追加](media/adfs-msal-web-app-web-api/webapp5.png)
  
  6. Access Control ポリシーの適用 画面で、すべてのユーザーを**許可**する を選択し、**次へ** をクリックします。 
  
      ![アプリケーショングループの追加](media/adfs-msal-web-app-web-api/webapp6.png)
  
  7. [アプリケーションのアクセス許可の構成] 画面で、 **openid**と**user_impersonation**が選択されていることを確認し、 **[次へ]** をクリックします。 
  
      ![アプリケーショングループの追加](media/adfs-msal-web-app-web-api/webapp7.png)
  
  8. 概要 画面で、**次へ** をクリックします。 
  
  9. 完了 画面で、**閉じる** をクリックします。



## <a name="code-configuration"></a>コードの構成 

このセクションでは、ASP.NET Web アプリを構成して、Web API を呼び出すために、サインインユーザーとトークンを取得する方法について説明します。 

  1. ここからサンプルをダウンロードして[ください](https://github.com/microsoft/adfs-sample-msal-dotnet-webapp-to-webapi)   
  
  2. Visual Studio を使用してサンプルを開く 
  
  3. Web.config ファイルを開きます。 次のように変更します。 
       - ida: ClientId-上の AD FS セクションの [アプリの登録] で #3 から**クライアント識別子**の値を入力します。 
       - ida: ClientSecret-上の AD FS セクションの [アプリの登録] の #4 から**シークレット**の値を入力します。 
       - ida: RedirectUri-前の AD FS セクションの「アプリの登録」の #3 から**リダイレクト uri**の値を入力します。 
       - ida: Authority- https://[your AD FS hostname]/adfs. を入力します 例: https://adfs.contoso.com/adfs 
       - ida: リソース-上の AD FS セクションの [アプリの登録] の #5 から**識別子**の値を入力します。 
      
          ![アプリケーショングループの追加](media/adfs-msal-web-app-web-api/webapp8.png)
 
 
### <a name="test-the-sample"></a>サンプルをテストする 
このセクションでは、上記で構成したサンプルをテストする方法について説明します。 

  1. コードの変更が行われたら、ソリューションをリビルドします。 
  
  2. Visual Studio の上部で、Internet Explorer が選択されていることを確認し、緑色の矢印をクリックします。 
  
      ![アプリケーショングループの追加](media/adfs-msal-web-app-web-api/webapp9.png)

  3. ホームページで、[サインイン] をクリックします。 
  
      ![アプリケーショングループの追加](media/adfs-msal-web-app-web-api/webapp10.png)

  4. AD FS サインインページにリダイレクトされます。 さあ、サインインします。 
  
      ![アプリケーショングループの追加](media/adfs-msal-web-app-web-api/webapp11.png)

  5. サインインしたら、[アクセストークン] をクリックします。  
  
      ![アプリケーショングループの追加](media/adfs-msal-web-app-web-api/webapp12.png)

  6. [アクセストークン] をクリックすると、Web API を呼び出すことによってアクセストークン情報が取得されます。 
  
      ![アプリケーショングループの追加](media/adfs-msal-web-app-web-api/webapp13.png)
 
 ## <a name="next-steps"></a>次の手順
[AD FS OpenID 接続/OAuth フローとアプリケーション シナリオ](../../overview/ad-fs-openid-connect-oauth-flows-scenarios.md)
 