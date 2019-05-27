---
title: Windows Server のハイブリッド クラウド印刷をデプロイします。
description: Microsoft ハイブリッド クラウド印刷の設定方法
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: Windows Server 2016
ms.tgt_pltfrm: na
ms.topic: ''
ms.assetid: fc239aec-e719-47ea-92fc-d82a7247c5e9
author: msjimwu
ms.author: coreyp
manager: dongill
ms.date: 3/15/2018
ms.openlocfilehash: 6e9833489277c84739d489da34d352db8f565663
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881843"
---
# <a name="deploy-windows-server-hybrid-cloud-print-with-pre-authentication"></a>Windows Server のハイブリッド クラウド印刷を事前認証で展開する

>適用先:Windows Server 2016

このトピックでは、IT 管理者は、Microsoft ハイブリッド クラウド印刷のソリューションのエンド ツー エンドの展開について説明します。 このソリューションには、プリント サーバー、および有効に参加している場合、Azure Active Directory と MDM 管理対象として実行されている既存の Windows サーバー上のレイヤーが、デバイスを検出して、組織に印刷するには、プリンターが管理されています。

## <a name="pre-requisites"></a>前提条件

これは、さまざまなサブスクリプション、サービス、およびコンピューターがこのインストールを開始する前に取得する必要があります。 それらは次のとおりです。

