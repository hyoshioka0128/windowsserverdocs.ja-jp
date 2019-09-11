---
title: AD FS MSAL ネイティブアプリでの Web API の呼び出し
description: AD FS 2019 によって認証され、MSAL ライブラリを使用してトークンを取得して web Api を呼び出すネイティブアプリのサインインユーザーを構築する方法を説明します。
author: billmath
ms.author: billmath
manager: daveba
ms.date: 08/09/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 588d717b8f03987b86af7dc0576d537ebd88c4ba
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70867617"
---
# <a name="scenario-native-app-calling-web-api"></a>シナリオ:ネイティブアプリ呼び出し Web API 
>適用先:AD FS 2019 以降 
 
AD FS 2019 によって認証され、 [Msal ライブラリ](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet/wiki)を使用してトークンを取得して web api を呼び出すネイティブアプリのサインインユーザーを構築する方法について説明します。  
 
この記事を読む前に、 [AD FS の概念](../ad-fs-openid-connect-oauth-concepts.md)と[認証コード付与フロー](../../overview/ad-fs-openid-connect-oauth-flows-scenarios.md#authorization-code-grant-flow)について理解しておく必要があります。
 
## <a name="overview"></a>概要 
 
 ![概要](media/adfs-msal-native-app-web-api/native1.png)

このフローでは、ネイティブアプリ (パブリッククライアント) に認証を追加します。これにより、ユーザーはサインインして Web API を呼び出すことができます。 ユーザーをサインインさせるネイティブアプリから Web API を呼び出すには、MSAL の[AcquireTokenInteractive](https://docs.microsoft.com/en-us/dotnet/api/microsoft.identity.client.ipublicclientapplication.acquiretokeninteractive?view=azure-dotnet#Microsoft_Identity_Client_IPublicClientApplication_AcquireTokenInteractive_System_Collections_Generic_IEnumerable_System_String__) token 取得方法を使用できます。 この対話を有効にするために、MSAL は web ブラウザーを活用します。 

 
アクセストークンを対話形式で取得するように ADFS でネイティブアプリを構成する方法について理解を深めるために、[こちら](https://github.com/microsoft/adfs-sample-msal-dotnet-native-to-webapi)で入手できるサンプルを使用して、アプリの登録とコードの構成手順を説明します。  
 

## <a name="pre-requisites"></a>前提条件 


- GitHub クライアントツール 
- AD FS 2019 以降が構成され、実行されています 
- Visual Studio 2013 以降 
 

## <a name="app-registration-in-ad-fs"></a>AD FS でのアプリの登録 
このセクションでは、ネイティブアプリをパブリッククライアントおよび Web API として証明書利用者 (RP) として登録する方法について説明し AD FS 

  1. **AD FS 管理** で、**アプリケーショングループ** を右クリックし、**アプリケーショングループの追加** を選択します。   
  
  2. アプリケーショングループウィザードの **[名前]** に「 **NativeAppToWebApi** 」と入力し、 **[クライアント-サーバーアプリケーション]** で、 **Web API テンプレートにアクセスするネイティブアプリケーション**を選択します。 **[次へ]** をクリックします。  
  
      ![アプリの Reg](media/adfs-msal-native-app-web-api/native2.png)  

  3. **クライアント識別子**の値をコピーします。 後でアプリケーションの**app.config**ファイルの**ClientId**の値として使用されます。 **リダイレクト URI** https://ToDoListClient には、次のように入力します。 **[追加]** をクリックします。 **[次へ]** をクリックします。  
 
     ![アプリの Reg](media/adfs-msal-native-app-web-api/native3.png) 

  4. [Web API の構成] 画面で、**識別子** https://localhost:44321/ として「」を入力します。 **[追加]** をクリックします。 **[次へ]** をクリックします。 この値**は、後でアプリケーションの app.config** **ファイルと web.config ファイル**で使用されます。
 
     ![アプリの Reg](media/adfs-msal-native-app-web-api/native4.png)   
  
  5. Access Control ポリシーの適用 画面で、**すべてのユーザーを許可**する を選択し、**次へ** をクリックします。 
  
     ![アプリの Reg](media/adfs-msal-native-app-web-api/native5.png)   
  
  6. アプリケーションのアクセス許可の構成 画面で  **openid** が選択されていることを確認し、**次へ** をクリックします。  
     
     ![アプリの Reg](media/adfs-msal-native-app-web-api/native6.png) 

  7. 概要 画面で、**次へ** をクリックします。
  
  8. 完了 画面で、**閉じる** をクリックします。 
  
  9. AD FS 管理 で、**アプリケーショングループ** をクリックし、**NativeAppToWebApi**アプリケーショングループ を選択します。 右クリックし、 **[プロパティ]** を選択します。
  
      ![アプリの Reg](media/adfs-msal-native-app-web-api/native7.png)

  10. NativeAppToWebApi のプロパティ 画面で、 **WEB api** の **NATIVEAPPTOWEBAPI – web api** を選択し、**編集...** をクリックします。 
  
      ![アプリの Reg](media/adfs-msal-native-app-web-api/native8.png) 

  11. NativeAppToWebApi-Web API のプロパティ 画面で、**発行変換規則** タブを選択し、**規則の追加...** をクリックします。 
  
      ![アプリの Reg](media/adfs-msal-native-app-web-api/native9.png) 

  12. 変換要求規則の追加ウィザードで、[**要求規則テンプレート**から**入力方向の要求を変換する**] を選択し、 **[次へ]** をクリックします。  
  
      ![アプリの Reg](media/adfs-msal-native-app-web-api/native10.png) 

  13. **[要求規則名:]** フィールドに「 **NameID** 」と入力します。 入力方向の要求の種類の**名前**を選択し**ます:** 、**出力方向の要求の種類**の**名前 id** : および**送信名 ID 形式**の**共通名**:。 **[完了]** をクリックします。
  
      ![アプリの Reg](media/adfs-msal-native-app-web-api/native11.png) 

  14. NativeAppToWebApi で [OK] をクリックします。 [Web API のプロパティ] 画面で、[NativeAppToWebApi のプロパティ] 画面をクリックします。  
 
## <a name="code-configuration"></a>コードの構成 
このセクションでは、サインインユーザーにネイティブアプリを構成し、Web API を呼び出すトークンを取得する方法について説明します。 

1. ここからサンプルをダウンロードして[ください](https://github.com/microsoft/adfs-sample-msal-dotnet-native-to-webapi) 

2. Visual Studio を使用してサンプルを開く 

3. App.config ファイルを開きます。 次のように変更します。 
   - ida: Authority: 「 https://[your AD FS hostname]/adfs」と入力します。
   - ida: ClientId-上の AD FS セクションの [アプリの登録] で #3 から**クライアント識別子**の値を入力します。 
   - ida: RedirectUri-前の AD FS セクションの「アプリの登録」の #3 から**リダイレクト uri**の値を入力します。
   - todo: TodoListResourceId-上の AD FS セクションのアプリ登録で #4 から**識別子**の値を入力してください 
   - ida: todo: TodoListBaseAddress-上記の AD FS セクションの「アプリの登録」の #4 から**識別子**の値を入力します。 
 
     ![コード構成](media/adfs-msal-native-app-web-api/native12.png)

 4. Web.config ファイルを開きます。 次のように変更します。 
    - ida: Audience-上の AD FS セクションのアプリ登録で #4 から**識別子**の値を入力します 
    - idaAdfsMetadataEndpoint-「 https://[your AD FS hostname]/federationmetadata/2007-06/federationmetadata.xml」と入力します。 
    
      ![コード構成](media/adfs-msal-native-app-web-api/native13.png)
 
  
## <a name="test-the-sample"></a>サンプルをテストする 
このセクションでは、上記で構成したサンプルをテストする方法について説明します。 

  1. コードの変更が行われたら、ソリューションをリビルドします。 
 
  2. Visual Studio で、ソリューションを右クリックし、 **[スタートアッププロジェクトの設定...]** を選択します。  
 
     ![アプリのテスト](media/adfs-msal-native-app-web-api/native14.png)

  3. プロパティページ で、各プロジェクトの **アクション** が **開始** に設定されていることを確認します。 
      
     ![アプリのテスト](media/adfs-msal-native-app-web-api/native15.png)

  4. Visual Studio の上部にある緑色の矢印をクリックします。  
 
     ![アプリのテスト](media/adfs-msal-native-app-web-api/native16.png)

  5. ネイティブアプリのメイン画面で、 **[サインイン]** をクリックします。  
  
     ![アプリのテスト](media/adfs-msal-native-app-web-api/native17.png)

    ネイティブアプリの画面が表示されない場合は、プロジェクトリポジトリがシステムに保存されているフォルダーから * msalcache. bin ファイルを検索して削除します。 

  6. AD FS サインインページにリダイレクトされます。 さあ、サインインします。 
  
      ![アプリのテスト](media/adfs-msal-native-app-web-api/native18.png)

  7. サインインしたら、 **Create a To Do 項目**に「 **Build Native App to Web Api** 」と入力します。 **[項目の追加]** をクリックします。  これ**により To Do List サービス (WEB API)** が呼び出され、キャッシュに項目が追加されます。 
    
       ![アプリのテスト](media/adfs-msal-native-app-web-api/native19.png)
 
## <a name="next-steps"></a>次の手順
[AD FS OpenID 接続/OAuth フローとアプリケーション シナリオ](../../overview/ad-fs-openid-connect-oauth-flows-scenarios.md)
 