---
title: Server Core の管理
description: Windows Server の Server Core インストールの管理方法について説明します。
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.author: elizapo
ms.localizationpriority: medium
ms.date: 12/18/2018
ms.openlocfilehash: 8eba1e081c57c1c668a4e52ecb85fb4716a36fdc
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87895910"
---
# <a name="administer-a-server-core-server"></a>Server Core サーバーの管理

>適用対象: Windows Server 2019、Windows Server 2016、および Windows Server (半期チャネル)

Server Core には UI がないため、基本的な管理タスクを実行するには、Windows PowerShell コマンドレット、コマンドラインツール、またはリモートツールを使用する必要があります。 以下のセクションでは、基本的なタスクに使用する PowerShell コマンドレットとコマンドの概要について説明します。 また、現在パブリックプレビュー中の統合された管理ポータルである[Windows 管理センター](../../manage/windows-admin-center/overview.md)を使用して、のインストールを管理することもできます。

## <a name="administrative-tasks-using-powershell-cmdlets"></a>PowerShell コマンドレットを使用した管理タスク
Windows PowerShell コマンドレットを使用して基本的な管理タスクを実行するには、次の情報を使用します。

### <a name="set-a-static-ip-address"></a>静的 IP アドレスを設定する
Server Core サーバーをインストールすると、既定では DHCP アドレスが使用されます。 静的 IP アドレスが必要な場合は、次の手順を使用して設定できます。

現在のネットワーク構成を表示するには、 **Get Ne? configuration**を使用します。

既に使用している IP アドレスを表示するには、 **new-netipaddress**を使用します。

静的 IP アドレスを設定するには、次の手順を実行します。

1. **Get Ne? インターフェイス**を実行します。
2. IP インターフェイスまたは**Interfacedescription**文字列の**IfIndex**列の番号に注意してください。 複数のネットワークアダプターがある場合は、静的 IP アドレスを設定するインターフェイスに対応する数値または文字列をメモします。
3. 次のコマンドレットを実行して、静的 IP アドレスを設定します。

   ```powershell
   New-NetIPaddress -InterfaceIndex 12 -IPAddress 192.0.2.2 -PrefixLength 24 -DefaultGateway 192.0.2.1
   ```

   各値の説明:
   - **InterfaceIndex**は、手順 2. の**IfIndex**の値です。 (この例では 12)
   - **IPAddress**は、設定する静的 IP アドレスです。 (この例では、191.0.2.2)
   - [**プレフィックス] は、** 設定する IP アドレスのプレフィックス長 (別の形式のサブネットマスク) です。 (この例では、24)
   - **DefaultGateway**は、デフォルトゲートウェイの IP アドレスです。 (この例では、192.0.2.1)
4. 次のコマンドレットを実行して、DNS クライアントサーバーのアドレスを設定します。

   ```powershell
   Set-DNSClientServerAddress –InterfaceIndex 12 -ServerAddresses 192.0.2.4
   ```

   各値の説明:
   - **InterfaceIndex**は、手順 2. の IfIndex の値です。
   - **Serveraddresses**は、DNS サーバーの IP アドレスです。
5. 複数の DNS サーバーを追加するには、次のコマンドレットを実行します。

   ```powershell
   Set-DNSClientServerAddress –InterfaceIndex 12 -ServerAddresses 192.0.2.4,192.0.2.5
   ```

   この例では、 **192.0.2.4 と 192.0.2.5**と**です。** は両方とも DNS サーバーの IP アドレスです。

DHCP の使用に切り替える必要がある場合は、 **Set-DnsClientServerAddress – InterfaceIndex 12 – ResetServerAddresses**を実行します。

### <a name="join-a-domain"></a>ドメインに参加する
コンピューターをドメインに参加させるには、次のコマンドレットを使用します。

1. **コンピューターの追加**を実行します。 ドメインに参加するための資格情報とドメイン名の両方を入力するように求められます。
2. ローカルの Administrators グループにドメインユーザーアカウントを追加する必要がある場合は、コマンドプロンプトで次のコマンドを実行します (PowerShell ウィンドウではありません)。

   ```
   net localgroup administrators /add <DomainName>\<UserName>
   ```
3. コンピューターを再起動します。 これを行うには、**コンピューターの再起動**を実行します。

### <a name="rename-the-server"></a>サーバー名を変更する
サーバーの名前を変更するには、次の手順に従います。

1. **hostname** または **ipconfig** コマンドで現在のサーバー名を確認します。
2. コンピューター名の** \<new_name\> 変更を**実行します。
3. コンピューターを再起動します。

### <a name="activate-the-server"></a>サーバーのライセンス認証をする

