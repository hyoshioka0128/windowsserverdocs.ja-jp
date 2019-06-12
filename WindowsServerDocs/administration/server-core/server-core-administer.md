---
title: Server Core を管理します。
description: Windows Server の Server Core インストールを管理する方法について説明します
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.author: elizapo
ms.localizationpriority: medium
ms.date: 12/18/2018
ms.openlocfilehash: 50fa737db5862132c1dde5cb6eb6b83674b3f02e
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66811387"
---
# <a name="administer-a-server-core-server"></a>Server Core サーバーを管理します。

>適用先:Windows Server (半期チャネル) および Windows Server 2016

Server Core では、UI があるないため、Windows PowerShell コマンドレット、コマンド ライン ツール、またはリモート ツールを使用して基本的な管理タスクを実行する必要があります。 次のセクションでは、PowerShell コマンドレットと基本的なタスクに使用されるコマンドを説明します。 使用することも[Windows Admin Center](../../manage/windows-admin-center/overview.md)、現在、インストールを管理する、パブリック プレビュー段階の統一された管理ポータル。 

## <a name="administrative-tasks-using-powershell-cmdlets"></a>PowerShell コマンドレットを使用して管理タスク
次の情報を使用すると、Windows PowerShell コマンドレットの基本的な管理タスクを実行できます。

### <a name="set-a-static-ip-address"></a>静的 IP アドレスを設定する
Server Core サーバーをインストールするときに既定では、DHCP アドレス。 静的 IP アドレスが必要な場合は、次の手順を使用して設定できます。

現在のネットワーク構成を表示する使用**Get NetIPConfiguration**します。

既に使用している IP アドレスを表示する使用**Get NetIPAddress**します。

静的 IP アドレスを設定するには、次の操作を行います。 

1. 実行**Get-netipinterface**します。 
2. 内の数に注意してください、 **IfIndex** IP インターフェイスの列、または**InterfaceDescription**文字列。 1 つ以上のネットワーク アダプターがある場合は、数またはの静的 IP アドレスを設定するインターフェイスに対応する文字列に注意してください。
3. 静的 IP アドレスを設定するのには、次のコマンドレットを実行します。

   ```powershell
   New-NetIPaddress -InterfaceIndex 12 -IPAddress 192.0.2.2 -PrefixLength 24 -DefaultGateway 192.0.2.1
   ```

   それぞれの文字の説明は次のとおりです。
   - **InterfaceIndex**の値である**IfIndex**から手順 2。 (ここでは、12)
   - **IPAddress**を設定する静的 IP アドレスです。 (ここでは、191.0.2.2)
   - **PrefixLength**プレフィックス長 (別の形式のサブネット マスク) を設定している IP アドレスです。 (たとえば、24)
   - **DefaultGateway**はデフォルト ゲートウェイに IP アドレスです。 (この例では 192.0.2.1) の
4. DNS クライアントにサーバーのアドレスを設定するには、次のコマンドレットを実行します。 

   ```powershell
   Set-DNSClientServerAddress –InterfaceIndex 12 -ServerAddresses 192.0.2.4
   ```
   
   それぞれの文字の説明は次のとおりです。
   - **InterfaceIndex**手順 2 の IfIndex の値です。
   - **ServerAddresses**は、DNS サーバーの IP アドレスです。
5. 複数の DNS サーバーを追加するには、次のコマンドレットを実行します。 

   ```powershell
   Set-DNSClientServerAddress –InterfaceIndex 12 -ServerAddresses 192.0.2.4,192.0.2.5
   ```

   この例では、where、 **192.0.2.4**と**192.0.2.5**は DNS サーバーの両方の IP アドレス。

かどうかは、DHCP、実行の使用に切り替える必要があります。 **Set-dnsclientserveraddress – InterfaceIndex 12 – ResetServerAddresses**します。

### <a name="join-a-domain"></a>ドメインに参加
次のコマンドレットを使用して、コンピューターをドメインに参加します。

1. 実行**Add-computer**します。 ドメインとドメイン名を結合する両方の資格情報を求めるメッセージが表示します。
2. ローカルの Administrators グループにドメイン ユーザー アカウントを追加する必要がある場合は、コマンド プロンプト (PowerShell ウィンドウ) ではなく、次のコマンドを実行します。

   ```
   net localgroup administrators /add <DomainName>\<UserName>
   ```
3. コンピューターを再起動します。 実行してこれを行う**Restart-computer**します。

### <a name="rename-the-server"></a>サーバー名を変更する
サーバーの名前を変更するのにには、次の手順を使用します。

1. **hostname** または **ipconfig** コマンドで現在のサーバー名を確認します。
2. 実行**Rename-computer-ComputerName \<new_name\>** します。
3. コンピューターを再起動します。

