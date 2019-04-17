---
title: Windows Admin Center の一般的なトラブルシューティングの手順
description: Windows Admin Center の一般的なトラブルシューティングの手順 (Project Honolulu)
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 02/12/2019
ms.openlocfilehash: a91a8dcf6f05ef0ef66dee603851150b2145d559
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297082"
---
# Windows Admin Center のトラブルシューティング

>適用対象: Windows Admin Center、Windows Admin Center Preview

> [!Important]
> このガイドは、Windows Admin Center を使用できない原因となっている問題を診断および解決するのに役立ちます。 特定のツールで問題が発生している場合は、[既知の問題](http://aka.ms/wacknownissues)が発生しているかどうかを確認してください。

<a id="toc"></a>

## クイック リンク

* [メッセージ、インストーラーが失敗した場合: ** _、モジュール 'Microsoft.PowerShell.LocalAccounts' が読み込まれていない可能性があります_。**](#psmodulepath)

* Web ブラウザーで **This site/page can't be reached** (このサイト/ページに到達できません) というエラーが表示される (展開の種類を選択してください)
    * [Windows 10 のアプリとして Windows Admin Center をインストールしている](#whitescreenw10)
    * [Windows Server でのゲートウェイとして Windows Admin Center をインストールしている](#whitescreenws)
    * [Azure VM でのゲートウェイとして Windows Admin Center をインストールしている](#whitescreenazvm)

* [Windows Admin Center のホーム ページに読み込まれるが [画面で動かなくなる、接続の追加、または任意のコンピューターに接続できません。](#winvercompat)

* ["Error while loading the module. Rpc: Expired retries 'Ping'" (モジュールの読み込み中にエラーが発生しました。Rpc: 'Ping' の再試行の有効期限が切れました) というメッセージが表示される](#winvercompat)

* [メッセージが表示:"はこのページに安全に接続します。 これは、可能性があります、サイトが古いか安全でない TLS セキュリティ設定を使用します。"](#tls)

* [リモート デスクトップ、イベント、および PowerShell ツールで問題があります。](#websockets)

* [Edge で Azure 機能を使用して、問題があります。](#azlogin)

* [一部のサーバーに接続できるが、他のサーバーには接続できない](#connectionissues)

* [**ワークグループ**で Windows Admin Center を使用している](#workgroup)

* [いた Windows Admin Center をインストール、および同じ TCP/IP ポートを使用して他に何もできるようになりました](#urlacl)

* [自分の問題がここに記載されていないか、このページの手順で問題が解決しなかった。](#filebug)

<a id="psmodulepath"></a>

## メッセージのインストーラーが失敗した場合: ** _、モジュール 'Microsoft.PowerShell.LocalAccounts' が読み込まれていない可能性があります_。**

これは、既定の PowerShell モジュールのパスが変更または削除された場合に発生することができます。 問題を解決することを確認```%SystemRoot%\system32\WindowsPowerShell\v1.0\Modules```PSModulePath 環境変数には、**最初**の項目です。 PowerShell の次の行で、これを実現することができます。

```powershell
[Environment]::SetEnvironmentVariable("PSModulePath","%SystemRoot%\system32\WindowsPowerShell\v1.0\Modules;" + ([Environment]::GetEnvironmentVariable("PSModulePath","User")),"User")
```

## Web ブラウザーで  **This site/page can't be reached** (このサイト/ページに到達できません) というエラーが表示される

<a id="whitescreenw10"></a>

### **Windows 10 のアプリ**として Windows Admin Center をインストールしている場合

* Windows Admin Center が実行されていることを確認します。 Windows Admin Center アイコンを探します![](../media/trayIcon.PNG)システム トレイのまたは**Windows Admin Center デスクトップ/SmeDesktop.exe**タスク マネージャーにします。 見つからない場合は、[スタート] メニューから **Windows Admin Center** を起動します。

> [!NOTE] 
> 再起動後、[スタート] メニューから Windows Admin Center を起動する必要があります。  

* [Windows のバージョンを確認します。](#winvercompat)

* Web ブラウザーとして Microsoft Edge または Google Chrome のいずれかを使用していることを確認します。

* [最初の起動](../use/get-started.md#selecting-a-client-certificate)時に正しい証明書を選択しましたか。

  * プライベート セッションでブラウザーを開いてみてください。問題が解決したら、キャッシュをクリアする必要があります。

* でした最近にアップグレードする Windows 10 のバージョンの新しいビルドかどうか。

  * これが、信頼されたホストの設定をオフに可能性があります。 [信頼されたホストの設定を更新する次の手順に従います。](#configure-trustedhosts) 

[[先頭に戻る]](#toc)

<a id="whitescreenws"></a>

### **Windows Server でのゲートウェイ**として Windows Admin Center をインストールした場合

* Windows Admin Center の以前のバージョンからアップグレードでしたか。 [この既知の問題](known-issues.md#upgrade)により、ファイアウォール規則が削除されていないことを確認します。 ルールが存在するかを判断するのにには、次の PowerShell コマンドを使用します。 必要でない場合は、それを再作成する[次の手順](known-issues.md#upgrade)に従います。
    ```powershell
    Get-NetFirewallRule -DisplayName "SmeInboundOpenException"
    ```

* クライアントとサーバーの [Windows バージョン](#winvercompat) を確認します。

* Web ブラウザーとして Microsoft Edge または Google Chrome のいずれかを使用していることを確認します。

* サーバーで、[タスク マネージャー _gt サービスを開き、確認**ServerManagementGateway/Windows Admin Center**が実行されています。
![](../media/Service-TaskMan.PNG)

* ゲートウェイへのネットワーク接続をテストします (<values> を自身の展開の情報に置き換えます)
    ```powershell
    Test-NetConnection -Port <port> -ComputerName <gateway> -InformationLevel Detailed
    ```

[[先頭に戻る]](#toc)

<a id="whitescreenazvm"></a>  

### Azure Windows Server VM に Windows Admin Center をインストールした場合

* [Windows のバージョンを確認します。](#winvercompat)
* HTTPS の受信ポート規則を追加しましたか 
* [Azure VM へのWindows Admin Center のインストールの詳細を確認してください](https://docs.microsoft.com/windows-server/manage/windows-admin-center/configure/azure-integration#use-a-windows-admin-center-gateway-deployed-in-azure)

[[先頭に戻る]](#toc)

<a id="winvercompat"></a>

### Windows のバージョンを確認します。

* [ファイル名を指定して実行] ダイアログを開き (Windows キー + R)、```winver``` を起動します。

* Windows 10 バージョン 1703 以下を使用している場合、Windows Admin Center はお使いのバージョンの Microsoft Edge ではサポートされません。 最新バージョンの Windows 10 にアップグレードするか、Chrome を使用します。

* 17134 と 17637 の間でビルド バージョンを Windows 10 または Server の insider preview バージョンを使用する場合、Windows には、Windows Admin Center が失敗の原因となったバグが必要があります。 現在サポートされているバージョンの Windows を使用してください。

### Windows リモート管理 (WinRM) サービスが、ゲートウェイ マシンと管理ノードで実行されているかどうかを確認します。

* WindowsKey + R と実行] ダイアログを開く
* 型```services.msc```し、enter キーを押します
* Windows リモート管理 (WinRM) の外観、ウィンドウが開き、確認が実行されていることと、自動的に開始するよう設定

### でしたにアップグレードする、server 2016 から 2019年かどうか。

* これが、信頼されたホストの設定をオフに可能性があります。 [信頼されたホストの設定を更新する次の手順に従います。](#configure-trustedhosts) 

[[先頭に戻る]](#toc)

<a id="tls"></a>

## メッセージが表示:"はこのページに安全に接続します。 サイトが古いか安全でない TLS セキュリティの設定を使っている可能性があります。

<!--REF: https://docs.microsoft.com/iis/get-started/whats-new-in-iis-10/http2-on-iis#when-is-http2-not-supported -->
コンピューターは、http/2 接続に制限されます。 Windows Admin Center は、統合 Windows 認証では、http/2 でサポートされていないを使用します。 次の 2 つのレジストリ値を追加、 ```HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Http\Parameters``` http/2 の制限を解除する **、ブラウザーを実行しているコンピューター**でキー。

```
EnableHttp2Cleartext=dword:00000000
EnableHttp2Tls=dword:00000000
```

[[先頭に戻る]](#toc)

<a id="websockets"></a> 

## リモート デスクトップ、イベント、および PowerShell ツールで問題があります。

これら 3 つのツールでは、websocket プロトコル、プロキシ サーバーとファイアウォールでよくブロックされている必要があります。 Google Chrome を使用している場合は、[既知の問題](known-issues.md#google-chrome)に関する websocket および NTLM 認証します。

[[先頭に戻る]](#toc)


<a id="connectionissues"></a> 

## 一部のサーバーに接続できるが、他のサーバーには接続できない
* ゲートウェイ マシンにローカルでログオンし、PowerShell で ```Enter-PSSession <machine name>``` を実行します。<machine name> は Windows Admin Center で管理しようとしているマシンの名前に置き換えます。 

* 環境でドメインの代わりにワークグループを使用している場合は、「[ワークグループでの Windows Admin Center の使用](#workgroup)」を参照してください。

* **ローカル管理者アカウントの使用:** ビルトイン Administrator アカウントではないローカル ユーザー アカウントを使用している場合は、PowerShell で、またはターゲット コンピューターで管理者としてコマンド プロンプトで次のコマンドを実行して、ターゲット コンピューターでポリシーを有効にする必要があります。

        REG ADD HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1


[[先頭に戻る]](#toc)

<a id="workgroup"></a>

## ワークグループでの Windows Admin Center の使用 

### 使用しているアカウント
使用している資格情報が、対象サーバーのローカル管理者グループのメンバーであることを確認します。 場合によっては、WinRM で Remote Management Users グループでのメンバーシップも必要になります。 **ビルトイン Administrator アカウントではない**ローカル ユーザー アカウントを使用している場合は、PowerShell で、またはターゲット コンピューターで管理者としてコマンド プロンプトで次のコマンドを実行して、ターゲット コンピューターでポリシーを有効にする必要があります。

```cmd
REG ADD HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1
```
### 異なるサブネットでワークグループ コンピューターに接続している場合

ゲートウェイと同じサブネット上にないワークグループ コンピューターに接続するには、WinRM (TCP 5985) のファイアウォール ポートにより、ターゲット コンピューターで受信トラフィックが許可されていることを確認します。 PowerShell で、またはターゲット コンピューターで管理者としてコマンド プロンプトで次のコマンドを実行して、このファイアウォール規則を作成することができます。

- **Windows Server**

    ```powershell
    Set-NetFirewallRule -Name WINRM-HTTP-In-TCP-PUBLIC -RemoteAddress Any
    ```

- **Windows 10**

    ```powershell
    Set-NetFirewallRule -Name WINRM-HTTP-In-TCP -RemoteAddress Any
    ```

### TrustedHosts の構成

Windows Admin Center のインストール時に、Windows Admin Center でゲートウェイの TrustedHosts 設定を管理できるように選択できます。 これは、ワークグループ環境またはドメインでローカル管理者の資格情報を使用している場合に必要です。 この設定を行わなかった場合は、TrustedHosts を手動で構成する必要があります。

**PowerShell コマンドを使用して TrustedHosts を変更するには:**

1. 管理者の PowerShell セッションを開きます。
2. 現在の TrustedHosts 設定を確認します。

    ```powershell
    Get-Item WSMan:\localhost\Client\TrustedHosts
    ```

    > [!WARNING]
    > TrustedHosts の現在の設定が空でない場合は、次のコマンドにより設定が上書きされます。 必要に応じて復元できるように、次のコマンドを使用して現在の設定をテキスト ファイルに保存することをお勧めします。

    > `Get-Item WSMan:localhost\Client\TrustedHosts | Out-File C:\OldTrustedHosts.txt`

3. TrustedHosts を、管理するコンピューターの NetBIOS、IP、または FQDN に設定します。

    ```powershell
    Set-Item WSMan:localhost\Client\TrustedHosts -Value '192.168.1.1,server01.contoso.com,server02'
    ```

    > [!TIP] 
    >すべての TrustedHosts を一度に設定する簡単な方法として、ワイルドカードを使用することができます。

    >     Set-Item WSMan:\localhost\Client\TrustedHosts -Value '*'

4. テストが完了したら、管理者特権の PowerShell セッションから次のコマンドを実行し、TrustedHosts 設定をクリアできます。

    ```powershell
    Clear-Item WSMan:localhost\Client\TrustedHosts
    ```

5. 以前に設定をエクスポートした場合は、ファイルを開いて値をコピーし、次のコマンドを使用します。

    ```powershell
    Set-Item WSMan:localhost\Client\TrustedHosts -Value '<paste values from text file>'
    ```

[[先頭に戻る]](#toc)

<a id="urlacl"></a>

## いた Windows Admin Center をインストール、および同じ TCP/IP ポートを使用して他に何もできるようになりました

手動で、管理者特権のコマンド プロンプトでこれら 2 つのコマンドを実行します。

```cmd
netsh http delete sslcert ipport=0.0.0.0:443
netsh http delete urlacl url=https://+:443/
```

[[先頭に戻る]](#toc)

<a id="azlogin"></a>

## Edge で Azure 機能を使用して、問題があります。

Edge では、[既知の問題](https://github.com/AzureAD/azure-activedirectory-library-for-js/wiki/Known-issues-on-Edge)に関連する Windows Admin Center で Azure ログインに影響を与えるセキュリティ ゾーンがあります。 Edge を使用する場合は、Azure の機能を使用して問題しない場合は、追加してみてくださいhttps://login.microsoftonline.com、https://login.live.comとして、ゲートウェイの URL が信頼済みサイト、およびクライアント側のブラウザーで Edge ポップアップ ブロックの設定のサイトを許可するとします。 

これには、次の手順を実行します。
1. Windows のスタート メニューの **[インターネット オプション**の検索
2. [**セキュリティ**] タブに移動します
3. [**信頼済みサイト**] では、**サイト**のボタンをクリックしを開く] ダイアログ ボックスで Url を追加します。 ゲートウェイ URL を追加する必要がありますだけでなくhttps://login.microsoftonline.comとhttps://login.live.comします。
4. [**プライバシー** ] タブに移動します
5. **ポップアップ ブロック**のセクションでは、[**設定**ボタンをクリックし、表示されるダイアログ ボックスで、Url を追加します。 ゲートウェイ URL を追加する必要がありますだけでなくhttps://login.microsoftonline.comとhttps://login.live.comします。


[[先頭に戻る]](#toc)

<a id="azissue"></a>

## Azure 関連の機能の問題があるかどうか。

お送りくださいメールで、次の情報と wacFeedbackAzure@microsoft.com:
* [質問を以下に](#filebug)一般的な問題の情報です。 
* 問題と、問題を再現するのにかかった時間の手順について説明します。 
* でした登録済みの新規 AadApp.ps1 ダウンロード可能なスクリプトを使用して Azure へのゲートウェイとバージョン 1807 にアップグレードしますか。 または、ゲートウェイ設定 _gt Azure から UI を使用して Azure へのゲートウェイを登録するために行ったかどうか。
* 複数のディレクトリ/テナントに関連付けられている Azure アカウントですか。
    * [はい]: Windows Admin Center を Azure AD アプリケーションを登録する場合が Azure で既定のディレクトリを使用したディレクトリかどうか。 
* Azure アカウントに複数のサブスクリプションへのアクセスがあるかどうか。
* 使用していたサブスクリプションには接続されている請求がありますか。
* されたで記録した複数の Azure アカウントに問題が発生したときですか。
* Azure アカウントには多要素認証が必要かどうか。
* Azure VM を管理しようとしているコンピューターとは
* Windows Admin Center は Azure VM にインストールされているかどうか。

[[先頭に戻る]](#toc)

<a id="filebug"></a>

## しない場合、または、問題がここに記載いないかどうか。 [よく寄せられる質問のトラブルシューティング]

[イベント ビューアー] > [アプリケーションとサービス] > [Microsoft-ServerManagementExperience] の順に移動し、エラーまたは警告がないか探します。

問題について説明している [UserVoice](https://windowsserver.uservoice.com/forums/295071/category/319162?query=%5BBug%5D) で問題を登録します。

イベント ログで見つけたエラーまたは警告、および次の情報を含めてください。 

* Windows Admin Center が**インストールされている**プラットフォーム (Windows 10 または Windows Server):
    * サーバーにインストールする場合は **、ブラウザーを実行しているコンピューター**に Windows Admin Center にアクセスするための Windows の[バージョン](#winvercompat)。 
    * インストーラーによって作成された自己署名証明書を使用しているかどうか。
    * 独自の証明書を使用している場合は、サブジェクト名とコンピューターが一致しますか。
    * 独自の証明書を使用している場合、別のサブジェクト名を指定していますか。
* 既定のポートの設定でインストールしましたか。
    * そうでない場合、どのポートを指定しましたか。
* Windows Admin Center が**インストールされている**コンピューターはドメインに参加していますか。
* Windows Admin Center が**インストールされている** Windows [バージョン](#winvercompat):
* **管理しようとしている**コンピューターはドメインに参加していますか。
* **管理しようとしている**コンピューターの Windows [バージョン](#winvercompat):
* どのブラウザーを使用していますか。
    * Google Chrome を使用している場合、バージョンは何ですか。 ([ヘルプ] > [Google Chromeについて])

[[先頭に戻る]](#toc)