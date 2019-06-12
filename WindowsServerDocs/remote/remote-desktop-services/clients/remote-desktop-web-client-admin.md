---
title: ユーザー用にリモート デスクトップ Web クライアントをセットアップする
description: リモート デスクトップ web クライアントを管理者を設定する方法について説明します。
ms.prod: windows-server-threshold
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 11/2/2018
ms.topic: article
author: Heidilohr
ms.localizationpriority: medium
ms.openlocfilehash: 45164e9eca0873c82148aa3b7baa179a3f626dd7
ms.sourcegitcommit: d888e35f71801c1935620f38699dda11db7f7aad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66804975"
---
# <a name="set-up-the-remote-desktop-web-client-for-your-users"></a>ユーザー用にリモート デスクトップ Web クライアントをセットアップする

リモート デスクトップ web クライアントでは、互換性のある web ブラウザーを通じて、組織のリモート デスクトップのインフラストラクチャにアクセスできます。 リモート アプリやデスクトップのどこからでもローカル PC と同じように操作したりすることがあります。 リモート デスクトップ web クライアントを設定すると、ユーザーが開始に必要なすべての URL です、自分の資格情報、およびサポートされている web ブラウザーをクライアントにアクセスできます。

>[!IMPORTANT]
>Web クライアントはサポートされていない Azure アプリケーション プロキシを使用して、Web アプリケーション プロキシがまったくサポートされません。 参照してください[アプリケーション プロキシ サービスを使用して RDS](../rds-supported-config.md#using-remote-desktop-services-with-application-proxy-services)詳細についてはします。

## <a name="what-youll-need-to-set-up-the-web-client"></a>Web クライアントを設定する必要があります内容

始める前に、次の点を考慮してください。

* 確認、[リモート デスクトップの展開](../rds-deploy-infrastructure.md)RD ゲートウェイ、RD 接続ブローカー、および Windows Server 2016 または 2019 で実行されている RD Web アクセスを持ちます。
* 配置が構成されていることを確認します[ユーザーごとのクライアント アクセス ライセンス](../rds-client-access-license.md)(Cal)、デバイスごとではなくそれ以外の場合すべてのライセンスが消費されることです。
* インストール、 [Windows 10 KB4025334 update](https://support.microsoft.com/en-us/help/4025334/windows-10-update-kb4025334) RD ゲートウェイ。 後で累積的更新プログラムには、このサポート技術情報が含まれます既に可能性があります。
* RD ゲートウェイ、RD Web アクセスの役割のパブリックの信頼された証明書が構成されていることを確認します。
* ユーザーが接続するすべてのコンピューターが実行されている次の OS バージョンのいずれかを確認します。
  * Windows 10
  * Windows Server 2008 r2 またはそれ以降

Windows Server 2016 (またはそれ以降)、パフォーマンスが接続して Windows 10 (バージョン 1611 またはそれ以降) の向上、ユーザーが表示されます。

>[!IMPORTANT]
>プレビュー期間中に、web クライアントを使用して 1.0.0 より前のバージョンがインストールされている場合は、新しいバージョンに移行する前に、古いクライアントをアンインストールする必要があります。 「Web クライアントは、RDWebClientManagement の以前のバージョンがインストールされ、新しいバージョンを展開する前に削除する必要があります」というエラーが発生した場合は、次の手順に従います。
>
>1. 管理者特権で PowerShell プロンプトを開きます。
>2. 実行**Uninstall-module RDWebClientManagement**新しいモジュールをアンインストールします。
>3. 管理者特権で PowerShell プロンプトを閉じてから。
>4. 実行**Install-module RDWebClientManagement RequiredVersion\<以前のバージョン > 古いモジュールをインストールします。**
>5. 実行**アンインストール RDWebClient**古い web クライアントをアンインストールします。
>6. 実行**Uninstall-module RDWebClientManagement**古いモジュールをアンインストールします。
>7. 管理者特権で PowerShell プロンプトを閉じてから。
>8. 次のように、通常のインストールの手順に進みます。

## <a name="how-to-publish-the-remote-desktop-web-client"></a>リモート デスクトップ web クライアントを発行する方法

最初に、web クライアントをインストールするには、次の次の手順を実行します。

1. RD 接続ブローカー サーバーでリモート デスクトップ接続を使用する証明書を取得し、.cer ファイルとしてエクスポートします。 RD Web ロールを実行するサーバーに RD 接続ブローカーから .cer ファイルをコピーします。
2. RD Web アクセス サーバーでは、管理者特権の PowerShell プロンプトを開きます。
3. 、Windows Server 2016 では、受信トレイのバージョンが web クライアントの管理モジュールのインストールをサポートしていないため、powershellget を更新します。 PowerShellGet を更新するには、次のコマンドレットを実行します。
    ```PowerShell
    Install-Module -Name PowerShellGet -Force
    ```

    >[!IMPORTANT]
    >更新プログラムが有効で、モジュールが動作しない可能性があります、それ以外の場合になる前に、PowerShell を再起動する必要があります。

4. このコマンドレットで PowerShell ギャラリーからのリモート デスクトップ web クライアントの管理 PowerShell モジュールをインストールします。
    ```PowerShell
    Install-Module -Name RDWebClientManagement
    ```

5. その後、リモート デスクトップ web クライアントの最新バージョンをダウンロードする、次のコマンドレットを実行します。
    ```PowerShell
    Install-RDWebClientPackage
    ```

6. 次に、RD ブローカーからコピーした .cer ファイルのパスに置き換え、かっこで囲まれた値でこのコマンドレットを実行します。
    ```PowerShell
    Import-RDWebClientBrokerCert <.cer file path>
    ```

7. 最後に、リモート デスクトップの web クライアントに発行するには、このコマンドレットを実行します。
    ```PowerShell
    Publish-RDWebClientPackage -Type Production -Latest
    ```
    Web クライアントの URL で web クライアントは、サーバー名として書式設定にアクセスできるように<https://server_FQDN/RDWeb/webclient/index.html>します。 RD Web アクセスに URL (通常、サーバーの FQDN) でのパブリック証明書に一致するサーバー名を使用する必要があります。

    >[!NOTE]
    >実行するときに、**発行 RDWebClientPackage**コマンドレット、する可能性がありますを参照してください、という警告が表示されたデバイス単位 Cal がサポートされていない場合でも、ユーザー単位 cal、配置が構成されています。 デプロイには、ユーザー単位 Cal が使用されている場合は、この警告を無視できます。 構成の制限のことを知っているかどうかを確認することが表示されます。
8. Web クライアントにアクセスするユーザーの準備ができたら、送信するだけです、作成した web クライアントの URL。

>[!NOTE]
>RDWebClientManagement モジュールのサポートされているすべてのコマンドレットの一覧を表示するには、PowerShell で次のコマンドレットを実行します。
>```PowerShell
>Get-Command -Module RDWebClientManagement
>```

## <a name="how-to-update-the-remote-desktop-web-client"></a>リモート デスクトップ web クライアントを更新する方法

リモート デスクトップ web クライアントの新しいバージョンが利用できる場合は、新しいクライアントで展開を更新する次の手順に従います。

1. RD Web アクセス サーバーで管理者特権の PowerShell プロンプトを開き、web クライアントの最新バージョンをダウンロードするのには、次のコマンドレットを実行します。
    ```PowerShell
    Install-RDWebClientPackage
    ```

2. 必要に応じて、このコマンドレットを実行して、公式リリース前に、テスト用クライアントを発行できます。
    ```PowerShell
    Publish-RDWebClientPackage -Type Test -Latest
    ```

    クライアントは、web クライアントの URL に対応する URL のテストに表示する必要があります (たとえば、 <https://server_FQDN/RDWeb/webclient-test/index.html>)。
3. 次のコマンドレットを実行してユーザー向けにクライアントを発行します。
    ```PowerShell
    Publish-RDWebClientPackage -Type Production -Latest
    ```

    Web ページを再実行するときに、すべてのユーザー用のクライアントに置き換わります。

## <a name="how-to-uninstall-the-remote-desktop-web-client"></a>リモート デスクトップ web クライアントをアンインストールする方法

Web クライアントのすべてのトレースを削除するには、次の手順を実行します。

1. RD Web アクセス サーバーでは、管理者特権の PowerShell プロンプトを開きます。
2. テストと実稼働クライアントを非公開に、ローカル パッケージをアンインストールし、web クライアントの設定を削除します。

   ```PowerShell
   Uninstall-RDWebClient
   ```

3. リモート デスクトップ web クライアントの管理 PowerShell モジュールをアンインストールします。

   ```PowerShell
   Uninstall-Module -Name RDWebClientManagement
   ```

## <a name="how-to-install-the-remote-desktop-web-client-without-an-internet-connection"></a>インターネットに接続せず、リモート デスクトップ web クライアントをインストールする方法

Web クライアント、インターネット接続がない RD Web アクセス サーバーを展開する次の手順に従います。

> [!NOTE]
> インターネット接続が使用できるは、バージョン 1.0.1 以降でないインストール RDWebClientManagement PowerShell モジュールの。

> [!NOTE]
> オフライン サーバーに転送する前に、必要なファイルをダウンロードにインターネットにアクセスできる管理者 PC が必要です。

> [!NOTE]
> エンドユーザーの PC では、ここでは、インターネット接続が必要です。 これは、完全なオフライン シナリオを提供するクライアントの将来のリリースで解決されます。

### <a name="from-a-device-with-internet-access"></a>インターネットにアクセスできるデバイスから

1. PowerShell プロンプトを開きます。

2. PowerShell ギャラリーから、リモート デスクトップ web クライアントの管理 PowerShell モジュールをインポートします。
    ```PowerShell
    Import-Module -Name RDWebClientManagement
    ```

3. 別のデバイスにインストールするためのリモート デスクトップ web クライアントの最新バージョンをダウンロードするには。
    ```PowerShell
    Save-RDWebClientPackage "C:\WebClient\"
    ```

4. RDWebClientManagement PowerShell モジュールの最新バージョンをダウンロードするには。
    ```PowerShell
    Find-Module -Name "RDWebClientManagement" -Repository "PSGallery" | Save-Module -Path "C:\WebClient\"
    ```

5. 内容をコピー"C:\WebClient\" RD Web アクセス サーバーにします。

### <a name="from-the-rd-web-access-server"></a>RD Web アクセス サーバーから

説明に従い[web のリモート デスクトップ クライアントを発行する方法](remote-desktop-web-client-admin.md#how-to-publish-the-remote-desktop-web-client)、手順 4. と 5. を次に置き換えます。

4. ローカル フォルダーから、リモート デスクトップ web クライアントの管理 PowerShell モジュールをインポートします。
    ```PowerShell
    Import-Module -Name "C:\WebClient\"
    ```

5. ローカル フォルダー (適切な zip ファイルに置き換えてください) からリモート デスクトップ web クライアントの最新バージョンを展開するには。
    ```PowerShell
    Install-RDWebClientPackage -Source "C:\WebClient\rdwebclient-1.0.1.zip"
    ```

## <a name="connecting-to-rd-broker-without-rd-gateway-in-windows-server-2019"></a>Windows server 2019 RD ゲートウェイなし RD ブローカーへの接続
このセクションでは、RD ブローカー、RD ゲートウェイの Windows Server 2019 せずへの web クライアント接続を有効にする方法について説明します。

### <a name="setting-up-the-rd-broker-server"></a>RD ブローカー サーバーを設定します。

#### <a name="follow-these-steps-if-there-is-no-certificate-bound-to-the-rd-broker-server"></a>RD ブローカー サーバーにバインドされた証明書がない場合に次の手順に従ってください。

1. 開いている**サーバー マネージャー** > **リモート デスクトップ サービス**します。

2. **展開の概要**セクションで、**タスク**ドロップダウン メニュー。

3. 選択**展開のプロパティの編集**、というタイトルの新しいウィンドウ**配置プロパティ**が開きます。

4. **配置プロパティ**ウィンドウで、**証明書**左側のメニュー。

5. 証明書のレベルの一覧で選択**RD 接続ブローカー - 有効にするシングル サインオンの**します。 次の 2 つの方法があります。(1) を作成、新しい証明書または (2) 既存の証明書。

#### <a name="follow-these-steps-if-there-is-a-certificate-previously-bound-to-the-rd-broker-server"></a>以前に RD ブローカー サーバーにバインドされた証明書がある場合これらの手順に従います

1. ブローカーとコピーにバインドされた証明書を open、**拇印**値。

2. セキュリティで保護されたポート 3392 にこの証明書をバインドする管理者特権の PowerShell ウィンドウを開くし、次を実行コマンドを置き換える **"< thumbprint >"** 値を前の手順からコピーされます。

    ```PowerShell
    netsh http add sslcert ipport=0.0.0.0:3392 certhash="<thumbprint>" certstorename="Remote Desktop" appid="{00000000-0000-0000-0000-000000000000}"
    ```

    > [!NOTE]
    > かどうか、証明書が正しくバインドされていることを確認するには、次のコマンドを実行します。
    >
    > ```PowerShell
    > netsh http show sslcert
    > ```
    >
    > 、SSL 証明書のバインドの一覧でポート 3392 に正しい証明書がバインドされていることを確認します。

3. 開き、Windows レジストリ (regedit) を nagivate```HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp```キーを検索および**WebSocketURI**します。 値を設定する必要があります <strong>https://+:3392/rdp/</strong>します。

### <a name="setting-up-the-rd-session-host"></a>RD セッション ホストの設定
RD セッション ホスト サーバーが RD ブローカー サーバーと異なる場合は、次の手順に従います。

1. RD セッション ホスト コンピューターの証明書を作成し、それを開き、コピー、**拇印**値。

2. セキュリティで保護されたポート 3392 にこの証明書をバインドする管理者特権の PowerShell ウィンドウを開くし、次を実行コマンドを置き換える **"< thumbprint >"** 値を前の手順からコピーされます。

    ```PowerShell
    netsh http add sslcert ipport=0.0.0.0:3392 certhash="<thumbprint>" appid="{00000000-0000-0000-0000-000000000000}"
    ```

    > [!NOTE]
    > かどうか、証明書が正しくバインドされていることを確認するには、次のコマンドを実行します。
    >
    > ```PowerShell
    > netsh http show sslcert
    > ```
    >
    > 、SSL 証明書のバインドの一覧でポート 3392 に正しい証明書がバインドされていることを確認します。

3. 開き、Windows レジストリ (regedit) を nagivate```HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp```キーを検索および**WebSocketURI**します。 値を設定する必要があります<https://+:3392/rdp/>します。

### <a name="general-observations"></a>一般的な所見

* RD セッション ホスト、RD ブローカーの両方のサーバーが Windows Server 2019 を実行していることを確認します。

* そのパブリックでは、RD セッション ホスト、RD ブローカーの両方のサーバー証明書が構成された信頼されていることを確認します。
    > [!NOTE]
    > RD セッション ホスト、RD ブローカー サーバーの両方に、同じコンピューターを共有している場合は、RD ブローカー サーバー証明書のみを設定します。 RD セッション ホスト、RD ブローカー サーバーは、さまざまなマシンを使用して、一意の証明書両方構成する必要があります。

* **サブジェクト代替名 (SAN)** にマシンの各証明書を設定する必要があります**完全修飾ドメイン名 (FQDN)** します。 **共通名 (CN)** 各証明書の SAN に一致する必要があります。

## <a name="how-to-pre-configure-settings-for-remote-desktop-web-client-users"></a>Web クライアントのリモート デスクトップ ユーザーの設定を事前に構成する方法
このセクションでは、PowerShell を使用して、リモート デスクトップ web クライアントの展開の設定を構成する方法を説明します。 これら PowerShell コマンドレットの制御の設定を変更するユーザーの機能は、組織のセキュリティに関する注意事項に基づくまたはワークフローを対象としています。 次の設定はすべてにある、**設定**web クライアントのサイド パネル。 

### <a name="suppress-telemetry"></a>製品利用統計情報を表示しません。
既定では、ユーザーを有効または Microsoft に送信されるテレメトリ データの収集を無効にできます。 Microsoft が収集テレメトリ データについてでリンクを使用して、プライバシーに関する声明を参照してください、**について**サイド パネル。

管理者は、次の PowerShell コマンドレットを使用して、デプロイのテレメトリの収集を抑制する選択できます。

   ```PowerShell
    Set-RDWebClientDeploymentSetting -SuppressTelemetry $true
   ```

既定では、ユーザーを有効またはテレメトリを無効にする選択可能性があります。 ブール値 **$false**は、既定のクライアント動作と一致します。 ブール値 **$true**テレメトリを無効にし、テレメトリを有効にすると、ユーザーを制限します。

### <a name="remote-resource-launch-method"></a>リモート リソースの起動方法
既定では、ユーザーは、ブラウザーで (1) または (2) コンピューターにインストールされている他のクライアントで処理するために、.rdp ファイルをダウンロードしてリモート リソースを起動する選択可能性があります。 管理者は、次の Powershell コマンドを使用して、デプロイ用のリモート リソースの起動方法を制限できます。

   ```PowerShell
    Set-RDWebClientDeploymentSetting -LaunchResourceInBrowser ($true|$false)
   ```
 既定では、ユーザーは、いずれかの起動方法を選択できます。 ブール値 **$true**ユーザーは、ブラウザー内のリソースを起動します。 ブール値 **$false**により、ユーザーをローカルにインストールされた RDP クライアントで処理するために、.rdp ファイルをダウンロードすることによってリソースを起動します。

### <a name="reset-rdwebclientdeploymentsetting-configurations-to-default"></a>既定値に RDWebClientDeploymentSetting 構成をリセットします。
すべての配置レベルの web クライアント設定を既定の構成をリセットするには、次の PowerShell コマンドレットを実行します。

   ```PowerShell
    Reset-RDWebClientDeploymentSetting 
   ```

## <a name="troubleshooting"></a>トラブルシューティング

ユーザーは web クライアントを初めて開くときに、次の問題のいずれかを報告する場合、次のセクションを教えてくれますそれらを解決するためにします。

### <a name="what-to-do-if-the-users-browser-shows-a-security-warning-when-they-try-to-access-the-web-client"></a>ユーザーのブラウザーの web クライアントにアクセスしようとすると、セキュリティの警告が表示される場合の対処方法

RD Web アクセス役割で信頼された証明書が使用していない可能性があります。 公的に信頼された証明書で、RD Web アクセスの役割が構成されていることを確認します。

うまく行かない場合、web でサーバー名クライアント URL 可能性がありますと一致しません RD Web 証明書によって指定された名前。 URL は、RD Web ロールをホストするサーバーの FQDN を使用することを確認します。

### <a name="what-to-do-if-the-user-cant-connect-to-a-resource-with-the-web-client-even-though-they-can-see-the-items-under-all-resources"></a>ユーザーは、web クライアントの場合でも、すべてのリソースの下の項目を表示で、リソースに接続できない場合の対処方法

ユーザーは、それらが示されているリソースを表示することができる場合でも web クライアントで接続できないことを報告する場合は、次のことを確認します。

* RD ゲートウェイの役割は信頼された公開証明書を使用して正しく構成されてでしょうか。
* RD ゲートウェイ サーバーにはインストールされている必要な更新プログラムがありますか。 サーバーが持つことを確認[KB4025334 update](https://support.microsoft.com/en-us/help/4025334/windows-10-update-kb4025334)をインストールします。

ユーザーが「予期しないサーバー認証証明書が受信されました」エラーを取得するかどうか、メッセージは、証明書の拇印を表示し、接続を試みたときのメッセージします。 その拇印を使用して、適切な証明書を検索する RD ブローカー サーバーの証明書マネージャーを検索します。 リモート デスクトップの展開のプロパティ ページで、RD ブローカー ロールを使用する証明書が構成されていることを確認します。 証明書を必ずが期限切れ後に証明書を .cer ファイル形式で、RD Web アクセス サーバーにコピーし、かっこで囲まれた値は、証明書のファイル パスに置き換え、RD Web アクセス サーバーで次のコマンドを実行します。

```PowerShell
Import-RDWebClientBrokerCert <certificate file path>
```

### <a name="diagnose-issues-with-the-console-log"></a>コンソール ログの問題を診断します。

コンソールを見て、自分で問題の原因を診断しようとすることができます、この記事のトラブルシューティング手順に基づいて、問題を解決できない場合、ブラウザーでログインします。 Web クライアントは、問題の診断に役立つ、web クライアントを使用しているときにブラウザーのコンソール ログのアクティビティを記録するためのメソッドを提供します。

* 右上隅にある省略記号を選択しに、**について**ページのドロップダウン メニュー。
* **サポート情報をキャプチャ**選択、**の記録を開始**ボタンをクリックします。
* 診断しようとして問題を生成する web クライアントでは、操作を実行します。
* 移動し、**について** ページ**記録終了**。
* お使いのブラウザーは「.txt ファイル自動的にダウンロード**RD コンソール Logs.txt**します。 このファイルは、ターゲットの問題を再現しながら生成された完全なコンソール ログ アクティビティが含まれます。

コンソールは、お使いのブラウザーから直接アクセスすることも可能性があります。 コンソールは通常、開発者ツールにあります。 たとえば、Microsoft Edge でログをアクセス キーを押して、 **F12**キー、または、省略記号ボタンを選択するに移動し**ツール** > **Developer Tools**.

## <a name="get-help-with-the-web-client"></a>Web クライアント ヘルプを表示します。

この記事の情報で解決できない問題が発生した場合は、[送り](mailto:rdwbclnt@microsoft.com)それを報告します。 また、リクエストするかの新機能に投票、[提案ボックス](https://aka.ms/rdwebfbk)します。