### <a name="activate-the-server"></a>サーバーのライセンス認証をする

実行**slmgr.vbs – ipk\<productkey\>** します。 実行して**slmgr.vbs – ato**します。 アクティブ化が成功すると、メッセージは取得されません。

> [!NOTE]
> サーバー上でアクティブ化することもできますを使用して、電話、[キー管理サービス (KMS) サーバー](../../get-started/server-2016-activation.md)、またはリモートでします。 をリモートでアクティブ化するには、リモート コンピューターから、次のコマンドレットを実行します。 
> 
> ```powershell
> **cscript windows\system32\slmgr.vbs <ServerName> <UserName> <password>:-ato**
> ```
 
### <a name="configure-windows-firewall"></a>Windows ファイアウォールを構成する

Windows PowerShell コマンドレットとスクリプトを使用して、Windows ファイアウォールを Server Core コンピューターにローカルに構成できます。 参照してください[NetSecurity](/powershell/module/netsecurity/?view=win10-ps)コマンドレットについては、Windows ファイアウォールの構成に使用することができます。

### <a name="enable-windows-powershell-remoting"></a>Windows PowerShell のリモート処理を有効にする

Windows PowerShell のリモート処理を有効にすることができます。Windows PowerShell のリモート処理では、あるコンピューターで入力したコマンドが別のコンピューターで実行されます。 Windows PowerShell リモート処理で有効にする**Enable-psremoting**します。

詳細については、次を参照してください。[リモート FAQ について](/powershell/module/microsoft.powershell.core/about/about_remote_faq?view=powershell-5.1)します。

## <a name="administrative-tasks-from-the-command-line"></a>管理タスクをコマンドラインから
コマンドラインから管理タスクを実行するのにには、次の参照情報を使用します。

### <a name="configuration-and-installation"></a>構成とインストール

|                             タスク                              |                                                                                                                                                                                                                 コマンド                                                                                                                                                                                                                 |
|---------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|             ローカルの管理パスワードを設定する             |                                                                                                                                                                                                      **net ユーザー管理者** \*                                                                                                                                                                                                      |
|                  コンピューターのドメインへの参加                  |                                                                                                                                                       **netdom join %computername%** **/domain:\<domain\> /userd:\<domain\\username\> /passwordd:** \* <br> コンピューターを再起動します。                                                                                                                                                        |
|              ドメインが変更されたことを確認する              |                                                                                                                                                                                                                 **set**                                                                                                                                                                                                                 |
|                コンピューターをドメインから削除する                |                                                                                                                                                                                                   **netdom remove \<computername\>**                                                                                                                                                                                                    |
|         ローカルの Administrators グループにユーザーを追加します。          |                                                                                                                                                                                       **net localgroup Administrators/add\<ドメイン\\ユーザー名\>**                                                                                                                                                                                       |
|       ローカルの Administrators グループからユーザーを削除する       |                                                                                                                                                                                     **net localgroup Administrators/delete\<ドメイン\\ユーザー名\>**                                                                                                                                                                                      |
|               ローカル コンピューターにユーザーを追加する                |                                                                                                                                                                                                **net user \<domain\username\> \* /add**                                                                                                                                                                                                 |
|               ローカル コンピューターにグループを追加する               |                                                                                                                                                                                                 **net localgroup\<グループ名\>/add**                                                                                                                                                                                                  |
|          ドメインに参加しているコンピューターの名前を変更する          |                                                                                                                                                           **netdom renamecomputer %computername% /NewName:\<new computer name\> /userd:\<domain\\username\> /passwordd:** \*                                                                                                                                                            |
|                 新しいコンピューター名を確認する                 |                                                                                                                                                                                                                 **set**                                                                                                                                                                                                                 |
|         ワーク グループ内のコンピューターの名前を変更する         |                                                                                                                                                                **netdom renamecomputer\<よび\>/NewName:\<newcomputername\>** <br>コンピューターを再起動します。                                                                                                                                                                 |
|                ページング ファイルの管理を無効にする                 |                                                                                                                                                                        **wmic computersystem 場所名 ="\<computername\>"AutomaticManagedPagefile 設定 = False**                                                                                                                                                                         |
|                   ページング ファイルを構成する                   |                                                            **wmic pagefileset 場所名 ="\<パス/ファイル名\>"InitialSize 設定 =\<initialsize\>、MaximumSize =\<maxsize\>** <br>場所*パス/ファイル名*へのパスと、ページング ファイルの名前は、 *initialsize*開始サイズ (バイト単位)、ページング ファイルのおよび*maxsize*の最大サイズは、ページのファイル (バイト単位)。                                                             |
|                 静的 IP アドレスに変更する                 | **ipconfig/all** <br>関連する情報を記録またはテキスト ファイルにリダイレクトする (**ipconfig/all > ipconfig.txt**)。<br>**netsh インターフェイスの ipv4 show インターフェイス**<br>インターフェイスの一覧があることを確認します。<br>**netsh interface ipv4 アドレスの名前を設定する\<インターフェイスの一覧から ID\>ソース静的アドレスを = =\<IP アドレスを優先\>ゲートウェイ =\<ゲートウェイ アドレス\>**<br>実行**ipconfig/all** DHCP を有効に設定されていることを確認する**いいえ**します。 |
|                   静的 DNS アドレスを設定します。                   |   <strong>netsh interface ipv4 dns サーバー名を追加する =\<ネットワーク インターフェイス カードの名前または ID\>アドレス =\<プライマリ DNS サーバーの IP アドレス\>インデックス = 1 <br></strong>netsh interface ipv4 dns サーバー名を追加する =\<セカンダリ DNS サーバーの名前\>アドレス =\<セカンダリ DNS サーバーの IP アドレス\>インデックス = 2\*\* <br> サーバーを追加するには必要に応じて繰り返します。<br>実行**ipconfig/all**アドレスが正しいことを確認します。   |
| 静的 IP アドレスから DHCP によって提供された IP アドレスに変更する |                                                                                                                                      **netsh interface ipv4 アドレスの名前を設定する =\<ローカル システムの IP アドレス\>ソース DHCP を =** <br>実行**ipconfig/all** DCHP を有効になっているに設定されていることを確認する**はい**。                                                                                                                                      |
|                      プロダクト キーを入力する                      |                                                                                                                                                                                                   **slmgr.vbs – ipk\<プロダクト キー\>**                                                                                                                                                                                                    |
|                  サーバーをローカルにライセンス認証する                  |                                                                                                                                                                                                           **slmgr.vbs -ato**                                                                                                                                                                                                            |
|                 サーバーをリモートからライセンス認証する                  |                                            **cscript slmgr.vbs – ipk\<プロダクト キー\>\<サーバー名\>\<username\>\<パスワード\>** <br>**cscript slmgr.vbs -ato \<servername\> \<username\> \<password\>** <br>実行して、コンピューターの GUID を取得**cscript slmgr.vbs-でした** <br> 実行**cscript slmgr.vbs-dli \<GUID\>** <br>ライセンスの状態に設定されていることを確認 **(アクティブ) ライセンス**します。                                             |

