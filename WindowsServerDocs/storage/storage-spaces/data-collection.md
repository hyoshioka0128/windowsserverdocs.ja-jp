---
title: 記憶域スペース ダイレクトの診断データを収集します。
description: 記憶域スペース ダイレクト データ コレクション ツールを実行し、それらを使用する方法の具体例について理解します。
keywords: 記憶域スペース、データの収集、トラブルシューティング、イベントのチャネル、Get SDDCDiagnosticInfo
ms.assetid: ''
ms.prod: windows-server-threshold
ms.author: adagashe
ms.technology: storage-spaces
ms.topic: article
author: adagashe
ms.date: 10/24/2018
ms.localizationpriority: ''
ms.openlocfilehash: eaa7d92fe6f77697614cacf1405a25e5a42e14b7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880273"
---
# <a name="collect-diagnostic-data-with-storage-spaces-direct"></a>記憶域スペース ダイレクトの診断データを収集します。

> 適用対象:Windows Server 2019、Windows Server 2016

記憶域スペース ダイレクトとフェールオーバー クラスターのトラブルシューティングに必要なデータを収集するために使用できるさまざまな診断ツールがあります。 この記事では、説明に**Get SDDCDiagnosticInfo** -クラスターの診断に役立つすべての関連情報を収集する 1 つのタッチ ツール。

<!-- The health summary report is a great start to understanding the status of your system to start diagnosing an issue. -->

ログとその他の情報を指定する**Get SDDCDiagnosticInfo**は高密度で、次に示すトラブルシューティングの情報は、問題をエスカレート済みし、する可能性のある高度なトラブルシューティングに役立つになりますデータの方針を Microsoft に送信する必要があります。

<!--
## Collecting live dumps

Windows will trigger the collection of a ``` LiveDump ``` when there are known resources that are hanging in kernel calls. ``` RHS ``` will trigger ```LiveDump``` collection if both the resource type and cluster ``` DumpPolicy ``` are set to 1. For physical disk it is set out of the box
-->

## <a name="installing-get-sddcdiagnosticinfo"></a>Get SDDCDiagnosticInfo をインストールします。

**Get SDDCDiagnosticInfo** PowerShell コマンドレット (別名。 **Get-PCStorageDiagnosticInfo**、旧称**テスト StorageHealth**) のログを収集し、実行に使用できる記憶域スペース (フェールオーバー クラスター (クラスター、リソース、ネットワーク、ノード) の正常性チェック物理ディスク、エンクロージャ、仮想ディスク)、クラスターの共有ボリューム、SMB ファイル共有、および重複除去します。 

以下のアウトラインをどちらも、スクリプトをインストールする 2 つの方法はあります。

### <a name="powershell-gallery"></a>PowerShell ギャラリー

