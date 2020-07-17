---
title: 記憶域スペースダイレクトを使用した診断データの収集
description: 記憶域スペースダイレクトのデータ収集ツールとその実行方法の具体的な例について説明します。
ms.prod: windows-server
ms.author: adagashe
ms.technology: storage-spaces
ms.topic: article
author: adagashe
ms.date: 10/24/2018
ms.openlocfilehash: 75a74017f48b357dd029b062a7ce06775836bd0a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858965"
---
# <a name="collect-diagnostic-data-with-storage-spaces-direct"></a>記憶域スペースダイレクトを使用した診断データの収集

> 適用対象: Windows Server 2019、Windows Server 2016

記憶域スペースダイレクトとフェールオーバークラスターのトラブルシューティングに必要なデータを収集するために使用できるさまざまな診断ツールがあります。 この記事では、 **SDDCDiagnosticInfo** -クラスターの診断に役立つすべての関連情報を収集するワンタッチツールに注目します。

**SDDCDiagnosticInfo**のログやその他の情報が高密度であることを考えると、以下に示すトラブルシューティングの情報は、エスカレートされた高度な問題のトラブルシューティングに役立ちます。また、トリアージのためにデータをマイクロソフトに送信することが必要になる場合があります。

## <a name="installing-get-sddcdiagnosticinfo"></a>SDDCDiagnosticInfo をインストールしています

