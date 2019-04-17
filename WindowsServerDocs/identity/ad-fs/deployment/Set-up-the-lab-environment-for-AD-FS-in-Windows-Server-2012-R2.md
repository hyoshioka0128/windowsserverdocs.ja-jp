---
ms.assetid: 6b38480e-5b1c-49f0-9d46-8cf22f70f0d2
title: "Windows Server 2012 R2 の AD FS のラボ環境を設定します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 049a1a1b0a419b0194edfe56b356a9f1e8b4b058
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="set-up-the-lab-environment-for-ad-fs-in-windows-server-2012-r2"></a>Windows Server 2012 R2 の AD FS のラボ環境を設定します。

>Windows Server 2012 R2 の適用対象:

このトピックでは、次のチュートリアル ガイドのチュートリアルを完了するために使用できるテスト環境を構成する手順について説明します。

-   [チュートリアル: iOS デバイスでワークプ レースに参加します。](../../ad-fs/operations/Walkthrough--Workplace-Join-with-an-iOS-Device.md)

-   [Windows デバイスのチュートリアル: 職場への参加](../../ad-fs/operations/Walkthrough--Workplace-Join-with-a-Windows-Device.md)


-   [チュートリアル ガイド: 条件付きアクセス制御によるリスクを管理します。](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md)

-   [チュートリアル ガイド: 追加の多要素認証による個人情報アプリケーションのリスクを管理します。](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)

> [!NOTE]
> Web サーバーとフェデレーション サーバーを同じコンピューターにインストールすることはお勧めできません。

このテスト環境をセットアップするには、次の手順を実行します。

1.  [手順 1: ドメイン コントローラー (DC1) を構成します。](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_1)

2.  [手順 2: デバイス登録サービスによるフェデレーション サーバー (ADFS1) を構成します。](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_4)

3.  [手順 3: Web サーバー (WebServ1) とサンプル クレーム ベースのアプリケーションを構成します。](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_5)

4.  [手順 4: クライアント コンピューター (Client1) を構成します。](../../ad-fs/deployment/../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_10)

## <a name="BKMK_1"></a>手順 1: ドメイン コントローラー (DC1) を構成します。
このテスト環境の目的上、ルート Active Directory ドメインを呼び出すことができます**contoso.com**指定と**pass@word1**管理者のパスワードにします。

