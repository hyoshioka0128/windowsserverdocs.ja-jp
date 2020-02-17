---
title: ユーザー用にリモート デスクトップ Web クライアントをセットアップする
description: 管理者がどのようにしてリモート デスクトップ Web クライアントをセットアップできるかについて説明します。
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 09/19/2019
ms.topic: article
author: Heidilohr
ms.localizationpriority: medium
ms.openlocfilehash: a8521eae302ade84904e3ba09c001eac21fffd6a
ms.sourcegitcommit: f0fcfee992b76f1ad5dad460d4557f06ee425083
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/11/2020
ms.locfileid: "77125153"
---
# <a name="set-up-the-remote-desktop-web-client-for-your-users"></a>ユーザー用にリモート デスクトップ Web クライアントをセットアップする

リモート デスクトップ Web クライアントにより、ユーザーは互換性のある Web ブラウザーを通して、組織のリモート デスクトップ インフラストラクチャにアクセスできます。 どこにいても、ローカル PC 使用時のようにリモート アプリやデスクトップを操作できるようになります。 リモート デスクトップ Web クライアントをセットアップしたら、ユーザーが利用し始めるために必要なのは、クライアント、自分の資格情報、およびサポートされている Web ブラウザーにアクセスできる URL だけです。

>[!IMPORTANT]
>Web クライアントは現在、Azure アプリケーション プロキシの使用をサポートしておらず、Web アプリケーション プロキシはまったくサポートされません。 詳細については、[アプリケーション プロキシ サービスと共に RDS を使用すること](../rds-supported-config.md#using-remote-desktop-services-with-application-proxy-services)に関するページを参照してください。

## <a name="what-youll-need-to-set-up-the-web-client"></a>Web クライアントをセットアップするために必要なこと

開始する前に、以下のことに留意してください。

* [リモート デスクトップの展開](../rds-deploy-infrastructure.md)に、RD ゲートウェイ、RD 接続ブローカー、Windows Server 2016 または 2019 で実行されている RD Web アクセスが含まれることを確認します。
* デバイスごとではなく、[ユーザーごとのクライアント アクセス ライセンス](../rds-client-access-license.md) (CAL) で配置が構成されていることを確認します。そうでないと、すべてのライセンスが消費されます。
* RD ゲートウェイに [Windows 10 の KB4025334 更新プログラム](https://support.microsoft.com/help/4025334/windows-10-update-kb4025334)をインストールします。 後の累積的な更新プログラムに、この KB が含まれている可能性があります。
* RD ゲートウェイの役割と RD Web アクセスの役割のために信頼できるパブリック証明書が構成されていることを確認します。
* ユーザーが接続するどのコンピューターでも、以下の OS バージョンのいずれかが実行されていることを確認します。
  * Windows 10
  * Windows Server 2008R2 以降

ユーザーは Windows Server 2016 (またはそれ以降) や Windows 10 (バージョン 1611 またはそれ以降) への接続ではパフォーマンスがより高いことに気付きます。

>[!IMPORTANT]
>プレビュー期間中に Web クライアントを使用し、1.0.0 より前のバージョンをインストールした場合は、まず古いクライアントをアンインストールしてから新しいバージョンに移行する必要があります。 "The web client was installed using an older version of RDWebClientManagement and must first be removed before deploying the new version" (古いバージョンの RDWebClientManagement を使用して Web クライアントがインストールされたため、まずそれを削除してから新しいバージョンを展開する必要があります) というエラーが発生した場合は、次の手順に従います。
>
>1. 管理者特権の PowerShell プロンプトを開きます。
>2. **Uninstall-Module RDWebClientManagement** を実行して新しいモジュールをアンインストールします。
>3. PowerShell プロンプトを閉じ、管理者特権で再度開きます。
>4. **Install-Module RDWebClientManagement -RequiredVersion \<古いバージョン> を実行して古いモジュールをインストールします。**
>5. **Uninstall-RDWebClient** を実行して古い Web クライアントをアンインストールします。
>6. **Uninstall-Module RDWebClientManagement** を実行して古いモジュールをアンインストールします。
>7. PowerShell プロンプトを閉じ、管理者特権で再度開きます。
>8. 以下のように通常のインストールの手順に進みます。

## <a name="how-to-publish-the-remote-desktop-web-client"></a>リモート デスクトップ Web クライアントを発行する方法

初めて Web クライアントをインストールするには、以下の次の手順に従います。

1. RD 接続ブローカー サーバーで、リモート デスクトップ接続に使用する証明書を取得し、.cer ファイルとしてエクスポートします。 RD 接続ブローカーから、RD Web の役割を実行するサーバーに .cer ファイルをコピーします。
2. RD Web アクセス サーバーで、管理者特権の PowerShell プロンプトを開きます。
3. Windows Server 2016 では、受信トレイのバージョンが Web クライアント管理モジュールのインストールをサポートしていないため、PowerShellGet モジュールを更新します。 PowerShellGet を更新するには、次のコマンドレットを実行します。
    ```PowerShell
    Install-Module -Name PowerShellGet -Force
    ```

    >[!IMPORTANT]
    >更新プログラムを有効にするには、PowerShell を再起動する必要があります。そうしないと、モジュールが動作しない可能性があります。

4. 次のコマンドレットで、リモート デスクトップの Web クライアント管理 PowerShell モジュールを PowerShell ギャラリーからインストールします。
    ```PowerShell
    Install-Module -Name RDWebClientManagement
    ```

5. その後、次のコマンドレットを実行し、最新バージョンのリモート デスクトップ Web クライアントをダウンロードします。
    ```PowerShell
    Install-RDWebClientPackage
    ```

6. 次に、かっこに囲まれた値を、RD ブローカーからコピーした .cer ファイルのパスに置き換えて、このコマンドレットを実行します。
    ```PowerShell
    Import-RDWebClientBrokerCert <.cer file path>
    ```

7. 最後に、このコマンドレットを実行してリモート デスクトップ Web クライアントを発行します。
    ```PowerShell
    Publish-RDWebClientPackage -Type Production -Latest
    ```
    <https://server_FQDN/RDWeb/webclient/index.html> の形式でサーバー名を指定して、Web クライアント URL にある Web クライアントにアクセスできることを確認します。 URL (通常はサーバーの FQDN) 内の RD Web アクセスのパブリック証明書に一致するサーバー名を使用することが重要です。

    >[!NOTE]
    >**Publish-RDWebClientPackage** コマンドレットの実行時に、展開がユーザー単位の CAL に構成されている場合でも、デバイス単位の CAL はサポートされていないという警告が表示される可能性があります。 展開でユーザー単位の CAL を使用している場合は、この警告を無視できます。 これが表示されるのは、ユーザーが構成の制限について知っていることを確認するためです。
8. ユーザーに Web クライアントにアクセスさせる準備ができたら、作成した Web クライアントの URL を送信します。

>[!NOTE]
>RDWebClientManagement モジュールでサポートされているすべてのコマンドレットの一覧を表示するには、PowerShell で次のコマンドレットを実行します。
>```PowerShell
>Get-Command -Module RDWebClientManagement
>```

## <a name="how-to-update-the-remote-desktop-web-client"></a>リモート デスクトップ Web クライアントを更新する方法

新しいバージョンのリモート デスクトップ Web クライアントが利用できる場合は、以下の手順に従って、新しいクライアントで展開を更新します。

1. RD Web アクセス サーバーで、管理者特権の PowerShell プロンプトを開き、次のコマンドレットを実行して、入手できる最新バージョンの Web クライアントをダウンロードします。
    ```PowerShell
    Install-RDWebClientPackage
    ```

2. 必要に応じて、次のコマンドレットを実行して、公式リリース前にテスト用のクライアントを発行できます。
    ```PowerShell
    Publish-RDWebClientPackage -Type Test -Latest
    ```

    クライアントは、Web クライアント URL (たとえば <https://server_FQDN/RDWeb/webclient-test/index.html>) に対応するテスト URL に表示される必要があります。
3. 次のコマンドレットを実行して、ユーザーのためにクライアントを発行します。
    ```PowerShell
    Publish-RDWebClientPackage -Type Production -Latest
    ```

    これで、ユーザーが Web ページを再度開くときに、すべてのユーザーのクライアントが置き換えられます。

## <a name="how-to-uninstall-the-remote-desktop-web-client"></a>リモート デスクトップ Web クライアントをアンインストールする方法

Web クライアントのすべてのトレースを削除するには、以下の手順に従います。

1. RD Web アクセス サーバーで、管理者特権の PowerShell プロンプトを開きます。
2. テストと運用クライアントの発行を解除し、すべてのローカル パッケージをアンインストールし、Web クライアントの設定を削除します。

   ```PowerShell
   Uninstall-RDWebClient
   ```

3. リモート デスクトップ Web クライアントの管理 PowerShell モジュールをアンインストールします。

   ```PowerShell
   Uninstall-Module -Name RDWebClientManagement
   ```

## <a name="how-to-install-the-remote-desktop-web-client-without-an-internet-connection"></a>インターネット接続なしでリモート デスクトップ Web クライアントをインストールする方法

インターネット接続がない RD Web アクセス サーバーに Web クライアントを展開するには、以下の手順に従います。

> [!NOTE]
> インターネット接続なしのインストールは、RDWebClientManagement PowerShell モジュールのバージョン 1.0.1 以上で使用できます。

> [!NOTE]
> その場合でも、オフライン サーバーに転送する前に必要なファイルをダウンロードするために、インターネットにアクセスできる管理者 PC が必要です。

> [!NOTE]
> 現在のところ、エンド ユーザーの PC にはインターネット接続が必要です。 これは、完全なオフライン シナリオを提供する将来のリリースのクライアントで対処されます。

### <a name="from-a-device-with-internet-access"></a>インターネット アクセスのあるデバイスから

1. PowerShell プロンプトを開きます。

2. リモート デスクトップの Web クライアント管理 PowerShell モジュールを PowerShell ギャラリーからインポートします。
    ```PowerShell
    Import-Module -Name RDWebClientManagement
    ```

3. 別のデバイスへのインストール用の、最新バージョンのリモート デスクトップ Web クライアントをダウンロードします。
    ```PowerShell
    Save-RDWebClientPackage "C:\WebClient\"
    ```

4. 最新バージョンの RDWebClientManagement PowerShell モジュールをダウンロードします。
    ```PowerShell
    Find-Module -Name "RDWebClientManagement" -Repository "PSGallery" | Save-Module -Path "C:\WebClient\"
    ```

5. "C:\WebClient\" の内容を RD Web アクセス サーバーにコピーします。

### <a name="from-the-rd-web-access-server"></a>RD Web アクセス サーバーから

「[リモート デスクトップ Web クライアントを発行する方法](remote-desktop-web-client-admin.md#how-to-publish-the-remote-desktop-web-client)」の説明に従い、手順 4. および 5. を以下に置き換えます。

4. 最新の Web クライアント管理 PowerShell モジュールを取得するには、次の 2 つのオプションがあります。
    - リモート デスクトップ Web クライアントの管理 PowerShell モジュールをインポートします。
      ```PowerShell
      Import-Module -Name RDWebClientManagement
      ```
    - ダウンロードした RDWebClientManagement フォルダーを **$env:psmodulePath** に一覧表示されているローカルの PowerShell モジュールフォルダーのいずれかにコピーするか、ダウンロードしたファイルを含むフォルダーへのパスを **$env:psmodulePath** に追加します。

5. ローカル フォルダーから最新バージョンのリモート デスクトップ Web クライアントを展開します (適切な zip ファイルに置き換えてください)。
    ```PowerShell
    Install-RDWebClientPackage -Source "C:\WebClient\rdwebclient-1.0.1.zip"
    ```

## <a name="connecting-to-rd-broker-without-rd-gateway-in-windows-server-2019"></a>Windows server 2019 の RD ゲートウェイのない RD ブローカーへの接続
このセクションでは、Windows Server 2019 の RD ゲートウェイのない RD ブローカーへの Web クライアント接続を有効にする方法について説明します。

### <a name="setting-up-the-rd-broker-server"></a>RD ブローカー サーバーをセットアップする

#### <a name="follow-these-steps-if-there-is-no-certificate-bound-to-the-rd-broker-server"></a>RD ブローカー サーバーにバインドされた証明書がない場合は、以下の手順に従います。

1. **[サーバー マネージャー]**  >  **[リモート デスクトップ サービス]** の順に開きます。

2. **[展開の概要]** セクションで、 **[タスク]** ドロップダウン メニューを選択します。

3. **[Edit Deployment Properties] (展開プロパティの編集)** を選択すると、 **[展開プロパティ]** というタイトルの新しいウィンドウが開きます。

4. **[展開プロパティ]** ウィンドウで、左側のメニューの **[証明書]** を選択します。

5. [証明書レベル] の一覧で、 **[RD 接続ブローカー - シングル サインオンを有効にする]** を選択します。 2 つのオプションがあります。(1) 新しい証明書の作成、または (2) 既存の証明書です。

#### <a name="follow-these-steps-if-there-is-a-certificate-previously-bound-to-the-rd-broker-server"></a>RD ブローカー サーバーに以前にバインドされた証明書がない場合は、以下の手順に従います。

1. ブローカーにバインドされている証明書を開き、**拇印**値をコピーします。

2. この証明書をセキュリティで保護されたポート 3392 にバインドするには、管理者特権の PowerShell ウィンドウを開き、 **"< thumbprint >"** を、前の手順でコピーした値に置き換えます。

    ```PowerShell
    netsh http add sslcert ipport=0.0.0.0:3392 certhash="<thumbprint>" certstorename="Remote Desktop" appid="{00000000-0000-0000-0000-000000000000}"
    ```

    > [!NOTE]
    > 証明書が正しくバインドされたかどうかを確認するには、次のコマンドを実行します。
    >
    > ```PowerShell
    > netsh http show sslcert
    > ```
    >
    > [SSL 証明書のバインド] の一覧で、ポート 3392 に正しい証明書がバインドされていることを確認します。

3. Windows レジストリ (regedit) を開き、```HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp``` に移動して、キー **WebSocketURI** を見つけます。 値は <strong>https://+:3392/rdp/</strong> に設定されている必要があります。

### <a name="setting-up-the-rd-session-host"></a>RD セッション ホストのセットアップ
RD セッション ホスト サーバーが RD ブローカー サーバーとは異なる場合は、以下の手順に従います。

1. RD セッション ホスト コンピューターの証明書を作成し、それを開きいて**拇印**値をコピーします。

2. この証明書をセキュリティで保護されたポート 3392 にバインドするには、管理者特権の PowerShell ウィンドウを開き、 **"< thumbprint >"** を、前の手順でコピーした値に置き換えます。

    ```PowerShell
    netsh http add sslcert ipport=0.0.0.0:3392 certhash="<thumbprint>" appid="{00000000-0000-0000-0000-000000000000}"
    ```

    > [!NOTE]
    > 証明書が正しくバインドされたかどうかを確認するには、次のコマンドを実行します。
    >
    > ```PowerShell
    > netsh http show sslcert
    > ```
    >
    > [SSL 証明書のバインド] の一覧で、ポート 3392 に正しい証明書がバインドされていることを確認します。

3. Windows レジストリ (regedit) を開き、```HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp``` に移動して、キー **WebSocketURI** を見つけます。 値は <https://+:3392/rdp/> に設定されている必要があります。

### <a name="general-observations"></a>一般的情報

* RD セッション ホストおよび RD ブローカーの両方のサーバーが Windows Server 2019 を実行していることを確認します。

* RD セッション ホストおよび RD ブローカーの両方のサーバーに対して、信頼できるパブリック証明書が構成されていることを確認します。
    > [!NOTE]
    > RD セッション ホストおよび RD ブローカーの両方のサーバーが同じコンピューターを共有している場合は、RD ブローカー サーバーの証明書のみを設定します。 RD セッション ホストおよび RD ブローカーのサーバーが異なるコンピューターを使用している場合は、両方が一意の証明書を使用して構成されている必要があります。

* 各証明書の**サブジェクト代替名 (SAN)** は、コンピューターの**完全修飾ドメイン名 (FQDN)** に設定する必要があります。 **共通名 (CN)** が各証明書の SAN に一致している必要があります。

## <a name="how-to-pre-configure-settings-for-remote-desktop-web-client-users"></a>リモート デスクトップ Web クライアント ユーザーの設定を事前に構成する方法
このセクションでは、PowerShell を使用して、リモート デスクトップ Web クライアントの展開の設定を構成する方法を説明します。 これらの PowerShell コマンドレットは、組織のセキュリティ上の懸念や目的のワークフローに基づいて設定を変更するユーザーの能力を制御します。 以下の設定はすべて、Web クライアントの **[設定]** サイド パネルにあります。

### <a name="suppress-telemetry"></a>製品利用統計情報を抑制する
既定では、ユーザーは Microsoft に送信される製品利用統計情報データの収集を有効または無効にできます。 Microsoft が収集する製品利用統計情報データについては、 **[バージョン情報]** サイド パネルのリンクからプライバシーに関する声明を参照してください。

管理者は、次の PowerShell コマンドレットを使用して、展開での製品利用統計情報の収集を抑制できます。

   ```PowerShell
    Set-RDWebClientDeploymentSetting -Name "SuppressTelemetry" $true
   ```

既定では、製品利用統計情報を有効にするか無効にするかをユーザーが選択できます。 ブール値 **$false** は、既定のクライアント動作と一致します。 ブール値 **$true** は製品利用統計情報を無効にし、ユーザーがこれを有効にすることを制限します。

### <a name="remote-resource-launch-method"></a>リモート リソースの起動方法

>[!NOTE]
>現在、この設定が機能するのは RDS Web クライアントのみであり、Windows 仮想デスクトップ Web クライアントでは機能しません。

既定では、ユーザーはリモート リソースの起動を、(1) ブラウザーで行うか、(2) .rdp ファイルをダウンロードし、コンピューターにインストールされている他のクライアントで処理するかを選択できます。 管理者は、以下の PowerShell コマンドを使用して、展開でのリモート リソースの起動方法を制限できます。

   ```PowerShell
    Set-RDWebClientDeploymentSetting -Name "LaunchResourceInBrowser" ($true|$false)
   ```
 既定では、ユーザーは、いずれかの起動方法を選択できます。 ブール値 **$true** では、ユーザーはブラウザー内でリソースを起動します。 ブール値 **$false** では、.rdp ファイルをダウンロードし、ローカルにインストールされた RDP クライアントで処理することで、リソースを起動します。

### <a name="reset-rdwebclientdeploymentsetting-configurations-to-default"></a>RDWebClientDeploymentSetting 構成を既定値にリセットする

展開レベルの Web クライアント設定を既定の構成にリセットするには、次の PowerShell コマンドレットを実行し、-name パラメーターを使用して、リセットする設定を指定します。

   ```PowerShell
    Reset-RDWebClientDeploymentSetting -Name "LaunchResourceInBrowser"
    Reset-RDWebClientDeploymentSetting -Name "SuppressTelemetry"
   ```

## <a name="troubleshooting"></a>トラブルシューティング

ユーザーが初めて Web クライアントを開くときに以下のいずれかの問題が報告される場合、以降のセクションがそれらをどう修正するかの参考になります。

### <a name="what-to-do-if-the-users-browser-shows-a-security-warning-when-they-try-to-access-the-web-client"></a>Web クライアントへのアクセスを試みたときに、ユーザーのブラウザーにセキュリティの警告が表示される場合の対処方法

RD Web アクセスの役割で、信頼できる証明書が使用されていない可能性があります。 RD Web アクセスの役割が、公的に信頼された証明書で構成されていることを確認します。

改善されない場合は、Web クライアント URL 内のサーバー名が、RD Web 証明書によって提供される名前と一致していない可能性があります。 URL で、RD Web の役割をホストしているサーバーの FQDN を使用していることを確認します。

### <a name="what-to-do-if-the-user-cant-connect-to-a-resource-with-the-web-client-even-though-they-can-see-the-items-under-all-resources"></a>[すべてのリソース] の下で項目を確認できるのに、Web クライアントでユーザーがリソースに接続できない場合の対処方法

一覧のリソースを参照できても Web クライアントで接続できないとユーザーが報告する場合は、以下のことを確認します。

* RD ゲートウェイの役割は、信頼できるパブリック証明書を使用するように正しく構成されていますか。
* RD ゲートウェイ サーバーに、必要な更新プログラムがインストールされていますか。 サーバーに [KB4025334 更新プログラム](https://support.microsoft.com/help/4025334/windows-10-update-kb4025334)がインストールされていることを確認します。

接続を試みたときにユーザーが "予期しないサーバー認証証明書を受け取った" というエラー メッセージを受け取る場合、メッセージは証明書の拇印を表示します。 その拇印を使用して RD ブローカー サーバーの証明書マネージャーを検索し、適切な証明書を見つけます。 リモート デスクトップの展開のプロパティ ページで、RD ブローカーの役割で使用されるように証明書が構成されていることを確認します。 証明書が期限切れになっていないことを確認したら、.cer ファイル形式の証明書を RD Web アクセス サーバーにコピーし、かっこに囲まれた値は証明書のファイル パスに置き換えて、RD Web アクセス サーバーで次のコマンドを実行します。

```PowerShell
Import-RDWebClientBrokerCert <certificate file path>
```

### <a name="diagnose-issues-with-the-console-log"></a>コンソール ログの問題を診断する

この記事のトラブルシューティング手順に基づいて問題を解決できない場合は、ブラウザーでコンソール ログを参照することで、自分自身で問題の原因の診断を試みることができます。 Web クライアントには、問題の診断に役立つように、Web クライアントの使用中にブラウザーのコンソール ログにアクティビティを記録する方法が用意されています。

* 右上隅にある省略記号を選択し、ドロップダウン メニューの **[バージョン情報]** ページに移動します。
* **[Capture support information] (サポート情報をキャプチャする)** の **[Start recording] (記録の開始)** ボタンを選択します。
* 診断しようとしている、問題を発生させた Web クライアントで操作を行います。
* **[バージョン情報]** ページに移動し、 **[Stop recording] (記録の終了)** を選択します。
* お使いのブラウザーが **RD Console Logs.txt** という .txt ファイルを自動的にダウンロードします。 このファイルには、対象の問題を再現しながら生成された完全なコンソール ログ アクティビティが含まれています。

コンソールには、ブラウザーから直接アクセスすることもできます。 コンソールは通常、開発者ツールの下に置かれています。 たとえば、**F12** キーを押すか、省略記号ボタンを選択してから **[ツール]**  >  **[開発者ツール]** と移動することで、Microsoft Edge でログにアクセスできます。

## <a name="get-help-with-the-web-client"></a>Web クライアントに関するヘルプの表示

この記事の情報では解決できない問題が発生した場合は、[Tech Community](https://aka.ms/wvdtc) で報告できます。 [提案ボックス](https://remotedesktop.uservoice.com/forums/911494-remote-desktop-web-client)でも、新機能についてのリクエストや投票を行うことがきます。
