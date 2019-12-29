---
title: Windows Server ハイブリッドクラウド印刷の展開
description: Microsoft ハイブリッドクラウド印刷をセットアップする方法
ms.prod: windows-server
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
ms.openlocfilehash: af5cd5f83633df7e704f4b768baf8dc6d78546aa
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370445"
---
# <a name="deploy-windows-server-hybrid-cloud-print-with-pre-authentication"></a>Windows Server のハイブリッド クラウド印刷を事前認証で展開する

>適用対象: Windows Server 2016

このトピックでは、IT 管理者向けに、Microsoft ハイブリッドクラウド印刷ソリューションのエンドツーエンドのデプロイについて説明します。 このソリューションレイヤーは、プリントサーバーとして実行されている既存の Windows Server 上にあり、Azure Active Directory 参加済みで、MDM で管理されたデバイスが、組織で管理されているプリンタを検出して印刷できるようにします。

## <a name="pre-requisites"></a>前提条件

このインストールを開始する前に、いくつかのサブスクリプション、サービス、およびコンピューターを取得する必要があります。 それらは次のとおりです。

-   Premium サブスクリプションの Azure AD
    
    Azure の試用版サブスクリプションについては、「 [azure サブスクリプションの概要](https://azure.microsoft.com/trial/get-started-active-directory/)」を参照してください。 

-   MDM サービス (Intune など)
    
    Intune の試用版サブスクリプションについては、「 [Microsoft Intune](https://www.microsoft.com/en-us/cloud-platform/microsoft-intune)」を参照してください。

-   Active Directory として実行されている Windows Server

    Active Directory を設定する方法については、「ステップバイ[ステップ: Windows Server 2016 での Active Directory](https://blogs.technet.microsoft.com/canitpro/2017/02/22/step-by-step-setting-up-active-directory-in-windows-server-2016/)のセットアップ」を参照してください。

-   プリントサーバーとして実行されているドメインに参加している Windows Server 2016
    
    Windows Server に役割と役割サービスをインストールする方法について[は、「役割と機能の追加ウィザードを使用して役割、役割サービス、および機能をインストール](https://docs.microsoft.com/windows-server/administration/server-manager/install-or-uninstall-roles-role-services-or-features#BKMK_installarfw)する」を参照してください。

-   Azure AD Connect
    
    Azure AD Connect を設定する方法については、「 [Azure AD Connect のカスタムインストール](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-get-started-custom)」を参照してください。

-   別のドメインに参加している Windows Server コンピューター上のプロキシコネクタを Azure アプリケーション
    
    Azure アプリケーションプロキシコネクタのセットアップについては、「[アプリケーションプロキシの概要」および「コネクタのインストール](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable)」を参照してください。

-   公開されるドメイン名
    
    Azure によって作成されたドメイン名を使用することも、独自のドメイン名を購入することもできます。

## <a name="deployment-steps"></a>展開の手順

このガイドでは、5つのインストール手順について説明します。

- 手順 1: Azure AD とオンプレミスの AD 間で同期するために Azure AD Connect をインストールする
- 手順 2: ハイブリッドクラウド印刷パッケージをプリントサーバーにインストールする
- 手順 3: Kerberos の制約付き委任 (KCD) を使用して Azure アプリケーションプロキシ (AAP) をインストールする
- 手順 4: 必要な MDM ポリシーを構成する
- 手順 5: 共有プリンターを公開する

### <a name="step-1---install-azure-ad-connect-to-sync-between-azure-ad-and-on-premises-ad"></a>手順 1-Azure AD とオンプレミスの AD を同期するために Azure AD Connect をインストールする
1. Windows Server Active Directory コンピューターで、Azure AD Connect ソフトウェアをダウンロードします。
2. Azure AD Connect インストールパッケージを起動し、 **[簡易設定を使用する]** を選択します。
3. インストールプロセスで要求された情報を入力し、 **[インストール]** をクリックします。

### <a name="step-2---install-hybrid-cloud-print-package-on-the-print-server"></a>手順 2-プリントサーバーへのハイブリッドクラウド印刷パッケージのインストール

1. ハイブリッドクラウド印刷の PowerShell モジュールをインストールする
   - 管理者特権の PowerShell コマンドプロンプトから次のコマンドを実行します。
      - コンピューターが PowerShell ギャラリーに接続できることを確認するための `find-module -Name "PublishCloudPrinter"` (PSGallery)
      - `install-module -Name "PublishCloudPrinter"`

     > 注: "PSGallery" が信頼されていないリポジトリであることを示すメッセージが表示される場合があります。  インストールを続行するには、「y」と入力します。

2. ハイブリッドクラウド印刷ソリューションをインストールする
    - 同じ管理者特権の PowerShell コマンドプロンプトで、ディレクトリをに変更し `C:\Program Files\WindowsPowerShell\Modules\PublishCloudPrinter\1.0.0.0`
    - Run <br>
        `CloudPrintDeploy.ps1 -AzureTenant <Domain name used by Azure AD Connect> -AzureTenantGuid <Azure AD Directory ID>`
3. 2つの IIS エンドポイントで SSL をサポートするように構成する
   -   SSL 証明書は、自己署名証明書か、一部の信頼された証明機関 (CA) から発行された証明書のいずれかになります。
   -  自己署名証明書を使用する場合は、証明書がクライアントコンピューターにインポートされていることを確認します。
4. SQLite パッケージのインストール
   - 管理者特権の PowerShell コマンドプロンプトを開く
   - 次のコマンドを実行して、system.string nuget パッケージをダウンロードします。 <br>
       `Register-PackageSource -Name nuget.org -ProviderName NuGet -Location https://www.nuget.org/api/v2/ -Trusted -Force`
   - 次のコマンドを実行して、パッケージをインストールします。<br>
   `Install-Package system.data.sqlite [-requiredversion x.x.x.x] -providername nuget`

   > 注: "-requiredversion" オプションを残して、最新バージョンをダウンロードしてインストールすることをお勧めします。

5. SQLite dll を MopriaCloudService Webapp \<bin\> フォルダー (**C:\\inetpub\\wwwroot\\MopriaCloudService\\bin**) にコピーします。 <br>
   - SQLite バイナリは、"\\Program Files\\PackageManagement\\NuGet\\Packages" にある必要があります。

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

   > 注: x.y は、上記でインストールされた SQLite バージョンです。

6. 次の \<ランタイム\>/\<assemblyBinding\> セクションに SQLite バージョン2.x を含めるように `c:\inetpub\wwwroot\MopriaCloudService\web.config` ファイルを更新します。

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
    -  <https://www.sqlite.org/> から SQLite ツールバイナリをダウンロードしてインストールします。
    -  **C:\\inetpub\\wwwroot\\MopriaCloudService\\データベース**ディレクトリにアクセスします。
    -  次のコマンドを実行して、このディレクトリにデータベースを作成します。 `sqlite3.exe MopriaDeviceDb.db ".read MopriaSQLiteDb.sql"`
    -  ファイルエクスプローラーで、Moare Adevicedb. db ファイルのプロパティを開き、[セキュリティ] タブで Mo先読みデータベースへの公開が許可されているユーザーまたはグループを追加します。
        - 必要な管理ユーザーグループのみを追加することをお勧めします。
8. OAuth2 認証をサポートするために Azure AD で2つの web アプリを登録する
   - Azure AD テナント管理ポータルにグローバル管理者としてログインします。
     1. 印刷エンドポイントを追加するには、[アプリの登録] タブを開きます
        - [アプリケーションの追加] を選択し、[新しいアプリケーションの登録] を選択します。
        - 適切な名前を入力し、[Web アプリ/API] を選択します。
        - サインオン URL = "<http://MicrosoftEnterpriseCloudPrint/CloudPrint>"
     2. 探索エンドポイントに対してこの手順を繰り返します。
        - サインオン URL = "<http://MopriaDiscoveryService/CloudPrint>"
     3. ネイティブクライアントアプリケーションに対してこの手順を繰り返します。
        -   アプリ名を指定する場合は、[アプリケーションの種類] として [ネイティブクライアントアプリケーション] を選択していることを確認してください。
        -   リダイレクト URI = "https://\<\>/redirecturl"
     4. ネイティブクライアントアプリの [設定] にアクセスします。
        -   後のセットアップ手順で使用する "アプリケーション ID" の値をコピーします。
        -   [必要なアクセス許可] を選択します。
            1.  [追加] をクリックします。
            2.  [API の選択] をクリックします。
            3.  アプリケーションエンドポイントの作成時に定義した名前を使用して、印刷エンドポイントと探索エンドポイントを検索します。
            4.  2つのエンドポイントを追加する
            5.  各アプリエンドポイントの [委任されたアクセス許可] オプションが有効になっていることを確認します。
            6.  下部にある [完了] ボタンをクリックしてください。
            7.  両方のエンドポイントが追加されたら、[アクセス許可の付与] をクリックします。  要求の承認を求めるメッセージが表示されたら、[はい] を選択します。
        -   "リダイレクト URI" にアクセスし、一覧に次のリダイレクト Uri を追加します: `ms-appx-web://Microsoft.AAD.BrokerPlugin/\<NativeClientAppID\>`
            `ms-appx-web://Microsoft.AAD.BrokerPlugin/S-1-15-2-3784861210-599250757-1266852909-3189164077-45880155-1246692841-283550366`

### <a name="step-3---install-azure-application-proxy-aap-with-kerberos-constrained-delegation-kcd"></a>手順 3-Kerberos の制約付き委任 (KCD) を使用して Azure アプリケーションプロキシ (AAP) をインストールする
1. Azure AD (AAD) テナント管理ポータルにログインします。
    - [AAD] メニューの一覧で、[アプリケーションプロキシ] を選択します。
    - 画面の上部にある [アプリケーションプロキシを有効にする] をクリックします。
    - Web アプリケーションプロキシ (WAP) として機能するドメインに参加している Windows Server コンピューターに "アプリケーションプロキシコネクタ" をダウンロードします。
2. WAP コンピューターで、管理者としてログインし、"アプリケーションプロキシコネクタ" をインストールします。
    - インストール中に、アプリケーションプロキシコネクタに対して、AAP を有効にする Azure の基本に対する資格情報を指定します。
    - WAP マシンがオンプレミスの Active Directory にドメイン参加していることを確認します。
3. Active Directory マシンで、[ツール] **-[> ユーザーとコンピューター** ] にアクセスします。
    - アプリケーションプロキシコネクタを実行しているコンピューターを選択します
    - 右クリックして**プロパティの委任** -> タブ
    - **[指定されたサービスへの委任でのみこのコンピューターを信頼する]** を選択します。
    - **[任意の認証プロトコルを使用する]** を選択します。
    - **[このアカウントが委任された資格情報を提示できるサービス]** で
        - サービスを実行しているコンピューターの SPN id の値を追加します (MoMicrosoftEnterpriseCloudPrint Adiscoveryservice と service)
            - SPN として、コンピューター自体の SPN を入力します。つまり、"HOST/\<MachineName\>です。\<ドメイン\>"<br>
                `HOST/appServer.Contoso.com`
4. AAD テナント管理ポータルに戻り、アプリケーションプロキシを追加します。
   - **[エンタープライズアプリケーション]** タブにアクセスします。
   - **[新しいアプリケーション]** をクリックします。
   - **[オンプレミスのアプリケーション**] を選択し、フィールドに入力します。
       - 名前: 任意の名前を指定します。
       - 内部 URL: これは、WAP コンピューターがアクセスできる、検出クラウドサービスの内部 URL です
       - 外部 URL: 組織に合わせて構成します。
       - 事前認証方法: Azure Active Directory

     >   注: 上記のすべての設定が見つからない場合は、使用可能な設定を使用してプロキシを追加してから、作成したアプリケーションプロキシを選択し、 **[アプリケーションプロキシ]** タブにアクセスして、上記のすべての情報を追加します。

   - 作成したら、[**すべてのアプリケーション** -> **エンタープライズアプリケーション**] に戻り、先ほど作成した新しいアプリケーションを選択します。
   - **シングルサインオン** にアクセスし、シングルサインオンモード が 統合 Windows 認証 に設定されていることを確認します。
   - 上記の手順3.3 で指定した SPN に "内部アプリケーション SPN" を設定します。
   - "委任されたログイン Id" が "ユーザープリンシパル名" に設定されていることを確認します。

5. Enterprise Cloud Print Service の場合は、上記の手順 4. を繰り返し、エンタープライズクラウド印刷サービスの内部 URL を指定します。
6. Azure AD テナント管理ポータルに戻り、**アプリの登録**にアクセスして、ネイティブクライアントアプリ > [設定] を選択します。
    - **必要なアクセス許可**の選択
        - 先ほど作成した2つの新しいプロキシアプリケーションを追加します。
        - これら2つのアプリケーションに対して委任されたアクセス許可を付与する
        - 両方のプロキシアプリケーションが追加されたら、[アクセス許可の付与] をクリックします。  要求の承認を求めるメッセージが表示されたら、[はい] を選択します。

7. IIS で、クラウドサービスとエンタープライズクラウド印刷サービスコンピューターの Windows 認証を有効にします。
    - Windows 認証機能がインストールされていることを確認してください。
        1. サーバー マネージャーを開く
        2. **[管理]** をクリック
        3. [**役割と機能の追加] を**クリックします。
        4. **役割ベースまたは機能ベースのインストール**の選択
        5. サーバーを選択します
        6. Web サーバー (IIS)-> Web サーバー-> セキュリティ で、 **Windows 認証** を選択します。
        7. インストールが完了するまで [次へ] をクリックします。
    - IIS で Windows 認証を有効にする:
        1. インターネットインフォメーションサービス (IIS) マネージャーを開く
        2. 各サービス/サイト:
            1.  サービス/サイトの選択
            2.  **[認証]** をダブルクリックします。
            3.  **[Windows 認証]** をクリックし、 **[アクション]** で **[有効]** をクリックします。

### <a name="step-4---configure-the-required-mdm-policies"></a>手順 4-必要な MDM ポリシーを構成する
- MDM プロバイダーにログインする
- 次のガイドラインに従って、エンタープライズクラウドの印刷ポリシーグループを見つけ、ポリシーを構成します。
  - CloudPrintOAuthAuthority = https://login.microsoftonline.com/\<Azure AD ディレクトリ ID\>
  - CloudPrintOAuthClientId = Azure AD 管理ポータルに登録したネイティブ Web アプリの "アプリケーション ID" の値
  - Cloudプリンター Discoveryendpoint = 手順3.3 で作成された Azure アプリケーションプロキシの外部 URL (完全に一致している必要がありますが、末尾は/以外である必要があります)
  - Mo先読み Adiscoveryresourceid = 手順3.4 で作成された Azure アプリケーションプロキシの外部 URL (末尾の/を含む、正確に同じである必要があります)
  - CloudPrintResourceId = 手順3.5 で作成されたエンタープライズクラウド印刷サービス Azure アプリケーションプロキシの外部 URL (末尾の/を含む完全に同じである必要があります)
  - Discoverymaxプリンター Limit = 正の整数 \<\>

>   注: Microsoft Intune サービスを使用している場合は、[Cloud Printer] (クラウドプリンター) カテゴリの下にこれらの設定が表示されます。

|Intune の表示名                     |ポリシー                         |
|----------------------------------------|-------------------------------|
|プリンター検出 URL                   |Cloudプリンター Discoveryendpoint  |
|プリンターアクセス機関の URL            |CloudPrintOAuthAuthority       |
|Azure native client アプリ GUID            |CloudPrintOAuthClientId        |
|印刷サービスのリソース URI              |CloudPrintResourceId           |
|クエリする最大プリンター (モバイルのみ)  |Discoverymaxプリンターの制限       |
|プリンター検出サービスのリソース URI  |Mo先読み Adiscoveryresourceid      |

>   注: [クラウド印刷ポリシー] グループが使用できないが、MDM プロバイダーが OMA-URI 設定をサポートしている場合は、同じポリシーを設定できます。  詳細については、こちらの<a href="https://docs.microsoft.com/windows/client-management/mdm/policy-csp-enterprisecloudprint#enterprisecloudprint-cloudprintoauthauthority">記事</a>を参照してください。

- OMA-URI
    - `CloudPrintOAuthAuthority = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/CloudPrintOAuthAuthority`
        - 値 = `https://login.microsoftonline.com/`\<Azure AD Directory ID\>
    - `CloudPrintOAuthClientId = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/CloudPrintOAuthClientId`
        - 値 = \<Azure AD ネイティブアプリのアプリケーション ID\>
    - `CloudPrinterDiscoveryEndPoint = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/CloudPrinterDiscoveryEndPoint`
        - 値 = 手順3.3 で作成された Azure アプリケーションプロキシの外部 URL (完全に同じである必要がありますが、末尾にはがありません)
    - `MopriaDiscoveryResourceId = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/MopriaDiscoveryResourceId`
        - 値 = 手順3.4 で作成された Azure アプリケーションプロキシの外部 URL (末尾の/を含む、正確に同じである必要があります)
    - `CloudPrintResourceId = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/CloudPrintResourceId`
        - 値 = 手順3.5 で作成された、エンタープライズクラウド印刷サービス Azure アプリケーションプロキシの外部 URL (末尾の/を含む完全に同じである必要があります)
    - `DiscoveryMaxPrinterLimit = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/DiscoveryMaxPrinterLimit`
        - 値 = 正の整数 \<\>

### <a name="step-5---publish-desired-shared-printers"></a>手順 5-必要な共有プリンターを発行する
1. プリントサーバーに必要なプリンターをインストールする
2. プリンターのプロパティ UI を使用してプリンターを共有する
3. アクセス権を付与するユーザーのセットを選択します
4. 変更を保存し、[プリンターのプロパティ] ウィンドウを閉じます。
5. Windows 10 フォール Creator 更新コンピューターから、管理者特権の Windows PowerShell コマンドプロンプトを開きます。
   1. 次のコマンドを実行します
      - コンピューターが PowerShell ギャラリーに接続できることを確認するための `find-module -Name "PublishCloudPrinter"` (PSGallery)
      - `install-module -Name "PublishCloudPrinter"`

        >   注: "PSGallery" が信頼されていないリポジトリであることを示すメッセージが表示される場合があります。  インストールを続行するには、「y」と入力します。

      - 発行-CloudPrinter
        - Printer = 定義されている共有プリンター名
        - 製造元 = プリンターの製造元
        - モデル = プリンターモデル
        - OrgLocation = プリンターの場所を指定する JSON 文字列 (例: `{"attrs": [{"category":"country", "vs":"USA", "depth":0}, {"category":"organization", "vs":"Microsoft", "depth":1}, {"category":"site", "vs":"Redmond, WA", "depth":2}, {"category":"building", "vs":"Building 1", "depth":3}, {"category":"floor\_number", "vn":1, "depth":4}, {"category":"room\_name", "vs":"1111", "depth":5}]}`
        - Sddl = プリンターのアクセス許可を表す SDDL 文字列。 これを取得するには、プリンターのプロパティの [セキュリティ] タブを適切に変更し、コマンドプロンプトで次のコマンドを実行します。 `(Get-Printer PrinterName -full).PermissionSDDL`
            例: "G: DUD: (A; OICI; FA;;;WD) "

          > 注: 値を SDDL 設定として設定する前に、上記のコマンドプロンプトコマンドから結果にプレフィックスとして **`O:BA`** を追加する必要があります。  例: SDDL = `O:BAG:DUD:(A;OICI;FA;;;WD)`

        - DiscoveryEndpoint = 手順3.4 で作成した Azure アプリケーションプロキシの外部 URL
        - PrintServerEndpoint = 手順3.5 で作成したエンタープライズクラウド印刷サービス Azure アプリケーションプロキシの外部 URL
        - AzureClientId = 上記の登録済みのネイティブ Web アプリの値のアプリケーション ID
        - AzureTenantGuid = Azure AD テナントのディレクトリ ID
        - DiscoveryResourceId = [省略可能] プロキシ化された検出クラウドサービスのアプリケーション ID

        > 注: すべての必須パラメーター値をコマンドラインに入力することもできます。<br>
        **発行-CloudPrinter**PowerShell コマンドの構文: <br>
        \<文字列\> 製造元 \<文字列\>-モデル \<文字列\>-OrgLocation \<string\>-Sddl \<string\>-DiscoveryEndpoint \<string\>-PrintServerEndpoint \<string\>-AzureClientId \<string\>-AzureTenantGuid \<string\> [-Discoveryendpoint \<string\>] を指定します。 <br>
        サンプルコマンド: `publish-cloudprinter -Printer EcpPrintTest -Manufacturer Microsoft -Model FilePrinterEcp -OrgLocation '{"attrs": [{"category":"country", "vs":"USA", "depth":0}, {"category":"organization", "vs":"MyCompany", "depth":1}, {"category":"site", "vs":"MyCity, State", "depth":2}, {"category":"building", "vs":"Building 1", "depth":3}, {"category":"floor\_number", "vn":1, "depth":4}, {"category":"room\_name", "vs":"1111", "depth":5}]}' -Sddl "O:BAG:DUD:(A;OICI;FA;;;WD)" -DiscoveryEndpoint https://<services-machine-endpoint>/mcs -PrintServerEndpoint https://<services-machine-endpoint>/ecp -AzureClientId <Native Web App ID> -AzureTenantGuid <Azure AD Directory ID> -DiscoveryResourceId <Proxied Mopria Discovery Cloud Service App ID>`


## <a name="verifying-the-deployment"></a>デプロイを確認しています
MDM ポリシーが構成されている Azure AD 参加済みデバイスの場合:
- Web ブラウザーを開き、 https://&lt;&gt;/mcs/services (探索エンドポイントの外部 URL) にアクセスします。
- このエンドポイントの一連の機能を説明する JSON テキストが表示されます。
- "OS の設定-\> デバイス-\> プリンター & スキャナー" にアクセスします。
    - "クラウドプリンターの検索" リンクが表示できます。
    - リンクをクリックします。
    - [検索場所を選択してください] リンクをクリックします。
        - デバイスの場所の階層が表示されます。
    - 場所を選択して **[OK]** をクリックし、 **[検索]** ボタンをクリックしてプリンターを検索します。
    - プリンター を選択し、**デバイスの追加** ボタンをクリックします。
    - プリンターが正常にインストールされたら、お気に入りのアプリからプリンターに印刷します

>   注: "EcpPrintTest" プリンターを使用している場合は、プリントサーバーコンピューターの "C:\\Ecpprinttest\\Ecpprinttest. xps" の場所に出力ファイルがあります。