-   AD DS 役割サービスをインストールし、Active Directory ドメイン サービス (AD DS) して、コンピューター、ドメイン コントローラーで Windows Server 2012 R2 をインストールします。 この操作は、ドメイン コントローラー作成の一環として、AD DS スキーマをアップグレードします。 For more information and step-by-step instructions, see[https://technet.microsoft.com/ library/hh472162.aspx](https://technet.microsoft.com/library/hh472162.aspx).

### <a name="BKMK_2"></a>Active Directory のテスト アカウントを作成します。
ドメイン コントローラーが機能は、このドメインでテスト グループおよびテスト ユーザー アカウントを作成し、ユーザー アカウント、グループ アカウントを追加します。 これらのアカウントを使用して、このトピックの前に参照されるチュートリアル ガイドのチュートリアルを完了します。

次のアカウントを作成します。

-   ユーザー: **Robert Hatley**資格情報は、: ユーザー名: **RobertH**とパスワード。**P@ssword**

-   グループ: **Finance**

Active Directory (AD) でユーザー アカウントとグループ アカウントを作成する方法については、次を参照してください。[https://technet.microsoft.com/library/cc783323%28v.aspx](https://technet.microsoft.com/library/cc783323%28v=ws.10%29.aspx)します。

追加、**Robert Hatley**アカウントを**Finance**グループ。 For information on how to add a user to a group in Active Directory, see [https://technet.microsoft.com/library/cc737130%28v=ws.10%29.aspx](https://technet.microsoft.com/library/cc737130%28v=ws.10%29.aspx).

### <a name="create-a-gmsa-account"></a>GMSA アカウントを作成します。
グループ管理サービス アカウント (GMSA) アカウントが Active Directory フェデレーション サービス (AD FS) のインストールと構成の中に必要です。

##### <a name="to-create-a-gmsa-account"></a>GMSA アカウントを作成するには

1.  Windows PowerShell コマンド ウィンドウと種類を開きます。

    ```
    Add-KdsRootKey -EffectiveTime (Get-Date).AddHours(-10)
    New-ADServiceAccount FsGmsa -DNSHostName adfs1.contoso.com -ServicePrincipalNames http/adfs1.contoso.com

    ```

## <a name="BKMK_4"></a>手順 2: デバイス登録サービスを使用してフェデレーション サーバー (ADFS1) を構成します。
To set up another virtual machine, install  Windows Server 2012 R2  and connect it to the domain **contoso.com**. Set up the computer after you have joined it to the domain, and then proceed to install and configure the AD FS role.

For a video, see [Active Directory Federation Services How-To Video Series: Installing an AD FS Server Farm](https://technet.microsoft.com/video/dn469436).

### <a name="install-a-server-ssl-certificate"></a>サーバーの SSL 証明書をインストールします。
ローカル コンピューター ストアに ADFS1 サーバーでサーバー Secure Socket Layer (SSL) 証明書をインストールする必要があります。 証明書には、次の属性を持つ必要があります。

-   サブジェクト名 (CN): adfs1.contoso.com

-   サブジェクトの別名 (DNS): adfs1.contoso.com

-   サブジェクトの別名 (DNS): enterpriseregistration.contoso.com

For more information about setting up SSL certificates, see [Configure SSL/TLS on a Web site in the domain with an Enterprise CA](https://social.technet.microsoft.com/wiki/contents/articles/12485.configure-ssltls-on-a-web-site-in-the-domain-with-an-enterprise-ca.aspx).

[Active Directory Federation Services How-To Video Series: Updating Certificates](https://technet.microsoft.com/video/adfs-updating-certificates).

### <a name="install-the-ad-fs-server-role"></a>AD FS サーバー役割をインストールします。

##### <a name="to-install-the-federation-service-role-service"></a>フェデレーション サービス役割サービスをインストールするには

1.  ドメイン管理者アカウントを使用してサーバーにログオンadministrator@contoso.comします。

2.  サーバー マネージャーを起動します。 サーバー マネージャーを開始する] をクリックして**サーバー マネージャー** windows の**開始**画面、またはクリックして**サーバー マネージャー** Windows デスクトップで、Windows タスク バーにします。 **クイック スタート**のタブ、**ようこそ**タイルで、**ダッシュ ボード**ページで、[**役割と機能の追加**します。 また、クリックすることができます**追加の役割と機能**上、**管理**メニュー。

3.  **開始する前に**] ページで [**次**します。

4.  **インストールの種類の選択**] ページで [**役割ベースまたは機能ベースのインストール**、] をクリックし、**[次へ]**します。

5.  **対象サーバーの選択**] ページで [**サーバー プールからサーバーを選択**、対象のコンピューターが選択されていることを確認] をクリックし、**[次へ]**します。

6.  **サーバーの役割の選択**] ページで [ **Active Directory フェデレーション サービス**、] をクリックし、**[次へ]**します。

7.  **機能の選択**] ページで [**次**します。

8.  **Active Directory フェデレーション サービス (AD FS)** ] ページで [**次**します。

9. 情報を確認した後、**インストール オプションの確認**] ページで、[、**必要な場合に、移行先サーバーを自動的に再起動**チェック ボックスをオンにし**インストール**します。

10. **インストールの進行状況**] ページで、正しくすべてインストールされていることを確認してをクリックして**閉じる**します。

### <a name="configure-the-federation-server"></a>フェデレーション サーバーを構成します。
次の手順では、フェデレーション サーバーを構成します。

##### <a name="to-configure-the-federation-server"></a>フェデレーション サーバーを構成するには

1.  サーバー マネージャーに**ダッシュ ボード**] ページで [、**通知**フラグを設定すると、クリックして**サーバーで、フェデレーション サービスを構成**します。

    **Active Directory フェデレーション サービス構成ウィザード**が開きます。

2.  **ようこそ**] ページで、[**フェデレーション サーバー ファームに最初のフェデレーション サーバーを作成する**、] をクリックし、**[次へ]**します。

3.  **AD DS への接続**] ページで、ドメイン管理者権限を持つアカウントを指定して、**contoso.com**クリックして、このコンピューターが参加している Active Directory ドメイン**次**します。

