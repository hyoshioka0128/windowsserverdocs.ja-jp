---
ms.assetid: 276a7f7d-5faa-4c00-a51c-3fa511fe52f9
title: AD FS ラボ環境を設定する
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.author: billmath
ms.openlocfilehash: d9625992d7098a1f5cd510901be07187702b3771
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87967089"
---
# <a name="set-up-an-ad-fs-lab-environment"></a>AD FS ラボ環境を設定する

このトピックでは、次のチュートリアル ガイドのチュートリアルを完了するために使用できるテスト環境の構成手順を説明します。

-   [チュートリアル: Workplace Join で iOS デバイスをワークプレースに参加させる](Walkthrough--Workplace-Join-with-an-iOS-Device.md)

-   [チュートリアル: Workplace Join で Windows デバイスをワークプレースに参加させる](Walkthrough--Workplace-Join-with-a-Windows-Device.md)

-   [チュートリアル ガイド: 条件付きアクセス制御によってリスクを管理する](Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md)

-   [チュートリアルガイド: 追加の Multi-Factor Authentication による機密アプリケーションのリスク管理](Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)

> [!NOTE]
> Web サーバーとフェデレーション サーバーを同じコンピューターにインストールすることはお勧めしません。

このテスト環境をセットアップするには、次の手順を完了します。

1.  [手順 1: ドメイン コントローラー (DC1) を構成する](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_1)

2.  [手順 2: デバイス登録サービスを使用してフェデレーションサーバー (ADFS1) を構成する](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_4)

3.  [手順 3: Web サーバー (WebServ1) とサンプルの要求ベースのアプリケーションを構成する](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_5)

4.  [手順 4: クライアント コンピューター (Client1) を構成する](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_10)

## <a name="step-1-configure-the-domain-controller-dc1"></a><a name="BKMK_1"></a>手順 1: ドメイン コントローラー (DC1) を構成する
このテスト環境では、ルート Active Directory ドメイン**contoso.com**を呼び出し、 <strong>pass@word1</strong> 管理者パスワードとしてを指定できます。