-   Azure AD premium サブスクリプション
    
    参照してください[Azure サブスクリプションの概要](https://azure.microsoft.com/trial/get-started-active-directory/)、試用版のサブスクリプションを Azure にします。 

-   Intune などの MDM サービス
    
    参照してください[Microsoft Intune](https://www.microsoft.com/en-us/cloud-platform/microsoft-intune)、intune 試用版のサブスクリプション。

-   Active Directory として実行されている Windows Server

    参照してください[ステップ バイ ステップ。Windows Server 2016 での Active Directory 設定](https://blogs.technet.microsoft.com/canitpro/2017/02/22/step-by-step-setting-up-active-directory-in-windows-server-2016/)の Active Directory の設定に関するヘルプ。

-   プリント サーバーとして実行されている Windows Server 2016 がドメインに参加しています。
    
    参照してください[役割の追加と機能のウィザードを使用して役割、役割サービス、および機能をインストール](https://docs.microsoft.com/windows-server/administration/server-manager/install-or-uninstall-roles-role-services-or-features#BKMK_installarfw)、Windows サーバーに役割と役割サービスをインストールする方法について。

-   Azure AD Connect
    
    参照してください[Azure AD Connect のカスタム インストール](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-get-started-custom)、Azure AD Connect のセットアップ ヘルプを参照します。

-   別のドメインに azure のアプリケーション プロキシ コネクタには、Windows Server マシンが参加しています。
    
    参照してください[アプリケーション プロキシの概要し、コネクタのインストール](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable)、Azure アプリケーション プロキシ コネクタのセットアップ ヘルプを参照します。

-   パブリックに公開ドメイン名
    
    Azure によって作成するドメイン名を使用して、または独自のドメイン名を購入できます。

## <a name="deployment-steps"></a>展開の手順

このガイドでは、5 つのインストール手順について説明します。

- 手順 1:Azure AD の間で同期する Azure AD Connect をインストールし、オンプレミスの AD
- 手順 2:プリント サーバーにハイブリッド クラウド印刷のパッケージをインストールします。
- 手順 3:Install Azure アプリケーション プロキシ (AAP) と Kerberos の制約付き委任 (KCD)
- 手順 4:必要な MDM ポリシーを構成します。
- 手順 5:共有プリンターを公開します。

### <a name="step-1---install-azure-ad-connect-to-sync-between-azure-ad-and-on-premises-ad"></a>手順 1 - Azure AD の間で同期に接続する Azure AD をインストールし、オンプレミスの AD
1. Windows Server Active Directory コンピューターでは、Azure AD Connect ソフトウェアをダウンロードします。
2. Azure AD Connect のインストール パッケージを起動し、選択**簡単設定を使う**
3. インストール プロセスで必要な情報を入力し、クリックして**インストール**

### <a name="step-2---install-hybrid-cloud-print-package-on-the-print-server"></a>手順 2 - プリント サーバーでのハイブリッド クラウド印刷のインストール パッケージ

1. ハイブリッド クラウド印刷の PowerShell モジュールをインストールします。
    -  管理者特権の PowerShell コマンド プロンプトから次のコマンドを実行します。
        - `find-module -Name "PublishCloudPrinter"` PowerShell ギャラリー (PSGallery) のコンピューターに到達できることを確認するには
        - `install-module -Name "PublishCloudPrinter"`

    > 注: メッセージが表示 'PSGallery' が、信頼されていないリポジトリであることを通知します。  インストールを続行するには、' y' を入力します。

2. クラウド印刷のハイブリッド ソリューションをインストールします。
    - 管理者特権で同一の PowerShell コマンド プロンプトでディレクトリに移動します。 `C:\Program Files\WindowsPowerShell\Modules\PublishCloudPrinter\1.0.0.0`
    - Run <br>
        `CloudPrintDeploy.ps1 -AzureTenant <Domain name used by Azure AD Connect> -AzureTenantGuid <Azure AD Directory ID>`
3.  SSL をサポートする 2 つの IIS エンドポイントを構成します。
    -   SSL 証明書は、自己署名証明書またはによって信頼された証明機関 (CA) から発行されたいずれかを指定できます。
    -  自己署名証明書を使用する場合、証明書がクライアント コンピューターにインポートされることを確認します。
4.  SQLite パッケージをインストールします。
    - 管理者特権で PowerShell コマンド プロンプトを開く
    - System.Data.SQLite nuget パッケージをダウンロードするには、次のコマンドを実行します。 <br>
        `Register-PackageSource -Name nuget.org -ProviderName NuGet -Location https://www.nuget.org/api/v2/ -Trusted -Force`
    - パッケージをインストールするには、次のコマンドを実行します。<br>
    `Install-Package system.data.sqlite [-requiredversion x.x.x.x] -providername nuget`

    > 注: ダウンロードして除外する最新のバージョンをインストールすることをお勧め、"-requiredversion"オプション。

5.  SQLite の dll に MopriaCloudService Webapp コピー \<bin\>フォルダー (**c:\\inetpub\\wwwroot\\MopriaCloudService\\bin**)。 <br>
    - SQLite バイナリがある必要があります"\\Program Files\\PackageManagement\\NuGet\\パッケージ"

            \\System.Data.SQLite.**Core**.x.x.x.x\\lib\\net46\\System.Data.SQLite.dll
            --\> \<bin\>\\System.Data.SQLite.dll  
            \\System.Data.SQLite.**Core**.x.x.x.x\\build\\net46\\x86\\SQLite.Interop.dll
            --\> \<bin\>\\**x86**\\SQLite.Interop.dll  
            \\System.Data.SQLite.**Core**.x.x.x.x\\build\\net46\\x64\\SQLite.Interop.dll
            --\> \<bin\>\\**x64**\\SQLite.Interop.dll
            \\System.Data.SQLite.**Linq**.x.x.x.x\\lib\\net46\\System.Data.SQLite.Linq.dll
            --\> \<bin\>\\System.Data.SQLite.Linq.dll  
            \\System.Data.SQLite.**EF6**.x.x.x.x\\lib\\net46\\System.Data.SQLite.EF6.dll
            --\> \<bin\>\\System.Data.SQLite.EF6.dll

    > 注: x.x.x.x は上にインストールされている SQLite バージョンです。

6.  更新プログラム、 `c:\inetpub\wwwroot\MopriaCloudService\web.config` SQLite バージョン x.x.x.x を次に含めるファイル\<ランタイム\>/\<assemblyBinding\>セクション。

        <dependentAssembly>
        assemblyIdentity name="System.Data.SQLite" culture="neutral" publicKeyToken="db937bc2d44ff139" /
        <bindingRedirect oldVersion="0.0.0.0-x.x.x.x" newVersion="x.x.x.x" />
        </dependentAssembly>
        <dependentAssembly>
        <assemblyIdentity name="System.Data.SQLite.Core" culture="neutral" publicKeyToken="db937bc2d44ff139" />
        <bindingRedirect oldVersion="0.0.0.0-x.x.x.x" newVersion="x.x.x.x" />
        </dependentAssembly>
        <dependentAssembly>
        <assemblyIdentity name="System.Data.SQLite.EF6" culture="neutral" publicKeyToken="db937bc2d44ff139" />
        <bindingRedirect oldVersion="0.0.0.0-x.x.x.x" newVersion="x.x.x.x" />
        </dependentAssembly>
        <dependentAssembly>
        <assemblyIdentity name="System.Data.SQLite.Linq" culture="neutral" publicKeyToken="db937bc2d44ff139" />
        <bindingRedirect oldVersion="0.0.0.0-x.x.x.x" newVersion="x.x.x.x" />
        </dependentAssembly>

7. SQLite データベースを作成します。
    -  ダウンロードしてから SQLite ツールのバイナリのインストール <https://www.sqlite.org/>
    -  移動して**c:\\inetpub\\wwwroot\\MopriaCloudService\\データベース**ディレクトリ
    -  このディレクトリにデータベースを作成する次のコマンドを実行します。  `sqlite3.exe MopriaDeviceDb.db ".read MopriaSQLiteDb.sql"`
    -  ファイル エクスプ ローラーでセキュリティ タブで Mopria データベースに発行することができるユーザーまたはグループを追加する MopriaDeviceDb.db ファイルのプロパティを開きます
        - 必要な管理者ユーザー グループの追加のみをお勧めします。
8. OAuth2 認証をサポートするために Azure AD で 2 つの web アプリ登録
    -   Azure AD テナントの管理ポータルにグローバル管理者としてログイン
        1. 印刷のエンドポイントを追加する"アプリの登録 タブを参照してください。
            -   アプリケーションを追加で、「新しいアプリケーションの登録」を選択します。
            -   適切な名前を指定し、選択"Web app/API
            -   サインオン URL ="http://MicrosoftEnterpriseCloudPrint/CloudPrint"
        2.  探索エンドポイントを繰り返します
            -   サインオン URL ="http://MopriaDiscoveryService/CloudPrint"
        3.  ネイティブ クライアント アプリケーションを繰り返します
            -   アプリ名を指定するときに、「アプリケーションの種類」として「ネイティブ クライアント アプリケーション」を選択して確認します。
            -   リダイレクト URI ="https://\<サービスのマシンのエンドポイント\>/RedirectUrl"
        4.  ネイティブ クライアント アプリの [設定] に移動します。
            -   後のセットアップ手順で使用される"アプリケーション ID"値をコピーします。
            -   [必要なアクセス許可] を選択します。
                1.  [追加] をクリックします。
                2.  "API の選択 をクリックします。
                3.  印刷のエンドポイントとアプリ エンドポイントを作成するときに定義した名前によって探索エンドポイントの検索
                4.  2 つのエンドポイントを追加します。
                5.  各アプリのエンドポイントの「デリゲートされたアクセス許可」オプションが有効かどうかを確認します。
                6.  下部にある"Done"ボタンをクリックするかどうかを確認します。
                7.  両方のエンドポイントが追加されたら、「許可」をクリックします。  要求を承認するように求められたら [はい] を選択します。
            -   [リダイレクト URI] に移動し、一覧に次のリダイレクト Uri を追加します。 `ms-appx-web://Microsoft.AAD.BrokerPlugin/\<NativeClientAppID\>`
                `ms-appx-web://Microsoft.AAD.BrokerPlugin/S-1-15-2-3784861210-599250757-1266852909-3189164077-45880155-1246692841-283550366`

### <a name="step-3---install-azure-application-proxy-aap-with-kerberos-constrained-delegation-kcd"></a>手順 3 - Azure アプリケーション プロキシ (AAP) をインストールの Kerberos の制約付き委任 (KCD)
1. Azure AD (AAD) テナントの管理ポータルにログイン
    - AAD メニュー 一覧で、アプリケーション プロキシ を選択します。
    - 画面の上部にある「アプリケーション プロキシを有効化」をクリックします。
    - Web アプリケーション プロキシ (WAP) として機能するドメイン参加済み Windows Server マシンに"Application Proxy Connector"をダウンロードします。
2. WAP コンピューターにインストール"Application Proxy Connector"で、管理者としてログイン
    - インストール中に、アプリケーション プロキシ コネクタは、資格情報に与える、Azure の理念で AAP を有効にします。
    - WAP コンピューターがドメインに、オンプレミスの Active Directory に参加しているかどうかを確認します。
3. 移動し、Active Directory マシン**ツール]、[ユーザーとコンピューター**
    - アプリケーション プロキシ コネクタを実行しているマシンを選択します
    - 右クリックして**プロパティの委任** -> タブ
    - 選択**指定されたサービスのみへの委任でこのコンピューターを信頼します。**
    - 選択**任意の認証プロトコルを使用します。**
    - **このアカウントが委任された資格情報を提示できるサービス**
        - サービス (MopriaDiscoveryService と MicrosoftEnterpriseCloudPrint サービス) を実行しているコンピューターの SPN id の値を追加します。
            - SPN の場合は、つまりコンピューター自体の SPN を入力します"ホスト/\<MachineName\>.\<ドメイン\>"<br>
                `HOST/appServer.Contoso.com`
4. AAD テナントの管理ポータルに戻るし、アプリケーション プロキシの追加
    - 移動して、**エンタープライズ アプリケーション** タブ
    - クリックして**新しいアプリケーション**
    - 選択**オンプレミス アプリケーション**し、フィールドに入力
        - 名前:希望する任意の名前
        - 内部 URL:これは、WAP コンピューターにアクセスできる Mopria 検出のクラウド サービスに内部 URL です。
        - 外部 URL:組織の適切な構成します。
        - 事前認証方法:Azure Active Directory

    >   注:上記のすべての設定がない場合は、使用可能な設定でプロキシを追加作成したアプリケーション プロキシを選択し、移動、**アプリケーション プロキシ**タブし、上記のすべての情報を追加します。

    - 作成後に戻す**エンタープライズ アプリケーション** -> **すべてのアプリケーション**、先ほど作成した新しいアプリケーションを選択します。
    - 移動して**でのシングル サインオン**、「シングル サインオン モード」が「統合 Windows 認証」に設定されているかどうかを確認
    - 上記手順 3.3 の場合で指定した SPN に"内部アプリケーション SPN"を設定します。
    - "委任されたログイン Id"は「ユーザー プリンシパル名」に設定されているかどうかを確認します。

5. エンタープライズ クラウドの印刷サービスの上、4 を繰り返して、エンタープライズ クラウドの印刷サービスに内部 URL を指定
6. Azure AD テナントの管理ポータルに戻りに移動**アプリの登録**および -> [設定] のネイティブ クライアント アプリを選択します
    - 選択**のために必要なアクセス許可**
        - 作成した 2 つの新しいプロキシ アプリケーションを追加します。
        - これら 2 つのアプリケーションの委任されたアクセス許可の付与
        - プロキシの両方のアプリケーションが追加されたら、"アクセス許可の付与 をクリックします。  要求を承認するように求められたら [はい] を選択します。

7. Mopria クラウド サービスと印刷のエンタープライズ クラウド サービスのマシンに対して IIS で Windows 認証を有効にします。
    - Windows 認証機能がインストールされていることを確認します。
        1. サーバー マネージャーを開く
        2. クリックして**管理**
        3. クリックして**役割と機能の追加**
        4. 選択**役割ベースまたは機能ベースのインストール**
        5. サーバーを選択します。
        6. Web サーバー (IIS) で Web サーバー]-> [セキュリティ]-> [、選択**Windows 認証**
        7. インストールを完了するまで、次へをクリックします。
    - IIS で Windows 認証を有効にします。
        1. インターネット インフォメーション サービス (IIS) マネージャーを開く
        2. 各サービス/サイト。
            1.  サービス/サイトを選択します。
            2.  ダブルクリック**認証**
            3.  クリックして**Windows 認証**] をクリック**を有効にする**[**アクション**

### <a name="step-4---configure-the-required-mdm-policies"></a>手順 4 - 必要な MDM ポリシーを構成します。
- MDM プロバイダーにログイン
- Enterprise Cloud Print ポリシー グループを検索し、次のガイドラインを次のポリシーを構成します。
    - CloudPrintOAuthAuthority = https://login.microsoftonline.com/\<Azure AD ディレクトリ ID\>
    - CloudPrintOAuthClientId Azure AD 管理ポータルで登録されているネイティブの Web アプリの"アプリケーション ID"値を =
    - CloudPrinterDiscoveryEndPoint = 手順 3.3 で作成した Mopria 検出サービス Azure アプリケーション プロキシの外部 URL (末尾には同じですが正確である必要があります/)
    - MopriaDiscoveryResourceId = 手順 3.4 で作成した Mopria 検出サービス Azure アプリケーション プロキシの外部 URL (する必要がありますが、まったく同じ末尾を含む、/)
    - CloudPrintResourceId = Enterprise Cloud Print サービス Azure アプリケーション プロキシの手順 3.5 で作成した外部 URL (する必要がありますが、まったく同じ末尾を含む、/)
    - DiscoveryMaxPrinterLimit =\<正の整数\>

>   注:Microsoft Intune サービスを使用している場合は、「クラウド プリンター」カテゴリの下のこれらの設定を確認できます。

|Intune の表示名                     |ポリシー                         |
|----------------------------------------|-------------------------------|
|プリンターの検出 URL                   |CloudPrinterDiscoveryEndpoint  |
|プリンター アクセスの権限 URL            |CloudPrintOAuthAuthority       |
|Azure のネイティブ クライアント アプリの GUID            |CloudPrintOAuthClientId        |
|印刷サービスのリソース URI              |CloudPrintResourceId           |
|(モバイルのみ) を照会するプリンターの最大数  |DiscoveryMaxPrinterLimit       |
|プリンター検出サービスのリソース URI  |MopriaDiscoveryResourceId      |

>   注:クラウド印刷のポリシー グループが使用できない場合は、MDM プロバイダーは、OMA-URI 設定をサポートしているのと同じポリシーを設定できます。  これを参照してください<a href="https://docs.microsoft.com/windows/client-management/mdm/policy-csp-enterprisecloudprint#enterprisecloudprint-cloudprintoauthauthority">記事</a>の追加情報。

- OMA-URI
    - `CloudPrintOAuthAuthority = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/CloudPrintOAuthAuthority`
        - 値 = `https://login.microsoftonline.com/` \<Azure AD ディレクトリ ID\>
    - `CloudPrintOAuthClientId = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/CloudPrintOAuthClientId`
        - 値 = \<Azure AD のネイティブ アプリのアプリケーション ID\>
    - `CloudPrinterDiscoveryEndPoint = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/CloudPrinterDiscoveryEndPoint`
        - 値 = 手順 3.3 で作成した Mopria 検出サービス Azure アプリケーション プロキシの外部 URL (末尾には同じですが正確である必要があります/)
    - `MopriaDiscoveryResourceId = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/MopriaDiscoveryResourceId`
        - 値 = 手順 3.4 で作成した Mopria 検出サービス Azure アプリケーション プロキシの外部 URL (する必要がありますが、まったく同じ末尾を含む、/)
    - `CloudPrintResourceId = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/CloudPrintResourceId`
        - 値 = Enterprise Cloud Print サービス Azure アプリケーション プロキシの手順 3.5 で作成した外部 URL (する必要がありますが、まったく同じ末尾を含む、/)
    - `DiscoveryMaxPrinterLimit = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/DiscoveryMaxPrinterLimit`
        - 値 =\<正の整数\>

### <a name="step-5---publish-desired-shared-printers"></a>手順 5 - 目的の共有プリンターを公開します。
1. 目的のプリンターをプリント サーバーをインストールします。
2. プリンターのプロパティの UI を使用して、プリンターを共有します。
3. 目的のアクセスを許可するユーザーのセットを選択します。
4. 変更を保存し、プリンターのプロパティ ウィンドウを閉じます
5. Windows 10 Fall Creator Update マシンでは、Windows PowerShell コマンド プロンプトを開く
    1. 次のコマンドを実行します
        - `find-module -Name "PublishCloudPrinter"` PowerShell ギャラリー (PSGallery) のコンピューターに到達できることを確認するには
        - `install-module -Name "PublishCloudPrinter"`

        >   注: メッセージが表示 'PSGallery' が、信頼されていないリポジトリであることを通知します。  インストールを続行するには、' y' を入力します。

        - 発行 CloudPrinter
            - プリンターが定義されている共有プリンター名を =
            - 製造元プリンターの製造元を =
            - モデル プリンター モデルを =
            - OrgLocation = などのプリンターの場所を指定する JSON 文字列。   `{"attrs": [{"category":"country", "vs":"USA", "depth":0}, {"category":"organization", "vs":"Microsoft", "depth":1}, {"category":"site", "vs":"Redmond, WA", "depth":2}, {"category":"building", "vs":"Building 1", "depth":3}, {"category":"floor\_number", "vn":1, "depth":4}, {"category":"room\_name", "vs":"1111", "depth":5}]}`
            - Sddl = プリンターのアクセス許可を表す SDDL 文字列。 これは、プリンターのプロパティのセキュリティ タブを適切に変更して、コマンド プロンプトで次のコマンドを実行して取得できます。 `(Get-Printer PrinterName -full).PermissionSDDL`
                例。"G:DUD:(A;OICI;FA;;;WD)"

            > 注: 追加する必要があります**`O:BA`** SDDL 設定として、値を設定する前に上記のコマンド プロンプト コマンドからの結果にプレフィックスとして。  以下に例を示します。SDDL = `O:BAG:DUD:(A;OICI;FA;;;WD)`

            - DiscoveryEndpoint 手順 3.4 で作成した Mopria 検出サービス Azure アプリケーション プロキシの外部 URL を =
            - PrintServerEndpoint Enterprise Cloud Print サービス Azure アプリケーション プロキシの手順 3.5 で作成した外部 URL を =
            - AzureClientId 上から登録済みの Web アプリのネイティブ値のアプリケーション ID を =
            - AzureTenantGuid、Azure AD テナントのディレクトリ ID を =
            - DiscoveryResourceId プロキシ Mopria 検出のクラウド サービスの [省略可能] アプリケーションの ID を =

        > 注: コマンドラインでは、すべての必須パラメーターの値を入力できます。<br>
**発行 CloudPrinter** PowerShell コマンドの構文。 <br>
発行 CloudPrinter-プリンター\<文字列\>-の製造元\<文字列\>-モデル\<文字列\>- OrgLocation\<文字列\>Sddl \<文字列\>- DiscoveryEndpoint\<文字列\>- PrintServerEndpoint\<文字列\>- AzureClientId\<文字列\>AzureTenantGuid \<文字列\>[-DiscoveryResourceId\<文字列\>] <br>
サンプル コマンド: `publish-cloudprinter -Printer EcpPrintTest -Manufacturer Microsoft -Model FilePrinterEcp -OrgLocation '{"attrs": [{"category":"country", "vs":"USA", "depth":0}, {"category":"organization", "vs":"MyCompany", "depth":1}, {"category":"site", "vs":"MyCity, State", "depth":2}, {"category":"building", "vs":"Building 1", "depth":3}, {"category":"floor\_number", "vn":1, "depth":4}, {"category":"room\_name", "vs":"1111", "depth":5}]}' -Sddl "O:BAG:DUD:(A;OICI;FA;;;WD)" -DiscoveryEndpoint https://<services-machine-endpoint>/mcs -PrintServerEndpoint https://<services-machine-endpoint>/ecp -AzureClientId <Native Web App ID> -AzureTenantGuid <Azure AD Directory ID> -DiscoveryResourceId <Proxied Mopria Discovery Cloud Service App ID>`


## <a name="verifying-the-deployment"></a>展開を確認します。
構成した MDM ポリシーを持つ Azure AD 参加しているデバイス。
- Web ブラウザーを開いて https:// に移動して&lt;サービスのマシンのエンドポイント&gt;mcs/サービス (探索エンドポイントの外部の URL)
- このエンドポイントの機能のセットを記述する JSON テキストを表示する必要があります。
- 移動して"OS の設定 -\>デバイス -\>プリンターおよびスキャナー"
    - 「クラウド プリンターを検索」のリンクが表示する必要があります。
    - リンクをクリックします
    - 「検索場所を選択してください」リンクをクリックします。
        - デバイスの場所の階層を表示する必要があります。
    - 場所を選択し、クリックして**OK**順にクリックします**検索**プリンターを検索する ボタン
    - プリンターの選択およびクリックして**デバイスの追加**ボタン
    - 成功したプリンターのインストール後からプリンターに印刷、お気に入りのアプリ

>   注:プリント サーバーのマシンで、出力ファイルを見つけることができます"EcpPrintTest"プリンターを使用して場合"c:\\ECPTestOutput\\EcpTestPrint.xps"の場所。
