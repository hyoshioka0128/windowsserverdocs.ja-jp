---
title: Web API を呼び出す AD FS MSAL Web api (シナリオに代わって)
description: 別の Web API を呼び出す Web API を構築する方法について説明します。
author: billmath
ms.author: billmath
manager: daveba
ms.date: 08/09/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 2ab6141b84d03102c5dedd1ede0ba99e5adf3e4a
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70867748"
---
# <a name="scenario-web-api-calling-web-api-on-behalf-of-scenario"></a>シナリオ:Web api 呼び出し Web API (シナリオの代理) 
> 適用先:AD FS 2019 以降 
 
ユーザーの代わりに別の Web API を呼び出す Web API を構築する方法について説明します。  
 
この記事を読む前に、 [AD FS の概念](../ad-fs-openid-connect-oauth-concepts.md)と[Behalf_Of flow](../../overview/ad-fs-openid-connect-oauth-flows-scenarios.md#on-behalf-of-flow)について理解しておく必要があります。

## <a name="overview"></a>概要 


- クライアント (Web アプリ)-次の図では示されていません-保護された Web API を呼び出し、その "Authorization" Http ヘッダーに JWT ベアラートークンを提供します。 
- 保護された Web api はトークンを検証し、msal [AcquireTokenOnBehalfOf](https://docs.microsoft.com/en-us/dotnet/api/microsoft.identitymodel.clients.activedirectory.authenticationcontext.acquiretokenasync?view=azure-dotnet#Microsoft_IdentityModel_Clients_ActiveDirectory_AuthenticationContext_AcquireTokenAsync_System_String_Microsoft_IdentityModel_Clients_ActiveDirectory_ClientCredential_Microsoft_IdentityModel_Clients_ActiveDirectory_UserAssertion_) メソッドを使用して別のトークンを (AD FS から) 要求します。これにより、ユーザーの代わりに2つ目の web api (下流の web api) を呼び出すことができます。 
- 保護された web API は、このトークンを使用して下流 API を呼び出します。 また、AcquireTokenSilentlater を呼び出して、他の下流 Api (ただし、同じユーザーの代わりに) のトークンを要求することもできます。 AcquireTokenSilent は、必要に応じてトークンを更新します。  
 
     ![概要](media/adfs-msal-web-api-web-api/webapi1.png)
 
ADFS で auth シナリオに代わってを構成する方法を理解するには、[こちら](https://github.com/microsoft/adfs-sample-msal-dotnet-webapi-to-webapi-onbehalfof)で入手できるサンプルを使用し、アプリの登録とコードの構成の手順について説明します。  
 
## <a name="pre-requisites"></a>前提条件 

- GitHub クライアントツール 
- AD FS 2019 以降が構成され、実行されています 
- Visual Studio 2013 以降 
 
## <a name="app-registration-in-ad-fs"></a>AD FS でのアプリの登録 

このセクションでは、ネイティブアプリをパブリッククライアントおよび Web Api として AD FS の証明書利用者 (RP) として登録する方法について説明します。 

  1. AD FS 管理 で、**アプリケーショングループ** を右クリックし、**アプリケーショングループの追加** を選択します。  
  
  2. アプリケーショングループウィザードの **[名前]** に「 **WebApiToWebApi** 」と入力し、 **[クライアント-サーバーアプリケーション]** で、 **Web API テンプレートにアクセスするネイティブアプリケーション**を選択します。 **[次へ]** をクリックします。

      ![アプリの登録](media/adfs-msal-web-api-web-api/webapi2.png)

  3. **クライアント識別子**の値をコピーします。 後でアプリケーションの**app.config**ファイルの**ClientId**の値として使用されます。 **リダイレクト URI** - には、次のよう https://ToDoListClient に入力します。 **[追加]** をクリックします。 **[次へ]** をクリックします。 
  
      ![アプリの登録](media/adfs-msal-web-api-web-api/webapi3.png)
  
  4. [Web API の構成] 画面で、**識別子** https://localhost:44321/ として「」を入力します。 **[追加]** をクリックします。 **[次へ]** をクリックします。 この値**は、後でアプリケーションの app.config** **ファイルと web.config ファイル**で使用されます。  
 
      ![アプリの登録](media/adfs-msal-web-api-web-api/webapi4.png)

  5. Access Control ポリシーの適用 画面で、**すべてのユーザーを許可**する を選択し、**次へ** をクリックします。 
  
      ![アプリの登録](media/adfs-msal-web-api-web-api/webapi5.png)  

  6. [アプリケーションのアクセス許可の構成] 画面で、[ **openid** and **user_impersonation**] を選択します。 **[次へ]** をクリックします。  
  
      ![アプリの登録](media/adfs-msal-web-api-web-api/webapi6.png)  

  7. 概要 画面で、**次へ** をクリックします。 

  8. 完了 画面で、**閉じる** をクリックします。 


  9. AD FS 管理 で、**アプリケーショングループ** をクリックし、**WebApiToWebApi**アプリケーショングループ を選択します。 右クリックし、 **[プロパティ]** を選択します。 
  
      ![アプリの登録](media/adfs-msal-web-api-web-api/webapi7.png)  

  10. WebApiToWebApi のプロパティ 画面で、**アプリケーションの追加...** をクリックします。 
  
      ![アプリの Reg](media/adfs-msal-web-api-web-api/webapi8.png)

  11. スタンドアロンアプリケーション で、**サーバーアプリケーション** を選択します。  
  
      ![アプリの Reg](media/adfs-msal-web-api-web-api/webapi9.png)

  12. サーバーアプリケーション画面で、を https://localhost:44321/ **クライアント識別子**および**リダイレクト URI**として追加します。 
  
      ![アプリの Reg](media/adfs-msal-web-api-web-api/webapi10.png)

  13. アプリケーション資格情報の構成 画面で、**共有シークレットの生成** を選択します。 後で使用するためにシークレットをコピーします。
  
      ![アプリの Reg](media/adfs-msal-web-api-web-api/webapi11.png)

  14. 概要 画面で、**次へ** をクリックします。 

  15. 完了 画面で、**閉じる** をクリックします。 

  16. AD FS 管理 で、**アプリケーショングループ** をクリックし、**WebApiToWebApi**アプリケーショングループ を選択します。 右クリックし、 **[プロパティ]** を選択します。 
  
      ![アプリの Reg](media/adfs-msal-web-api-web-api/webapi12.png)

  17. WebApiToWebApi のプロパティ 画面で、**アプリケーションの追加...** をクリックします。 
  
      ![アプリの Reg](media/adfs-msal-web-api-web-api/webapi13.png)

  18. スタンドアロンアプリケーション で、 **WEB API** を選択します。 
  
      ![アプリの Reg](media/adfs-msal-web-api-web-api/webapi14.png)  

  19. [Web API の構成] https://localhost:44300 で、を**識別子**として追加します。  
  
      ![アプリの Reg](media/adfs-msal-web-api-web-api/webapi15.png)

  20. Access Control ポリシーの適用 画面で、**すべてのユーザーを許可**する を選択し、**次へ** をクリックします。 
  
      ![アプリの Reg](media/adfs-msal-web-api-web-api/webapi16.png)

  21. アプリケーションのアクセス許可の構成 画面で、**次へ** をクリックします。 
  
      ![アプリの Reg](media/adfs-msal-web-api-web-api/webapi17.png)

  22. 概要 画面で、**次へ** をクリックします。

  23. 完了 画面で、**閉じる** をクリックします。  

  24. WebApiToWebApi で [OK] をクリックします。 [Web API 2 のプロパティ] 画面  

  25. WebApiToWebApi のプロパティ 画面で、 **WebApiToWebApi – WEB API** を選択し、**編集...** をクリックします。  
  
      ![アプリの Reg](media/adfs-msal-web-api-web-api/webapi18.png)

  26. WebApiToWebApi – Web API のプロパティ 画面で、**発行変換規則** タブを選択し、**規則の追加...** をクリックします。 
  
      ![アプリの Reg](media/adfs-msal-web-api-web-api/webapi19.png)

  27. 変換要求規則の追加ウィザードで、ドロップダウンから **[カスタム規則を使用して要求を送信]** する を選択し、 **[次へ]** をクリックします。 
  
      ![アプリの Reg](media/adfs-msal-web-api-web-api/webapi20.png)

  28. **要求規則名に「** **pass allclaim** 」と入力し、フィールドと**x: [] = > issue (Claim = x);** カスタムルール: field の要求規則を入力して、[完了] をクリックします。  
   
      ![アプリの Reg](media/adfs-msal-web-api-web-api/webapi21.png)

  29. WebApiToWebApi で [OK] をクリックします。 Web API のプロパティ画面

  30. WebApiToWebApi のプロパティ画面で、[WebApiToWebApi – Web API 2 を選択する] を選択し、[編集...] をクリックします。</br> 
  ![アプリの Reg](media/adfs-msal-web-api-web-api/webapi22.png)

  31. [WebApiToWebApi – Web API 2 のプロパティ] 画面で、[発行変換規則] タブを選択し、[規則の追加...] をクリックします。 

  32. 変換要求規則の追加ウィザードで、dopdown からカスタムルールを使用して要求を![送信する を選択し、次のアプリの Reg をクリックします。](media/adfs-msal-web-api-web-api/webapi23.png)

  33. 要求規則名に「Pass Allclaim」と入力し、フィールドと**x: [] = > issue (claim = x);** **カスタムルール:** field の要求規則を入力して、 **[完了]** をクリックします。  
   
      ![アプリの Reg](media/adfs-msal-web-api-web-api/webapi24.png)

  34.  WebApiToWebApi – Web API 2 のプロパティ画面で [OK] をクリックし、WebApiToWebApi のプロパティ画面で [OK] をクリックします。  
 

## <a name="code-configuration"></a>コードの構成 

このセクションでは、Web API が別の Web API を呼び出すように構成する方法について説明します。 

  1. ここからサンプルをダウンロードして[ください](https://github.com/microsoft/adfs-sample-msal-dotnet-webapi-to-webapi-onbehalfof)  
  
  2. Visual Studio を使用してサンプルを開く 
  
  3. App.config ファイルを開きます。 次のように変更します。 
       - ida: Authority- https://[your AD FS hostname]/adfs/を入力します
       - ida: ClientId-上の AD FS セクションの [アプリの登録] の #3 から値を入力します。 
       - ida: RedirectUri-上の AD FS セクションの [アプリの登録] の #3 から値を入力します。 
       - todo: TodoListResourceId-上の AD FS セクションのアプリ登録で #4 から識別子の値を入力してください 
       - ida: todo: TodoListBaseAddress-上記の AD FS セクションの「アプリの登録」の #4 から識別子の値を入力します。 
      
            ![アプリの Reg](media/adfs-msal-web-api-web-api/webapi25.png)

  4. ToDoListService の下にある web.config ファイルを開きます。 次のように変更します。 
       - ida: Audience-上の AD FS セクションの [アプリの登録] の #12 からクライアント識別子の値を入力します
       - ida: ClientId-上の AD FS セクションの [アプリの登録] で #12 からクライアント識別子の値を入力します。 
       - idaClientSecret-前の AD FS セクションの「アプリの登録」で #13 からコピーした共有シークレットを入力します。
       - ida: RedirectUri-前の AD FS セクションの「アプリの登録」の #12 から、RedirectUri の値を入力します。 
       - idaAdfsMetadataEndpoint-「 https://[your AD FS hostname]/federationmetadata/2007-06/federationmetadata.xml」と入力します。 
       - ida: OBOWebAPIBase-上の AD FS セクションの [アプリの登録] の #19 から識別子の値を入力します。 
       - ida: Authority: 「 https://[your AD FS hostname]/adfs」と入力します。 
  
          ![アプリの Reg](media/adfs-msal-web-api-web-api/webapi26.png) 

 5. WebAPIOBO の下にある web.config ファイルを開きます。 次のように変更します。 
       - idaAdfsMetadataEndpoint-「 https://[your AD FS hostname]/federationmetadata/2007-06/federationmetadata.xml」と入力します。 
       - ida: Audience-上の AD FS セクションの [アプリの登録] の #12 からクライアント識別子の値を入力します 
 
          ![アプリの Reg](media/adfs-msal-web-api-web-api/webapi27.png)
 
## <a name="test-the-sample"></a>サンプルをテストする 

このセクションでは、上記で構成したサンプルをテストする方法について説明します。 

コードの変更が行われたら、ソリューションをリビルドします。 
 
  1. Visual Studio で、ソリューションを右クリックし、 **[スタートアッププロジェクトの設定...]** を選択します。 
      
      ![アプリの Reg](media/adfs-msal-web-api-web-api/webapi28.png)

  2. プロパティページ で、TodoListSPA を除く各プロジェクトに対して **アクション** が **開始** に設定されていることを確認します。  
  
      ![アプリの Reg](media/adfs-msal-web-api-web-api/webapi29.png)
  
  3. Visual Studio の上部にある緑色の矢印をクリックします。  
  
      ![アプリの Reg](media/adfs-msal-web-api-web-api/webapi30.png)

  4. ネイティブアプリのメイン画面で、 **[サインイン]** をクリックします。 
  
      ![アプリの Reg](media/adfs-msal-web-api-web-api/webapi31.png)

     ネイティブアプリの画面が表示されない場合は、プロジェクトリポジトリがシステムに保存されているフォルダーから * msalcache. bin ファイルを検索して削除します。 
  
  5. AD FS サインインページにリダイレクトされます。 さあ、サインインします。 
  
      ![アプリの Reg](media/adfs-msal-web-api-web-api/webapi32.png)

  6. サインインしたら、 **Create a To Do 項目**に「web Api To Web api Call」と入力します。 **[項目の追加]** をクリックします。  これにより、web api (To Do List Service) が呼び出され、Web API 2 (WebAPIOBO) が呼び出され、キャッシュに項目が追加されます。  
 
      ![アプリの Reg](media/adfs-msal-web-api-web-api/webapi33.png)
 
 ## <a name="next-steps"></a>次の手順
[AD FS OpenID 接続/OAuth フローとアプリケーション シナリオ](../../overview/ad-fs-openid-connect-oauth-flows-scenarios.md)
 
 
