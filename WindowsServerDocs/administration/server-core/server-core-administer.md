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
ms.openlocfilehash: 39fbb92645d39a46613f2142d0258c78a6ba425b
ms.sourcegitcommit: 4df1bc940338219316627ad03f0525462a05a606
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2018
ms.locfileid: "8977999"
---
# Server Core サーバーを管理します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

Server Core では、UI はあるしないために、Windows PowerShell コマンドレット、コマンド ライン ツール、またはリモート ツールを使って基本的な管理タスクを実行する必要があります。 次のセクションでは、PowerShell コマンドレットと基本的なタスクに使用するコマンドの概要を説明します。 インストールを管理するのに、 [Windows Admin Center](../../manage/windows-admin-center/overview.md)、パブリック プレビューで現在の統一された管理ポータルを使用することもできます。 

## PowerShell コマンドレットを使用して管理タスク
Windows PowerShell コマンドレットの基本的な管理タスクを実行するのにには、次の情報を使用します。

### 静的 IP アドレスを設定します。
Server Core サーバーをインストールすると既定では、DHCP アドレスがあります。 静的 IP アドレスが必要な場合は、次の手順を使用して設定できます。

現在のネットワーク構成を表示するには、 **Get NetIPConfiguration**を使用します。

既に使用している IP アドレスを表示するには、 **Get NetIPAddress**を使用します。

静的 IP アドレスを設定するには、次の操作を行います。 

1. **Get NetIPInterface**を実行します。 
2. **IfIndex**列で、IP インターフェイスまたは**InterfaceDescription**文字列の数に注意してください。 複数のネットワーク アダプターがある場合は、番号またはの静的 IP アドレスを設定するインターフェイスに対応する文字列に注意してください。
3. 静的 IP アドレスを設定するのには、次のコマンドレットを実行します。

   ```powershell
   New-NetIPaddress -InterfaceIndex 12 -IPAddress 192.0.2.2 -PrefixLength 24 -DefaultGateway 192.0.2.1
   ```

   この場合
   - **InterfaceIndex**は、手順 2. **IfIndex**の値です。 (例では、12)
   - **Ip アドレス**は、静的 IP アドレスを設定します。 (例では、191.0.2.2)
   - **PrefixLength**は IP アドレスを設定するプレフィックスの長さ (サブネット マスクの別の形式です)。 (たとえば、24)
   - **DefaultGateway**は、デフォルト ゲートウェイに IP アドレスです。 (たとえば、192.0.2.1)
4. DNS クライアント サーバーのアドレスを設定するには、次のコマンドレットを実行します。 

   ```powershell
   Set-DNSClientServerAddress –InterfaceIndex 12 -ServerAddresses 192.0.2.4
   ```
   
   この場合
   - **InterfaceIndex**は、手順 2. IfIndex の値です。
   - **ServerAddresses**は、DNS サーバーの IP アドレスです。
5. 複数の DNS サーバーを追加するには、次のコマンドレットを実行します。 

   ```powershell
   Set-DNSClientServerAddress –InterfaceIndex 12 -ServerAddresses 192.0.2.4,192.0.2.5
   ```

   どこで、この例では**192.0.2.4**と**192.0.2.5**は DNS サーバーの両方の IP アドレスです。

かどうかは、DHCP、実行を使用して切り替える必要があります。**セット DnsClientServerAddress – InterfaceIndex 12 – ResetServerAddresses**します。

### ドメインに参加します。
コンピューターをドメインに参加させるには、次のコマンドレットを使用します。

1. **コンピューターの追加**を実行します。 ドメインとドメイン名への参加を両方の資格情報を求めします。
2. ローカルの Administrators グループにドメイン ユーザー アカウントを追加する必要がある場合は、コマンド プロンプト (PowerShell ウィンドウ) ではなく、次のコマンドを実行します。

   ```
   net localgroup administrators /add <DomainName>\<UserName>
   ```
3. コンピューターを再起動します。 **コンピューターの再起動**を実行して、これを行うことができます。

### サーバーの名前を変更します。
サーバーの名前を変更するのにには、次の手順を使用します。