[PowerShell ギャラリー](https://www.powershellgallery.com/packages/PrivateCloud.DiagnosticInfo)は GitHub リポジトリのスナップショットです。 PowerShell ギャラリーから項目をインストールすると、これは、Windows Management Framework (WMF) 5.0、または MSI ベースのインストーラー (PowerShell 3 および 4) を Windows 10 で使用可能な PowerShellGet モジュールの最新バージョンが必要がありますに注意してください。

管理者特権で PowerShell で、次のコマンドの実行中で、モジュールをインストールできます。

``` PowerShell
Install-PackageProvider NuGet -Force
Install-Module PrivateCloud.DiagnosticInfo -Force
Import-Module PrivateCloud.DiagnosticInfo -Force
```

モジュールを更新するには、PowerShell で次のコマンドを実行します。

``` PowerShell
Update-Module PrivateCloud.DiagnosticInfo
```

### <a name="github"></a>GitHub

[GitHub リポジトリ](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/)継続的に反復処理をここでは、モジュールの最新バージョン。 GitHub からモジュールをインストールするから最新のモジュールをダウンロード、[アーカイブ](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/archive/master.zip)PrivateCloud.DiagnosticInfo ディレクトリによって示される正しい PowerShell モジュールのパスへの抽出と ```$env:PSModulePath```

``` PowerShell
# Allowing Tls12 and Tls11 -- e.g. github now requires Tls12
# If this is not set, the Invoke-WebRequest fails with "The request was aborted: Could not create SSL/TLS secure channel."
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
$module = 'PrivateCloud.DiagnosticInfo'
Invoke-WebRequest -Uri https://github.com/PowerShell/$module/archive/master.zip -OutFile $env:TEMP\master.zip
Expand-Archive -Path $env:TEMP\master.zip -DestinationPath $env:TEMP -Force
if (Test-Path $env:SystemRoot\System32\WindowsPowerShell\v1.0\Modules\$module) {
    rm -Recurse $env:SystemRoot\System32\WindowsPowerShell\v1.0\Modules\$module -ErrorAction Stop
    Remove-Module $module -ErrorAction SilentlyContinue
} else {
    Import-Module $module -ErrorAction SilentlyContinue
} 
if (-not ($m = Get-Module $module -ErrorAction SilentlyContinue)) {
    $md = "$env:ProgramFiles\WindowsPowerShell\Modules"
} else {
    $md = (gi $m.ModuleBase -ErrorAction SilentlyContinue).PsParentPath
    Remove-Module $module -ErrorAction SilentlyContinue
    rm -Recurse $m.ModuleBase -ErrorAction Stop
}
cp -Recurse $env:TEMP\$module-master\$module $md -Force -ErrorAction Stop
rm -Recurse $env:TEMP\$module-master,$env:TEMP\master.zip
Import-Module $module -Force

``` 

オフラインのクラスターでこのモジュールを取得する必要がある場合、zip のダウンロード、ターゲットのサーバー ノードに移動し、モジュールをインストールします。

## <a name="gathering-logs"></a>ログを収集しています

イベント チャネルを有効にし、インストール プロセスが完了したら後、は、取得するモジュールで、Get SDDCDiagnosticInfo PowerShell コマンドレットを使用できます。

- ストレージのヘルス状態と異常なコンポーネントの詳細レポート
- 記憶域の容量プール、ボリュームおよび重複除去されたボリュームでのレポート
- すべてのクラスター ノードと、エラーの一覧レポートからのイベント ログ

記憶域クラスターに、名前が付いていると仮定 *"CLUS01"。*

リモート記憶域クラスターに対して実行されます。

``` PowerShell
Get-SDDCDiagnosticInfo -ClusterName CLUS01
```

クラスター化された記憶域 ノードでローカルに実行します。

``` PowerShell
Get-SDDCDiagnosticInfo
```

指定したフォルダーに結果の保存。

``` PowerShell
Get-SDDCDiagnosticInfo -WriteToPath D:\Folder 
```

実際のクラスターでのこのしくみの例を次に示します。

``` PowerShell
New-Item -Name SDDCDiagTemp -Path d:\ -ItemType Directory -Force
Get-SddcDiagnosticInfo -ClusterName S2D-Cluster -WriteToPath d:\SDDCDiagTemp
```

ご覧のとおり、スクリプトもクラスターの現在の状態の検証を行う

![データ コレクションの powershell スクリーン ショット](media/data-collection/CollectData.png)

すべてのデータが SDDCDiagTemp フォルダーに書き込まれているように、

![データのファイル エクスプ ローラーのスクリーン ショット](media/data-collection/CollectDataFolder.png)

スクリプトが完了すると、ユーザーのディレクトリに ZIP が作成されます。

![データの zip の powershell スクリーン ショット](media/data-collection/CollectDataResult.png)

テキスト ファイルにレポートを生成しましょう

```PowerShell
#find the latest diagnostic zip in UserProfile
    $DiagZip=(get-childitem $env:USERPROFILE | where Name -like HealthTest*.zip)
    $LatestDiagPath=($DiagZip | sort lastwritetime | select -First 1).FullName
#expand to temp directory
    New-Item -Name SDDCDiagTemp -Path d:\ -ItemType Directory -Force
    Expand-Archive -Path $LatestDiagPath -DestinationPath D:\SDDCDiagTemp -Force
#generate report and save to text file
    $report=Show-SddcDiagnosticReport -Path D:\SDDCDiagTemp
    $report | out-file d:\SDDCReport.txt
    
```

リファレンスについてへのリンクをここでは、[サンプル レポート](https://github.com/Microsoft/WSLab/blob/dev/Scenarios/S2D%20Tools/Get-SDDCDiagnosticInfo/SDDCReport.txt)と[サンプル zip](https://github.com/Microsoft/WSLab/blob/dev/Scenarios/S2D%20Tools/Get-SDDCDiagnosticInfo/HealthTest-S2D-Cluster-20180522-1546.ZIP)します。

Windows Admin Center (バージョン 1812 以降) でこれを表示するに移動し、*診断*タブ。次のスクリーン ショットで確認できます。 

- 診断ツールをインストールします。
- 更新 (最新ではない) 場合、 
- 毎日の診断の実行をスケジュール (低いシステムに影響を与えるには、通常の実行があるこれら < バック グラウンドで 5 分間、クラスターで 500 mb を超えるを占有しません)
- 以前、ビューでは、サポートしたり、自分で分析を指定する必要がある場合に診断情報を収集します。

![wac 診断のスクリーン ショット](media/data-collection/Wac.png)

## <a name="get-sddcdiagnosticinfo-output"></a>Get SDDCDiagnosticInfo 出力

Get SDDCDiagnosticInfo の zip 形式の出力に含まれるファイルを次に示します。

### <a name="health-summary-report"></a>正常性の概要レポート

正常性の概要レポートとしてを保存されます。
- 0_CloudHealthSummary.log

このファイルは収集され、システムの簡単な概要を提供するものでは、すべてのデータを解析した後に生成されます。 含まれています。

- システム情報
- 記憶域の正常性の概要 (数、リソース オンラインの場合、クラスターの共有ボリュームをオンラインのノード、異常なコンポーネントなどの)
- 詳細については、異常なコンポーネント (オフライン、失敗、または保留中のオンラインであるクラスター リソース)
- ファームウェアとドライバーの情報
- プール、物理ディスク、およびボリュームの詳細
- 記憶域のパフォーマンス (パフォーマンス カウンターが収集されます)

このレポートより有用な情報を含めるように継続的に更新中です。 最新情報については、次を参照してください。、 [GitHub README](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/edit/master/README.md)します。

### <a name="logs-and-xml-files"></a>ログと XML ファイル

スクリプトでは、さまざまなログの収集スクリプトを実行し、出力を xml ファイルとして保存します。 クラスターと正常性のログ、システム情報 (MSInfo32)、フィルター処理されていないイベントのログ (フェールオーバー クラスタ リング、dis 診断、hyper-v の概要、記憶域スペースなど)、およびストレージの診断情報を収集します (操作ログ)。 収集される情報の最新情報については、次を参照してください。、 [(どのような収集) GitHub README](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/blob/master/README.md#what-does-the-cmdlet-output-include)します。

<!--
## Enabling event channels

When Windows Server is installed, many event channels are enabled by default. But sometimes when diagnosing an issue, we want to be able to enable some of these event channels since it will help in triaging and diagnosing system issues.

You could enable additional event channels on each server node in your cluster as needed; however, this approach presents two problems:

1. You need to remember to enable the same event channels on every new server node that you add to your cluster.
2. When diagnosing, it can be tedious to enable specific event channels, reproduce the error, and repeat this process until you root cause.

To avoid these issues, you can enable event channels on cluster startup. The list of enabled event channels on your cluster can be configured using the public property **EnabledEventLogs**. By default, the following event channels are enabled:

```powershell
PS C:\Windows\system32> (get-cluster).EnabledEventLogs
```

Here's an example of the output:
```
Microsoft-Windows-Hyper-V-VmSwitch-Diagnostic,4,0xFFFFFFFD
Microsoft-Windows-SMBDirect/Debug,4
Microsoft-Windows-SMBServer/Analytic
Microsoft-Windows-Kernel-LiveDump/Analytic
```

The **EnabledEventLogs** property is a multistring, where each string is in the form: **channel-name, log-level, keyword-mask**. The **keyword-mask** can be a hexadecimal (prefix 0x), octal (prefix 0), or decimal number (no prefix) number that each event contains (so you can filter by it). For instance, to add a new event channel to the list and to configure both **log-level** and **keyword-mask** you can run:

```powershell
(get-cluster).EnabledEventLogs += "Microsoft-Windows-WinINet/Analytic,2,321"
```

If you want to set the **log-level** but keep the **keyword-mask** at its default value, you can use either of the following commands:

```powershell
(get-cluster).EnabledEventLogs += "Microsoft-Windows-WinINet/Analytic,2"
(get-cluster).EnabledEventLogs += "Microsoft-Windows-WinINet/Analytic,2,"
```

If you want to keep the **log-level** at its default value, but set the **keyword-mask** you can run the following command:

```powershell
(get-cluster).EnabledEventLogs += "Microsoft-Windows-WinINet/Analytic,,0xf1"
```

If you want to keep both the **log-level** and the **keyword-mask** at their default values, you can run any of the following commands:

```powershell
(get-cluster).EnabledEventLogs += "Microsoft-Windows-WinINet/Analytic"
(get-cluster).EnabledEventLogs += "Microsoft-Windows-WinINet/Analytic,"
(get-cluster).EnabledEventLogs += "Microsoft-Windows-WinINet/Analytic,,"
```

These event channels will be enabled on every cluster node when the cluster service starts or whenever the **EnabledEventLogs** property is changed.
-->

## <a name="how-to-consume-the-xml-files-from-get-pcstoragediagnosticinfo"></a>Get PCStorageDiagnosticInfo から XML ファイルを使用する方法
によって収集されたデータで提供されている XML ファイルからデータを使用することができます、 **Get PCStorageDiagnosticInfo**コマンドレット。 これらのファイルがある情報について、仮想ディスク、物理ディスク、クラスターの基本情報およびその他の PowerShell の出力に関連します。 

これらの出力の結果を表示するには、PowerShell ウィンドウを開き、次の手順を実行します。 

```PowerShell
ipmo storage
$d = import-clixml <filename> 
$d
```

## <a name="what-to-expect-next"></a>次に期待するでしょうか。
多くの機能強化と SDDC システム正常性を分析する新しいコマンドレットです。
問題を提出して希望ものに関するフィードバックを提供[ここ](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/issues)します。 また、気軽に送信することで、スクリプトに変更を投稿、[プル要求](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/pulls)します。