**SDDCDiagnosticInfo** PowerShell コマンドレット ( **PCStorageDiagnosticInfo**(以前の**テスト-storagehealth**) を使用すると、フェールオーバークラスタリング (クラスター、リソース、ネットワーク、ノード)、記憶域スペース (物理ディスク、エンクロージャ、仮想ディスク)、クラスターの共有ボリューム、SMB ファイル共有、および重複除去のログを収集し、正常性チェックを実行できます。 

スクリプトをインストールする方法は2つあります。どちらも以下のようなものです。

### <a name="powershell-gallery"></a>PowerShell ギャラリー

[PowerShell ギャラリー](https://www.powershellgallery.com/packages/PrivateCloud.DiagnosticInfo)は、GitHub リポジトリのスナップショットです。 PowerShell ギャラリーから項目をインストールするには、PowerShellGet モジュールの最新バージョンが必要であることに注意してください。これは、Windows 10、Windows Management Framework (WMF) 5.0、または MSI ベースのインストーラー (PowerShell 3 および4の場合) で使用できます。

[Microsoft ネットワーク診断ツール](https://www.powershellgallery.com/packages/MSFT.Network.Diag)の最新バージョンは、SDDCDiagnosticInfo がこれに依存しているため、このプロセス中にもインストールされます。 このマニフェストモジュールには、microsoft の Microsoft Core ネットワーク製品グループによって管理されるネットワーク診断およびトラブルシューティングツールが含まれています。

モジュールをインストールするには、PowerShell で管理者特権を使用して次のコマンドを実行します。

``` PowerShell
Install-PackageProvider NuGet -Force
Install-Module PrivateCloud.DiagnosticInfo -Force
Import-Module PrivateCloud.DiagnosticInfo -Force
Install-Module -Name MSFT.Network.Diag
```

モジュールを更新するには、PowerShell で次のコマンドを実行します。

``` PowerShell
Update-Module PrivateCloud.DiagnosticInfo
```

### <a name="github"></a>GitHub

[GitHub リポジトリ](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/)は、このモジュールの最新バージョンです。ここでは繰り返し反復しているためです。 GitHub からモジュールをインストールするには、[アーカイブ](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/archive/master.zip)から最新のモジュールをダウンロードし、PrivateCloud ディレクトリを正しい PowerShell モジュールパスに抽出し ```$env:PSModulePath```

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

オフラインクラスターでこのモジュールを入手する必要がある場合は、zip ファイルをダウンロードし、ターゲットサーバーノードに移動して、モジュールをインストールします。

## <a name="gathering-logs"></a>ログの収集

イベントチャネルを有効にし、インストールプロセスを完了したら、モジュールの SDDCDiagnosticInfo PowerShell コマンドレットを使用して次を取得できます。

- ストレージの正常性に関するレポート、および異常なコンポーネントの詳細
- プール、ボリューム、重複除去ボリューム別の記憶域容量のレポート
- すべてのクラスターノードからのイベントログとエラー報告の概要

記憶域クラスターに *"CLUS01"* という名前が付いているとします。

リモート記憶域クラスターに対して実行するには、次のようにします。

``` PowerShell
Get-SDDCDiagnosticInfo -ClusterName CLUS01
```

クラスター化された記憶域ノードでローカルに実行するには:

``` PowerShell
Get-SDDCDiagnosticInfo
```

指定したフォルダーに結果を保存するには:

``` PowerShell
Get-SDDCDiagnosticInfo -WriteToPath D:\Folder 
```

実際のクラスターでは、次の例のようになります。

``` PowerShell
New-Item -Name SDDCDiagTemp -Path d:\ -ItemType Directory -Force
Get-SddcDiagnosticInfo -ClusterName S2D-Cluster -WriteToPath d:\SDDCDiagTemp
```

ご覧のとおり、スクリプトは現在のクラスター状態の検証も行います。

![データコレクション powershell のスクリーンショット](media/data-collection/CollectData.png)

ご覧のように、すべてのデータは SDDCDiagTemp フォルダーに書き込まれています。

![エクスプローラーのデータのスクリーンショット](media/data-collection/CollectDataFolder.png)

スクリプトが完了すると、ユーザーディレクトリに ZIP が作成されます。

![powershell でのデータ zip のスクリーンショット](media/data-collection/CollectDataResult.png)

レポートをテキストファイルに生成しましょう

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

参考までに、[サンプルレポート](https://github.com/Microsoft/WSLab/blob/dev/Scenarios/S2D%20Tools/Get-SDDCDiagnosticInfo/SDDCReport.txt)と[サンプル zip](https://github.com/Microsoft/WSLab/blob/dev/Scenarios/S2D%20Tools/Get-SDDCDiagnosticInfo/HealthTest-S2D-Cluster-20180522-1546.ZIP)へのリンクを示します。

Windows 管理センター (バージョン1812以降) でこれを表示するには、[*診断*] タブに移動します。次のスクリーンショットに示すように、次のようにします。 

- 診断ツールのインストール
- 更新 (最新ではない場合) 
- 毎日の診断の実行をスケジュールします (これらはシステムに影響が少ないため、通常はバックグラウンドで5分 < かかり、クラスターで 500 mb を超えることはありません)。
- 以前に収集した診断情報を自分でサポートまたは分析する必要がある場合は、それを表示します。

![wac diagnostics スクリーンショット](media/data-collection/Wac.png)

## <a name="get-sddcdiagnosticinfo-output"></a>SDDCDiagnosticInfo の出力

SDDCDiagnosticInfo の zip 形式の出力に含まれるファイルを次に示します。

### <a name="health-summary-report"></a>正常性の概要レポート

正常性の概要レポートは、次の形式で保存されます。
- 0_CloudHealthSummary .log

このファイルは収集されたすべてのデータを解析した後に生成され、システムの概要を簡単に示すために使用されます。 次のものが含まれます。

- システム情報
- 記憶域の正常性の概要 (ノードの数の上限、リソースオンライン、クラスターの共有ボリュームオンライン、異常なコンポーネントなど)
- 異常なコンポーネント (オフライン、失敗、またはオンラインの保留中のクラスターリソース) の詳細
- ファームウェアとドライバーの情報
- プール、物理ディスク、ボリュームの詳細
- ストレージのパフォーマンス (パフォーマンスカウンターが収集されます)

このレポートは、より有用な情報を含むように継続的に更新されています。 最新情報については、 [GitHub の README](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/edit/master/README.md)を参照してください。

### <a name="logs-and-xml-files"></a>ログと XML ファイル

このスクリプトは、さまざまなログ収集スクリプトを実行し、出力を xml ファイルとして保存します。 クラスターおよび正常性ログ、システム情報 (MSInfo32)、フィルター処理されていないイベントログ (フェールオーバークラスタリング、非診断、hyper-v、記憶域スペースなど)、および記憶域診断情報 (操作ログ) を収集します。 収集される情報の最新情報については、 [GitHub の README (収集内容)](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/blob/master/README.md#what-does-the-cmdlet-output-include)を参照してください。

## <a name="how-to-consume-the-xml-files-from-get-pcstoragediagnosticinfo"></a>PCStorageDiagnosticInfo から XML ファイルを使用する方法
**PCStorageDiagnosticInfo**コマンドレットによって収集されたデータに含まれている XML ファイルのデータを使用できます。 これらのファイルには、仮想ディスク、物理ディスク、基本クラスター情報、およびその他の PowerShell 関連の出力に関する情報が含まれています。 

これらの出力の結果を表示するには、PowerShell ウィンドウを開き、次の手順を実行します。 

```PowerShell
ipmo storage
$d = import-clixml <filename> 
$d
```

## <a name="what-to-expect-next"></a>次に期待されること
SDDC システムの正常性を分析するための多数の機能強化と新しいコマンドレット。
[ここで](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/issues)問題を報告することで、表示する内容に関するフィードバックを提供します。 また、[プル要求](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/pulls)を送信することで、スクリプトに対する有益な変更を自由に投稿できます。