1. **ホスト名**または**ipconfig**コマンドを使用してサーバーの現在の名前を決定します。
2. 実行**名前の変更コンピューター-ComputerName \<new_name\ >** します。
3. コンピューターを再起動します。

### サーバーをアクティブ化します。

実行**slmgr.vbs – ipk\<productkey\ >** します。 **Slmgr.vbs – ato**を実行します。 ライセンス認証が成功した場合は、メッセージを取得しません。

> [!NOTE]
> こともサーバー電話でライセンス認証、[キー管理サービス (KMS) サーバー](../../get-started/server-2016-activation.md)を使用して、またはリモートでします。 、リモートでライセンス認証するには、リモート コンピューターから、次のコマンドレットを実行します。 

>```powershell
>**cscript windows\system32\slmgr.vbs <ServerName> <UserName> <password>:-ato**
>```
 
### Windows ファイアウォールを構成します。

Windows PowerShell コマンドレットとスクリプトを使用して、Server Core のコンピューターにローカル Windows ファイアウォールを構成できます。 Windows ファイアウォールを構成に使用できるコマンドレット[NetSecurity](/powershell/module/netsecurity/?view=win10-ps)を参照してください。

### Windows PowerShell リモート処理を有効にします。

入力コマンドは Windows PowerShell で別のコンピューター上で実行する 1 台のコンピューターで Windows PowerShell リモート処理を有効にすることができます。 **Enable-psremoting**で Windows PowerShell リモート処理を有効にします。

詳細については、[に関するリモートよく寄せられる質問](/powershell/module/microsoft.powershell.core/about/about_remote_faq?view=powershell-5.1)をご覧ください。
</br>

## コマンドラインから管理タスク
次の参照情報を使用して、コマンドラインから管理タスクを実行します。