### <a name="networking-and-firewall"></a>ネットワークとファイアウォール

|タスク|コマンド| 
|----|-------|
|プロキシ サーバーを使用するようにサーバーを構成します。|**netsh Winhttp プロキシを設定する\<servername\>:\<ポート番号\>** <br>**注:** Server Core インストールは、接続を許可するためのパスワードを必要とするプロキシを介してインターネットにアクセスできません。|
|インターネット アドレスのプロキシをバイパスするようにサーバーを構成します。|**netsh winttp プロキシを設定する\<servername\>:\<ポート番号\>バイパス リスト ="\<ローカル\>"**| 
|IPSEC 構成表示または変更|**netsh ipsec**| 
|NAP 構成表示または変更|**netsh nap**| 
|表示または物理アドレスへの変換からの IP の変更|**arp**| 
|表示するか、またはローカル ルーティング テーブルの構成|**ルート**| 
|表示または DNS サーバーの設定を構成します。|**nslookup**| 
|プロトコル統計と現在の TCP/IP ネットワーク接続を表示する|**netstat**| 
|プロトコル統計と現在の TCP/IP 接続が TCP/IP (NBT) 経由で NetBIOS を使用して表示します。|**nbtstat**| 
|ネットワーク接続のホップを表示します。|**pathping**| 
|ネットワーク接続のホップをトレースします。|**tracert**| 
|マルチキャスト ルーターの構成を表示する|**mrinfo**| 
|ファイアウォールのリモート管理を有効にします。|**netsh advfirewall のファイアウォール設定のルール グループ =「Windows ファイアウォールのリモート管理」の新しい有効にする = [はい]**| 
 

### <a name="updates-error-reporting-and-feedback"></a>更新プログラム、エラーが報告およびフィードバック

