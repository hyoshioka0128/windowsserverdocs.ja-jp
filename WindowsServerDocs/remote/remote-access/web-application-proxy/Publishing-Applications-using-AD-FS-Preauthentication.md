---
ms.assetid: 5f733510-c96e-4d3a-85d2-4407de95926e
title: AD FS 事前認証を使用してアプリケーションを公開する
description: ''
author: kgremban
manager: femila
ms.date: 07/13/2016
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: web-app-proxy
ms.openlocfilehash: c7dab1dbf97d2dcbda1fe0375e61300f2a1cc373
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862243"
---
# <a name="publishing-applications-using-ad-fs-preauthentication"></a>AD FS 事前認証を使用してアプリケーションを公開する

>適用先:Windows Server 2016

**このコンテンツは、Web アプリケーション プロキシのオンプレミス バージョンに関連します。クラウドでオンプレミス アプリケーションに安全にアクセスを有効にするのを参照してください。、 [Azure AD アプリケーション プロキシのコンテンツ](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-get-started/)します。**  
  
このトピックでは、Active Directory フェデレーション サービス (AD FS) 事前認証を使用して Web アプリケーション プロキシ経由でアプリケーションを発行する方法について説明します。  
  
AD FS 事前認証を使用して発行するアプリケーションのすべての種類をフェデレーション サービスの信頼証明書利用者の AD FS を追加する必要があります。  
  
一般的な AD FS 事前認証フローは次のとおりです。  
  
> [!NOTE]  
> この認証フローでは、Microsoft Store アプリを使用するクライアントに適用されません。  
  
1.  クライアント デバイスが、; 特定のリソース URL で公開された web アプリケーションにアクセスしようとしています。たとえば https://app1.contoso.com/します。  
  
    リソース URL は、Web アプリケーション プロキシが着信 HTTPS 要求をリッスンするパブリック アドレスです。  
  
    HTTP HTTPS へのリダイレクトからが有効になっている場合、Web アプリケーション プロキシは受信 HTTP 要求のリッスンもします。  
  
2.  Web アプリケーション プロキシは、リソース URL や appRealm (証明書利用者の識別子) を含む URL でエンコードされたパラメーターは、使用して AD FS サーバーに HTTPS 要求をリダイレクトします。  
  
    AD FS サーバーで必要な認証方法を使用して、ユーザーの認証します。たとえば、ユーザー名とパスワード、ワンタイム パスワードの 2 要素認証。  
  
3.  ユーザーが認証された後、AD FS サーバー、セキュリティ トークン、トークンを発行 ' edge'、次の情報と Web アプリケーション プロキシ サーバーに HTTPS が要求のリダイレクトを含みます。  
  
    -   ユーザーがアクセスしようとしているリソースの識別子。  
  
    -   ユーザー プリンシパル名 (UPN) として、ユーザーの id。  
  
    -   アクセス許可の承認有効期限。つまり、ユーザーは、期間限定でアクセスを許可されますが、期限を過ぎると再び認証する必要があります。  
  
    -   エッジ トークンの情報の署名。  
  
4.  Web アプリケーション プロキシはエッジ トークンを使って AD FS サーバーからリダイレクトされた HTTPS 要求を受け取る検証して、次のように、トークンを使用します。  
  
    -   Web アプリケーション プロキシの構成で構成されているフェデレーション サービスからエッジ トークンの署名を検証します。  
  
    -   トークンが適切なアプリケーション用に発行されていることを検証します。  
  
    -   トークンが期限切れになっていないこと検証します。  
  
    -   必要に応じてユーザー ID を使用します。たとえば、バックエンド サーバーが統合 Windows 認証を使用するように構成されているときに、Kerberos チケットを取得するような場合です。  
  
5.  エッジ トークンが有効な場合は、Web アプリケーション プロキシは HTTP または HTTPS を使用して公開された web アプリケーションに HTTPS 要求を転送します。  
  
6.  これで、クライアントは、公開された Web アプリケーションにアクセスできるようになります。ただし、公開されたアプリケーションで、ユーザーに追加の認証を要求するように構成されている場合があります。 たとえば、公開された Web アプリケーションが SharePoint サイトであり、追加の認証を要求しない場合、ユーザーのブラウザーに SharePoint サイトが表示されます。  
  
7.  Web アプリケーション プロキシは、クライアント デバイスに cookie を保存します。 Web アプリケーション プロキシでは、クッキーを使用して、このセッションが既に事前認証と、さらに事前認証が必要ないことを識別します。  
  
> [!IMPORTANT]  
> 外部 URL とバックエンド サーバーの URL を構成するときに、IP アドレスではなく、完全修飾ドメイン名 (FQDN) を含めます。  
  