4.  **サービスのプロパティの指定**] ページで、次の操作ををクリックして**次**:

    -   前に入手した、SSL 証明書をインポートします。 この証明書は、必要なサービスの認証証明書です。 SSL 証明書の場所を参照します。

    -   To provide a name for your federation service, type **adfs1.contoso.com**. This value is the same value that you provided when you enrolled an SSL certificate in Active Directory Certificate Services (AD CS).

    -   フェデレーション サービスの表示名を指定する次のように入力します。**Contoso Corporation**します。

5.  **サービス アカウントの指定**] ページで、[**既存のドメイン ユーザー アカウントを使用または管理されたサービス アカウントをグループ化**、GMSA アカウントを指定**fsgmsa**ドメイン コントローラーの作成時に作成することです。

6.  **構成データベースの指定**] ページで、[ **Windows Internal Database を使用してこのサーバーにデータベースを作成**、] をクリックし、**次**します。

7.  **オプションの確認**] ページで、構成の選択を確認してをクリックして**次**します。

8.  **前提チェック**] ページで、すべての前提条件チェックが正常に完了したことを確認] をクリックし、**構成**します。

9. **結果**ページ、結果を確認して、構成が正常に完了するかどうかを確認および] をクリックし、**フェデレーション サービスの展開を完了するために必要な次の手順**します。

### <a name="configure-device-registration-service"></a>デバイス登録サービスを構成します。
次の手順では、ADFS1 サーバーでデバイス登録サービスを構成します。 For a video, see [Active Directory Federation Services How-To Video Series: Enabling the Device Registration Service](https://technet.microsoft.com/video/adfs-how-to-enabling-the-device-registration-service).

##### <a name="to-configure-device-registration-service-for-windows-server-2012-rtm"></a>デバイス登録サービスの Windows Server 2012 RTM を構成するには

1.  > [!IMPORTANT]
    > **次の手順は、Windows Server 2012 R2 RTM ビルドに適用されます。**

    Windows PowerShell コマンド ウィンドウと種類を開きます。

    ```
    Initialize-ADDeviceRegistration
    ```

    サービス アカウントのメッセージが表示されたら、入力**\fsgmsa$**します。

    Windows PowerShell コマンドレットを実行できるようになりました。

    ```
    Enable-AdfsDeviceRegistration
    ```

2.  ADFS1 サーバーで、**AD FS 管理**コンソールに移動**認証ポリシー**します。 選択**グローバル プライマリ認証の編集**します。 横にチェック ボックスをオン**デバイス認証を有効にする**、] をクリックし、**OK**します。

### <a name="add-host-a-and-alias-cname-resource-records-to-dns"></a>DNS にホスト (A) およびエイリアス (CNAME) リソース レコードを追加します。
DC1 で、デバイス登録サービスを次のドメイン ネーム システム (DNS) レコードが作成されたことを確認する必要があります。

|エントリ|種類|アドレス|
|---------|--------|-----------|
|adfs1|ホスト (A)|AD FS サーバーの IP アドレス|
|enterpriseregistration|エイリアス (CNAME)|adfs1.contoso.com|

フェデレーション サーバーとデバイス登録サービスの企業の DNS ネーム サーバーにホスト (A) リソース レコードを追加するのに、次の手順を使用することができます。

Administrators グループまたは同等のメンバーシップは、この手順を実行する最低限必要です。 Review details about using the appropriate accounts and group memberships in the  HYPERLINK "https://go.microsoft.com/fwlink/?LinkId=83477" Local and Domain Default Groups (https://go.microsoft.com/fwlink/p/?LinkId=83477).

##### <a name="to-add-a-host-a-and-alias-cname-resource-records-to-dns-for-your-federation-server"></a>フェデレーション サーバーの DNS にホスト (A) およびエイリアス (CNAME) リソース レコードを追加するには

1.  DC1 で、サーバー マネージャーで、上、**ツール**] メニューのをクリックして**DNS**、DNS スナップインを開きます。

