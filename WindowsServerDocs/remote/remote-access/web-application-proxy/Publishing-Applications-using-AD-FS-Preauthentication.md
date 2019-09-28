---
ms.assetid: 5f733510-c96e-4d3a-85d2-4407de95926e
title: AD FS 事前認証を使用してアプリケーションを公開する
description: ''
author: kgremban
manager: femila
ms.date: 07/13/2016
ms.topic: article
ms.prod: windows-server
ms.technology: web-app-proxy
ms.openlocfilehash: bd5c4c97e01942e7c5ab8ed1aba3fcf92030ac59
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404267"
---
# <a name="publishing-applications-using-ad-fs-preauthentication"></a>AD FS 事前認証を使用してアプリケーションを公開する

>適用先:Windows Server 2016

@no__t-このコンテンツは、オンプレミスバージョンの Web アプリケーションプロキシに関連しています。クラウド経由でオンプレミスアプリケーションへのセキュリティで保護されたアクセスを有効にするには、 [Azure AD アプリケーションプロキシのコンテンツ](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-get-started/)を参照してください。 **  
  
このトピックでは、Active Directory フェデレーションサービス (AD FS) (AD FS) 事前認証を使用して Web アプリケーションプロキシ経由でアプリケーションを公開する方法について説明します。  
  
AD FS 事前認証を使用して公開できるすべての種類のアプリケーションについて、フェデレーションサービスに AD FS 証明書利用者信頼を追加する必要があります。  
  
一般的な AD FS 事前認証フローは次のとおりです。  
  
> [!NOTE]  
> この認証フローは、Microsoft Store アプリを使用するクライアントには適用されません。  
  
1.  クライアントデバイスは、特定のリソース URL で公開された web アプリケーションにアクセスしようとします。たとえば https://app1.contoso.com/ のようになります。  
  
    リソース URL は、Web アプリケーションプロキシが受信 HTTPS 要求をリッスンするパブリックアドレスです。  
  
    HTTP から HTTPS へのリダイレクトが有効になっている場合は、Web アプリケーションプロキシも受信 HTTP 要求をリッスンします。  
  
2.  Web アプリケーションプロキシは、URL でエンコードされたパラメーター (リソース URL、appRealm (証明書利用者の識別子) など) を使用して、HTTPS 要求を AD FS サーバーにリダイレクトします。  
  
    ユーザーは、AD FS サーバーに必要な認証方法を使用して認証を行います。たとえば、ユーザー名とパスワード、ワンタイムパスワードを使用した2要素認証などです。  
  
3.  ユーザーが認証されると、AD FS サーバーは、次の情報を含むセキュリティトークン "エッジトークン" を発行し、Web アプリケーションプロキシサーバーに HTTPS 要求をリダイレクトします。  
  
    -   ユーザーがアクセスしようとしているリソースの識別子。  
  
    -   ユーザーの id をユーザープリンシパル名 (UPN) として指定します。  
  
    -   アクセス許可の承認有効期限。つまり、ユーザーは、期間限定でアクセスを許可されますが、期限を過ぎると再び認証する必要があります。  
  
    -   エッジ トークンの情報の署名。  
  
4.  Web アプリケーションプロキシは、エッジトークンを使用して AD FS サーバーからリダイレクトされた HTTPS 要求を受け取り、次のようにトークンを検証して使用します。  
  
    -   エッジトークンの署名が、Web アプリケーションプロキシ構成で構成されているフェデレーションサービスからのものであることを検証します。  
  
    -   トークンが適切なアプリケーション用に発行されていることを検証します。  
  
    -   トークンが期限切れになっていないこと検証します。  
  
    -   必要に応じてユーザー ID を使用します。たとえば、バックエンド サーバーが統合 Windows 認証を使用するように構成されているときに、Kerberos チケットを取得するような場合です。  
  
5.  エッジトークンが有効な場合、Web アプリケーションプロキシは、HTTP または HTTPS のいずれかを使用して、公開された web アプリケーションに HTTPS 要求を転送します。  
  
6.  これで、クライアントは、公開された Web アプリケーションにアクセスできるようになります。ただし、公開されたアプリケーションで、ユーザーに追加の認証を要求するように構成されている場合があります。 たとえば、公開された Web アプリケーションが SharePoint サイトであり、追加の認証を要求しない場合、ユーザーのブラウザーに SharePoint サイトが表示されます。  
  
7.  Web アプリケーションプロキシは、クライアントデバイスに cookie を保存します。 Cookie は、このセッションが既に事前認証済みであり、それ以上の事前認証が不要であることを識別するために、Web アプリケーションプロキシによって使用されます。  
  