|                               タスク                                |                                                                                                                               コマンド                                                                                                                                |
|-------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                         更新プログラムをインストールする                         |                                                                                                                    **wusa \<update\>.msu /quiet**                                                                                                                    |
|                      インストールされている更新プログラムの一覧を表示する                       |                                                                                                                            **systeminfo**                                                                                                                            |
|                         更新プログラムを削除する                          |                                 **展開/f:\* \<更新\>.msu c:\test** <br>C:\test\ に移動して開く\<更新\>.xml をテキスト エディターでします。<br>置換**インストール**で**削除**ファイルを保存します。<br>**pkgmgr/n:\<更新\>.xml**                                 |
|                    自動更新を構成する                    |          現在の設定を確認する: **cscript %systemroot%\system32\scregedit.wsf/AU/v \* \*<br>自動更新を有効にする: \* \*cscript ある scregedit.wsf/AU 4** <br>自動更新を無効にする: **cscript %systemroot%\system32\scregedit.wsf/AU 1**          |
|                      エラー報告を有効にする                       | 現在の設定を確認する: **serverWerOptin/query** <br>詳細なレポートを自動的に送信する: **serverWerOptin 詳細/** <br>概要レポートを自動的に送信する: **serverWerOptin/summary がありません** <br>エラー報告を無効にする: **serverWerOptin/disable** |
| カスタマー エクスペリエンス向上プログラム (CEIP) に参加する |                                                     現在の設定を確認する: **serverCEIPOptin/query** <br>CEIP を有効にする: **serverCEIPOptin/enable** <br>CEIP を無効にする: **serverCEIPOptin/disable**                                                      |

### <a name="services-processes-and-performance"></a>サービス、プロセス、およびパフォーマンス

|                               タスク                               |                                                                                                                                                                                                             コマンド                                                                                                                                                                                                              |
|------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                    実行中のサービスを一覧表示します。                     |                                                                                                                                                                                                  **sc クエリ**または**net start**                                                                                                                                                                                                   |
|                         サービスを開始する                          |                                                                                                                                                                                 **sc start\<サービス名\>** または**net start\<サービス名\>**                                                                                                                                                                                  |
|                          サービスを停止する                          |                                                                                                                                                                                  **sc stop\<サービス名\>** または**net stop\<サービス名\>**                                                                                                                                                                                   |
| 実行中のアプリケーションと関連するプロセスの一覧を取得する |                                                                                                                                                                                                           **tasklist**                                                                                                                                                                                                           |
|                        タスク マネージャーを開始する                        |                                                                                                                                                                                                           **タスク マネージャー**                                                                                                                                                                                                            |
|    作成およびイベント トレース セッションとパフォーマンス ログの管理    | カウンター、トレース、構成データの収集、または API を作成する: **logman の作成** <br>データ コレクターのプロパティの照会: **logman クエリ** <br>開始またはデータの収集を停止する: **logman start\|停止** <br>コレクターを削除する: **logman の削除** <br> コレクターのプロパティを更新する: **logman update** <br>XML ファイルからデータ コレクター セットをインポートまたは XML ファイルにエクスポートする: **logman import\|エクスポート** |

### <a name="event-logs"></a>イベント ログ

|タスク|コマンド| 
|----|-------|
|イベントのログを一覧表示|**wevtutil el**| 
|指定したログのイベントをクエリします。|**wevtutil qe /f:text \<log name\>**| 
|イベント ログをエクスポートします。|**wevtutil epl\<ログ名\>**| 
|イベント ログを消去します。|**wevtutil cl\<ログ名\>**| 


### <a name="disk-and-file-system"></a>ディスクとファイル システム

|                   タスク                   |                        コマンド                        |
|------------------------------------------|-------------------------------------------------------|
|          ディスク パーティションを管理する          | コマンドの一覧は、実行**diskpart/でしょうか。**  |
|           ソフトウェアの RAID を管理する           | コマンドの一覧は、実行**diskraid/でしょうか。**  |
|        ボリューム マウント ポイントを管理する        | コマンドの一覧は、実行**mountvol/でしょうか。**  |
|           ボリュームを最適化する            |  コマンドの一覧は、実行**デフラグ/でしょうか。**   |
| ボリュームを NTFS ファイル システムに変換する |        **変換\<ボリューム文字\>/FS:NTFS**         |
|              ファイルを圧縮する              |  コマンドの一覧は、実行**compact/でしょうか。**  |
|          開いているファイルを管理する           | コマンドの一覧は、実行**openfiles/でしょうか。** |
|          VSS フォルダーを管理する          | コマンドの一覧は、実行**vssadmin/でしょうか。**  |
|        ファイル システムを管理する        |  コマンドの一覧は、実行**fsutil/でしょうか。**   |
|    ファイルまたはフォルダーの所有権を取得する    |  コマンドの一覧は、実行**icacls/でしょうか。**   |
 
### <a name="hardware"></a>ハードウェア

|タスク|コマンド| 
|----|-------|
|新しいハードウェア デバイスのドライバーを追加する|%Homedrive% フォルダーにドライバーをコピー\\\<ドライバー フォルダー\>します。 実行**pnputil-i-%homedrive%\\\<ドライバー フォルダー\>\\\<ドライバー\>.inf**|
|ハードウェア デバイスのドライバーを削除する|読み込まれているドライバーの一覧は、実行**sc クエリの種類 = ドライバー**します。 実行して**sc delete \<service_name\>**|