**Slmgr.vbs – ipk \<productkey\> **を実行します。 次に、 **slmgr.vbs – ato**を実行します。 アクティブ化が成功した場合、メッセージは表示されません。

> [!NOTE]
> また、[キー管理サービス (KMS) サーバー](../../get-started/server-2016-activation.md)を使用して、またはリモートで、サーバーを電話でアクティブ化することもできます。 リモートからライセンス認証するには、リモートコンピューターから次のコマンドレットを実行します。
>
> ```
> cscript windows\system32\slmgr.vbs <ServerName> <UserName> <password>:-ato
> ```

### <a name="configure-windows-firewall"></a>Windows ファイアウォールの構成

Windows PowerShell コマンドレットとスクリプトを使用して、Windows ファイアウォールを Server Core コンピューターにローカルに構成できます。 Windows ファイアウォールの構成に使用できるコマンドレットについては、「 [Netsecurity](/powershell/module/netsecurity/?view=win10-ps) 」を参照してください。

### <a name="enable-windows-powershell-remoting"></a>Windows PowerShell のリモート処理を有効にする

Windows PowerShell のリモート処理を有効にすることができます。Windows PowerShell のリモート処理では、あるコンピューターで入力したコマンドが別のコンピューターで実行されます。 **Enable-psremoting**を使用して Windows PowerShell リモート処理を有効にします。

詳細については、「[リモートの FAQ につい](/powershell/module/microsoft.powershell.core/about/about_remote_faq?view=powershell-5.1)て」を参照してください。

## <a name="administrative-tasks-from-the-command-line"></a>コマンドラインからの管理タスク
コマンドラインから管理タスクを実行するには、次の参照情報を使用します。

### <a name="configuration-and-installation"></a>構成とインストール

|                             タスク                              |                                                                                                                                                                                                                 command                                                                                                                                                                                                                 |
|---------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|             ローカルの管理パスワードを設定する             |                                                                                                                                                                                                      **net ユーザー管理者**\*                                                                                                                                                                                                      |
|                  コンピューターのドメインへの参加                  |                                                                                                                                                       **netdom join% computername%** **/domain: \<domain\> /userd: \<domain\\username\> /passwordd:**\* <br> コンピューターを再起動します。                                                                                                                                                        |
|              ドメインが変更されたことを確認する              |                                                                                                                                                                                                                 **set**                                                                                                                                                                                                                 |
|                コンピューターをドメインから削除する                |                                                                                                                                                                                                   **netdom の削除\<computername\>**                                                                                                                                                                                                    |
|         ローカルの Administrators グループにユーザーを追加する          |                                                                                                                                                                                       **net localgroup 管理者/add\<domain\\username\>**                                                                                                                                                                                       |
|       ローカルの Administrators グループからユーザーを削除する       |                                                                                                                                                                                     **net localgroup 管理者/delete\<domain\\username\>**                                                                                                                                                                                      |
|               ローカル コンピューターにユーザーを追加する                |                                                                                                                                                                                                **net user \<domain\username\> \* /add**                                                                                                                                                                                                 |
|               ローカル コンピューターにグループを追加する               |                                                                                                                                                                                                 **net localgroup \<group name\> /add**                                                                                                                                                                                                  |
|          ドメインに参加しているコンピューターの名前を変更する          |                                                                                                                                                           **netdom renamecomputer% computername%/newname: \<new computer name\> /userd: \<domain\\username\> /passwordd:**\*                                                                                                                                                            |
|                 新しいコンピューター名を確認する                 |                                                                                                                                                                                                                 **set**                                                                                                                                                                                                                 |
|         ワーク グループ内のコンピューターの名前を変更する         |                                                                                                                                                                **netdom renamecomputer \<currentcomputername\> /newname:\<newcomputername\>** <br>コンピューターを再起動します。                                                                                                                                                                 |
|                ページング ファイルの管理を無効にする                 |                                                                                                                                                                        **wmic computersystem (name = " \<computername\> ") set 自動ページファイル = False**                                                                                                                                                                         |
|                   ページング ファイルを構成する                   |                                                            **wmic pagefileset where name = " \<path/filename\> " Set = \<initialsize\> , MaximumSize =\<maxsize\>** <br>*Path/filename*はページングファイルのパスと名前、 *initialsize*はページングファイルの開始サイズ (バイト単位)、 *maxsize*はページファイルの最大サイズ (バイト単位) です。                                                             |
|                 静的 IP アドレスに変更する                 | **ipconfig/all** <br>関連する情報を記録するか、テキストファイルにリダイレクトします (**ipconfig/all >ipconfig.txt**)。<br>**netsh interface ipv4 show インターフェイス**<br>インターフェイスリストがあることを確認します。<br>**netsh インターフェイス ipv4 set アドレス \<Name ID from interface list\> ソース = 静的アドレス = \<preferred IP address\> ゲートウェイ =\<gateway address\>**<br>**Ipconfig/all**を実行して、DHCP Enabled が**No**に設定されていることを確認します。 |
|                   静的 DNS アドレスを設定します。                   |   <strong>netsh interface ipv4 add dnsserver name = \<name or ID of the network interface card\> address = \<IP address of the primary DNS server\> index = 1 <br></strong>netsh interface ipv4 add dnsserver name = \<name of secondary DNS server\> address = \<IP address of the secondary DNS server\> index = 2\*\* <br> 必要に応じて、サーバーを追加します。<br>**Ipconfig/all**を実行して、アドレスが正しいことを確認します。   |
| 静的 IP アドレスから DHCP によって提供された IP アドレスに変更する |                                                                                                                                      **netsh interface ipv4 set address name = \<IP address of local system\> source = DHCP** <br>**Ipconfig/all**を実行して、DCHP Enabled が**Yes**に設定されていることを確認します。                                                                                                                                      |
|                      プロダクト キーを入力する                      |                                                                                                                                                                                                   **slmgr.vbs – ipk\<product key\>**                                                                                                                                                                                                    |
|                  サーバーをローカルにライセンス認証する                  |                                                                                                                                                                                                           **slmgr.vbs-ato**                                                                                                                                                                                                            |
|                 サーバーをリモートからライセンス認証する                  |                                            **cscript slmgr.vbs-ipk\<product key\>\<server name\>\<username\>\<password\>** <br>**cscript slmgr.vbs-ato \<servername\> \<username\>\<password\>** <br>**Cscript slmgr.vbs**を実行してコンピューターの GUID を取得する <br> **Cscript slmgr.vbs の実行 \<GUID\> -dli** <br>ライセンスステータスが "ライセンス済み **(アクティブ化済み)**" に設定されていることを確認します。                                             |

