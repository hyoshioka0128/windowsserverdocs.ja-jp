---
title: Nano Server の管理
description: 更新プログラム、サービス パッケージ、ネットワーク トレース、パフォーマンスの監視
ms.prod: windows-server-threshold
ms.service: na
manager: DonGill
ms.technology: server-nano
ms.date: 09/06/2017
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 599d6438-a506-4d57-a0ea-1eb7ec19f46e
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: 165b7e7aea7a7d0bb56d21f350f6ee646d5fa973
ms.sourcegitcommit: af80963a1d16c0b836da31efd9c5caaaf6708133
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2019
ms.locfileid: "67280404"
---
# <a name="manage-nano-server"></a>Nano Server の管理

>適用先:Windows Server 2016

> [!IMPORTANT]
> Windows Server バージョン 1709 以降、Nano Server は[コンテナー基本 OS イメージ](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image)としてのみ提供されます。 その意味については、「[Nano Server に加えられる変更](nano-in-semi-annual-channel.md)」をご覧ください。   

Nano Server はリモートで管理します。 Nano Server にローカル ログオン機能はありません。ターミナル サービスもサポートされません。 ただし、Windows PowerShell、Windows Management Instrumentation (WMI)、Windows リモート管理、緊急管理サービス (EMS) など、さまざまなオプションを利用して Nano Server をリモートで管理できます。  

任意のリモート管理ツールを使用するには、Nano Server の IP アドレスが必要な場合があります。 IP アドレスを確認する方法は、次のとおりいくつかあります。  
  
-   Nano 回復コンソールを使用する (詳細については、このトピックの「Using the Nano Server Recovery Console (Nano Server 回復コンソールの使用)」を参照してください)。  
  
-   コンピューターにシリアル ケーブルを接続し、EMS を使用する。  
  
-   構成時に Nano Server に割り当てたコンピューター名と ping を使用して、IP アドレスを取得できます。 たとえば、`ping NanoServer-PC /4` のように指定します。  
  
## <a name="using-windows-powershell-remoting"></a>Windows PowerShell リモート処理を使用する  
Windows PowerShell リモート処理を使用して Nano Server を管理するには、Nano Server の IP アドレスを管理コンピューターの信頼されたホストの一覧に追加し、使用しているアカウントを Nano Server の管理者に追加する必要があります。CredSSP を使用する場合は、その機能を有効にする必要もあります。  

> [!NOTE]
> 対象の Nano Server と管理コンピューターが同じ AD DS フォレスト (または信頼関係のあるフォレスト) に属している場合、Nano Server を信頼されたホストの一覧に追加する必要はありません。完全修飾ドメイン名を使用して、Nano Server に接続できます。次に例を示します。PS C:\>Enter-PSSession -ComputerName nanoserver.contoso.com -Credential (Get-Credential)
  
  
Nano Server を信頼されたホストの一覧に追加するには、管理者特権での Windows PowerShell プロンプトで次のコマンドを実行します。  
  
`Set-Item WSMan:\localhost\Client\TrustedHosts "<IP address of Nano Server>"`  
  
リモートの Windows PowerShell セッションを開始するには、管理者特権のローカル Windows PowerShell セッションを開始し、次のコマンドを実行します。  
  
  
```  
$ip = "<IP address of Nano Server>"  
$user = "$ip\Administrator"  
Enter-PSSession -ComputerName $ip -Credential $user  
```  
  
  
これで、Nano Server で通常どおりに Windows PowerShell コマンドを実行できます。  
  
> [!NOTE]  
> このリリースの Nano Server では、一部の Windows PowerShell コマンドを利用できません。 どれが利用できるかを確認するには、`Get-Command -CommandType Cmdlet` を実行します  
  
リモート セッションを停止するには、コマンド `Exit-PSSession` を使用します  
  
## <a name="using-windows-powershell-cim-sessions-over-winrm"></a>WinRM を介して Windows PowerShell CIM セッションを使用する  
Windows リモート管理 (WinRM) を介して、Windows PowerShell の CIM セッションとインスタンスを使用して、WMI コマンドを実行できます。  
  