### 構成とインストール
|タスク | コマンド |
|-----|-------|
|ローカルの管理者パスワードを設定します。| **net ユーザー管理者** \* |
|コンピューターをドメインに参加させる| **netdom への参加 computername %****/domain:\<domain\ >/userd:\<domain\\username\ >/passwordd:**\* <br> コンピューターを再起動します。|
|ドメインが変更されていることを確認します。| **set** |
|コンピューターをドメインから削除します。|**netdom 削除 \ < computername\ >**| 
|ローカルの Administrators グループにユーザーを追加します。|**正味のローカル グループ管理者/追加 \ < domain\\username\ >** |
|ローカルの Administrators グループからユーザーを削除します。|**正味のローカル グループ管理者/delete \ < domain\\username\ >** |
|ローカル コンピューターにユーザーを追加します。|**net use \ < domain\username\ > * 追加/** |
|ローカル コンピューターにグループを追加します。|**正味のローカル グループ \ < グループ name\ > 追加/**|
|ドメインに参加しているコンピューターの名前を変更します。|**netdom renamecomputer %computername%/NewName:\<new コンピューター name\ >/userd:\<domain\\username\ >/passwordd:** * |
|新しいコンピューター名を確認します。|**set**| 
|作業グループ内のコンピューターの名前を変更します。|**netdom renamecomputer \ < currentcomputername\ >/NewName: \ < newcomputername\ >** <br>コンピューターを再起動します。|
|ページング ファイルの管理を無効にします。|**wmic コンピューター システム =「\ < computername\ >」の名前が設定 AutomaticManagedPagefile = False**| 
|ページング ファイルを構成します。|**wmic pagefileset =「\ < パス/filename\ >」の名前が使う設定 = \ < initialsize\ > 使う = \ < maxsize\ >** <br>バイトで、ページング ファイルの元のサイズは、*作成*、ページング ファイルの名前とパスを*パス/filename*には、 *maxsize*バイトでページファイルの最大サイズ。|
|静的 IP アドレスに変更します。|**ipconfig すべて/** <br>関連する情報を記録またはテキスト ファイルにリダイレクトする (**ipconfig すべて/> ipconfig.txt**)。<br>**netsh インターフェイスの ipv4 表示インターフェイス**<br>インターフェイスの一覧があることを確認します。<br>**netsh インターフェイスの ipv4 アドレス名の設定 \ < インターフェイス list\ から ID > ソース静的アドレスを = = \ < 優先 IP address\ > ゲートウェイ = \ < ゲートウェイ address\ >**<br>実行**ipconfig すべて/** **なし**に有効になっている DHCP が設定されている vierfy にします。|
|静的な DNS アドレスを設定します。|**netsh インターフェイスの ipv4 dnsserver 名を追加する = \<name またはネットワーク インターフェイス card\ の ID > アドレスのプライマリ DNS server\ \<IP アドレスを = > インデックス 1 = <br> **netsh インターフェイスの ipv4 dnsserver 名に追加のセカンダリ DNS server\ \<name = >アドレスのセカンダリ DNS server\ \<IP アドレスを = > インデックス 2 = * * <br> その他のサーバーを追加する適切なを繰り返します。<br>実行**ipconfig すべて/** アドレスが正しいことを確認します。|
|静的 IP アドレスから DHCP による IP アドレスへの変更します。|**netsh インターフェイスの ipv4 アドレスの名前を設定する = \ < ローカル システムの IP アドレス > ソース DHCP =** <br>実行**Ipconfig すべて/** を有効になっている DCHP が **[はい]** に設定されていることを確認します。|
|プロダクト キーを入力します。|**slmgr.vbs – ipk \ < 製品 key \ >**| 
|ローカル サーバーをアクティブ化します。|**slmgr.vbs ato**| 
|サーバーをリモートでアクティブ化します。|**コマンド slmgr.vbs – ipk \ < 製品 key \ > \ < サーバー name\ > \ < username\ > \ < password\ >** <br>**コマンドの slmgr.vbs ato \ < servername\ > \ < username\ > \ < password\ >** <br>実行して、コンピューターの GUID を取得する**コマンド slmgr.vbs-でした** <br> 実行**コマンド slmgr.vbs-dli \<GUID\ >** <br>ライセンスの状態が**ライセンス (アクティブ化されます)** に設定されていることを確認します。


### ネットワークとファイアウォール

|タスク|コマンド| 
|----|-------|
|プロキシ サーバーを使用するようにサーバーを構成します。|**netsh Winhttp プロキシの設定 \ < servername\ >: \ < ポート番号 \ >** <br>**注:** Server Core インストール接続を許可するパスワードが必要なプロキシによって、インターネットにアクセスできません。|
|インターネット アドレスにプロキシをバイパスするようにサーバーを構成します。|**netsh winttp プロキシの設定 \ < servername\ >: \ < ポート番号 \ > のバイパス リスト =「\ < は >」**| 
|表示または IPSEC 構成の変更|**netsh ipsec**| 
|表示または NAP 構成の変更|**netsh nap**| 
|表示または物理アドレス変換に IP を変更します。|**arp**| 
|表示するか、構成して、ローカルのルーティング テーブル|**ルート**| 
|表示または DNS サーバーの設定を構成します。|**nslookup**| 
|プロトコルの統計情報と現在の TCP/IP ネットワーク接続を表示します。|**netstat**| 
|プロトコルの統計情報と TCP/IP (NBT) 経由で NetBIOS を使用して現在の TCP/IP 接続を表示します。|**nbtstat**| 
|ネットワーク接続のホップを表示します。|**pathping**| 
|ネットワーク接続のトレース ホップ|**tracert**| 
|マルチキャスト ルーターの構成を表示します。|**mrinfo**| 
|ファイアウォールのリモート管理を有効にします。|**netsh advfirewall ファイアウォール規則のグループを設定して =「Windows ファイアウォールのリモート管理」新しい enable = yes**| 
 

### 更新プログラム、エラーの報告、フィードバック

|タスク|コマンド| 
|----|-------|
|更新プログラムをインストールします。|**wusa \ < update\ > .msu/quiet**| 
|インストールされている一覧の更新|**systeminfo**| 
|更新プログラムを削除します。|**展開/f:\* \ < update\ > .msu c:\test** <br>移動 c:\test\ して開く \ < update\ > .xml をテキスト エディターでします。<br>置き換えます**インストール****を削除**し、ファイルを保存します。<br>**pkgmgr/n:\ < update\ > .xml**|
|自動更新を構成します。|現在の設定を確認する: * * コマンド %systemroot%\system32\scregedit.wsf/AU/v * *<br>自動更新を有効にする:**コマンド scregedit.wsf/AU 4** <br>自動更新を無効にする:**コマンド %systemroot%\system32\scregedit.wsf/AU 1**| 
|エラー報告を有効にします。|現在の設定を確認する: **serverWerOptin/query** <br>詳細なレポートを自動的に送信する: **serverWerOptin/詳細な** <br>要約レポートを自動的に送信する: **serverWerOptin/summary** <br>エラー報告を無効にする: **serverWerOptin/disable**|
|カスタマー エクスペリエンス向上プログラム (CEIP) に参加します。|現在の設定を確認する: **serverCEIPOptin/query** <br>CEIP を有効にする: **serverCEIPOptin/enable** <br>CEIP を無効にする: **serverCEIPOptin/disable**|

### サービス、プロセス、およびパフォーマンス

|タスク|コマンド| 
|----|-------|
|実行中のサービスを一覧します。|**sc クエリ**または**net start**| 
|サービスを開始します。|**sc 開始 \<service name\ >** または**net 開始 \<service name\ >**| 
|サービスを停止します。|**sc stop \<service name\ >** または**net stop \<service name\ >**| 
|アプリケーションの実行と関連付けられているプロセスの一覧を取得します。|**tasklist**||プロセスを強制的に停止します。|**Tasklist**取得プロセス ID (PID) を実行し、実行**taskkill/PID \<process ID\ >**|
|タスク マネージャーを起動|**タスク マネージャー**| 
|作成およびイベント トレース セッションとパフォーマンス ログの管理|カウンター、トレース、構成データの収集や API を作成する: **logman ceate** <br>クエリのデータ コレクターのプロパティを: **logman クエリ** <br>開始またはデータの収集を停止する: **logman start\ | 停止** <br>コレクターを削除する: **logman delete** <br> コレクターのプロパティを更新する: **logman update** <br>XML ファイルからデータ コレクター セットをインポートまたは XML ファイルにエクスポートします: **logman import\ | エクスポート**|

### イベント ログ

|タスク|コマンド| 
|----|-------|
|イベント ログの一覧|**wevtutil el**| 
|指定したログでイベントを照会します。|**wevtutil qe/f:text \ < name\ をログに記録 >**| 
|イベント ログをエクスポートします。|**wevtutil epl \ < name\ をログに記録 >**| 
|イベント ログを消去します。|**wevtutil cl \ < name\ をログに記録 >**| 


### ディスクとファイル システム

|タスク|コマンド|
|----|-------|
|ディスクのパーティションを管理します。|コマンドの一覧は、実行**diskpart/?**|  
|RAID ソフトウェアを管理します。|コマンドの一覧は、実行**diskraid/?**|  
|ボリュームのマウント ポイントを管理します。|コマンドの一覧は、実行**mountvol/?**| 
|ボリュームを最適化します。|コマンドの一覧は、実行**ディスク デフラグ ツール/?**|  
|ボリュームを NTFS ファイル システムに変換します。|**変換 \ < ボリューム letter\ >/FS:NTFS**| 
|ファイルを最適化します。|コマンドの一覧は、実行**compact/?**|  
|開いているファイルを管理します。|コマンドの一覧は、実行**openfiles/?**|  
|VSS フォルダーを管理します。|コマンドの一覧は、実行**vssadmin/?**| 
|ファイル システムを管理します。|コマンドの一覧は、実行**fsutil/?**||ファイルの署名を確認します。|**ファイル名を指定/かどうか。**| 
|ファイルまたはフォルダーの所有権を取得します。|コマンドの一覧は、実行**icacls/?**| 
 
### ハードウェア

|タスク|コマンド| 
|----|-------|
|新しいハードウェア デバイスのドライバーを追加します。|%Homedrive%\\\ < ドライバー folder\ > フォルダーにドライバーをコピーします。 実行**pnputil-i-%homedrive%\\\<driver folder\ > \\\<driver\ > .inf**|
|ハードウェア デバイスのドライバーを削除します。|読み込まれたドライバーの一覧、実行**sc クエリの種類 = ドライバー**します。 実行し、 **sc 削除 \<service_name\ >**|
