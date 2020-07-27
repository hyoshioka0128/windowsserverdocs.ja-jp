---
title: Nano Server の PowerShell
description: Nano Server 上の縮小された PowerShell 機能セットにおける相違点
ms.prod: windows-server
manager: DonGill
ms.technology: server-nano
ms.topic: article
ms.assetid: 9b25b939-1e2c-4bed-a8d3-2a8e8e46b53d
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: 6535cb9cc6ad77d4ea5e5e33c2d28e03fd447968
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86963581"
---
# <a name="powershell-on-nano-server"></a>Nano Server の PowerShell

> 適用先:Windows Server 2016

> [!IMPORTANT]
> Windows Server バージョン 1709 以降では、Nano Server は[コンテナーの基本 OS イメージ](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image)としてのみ提供されます。 その意味については、[Nano Server に加えられる変更](nano-in-semi-annual-channel.md)に関する記事をご覧ください。

## <a name="powershell-editions"></a>PowerShell のエディション

PowerShell は、バージョン 5.1 以降、機能セットとプラットフォーム互換性が異なるさまざまなエディションが提供されるようになりました。

- **Desktop Edition:** .NET Framework 上に構築され、Windows の完全フットプリント エディション (Server Core、Windows Desktop など) で実行される PowerShell のバージョンをターゲットとするスクリプトおよびモジュールと互換性があります。
- **Core Edition:** .NET Core 上に構築され、Windows のフットプリントが小さいエディション (Nano Server、Windows IoT など) で実行される PowerShell のバージョンをターゲットとするスクリプトおよびモジュールと互換性があります。

PowerShell の実行中のエディションは、$PSVersionTable の PSEdition プロパティに表示されます。
```powershell
$PSVersionTable

Name                           Value
----                           -----
PSVersion                      5.1.14300.1000
PSEdition                      Desktop
PSCompatibleVersions           {1.0, 2.0, 3.0, 4.0...}
CLRVersion                     4.0.30319.42000
BuildVersion                   10.0.14300.1000
WSManStackVersion              3.0
PSRemotingProtocolVersion      2.3
SerializationVersion           1.1.0.1
```

モジュールの作成者は、CompatiblePSEditions モジュール マニフェスト キーを使用して、モジュールが 1 つまたは複数の PowerShell エディションと互換性があることを宣言できます。 このキーは、PowerShell 5.1 以降でのみサポートされます。
```powershell
New-ModuleManifest -Path .\TestModuleWithEdition.psd1 -CompatiblePSEditions Desktop,Core -PowerShellVersion 5.1
$moduleInfo = Test-ModuleManifest -Path \TestModuleWithEdition.psd1
$moduleInfo.CompatiblePSEditions
Desktop
Core

$moduleInfo | Get-Member CompatiblePSEditions

   TypeName: System.Management.Automation.PSModuleInfo

Name                 MemberType Definition
----                 ---------- ----------
CompatiblePSEditions Property   System.Collections.Generic.IEnumerable[string] CompatiblePSEditions {get;}

```
利用可能なモジュールの一覧を取得するとき、PowerShell のエディションで一覧にフィルターを適用できます。
```powershell
Get-Module -ListAvailable | ? CompatiblePSEditions -Contains Desktop

    Directory: C:\Program Files\WindowsPowerShell\Modules


ModuleType Version    Name                                ExportedCommands
---------- -------    ----                                ----------------
Manifest   1.0        ModuleWithPSEditions

Get-Module -ListAvailable | ? CompatiblePSEditions -Contains Core | % CompatiblePSEditions
Desktop
Core

```
スクリプトの作成者は、#requires ステートメントに PSEdition パラメーターを使用することで、PowerShell の互換性のあるエディション以外でスクリプトが実行されるのを防止できます。
```powershell
Set-Content C:\script.ps1 -Value #requires -PSEdition Core
Get-Process -Name PowerShell
Get-Content C:\script.ps1
#requires -PSEdition Core
Get-Process -Name PowerShell

C:\script.ps1
C:\script.ps1 : The script 'script.ps1' cannot be run because it contained a #requires statement for PowerShell editions 'Core'. The edition of PowerShell that is required by the script does not match the currently running PowerShell Desktop edition.
At line:1 char:1
+ C:\script.ps1
+ ~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (script.ps1:String) [], RuntimeException
    + FullyQualifiedErrorId : ScriptRequiresUnmatchedPSEdition
```