2.  コンソール ツリーで、DC1 を展開し、**前方参照ゾーン**、右クリックして**contoso.com**、] をクリックし、**新しいホスト (A または AAAA)**します。

3.  **名、** AD FS ファームを使用する名前を入力します。 このチュートリアルでは、次のように入力します。**adfs1**します。

4.  **IP アドレス**、ADFS1 サーバーの IP アドレスを入力します。 をクリックして**ホストの追加**します。

5.  右クリック**contoso.com**、] をクリックし、**新しいエイリアス (CNAME)**します。

6.  **新しいリソース レコード**] ダイアログ ボックスで、「 **enterpriseregistration**で、**エイリアス名**ボックス。

7.  完全修飾ドメイン名 (FQDN) のターゲット ホスト ボックス、入力**adfs1.contoso.com**、] をクリックし、**OK**します。

    > [!IMPORTANT]
    > 実際の展開では、複数のユーザー プリンシパル名 (UPN) サフィックスがある企業複数の CNAME レコードが DNS 内の各 UPN サフィックスごとに 1 つを作成する必要があります。

## <a name="BKMK_5"></a>手順 3: Web サーバー (WebServ1) とサンプル クレーム ベースのアプリケーションを構成します。
Set up a virtual machine (WebServ1) by installing the  Windows Server 2012 R2  operating system and connect it to the domain **contoso.com**. After it is joined to the domain, you can proceed to install and configure the Web Server role.

このトピックの前に参照したチュートリアルを完了するには、フェデレーション サーバー (ADFS1) で保護されているサンプル アプリケーションが必要です。

You can download Windows Identity Foundation SDK ([https://www.microsoft.com/download/details.aspx?id=4451](https://www.microsoft.com/download/details.aspx?id=4451), which includes a sample claims-based application.

このサンプルの要求ベース アプリケーションと Web サーバーを設定する次の手順を実行する必要があります。

> [!NOTE]
> 次の手順は、Windows Server 2012 R2 オペレーティング システムを実行する Web サーバーでテスト済みです。

1.  [Web サーバーの役割と Windows Identity Foundation をインストールします。](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_15)

2.  [Windows Identity Foundation SDK をインストールします。](../../ad-fs/deployment/../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_13)

3.  [IIS でシンプルなクレーム アプリを構成します。](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_9)

4.  [フェデレーション サーバーで証明書利用者信頼を作成します。](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_11)

### <a name="BKMK_15"></a>Web サーバーの役割と Windows Identity Foundation をインストールします。

1.  > [!NOTE]
    > Windows Server 2012 R2 インストール メディアへのアクセスが必要です。

    使用して WebServ1 にログオン**administrator@contoso.com**と、パスワード**pass@word1**します。

2.  サーバー マネージャーで、**クイック スタート**のタブ、**ようこそ**タイルで、**ダッシュ ボード**ページで、[**役割と機能の追加**します。 また、クリックすることができます**追加の役割と機能**上、**管理**メニュー。

3.  **開始する前に**] ページで [**次**します。

4.  **インストールの種類の選択**] ページで [**役割ベースまたは機能ベースのインストール**、] をクリックし、**[次へ]**します。

5.  **対象サーバーの選択**] ページで [**サーバー プールからサーバーを選択**、対象のコンピューターが選択されていることを確認] をクリックし、**[次へ]**します。

6.  **サーバーの役割の選択**] ページで、横にチェック ボックスをオン**Web サーバー (IIS)**、] をクリックして**機能の追加**、] をクリックし、**次**します。

7.  **機能の選択**ページで、選択**Windows Identity Foundation 3.5**、] をクリックし、**[次へ]**します。

8.  **Web サーバーの役割 (IIS)** ] ページで [**次**します。

9. **役割サービスの選択**] ページで選択して展開**アプリケーション開発**します。 選択**ASP.NET 3.5**、] をクリックして**機能の追加**、] をクリックし、**[次へ]**します。