### <a name="networking-and-firewall"></a>ネットワークとファイアウォール

|タスク|command|
|----|-------|
|プロキシサーバーを使用するようにサーバーを構成する|**netsh Winhttp set proxy \<servername\> :\<port number\>** <br>**注:** Server Core インストールでは、接続を許可するためにパスワードを必要とするプロキシ経由でインターネットにアクセスすることはできません。|
|インターネットアドレスのプロキシをバイパスするようにサーバーを構成する|**netsh winhttp set proxy \<servername\> : \<port number\> バイパスリスト = " \<local\> "**|
|IPSEC 構成を表示または変更する|**netsh ipsec**|
|NAP 構成を表示または変更する|**netsh nap**|
|IP から物理アドレスへの変換を表示または変更する|**arp**|
|ローカルルーティングテーブルを表示または構成する|**route**|
|DNS サーバーの設定を表示または構成する|**nslookup**|
|プロトコル統計と現在の TCP/IP ネットワーク接続を表示する|**netstat**|
|NetBIOS over TCP/IP (NBT) を使用してプロトコル統計と現在の TCP/IP 接続を表示する|**nbtstat**|
|ネットワーク接続のホップを表示する|**pathping**|
|ネットワーク接続のホップをトレースする|**tracert**|
|マルチキャスト ルーターの構成を表示する|**mrinfo**|
|ファイアウォールのリモート管理を有効にする|**netsh advfirewall firewall set rule group = "Windows Defender ファイアウォールリモート管理" 新しい有効化 = はい**|


### <a name="updates-error-reporting-and-feedback"></a>更新プログラム、エラー報告、およびフィードバック

|                               タスク                                |                                                                                                                               command                                                                                                                                |
|-------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                         更新プログラムをインストールする                         |                                                                                                                    **wusa \<update\> /quiet**                                                                                                                    |
|                      インストールされている更新プログラムの一覧を表示する                       |                                                                                                                            **systeminfo**                                                                                                                            |
|                         更新プログラムを削除する                          |                                 **展開/f: \* \<update\> .msu c:\test** <br>c:\test\ に移動して \<update\>.xml をテキスト エディターで開きます。<br>[**インストール**] を [**削除**] に置き換えて、ファイルを保存します。<br>**pkgmgr/n: \<update\> .xml**                                 |
|                    自動更新を構成する                    |          現在の設定を確認するには: **cscript%systemroot%\system32\scregedit.wsf/au/v 自動更新を有効にするには、 \* \* <br> \* \* cscript scregedit.exe/au 4** <br>自動更新を無効にするには: **cscript%systemroot%\system32\scregedit.wsf/AU 1**          |
|                      エラー報告を有効にする                       | 現在の設定を確認するには: **serverWerOptin/query** <br>詳細レポートを自動的に送信するには: **serverWerOptin/detailed** <br>概要レポートを自動的に送信するには: **serverWerOptin/summary** <br>エラー報告を無効にするには: **serverWerOptin/disable** |
| カスタマー エクスペリエンス向上プログラム (CEIP) に参加する |                                                     現在の設定を確認するには: **serverCEIPOptin/query** <br>CEIP を有効にするには: **serverCEIPOptin/enable** <br>CEIP を無効にするには: **serverCEIPOptin/disable**                                                      |