## <a name="differences-in-powershell-on-nano-server"></a>Nano Server 上の PowerShell の相違点
すべての Nano Server インストールには PowerShell Core が既定で含まれます。 PowerShell Core は、.NET Core に基づいて作成された PowerShell のフットプリントが小さいエディションであり、Windows のフットプリントが小さいエディション (Nano Server、Windows IoT Core など) で動作します。 PowerShell Core は、PowerShell の他のエディション (Windows Server 2016 で実行される Windows PowerShell など) と同じように動作します。 ただし、Nano Server のフットプリントが小さいため、Nano Server 上の PowerShell Core では、Windows Server 2016 の PowerShell 機能のうち、使用できない機能があります。


**Nano Server で使用できない Windows PowerShell の機能**
* ADSI、ADO、および WMI の型アダプター
* Enable-PSRemoting、Disable-PSRemoting (PowerShell リモート処理は既定で有効になります。「[Nano Server のインストール](Getting-Started-with-Nano-Server.md)」の「Windows PowerShell リモート処理を使用する」を参照してください)。
* スケジュールされたジョブと PSScheduledJob モジュール
* ドメインに参加するための Computer コマンドレット { Add | Remove } (Nano Server をドメインに参加させるさまざまな方法については、「[Nano Server のインストール](Getting-Started-with-Nano-Server.md)」の「Nano Server のドメインへの参加」を参照してください)。
* Reset-ComputerMachinePassword、Test-ComputerSecureChannel
* プロファイル (受信リモート接続のスタートアップ スクリプトは `Set-PSSessionConfiguration` を使用して追加できます)
* クリップボードのコマンドレット
* EventLog コマンドレット { Clear | Get | Limit | New | Remove | Show | Write } (代わりに、New-WinEvent コマンドレットと Get-WinEvent コマンドレットを使用します)
* Get-PfxCertificate コマンドレット
* TraceSource コマンドレット { Get | Set }
* Counter コマンドレット { Get | Export | Import }
* 一部の Web 関連コマンドレット { New-WebServiceProxy、Send-MailMessage、ConvertTo-Html }
* PSDiagnostics モジュールを使用したログおよびトレース
* Get-HotFix (Nano Server での更新プログラムの入手と管理については、「[Nano Server の管理](Manage-Nano-Server.md)」を参照してください)
* 暗黙的なリモート処理コマンドレット { Export-PSSession | Import-PSSession }
* New-PSSessionOption
* PowerShell のトランザクションと Transaction コマンドレット { Complete | Get | Start | Undo | Use }
* PowerShell ワークフローのインフラストラクチャ、モジュール、およびコマンドレット
* Out-Printer
* Update-List
* WMI v1 コマンドレット:Get-WmiObject、Invoke-WmiMethod、Register-WmiEvent、Remove-WmiObject、Set-WmiInstance (代わりに、CimCmdlets モジュールを使用します)

## <a name="using-windows-powershell-desired-state-configuration-with-nano-server"></a>Nano Server に対して Windows PowerShell Desired State Configuration を使用する

Windows PowerShell Desired State Configuration (DSC) で Nano Server をターゲット ノードとして管理できます。 現在、DSC ではプッシュ モードでのみ Nano Server を実行しているノードを管理できます。 一部の DSC 機能は Nano Server に対して機能しません。

詳細については、「[DSC on Nano Server の使用](/powershell/scripting/dsc/getting-started/nanodsc)」を参照してください。