10. **インストール オプションの確認**] ページで [**代替ソース パスの指定**します。 Windows Server 2012 R2 インストール メディアにある Sxs ディレクトリへのパスを入力します。 たとえば D:\Sources\Sxs です。 をクリックして**OK**、] をクリックし、**インストール**します。

### <a name="BKMK_13"></a>Windows Identity Foundation SDK をインストールします。

1.  Run WindowsIdentityFoundation-SDK-3.5.msi to install Windows Identity Foundation SDK 3.5 (https://www.microsoft.com/download/details.aspx?id=4451). すべての既定のオプションを選択します。

### <a name="BKMK_9"></a>IIS でシンプルなクレーム アプリを構成します。

1.  コンピューターの証明書ストアに有効な SSL 証明書をインストールします。 証明書は、Web サーバーの名前を含める必要があります**webserv1.contoso.com**します。

2.  C:\Inetpub\Claimapp を C:\Program Files (x86) \Windows Identity Foundation SDK\v3.5\Samples\Quick Start\Web Application\PassiveRedirectBasedClaimsAwareWebApp の内容をコピーします。

3.  編集、**Default.aspx.cs**ファイルを要求のフィルター処理は行われません。 この手順を実行して、サンプル アプリケーションがフェデレーション サーバーによって発行されたすべての信頼性情報が表示されていることを確認します。 次の操作を行います。

    1.  開いている**Default.aspx.cs**テキスト エディターでします。

    2.  ファイルの 2 番目のインスタンスを検索します`ExpectedClaims`します。

    3.  全体をコメント アウト`IF`ステートメントとその中かっこします。 」と入力してコメントを示すため"//"(引用符は不要)、行の先頭にします。

    4.  `FOREACH`ステートメントは次のコード例のようになります。

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

    5.  保存して閉じます**Default.aspx.cs**します。

    6.  開いている**Web.config**テキスト エディターでします。

    7.  全体を削除します`<microsoft.identityModel>`セクションです。 すべて削除する`including <microsoft.identityModel>`と最大と`</microsoft.identityModel>`します。

    8.  保存して閉じます**Web.config**します。

4.  **IIS マネージャーを構成します。**

    1.  開いている**インターネット インフォメーション サービス (IIS) マネージャー**します。

    2.  移動**アプリケーション プール**、右クリックして**DefaultAppPool**を選択する**高度な設定**します。 設定**ユーザー プロファイルの読み込み**に**True**、] をクリックし、**OK**します。

    3.  右クリック**DefaultAppPool**を選択する**基本的な設定**します。 変更、**.NET CLR バージョン**に**.NET CLR バージョン v2.0.50727**します。

    4.  右クリック**既定の Web サイト**を選択する**バインドの編集]**します。

    5.  追加、**HTTPS**ポートにバインドする**443**インストールされている SSL 証明書を使用します。

    6.  右クリック**既定の Web サイト**を選択する**アプリケーションの追加**します。

    7.  エイリアスを設定**claimapp**とへの物理パス**c:\inetpub\claimapp**します。