### <a name="services-processes-and-performance"></a>サービス、プロセス、およびパフォーマンス

|                               タスク                               |                                                                                                                                                                                                             command                                                                                                                                                                                                              |
|------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                    実行中のサービスを一覧表示する                     |                                                                                                                                                                                                  **sc クエリ**または**net start**                                                                                                                                                                                                   |
|                         サービスを開始する                          |                                                                                                                                                                                 **sc の \<service name\> 開始**または**net \<service name\> start**                                                                                                                                                                                  |
|                          サービスを停止する                          |                                                                                                                                                                                  **sc の \<service name\> 停止**または**net \<service name\> stop**                                                                                                                                                                                   |
| 実行中のアプリケーションと関連するプロセスの一覧を取得する |                                                                                                                                                                                                           **tasklist**                                                                                                                                                                                                           |
|                        タスク マネージャーを開始する                        |                                                                                                                                                                                                           **taskmgr-networking**                                                                                                                                                                                                            |
|    イベントトレースセッションとパフォーマンスログの作成と管理    | カウンター、トレース、構成データの収集、API を作成するには **、次のように**します。 <br>データコレクターのプロパティを照会するには: **logman クエリ** <br>データ収集を開始または停止するには: **logman start \| stop** <br>コレクターを削除するには: **logman delete** <br> コレクターのプロパティを更新するには: **logman update** <br>XML ファイルからデータコレクターセットをインポートする、または XML ファイルにエクスポートするには: **logman インポート \| エクスポート** |

### <a name="event-logs"></a>イベント ログ

|タスク|command|
|----|-------|
|イベントログの一覧表示|**wevtutil el**|
|指定されたログのイベントを照会する|**wevtutil qe/f: テキスト\<log name\>**|
|イベントログをエクスポートする|**wevtutil epl\<log name\>**|
|イベントログの消去|**wevtutil cl\<log name\>**|


### <a name="disk-and-file-system"></a>ディスクとファイル システム

|                   タスク                   |                        command                        |
|------------------------------------------|-------------------------------------------------------|
|          ディスク パーティションを管理する          | コマンドの完全な一覧を表示するには、 **diskpart/?** を実行します。  |
|           ソフトウェアの RAID を管理する           | コマンドの完全な一覧を表示するには、 **diskraid/?** を実行します。  |
|        ボリューム マウント ポイントを管理する        | コマンドの完全な一覧を表示するには、 **mountvol/?** を実行します。  |
|           ボリュームを最適化する            |  コマンドの完全な一覧を表示するには、 **defrag/?** を実行します。   |
| ボリュームを NTFS ファイル システムに変換する |        **/Fs の変換 \<volume letter\> : NTFS**         |
|              ファイルを圧縮する              |  コマンドの完全な一覧を表示するには、 **compact/?** を実行します。  |
|          開いているファイルを管理する           | コマンドの完全な一覧については、「 **openfiles/?** 」を実行してください。 |
|          VSS フォルダーを管理する          | コマンドの完全な一覧については、「 **vssadmin/?** 」を実行してください。  |
|        ファイル システムを管理する        |  コマンドの完全な一覧を表示するには、 **fsutil/?** を実行します。   |
|    ファイルまたはフォルダーの所有権を取得する    |  コマンドの完全な一覧を表示するには、 **icacls/?** を実行します。   |

### <a name="hardware"></a>ハードウェア

|タスク|command|
|----|-------|
|新しいハードウェア デバイスのドライバーを追加する|% Homedrive% のフォルダーにドライバーをコピーし \\ \<driver folder\> ます。 Pnputil の実行 **-i-a% homedrive% \\ \<driver folder\> \\ \<driver\> .inf**|
|ハードウェア デバイスのドライバーを削除する|読み込まれたドライバーの一覧を表示するには、 **sc query type = driver**を実行します。 その後、 **sc \<service_name\> delete**を実行します。|