CIM セッションを開始するには、Windows PowerShell プロンプトで次のコマンドを実行します。  
  
  
```  
$ip = "<IP address of the Nano Server\>"  
$user = $ip\Administrator  
$cim = New-CimSession -Credential $user -ComputerName $ip  
```  
  
  
セッションが確立されたら、さまざまな WMI コマンドを実行できます。次に例を示します。  
  
  
```  
Get-CimInstance -CimSession $cim -ClassName Win32_ComputerSystem | Format-List *  
Get-CimInstance -CimSession $Cim -Query "SELECT * from Win32_Process WHERE name LIKE 'p%'"  
```  
  
  
## <a name="windows-remote-management"></a>Windows リモート管理  
Windows リモート管理 (WinRM) を使用して、リモートから Nano Server でプログラムを実行できます。 WinRM を使用するには、まず、管理者特権でのコマンド プロンプトで次のコマンドを使用して、サービスを構成し、コード ページを設定します。  
  
```
winrm quickconfig
winrm set winrm/config/client @{TrustedHosts="<ip address of Nano Server>"}
chcp 65001
```
  
これで、リモートから Nano Server でコマンドを実行できます。 次に、例を示します。  

```
winrs -r:<IP address of Nano Server> -u:Administrator -p:<Nano Server administrator password> ipconfig
```
  
