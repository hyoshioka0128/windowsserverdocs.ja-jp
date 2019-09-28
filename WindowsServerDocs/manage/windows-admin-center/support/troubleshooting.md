---
title: Windows Admin Center の一般的なトラブルシューティングの手順
description: Windows Admin Center の一般的なトラブルシューティングの手順 (Project Honolulu)
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.localizationpriority: medium
ms.prod: windows-server
ms.date: 06/07/2019
ms.openlocfilehash: f4e772550aaba6fe9a4f78a6032eaabde4aeb0bf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406860"
---
# <a name="troubleshooting-windows-admin-center"></a>Windows Admin Center のトラブルシューティング

> 適用対象:Windows Admin Center、Windows Admin Center Preview

> [!Important]
> このガイドは、Windows Admin Center を使用できない原因となっている問題を診断および解決するのに役立ちます。 特定のツールで問題が発生している場合は、[既知の問題](http://aka.ms/wacknownissues)が発生しているかどうかを確認してください。

## <a name="installer-fails-with-message-_the-module-microsoftpowershelllocalaccounts-could-not-be-loaded_"></a>インストーラーが失敗し、次のメッセージが表示される: **_モジュール ' Microsoft. PowerShell. LocalAccounts ' を読み込めませんでした。_**

これは、既定の PowerShell モジュールパスが変更または削除された場合に発生する可能性があります。 この問題を解決するには、PSModulePath 環境変数の**最初**の項目が ```%SystemRoot%\system32\WindowsPowerShell\v1.0\Modules``` であることを確認します。 これは、次の PowerShell の行を使用して実現できます。

```powershell
[Environment]::SetEnvironmentVariable("PSModulePath","%SystemRoot%\system32\WindowsPowerShell\v1.0\Modules;" + ([Environment]::GetEnvironmentVariable("PSModulePath","User")),"User")
```

## <a name="i-get-a-this-sitepage-cant-be-reached-error-in-my-web-browser"></a>Web ブラウザーで  **This site/page can't be reached** (このサイト/ページに到達できません) というエラーが表示される

### <a name="if-youve-installed-windows-admin-center-as-an-app-on-windows-10"></a>**Windows 10 のアプリ**として Windows Admin Center をインストールしている場合

* Windows Admin Center が実行されていることを確認します。 タスクマネージャーのシステムトレイまたは**Windows 管理センターのデスクトップ/SmeDesktop**で、Windows 管理センターのアイコン ![](../media/trayIcon.PNG) を探します。 見つからない場合は、[スタート] メニューから **Windows Admin Center** を起動します。

> [!NOTE] 
> 再起動後、[スタート] メニューから Windows Admin Center を起動する必要があります。  

* [Windows のバージョンを確認する](#check-the-windows-version)

* Web ブラウザーとして Microsoft Edge または Google Chrome のいずれかを使用していることを確認します。

* [最初の起動](../use/get-started.md#selecting-a-client-certificate)時に正しい証明書を選択しましたか。

  * プライベート セッションでブラウザーを開いてみてください。問題が解決したら、キャッシュをクリアする必要があります。

* 最近、Windows 10 を新しいビルドまたはバージョンにアップグレードしましたか?

  * これにより、信頼されたホストの設定がクリアされた可能性があります。 [信頼されたホストの設定を更新するには、次の手順に従います。](#configure-trustedhosts)

### <a name="if-youve-installed-windows-admin-center-as-a-gateway-on-windows-server"></a>**Windows Server でのゲートウェイ**として Windows Admin Center をインストールした場合

* 以前のバージョンの Windows 管理センターからアップグレードしましたか? [この既知の問題](known-issues.md#upgrade)により、ファイアウォール規則が削除されていないことを確認してください。 次の PowerShell コマンドを使用して、ルールが存在するかどうかを確認します。 そうでない場合は、[次の手順](known-issues.md#upgrade)に従って再作成します。
    
    ```powershell
    Get-NetFirewallRule -DisplayName "SmeInboundOpenException"
    ```

* クライアントとサーバーの [Windows バージョン](#check-the-windows-version) を確認します。

* Web ブラウザーとして Microsoft Edge または Google Chrome のいずれかを使用していることを確認します。

* サーバーで、[タスクマネージャー > サービス] を開き、 **Servermanagementgateway/Windows 管理センター**が実行されていることを確認します。
![](../media/Service-TaskMan.PNG)

* ゲートウェイへのネットワーク接続をテストします (@no__t 0values > を展開の情報に置き換えてください)。

    ```powershell
    Test-NetConnection -Port <port> -ComputerName <gateway> -InformationLevel Detailed
    ```

### <a name="if-you-have-installed-windows-admin-center-in-an-azure-windows-server-vm"></a>Windows 管理センターが Azure Windows Server VM にインストールされている場合

* [Windows のバージョンを確認する](#check-the-windows-version)
* HTTPS の受信ポート規則を追加しましたか 
* [Azure VM への Windows 管理センターのインストールについての詳細情報](https://docs.microsoft.com/windows-server/manage/windows-admin-center/configure/azure-integration#use-a-windows-admin-center-gateway-deployed-in-azure)

### <a name="check-the-windows-version"></a>Windows のバージョンを確認します。

* [ファイル名を指定して実行] ダイアログを開き (Windows キー + R)、```winver``` を起動します。

* Windows 10 バージョン 1703 以下を使用している場合、Windows Admin Center はお使いのバージョンの Microsoft Edge ではサポートされません。 最新バージョンの Windows 10 にアップグレードするか、Chrome を使用します。

* Windows 10 または17134と17637の間にビルドバージョンがあるサーバーを使用している場合は、windows 管理センターで障害が発生する原因となったバグが Windows にあります。 現在サポートされているバージョンの Windows を使用してください。

### <a name="make-sure-the-windows-remote-management-winrm-service-is-running-on-both-the-gateway-machine-and-managed-node"></a>ゲートウェイコンピューターと管理ノードの両方で Windows リモート管理 (WinRM) サービスが実行されていることを確認します。

* WindowsKey + R を使用して [実行] ダイアログを開く
* 「@No__t-0」と入力し、enter キーを押します。
* 開いたウィンドウで Windows リモート管理 (WinRM) を探し、それが実行中であり、自動的に開始するように設定されていることを確認します。

### <a name="did-you-upgrade-your-server-from-2016-to-2019"></a>サーバーを2016から2019にアップグレードしましたか?

* これにより、信頼されたホストの設定がクリアされた可能性があります。 [信頼されたホストの設定を更新するには、次の手順に従います。](#configure-trustedhosts) 

## <a name="i-get-the-message-cant-connect-securely-to-this-page-this-might-be-because-the-site-uses-outdated-or-unsafe-tls-security-settings"></a>次のメッセージが表示されます。"このページに安全に接続できません。 これは、サイトで TLS セキュリティ設定が古くなっているか、安全でないことが原因である可能性があります。

コンピューターは、HTTP/2 接続に制限されています。 Windows 管理センターでは、HTTP/2 でサポートされていない統合 Windows 認証が使用されます。 **ブラウザーを実行しているコンピューター**の ```HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Http\Parameters``` キーの下に次の2つのレジストリ値を追加して、HTTP/2 の制限を削除します。

```
EnableHttp2Cleartext=dword:00000000
EnableHttp2Tls=dword:00000000
```

## <a name="im-having-trouble-with-the-remote-desktop-events-and-powershell-tools"></a>リモートデスクトップ、イベント、PowerShell ツールで問題が発生しています。

これら3つのツールには websocket プロトコルが必要です。これは通常、プロキシサーバーとファイアウォールによってブロックされます。 Google Chrome を使用している場合は、websocket と NTLM 認証に関する[既知の問題](known-issues.md#google-chrome)があります。

## <a name="i-can-connect-to-some-servers-but-not-others"></a>一部のサーバーに接続できるが、他のサーバーには接続できない

* ゲートウェイコンピューターにローカルでログオンし、PowerShell で ```Enter-PSSession <machine name>``` を試行します。 \<machine name > を Windows 管理センターで管理しようとしているコンピューターの名前に置き換えます。 

* 環境でドメインの代わりにワークグループを使用している場合は、「[ワークグループでの Windows Admin Center の使用](#using-windows-admin-center-in-a-workgroup)」を参照してください。

* **ローカル管理者アカウントを使用する場合:** 組み込みの administrator アカウントではないローカルユーザーアカウントを使用している場合は、PowerShell で次のコマンドを実行するか、ターゲットコンピューターで管理者としてコマンドプロンプトを実行して、ターゲットコンピューターでポリシーを有効にする必要があります。

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

**PowerShell コマンドを使用して TrustedHosts を変更するには:**

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

## <a name="i-previously-had-windows-admin-center-installed-and-now-nothing-else-can-use-the-same-tcpip-port"></a>以前は Windows 管理センターがインストールされていましたが、それ以外は同じ TCP/IP ポートを使用できません。

管理者特権のコマンドプロンプトで、次の2つのコマンドを手動で実行します。

```cmd
netsh http delete sslcert ipport=0.0.0.0:443
netsh http delete urlacl url=https://+:443/
```

## <a name="azure-features-dont-work-properly-in-edge"></a>Azure の機能がエッジで適切に動作しない

エッジには、Windows 管理センターでの Azure ログインに影響を与えるセキュリティゾーンに関連する[既知の問題](https://github.com/AzureAD/azure-activedirectory-library-for-js/wiki/Known-issues-on-Edge)があります。 Edge を使用しているときに Azure の機能を使用する際に問題が発生した場合は、クライアント側ブラウザーで、 https://login.microsoftonline.com 、 https://login.live.com 、ゲートウェイの URL を信頼済みサイトとして追加し、エッジポップアップブロックの設定で許可されたサイトに追加してみてください。 

これを行うには :
1. Windows の スタート メニューの **インターネットオプション** を検索します。
2. **[セキュリティ]** タブにアクセスします。
3. **[信頼済みサイト]** オプションで、 **[サイト]** ボタンをクリックし、表示されるダイアログボックスに url を追加します。 ゲートウェイの URL と https://login.microsoftonline.com および https://login.live.com を追加する必要があります。
4. **[プライバシー]** タブにアクセスします。
5. **[ポップアップブロック]** セクションで、 **[設定]** ボタンをクリックし、表示されるダイアログボックスに url を追加します。 ゲートウェイの URL と https://login.microsoftonline.com および https://login.live.com を追加する必要があります。

## <a name="having-an-issue-with-an-azure-related-feature"></a>Azure 関連の機能に問題がある場合は、

@No__t-0 で、次の情報を含む電子メールをお送りください。
* [以下に記載されている質問](#providing-feedback-on-issues)の一般的な問題情報。
* 問題とその再現手順について説明します。 
* New-AadApp ダウンロード可能なスクリプトを使用してゲートウェイを Azure に登録した後、バージョン1807にアップグレードしましたか? または、ゲートウェイ設定の UI を使用して azure > azure にゲートウェイを登録しましたか?
* Azure アカウントは複数のディレクトリ/テナントに関連付けられていますか?
    * [はい] の場合:Windows 管理センターに Azure AD アプリケーションを登録するときに、Azure で既定のディレクトリを使用していたディレクトリはありますか。 
* Azure アカウントは複数のサブスクリプションにアクセスできますか。
* 使用していたサブスクリプションに課金が適用されていますか?
* 問題が発生したときに複数の Azure アカウントにログインしましたか?
* Azure アカウントは多要素認証を必要としますか。
* Azure VM を管理しようとしているマシンはありますか?
* Windows 管理センターは Azure VM にインストールされていますか?

## <a name="providing-feedback-on-issues"></a>問題に関するフィードバックの提供

[イベント ビューアー] > [アプリケーションとサービス] > [Microsoft-ServerManagementExperience] の順に移動し、エラーまたは警告がないか探します。

問題について説明している [UserVoice](https://windowsserver.uservoice.com/forums/295071/category/319162?query=%5BBug%5D) で問題を登録します。

イベント ログで見つけたエラーまたは警告、および次の情報を含めてください。 

* Windows Admin Center が**インストールされている**プラットフォーム (Windows 10 または Windows Server):
    * サーバーにインストールされている場合、Windows 管理センターにアクセスするには、**ブラウザーを実行**しているコンピューターの windows[バージョン](#check-the-windows-version)は次のようになります。 
    * インストーラーによって作成された自己署名証明書を使用していますか?
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

