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
ms.openlocfilehash: c756aaeb293f9e6822e979e0f305f0c4f98adf72
ms.sourcegitcommit: bfe9c5f7141f4f2343a4edf432856f07db1410aa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75352101"
---
# <a name="deploy-windows-server-hybrid-cloud-print"></a>Windows Server ハイブリッドクラウド印刷の展開

>適用先: Windows Server 2016

このトピックでは、IT 管理者向けに、Microsoft ハイブリッドクラウド印刷 (HCP) ソリューションのエンドツーエンドの展開について説明します。 このソリューションレイヤーは、プリントサーバーとして実行されている既存の Windows Server 上にあり、Azure Active Directory (Azure AD) 参加済みのデバイスと、MDM で管理されたデバイスが組織で管理されているプリンタを検出して印刷できるようにします。

## <a name="pre-requisites"></a>前提条件

このインストールを開始する前に、いくつかのサブスクリプション、サービス、およびコンピューターを取得する必要があります。 それらは次のとおりです。

- Premium サブスクリプションを Azure AD します。

  Azure の試用版サブスクリプションについては[、「azure サブスクリプションの概要](https://azure.microsoft.com/trial/get-started-active-directory/)」を参照してください。

- MDM サービス (Intune など)。

  Intune の試用版サブスクリプションについては、「 [Microsoft Intune](https://www.microsoft.com/cloud-platform/microsoft-intune) 」を参照してください。

- Active Directory を実行している Windows Server 2016 以降のコンピューター。

  Active Directory を設定する方法については、「ステップバイ[ステップ: Windows Server 2016 での Active Directory](https://blogs.technet.microsoft.com/canitpro/2017/02/22/step-by-step-setting-up-active-directory-in-windows-server-2016/)のセットアップ」を参照してください。

- プリントサーバーとして実行されている、ドメインに参加している専用の Windows Server 2016 以降のコンピューター。

- コネクタサーバーとして実行されている、ドメインに参加している専用の Windows Server 2016 以降のコンピューター。

  詳細については、「 [Azure AD アプリケーションプロキシコネクタ](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-connectors)について」を参照してください。

- プリンターを公開するための Windows 10 の Creator Creator 更新プログラムまたはそれ以降のコンピューター。

- 公開されているドメイン名。

  Azure によって作成されたドメイン*名 (onmicrosoft.com*) を使用することも、独自のドメイン名を購入することもできます。 「 [Azure Active Directory ポータルを使用したカスタムドメイン名の追加」を](https://docs.microsoft.com/azure/active-directory/fundamentals/add-custom-domain)参照してください。

## <a name="deployment-steps"></a>展開の手順

次の手順は、一般的なハイブリッドクラウドの印刷展開用です。

### <a name="step-1---install-azure-ad-connect"></a>手順 1-Azure AD Connect をインストールする

1. Azure AD 接続は Azure AD をオンプレミスの AD に同期します。 Active Directory がインストールされている Windows Server コンピューターで、簡易設定を使用して Azure AD Connect ソフトウェアをダウンロードしてインストールします。 「[簡易設定を使用した Azure AD Connect の概要」を](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-install-express)参照してください。

### <a name="step-2---install-application-proxy"></a>手順 2-アプリケーションプロキシをインストールする

1. アプリケーションプロキシを使用すると、組織のユーザーはクラウドからオンプレミスのアプリケーションにアクセスできます。 コネクタサーバーにアプリケーションプロキシをインストールします。
    - インストール手順については、 [Azure Active Directory の「チュートリアル: アプリケーションプロキシを使用したリモートアクセスのためのオンプレミスアプリケーションの追加](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-add-on-premises-application)」を参照してください。
    - 組織に複雑なネットワークトポロジがある場合は、専用のコネクタグループをお勧めします。 「[コネクタグループを使用して別のネットワークや場所にアプリケーションを発行する](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-connector-groups)」を参照してください。

### <a name="step-3---register-and-configure-applications"></a>手順 3-アプリケーションを登録して構成する

HCP サービスとの認証された通信を有効にするには、3つのアプリケーションを作成する必要があります。2つの Web アプリケーションは2つの HCP サービスを表し、1つはネイティブアプリケーションで、これらのサービスと通信します。

1. Azure portal にログインして、web アプリを登録します。
    - Azure Active Directory で、**アプリの登録** > **新規登録** にアクセスします。

    ![AAD アプリの登録1](../media/hybrid-cloud-print/AAD-AppRegistration.png)

    - アプリ名を入力します。 **[登録]** をクリックして完了します。

    ![AAD アプリの登録2](../media/hybrid-cloud-print/AAD-AppRegistration-Mopria.png)

    - Enterprise Cloud Print service についても同じ手順を繰り返します。
    - ネイティブアプリについても同じ手順を繰り返します。
    - 3つのアプリケーションが **[アプリの登録]** の下に表示されます。

    ![AAD アプリの登録3](../media/hybrid-cloud-print/AAD-AppRegistration-AllApps.png)

2. 2つの Web アプリケーションの API を公開します。
    - **[アプリの登録]** ブレードのままの状態で、探索サービスアプリをクリックし、 **[API の公開]** を選択します。次に、アプリケーション ID URI の横にある **[設定]** をクリックします。

    ![AAD は API 1 を公開します](../media/hybrid-cloud-print/AAD-AppRegistration-Mopria-ExposeAPI.png)

    - アプリケーション ID URI の既定値を変更せずに **保存** をクリックします。 この値はすぐに設定する必要があり、後で変更されます。

    ![AAD は API 2 を公開します](../media/hybrid-cloud-print/AAD-AppRegistration-Mopria-ExposeAPI-Save.png)

    - **[スコープの追加]** をクリックします。

    ![AAD は API 3 を公開します](../media/hybrid-cloud-print/AAD-AppRegistration-Mopria-ExposeAPI-AddScope.png)

    - スコープ名 を指定し、管理者とユーザーの両方に同意を許可して同意の説明を入力し、**スコープの追加** をクリックして終了します。

    ![AAD は API 4 を公開します](../media/hybrid-cloud-print/AAD-AppRegistration-Mopria-ExposeAPI-ScopeName.png)

    - Enterprise Cloud Print service についても同じ手順を繰り返します。 別のスコープ名と同意の説明を使用します。

    ![AAD は API 5 を公開します](../media/hybrid-cloud-print/AAD-AppRegistration-ECP-ExposeAPI-ScopeName.png)

3. API アクセス許可を追加する
    - アプリの登録ブレードに戻ります。 ネイティブアプリをクリックし、[API のアクセス許可] を選択します。 **[アクセス許可の追加]** をクリックします。

    ![AAD API アクセス許可1](../media/hybrid-cloud-print/AAD-AppRegistration-APIPermission.png)

    - 組織が**使用**している api に切り替え、検索ボックスを使用して、前に追加した探索サービスを検索します。 検索結果からサービスをクリックします。

    ![AAD API アクセス許可2](../media/hybrid-cloud-print/AAD-AppRegistration-APIPermission-Mopria.png)

    - [**委任**された権限] を選択します。 API のスコープの横にあるチェックボックスをオンにします。 **[アクセス許可の追加]** をクリックします。

    ![AAD API アクセス許可3](../media/hybrid-cloud-print/AAD-AppRegistration-APIPermission-Mopria-Add.png)

    - この手順を繰り返して、Enterprise Cloud Print Service にアクセス許可を追加します。

    ![AAD API アクセス許可4](../media/hybrid-cloud-print/AAD-AppRegistration-APIPermission-ECP-Add.png)

    - API のアクセス許可 ブレードに戻ったら、10秒待ってから、**全体管理者の同意** をクリックします。

    ![AAD API アクセス許可5](../media/hybrid-cloud-print/AAD-AppRegistration-APIPermission-GrantConsent.png)

    - プロンプトが表示されたら、[**はい]** をクリックします。

    ![AAD API アクセス許可6](../media/hybrid-cloud-print/AAD-AppRegistration-APIPermission-GrantConsent-Yes.png)

    - API 権限の 状態」列に緑色のチェックマークが表示されていることを確認します。

    ![AAD API アクセス許可7](../media/hybrid-cloud-print/AAD-AppRegistration-APIPermission-Verify.png)

4. Web アプリケーションのアプリケーションプロキシを構成する
    - **[すべてのアプリケーション]**  >  **[エンタープライズアプリケーション]**  > **Azure Active Directory**にアクセスします。 検出サービスを検索してクリックします。

    ![AAD アプリプロキシ1](../media/hybrid-cloud-print/AAD-EnterpriseApp-AllApps.png)

    - **[アプリケーションプロキシ]** をクリックします。 `https://<fully qualified domain name of the Print Server>/mcs/`の形式を使用して内部 Url を入力します。 **[保存]** をクリックして完了します。

    ![AAD アプリプロキシ2](../media/hybrid-cloud-print/AAD-EnterpriseApp-Mopria-AppProxy.png)

    - Enterprise Cloud Print service についても同じ手順を繰り返します。 内部 URL が `https://<fully qualified domain name of the Print Server>/ecp/`であることに注意してください。

    ![AAD アプリプロキシ3](../media/hybrid-cloud-print/AAD-EnterpriseApp-ECP-AppProxy.png)

    - **[Azure Active Directory]**  >  **[アプリの登録]** に移動します。 [検出サービス] をクリックします。 **[概要]** で、アプリケーション ID URI が既定から **[アプリケーションプロキシ]** の下の外部 URL に変更されていることを確認します。 この URI は、プリントサーバーのセットアップ、クライアント MDM ポリシー、およびプリンタの発行時に使用されます。

    ![AAD アプリプロキシ4](../media/hybrid-cloud-print/AAD-AppRegistration-Mopria-Overview.png)

5. アプリケーションへのユーザーの割り当て
    - **[すべてのアプリケーション]**  >  **[エンタープライズアプリケーション]**  > **Azure Active Directory**にアクセスします。 検出サービスを検索してクリックします
    - **[ユーザーとグループ]** をクリックしてユーザーを割り当てるか、 **[プロパティ]** をクリックして [**ユーザー割り当てが必要]** を **[いいえ]** に変更します。
    - Enterprise Cloud Print service についても同じ手順を繰り返します。

6. ネイティブアプリでリダイレクト URI を構成する
    - **[Azure Active Directory]**  >  **[アプリの登録]** に移動します。 ネイティブアプリをクリックします。 **[概要]** にアクセスし、**アプリケーション (クライアント) ID**をコピーします。

    ![AAD リダイレクト URI 1](../media/hybrid-cloud-print/AAD-AppRegistration-Native-Overview.png)

    - **[認証]** にアクセスします。 **[種類]** ドロップダウンボックスを `Public...`に変更し、次の形式を使用して2つのリダイレクト uri を入力します。ここで `<NativeClientAppID>` は前の手順からのものです。

        `ms-appx-web://Microsoft.AAD.BrokerPlugin/<NativeClientAppID>`

        `ms-appx-web://Microsoft.AAD.BrokerPlugin/S-1-15-2-3784861210-599250757-1266852909-3189164077-45880155-1246692841-283550366`

    ![AAD リダイレクト URI 2](../media/hybrid-cloud-print/AAD-AppRegistration-Native-Authentication.png)

    - **[保存]** をクリックして終了します。

### <a name="step-4---setup-the-print-server"></a>手順 4-プリントサーバーをセットアップする

1. プリントサーバーに、使用可能なすべての Windows Update がインストールされていることを確認します。 注: 17763.165 以降をビルドするには、サーバー2019にパッチを適用する必要があります。
    - 次のサーバーの役割をインストールします。
        - プリントサーバーの役割
        - インターネット インフォメーション サービス (IIS)
    - サーバーの役割のインストール方法の詳細について[は、「役割と機能の追加ウィザードを使用して役割、役割サービス、および機能をインストール](https://docs.microsoft.com/windows-server/administration/server-manager/install-or-uninstall-roles-role-services-or-features#BKMK_installarfw)する」を参照してください。

    ![プリントサーバーの役割](../media/hybrid-cloud-print/PrintServer-Roles.png)

2. ハイブリッドクラウド印刷の PowerShell モジュールをインストールします。
    - 管理者特権の PowerShell コマンドプロンプトから次のコマンドを実行します。

        コンピューターが PowerShell ギャラリーに接続できることを確認するための `find-module -Name "PublishCloudPrinter"` (PSGallery)

        `install-module -Name "PublishCloudPrinter"`

    > 注: "PSGallery" が信頼されていないリポジトリであることを示すメッセージが表示される場合があります。  インストールを続行するには、「y」と入力します。

    ![プリントサーバーのクラウドプリンターの発行](../media/hybrid-cloud-print/PrintServer-PublishCloudPrinter.png)

3. ハイブリッドクラウド印刷ソリューションをインストールします。
    - 同じ管理者特権の PowerShell コマンドプロンプトで、次のいずれかのディレクトリに移動します (引用符が必要です)。

        `"C:\Program Files\WindowsPowerShell\Modules\PublishCloudPrinter\1.0.0.0"`

    - を実行します。

        `.\CloudPrintDeploy.ps1 -AzureTenant <Azure Active Directory domain name> -AzureTenantGuid <Azure Active Directory ID>`

    - Azure Active Directory のドメイン名を確認するには、次のスクリーンショットを参照してください。

    ![プリントサーバー AAD ドメイン名を取得する方法](../media/hybrid-cloud-print/PrintServer-GetAADDomainName.png)

    - Azure Active Directory ID を確認するには、次のスクリーンショットを参照してください。

    ![プリントサーバークラウドの印刷配置](../media/hybrid-cloud-print/PrintServer-GetAADId.png)

    - CloudPrintDeploy スクリプトの出力は次のようになります。

    ![プリントサーバークラウドの印刷配置](../media/hybrid-cloud-print/PrintServer-CloudPrintDeploy.png)

    - ログファイルを調べて、エラーが発生していないかどうかを確認します。 `C:\Program Files\WindowsPowerShell\Modules\PublishCloudPrinter\1.0.0.0>notepad CloudPrintDeploy.log`

4. 管理者特権のコマンドプロンプトで RegitEdit を開きます。 コンピューター \ HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Windows\CurrentVersion\CloudPrint\EnterpriseCloudPrintService. にアクセス
    - AzureAudience がエンタープライズクラウド印刷アプリのアプリケーション ID URI に設定されていることを確認してください。
    - AzureTenant が Azure AD ドメイン名に設定されていることを確認します。

    ![プリントサーバーの ECP レジストリキー](../media/hybrid-cloud-print/PrintServer-RegEdit-ECP.png)

5. コンピューター \ HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Windows\CurrentVersion\CloudPrint\MopriaDiscoveryService. にアクセス
    - AzureAudience が探索サービスアプリのアプリケーション ID URI であることを確認してください。
    - AzureTenant が Azure AD ドメイン名であることを確認してください。
    - URL が、探索サービスアプリのアプリケーション ID URI であることを確認します。

    ![プリントサーバーのレジストリキー](../media/hybrid-cloud-print/PrintServer-RegEdit-Mopria.png)

6. Powershell の昇格コマンドプロンプトで**iisreset**を実行します。 これにより、前の手順で行われたレジストリの変更が有効になります。

7. SSL をサポートするように IIS エンドポイントを構成します。
    - SSL 証明書には、自己署名証明書、または信頼された証明機関 (CA) から発行された証明書を使用できます。
    - 自己署名証明書を使用する場合は、**証明書がクライアントコンピューターにインポートされていることを確認**します。
    - サードパーティプロバイダーにドメインを登録する場合は、SSL 証明書を使用して IIS エンドポイントを構成する必要があります。 詳細については、この[ガイド](https://www.sslsupportdesk.com/microsoft-server-2016-iis-10-10-5-ssl-installation/)を参照してください。

8. SQLite パッケージをインストールします。
   - 管理者特権の PowerShell コマンド プロンプトを開きます。
   - 次のコマンドを実行して、システムのデータをダウンロードします。

        `Register-PackageSource -Name nuget.org -ProviderName NuGet -Location https://www.nuget.org/api/v2/ -Trusted -Force`

   - 次のコマンドを実行して、パッケージをインストールします。

        `Install-Package system.data.sqlite [-requiredversion x.x.x.x] -providername nuget`

   > 注: "-requiredversion" オプションを残して、最新バージョンをダウンロードしてインストールすることをお勧めします。

    ![プリントサーバーのレジストリキー](../media/hybrid-cloud-print/PrintServer-InstallSQLite.png)

9. SQLite dll を MopriaCloudService Webapp bin フォルダー (C:\inetpub\wwwroot\MopriaCloudService\bin) にコピーします。
    - 次の PowerShell スクリプトを含む ps1 ファイルを作成します。
    - $Version 変数を、前の手順でインストールした SQLite のバージョンに変更します。
    - 管理者特権の PowerShell コマンドプロンプトで、ps1 ファイルを実行します。

    ```powershell
    $source = "\Program Files\PackageManagement\NuGet\Packages"
    $core = "System.Data.SQLite.Core"
    $linq = "System.Data.SQLite.Linq"
    $ef6 = "System.Data.SQLite.EF6"
    $version = "x.x.x.x"
    $target = "C:\inetpub\wwwroot\MopriaCloudService\bin"

    xcopy /y "$source\$core.$version\lib\net46\System.Data.SQLite.dll" "$target\"
    xcopy /y "$source\$core.$version\build\net46\x86\SQLite.Interop.dll" "$target\x86\"
    xcopy /y "$source\$core.$version\build\net46\x64\SQLite.Interop.dll" "$target\x64\"
    xcopy /y "$source\$linq.$version\lib\net46\System.Data.SQLite.Linq.dll" "$target\"
    xcopy /y "$source\$ef6.$version\lib\net46\System.Data.SQLite.EF6.dll" "$target\"
    ```

10. 次の `<runtime>/<assemblyBinding>` セクションで、c:\inetpub\wwwroot\MopriaCloudService\web.config ファイルを更新して SQLite バージョン2.x を含むようにします。 これは、前の手順で使用したバージョンと同じです。

    ```xml
    ...
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
    ...
    ```

11. SQLite データベースを作成します。
    - `https://www.sqlite.org/`から SQLite ツールバイナリをダウンロードしてインストールします。
    - `c:\inetpub\wwwroot\MopriaCloudService\Database` ディレクトリにアクセスします。
    - 次のコマンドを実行して、このディレクトリにデータベースを作成します。

        `sqlite3.exe MopriaDeviceDb.db ".read MopriaSQLiteDb.sql"`

    - ファイルエクスプローラーで、Mo先読み Adevicedb. db ファイルのプロパティを開き、[セキュリティ] タブで Mo先読みデータベースへの発行が許可されているユーザーまたはグループを追加します。ユーザーまたはグループは、オンプレミスの Active Directory に存在し、Azure AD と同期されている必要があります。
    - ソリューションがルーティング不可能なドメイン (例: *mydomain*) にデプロイされている場合は、Azure AD ドメイン (例: onmicrosoft.com、またはサードパーティベンダーから*購入した*ドメイン) を、オンプレミスの Active Directory に UPN サフィックスとして追加する必要があります。 これは、プリンターを発行するのとまったく同じユーザー (例 admin@: onmicrosoft.com) をデータベースファイルのセキュリティ設定に追加できるようにする*ためです。* 「[ディレクトリ同期のためにルーティング不可能なドメインを準備する」を](https://docs.microsoft.com/office365/enterprise/prepare-a-non-routable-domain-for-directory-synchronization)参照してください。

    ![プリントサーバーのレジストリキー](../media/hybrid-cloud-print/PrintServer-SQLiteDB.png)

### <a name="step-5-optional---configure-pre-authentication-with-azure-ad"></a>手順 5 \[オプションの\]-Azure AD を使用した事前認証を構成する

1. [アプリケーションプロキシを使用したアプリへのシングルサインオンに関するドキュメント「Kerberos の制約付き委任](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-configure-single-sign-on-with-kcd)」を確認します。

2. オンプレミスの Active Directory を構成します。
    - Active Directory マシンでサーバーマネージャーを開き、 **[ツール]** **[Active Directory ユーザーとコンピューター]** の > にアクセスします。
    - **[コンピューター]** ノードに移動し、コネクタサーバーを選択します。
    - 右クリックし、 **プロパティ** -> **委任**  タブを選択します。
    - [ **指定されたサービスへの委任でのみこのコンピューターを信頼する**] を選択します。
    - [ **任意の認証プロトコルを使用する**] を選択します。
    - [ **このアカウントが委任された資格情報を提示できるサービス**] の下。
        - プリントサーバーコンピューターのサービスプリンシパル名 (SPN) を追加します。
        - サービスの種類として [ホスト] を選択します。
    ![Active Directory 委任](../media/hybrid-cloud-print/AD-Delegation.png)

3. IIS で Windows 認証が有効になっていることを確認します。
    - プリントサーバーでサーバーマネージャー > ツール > インターネットインフォメーションサービス (IIS) マネージャーを開きます。
    - サイトに移動します。
    - **[認証]** をダブルクリックします。
    - **[Windows 認証]** をクリックし、 **[アクション]** で **[有効]** をクリックします。
    プリントサーバー IIS 認証の ![](../media/hybrid-cloud-print/PrintServer-IIS-Authentication.png)

4. シングルサインオンを構成します。
    - Azure portal で、[**すべてのアプリケーション** >  > **エンタープライズアプリケーション**] **Azure Active Directory**にアクセスします。
    - [Mo先読み Adiscoveryservice アプリ] を選択します。
    - **アプリケーションプロキシ**にアクセスします。 事前認証方法を**Azure Active Directory**に変更します。
    - **[Single sign-on]\(シングル サインオン\)** に移動します。 シングルサインオンの方法として [統合 Windows 認証] を選択します。
    - **内部アプリケーション spn**をプリントサーバーコンピューターの spn に設定します。
    - [委任された**ログイン id** ] を "ユーザープリンシパル名" に設定します。
    - EntperiseCloudPrint アプリに対して繰り返します。
    AAD シングルサインオンの ![IWA](../media/hybrid-cloud-print/AAD-SingleSignOn-IWA.png)

### <a name="step-6---configure-the-required-mdm-policies"></a>手順 6-必要な MDM ポリシーを構成する

1. MDM プロバイダーにログインします。
2. 次のガイドラインに従って、エンタープライズクラウドの印刷ポリシーグループを見つけ、ポリシーを構成します。
    - CloudPrintOAuthAuthority = `https://login.microsoftonline.com/<Azure AD Directory ID>`。 ディレクトリ ID は Azure Active Directory > のプロパティ にあります。
    - CloudPrintOAuthClientId = "Application \(client\) ID" ネイティブアプリの値。 これは Azure Active Directory > > アプリの登録の下で確認できます。 [ネイティブアプリ > 概要] を選択します。
    - Cloudプリンター Discoveryendpoint = 検索サービスアプリの外部 URL。 これは、[Azure Active Directory > エンタープライズアプリケーション] の下で確認できます。アプリプロキシ > アプリケーションプロキシを選択 > ます。 **正確に一致している必要がありますが、末尾に "/" を**指定することはできません。
    - Mo先読み Adiscoveryresourceid = アプリのアプリケーション ID の URI です。 これは、[Azure Active Directory > アプリの登録] の下にあり > [探索サービスアプリの概要] > 選択します。 **これは、末尾の "/" とまったく同じである必要があり**ます。
    - CloudPrintResourceId = エンタープライズクラウド印刷アプリのアプリケーション ID URI。 これは Azure Active Directory > > アプリの登録の下にあります。 [エンタープライズクラウド印刷アプリ > 概要] を選択します。 **これは、末尾の "/" とまったく同じである必要があり**ます。
    - Discoverymaxプリンター Limit = \<正の整数\>です。

> 注: Microsoft Intune サービスを使用している場合は、[Cloud Printer] (クラウドプリンター) カテゴリの下にこれらの設定が表示されます。

|Intune の表示名                     |のポリシー                         |
|----------------------------------------|-------------------------------|
|プリンター検出 URL                   |Cloudプリンター Discoveryendpoint  |
|プリンターアクセス機関の URL            |CloudPrintOAuthAuthority       |
|Azure Native client アプリ GUID            |CloudPrintOAuthClientId        |
|印刷サービスのリソース URI              |CloudPrintResourceId           |
|クエリする最大プリンター (モバイルのみ)  |Discoverymaxプリンターの制限       |
|プリンター検出サービスのリソース URI  |Mo先読み Adiscoveryresourceid      |

> 注: [クラウド印刷ポリシー] グループが使用できないが、MDM プロバイダーが OMA-URI 設定をサポートしている場合は、同じポリシーを設定できます。  詳細については、[こちらを参照](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-enterprisecloudprint#enterprisecloudprint-cloudprintoauthauthority)してください。

    - OMA-URI の値
        - CloudPrintOAuthAuthority =./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/CloudPrintOAuthAuthority
            - 値 = https://login.microsoftonline.com/<Azure AD Directory ID>
        - CloudPrintOAuthClientId =./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/CloudPrintOAuthClientId
            - 値 = < Azure AD ネイティブアプリのアプリケーション ID >
        - Cloudプリンター Discoveryendpoint =./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/CloudPrinterDiscoveryEndPoint
            - 値 = 検索サービスアプリの外部 URL (完全に一致している必要がありますが、末尾に "/" が含まれていない必要があります)
        - Mo/Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/MopriaDiscoveryResourceId Adiscoveryresourceid =.
            - 値 = 検出サービスアプリのアプリケーション ID の URI
        - CloudPrintResourceId =./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/CloudPrintResourceId
            - 値 = エンタープライズクラウド印刷アプリのアプリケーション ID URI
        - Discoverymaxプリンター Limit =/Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/DiscoveryMaxPrinterLimit
            - 値 = 正の整数
    
### <a name="step-7---publish-the-shared-printer"></a>手順 7-共有プリンターを公開する

1. 必要なプリンターをプリントサーバーにインストールします。
2. プリンターのプロパティ UI を使用してプリンターを共有します。
3. アクセス権を付与するユーザーのセットを選択します。
4. 変更を保存し、[プリンターのプロパティ] ウィンドウを閉じます。
5. Windows 10 フォール Creator 更新プログラムまたはそれ以降のコンピューターを準備します。 コンピューターを Azure AD に参加させ、オンプレミスの Active Directory と同期しているユーザーとしてログインします。また、Mo先読み Adevicedb. db ファイルに対する適切なアクセス許可が付与されています。
6. Windows 10 コンピューターから、管理者特権で Windows PowerShell コマンドプロンプトを開きます。
    - 次のコマンドを実行します。
        - コンピューターが PowerShell ギャラリーに接続できることを確認するための `find-module -Name "PublishCloudPrinter"` (PSGallery)
        - `install-module -Name "PublishCloudPrinter"`

            > 注: "PSGallery" が信頼されていないリポジトリであることを示すメッセージが表示される場合があります。  インストールを続行するには、「y」と入力します。

        - `Publish-CloudPrinter`
        - Printer = 共有プリンターの名前。 この名前は、プリントサーバーで開かれている、プリンターのプロパティの **[共有]** タブに表示されている共有名と正確に一致する必要があります。

        ![プリントサーバープリンターのプロパティ](../media/hybrid-cloud-print/PrintServer-PrinterProperties.png)

        - 製造元 = プリンターの製造元。
        - モデル = プリンターモデル。
        - OrgLocation = プリンターの場所を指定する JSON 文字列 (例:

            `{"attrs": [{"category":"country", "vs":"USA", "depth":0}, {"category":"organization", "vs":"Microsoft", "depth":1}, {"category":"site", "vs":"Redmond, WA", "depth":2}, {"category":"building", "vs":"Building 1", "depth":3}, {"category":"floor_number", "vs":1, "depth":4}, {"category":"room_name", "vs":"1111", "depth":5}]}`

        - Sddl = プリンターのアクセス許可を表す SDDL 文字列。
            - プリントサーバーに管理者としてログオンし、発行するプリンタに対して次の PowerShell コマンドを実行します。 `(Get-Printer PrinterName -full).PermissionSDDL`。
            - 上記のコマンドの結果に、プレフィックスとして**O: BA**を追加します。 例: 前のコマンドによって返された文字列が "G: DUD: (A; OICI; FA;;;WD) "、SDDL =" O: BAG: DUD: (A; O:BAG; FA;;;WD) "。
        - DiscoveryEndpoint = Azure portal にログインしてから、エンタープライズアプリケーション > 検索サービスアプリ > アプリケーションプロキシ > 外部 URL の文字列を取得します。 末尾の "/" を省略します。
        - PrintServerEndpoint = Azure portal にログインし、エンタープライズアプリケーション > エンタープライズクラウド印刷アプリ > アプリケーションプロキシ > 外部 URL の文字列を取得します。 末尾の "/" を省略します。
        - AzureClientId = 登録されているネイティブアプリケーションのアプリケーション ID。
        - AzureTenantGuid = Azure AD テナントのディレクトリ ID。
        - DiscoveryResourceId = アプリケーション ID URI は、検出サービスアプリケーションの URI です。

    - 必要なすべてのパラメーター値をコマンドラインに入力することもできます。 構文は次のとおりです。

        `Publish-CloudPrinter -Printer <string> -Manufacturer <string> -Model <string> -OrgLocation <string> -Sddl <string> -DiscoveryEndpoint <string> -PrintServerEndpoint <string> -AzureClientId <string> -AzureTenantGuid <string> -DiscoveryResourceId <string>`

        サンプル コマンド:

        `Publish-CloudPrinter -Printer HcpTestPrinter -Manufacturer Manufacturer1 -Model Model1 -OrgLocation '{"attrs": [{"category":"country", "vs":"USA", "depth":0}, {"category":"organization", "vs":"MyCompany", "depth":1}, {"category":"site", "vs":"MyCity, State", "depth":2}, {"category":"building", "vs":"Building 1", "depth":3}, {"category":"floor_name", "vs":1, "depth":4}, {"category":"room_name", "vs":"1111", "depth":5}]}' -Sddl "O:BAG:DUD:(A;OICI;FA;;;WD)" -DiscoveryEndpoint "https://mopriadiscoveryservice-contoso.msappproxy.net/mcs" -PrintServerEndpoint "https://enterprisecloudprint-contoso.msappproxy.net/ecp" -AzureClientId "dbe4feeb-cb69-40fc-91aa-73272f6d8fe1" -AzureTenantGuid "8de6a14a-5a23-4c1c-9ae4-1481ce356034" -DiscoveryResourceId "https://mopriadiscoveryservice-contoso.msappproxy.net/mcs/"`

    - 次のコマンドを使用して、プリンターが発行されていることを確認します。

        `Publish-CloudPrinter -Query -DiscoveryEndpoint <string> -AzureClientId <string> -AzureTenantGuid <string> -DiscoveryResourceId <string>`

        サンプル コマンド:

        `Publish-CloudPrinter -Query -DiscoveryEndpoint "https://mopriadiscoveryservice-contoso.msappproxy.net/mcs" -AzureClientId "dbe4feeb-cb69-40fc-91aa-73272f6d8fe1" -AzureTenantGuid "8de6a14a-5a23-4c1c-9ae4-1481ce356034" -DiscoveryResourceId "https://mopriadiscoveryservice-contoso.msappproxy.net/mcs/"`

## <a name="verify-the-deployment"></a>展開を確認する

MDM ポリシーが構成されている Azure AD 参加済みデバイスの場合:
- Web ブラウザーを開き *、 https://mopriadiscoveryservice- msappproxy.net/mcs/services*にアクセスします。
- このエンドポイントの一連の機能を説明する JSON テキストが表示されます。
- **[設定]** **[デバイス]**  > [**プリンター] & [スキャナー**] の > にアクセスします。
    - **[プリンターまたはスキャナーの追加]** をクリックします。
    - "クラウドプリンターの検索" (または、[組織内のプリンターを検索する]) リンクが表示されます。
    - リンクをクリックします。
    - [検索場所を選択してください] リンクをクリックします。
        - デバイスの場所の階層が表示されます。
    - 場所を選択して **[OK]** をクリックし、 **[検索]** ボタンをクリックしてプリンターを検索します。
    - プリンター を選択し、**デバイスの追加** ボタンをクリックします。
    - プリンターが正常にインストールされたら、お気に入りのアプリからプリンターに印刷します。

> 注: "EcpPrintTest" プリンターを使用している場合は、プリントサーバーコンピューターの "C:\\Ecpprinttest\\Ecpprinttest. xps" の場所に出力ファイルがあります。

## <a name="troubleshooting"></a>[トラブルシューティング]

エラーのトラブルシューティングに役立つさまざまなログがあります。
- Windows 10 クライアントの場合。
    - フィードバックハブを使用して、新しいフィードバックを追加します。
        - **[スタート]** をクリックし、「フィードバックハブ」と入力します。
        - [カテゴリ] で、[**問題**、**デバイス、ドライバー**、**印刷**] を選択します。
        - 詳細を追加するセクションで、 **[記録の開始]** ボタンをクリックします。
        - 失敗した印刷ジョブを再試行します。
        - フィードバックハブに戻り、 **[記録の停止]** ボタンをクリックします。
        - **[送信]** をクリックしてフィードバックを送信します。
    - Azure AD 操作のログを表示するには、イベントビューアーを使用します。 **[スタート]** をクリックし、「イベントビューアー」と入力します。 Microsoft > Windows > AAD > 操作 > [アプリケーションとサービスログ] に移動します。
- コネクタサーバー。
    - アプリケーションプロキシのログを表示するには、イベントビューアーを使用します。 **[スタート]** をクリックし、「イベントビューアー」と入力します。 アプリケーションとサービスログ > Microsoft > AadApplicationProxy > Connector > Admin に移動します。
- プリントサーバー上。
    - 探索サービスアプリとエンタープライズクラウド印刷アプリのログは、C:\inetpub\logs\LogFiles\W3SVC1. にあります。