Windows リモート管理の詳細については、「[Windows リモート管理 (WinRM) の概要](https://technet.microsoft.com/library/dn265971.aspx)」を参照してください。  
   
   
  
## <a name="running-a-network-trace-on-nano-server"></a>Nano Server でネットワーク トレースを実行する  
 netsh トレース、Tracelog.exe、および Logman.exe は、Nano Server では利用できません。 ネットワーク パケットをキャプチャするには、次の Windows PowerShell コマンドレットを使用できます。  
   
   
```  
New-NetEventSession [-Name]  
Add-NetEventPacketCaptureProvider -SessionName  
Start-NetEventSession [-Name]  
Stop-NetEventSession [-Name]  
```  
これらのコマンドレットの詳細については、「[Network Event Packet Capture Cmdlets in Windows PowerShell (Windows PowerShell のネットワーク イベント パケット キャプチャ コマンドレット)](https://technet.microsoft.com/library/dn268520(v=wps.630).aspx)」を参照してください。  

## <a name="installing-servicing-packages"></a>サービス パッケージをインストールする  
サービス パッケージをインストールする場合は、-ServicingPackagePath パラメーターを使用します (.cab ファイルへのパスの配列を渡すことができます)。  
  
`New-NanoServerImage -DeploymentType Guest -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\NanoServer.wim -ServicingPackagePath \\path\to\kb123456.cab`  
  
多くの場合、サービス パッケージまたは修正プログラムは、.cab ファイルを含む KB 項目としてダウンロードされます。 次の手順に従って、.cab ファイルを抽出します。その後、-ServicingPackagePath パラメーターを使用して、抽出したファイルをインストールできます。  
  
1.  (関連するサポート技術情報の記事または [Microsoft Update カタログ](https://catalog.update.microsoft.com/v7/site/home.aspx)から) サービス パッケージをダウンロードします。 ローカル ディレクトリまたはネットワーク共有に保存します。次に例を示します。C:\ServicingPackages  
2.  抽出されたサービス パッケージを保存するフォルダーを作成します。  例: c:\KB3157663_expanded  
3.  Windows PowerShell コンソールを開き、`Expand` コマンドを使用し、サービス パッケージの .msu ファイルへのパスを指定します。さらに、`-f:*` パラメーターと、サービス パッケージを抽出する場所のパスを含めます。  次に例を示します。`Expand "C:\ServicingPackages\Windows10.0-KB3157663-x64.msu" -f:* "C:\KB3157663_expanded"`  
  
    抽出されたファイルは次のようになります。  
C:>dir C:\KB3157663_expanded   
Volume in drive C is OS  
Volume Serial Number is B05B-CC3D  
   
      Directory of C:\KB3157663_expanded  
   
      04/19/2016  01:17 PM    \<DIR>          .  
      04/19/2016  01:17 PM    \<DIR&gt;          .  
        04/17/2016  12:31 AM               517 Windows10.0-KB3157663-x64-pkgProperties.txt  
04/17/2016  12:30 AM        93,886,347 Windows10.0-KB3157663-x64.cab  
04/17/2016  12:31 AM               454 Windows10.0-KB3157663-x64.xml  
04/17/2016  12:36 AM           185,818 WSUSSCAN.cab  
               4 File(s)     94,073,136 bytes  
               2 Dir(s)  328,559,427,584 bytes free  
4.  -ServicingPackagePath パラメーターにこのディレクトリ内の .cab ファイルを指定して、`New-NanoServerImage` を実行します。次に例を示します。`New-NanoServerImage -DeploymentType Guest -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\NanoServer.wim -ServicingPackagePath C:\KB3157663_expanded\Windows10.0-KB3157663-x64.cab`  

## <a name="managing-updates-in-nano-server"></a>Nano Server の更新を管理する

現在、Windows Management Instrumentation (WMI) の Windows Update プロバイダーを使用して、適用可能な更新プログラムの一覧を検索し、そのすべてまたは一部をインストールできます。 Windows Server Update Services (WSUS) を使用する場合は、WSUS サーバーに接続して更新プログラムを取得するように Nano Server を構成することもできます。  

どちらの場合も、まず Nano Server コンピューターへのリモート Windows PowerShell セッションを確立します。 次の例では、セッションに *$sess* を使用しています。別の要素を使用する場合は、必要に応じてその要素に置き換えてください。  


### <a name="view-all-available-updates"></a>利用可能なすべての更新プログラムの表示  
---  
適用可能な更新プログラムの完全な一覧を取得するには、次のコマンドを使用します。  
```  
$sess = New-CimInstance -Namespace root/Microsoft/Windows/WindowsUpdate -ClassName MSFT_WUOperationsSession  

$scanResults = Invoke-CimMethod -InputObject $sess -MethodName ScanForUpdates -Arguments @{SearchCriteria="IsInstalled=0";OnlineScan=$true}  
```  
**注:**  
利用可能な更新プログラムがない場合、このコマンドでは次のエラーが返されます。  
```  
Invoke-CimMethod : A general error occurred that is not covered by a more specific error code.  

At line:1 char:16  

+ ... anResults = Invoke-CimMethod -InputObject $sess -MethodName ScanForUp ...  

+                 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~  

    + CategoryInfo          : NotSpecified: (MSFT_WUOperatio...-5b842a3dd45d")  

   :CimInstance) [Invoke-CimMethod], CimException  

    + FullyQualifiedErrorId : MI RESULT 1,Microsoft.Management.Infrastructure.  

   CimCmdlets.InvokeCimMethodCommand  
```  

### <a name="install-all-available-updates"></a>利用可能なすべての更新プログラムのインストール  
---  
次のコマンドを使用すると、利用可能な更新プログラムを**すべて**検出、ダウンロード、およびインストールできます。  

```  
$sess = New-CimInstance -Namespace root/Microsoft/Windows/WindowsUpdate -ClassName MSFT_WUOperationsSession  

$scanResults = Invoke-CimMethod -InputObject $sess -MethodName ApplyApplicableUpdates  

Restart-Computer  
```  
**注:**  
Windows Defender により、更新プログラムがインストールされません。 この問題を回避するには、Windows Defender をアンインストールし、更新プログラムをインストールしてから、Windows Defender を再インストールします。 または、更新プログラムを別のコンピューターでダウンロードし、Nano Server にコピーしてから、DISM.exe を使用して適用します。  


### <a name="verify-installation-of-updates"></a>更新プログラムのインストールの確認  
---  
現在インストールされている更新プログラムの一覧を取得するには、次のコマンドを使用します。  
```  
$sess = New-CimInstance -Namespace root/Microsoft/Windows/WindowsUpdate -ClassName MSFT_WUOperationsSession  

$scanResults = Invoke-CimMethod -InputObject $sess -MethodName ScanForUpdates -Arguments @{SearchCriteria="IsInstalled=1";OnlineScan=$true}  
```  

**注:**  
これらのコマンドでは、インストールされている更新プログラムの一覧が返されますが、出力に "インストール済み" とは明記されません。 レポートなどのために、明記された出力が必要な場合は、次を実行できます。  
```  
Get-WindowsPackage--Online  
```  

### <a name="using-wsus"></a>WSUS の使用  
---  
上記のコマンドでは、インターネット上の Windows Update と Microsoft Update サービスを照会して、更新プログラムを検索およびダウンロードします。 WSUS を使用する場合は、代わりに WSUS サーバーを使用するように Nano Server のレジストリ キーを設定できます。  
  
「[Active Directory 以外の環境で自動更新を構成する](https://technet.microsoft.com/library/cc708449(v=ws.10).aspx)」の「Windows Update エージェント環境のオプションのレジストリ キー」の表をご覧ください。  
  
少なくとも **WUServer** レジストリ キーと **WUStatusServer** レジストリ キーを設定する必要があります。WSUS を実装する方法によっては、その他の値も設定が必要になることがあります。 これらの設定は、同じ環境内の他の Windows Server を確認することで、いつでも確認できます。  

これらの値を WSUS 用に設定すると、前のセクションのコマンドでは、更新プログラムについてそのサーバーを照会し、ダウンロード ソースとして使用します。  

### <a name="automatic-updates"></a>自動更新  
---  
現在、更新プログラムのインストールを自動化するには、上記の手順をローカルの Windows PowerShell スクリプトに変換します。その後、スケジュールに従って、そのスクリプトを実行し、システムを再起動するようにスケジュールしたタスクを作成します。


## <a name="performance-and-event-monitoring-on-nano-server"></a>Nano Server のパフォーマンスおよびイベントを監視する
[comment]: # (Venkat Yalla より。)
Nano Server では、[Windows イベント トレーシング](https://aka.ms/u2pa0i) (ETW) フレームワークを完全にサポートしています。しかし、トレースとパフォーマンス カウンターを管理するための使い慣れたツールには、Nano Server で現在使用できないものがあります。 ただし、Nano Server には、最も一般的なパフォーマンス分析シナリオを実現するツールとコマンドレットが用意されています。

大まかなワークフローは、どの Window Server インストールでも同じです。オーバーヘッドの少ないトレースをターゲットの (Nano Server) コンピューターで実行し、生成されたトレース ファイルやログを別のコンピューターで [Windows Performance Analyzer](https://msdn.microsoft.com/library/windows/hardware/hh448170.aspx) や [Message Analyzer](https://www.microsoft.com/download/details.aspx?id=44226) などのツールを使用してオフラインで後処理します。

> [!NOTE]
> PowerShell リモート処理を使用してファイルを転送する方法については、「[How to copy files to and from Nano Server (Nano Server との間でファイルをコピーする方法)](https://aka.ms/nri9c8)」を参照してください。

次のセクションでは、最も一般的なパフォーマンス データ収集作業と、Nano Server でそれを実現するためのサポートされている方法の一覧を示します。

### <a name="query-available-event-providers"></a>使用可能なイベント プロバイダーの照会
[Windows Performance Recorder](https://msdn.microsoft.com/library/hh448229.aspx) は、次のように使用可能なイベント プロバイダーを照会するツールです。
```
wpr.exe -providers
```

関心のあるイベントの種類で出力にフィルターを適用できます。 次に、例を示します。
```
PS C:\> wpr.exe -providers | select-string "Storage"

       595f33ea-d4af-4f4d-b4dd-9dacdd17fc6e                              : Microsoft-Windows-StorageManagement-WSP-Host
       595f7f52-c90a-4026-a125-8eb5e083f15e                              : Microsoft-Windows-StorageSpaces-Driver
       69c8ca7e-1adf-472b-ba4c-a0485986b9f6                              : Microsoft-Windows-StorageSpaces-SpaceManager
       7e58e69a-e361-4f06-b880-ad2f4b64c944                              : Microsoft-Windows-StorageManagement
       88c09888-118d-48fc-8863-e1c6d39ca4df                              : Microsoft-Windows-StorageManagement-WSP-Spaces
```

### <a name="record-traces-from-a-single-etw-provider"></a>1 つの ETW プロバイダーからのトレースの記録
これには、新しい[イベント トレース管理コマンドレット](https://technet.microsoft.com/library/dn919247.aspx)を使用できます。 次にワークフローの例を示します。

イベントを格納するファイルの名前を指定して、トレースを作成し、開始します。
```
PS C:\> New-EtwTraceSession -Name "ExampleTrace" -LocalFilePath c:\etrace.etl
```

プロバイダーの GUID をトレースに追加します。 ```wpr.exe -providers``` を使用して、プロバイダー名を GUID に変換します。 
```
PS C:\> wpr.exe -providers | select-string "Kernel-Memory"

       d1d93ef7-e1f2-4f45-9943-03d245fe6c00                              : Microsoft-Windows-Kernel-Memory

PS C:\> Add-EtwTraceProvider -Guid "{d1d93ef7-e1f2-4f45-9943-03d245fe6c00}" -SessionName "ExampleTrace"
```

トレースを削除します。これにより、トレース セッションが停止し、イベントが関連するログ ファイルにフラッシュされます。
```
PS C:\> Remove-EtwTraceSession -Name "ExampleTrace"

PS C:\> dir .\etrace.etl

    Directory: C:\

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        9/14/2016  11:17 AM       16515072 etrace.etl
```
> [!NOTE]
> この例では 1 つのトレース プロバイダーをセッションに追加する方法を示していますが、トレース セッションで異なるプロバイダー GUID を指定した ```Add-EtwTraceProvider``` コマンドレットを複数回使用して、複数のソースからのトレースを有効にすることもできます。 他には、以下で説明する ```wpr.exe``` プロファイルを使用する方法があります。

### <a name="record-traces-from-multiple-etw-providers"></a>複数の ETW プロバイダーからのトレースの記録
[Windows Performance Recorder](https://msdn.microsoft.com/library/hh448229.aspx) の ```-profiles``` オプションを使用すると、同時に複数のプロバイダーからのトレースを有効にできます。 CPU、Network、DiskIO など、さまざまな組み込みのプロファイルから選択することができます。
```
PS C:\Users\Administrator\Documents> wpr.exe -profiles 

Microsoft Windows Performance Recorder Version 10.0.14393 (CoreSystem)
Copyright (c) 2015 Microsoft Corporation. All rights reserved.

        GeneralProfile              First level triage
        CPU                         CPU usage
        DiskIO                      Disk I/O activity
        FileIO                      File I/O activity
        Registry                    Registry I/O activity
        Network                     Networking I/O activity
        Heap                        Heap usage
        Pool                        Pool usage
        VirtualAllocation           VirtualAlloc usage
        Audio                       Audio glitches
        Video                       Video glitches
        Power                       Power usage
        InternetExplorer            Internet Explorer
        EdgeBrowser                 Edge Browser
        Minifilter                  Minifilter I/O activity
        GPU                         GPU activity
        Handle                      Handle usage
        XAMLActivity                XAML activity
        HTMLActivity                HTML activity
        DesktopComposition          Desktop composition activity
        XAMLAppResponsiveness       XAML App Responsiveness analysis
        HTMLResponsiveness          HTML Responsiveness analysis
        ReferenceSet                Reference Set analysis
        ResidentSet                 Resident Set analysis
        XAMLHTMLAppMemoryAnalysis   XAML/HTML application memory analysis
        UTC                         UTC Scenarios
        DotNET                      .NET Activity
        WdfTraceLoggingProvider     WDF Driver Activity
```

カスタム プロファイルを作成する詳細なガイダンスについては、[WPR.exe のドキュメント](https://msdn.microsoft.com/library/windows/hardware/hh448223.aspx)を参照してください。

### <a name="record-etw-traces-during-operating-system-boot-time"></a>オペレーティング システム起動時の ETW トレースの記録
システム起動時のイベントを収集するには、```New-AutologgerConfig``` コマンドレットを使用します。 使用方法は ```New-EtwTraceSession``` コマンドレットとよく似ていますが、自動ロガー構成に追加されたプロバイダーは次回起動時の初期にのみ有効になります。 全体的なワークフローは次のようになります。

最初に、新しい自動ロガー構成を作成します。
```
PS C:\> New-AutologgerConfig -Name "BootPnpLog" -LocalFilePath c:\bootpnp.etl 
```

ETW プロバイダーを構成に追加します。 この例では、Kernel PnP プロバイダーを使用します。 同じ自動ロガー名 (ただし、GUID が異なる) を指定して ```Add-EtwTraceProvider``` を再度呼び出して、複数のソースからのブート トレース コレクションを有効にします。
```
Add-EtwTraceProvider -Guid "{9c205a39-1250-487d-abd7-e831c6290539}" -AutologgerName BootPnpLog
```

ETW セッションはすぐには開始されず、次回の起動時に開始するように構成されます。 再起動すると、追加したトレース プロバイダーが有効になった状態で、自動ロガー構成名を持つ新しい ETW セッションが自動的に開始されます。 Nano Server が起動したら、次のコマンドでトレース セッションを停止します。停止する前に、記録されたイベントが関連するトレース ファイルにフラッシュされます。
```
PS C:\> Remove-EtwTraceSession -Name BootPnpLog
```

次回の起動時に別のトレース セッションが自動的に作成されないように、次のように自動ロガー構成を削除します。
```
PS C:\> Remove-AutologgerConfig -Name BootPnpLog
```

複数のシステムやディスクなしのシステムでブート トレースとセットアップ トレースを収集するには、[セットアップおよびブート イベント収集](../administration/get-started-with-setup-and-boot-event-collection.md)の使用を検討してください。

### <a name="capture-performance-counter-data"></a>パフォーマンス カウンター データのキャプチャ
通常、パフォーマンス カウンター データは Perfmon.exe の GUI で監視します。 Nano Server では、同等の ```Typeperf.exe``` コマンド ラインを使用します。 次に、例を示します。

使用可能なカウンターを照会します。出力にフィルターを適用して、関心のあるカウンターを簡単に見つけることができます。
```
PS C:\> typeperf.exe -q | Select-String "UDPv6"

\UDPv6\Datagrams/sec
\UDPv6\Datagrams Received/sec
\UDPv6\Datagrams No Port/sec
\UDPv6\Datagrams Received Errors
\UDPv6\Datagrams Sent/sec
```

オプションを使用して、カウンターの値を収集する回数と間隔を指定できます。 次の例では、プロセッサ アイドル時間を 3 秒おきに 5 回収集します。
```
PS C:\> typeperf.exe "\Processor Information(0,0)\% Idle Time" -si 3 -sc 5

"(PDH-CSV 4.0)","\\ns-g2\Processor Information(0,0)\% Idle Time"
"09/15/2016 09:20:56.002","99.982990"
"09/15/2016 09:20:59.002","99.469634"
"09/15/2016 09:21:02.003","99.990081"
"09/15/2016 09:21:05.003","99.990454"
"09/15/2016 09:21:08.003","99.998577"
Exiting, please wait...
The command completed successfully.
```

その他のコマンド ライン オプションを使用すると、構成ファイル内の関心のあるパフォーマンス カウンターの名前を指定することや、ログ ファイルに出力をリダイレクトすることなどができます。 詳細については、[typeperf.exe のドキュメント](https://technet.microsoft.com/library/bb490960.aspx)を参照してください。

Nano Server ターゲットで Perfmon.exe のグラフィカル インターフェイスをリモートで使用することもできます。 パフォーマンス カウンターをビューに追加する場合、既定の *<Local computer>* の代わりに、コンピューター名で Nano Server ターゲットを指定します。

### <a name="interact-with-the-windows-event-log"></a>Windows イベント ログの操作

Nano Server では、```Get-WinEvent``` コマンドレットをサポートしています。このコマンドレットでは、ローカルとリモート コンピューターの両方に対する Windows イベント ログのフィルター処理と照会機能が提供されます。 詳細なオプションと例については、[Get-WinEvent のドキュメント ページ](https://technet.microsoft.com/library/hh849682.aspx)を参照してください。 次の簡単な例では、*System* ログに記録されている過去 2 日間の "*エラー*" を取得します。
```
PS C:\> $StartTime = (Get-Date) - (New-TimeSpan -Day 2)
PS C:\> Get-WinEvent -FilterHashTable @{LogName='System'; Level=2; StartTime=$StartTime} | select TimeCreated, Message

TimeCreated           Message
-----------           -------
9/15/2016 11:31:19 AM Task Scheduler service failed to start Task Compatibility module. Tasks may not be able to reg...
9/15/2016 11:31:16 AM The Virtualization Based Security enablement policy check at phase 6 failed with status: {File...
9/15/2016 11:31:16 AM The Virtualization Based Security enablement policy check at phase 0 failed with status: {File...
```

Nano Server では、```wevtutil.exe``` もサポートしています。このコマンドレットを使用すると、イベント ログと発行元に関する情報を取得できます。 詳細については、[wevtutil.exe のドキュメント](https://aka.ms/qvod7p)を参照してください。 

### <a name="graphical-interface-tools"></a>グラフィカル インターフェイス ツール
[Web ベースのサーバー管理ツール](https://blogs.technet.microsoft.com/servermanagement/2016/08/17/deploy-setup-server-management-tools/)を使用して、Nano Server ターゲットをリモートで管理し、Web ブラウザーで Nano Server のイベント ログを表示できます。 最後に、MMC スナップイン イベント ビューアー (eventvwr.msc) を使用して、ログを表示することもできます (コンピューターのデスクトップで開き、リモートの Nano Server を参照するだけです)。




## <a name="using-windows-powershell-desired-state-configuration-with-nano-server"></a>Nano Server に対して Windows PowerShell Desired State Configuration を使用する  
  
Windows PowerShell Desired State Configuration (DSC) で Nano Server をターゲット ノードとして管理できます。 現在、DSC ではプッシュ モードでのみ Nano Server を実行しているノードを管理できます。 一部の DSC 機能は Nano Server に対して機能しません。  
  
詳細については、「[DSC on Nano Server の使用](https://msdn.microsoft.com/powershell/dsc/nanoDsc)」を参照してください。  