5.  構成する**claimapp**、フェデレーション サーバーを使用するには、次を実行します。

    1.  FedUtil.exe にある実行**C:\Program Files (x86) \Windows Identity Foundation SDK\v3.5**します。

    2.  アプリケーション構成の場所に設定**C:\inetput\claimapp\Web.config**、サイトの URL をアプリケーション URI を設定および**https://webserv1.contoso.com/claimapp/**します。 をクリックして**次**します。

    3.  選択**既存の STS を使用して**AD FS サーバーのメタデータ URL を参照して**https://adfs1.contoso.com/federationmetadata/2007-06/federationmetadata.xml**します。 をクリックして**次**します。

    4.  選択**証明書チェーンの検証を無効にする**、] をクリックし、**[次へ]**します。

    5.  選択**暗号化なし**、] をクリックし、**次**します。 **信頼性情報を提供**] ページで [**次**します。

    6.  横にチェック ボックスをオン**毎日 Ws-federation メタデータ更新を実行するタスクをスケジュール**します。 をクリックして**完了**します。

    7.  サンプル アプリケーションが構成されているようになりました。 アプリケーションの URL をテストする場合**https://webserv1.contoso.com/claimapp**、フェデレーション サーバーにリダイレクトする必要があります。 フェデレーション サーバーの証明書利用者信頼を構成していないためエラー ページが表示されます。 つまり、AD FS によってこのテスト アプリケーションを保護されていません。

AD FS と Web サーバーで実行されているサンプル アプリケーションをセキュリティで保護する必要がありますできるようになりました。 フェデレーション サーバー (ADFS1) で証明書利用者信頼を追加することで、これを行うことができます。 For a video, see [Active Directory Federation Services How-To Video Series: Add a Relying Party Trust](https://technet.microsoft.com/video/adfs-how-to-add-a-relying-party-trust).

### <a name="BKMK_11"></a>フェデレーション サーバーで証明書利用者信頼を作成します。

1.  フェデレーション サーバー (ADFS1) での**AD FS 管理コンソール**に移動**証明書利用者信頼**、] をクリックし、**証明書利用者信頼の追加**します。

2.  **データ ソースの選択**ページで、選択**オンラインまたはローカル ネットワーク上に発行された証明書利用者についてのデータをインポート**のメタデータ URL を入力**claimapp**、] をクリックし、**[次へ]**します。 FedUtil.exe を実行するいると、メタデータの .xml ファイルが作成されます。 ある**https://webserv1.contoso.com/claimapp/federationmetadata/2007-06/federationmetadata.xml**します。

3.  **表示名の指定**] ページで、指定の**表示名**、証明書利用者信頼の**claimapp**、] をクリックし、**[次へ]**します。

4.  **Multi-factor Authentication を今すぐ構成しますか?** ] ページで、[**をこの時点でこの証明書利用者信頼に対して多要素認証の設定を指定しない**、] をクリックし、**次**します。

5.  **[発行承認規則**] ページで、[**この証明書利用者にアクセスするすべてのユーザーを許可**、] をクリックし、**[次へ]**します。

6.  **信頼を追加する準備ができて**ページで、[**次**します。

7.  **要求規則の編集**ダイアログ ボックスで、をクリックして**規則の追加**します。

8.  **ルールの種類の選択**] ページで、[**カスタム規則を使用して要求を送信**、] をクリックし、**[次へ]**します。

9. **要求規則の構成**] ページで、**要求規則名**ボックスに、入力**すべてクレーム**します。 **カスタム規則**ボックスに、次の要求規則を入力します。

    ```
    c:[ ]
    => issue(claim = c);

    ```

10. をクリックして**完了**、] をクリックし、 **OK**します。

## <a name="BKMK_10"></a>手順 4: クライアント コンピューター (Client1) を構成します。
別の仮想マシンをセットアップし、Windows 8.1 をインストールします。 この仮想マシンは、他のマシンと同じ仮想ネットワーク上でなければなりません。 このコンピューターは、Contoso ドメインに参加していない必要があります。

クライアントで設定したフェデレーション サーバー (ADFS1) で使用される SSL 証明書を信頼する必要があります[手順 2: デバイス登録サービスによるフェデレーション サーバー (ADFS1) を構成する](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_4)します。 また、証明書の証明書の失効情報を検証できる必要があります。

設定し、Microsoft アカウントを使用して、Client1 にログオンする必要があります。

## <a name="see-also"></a>参照してください。


- [Active Directory フェデレーション サービスの使い方ビデオ シリーズ: AD FS サーバー ファームのインストール](https://technet.microsoft.com/video/dn469436)
- [Active Directory フェデレーション サービスの使い方ビデオ シリーズ: 証明書の更新](https://technet.microsoft.com/video/adfs-updating-certificates)
- [Active Directory フェデレーション サービスの使い方ビデオ シリーズ: 証明書利用者信頼を追加します。](https://technet.microsoft.com/video/adfs-how-to-add-a-relying-party-trust)
- [Active Directory フェデレーション サービスの使い方ビデオ シリーズ: デバイス登録サービスを有効にします。](https://technet.microsoft.com/video/adfs-how-to-enabling-the-device-registration-service)
- [Active Directory フェデレーション サービスの使い方ビデオ シリーズ: Web アプリケーション プロキシのインストール](https://technet.microsoft.com/video/dn469438)