-   AD DS の役割サービスをインストールし Active Directory Domain Services (AD DS) をインストールして、Windows Server 2012 R2 でコンピューターをドメインコントローラーにします。 この操作により、ドメインコントローラーの作成の一環として AD DS スキーマがアップグレードされます。 詳細と詳細な手順については、「[ https://technet.microsoft.com/ library/hh472162.aspx http://technet.microsoft.com/library/hh472162.aspx](../../ad-ds/deploy/install-active-directory-domain-services--level-100-.md)」を参照してください。

### <a name="create-test-active-directory-accounts"></a><a name="BKMK_2"></a>テスト用 Active Directory アカウントの作成
ドメイン コントローラーが機能するようになったら、このドメインにテスト用のグループとユーザー アカウントを作成して、作成したユーザー アカウントをグループ アカウントに追加できます。 このトピックの最初に示したチュートリアル ガイドのチュートリアルを完了するには、これらのアカウントを使用します。

次のアカウントを作成します。

- ユーザー: **Robert Hatley**次の資格情報: ユーザー名: **roth th** and password:<strong>P@ssword</strong>

- グループ: **Finance**

Active Directory (AD) でユーザーアカウントとグループアカウントを作成する方法の詳細については、「」を参照してください [https://technet.microsoft.com/library/cc783323%28v=ws.10%29.aspx](/previous-versions/windows/it-pro/windows-server-2003/cc783323(v=ws.10)) 。

**Robert Hatley** アカウントを **Finance** グループに追加します。 Active Directory のグループにユーザーを追加する方法の詳細については、「」を参照してください [https://technet.microsoft.com/library/cc737130%28v=ws.10%29.aspx](/previous-versions/windows/it-pro/windows-server-2003/cc737130(v=ws.10)) 。

### <a name="create-a-gmsa-account"></a>GMSA アカウントの作成
Active Directory フェデレーションサービス (AD FS) (AD FS) のインストールと構成では、グループの管理されたサービスアカウント (GMSA) アカウントが必要です。

##### <a name="to-create-a-gmsa-account"></a>GMSA アカウントを作成するには

1.  Windows PowerShell コマンド ウィンドウを開いて、次のコマンドを入力します。

    ```
    Add-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)
    New-ADServiceAccount FsGmsa -DNSHostName adfs1.contoso.com -ServicePrincipalNames http/adfs1.contoso.com

    ```

## <a name="step-2-configure-the-federation-server-adfs1-by-using-device-registration-service"></a><a name="BKMK_4"></a>手順 2: デバイス登録サービスを使用してフェデレーション サーバー (ADFS1) を構成する
別の仮想マシンをセットアップするには、Windows Server 2012 R2 をインストールし、ドメイン**contoso.com**に接続します。 ドメインに参加した後、コンピューターをセットアップし、AD FS の役割のインストールと構成に進みます。

これらの手順を説明したビデオを視聴するには、「 [Active Directory フェデレーション サービスの使い方ビデオ シリーズ: AD FS サーバー ファームのインストール](https://channel9.msdn.com/Search?term=Active%20Directory%20Federation%20Services#pubDate=year&ch9Search)」を参照してください。

### <a name="install-a-server-ssl-certificate"></a>サーバー SSL 証明書のインストール
ADFS1 サーバーのサーバー SSL (Secure Socket Layer) 証明書を、ローカル コンピューター ストアにインストールする必要があります。 この証明書には次の属性が必要です。

-   サブジェクト名 (CN): adfs1.contoso.com

-   サブジェクト代替名 (DNS): adfs1.contoso.com

-   サブジェクト代替名 (DNS): enterpriseregistration.contoso.com

[証明書の登録 Web サービスガイダンス](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831822(v=ws.11)#configure-a-ca-for-the-certificate-enrollment-web-service)

「[Active Directory フェデレーション サービスの使い方ビデオ シリーズ: 証明書の更新](https://channel9.msdn.com/Search?term=Active%20Directory%20Federation%20Services#pubDate=year&ch9Search)」。

### <a name="install-the-ad-fs-server-role"></a>AD FS サーバーの役割のインストール

##### <a name="to-install-the-federation-service-role-service"></a>フェデレーション サービス役割サービスをインストールするには

1. ドメイン管理者アカウントを使用してサーバーにログオン administrator@contoso.com します。

2. Server Manager を起動します。 サーバー マネージャーを起動するには、Windows の**スタート**画面で **[サーバー マネージャー]** をクリックするか、または Windows デスクトップの Windows タスク バーで **[サーバー マネージャー]** をクリックします。 **[ダッシュボード]** ページにある **[ようこそ]** タイルの **[クイック スタート]** タブで、**[役割と機能の追加]** をクリックします。 または、**[管理]** メニューの **[役割と機能の追加]** をクリックすることもできます。

3. **[開始する前に]** ページで、 **[次へ]** をクリックします。

4. **[インストールの種類の選択]** ページで、**[役割ベースまたは機能ベースのインストール]** をクリックし、**[次へ]** をクリックします。

5. **[宛先サーバーの選択]** ページで、**[サーバー プールからサーバーを選択]** をクリックし、ターゲット コンピューターが選択されていることを確認してから、**[次へ]** をクリックします。

6. **[サーバーの役割の選択]** ページで、**[Active Directory フェデレーション サービス]** をクリックし、**[次へ]** をクリックします。

7. [**機能の選択**] ページで、[**次へ**] をクリックします。

8. [**Active Directory フェデレーション サービス (AD FS)**] ページで、[**次へ**] をクリックします。

9. **[インストール オプションの確認]** ページの情報を確認し、**[必要に応じて対象サーバーを自動的に再起動する]** チェック ボックスをオンにして、**[インストール]** をクリックします。

10. **[インストールの進行状況]** ページで、すべてが正常にインストールされたことを確認し、**[閉じる]** をクリックします。

### <a name="configure-the-federation-server"></a>フェデレーション サーバーの構成
次の手順ではフェデレーション サーバーを構成します。

##### <a name="to-configure-the-federation-server"></a>フェデレーション サーバーを構成するには

1.  Server Manager の [**ダッシュボード**] ページで、[**通知**] フラグをクリックし、[**サーバーにフェデレーション サービスを構成します**] をクリックします。

    **Active Directory フェデレーション サービス構成ウィザード**が開きます。

2.  **[ようこそ]** ページで、**[フェデレーション サーバー ファームに最初のフェデレーション サーバーを作成します]** を選択し、**[次へ]** をクリックします。

3.  **[AD DS への接続]** ページで、このコンピューターが参加している **contoso.com** Active Directory ドメインのドメイン管理者権限を持つアカウントを指定し、**[次へ]** をクリックします。

4.  **[サービスのプロパティの指定]** ページで次の操作を実行してから、**[次へ]** をクリックします。

    -   前の手順で取得した SSL 証明書をインポートします。 この証明書は必須のサービス認証証明書です。 SSL 証明書の保存場所を参照します。

    -   フェデレーション サービスの名前に「**adfs1.contoso.com**」と入力します。 この値は、Active Directory 証明書サービス (AD CS) に SSL 証明書を登録したときに指定したのと同じ値です。

    -   フェデレーション サービスの表示名に「**Contoso Corporation**」と入力します。

5.  **[サービス アカウントの指定]** ページで、**[既存のドメイン ユーザー アカウントまたはグループの管理されたサービス アカウントを使用してください]** を選択し、ドメイン コントローラーの作成時に作成した GMSA アカウント **fsgmsa** を指定します。

6.  **[構成データベースの指定]** ページで、**[Windows Internal Database を使用してサーバーにデータベースを作成します]** を選択し、**[次へ]** をクリックします。

7.  **[オプションの確認]** ページで、構成の選択内容を確認し、**[次へ]** をクリックします。

8.  **[前提条件の確認]** ページで、すべての前提条件の確認が正常に完了したことを確認し、**[構成]** をクリックします。

9. **[結果]** ページで結果を確認し、構成が正常に完了したことを確認してから、**[フェデレーション サービス展開を完了するために必要な次の手順]** をクリックします。

### <a name="configure-device-registration-service"></a>デバイス登録サービスの構成
次の手順では、ADFS1 サーバーでデバイス登録サービスを構成します。 これらの手順を説明したビデオを視聴するには、「 [Active Directory フェデレーション サービスの使い方ビデオ シリーズ: デバイス登録サービスを有効にする](https://channel9.msdn.com/)」を参照してください。

##### <a name="to-configure-device-registration-service-for-windows-server-2012-rtm"></a>Windows Server 2012 RTM でデバイス登録サービスを構成するには

1.  > [!IMPORTANT]
    > **次の手順は、Windows Server 2012 R2 RTM ビルドに該当します。**

    Windows PowerShell コマンド ウィンドウを開いて、次のコマンドを入力します。

    ```
    Initialize-ADDeviceRegistration
    ```

    サービスアカウントの入力を求められたら、「 **contosofsgmsa $**」と入力します。

    次に、Windows PowerShell コマンドレットを実行します。

    ```
    Enable-AdfsDeviceRegistration
    ```

2.  ADFS1 サーバーで、**AD FS 管理**コンソールの **[認証ポリシー]** に移動します。 **[グローバル プライマリ認証の編集]** を選択します。 **[デバイス認証の有効化]** の横にあるチェック ボックスをオンにして、**[OK]** をクリックします。

### <a name="add-host-a-and-alias-cname-resource-records-to-dns"></a>ホスト (A) およびエイリアス (CNAME) リソース レコードの DNS への追加
DC1 では、デバイス登録サービス用に次のドメイン ネーム システム (DNS) レコードを作成する必要があります。

|入力|種類|Address|
|---------|--------|-----------|
|adfs1|ホスト (A)|AD FS サーバーの IP アドレス|
|enterpriseregistration|エイリアス (CNAME)|adfs1.contoso.com|

次の手順に従って、ホスト (A) リソース レコードを会社のフェデレーション サーバーとデバイス登録サービスの DNS ネーム サーバーに追加できます。

この手順を実行するには、少なくとも Administrators グループのメンバーシップまたは同等の権限を持つメンバーシップが必要です。 適切なアカウントおよびグループメンバーシップの使用方法の詳細については、「 <https://go.microsoft.com/fwlink/?LinkId=83477> ローカルおよびドメインの既定のグループ ()」を参照して <https://go.microsoft.com/fwlink/p/?LinkId=83477> ください。

##### <a name="to-add-a-host-a-and-alias-cname-resource-records-to-dns-for-your-federation-server"></a>ホスト (A) およびエイリアス (CNAME) リソース レコードをフェデレーション サーバーの DNS に追加するには

1.  DC1 のサーバー マネージャーで、**[ツール]** メニューの **[DNS]** をクリックし、DNS スナップインを開きます。

2.  コンソール ツリーで [DC1] を展開し、**[前方参照ゾーン]** を展開して **[contoso.com]** を右クリックし、**[新しいホスト (A または AAAA)]** をクリックします。

3.  **[名前]** に AD FS ファームで使用する名前を入力します。 このチュートリアルでは、「**adfs1**」と入力します。

4.  **[IP アドレス]** に ADFS1 サーバーの IP アドレスを入力します。 **[ホストの追加]** をクリックします。

5.  **[contoso.com]** を右クリックし、**[新しいエイリアス (CNAME)]** をクリックします。

6.  **[新しいリソース レコード]** ダイアログ ボックスで、**[エイリアス名]** ボックスに「**enterpriseregistration**」と入力します。

7.  ターゲット ホスト ボックスの [完全修飾ドメイン名 (FQDN)] に「**adfs1.contoso.com**」と入力し、[**OK**] をクリックします。

    > [!IMPORTANT]
    > 実際の展開では、会社に複数のユーザー プリンシパル名 (UPN) サフィックスがある場合、DNS の各 UPN サフィックスに 1 つずつ、複数の CNAME レコードを作成する必要があります。

## <a name="step-3-configure-the-web-server-webserv1-and-a-sample-claims-based-application"></a><a name="BKMK_5"></a>手順 3: Web サーバー (WebServ1) とサンプルの要求ベースのアプリケーションを構成する
Windows Server 2012 R2 オペレーティングシステムをインストールして仮想マシン (WebServ1) をセットアップし、それをドメイン**contoso.com**に接続します。 ドメインに参加したら、Web サーバーの役割のインストールと構成を開始できます。

このトピックの最初に示したチュートリアルを完了するには、フェデレーション サーバー (ADFS1) で保護されたサンプル アプリケーションが必要です。

[https://www.microsoft.com/download/details.aspx?id=4451](https://www.microsoft.com/download/details.aspx?id=4451)サンプルの要求ベースのアプリケーションを含む、Windows Identity FOUNDATION SDK () をダウンロードできます。

このサンプルの要求ベースのアプリケーションで Web サーバーをセットアップするには、次の手順を完了する必要があります。

> [!NOTE]
> これらの手順は、Windows Server 2012 R2 オペレーティングシステムを実行する web サーバーでテストされています。

1.  [Web サーバーの役割と Windows Identity Foundation をインストールする](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_15)

2.  [Windows Identity Foundation SDK をインストールする](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_13)

3.  [単純な要求ベースのアプリケーションを IIS で構成する](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_9)

4.  [フェデレーション サーバーで証明書利用者信頼を作成する](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_11)

### <a name="install-the-web-server-role-and-windows-identity-foundation"></a><a name="BKMK_15"></a>Web サーバーの役割と Windows Identity Foundation をインストールする

1. > [!NOTE]
   > Windows Server 2012 R2 のインストールメディアにアクセスできる必要があります。

   とパスワードを使用して、WebServ1 にログオンし <strong>administrator@contoso.com</strong> <strong>pass@word1</strong> ます。

2. サーバー マネージャーを開き、**[ダッシュボード]** ページにある **[ようこそ]** タイルの **[クイック スタート]** タブで、**[役割と機能の追加]** をクリックします。 または、**[管理]** メニューの **[役割と機能の追加]** をクリックすることもできます。

3. **[開始する前に]** ページで、 **[次へ]** をクリックします。

4. **[インストールの種類の選択]** ページで、**[役割ベースまたは機能ベースのインストール]** をクリックし、**[次へ]** をクリックします。

5. **[宛先サーバーの選択]** ページで、**[サーバー プールからサーバーを選択]** をクリックし、ターゲット コンピューターが選択されていることを確認してから、**[次へ]** をクリックします。

6. **[サーバーの役割の選択]** ページで、**[Web サーバー (IIS)]** の横にあるチェック ボックスをオンにして、**[機能の追加]** をクリックし、**[次へ]** をクリックします。

7. **[機能の選択]** ページで、**[Windows Identity Foundation 3.5]** を選択し、**[次へ]** をクリックします。

8. **[Web サーバーの役割 (IIS)]** ページで、**[次へ]** をクリックします。

9. **[役割サービスの選択]** ページで、**[アプリケーション開発]** を選択して展開します。 **[ASP.NET 3.5]** を選択して **[機能の追加]** をクリックし、**[次へ]** をクリックします。

10. **[インストール オプションの確認]** ページで、**[代替ソース パスの指定]** をクリックします。 Windows Server 2012 R2 のインストールメディアにある Sxs ディレクトリへのパスを入力します。 例については、「d」を使用します。 **[OK]** をクリックし、**[インストール]** をクリックします。

### <a name="install-windows-identity-foundation-sdk"></a><a name="BKMK_13"></a>Windows Identity Foundation SDK をインストールする

1.  WindowsIdentityFoundation-SDK-3.5.msi を実行して、Windows Identity Foundation SDK 3.5 (をインストールし https://www.microsoft.com/download/details.aspx?id=4451) ます。 既定のオプションをすべて選択してください。

### <a name="configure-the-simple-claims-app-in-iis"></a><a name="BKMK_9"></a>単純な要求ベースのアプリケーションを IIS で構成する

1.  コンピューターの証明書ストアに有効な SSL 証明書をインストールします。 この証明書には、Web サーバーの名前 **webserv1.contoso.com** が含まれている必要があります。

2.  C:program files Files (x86) Windows Identity Foundation SDKv 3.5 SamplesQuick StartWeb ApplicationPassiveRedirectBasedClaimsAwareWebApp の内容を C:InetpubClaimapp. にコピーします。

3.  **Default.aspx.cs** ファイルを編集して、要求のフィルタリングを無効にします。 この手順を実行することで、フェデレーション サーバーが発行するすべての要求がサンプル アプリケーションに表示されます。 次の操作を行います。

    1.  **Default.aspx.cs** をテキスト エディターで開きます。

    2.  ファイル内を検索して `ExpectedClaims`の 2 つ目のインスタンスを見つけます。

    3.  `IF` ステートメントとその中かっこ全体をコメント アウトします。 行の先頭に "//" (引用符を除く) を入力してコメントを指定します。

    4.  `FOREACH` ステートメントは次のコード例のようになります。

        ```
        Foreach (claim claim in claimsIdentity.Claims)
        {
           //Before showing the claims validate that this is an expected claim
           //If it is not in the expected claims list then don't show it
           //if (ExpectedClaims.Contains( claim.ClaimType ) )
           // {
              writeClaim( claim, table );
           //}
        }

        ```

    5.  **Default.aspx.cs** を保存して閉じます。

    6.  **web.config** をテキスト エディターで開きます。

    7.  `<microsoft.identityModel>` セクション全体を削除します。 `including <microsoft.identityModel>` から `</microsoft.identityModel>`までの内容 (開始および終了タグを含む) をすべて削除します。

    8.  **web.config** を保存して閉じます。

4.  **IIS マネージャーを構成します。**

    1.  **[インターネット インフォメーション サービス (IIS) マネージャー]** を開きます。

    2.  **[アプリケーション プール]** に移動して **[DefaultAppPool]** を右クリックし、**[詳細設定]** を選択します。 **[ユーザー プロファイルの読み込み]** を **[True]** に設定して、**[OK]** をクリックします。

    3.  **[DefaultAppPool]** を右クリックし、**[基本設定]** を選択します。 **[.NET CLR バージョン]** を **[.NET CLR バージョン v2.0.50727]** に変更します。

    4.  **[既定の Web サイト]** を右クリックし、**[バインドの編集]** を選択します。

    5.  ポート **443** への **HTTPS** バインドと、インストール済みの SSL 証明書を追加します。

    6.  **[既定の Web サイト]** を右クリックし、**[アプリケーションの追加]** を選択します。

    7.  エイリアスを**claimapp**に設定し、物理パスを**c:inetpubclaimapp**に設定します。

5.  フェデレーション サーバーで動作するように **claimapp** を構成するには、次の手順を実行します。

    1.  FedUtil.exe を実行します。これは、 **C:program files Files (x86) Windows Identity Foundation sdkv 3.5**にあります。

    2.  アプリケーションの構成の場所を**C:inetputclaimappweb.config**に設定し、アプリケーションの URI にサイトの URL ( ** https://webserv1.contoso.com /claimapp/**) を設定します。 **[次へ]** をクリックします。

    3.  [**既存の STS を使用**する] を選択し、AD FS サーバーのメタデータ URL を参照し **https://adfs1.contoso.com/federationmetadata/2007-06/federationmetadata.xml** ます。 **[次へ]** をクリックします。

    4.  **[証明書チェーンの検証を無効にする]** を選択し、**[次へ]** をクリックします。

    5.  **[暗号化なし]** を選択し、**[次へ]** をクリックします。 [**提供された要求**] ページで、**[次へ]** をクリックします。

    6.  **[毎日 WS-Federation メタデータを更新するタスクをスケジュールする]** の横にあるチェック ボックスをオンにします。 **[完了]** をクリックします。

    7.  サンプル アプリケーションの構成が完了しました。 アプリケーションの URL をテストすると **https://webserv1.contoso.com/claimapp** 、フェデレーションサーバーにリダイレクトされます。 証明書利用者信頼をまだ構成していないため、フェデレーション サーバーによりエラー ページが表示されます。 つまり、このテストアプリケーションは AD FS によってセキュリティ保護されていません。

Web サーバーで実行されるサンプルアプリケーションを AD FS でセキュリティで保護する必要があります。 これを行うには、フェデレーション サーバー (ADFS1) に証明書利用者信頼を追加します。 これらの手順を説明したビデオを視聴するには、「 [Active Directory フェデレーション サービスの使い方ビデオ シリーズ: 証明書利用者の信頼を追加する](https://channel9.msdn.com/Search?term=Active%20Directory%20Federation%20Services#pubDate=year&ch9Search)」を参照してください。

### <a name="create-a-relying-party-trust-on-your-federation-server"></a><a name="BKMK_11"></a>フェデレーション サーバーで証明書利用者信頼を作成する

1.  フェデレーション サーバー (ADFS1) で、**AD FS 管理コンソール**の **[証明書利用者信頼]** に移動し、**[証明書利用者信頼の追加]** をクリックします。

2.  **[データ ソースの選択]** ページで、**[オンラインまたはローカル ネットワークで公開されている証明書利用者についてのデータをインポートする]** を選択して、**claimapp** のメタデータ URL を入力し、**[次へ]** をクリックします。 FedUtil.exe の実行時にメタデータの .xml ファイルが作成されています。 このファイルはにあり **https://webserv1.contoso.com/claimapp/federationmetadata/2007-06/federationmetadata.xml** ます。

3.  **[表示名の指定]** ページで、証明書利用者信頼 **claimapp** の **[表示名]** を指定し、**[次へ]** をクリックします。

4.  **[多要素認証を今すぐ構成しますか?]** ページで、**[この証明書利用者信頼に対して多要素認証の設定を今は構成しません]** を選択し、**[次へ]** をクリックします。

5.  **[発行承認規則の選択]** ページで、**[すべてのユーザーに対してこの証明書利用者へのアクセスを許可する]** を選択し、**[次へ]** をクリックします。

6.  **[信頼の追加の準備完了]** ページで、**[次へ]** をクリックします。

7.  **[要求規則の編集]** ダイアログ ボックスで、**[規則の追加]** をクリックします。

8.  **[規則の種類の選択]** ページで、**[カスタム規則を使用して要求を送信]** を選択し、**[次へ]** をクリックします。

9. **[要求規則の構成]** ページで、**[要求規則名]** ボックスに「**All Claims**」と入力します。 **[カスタム規則]** ボックスに、次の要求規則を入力します。

    ```
    c:[ ]
    => issue(claim = c);

    ```

10. **[完了]** をクリックし、**[OK]** をクリックします。

## <a name="step-4-configure-the-client-computer-client1"></a><a name="BKMK_10"></a>手順 4: クライアント コンピューター (Client1) を構成する
別の仮想マシンをセットアップし、Windows 8.1 をインストールします。 この仮想マシンは、他の仮想マシンと同じ仮想ネットワークに属している必要があります。 このマシンは Contoso ドメインに参加させないでください。

クライアントは、フェデレーション サーバー (ADFS1) で使用される SSL 証明書を信頼する必要があります。これは、「 [Step 2: Configure the federation server (ADFS1) with Device Registration Service](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_4)」で設定します。 また、証明書の失効情報の検証が可能になっている必要もあります。

さらに、Client1 にログオンするには、Microsoft アカウントをセットアップして使用する必要があります。

## <a name="see-also"></a>参照
[Active Directory フェデレーションサービス (AD FS) 方法に関するビデオシリーズ: AD FS サーバーファーム](https://channel9.msdn.com/Search?term=Active%20Directory%20Federation%20Services#pubDate=year&ch9Search) 
 のインストール[Active Directory フェデレーションサービス (AD FS) 方法に関するビデオシリーズ: 証明書](https://channel9.msdn.com/Search?term=Active%20Directory%20Federation%20Services#pubDate=year&ch9Search) 
 の更新[Active Directory フェデレーションサービス (AD FS) 操作方法ビデオシリーズ: 証明書利用者信頼](https://channel9.msdn.com/Search?term=Active%20Directory%20Federation%20Services#pubDate=year&ch9Search) 
 を追加する[Active Directory フェデレーションサービス (AD FS) 方法に関するビデオシリーズ: デバイス登録サービス](https://channel9.msdn.com/) 
 を有効にする[Active Directory フェデレーションサービス (AD FS) 方法に関するビデオシリーズ: Web アプリケーションプロキシのインストール](https://channel9.msdn.com/Search?term=Active%20Directory%20Federation%20Services#pubDate=year&ch9Search)