> [!NOTE]  
> このトピックでは、サンプル Windows PowerShell コマンドレットを紹介します。ここで説明する手順の一部はこのコマンドレットで自動化できます。 詳しくは、 [コマンドレットの使用に関するページ](https://go.microsoft.com/fwlink/p/?linkid=230693)をご覧ください。  
  
## <a name="BKMK_1.1"></a>Web ブラウザー クライアント用の信頼性情報ベースのアプリケーションを発行します。  
認証の要求を使用するアプリケーションを公開するには、フェデレーション サービスにアプリケーションの証明書利用者信頼を追加する必要があります。  
  
要求ベースのアプリケーションを公開し、ブラウザーからアプリケーションにアクセスする場合、一般的な認証フローは次のとおりです。  
  
1.  クライアントは、web ブラウザーを使用してクレーム ベースのアプリケーションにアクセスしようとしました。たとえば、 https://appserver.contoso.com/claimapp/します。  
  
2.  Web ブラウザーでは、AD FS サーバーに要求をリダイレクトする Web アプリケーション プロキシ サーバーに HTTPS 要求を送信します。  
  
3.  AD FS サーバーでは、ユーザーとデバイスを認証し、要求を Web アプリケーション プロキシにリダイレクトします。 この要求にはエッジ トークンが含まれています。 AD FS サーバーでは、ユーザーが AD FS サーバーに対する認証を実行して既にために、シングル サインオン (SSO) cookie を要求に追加します。  
  
4.  Web アプリケーション プロキシはトークンを検証し、独自の cookie を追加します、バックエンド サーバーに要求を転送します。  
  
5.  バックエンド サーバーは、アプリケーションのセキュリティ トークンを取得する AD FS サーバーに要求をリダイレクトします。  
  
6.  要求は、AD FS サーバーによってバックエンド サーバーにリダイレクトされます。 この要求には、アプリケーション トークンと SSO の Cookie が含まれています。 ユーザーはアプリケーションへのアクセスを許可され、ユーザー名またはパスワードを入力する必要はありません。  
  
この手順では、Web ブラウザー クライアントからアクセスする、SharePoint サイトなどの要求ベースのアプリケーションを公開する方法について説明します。 開始する前に、次の作業が完了していることを確認します。  
  
-   AD FS 管理コンソールで証明書利用者の信頼をアプリケーションを作成します。  
  
-   Web アプリケーション プロキシ サーバーの証明書が発行するアプリケーションに適したであることを確認します。  
  

  
#### <a name="to-publish-a-claims-based-application"></a>要求ベースのアプリケーションを公開するには  
  
1.  Web アプリケーション プロキシ サーバーで、リモート アクセス管理コンソールで、**ナビゲーション**ウィンドウで、をクリックして**Web アプリケーション プロキシ**、し、**タスク**ウィンドウで、 をクリックして**発行**します。  
  
2.  **新しいアプリケーションの公開ウィザード**の **[ようこそ]** ページで **[次へ]** をクリックします。  
  
3.  **事前認証**] ページで [ **Active Directory フェデレーション サービス (AD FS)**、順にクリックします**次**します。  
  
4.  **[サポート対象のクライアント]** ページで、 **[Web および MSOFBA]** を選択し、 **[次へ]** をクリックします。  
  
5.  **[証明書利用者]** ページの証明書利用者の一覧から、公開するアプリケーションの証明書利用者を選択し、 **[次へ]** をクリックします。  
  
6.  **[公開設定]** ページで、次の操作を行い、**[次へ]** をクリックします。  
  
    -   **[名前]** ボックスに、アプリケーションのフレンドリ名を入力します。  
  
        この名前は、リモート アクセス管理コンソールの公開するアプリケーションの一覧でのみ使用されます。  
  
    -   **[外部 URL]** ボックスに、このアプリケーションの外部 URL (https://sp.contoso.com/app1/ など) を入力します。  
  
    -   **[外部証明書]** の一覧で、外部 URL に対応するサブジェクトを持つ証明書を選択します。  
  
    -   **[バックエンド サーバー URL]** ボックスに、バックエンド サーバーの URL を入力します。 外部 URL を入力して、バックエンド サーバーの URL が異なる場合にのみ変更する必要がありますと自動的にこの値が入力することに注意してください。たとえば、 https://sp/app1/します。  
  
        > [!NOTE]  
        > Web アプリケーション プロキシは、Url でホスト名を変換できますが、パス名を変換することはできません。 そのため、異なるホスト名を入力できますが、同じパス名を入力する必要があります。 たとえば、外部 URL を入力できます https://apps.contoso.com/app1/とバックエンド サーバーの URL を https://app-server/app1/します。 ただし、外部 URL を入力することはできません https://apps.contoso.com/app1/とバックエンド サーバーの URL を https://apps.contoso.com/internal-app1/します。  
  
7.  **[確認]** ページで設定を確認し、**[公開]** をクリックします。 PowerShell コマンドをコピーして、追加で公開するアプリケーションをセットアップすることができます。  
  
8.  **[結果]** ページで、アプリケーションが正常に公開されたことを確認し、 **[閉じる]** をクリックします。  
  
![](../../media/Publishing-Applications-using-AD-FS-Preauthentication/PowerShellLogoSmall.gif)Windows PowerShell と同じコマンド。  
  
以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。  
  
```  
Add-WebApplicationProxyApplication  
    -BackendServerURL 'https://sp.contoso.com/app1/'  
    -ExternalCertificateThumbprint '1a2b3c4d5e6f1a2b3c4d5e6f1a2b3c4d5e6f1a2b'  
    -ExternalURL 'https://sp.contoso.com/app1/'  
    -Name 'SP'  
    -ExternalPreAuthentication ADFS  
    -ADFSRelyingPartyName 'SP_Relying_Party'  
```  
  
## <a name="BKMK_1.2"></a>Web ブラウザー クライアント用の統合 Windows 認証ベースのアプリケーションを発行します。  
統合 Windows 認証を使用するアプリケーションを公開する web アプリケーション プロキシを使用できます。つまり、Web アプリケーション プロキシは、必要に応じて事前認証を実行し、統合 Windows 認証を使用する公開されたアプリケーションに SSO を実行できます。 統合 Windows 認証を使用するアプリケーションを公開するには、フェデレーション サービスに要求対応ではない証明書利用者信頼を追加する必要があります。  
  
制約付き委任では、Web アプリケーション プロキシ サーバーをドメインに参加する必要がありますのシングル サインオン (SSO) を実行して、Kerberos を使用して資格情報の委任を実行する、Web アプリケーション プロキシを許可します。 参照してください[Active Directory を計画](https://technet.microsoft.com/library/dn383648.aspx#BKMK_AD)します。  
  
統合 Windows 認証を使用するアプリケーションにアクセスするユーザーを許可するには、Web アプリケーション プロキシ サーバーは公開されたアプリケーションにユーザーの委任を提供できる必要があります。 この作業は、どのアプリケーションについてもドメイン コントローラーで実行できます。 行うことができますもこのバックエンド サーバーで Windows Server 2012 R2 または Windows Server 2012 で実行されている場合。 詳細については、「 [Kerberos 認証の新機能](https://technet.microsoft.com/library/hh831747.aspx)」を参照してください。  
  
統合 Windows 認証を使用してアプリケーションを公開する Web アプリケーション プロキシを構成する方法のチュートリアルは、次を参照してください。[統合 Windows 認証を使用するようにサイト](https://technet.microsoft.com/library/dn280943.aspx#BKMK_3)します。  
  
バックエンド サーバーに対して統合 Windows 認証を使用する場合は、Web アプリケーション プロキシと、公開されたアプリケーション間の認証は要求ベースではありません、代わりに、アプリケーションをエンドユーザーの認証に Kerberos の制約付き委任を使用します。 一般的なフローは次のとおりです。  
  
1.  クライアントは、web ブラウザーを使用して、非要求ベースのアプリケーションにアクセスしようとしました。たとえば、 https://appserver.contoso.com/nonclaimapp/します。  
  
2.  Web ブラウザーでは、AD FS サーバーに要求をリダイレクトする Web アプリケーション プロキシ サーバーに HTTPS 要求を送信します。  
  
3.  AD FS サーバーでは、ユーザーを認証し、要求を Web アプリケーション プロキシにリダイレクトします。 この要求にはエッジ トークンが含まれています。  
  
4.  Web アプリケーション プロキシは、トークンを検証します。  
  
5.  トークンが有効な場合は、Web アプリケーション プロキシは、ユーザーの代理として、ドメイン コント ローラーから Kerberos チケットを取得します。  
  
6.  Web アプリケーション プロキシは、Simple and Protected GSS-API Negotiation Mechanism (SPNEGO) トークンの一部として、Kerberos チケットを要求に追加し、バックエンド サーバーへの要求を転送します。 この要求には Kerberos チケットが含まれています。そのため、ユーザーはそれ以上の認証を使わずに、アプリケーションへのアクセスが許可されます。  
  
この手順では、Web ブラウザー クライアントからアクセスする、Outlook Web アプリなどの統合 Windows 認証を使用するアプリケーションを公開する方法について説明します。 開始する前に、次の作業が完了していることを確認します。  
  
-   AD FS 管理コンソールで要求に対応していない証明書利用者の信頼をアプリケーションを作成します。  
  
-   Set-ADUser コマンドレットを -PrincipalsAllowedToDelegateToAccount パラメーターを指定して使用することによって、ドメイン コントローラーで Kerberos の制約付き委任をサポートするようにバックエンド サーバーを構成する。 場合は、バックエンド サーバーは、Windows Server 2012 R2 または Windows Server 2012 で実行されて、実行することできますもこの PowerShell コマンド、バックエンド サーバーでに注意してください。  
  
-   バックエンド サーバーのサービス プリンシパル名への委任、Web アプリケーション プロキシ サーバーが構成されていることを確認しました。  
  
-   Web アプリケーション プロキシ サーバーの証明書が発行するアプリケーションに適したであることを確認します。  
  
 
  
#### <a name="to-publish-a-non-claims-based-application"></a>要求ベースではないアプリケーションを公開するには  
  
1.  Web アプリケーション プロキシ サーバーで、リモート アクセス管理コンソールで、**ナビゲーション**ウィンドウで、をクリックして**Web アプリケーション プロキシ**、し、**タスク**ウィンドウで、 をクリックして**発行**します。  
  
2.  **新しいアプリケーションの公開ウィザード**の **[ようこそ]** ページで **[次へ]** をクリックします。  
  
3.  **事前認証**] ページで [ **Active Directory フェデレーション サービス (AD FS)**、順にクリックします**次**します。  
  
4.  **[サポート対象のクライアント]** ページで、 **[Web および MSOFBA]** を選択し、 **[次へ]** をクリックします。  
  
5.  **[証明書利用者]** ページの証明書利用者の一覧から、公開するアプリケーションの証明書利用者を選択し、 **[次へ]** をクリックします。  
  
6.  **[公開設定]** ページで、次の操作を行い、**[次へ]** をクリックします。  
  
    -   **[名前]** ボックスに、アプリケーションのフレンドリ名を入力します。  
  
        この名前は、リモート アクセス管理コンソールの公開するアプリケーションの一覧でのみ使用されます。  
  
    -   **[外部 URL]** ボックスに、このアプリケーションの外部 URL (https://owa.contoso.com/ など) を入力します。  
  
    -   **[外部証明書]** の一覧で、外部 URL に対応するサブジェクトを持つ証明書を選択します。  
  
    -   **[バックエンド サーバー URL]** ボックスに、バックエンド サーバーの URL を入力します。 外部 URL を入力して、バックエンド サーバーの URL が異なる場合にのみ変更する必要がありますと自動的にこの値が入力することに注意してください。たとえば、 https://owa/します。  
  
        > [!NOTE]  
        > Web アプリケーション プロキシは、Url でホスト名を変換できますが、パス名を変換することはできません。 そのため、異なるホスト名を入力できますが、同じパス名を入力する必要があります。 たとえば、外部 URL を入力できます https://apps.contoso.com/app1/とバックエンド サーバーの URL を https://app-server/app1/します。 ただし、外部 URL を入力することはできません https://apps.contoso.com/app1/とバックエンド サーバーの URL を https://apps.contoso.com/internal-app1/します。  
  
    -   **[バックエンド サーバー SPN]** ボックスに、バックエンド サーバーのサービス プリンシパル名 (HTTP/owa.contoso.com など) を入力します。  
  
7.  **[確認]** ページで設定を確認し、**[公開]** をクリックします。 PowerShell コマンドをコピーして、追加で公開するアプリケーションをセットアップすることができます。  
  
8.  **[結果]** ページで、アプリケーションが正常に公開されたことを確認し、 **[閉じる]** をクリックします。  
  
![](../../media/Publishing-Applications-using-AD-FS-Preauthentication/PowerShellLogoSmall.gif)Windows PowerShell と同じコマンド。  
  
以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。  
  
```  
Add-WebApplicationProxyApplication  
    -BackendServerAuthenticationSpn 'HTTP/owa.contoso.com'  
    -BackendServerURL 'https://owa.contoso.com/'  
    -ExternalCertificateThumbprint '1a2b3c4d5e6f1a2b3c4d5e6f1a2b3c4d5e6f1a2b'  
    -ExternalURL 'https://owa.contoso.com/'  
    -Name 'OWA'  
    -ExternalPreAuthentication ADFS  
    -ADFSRelyingPartyName 'Non-Claims_Relying_Party'  
```  
  
## <a name="BKMK_1.3"></a>MS OFBA を使用するアプリケーションを発行します。  
Web アプリケーション プロキシ Microsoft Word などの Microsoft Office クライアントからのアクセスをそのドキュメントにアクセスしてサポート データ バックエンド サーバーでします。 これらのアプリケーションと標準的なブラウザーの唯一の違いは、通常の HTTP リダイレクトではなくで指定されている特殊な MS OFBA ヘッダーで、STS へのリダイレクトが実行された: [ https://msdn.microsoft.com/library/dd773463(v=office.12).aspx](https://msdn.microsoft.com/library/dd773463(v=office.12).aspx)します。 バックエンド アプリケーションは、要求ベースまたは IWA ベースです。   
MS OFBA を使用するクライアント アプリケーションを発行するには、証明書利用者の信頼をフェデレーション サービスにアプリケーションを追加する必要があります。 アプリケーションに応じて、要求ベースの認証または統合 Windows 認証を使用できます。 そのため、アプリケーションに応じて、関連する証明書利用者信頼を追加する必要があります。  
  
制約付き委任では、Web アプリケーション プロキシ サーバーをドメインに参加する必要がありますのシングル サインオン (SSO) を実行して、Kerberos を使用して資格情報の委任を実行する、Web アプリケーション プロキシを許可します。 参照してください[Active Directory を計画](https://technet.microsoft.com/library/dn383648.aspx#BKMK_AD)します。  
  
アプリケーションが要求ベースの認証を使用している場合、追加の計画手順はありません。 アプリケーションが統合 Windows 認証を使用する場合は、次を参照してください。 [Web ブラウザー クライアント用の統合 Windows 認証ベースのアプリケーションの発行](../web-application-proxy/../web-application-proxy/Publishing-Applications-using-AD-FS-Preauthentication.md#BKMK_1.2)します。  
  
クレーム ベース認証を使用して MS OFBA プロトコルを使用するクライアントの認証フローを以下に示します。 このシナリオの認証では、URL または本文でアプリケーション トークンを使用できます。  
  
1.  ユーザーが Office プログラムで作業しているときに、 **[最近使ったファイル]** の一覧から、SharePoint サイトのファイルを開きます。  
  
2.  Office プログラムは、ユーザーに資格情報の入力を要求するブラウザー コントロールを含むウィンドウを表示します。  
  
    > [!NOTE]  
    > 場合によっては、クライアントが既に認証されているため、このウィンドウが表示されないことがあります。  
  
3.  Web アプリケーション プロキシは、認証を実行する AD FS サーバーに要求をリダイレクトします。  
  
4.  AD FS サーバーは、Web アプリケーション プロキシを要求をリダイレクトします。 この要求にはエッジ トークンが含まれています。  
  
5.  AD FS サーバーでは、ユーザーが AD FS サーバーに対する認証を実行して既にために、シングル サインオン (SSO) cookie を要求に追加します。  
  
6.  Web アプリケーション プロキシはトークンを検証し、バックエンド サーバーに要求を転送します。  
  
7.  バックエンド サーバーは、アプリケーションのセキュリティ トークンを取得する AD FS サーバーに要求をリダイレクトします。  
  
8.  要求はバックエンド サーバーにリダイレクトされます。 この要求には、アプリケーション トークンと SSO の Cookie が含まれています。 ユーザーは SharePoint サイトへのアクセスを許可され、ファイルを表示するためにユーザー名またはパスワードを入力する必要はありません。  
  
MS OFBA を使用するアプリケーションを発行する手順は、クレーム ベースのアプリケーションまたは非要求ベース アプリケーション用の手順と同じです。 クレーム ベースのアプリケーションでは、次を参照してください[Web ブラウザー クライアント用の信頼性情報ベースのアプリケーションの発行](../web-application-proxy/../web-application-proxy/Publishing-Applications-using-AD-FS-Preauthentication.md#BKMK_1.1)、非要求ベースのアプリケーションでは、次を参照してください。 [Web に対して統合 Windows 認証ベース アプリケーションを公開。ブラウザー クライアント](../web-application-proxy/../web-application-proxy/Publishing-Applications-using-AD-FS-Preauthentication.md#BKMK_1.2)します。 Web アプリケーション プロキシは自動的にクライアントを検出し、必要に応じてユーザーを認証します。  
  
## <a name="publish-an-application-that-uses-http-basic"></a>HTTP Basic を使用するアプリケーションを発行します。  

HTTP Basic は、多くのプロトコルと、Exchange メールボックスのスマート フォンを含む、リッチ クライアントの接続に使用する承認プロトコルです。 HTTP 基本の詳細については、次を参照してください。 [RFC 2617](https://www.ietf.org/rfc/rfc2617.txt)します。 Web アプリケーション プロキシは、従来のリダイレクト; を使用して AD FS と対話します。ほとんどの機能豊富なクライアントは、cookie や状態管理でサポートされていません。 この方法で Web アプリケーション プロキシ アプリができるように、HTTP 以外の要求を受信するアプリケーションをフェデレーション サービスの証明書利用者信頼。 参照してください[Active Directory を計画](https://technet.microsoft.com/library/dn383648.aspx#BKMK_AD)します。  
  
HTTP Basic を使用するクライアントの認証フローとこの図では以下のとおりです。  
  
![](../../media/Publishing-Applications-using-AD-FS-Preauthentication/WebApplicationProxy_httpBasicflow.png)  
  
1.  ユーザーは、公開された web アプリケーション、電話クライアントにアクセスしようとします。  
  
2.  アプリは、Web アプリケーション プロキシによって発行された URL に HTTPS 要求を送信します。  
  
3.  要求に資格情報が含まれていない場合、Web アプリケーション プロキシは、認証の AD FS サーバーの URL を含むアプリに HTTP 401 応答を返します。  
  
4.  ユーザーがアプリへの HTTPS 要求もう一度承認 Basic とユーザー名と Base 64 に設定を持つ暗号化 www 内のユーザーのパスワードを送信-要求ヘッダーを認証します。  
  
5.  デバイスは、AD FS にリダイレクトできません、ため、Web アプリケーション プロキシ認証要求を送信資格情報で AD FS にユーザー名とパスワードを含むがあります。 デバイスに代わって、トークンが取得されます。  
  
6.  AD FS に送信された要求の数を最小限に抑えるためには、Web アプリケーション プロキシはのキャッシュされたトークンを使用して、トークンが有効な限り、後続のクライアント要求を検証します。 Web アプリケーション プロキシは、キャッシュを定期的にクリーンアップします。 パフォーマンス カウンターを使用して、キャッシュのサイズを表示することができます。  
  
7.  トークンが有効な場合は、Web アプリケーション プロキシは、バックエンド サーバーに要求を転送し、公開された web アプリケーションへのアクセスをユーザーに許可します。  
  
次の手順では、HTTP の基本的なアプリケーションを発行する方法について説明します。  
  
#### <a name="to-publish-an-http-basic-application"></a>HTTP 基本アプリケーションを公開するには  
  
1.  Web アプリケーション プロキシ サーバーで、リモート アクセス管理コンソールで、**ナビゲーション**ウィンドウで、をクリックして**Web アプリケーション プロキシ**、し、**タスク**ウィンドウで、 をクリックして**発行**します。  
  
2.  **新しいアプリケーションの公開ウィザード**の **[ようこそ]** ページで **[次へ]** をクリックします。  
  
3.  **事前認証**] ページで [ **Active Directory フェデレーション サービス (AD FS)**、順にクリックします**次**します。  
  
4.  **サポート対象のクライアント**] ページで、[ **HTTP Basic**順にクリックします**次**します。  
  
    社内参加しているデバイスからのみ、Exchange へのアクセスを有効にする場合は、選択、**参加済みデバイスをワークプ レースにのみアクセスを有効にする**ボックス。 詳細については、次を参照してください。 [SSO およびシームレスな第 2 要素認証用アプリケーション間の任意のデバイスから社内への参加](https://technet.microsoft.com/library/dn280945.aspx)します。  
  
5.  **[証明書利用者]** ページの証明書利用者の一覧から、公開するアプリケーションの証明書利用者を選択し、 **[次へ]** をクリックします。 この一覧を含むのみに注意してくださいでの信頼性情報証明書利用者です。  
  
6.  **[公開設定]** ページで、次の操作を行い、**[次へ]** をクリックします。  
  
    -   **[名前]** ボックスに、アプリケーションのフレンドリ名を入力します。  
  
        この名前は、リモート アクセス管理コンソールの公開するアプリケーションの一覧でのみ使用されます。  
  
    -   **外部 URL**ボックスに、このアプリケーションの外部 URL を入力しますたとえば、mail.contoso.com。  
  
    -   **[外部証明書]** の一覧で、外部 URL に対応するサブジェクトを持つ証明書を選択します。  
  
    -   **[バックエンド サーバー URL]** ボックスに、バックエンド サーバーの URL を入力します。 外部 URL を入力して、バックエンド サーバーの URL が異なる場合にのみ変更する必要がありますと自動的にこの値が入力することに注意してください。たとえば、mail.contoso.com は。  
  
7.  **[確認]** ページで設定を確認し、**[公開]** をクリックします。 PowerShell コマンドをコピーして、追加で公開するアプリケーションをセットアップすることができます。  
  
8.  **[結果]** ページで、アプリケーションが正常に公開されたことを確認し、 **[閉じる]** をクリックします。  
  
![](../../media/Publishing-Applications-using-AD-FS-Preauthentication/PowerShellLogoSmall.gif)Windows PowerShell と同じコマンド。  
  
以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。  
  
社内参加しているデバイスだけでなく、すべてのデバイスの事前認証としたときにこの Windows PowerShell スクリプトが有効にします。  
  
```  
Add-WebApplicationProxyApplication  
     -BackendServerUrl 'https://mail.contoso.com'   
     -ExternalCertificateThumbprint '697F4FF0B9947BB8203A96ED05A3021830638E50'   
     -ExternalUrl 'https://mail.contoso.com'   
     -Name 'Exchange'   
     -ExternalPreAuthentication ADFSforRichClients  
     -ADFSRelyingPartyName 'EAS_Relying_Party'  
```  
  
次の事前認証ワークプ レース参加済みデバイスのみです。  
  
```  
Add-WebApplicationProxyApplication  
     -BackendServerUrl 'https://mail.contoso.com'   
     -ExternalCertificateThumbprint '697F4FF0B9947BB8203A96ED05A3021830638E50'   
     -EnableHTTPRedirect:$true   
     -ExternalUrl 'https://mail.contoso.com'   
     -Name 'Exchange'   
     -ExternalPreAuthentication ADFSforRichClients  
     -ADFSRelyingPartyName 'EAS_Relying_Party'  
```  
  
## <a name="BKMK_1.4"></a>Microsoft Store アプリなど、OAuth2 を使用したアプリケーションを発行します。  
Microsoft Store アプリ用のアプリケーションを発行するには、証明書利用者の信頼をフェデレーション サービスにアプリケーションを追加する必要があります。  
  
制約付き委任では、Web アプリケーション プロキシ サーバーをドメインに参加する必要がありますのシングル サインオン (SSO) を実行して、Kerberos を使用して資格情報の委任を実行する、Web アプリケーション プロキシを許可します。 参照してください[Active Directory を計画](https://technet.microsoft.com/library/dn383648.aspx#BKMK_AD)します。  
  
> [!NOTE]  
> Web アプリケーション プロキシでは、OAuth 2.0 プロトコルを使用する Microsoft Store アプリに対してのみ発行をサポートしています。  
  
AD FS 管理コンソールでは、OAuth エンドポイントがプロキシは有効であることを確認の操作を行う必要があります。 OAuth エンドポイントがプロキシに対応しているかどうかを確認するには、AD FS 管理コンソールを開き、**[サービス]** を展開して、**[エンドポイント]** をクリックします。次に、**[エンドポイント]** の一覧で OAuth エンドポイントを見つけ、**[プロキシ有効]** 列の値が **[はい]** であることを確認します。  
  
Microsoft Store アプリを使用するクライアントの認証フローを以下に示します。  
  
> [!NOTE]  
> Web アプリケーション プロキシは、認証用の AD FS サーバーにリダイレクトします。 Microsoft Store アプリは、リダイレクトをサポートしていない Microsoft Store アプリを使用する場合、ためには、Set-webapplicationproxyconfiguration コマンドレットと OAuthAuthenticationURL パラメーターを使用して、AD FS サーバーの URL を設定する必要があります。  
>   
> Windows PowerShell を使用してのみ、Microsoft Store アプリを発行できます。  
  
1.  クライアントは、Microsoft Store アプリを使用して公開された web アプリケーションにアクセスしようとします。  
  
2.  アプリは、Web アプリケーション プロキシによって発行された URL に HTTPS 要求を送信します。  
  
3.  Web アプリケーション プロキシは、認証の AD FS サーバーの URL を含むアプリに HTTP 401 応答を返します。 このプロセスは「検出」と呼ばれます。  
  
    > [!NOTE]  
    > 場合は、アプリでは、認証の AD FS サーバーの URL を知っているし、OAuth トークンとエッジ トークンを含むコンボ トークンが既に、この認証フローで手順 2. および 3. はスキップされます。  
  
4.  アプリは、AD FS サーバーに HTTPS 要求を送信します。  
  
5.  アプリは web 認証ブローカーを使用して、ユーザーが、AD FS サーバーを認証する資格情報を入力するダイアログ ボックスを生成します。 Web 認証ブローカーの詳細については、「 [Web 認証ブローカー](https://msdn.microsoft.com/library/windows/apps/hh750287.aspx)」を参照してください。  
  
6.  認証が成功した後は、AD FS サーバーは、OAuth トークンとエッジ トークンが含まれていますし、アプリに、トークンを送信しますコンボ トークンを作成します。  
  
7.  アプリでは、Web アプリケーション プロキシによって発行された URL に、コンボ トークンを含む HTTPS 要求を送信します。  
  
8.  Web アプリケーション プロキシは、コンボ トークンを 2 つの部分に分割し、エッジ トークンを検証します。  
  
9. エッジ トークンが有効な場合、Web アプリケーション プロキシは、OAuth トークンのみを使ってバックエンド サーバーに要求を転送します。 ユーザーは、公開された Web アプリケーションへのアクセスが許可されます。  
  
この手順では、OAuth2 用のアプリケーションを公開する方法について説明します。 この種類のアプリケーションは、Windows PowerShell を使用してのみ発行できます。 開始する前に、次の作業が完了していることを確認します。  
  
-   AD FS 管理コンソールで証明書利用者の信頼をアプリケーションを作成します。  
  
-   いることを確認は、OAuth エンドポイントがプロキシが AD FS 管理コンソールで有効になっているし、URL パスをメモしておきます。  
  
-   Web アプリケーション プロキシ サーバーの証明書が発行するアプリケーションに適したであることを確認します。  
  
#### <a name="to-publish-an-oauth2-app"></a>OAuth2 アプリを発行するには  
  
1.  Web アプリケーション プロキシ サーバーで、リモート アクセス管理コンソールで、**ナビゲーション**ウィンドウで、をクリックして**Web アプリケーション プロキシ**、し、**タスク**ウィンドウで、 をクリックして**発行**します。  
  
2.  **新しいアプリケーションの公開ウィザード**の **[ようこそ]** ページで **[次へ]** をクリックします。  
  
3.  **事前認証**] ページで [ **Active Directory フェデレーション サービス (AD FS)**、順にクリックします**次**します。  
  
4.  **サポート対象のクライアント**] ページで、[ **OAuth2**順にクリックします**次**します。  
  
5.  **[証明書利用者]** ページの証明書利用者の一覧から、公開するアプリケーションの証明書利用者を選択し、 **[次へ]** をクリックします。  
  
6.  **[公開設定]** ページで、次の操作を行い、**[次へ]** をクリックします。  
  
    -   **[名前]** ボックスに、アプリケーションのフレンドリ名を入力します。  
  
        この名前は、リモート アクセス管理コンソールの公開するアプリケーションの一覧でのみ使用されます。  
  
    -   **[外部 URL]** ボックスに、このアプリケーションの外部 URL (https://server1.contoso.com/app1/ など) を入力します。  
  
    -   **[外部証明書]** の一覧で、外部 URL に対応するサブジェクトを持つ証明書を選択します。  
  
        確認するために、ユーザーは、アプリにアクセスできる HTTPS URL を入力を怠ると、場合でも、選択、 **HTTPS へのリダイレクトを有効に HTTP**ボックス。  
  
    -   **[バックエンド サーバー URL]** ボックスに、バックエンド サーバーの URL を入力します。 外部 URL を入力して、バックエンド サーバーの URL が異なる場合にのみ変更する必要がありますと自動的にこの値が入力することに注意してください。たとえば、 https://sp/app1/します。  
  
        > [!NOTE]  
        > Web アプリケーション プロキシは、Url でホスト名を変換できますが、パス名を変換することはできません。 そのため、異なるホスト名を入力できますが、同じパス名を入力する必要があります。 たとえば、外部 URL を入力できます https://apps.contoso.com/app1/とバックエンド サーバーの URL を https://app-server/app1/します。 ただし、外部 URL を入力することはできません https://apps.contoso.com/app1/とバックエンド サーバーの URL を https://apps.contoso.com/internal-app1/します。  
  
7.  **[確認]** ページで設定を確認し、**[公開]** をクリックします。 PowerShell コマンドをコピーして、追加で公開するアプリケーションをセットアップすることができます。  
  
8.  **[結果]** ページで、アプリケーションが正常に公開されたことを確認し、 **[閉じる]** をクリックします。  
  
ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。  
  
Fs.contoso.com のアドレスと、URL パスが/adfs/oauth2/フェデレーション サーバーの OAuth 認証 URL を設定します。  
  
```  
Set-WebApplicationProxyConfiguration -OAuthAuthenticationURL 'https://fs.contoso.com/adfs/oauth2/'  
```  
  
アプリケーションを公開するには  
  
```  
Add-WebApplicationProxyApplication  
    -BackendServerURL 'https://storeapp.contoso.com/'  
    -ExternalCertificateThumbprint '1a2b3c4d5e6f1a2b3c4d5e6f1a2b3c4d5e6f1a2b'  
    -ExternalURL 'https://storeapp.contoso.com/'  
    -Name 'Microsoft Store app Server'  
    -ExternalPreAuthentication ADFS  
    -ADFSRelyingPartyName 'Store_app_Relying_Party'  
    -UseOAuthAuthentication  
```  
  
## <a name="BKMK_Links"></a>参照してください。  
  
-   [Web アプリケーション プロキシのトラブルシューティング](https://technet.microsoft.com/library/dn770156.aspx)  
  
-   [Web アプリケーション プロキシ経由でアプリケーションを発行します。](https://technet.microsoft.com/library/dn383659.aspx)  
  
-   [Web アプリケーション プロキシを使用してアプリケーションを発行する計画](https://technet.microsoft.com/library/dn383650.aspx)  
  
-   [Web アプリケーション プロキシのチュートリアル ガイド](https://technet.microsoft.com/library/dn280944.aspx)  
  
-   [Windows PowerShell で web アプリケーション プロキシ コマンドレット](https://technet.microsoft.com/library/dn283404.aspx)  
  
-   [Add-WebApplicationProxyApplication](https://technet.microsoft.com/library/dn283409.aspx)  
  
-   [Set-WebApplicationProxyConfiguration](https://technet.microsoft.com/library/dn283406.aspx)  
  