> [!IMPORTANT]  
> 外部 URL とバックエンド サーバーの URL を構成するときに、IP アドレスではなく、完全修飾ドメイン名 (FQDN) を含めます。  
  
> [!NOTE]  
> このトピックでは、サンプル Windows PowerShell コマンドレットを紹介します。ここで説明する手順の一部はこのコマンドレットで自動化できます。 詳しくは、 [コマンドレットの使用に関するページ](https://go.microsoft.com/fwlink/p/?linkid=230693)をご覧ください。  
  
## <a name="BKMK_1.1"></a>Web ブラウザークライアント用の要求ベースのアプリケーションを公開する  
認証の要求を使用するアプリケーションを公開するには、フェデレーション サービスにアプリケーションの証明書利用者信頼を追加する必要があります。  
  
要求ベースのアプリケーションを公開し、ブラウザーからアプリケーションにアクセスする場合、一般的な認証フローは次のとおりです。  
  
1.  クライアントは、web ブラウザーを使用して要求ベースのアプリケーションにアクセスしようとします。たとえば、 https://appserver.contoso.com/claimapp/ です。  
  
2.  Web ブラウザーは、要求を AD FS サーバーにリダイレクトする HTTPS 要求を Web アプリケーションプロキシサーバーに送信します。  
  
3.  AD FS サーバーは、ユーザーとデバイスを認証し、Web アプリケーションプロキシに要求をリダイレクトします。 この要求にはエッジ トークンが含まれています。 ユーザーが AD FS サーバーに対して認証を既に実行しているため、AD FS サーバーはシングルサインオン (SSO) cookie を要求に追加します。  
  
4.  Web アプリケーションプロキシは、トークンを検証し、独自の cookie を追加し、バックエンドサーバーに要求を転送します。  
  
5.  バックエンドサーバーは、アプリケーションのセキュリティトークンを取得するために、AD FS サーバーに要求をリダイレクトします。  
  
6.  要求は、AD FS サーバーによってバックエンドサーバーにリダイレクトされます。 この要求には、アプリケーション トークンと SSO の Cookie が含まれています。 ユーザーはアプリケーションへのアクセスを許可され、ユーザー名またはパスワードを入力する必要はありません。  
  
この手順では、Web ブラウザー クライアントからアクセスする、SharePoint サイトなどの要求ベースのアプリケーションを公開する方法について説明します。 開始する前に、次の作業が完了していることを確認します。  
  
-   AD FS 管理コンソールでアプリケーションの証明書利用者信頼を作成しました。  
  
-   Web アプリケーションプロキシサーバー上の証明書が、公開するアプリケーションに適していることを確認しました。  
  

  
#### <a name="to-publish-a-claims-based-application"></a>要求ベースのアプリケーションを公開するには  
  
1.  Web アプリケーションプロキシサーバーのリモートアクセス管理コンソールで、**ナビゲーション**ウィンドウの **[web アプリケーションプロキシ]** をクリックし、 **[タスク]** ウィンドウで **[公開]** をクリックします。  
  
2.  **新しいアプリケーションの公開ウィザード**の **[ようこそ]** ページで **[次へ]** をクリックします。  
  
3.  **[事前認証]** ページで、 **[Active Directory フェデレーションサービス (AD FS) (AD FS)]** をクリックし、 **[次へ]** をクリックします。  
  
4.  **[サポート対象のクライアント]** ページで、 **[Web および MSOFBA]** を選択し、 **[次へ]** をクリックします。  
  
5.  **[証明書利用者]** ページの証明書利用者の一覧から、公開するアプリケーションの証明書利用者を選択し、 **[次へ]** をクリックします。  
  
6.  **[公開設定]** ページで、次の操作を行い、 **[次へ]** をクリックします。  
  
    -   **[名前]** ボックスに、アプリケーションのフレンドリ名を入力します。  
  
        この名前は、リモート アクセス管理コンソールの公開するアプリケーションの一覧でのみ使用されます。  
  
    -   **[外部 URL]** ボックスに、このアプリケーションの外部 URL (https://sp.contoso.com/app1/ など) を入力します。  
  
    -   **[外部証明書]** の一覧で、外部 URL に対応するサブジェクトを持つ証明書を選択します。  
  
    -   **[バックエンド サーバー URL]** ボックスに、バックエンド サーバーの URL を入力します。 外部 URL を入力すると、この値は自動的に入力されることに注意してください。バックエンドサーバーの URL が異なる場合にのみ、この値を変更する必要があります。たとえば、 https://sp/app1/ です。  
  
        > [!NOTE]  
        > Web アプリケーションプロキシは Url 内のホスト名を変換できますが、パス名を変換することはできません。 そのため、異なるホスト名を入力できますが、同じパス名を入力する必要があります。 たとえば、 https://apps.contoso.com/app1/ の外部 URL と、 https://app-server/app1/ のバックエンドサーバー URL を入力できます。 ただし、外部 URL https://apps.contoso.com/app1/ とバックエンドサーバー URL https://apps.contoso.com/internal-app1/ を入力することはできません。  
  
7.  **[確認]** ページで設定を確認し、 **[公開]** をクリックします。 PowerShell コマンドをコピーして、追加で公開するアプリケーションをセットアップすることができます。  
  
8.  **[結果]** ページで、アプリケーションが正常に公開されたことを確認し、 **[閉じる]** をクリックします。  
  
![](../../media/Publishing-Applications-using-AD-FS-Preauthentication/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>***  
  
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
  
## <a name="BKMK_1.2"></a>Web ブラウザークライアント用の統合 Windows 認証ベースのアプリケーションを公開する  
Web アプリケーションプロキシを使用して、統合 Windows 認証を使用するアプリケーションを公開できます。つまり、Web アプリケーションプロキシは、必要に応じて事前認証を実行し、統合 Windows 認証を使用する公開されたアプリケーションに対して SSO を実行できます。 統合 Windows 認証を使用するアプリケーションを公開するには、フェデレーション サービスに要求対応ではない証明書利用者信頼を追加する必要があります。  
  
Web アプリケーションプロキシがシングルサインオン (SSO) を実行し、Kerberos の制約付き委任を使用して資格情報の委任を実行できるようにするには、Web アプリケーションプロキシサーバーがドメインに参加している必要があります。 「 [Plan Active Directory](https://technet.microsoft.com/library/dn383648.aspx#BKMK_AD)」を参照してください。  
  
統合 Windows 認証を使用するアプリケーションにユーザーがアクセスできるようにするには、Web アプリケーションプロキシサーバーが、発行されたアプリケーションにユーザーの委任を提供できる必要があります。 この作業は、どのアプリケーションについてもドメイン コントローラーで実行できます。 Windows Server 2012 R2 または Windows Server 2012 で実行されている場合は、バックエンドサーバーでこの操作を行うこともできます。 詳細については、「 [Kerberos 認証の新機能](https://technet.microsoft.com/library/hh831747.aspx)」を参照してください。  
  
統合 Windows 認証を使用してアプリケーションを公開するように Web アプリケーションプロキシを構成する方法のチュートリアルについては、「[統合 windows 認証を使用する](https://technet.microsoft.com/library/dn280943.aspx#BKMK_3)ようにサイトを構成する」を参照してください。  
  
バックエンドサーバーに対して統合 Windows 認証を使用する場合、Web アプリケーションプロキシと公開されたアプリケーションの間の認証は要求ベースではなく、代わりに Kerberos の制約付き委任を使用してアプリケーションに対してエンドユーザーを認証します。 一般的なフローは次のとおりです。  
  
1.  クライアントは、web ブラウザーを使用して、要求ベースではないアプリケーションにアクセスしようとします。たとえば、 https://appserver.contoso.com/nonclaimapp/ です。  
  
2.  Web ブラウザーは、要求を AD FS サーバーにリダイレクトする HTTPS 要求を Web アプリケーションプロキシサーバーに送信します。  
  
3.  AD FS サーバーは、ユーザーを認証し、Web アプリケーションプロキシに要求をリダイレクトします。 この要求にはエッジ トークンが含まれています。  
  
4.  Web アプリケーションプロキシはトークンを検証します。  
  
5.  トークンが有効な場合、Web アプリケーションプロキシは、ユーザーの代わりにドメインコントローラーから Kerberos チケットを取得します。  
  
6.  Web アプリケーションプロキシは、Simple and Protected GSS API ネゴシエーションメカニズム (SPNEGO) トークンの一部として Kerberos チケットを要求に追加し、要求をバックエンドサーバーに転送します。 この要求には Kerberos チケットが含まれています。そのため、ユーザーはそれ以上の認証を使わずに、アプリケーションへのアクセスが許可されます。  
  
この手順では、Web ブラウザー クライアントからアクセスする、Outlook Web アプリなどの統合 Windows 認証を使用するアプリケーションを公開する方法について説明します。 開始する前に、次の作業が完了していることを確認します。  
  
-   AD FS 管理コンソールで、アプリケーションの要求対応ではない証明書利用者信頼を作成しました。  
  
-   Set-ADUser コマンドレットを -PrincipalsAllowedToDelegateToAccount パラメーターを指定して使用することによって、ドメイン コントローラーで Kerberos の制約付き委任をサポートするようにバックエンド サーバーを構成する。 バックエンドサーバーが Windows Server 2012 R2 または Windows Server 2012 で実行されている場合は、この PowerShell コマンドをバックエンドサーバーで実行することもできます。  
  
-   Web アプリケーションプロキシサーバーが、バックエンドサーバーのサービスプリンシパル名への委任用に構成されていることを確認します。  
  
-   Web アプリケーションプロキシサーバー上の証明書が、公開するアプリケーションに適していることを確認しました。  
  
 
  
#### <a name="to-publish-a-non-claims-based-application"></a>要求ベースではないアプリケーションを公開するには  
  
1.  Web アプリケーションプロキシサーバーのリモートアクセス管理コンソールで、**ナビゲーション**ウィンドウの **[web アプリケーションプロキシ]** をクリックし、 **[タスク]** ウィンドウで **[公開]** をクリックします。  
  
2.  **新しいアプリケーションの公開ウィザード**の **[ようこそ]** ページで **[次へ]** をクリックします。  
  
3.  **[事前認証]** ページで、 **[Active Directory フェデレーションサービス (AD FS) (AD FS)]** をクリックし、 **[次へ]** をクリックします。  
  
4.  **[サポート対象のクライアント]** ページで、 **[Web および MSOFBA]** を選択し、 **[次へ]** をクリックします。  
  
5.  **[証明書利用者]** ページの証明書利用者の一覧から、公開するアプリケーションの証明書利用者を選択し、 **[次へ]** をクリックします。  
  
6.  **[公開設定]** ページで、次の操作を行い、 **[次へ]** をクリックします。  
  
    -   **[名前]** ボックスに、アプリケーションのフレンドリ名を入力します。  
  
        この名前は、リモート アクセス管理コンソールの公開するアプリケーションの一覧でのみ使用されます。  
  
    -   **[外部 URL]** ボックスに、このアプリケーションの外部 URL (https://owa.contoso.com/ など) を入力します。  
  
    -   **[外部証明書]** の一覧で、外部 URL に対応するサブジェクトを持つ証明書を選択します。  
  
    -   **[バックエンド サーバー URL]** ボックスに、バックエンド サーバーの URL を入力します。 外部 URL を入力すると、この値は自動的に入力されることに注意してください。バックエンドサーバーの URL が異なる場合にのみ、この値を変更する必要があります。たとえば、 https://owa/ です。  
  
        > [!NOTE]  
        > Web アプリケーションプロキシは Url 内のホスト名を変換できますが、パス名を変換することはできません。 そのため、異なるホスト名を入力できますが、同じパス名を入力する必要があります。 たとえば、 https://apps.contoso.com/app1/ の外部 URL と、 https://app-server/app1/ のバックエンドサーバー URL を入力できます。 ただし、外部 URL https://apps.contoso.com/app1/ とバックエンドサーバー URL https://apps.contoso.com/internal-app1/ を入力することはできません。  
  
    -   **[バックエンド サーバー SPN]** ボックスに、バックエンド サーバーのサービス プリンシパル名 (HTTP/owa.contoso.com など) を入力します。  
  
7.  **[確認]** ページで設定を確認し、 **[公開]** をクリックします。 PowerShell コマンドをコピーして、追加で公開するアプリケーションをセットアップすることができます。  
  
8.  **[結果]** ページで、アプリケーションが正常に公開されたことを確認し、 **[閉じる]** をクリックします。  
  
![](../../media/Publishing-Applications-using-AD-FS-Preauthentication/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>***  
  
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
  
## <a name="BKMK_1.3"></a>MS-OFBA を使用するアプリケーションを公開する  
Web アプリケーションプロキシは、バックエンドサーバーのドキュメントやデータにアクセスする Microsoft Word などの Microsoft Office クライアントからのアクセスをサポートします。 これらのアプリケーションと標準的なブラウザーの唯一の違いは、STS へのリダイレクトは通常の HTTP リダイレクトではなく、特別な MS OFBA ヘッダーを使用して行われます[(https://msdn.microsoft.com/library/dd773463(v=office.12).aspx )](https://msdn.microsoft.com/library/dd773463(v=office.12).aspx)。 バックエンド アプリケーションは、要求ベースまたは IWA ベースです。   
MS OFBA を使用するクライアントのアプリケーションを公開するには、アプリケーションの証明書利用者信頼をフェデレーションサービスに追加する必要があります。 アプリケーションに応じて、要求ベースの認証または統合 Windows 認証を使用できます。 そのため、アプリケーションに応じて、関連する証明書利用者信頼を追加する必要があります。  
  
Web アプリケーションプロキシがシングルサインオン (SSO) を実行し、Kerberos の制約付き委任を使用して資格情報の委任を実行できるようにするには、Web アプリケーションプロキシサーバーがドメインに参加している必要があります。 「 [Plan Active Directory](https://technet.microsoft.com/library/dn383648.aspx#BKMK_AD)」を参照してください。  
  
アプリケーションが要求ベースの認証を使用している場合、追加の計画手順はありません。 アプリケーションが統合 Windows 認証を使用している場合は、「 [Web ブラウザークライアント用の統合 windows 認証ベースのアプリケーションの発行](../web-application-proxy/../web-application-proxy/Publishing-Applications-using-AD-FS-Preauthentication.md#BKMK_1.2)」を参照してください。  
  
要求ベースの認証を使用する MS OFBA プロトコルを使用するクライアントの認証フローを以下に示します。 このシナリオの認証では、URL または本文でアプリケーション トークンを使用できます。  
  
1.  ユーザーが Office プログラムで作業しているときに、 **[最近使ったファイル]** の一覧から、SharePoint サイトのファイルを開きます。  
  
2.  Office プログラムは、ユーザーに資格情報の入力を要求するブラウザー コントロールを含むウィンドウを表示します。  
  
    > [!NOTE]  
    > 場合によっては、クライアントが既に認証されているため、このウィンドウが表示されないことがあります。  
  
3.  Web アプリケーションプロキシは、認証を実行する AD FS サーバーに要求をリダイレクトします。  
  
4.  AD FS サーバーは、Web アプリケーションプロキシに要求をリダイレクトします。 この要求にはエッジ トークンが含まれています。  
  
5.  ユーザーが AD FS サーバーに対して認証を既に実行しているため、AD FS サーバーはシングルサインオン (SSO) cookie を要求に追加します。  
  
6.  Web アプリケーションプロキシは、トークンを検証し、バックエンドサーバーに要求を転送します。  
  
7.  バックエンドサーバーは、アプリケーションのセキュリティトークンを取得するために、AD FS サーバーに要求をリダイレクトします。  
  
8.  要求はバックエンド サーバーにリダイレクトされます。 この要求には、アプリケーション トークンと SSO の Cookie が含まれています。 ユーザーは SharePoint サイトへのアクセスを許可され、ファイルを表示するためにユーザー名またはパスワードを入力する必要はありません。  
  
MS OFBA を使用するアプリケーションを公開する手順は、要求ベースのアプリケーションまたは要求ベースではないアプリケーションの手順と同じです。 要求ベースのアプリケーションについては、「 [Web ブラウザークライアント用の要求ベースのアプリケーションの発行](../web-application-proxy/../web-application-proxy/Publishing-Applications-using-AD-FS-Preauthentication.md#BKMK_1.1)」を参照してください。要求ベースではないアプリケーションについては、「 [web ブラウザークライアント用の統合 Windows 認証ベースのアプリケーションの発行](../web-application-proxy/../web-application-proxy/Publishing-Applications-using-AD-FS-Preauthentication.md#BKMK_1.2)」を参照してください。 Web アプリケーションプロキシは、クライアントを自動的に検出し、必要に応じてユーザーを認証します。  
  
## <a name="publish-an-application-that-uses-http-basic"></a>HTTP Basic を使用するアプリケーションを公開する  

HTTP Basic は、スマートフォンなどのリッチクライアントを Exchange メールボックスに接続するために多くのプロトコルによって使用される認証プロトコルです。 HTTP 基本の詳細については、 [RFC 2617](https://www.ietf.org/rfc/rfc2617.txt)を参照してください。 Web アプリケーションプロキシは従来、リダイレクトを使用して AD FS と対話します。ほとんどのリッチクライアントでは、cookie や状態管理はサポートされていません。 このようにして、Web アプリケーションプロキシを使用すると、HTTP アプリは、アプリケーションに対する要求のない証明書利用者信頼をフェデレーションサービスに対して受け取ることができます。 「 [Plan Active Directory](https://technet.microsoft.com/library/dn383648.aspx#BKMK_AD)」を参照してください。  
  
HTTP Basic を使用するクライアントの認証フローについては、次の図を参照してください。  
  
![](../../media/Publishing-Applications-using-AD-FS-Preauthentication/WebApplicationProxy_httpBasicflow.png)  
  
1.  ユーザーが、発行された web アプリケーションへの電話クライアントへのアクセスを試みます。  
  
2.  アプリは、Web アプリケーションプロキシによって発行された URL に HTTPS 要求を送信します。  
  
3.  要求に資格情報が含まれていない場合、Web アプリケーションプロキシは、認証 AD FS サーバーの URL を含む HTTP 401 応答をアプリに返します。  
  
4.  ユーザーは、認証が基本とユーザー名に設定された HTTPS 要求をアプリに再度送信し、www-認証要求ヘッダーでユーザーの基本64暗号化パスワードを使用します。  
  
5.  デバイスを AD FS にリダイレクトすることはできないため、Web アプリケーションプロキシは、ユーザー名とパスワードを含む資格情報を使用して AD FS に認証要求を送信します。 トークンは、デバイスに代わって取得されます。  
  
6.  Web アプリケーションプロキシ AD FS に送信される要求の数を最小限に抑えるために、トークンが有効である限り、はキャッシュされたトークンを使用して後続のクライアント要求を検証します。 Web アプリケーションプロキシは、定期的にキャッシュを消去します。 パフォーマンスカウンターを使用して、キャッシュのサイズを表示できます。  
  
7.  トークンが有効な場合、Web アプリケーションプロキシはバックエンドサーバーに要求を転送し、ユーザーには公開された web アプリケーションへのアクセスが許可されます。  
  
次の手順では、HTTP 基本アプリケーションを公開する方法について説明します。  
  
#### <a name="to-publish-an-http-basic-application"></a>HTTP 基本アプリケーションを公開するには  
  
1.  Web アプリケーションプロキシサーバーのリモートアクセス管理コンソールで、**ナビゲーション**ウィンドウの **[web アプリケーションプロキシ]** をクリックし、 **[タスク]** ウィンドウで **[公開]** をクリックします。  
  
2.  **新しいアプリケーションの公開ウィザード**の **[ようこそ]** ページで **[次へ]** をクリックします。  
  
3.  **[事前認証]** ページで、 **[Active Directory フェデレーションサービス (AD FS) (AD FS)]** をクリックし、 **[次へ]** をクリックします。  
  
4.  **[サポートされているクライアント]** ページで、 **[HTTP 基本]** を選択し、 **[次へ]** をクリックします。  
  
    社内参加しているデバイスからのみ Exchange へのアクセスを有効にする場合は、[**社内参加済みデバイスに対してのみアクセスを有効**にする] ボックスをオンにします。 詳細については[、「任意のデバイスからの職場への参加](https://technet.microsoft.com/library/dn280945.aspx)」を参照してください。  
  
5.  **[証明書利用者]** ページの証明書利用者の一覧から、公開するアプリケーションの証明書利用者を選択し、 **[次へ]** をクリックします。 この一覧には、要求証明書利用者のみが含まれていることに注意してください。  
  
6.  **[公開設定]** ページで、次の操作を行い、 **[次へ]** をクリックします。  
  
    -   **[名前]** ボックスに、アプリケーションのフレンドリ名を入力します。  
  
        この名前は、リモート アクセス管理コンソールの公開するアプリケーションの一覧でのみ使用されます。  
  
    -   **[外部 url]** ボックスに、このアプリケーションの外部 url を入力します。たとえば、mail.contoso.com のようになります。  
  
    -   **[外部証明書]** の一覧で、外部 URL に対応するサブジェクトを持つ証明書を選択します。  
  
    -   **[バックエンド サーバー URL]** ボックスに、バックエンド サーバーの URL を入力します。 外部 URL を入力すると、この値は自動的に入力されることに注意してください。バックエンドサーバーの URL が異なる場合にのみ、この値を変更する必要があります。たとえば、mail.contoso.com のようになります。  
  
7.  **[確認]** ページで設定を確認し、 **[公開]** をクリックします。 PowerShell コマンドをコピーして、追加で公開するアプリケーションをセットアップすることができます。  
  
8.  **[結果]** ページで、アプリケーションが正常に公開されたことを確認し、 **[閉じる]** をクリックします。  
  
![](../../media/Publishing-Applications-using-AD-FS-Preauthentication/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>***  
  
以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。  
  
この Windows PowerShell スクリプトでは、ワークプレースに参加しているデバイスだけでなく、すべてのデバイスの事前認証が有効になります。  
  
```  
Add-WebApplicationProxyApplication  
     -BackendServerUrl 'https://mail.contoso.com'   
     -ExternalCertificateThumbprint '697F4FF0B9947BB8203A96ED05A3021830638E50'   
     -ExternalUrl 'https://mail.contoso.com'   
     -Name 'Exchange'   
     -ExternalPreAuthentication ADFSforRichClients  
     -ADFSRelyingPartyName 'EAS_Relying_Party'  
```  
  
次の例では、ワークプレースに参加しているデバイスのみを事前に認証します。  
  
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
  
## <a name="BKMK_1.4"></a>Microsoft Store アプリなどの OAuth2 を使用するアプリケーションを発行する  
Microsoft Store アプリ用のアプリケーションを公開するには、アプリケーションの証明書利用者信頼をフェデレーションサービスに追加する必要があります。  
  
Web アプリケーションプロキシがシングルサインオン (SSO) を実行し、Kerberos の制約付き委任を使用して資格情報の委任を実行できるようにするには、Web アプリケーションプロキシサーバーがドメインに参加している必要があります。 「 [Plan Active Directory](https://technet.microsoft.com/library/dn383648.aspx#BKMK_AD)」を参照してください。  
  
> [!NOTE]  
> Web アプリケーションプロキシは、OAuth 2.0 プロトコルを使用する Microsoft Store アプリの発行のみをサポートしています。  
  
AD FS 管理コンソールで、OAuth エンドポイントがプロキシに対応していることを確認する必要があります。 OAuth エンドポイントがプロキシに対応しているかどうかを確認するには、AD FS 管理コンソールを開き、 **[サービス]** を展開して、 **[エンドポイント]** をクリックします。次に、 **[エンドポイント]** の一覧で OAuth エンドポイントを見つけ、 **[プロキシ有効]** 列の値が **[はい]** であることを確認します。  
  
Microsoft Store アプリを使用するクライアントの認証フローを次に示します。  
  
> [!NOTE]  
> Web アプリケーションプロキシは、認証のために AD FS サーバーにリダイレクトします。 Microsoft Store アプリではリダイレクトがサポートされないため、Microsoft Store アプリを使用する場合は、Set WebApplicationProxyConfiguration コマンドレットと OAuthAuthenticationURL パラメーターを使用して AD FS サーバーの URL を設定する必要があります。  
>   
> Microsoft Store アプリは、Windows PowerShell を使用してのみ発行できます。  
  
1.  クライアントは、Microsoft Store アプリを使用して、公開された web アプリケーションにアクセスしようとします。  
  
2.  アプリは、Web アプリケーションプロキシによって発行された URL に HTTPS 要求を送信します。  
  
3.  Web アプリケーションプロキシは、認証 AD FS サーバーの URL を含む HTTP 401 応答をアプリに返します。 このプロセスは "検出" と呼ばれます。  
  
    > [!NOTE]  
    > アプリが認証 AD FS サーバーの URL を認識しており、既に OAuth トークンとエッジトークンを含むコンボトークンがある場合、手順 2. と 3. はこの認証フローではスキップされます。  
  
4.  アプリが AD FS サーバーに HTTPS 要求を送信します。  
  
5.  このアプリでは、web 認証ブローカーを使用して、ユーザーが AD FS サーバーに対して認証するための資格情報を入力するダイアログボックスを生成します。 Web 認証ブローカーの詳細については、「 [Web 認証ブローカー](https://msdn.microsoft.com/library/windows/apps/hh750287.aspx)」を参照してください。  
  
6.  認証が成功すると、AD FS サーバーは、OAuth トークンとエッジトークンを含むコンボトークンを作成し、そのトークンをアプリに送信します。  
  
7.  アプリは、コンボトークンを含む HTTPS 要求を、Web アプリケーションプロキシによって発行された URL に送信します。  
  
8.  Web アプリケーションプロキシは、コンボトークンを2つの部分に分割し、エッジトークンを検証します。  
  
9. エッジトークンが有効な場合、Web アプリケーションプロキシは、OAuth トークンのみを使用してバックエンドサーバーに要求を転送します。 ユーザーは、公開された Web アプリケーションへのアクセスが許可されます。  
  
この手順では、OAuth2 用のアプリケーションを公開する方法について説明します。 この種類のアプリケーションは、Windows PowerShell を使用してのみ発行できます。 開始する前に、次の作業が完了していることを確認します。  
  
-   AD FS 管理コンソールでアプリケーションの証明書利用者信頼を作成しました。  
  
-   AD FS 管理コンソールで OAuth エンドポイントがプロキシに対応していることを確認し、URL パスをメモしておきます。  
  
-   Web アプリケーションプロキシサーバー上の証明書が、公開するアプリケーションに適していることを確認しました。  
  
#### <a name="to-publish-an-oauth2-app"></a>OAuth2 アプリを発行するには  
  
1.  Web アプリケーションプロキシサーバーのリモートアクセス管理コンソールで、**ナビゲーション**ウィンドウの **[web アプリケーションプロキシ]** をクリックし、 **[タスク]** ウィンドウで **[公開]** をクリックします。  
  
2.  **新しいアプリケーションの公開ウィザード**の **[ようこそ]** ページで **[次へ]** をクリックします。  
  
3.  **[事前認証]** ページで、 **[Active Directory フェデレーションサービス (AD FS) (AD FS)]** をクリックし、 **[次へ]** をクリックします。  
  
4.  **[サポートされているクライアント]** ページで、 **[OAuth2]** を選択し、 **[次へ]** をクリックします。  
  
5.  **[証明書利用者]** ページの証明書利用者の一覧から、公開するアプリケーションの証明書利用者を選択し、 **[次へ]** をクリックします。  
  
6.  **[公開設定]** ページで、次の操作を行い、 **[次へ]** をクリックします。  
  
    -   **[名前]** ボックスに、アプリケーションのフレンドリ名を入力します。  
  
        この名前は、リモート アクセス管理コンソールの公開するアプリケーションの一覧でのみ使用されます。  
  
    -   **[外部 URL]** ボックスに、このアプリケーションの外部 URL (https://server1.contoso.com/app1/ など) を入力します。  
  
    -   **[外部証明書]** の一覧で、外部 URL に対応するサブジェクトを持つ証明書を選択します。  
  
        URL に HTTPS を入力しない場合でも、ユーザーがアプリにアクセスできるようにするには、[ **HTTP から https へのリダイレクトを有効**にする] ボックスをオンにします。  
  
    -   **[バックエンド サーバー URL]** ボックスに、バックエンド サーバーの URL を入力します。 外部 URL を入力すると、この値は自動的に入力されることに注意してください。バックエンドサーバーの URL が異なる場合にのみ、この値を変更する必要があります。たとえば、 https://sp/app1/ です。  
  
        > [!NOTE]  
        > Web アプリケーションプロキシは Url 内のホスト名を変換できますが、パス名を変換することはできません。 そのため、異なるホスト名を入力できますが、同じパス名を入力する必要があります。 たとえば、 https://apps.contoso.com/app1/ の外部 URL と、 https://app-server/app1/ のバックエンドサーバー URL を入力できます。 ただし、外部 URL https://apps.contoso.com/app1/ とバックエンドサーバー URL https://apps.contoso.com/internal-app1/ を入力することはできません。  
  
7.  **[確認]** ページで設定を確認し、 **[公開]** をクリックします。 PowerShell コマンドをコピーして、追加で公開するアプリケーションをセットアップすることができます。  
  
8.  **[結果]** ページで、アプリケーションが正常に公開されたことを確認し、 **[閉じる]** をクリックします。  
  
ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。  
  
フェデレーションサーバーアドレス fs.contoso.com の OAuth 認証 URL と/adfs/oauth2/の URL パスを設定するには、次のようにします。  
  
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
  
## <a name="BKMK_Links"></a>関連項目  
  
-   [Web アプリケーション プロキシのトラブルシューティング](https://technet.microsoft.com/library/dn770156.aspx)  
  
-   [Web アプリケーションプロキシ経由でアプリケーションを公開する](https://technet.microsoft.com/library/dn383659.aspx)  
  
-   [Web アプリケーションプロキシを使用してアプリケーションを公開することを計画する](https://technet.microsoft.com/library/dn383650.aspx)  
  
-   [Web アプリケーションプロキシのチュートリアルガイド](https://technet.microsoft.com/library/dn280944.aspx)  
  
-   [Windows PowerShell の Web アプリケーションプロキシコマンドレット](https://technet.microsoft.com/library/dn283404.aspx)  
  
-   [アドオン WebApplicationProxyApplication](https://technet.microsoft.com/library/dn283409.aspx)  
  
-   [設定-WebApplicationProxyConfiguration](https://technet.microsoft.com/library/dn283406.aspx)  
  


