---
title: Windows Admin Center の一般的なトラブルシューティングの手順
description: Windows Admin Center の一般的なトラブルシューティングの手順 (Project Honolulu)
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 06/07/2019
ms.openlocfilehash: 4d108161dd4f6b57d4a86cbcaa5852aff53f0ac3
ms.sourcegitcommit: 63926404009f9e1330a4a0aa8cb9821a2dd7187e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2019
ms.locfileid: "67469522"
---
# <a name="troubleshooting-windows-admin-center"></a>Windows Admin Center のトラブルシューティング

> 適用対象:Windows Admin Center、Windows Admin Center プレビュー

> [!Important]
> このガイドは、Windows Admin Center を使用できない原因となっている問題を診断および解決するのに役立ちます。 特定のツールで問題が発生している場合は、[既知の問題](http://aka.ms/wacknownissues)が発生しているかどうかを確認してください。

## <a name="installer-fails-with-message-the-module-microsoftpowershelllocalaccounts-could-not-be-loaded"></a>インストーラーは、メッセージで失敗します。 **_モジュール 'Microsoft.PowerShell.LocalAccounts' を読み込むことができませんでした。_ **

これは、既定の PowerShell モジュールのパスが変更または削除された場合に発生することができます。 この問題を解決することを確認します```%SystemRoot%\system32\WindowsPowerShell\v1.0\Modules```は、**最初**PSModulePath 環境変数内の項目。 PowerShell の次の行では、これを実現できます。

```powershell
[Environment]::SetEnvironmentVariable("PSModulePath","%SystemRoot%\system32\WindowsPowerShell\v1.0\Modules;" + ([Environment]::GetEnvironmentVariable("PSModulePath","User")),"User")
```

## <a name="i-get-a-this-sitepage-cant-be-reached-error-in-my-web-browser"></a>Web ブラウザーで  **This site/page can't be reached** (このサイト/ページに到達できません) というエラーが表示される

### <a name="if-youve-installed-windows-admin-center-as-an-app-on-windows-10"></a>**Windows 10 のアプリ**として Windows Admin Center をインストールしている場合

* Windows Admin Center が実行されていることを確認します。 Windows Admin Center アイコンを探します![](../media/trayIcon.PNG)システム トレイまたは**Windows Admin Center のデスクトップ/SmeDesktop.exe**タスク マネージャーでします。 見つからない場合は、[スタート] メニューから **Windows Admin Center** を起動します。

> [!NOTE] 
> 再起動後、[スタート] メニューから Windows Admin Center を起動する必要があります。  

* [Windows のバージョンを確認してください。](#check-the-windows-version)

* Web ブラウザーとして Microsoft Edge または Google Chrome のいずれかを使用していることを確認します。

* [最初の起動](../use/get-started.md#selecting-a-client-certificate)時に正しい証明書を選択しましたか。

  * プライベート セッションでブラウザーを開いてみてください。問題が解決したら、キャッシュをクリアする必要があります。

* 最近にアップグレードする Windows 10、新しいビルドまたはバージョンをでしょうか。

  * 信頼されたホストの設定をクリアこの可能性があります。 [この手順では、信頼されたホストの設定を更新します。](#configure-trustedhosts)

### <a name="if-youve-installed-windows-admin-center-as-a-gateway-on-windows-server"></a>**Windows Server でのゲートウェイ**として Windows Admin Center をインストールした場合

* Windows Admin Center の以前のバージョンからアップグレードするでしたか。 ために、ファイアウォール規則は削除されなかったかどうかを確認する[既知の問題これ](known-issues.md#upgrade)します。 ルールが存在するかを判断するのにには、次の PowerShell コマンドを使用します。 ない場合は、次の[手順](known-issues.md#upgrade)再作成します。
    
    ```powershell
    Get-NetFirewallRule -DisplayName "SmeInboundOpenException"
    ```

* クライアントとサーバーの [Windows バージョン](#check-the-windows-version) を確認します。

* Web ブラウザーとして Microsoft Edge または Google Chrome のいずれかを使用していることを確認します。

* サーバーで、タスク マネージャーを開き > サービスと必ず**ServerManagementGateway/Windows Admin Center**が実行されています。
![](../media/Service-TaskMan.PNG)

* ゲートウェイへのネットワーク接続のテスト (置換\<値 > のデプロイメントから情報を含む)

    ```powershell
    Test-NetConnection -Port <port> -ComputerName <gateway> -InformationLevel Detailed
    ```

### <a name="if-you-have-installed-windows-admin-center-in-an-azure-windows-server-vm"></a>Azure Windows Server VM で Windows Admin Center をインストールした場合

* [Windows のバージョンを確認してください。](#check-the-windows-version)
* HTTPS の受信ポート規則を追加しましたか 
* [Azure VM で Windows Admin Center をインストールする方法の詳細します。](https://docs.microsoft.com/windows-server/manage/windows-admin-center/configure/azure-integration#use-a-windows-admin-center-gateway-deployed-in-azure)

### <a name="check-the-windows-version"></a>Windows のバージョンを確認します。

* [ファイル名を指定して実行] ダイアログを開き (Windows キー + R)、```winver``` を起動します。

* Windows 10 バージョン 1703 以下を使用している場合、Windows Admin Center はお使いのバージョンの Microsoft Edge ではサポートされません。 最新バージョンの Windows 10 にアップグレードするか、Chrome を使用します。

* 17134 と 17637 間のビルド バージョンの Windows 10 または Server の insider プレビュー バージョンを使用する場合、Windows には、Windows Admin Center の失敗の原因となったバグが必要があります。 Windows の場合は、現在サポートされているバージョンを使用してください。

### <a name="make-sure-the-windows-remote-management-winrm-service-is-running-on-both-the-gateway-machine-and-managed-node"></a>Windows リモート管理 (WinRM) サービスがゲートウェイ コンピューターと管理対象ノードの両方で実行されていることを確認します。

* WindowsKey を押しながら R を実行 ダイアログを開く
* 型```services.msc```し、enter キーを押します
* Windows リモート管理 (WinRM) を探して、ウィンドウが開き、ことが実行されていることと、自動開始設定を確認します。

### <a name="did-you-upgrade-your-server-from-2016-to-2019"></a>サーバーからにアップグレードする 2016年 2019年でしょうか。

* 信頼されたホストの設定をクリアこの可能性があります。 [この手順では、信頼されたホストの設定を更新します。](#configure-trustedhosts) 

## <a name="i-get-the-message-cant-connect-securely-to-this-page-this-might-be-because-the-site-uses-outdated-or-unsafe-tls-security-settings"></a>メッセージが表示されます。"できません。 このページに安全に接続します。 サイトが古いか、安全でない TLS セキュリティ設定を使用して可能性があります。

コンピューターは、http/2 接続に限定されます。 Windows Admin Center では、統合 Windows 認証では、http/2 でサポートされていないを使用します。 次の 2 つのレジストリ値を追加、```HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Http\Parameters```キーを**ブラウザーを実行しているマシン**http/2 制限を解除します。

```
EnableHttp2Cleartext=dword:00000000
EnableHttp2Tls=dword:00000000
```

## <a name="im-having-trouble-with-the-remote-desktop-events-and-powershell-tools"></a>リモート デスクトップ、イベント、および PowerShell ツールで問題が発生しました。

これら 3 つのツールでは、websocket プロトコルは、プロキシ サーバーやファイアウォールによってブロックがよく必要があります。 Google Chrome を使用している場合は、[既知の問題](known-issues.md#google-chrome)websockets および NTLM 認証を使用します。

## <a name="i-can-connect-to-some-servers-but-not-others"></a>一部のサーバーに接続できるが、他のサーバーには接続できない

* しようとゲートウェイ コンピューターでローカルにログオン```Enter-PSSession <machine name>```PowerShell では、置き換える\<マシン名 > Windows Admin Center で管理しようとしているコンピューターの名前に置き換えます。 

* 環境でドメインの代わりにワークグループを使用している場合は、「[ワークグループでの Windows Admin Center の使用](#using-windows-admin-center-in-a-workgroup)」を参照してください。

* **ローカル管理者アカウントを使用するには。** ビルトイン administrator アカウントではないローカル ユーザー アカウントを使用している場合は、次のコマンドでは、PowerShell またはコマンド プロンプトで管理者として、対象コンピューターで実行してターゲット コンピューターのポリシーを有効にする必要があります。

    ```
    REG ADD HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1
    ```

## <a name="using-windows-admin-center-in-a-workgroup"></a>ワークグループでの Windows Admin Center の使用

### <a name="what-account-are-you-using"></a>使用しているアカウント
使用している資格情報が、対象サーバーのローカル管理者グループのメンバーであることを確認します。 場合によっては、WinRM で Remote Management Users グループでのメンバーシップも必要になります。 **ビルトイン Administrator アカウントではない**ローカル ユーザー アカウントを使用している場合は、PowerShell で、またはターゲット コンピューターで管理者としてコマンド プロンプトで次のコマンドを実行して、ターゲット コンピューターでポリシーを有効にする必要があります。

```cmd
REG ADD HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1
```
### <a name="are-you-connecting-to-a-workgroup-machine-on-a-different-subnet"></a>異なるサブネットでワークグループ コンピューターに接続している場合

ゲートウェイと同じサブネット上にないワークグループ コンピューターに接続するには、WinRM (TCP 5985) のファイアウォール ポートにより、ターゲット コンピューターで受信トラフィックが許可されていることを確認します。 PowerShell で、またはターゲット コンピューターで管理者としてコマンド プロンプトで次のコマンドを実行して、このファイアウォール規則を作成することができます。

- **Windows Server**

    ```powershell
    Set-NetFirewallRule -Name WINRM-HTTP-In-TCP-PUBLIC -RemoteAddress Any
    ```

- **Windows 10**

    ```powershell
    Set-NetFirewallRule -Name WINRM-HTTP-In-TCP -RemoteAddress Any
    ```

### <a name="configure-trustedhosts"></a>TrustedHosts の構成

Windows Admin Center のインストール時に、Windows Admin Center でゲートウェイの TrustedHosts 設定を管理できるように選択できます。 これは、ワークグループ環境またはドメインでローカル管理者の資格情報を使用している場合に必要です。 この設定を行わなかった場合は、TrustedHosts を手動で構成する必要があります。

**PowerShell コマンドを使用して TrustedHosts を変更するには。**

1. 管理者の PowerShell セッションを開きます。
2. 現在の TrustedHosts 設定を確認します。

    ```powershell
    Get-Item WSMan:\localhost\Client\TrustedHosts
    ```

   > [!WARNING]
   > TrustedHosts の現在の設定が空でない場合は、次のコマンドにより設定が上書きされます。 必要に応じて復元できるように、次のコマンドを使用して現在の設定をテキスト ファイルに保存することをお勧めします。
   > 
   > `Get-Item WSMan:localhost\Client\TrustedHosts | Out-File C:\OldTrustedHosts.txt`

3. TrustedHosts を、管理するコンピューターの NetBIOS、IP、または FQDN に設定します。

    ```powershell
    Set-Item WSMan:localhost\Client\TrustedHosts -Value '192.168.1.1,server01.contoso.com,server02'
    ```

   > [!TIP]
   > すべての TrustedHosts を一度に設定する簡単な方法として、ワイルドカードを使用することができます。
   > 
   >     Set-Item WSMan:\localhost\Client\TrustedHosts -Value '*'

4. テストが完了したら、管理者特権の PowerShell セッションから次のコマンドを実行し、TrustedHosts 設定をクリアできます。

    ```powershell
    Clear-Item WSMan:localhost\Client\TrustedHosts
    ```

5. 以前に設定をエクスポートした場合は、ファイルを開いて値をコピーし、次のコマンドを使用します。

    ```powershell
    Set-Item WSMan:localhost\Client\TrustedHosts -Value '<paste values from text file>'
    ```

## <a name="i-previously-had-windows-admin-center-installed-and-now-nothing-else-can-use-the-same-tcpip-port"></a>以前 Windows Admin Center がインストールされているし、同じ TCP/IP ポートを使用して他に何もようになりました

手動で管理者特権でコマンド プロンプトでこれら 2 つのコマンドを実行します。

```cmd
netsh http delete sslcert ipport=0.0.0.0:443
netsh http delete urlacl url=https://+:443/
```

## <a name="azure-features-dont-work-properly-in-edge"></a>Azure の機能は Edge で適切に動作しません。

エッジが[既知の問題](https://github.com/AzureAD/azure-activedirectory-library-for-js/wiki/Known-issues-on-Edge)Windows Admin Center での Azure のログインに影響を与えるセキュリティ ゾーンに関連します。 Edge を使用する場合は、Azure の機能を使用していて問題が発生した場合は、追加してみてください https://login.microsoftonline.com 、 https://login.live.com としてゲートウェイの URL は、信頼済みサイトと、エッジ、クライアント側のブラウザーでポップアップ ブロックの設定のサイトを許可するとします。 

これには、次の手順を実行します。
1. 検索**インターネット オプション**Windows の [スタート] メニュー
2. 移動して、**セキュリティ** タブ
3. で、**信頼済みサイト**オプションで、をクリックして、**サイト**ボタンをクリックし、表示されたダイアログ ボックスで Url を追加します。 ゲートウェイの URL を追加する必要がありますだけでなく https://login.microsoftonline.com と https://login.live.com します。
4. 移動して、**プライバシー**  タブ
5. で、**ポップアップ ブロック**セクションで、をクリックして、**設定**ボタンをクリックし、表示されたダイアログ ボックスで Url を追加します。 ゲートウェイの URL を追加する必要がありますだけでなく https://login.microsoftonline.com と https://login.live.com します。

## <a name="having-an-issue-with-an-azure-related-feature"></a>Azure 関連の機能の問題があるでしょうか。

電子メールでお送りくださいwacFeedbackAzure@microsoft.com次の情報。
* 一般的な問題について、[質問を以下に示す](#providing-feedback-on-issues)します。
* 問題と問題を再現するために行った手順について説明します。 
* でした以前新規 AadApp.ps1 ダウンロード可能なスクリプトを使用して Azure へのゲートウェイを登録し、1807 バージョンにアップグレードしますか。 ゲートウェイの設定から UI を使用して Azure へのゲートウェイを登録するでしたまたは > Azure でしょうか。
* 複数のテナント/ディレクトリに関連付けられている Azure アカウントとは
    * [はい] の場合。Windows Admin Center を Azure AD アプリケーションを登録するときに、Azure で、既定のディレクトリを使用したディレクトリをでしたか。 
* Azure アカウントに複数のサブスクリプションへのアクセスがあるでしょうか。
* 接続されている課金を使用していたサブスクリプションはありますか
* ログに記録された複数の Azure アカウントに問題が発生したときか。
* Azure アカウントには、多要素認証を要求しますか。
* Azure VM を管理しようとしているマシンとは
* Azure VM にインストールする Windows Admin Center でしょうか。

## <a name="providing-feedback-on-issues"></a>問題に関するフィードバックの提供

[イベント ビューアー] > [アプリケーションとサービス] > [Microsoft-ServerManagementExperience] の順に移動し、エラーまたは警告がないか探します。

問題について説明している [UserVoice](https://windowsserver.uservoice.com/forums/295071/category/319162?query=%5BBug%5D) で問題を登録します。

イベント ログで見つけたエラーまたは警告、および次の情報を含めてください。 

* Windows Admin Center が**インストールされている**プラットフォーム (Windows 10 または Windows Server):
    * サーバーにインストールする場合は、Windows[バージョン](#check-the-windows-version)の**ブラウザーを実行しているマシン**Windows Admin Center にアクセスします。 
    * インストーラーによって作成された自己署名証明書を使用しているでしょうか。
    * 独自の証明書を使用している場合は、サブジェクト名とコンピューターが一致しますか。
    * 独自の証明書を使用している場合、別のサブジェクト名を指定していますか。
* 既定のポートの設定でインストールしましたか。
    * そうでない場合、どのポートを指定しましたか。
* Windows Admin Center が**インストールされている**コンピューターはドメインに参加していますか。
* Windows Admin Center が**インストールされている** Windows [バージョン](#check-the-windows-version):
* **管理しようとしている**コンピューターはドメインに参加していますか。
* **管理しようとしている**コンピューターの Windows [バージョン](#check-the-windows-version):
* どのブラウザーを使用していますか。
    * Google Chrome を使用している場合、バージョンは何ですか。 ([ヘルプ] > [Google Chromeについて])

