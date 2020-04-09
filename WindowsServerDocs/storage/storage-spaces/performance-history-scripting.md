---
title: 記憶域スペースダイレクトパフォーマンス履歴を使用したスクリプト作成
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4c25ed4112035fa729ccf17792a846263ec68dfc
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856175"
---
# <a name="scripting-with-powershell-and-storage-spaces-direct-performance-history"></a>PowerShell と記憶域スペースダイレクトパフォーマンス履歴を使用したスクリプト

> 適用対象: Windows Server 2019

Windows Server 2019 では、[記憶域スペースダイレクト](storage-spaces-direct-overview.md)は、仮想マシン、サーバー、ドライブ、ボリューム、ネットワークアダプターなどのさまざまな[パフォーマンス履歴](performance-history.md)を記録して格納します。 パフォーマンス履歴は PowerShell でのクエリと処理が簡単であるため、*生データ*から次*のような質問にすばやく*アクセスできます。

1. 先週、CPU のスパイクが発生しましたか?
2. 物理ディスクに異常な待機時間が発生しているか。
3. 現時点で最も多くのストレージ IOPS を消費しているのはどの Vm ですか。
4. ネットワーク帯域幅が飽和状態になっていますか。
5. このボリュームの空き領域がなくなるのはいつですか?
6. 過去1か月間、どの Vm で最も多くのメモリが使用されていましたか。

`Get-ClusterPerf` コマンドレットは、スクリプト用に構築されています。 これは、`Get-VM` のようなコマンドレットからの入力、またはパイプラインによって関連付けを処理する `Get-PhysicalDisk` を受け取り、`Sort-Object`、`Where-Object`、`Measure-Object` などのユーティリティコマンドレットに出力をパイプ処理して、強力なクエリをすばやく作成できます。

**このトピックでは、上記6つの質問に回答する6つのサンプルスクリプトについて説明します。** さまざまなデータや期間にわたって、ピークの検索、平均の検索、傾向線のプロット、外れ値検出の実行などを行うために適用できるパターンが用意されています。 これらのファイルは、コピー、拡張、再利用のための無料のスタートコードとして提供されています。

   > [!NOTE]
   > 簡潔にするため、サンプルスクリプトでは、高品質の PowerShell コードを想定しているようなエラー処理を省略しています。 これらは、主に運用環境ではなく、インスピレーションと教育を目的としています。

## <a name="sample-1-cpu-i-see-you"></a>サンプル 1: CPU、ご確認ください。

このサンプルでは、`LastWeek` の期間の `ClusterNode.Cpu.Usage` シリーズを使用して、クラスター内の各サーバーの最大 CPU 使用率を表示します。 また、過去8日間の CPU 使用率が25%、50%、75% を超えた時間を示す単純な四分の分析も行います。

### <a name="screenshot"></a>Screenshot

次のスクリーンショットでは、*サーバー-02*に先週のスパイクがあることがわかります。

![PowerShell のスクリーンショット](media/performance-history/Show-CpuMinMaxAvg.png)

### <a name="how-it-works"></a>方法

パイプを `Get-ClusterPerf` 組み込みの `Measure-Object` コマンドレットに出力すると、`Value` プロパティを指定するだけです。 `-Maximum`、`-Minimum`、および `-Average` フラグを使用して、`Measure-Object` 最初の3列を無料で提供します。 四分の分析を行うには、パイプを使用して `Where-Object` に `-Gt`、25、50、または75よりも大きい値の数をカウントします。 最後の手順では、`Format-Hours` と `Format-Percent` ヘルパー関数を整形します。もちろん、省略可能です。

### <a name="script"></a>スクリプト

スクリプトは次のようになります。

```
Function Format-Hours {
    Param (
        $RawValue
    )
    # Weekly timeframe has frequency 15 minutes = 4 points per hour
    [Math]::Round($RawValue/4)
}

Function Format-Percent {
    Param (
        $RawValue
    )
    [String][Math]::Round($RawValue) + " " + "%"
}

$Output = Get-ClusterNode | ForEach-Object {
    $Data = $_ | Get-ClusterPerf -ClusterNodeSeriesName "ClusterNode.Cpu.Usage" -TimeFrame "LastWeek"

    $Measure = $Data | Measure-Object -Property Value -Minimum -Maximum -Average
    $Min = $Measure.Minimum
    $Max = $Measure.Maximum
    $Avg = $Measure.Average

    [PsCustomObject]@{
        "ClusterNode"    = $_.Name
        "MinCpuObserved" = Format-Percent $Min
        "MaxCpuObserved" = Format-Percent $Max
        "AvgCpuObserved" = Format-Percent $Avg
        "HrsOver25%"     = Format-Hours ($Data | Where-Object Value -Gt 25).Length
        "HrsOver50%"     = Format-Hours ($Data | Where-Object Value -Gt 50).Length
        "HrsOver75%"     = Format-Hours ($Data | Where-Object Value -Gt 75).Length
    }
}

$Output | Sort-Object ClusterNode | Format-Table
```

## <a name="sample-2-fire-fire-latency-outlier"></a>サンプル 2: 火災、火災、待機時間の外れ値

このサンプルでは、`LastHour` 期間の `PhysicalDisk.Latency.Average` シリーズを使用して、人口平均を超える +3 σ (3 つの標準偏差) を超える時間単位の平均待機時間を持つドライブとして定義された統計外れ値を探します。

   > [!IMPORTANT]
   > 簡潔にするために、このスクリプトは低レベルの分散に対するセーフガードを実装しておらず、部分的な欠損データを処理せず、モデルやファームウェアなどを区別しません。適切な略しを使用してください。ハードディスクを交換するかどうかを判断するために、このスクリプトだけに依存しないでください。 ここでは、教育目的でのみ提供されています。

### <a name="screenshot"></a>Screenshot

次のスクリーンショットには、外れ値がないことがわかります。

![PowerShell のスクリーンショット](media/performance-history/Show-LatencyOutlierHDD.png)

### <a name="how-it-works"></a>方法

まず、`PhysicalDisk.Iops.Total` が一貫して `-Gt 1`されていることを確認して、アイドル状態またはほぼアイドル状態のドライブを除外します。 すべてのアクティブな HDD について、360の測定値で構成される `LastHour` の期間を10秒間隔でパイプして、過去1時間の平均待機時間を取得するように `Measure-Object -Average` します。 これにより、作成が設定されます。

母集団の平均 `μ` と標準偏差 `σ` を検索するために、[広く知ら](http://www.mathsisfun.com/data/standard-deviation.html)れている数式を実装しています。 すべてのアクティブな HDD について、平均待機時間と母集団平均を比較し、標準偏差で除算します。 生の値は保持されるため、結果を `Sort-Object` できますが、`Format-Latency` と `Format-StandardDeviation` ヘルパー関数を使用して、表示される内容を整形ことができます (省略可能)。

ドライブが +3 σよりも多い場合は、赤で `Write-Host` ます。それ以外の場合は、緑色になります。

### <a name="script"></a>スクリプト

スクリプトは次のようになります。

```
Function Format-Latency {
    Param (
        $RawValue
    )
    $i = 0 ; $Labels = ("s", "ms", "μs", "ns") # Petabits, just in case!
    Do { $RawValue *= 1000 ; $i++ } While ( $RawValue -Lt 1 )
    # Return
    [String][Math]::Round($RawValue, 2) + " " + $Labels[$i]
}

Function Format-StandardDeviation {
    Param (
        $RawValue
    )
    If ($RawValue -Gt 0) {
        $Sign = "+"
    }
    Else {
        $Sign = "-"
    }
    # Return
    $Sign + [String][Math]::Round([Math]::Abs($RawValue), 2) + "σ"
}

$HDD = Get-StorageSubSystem Cluster* | Get-PhysicalDisk | Where-Object MediaType -Eq HDD

$Output = $HDD | ForEach-Object {

    $Iops = $_ | Get-ClusterPerf -PhysicalDiskSeriesName "PhysicalDisk.Iops.Total" -TimeFrame "LastHour"
    $AvgIops = ($Iops | Measure-Object -Property Value -Average).Average

    If ($AvgIops -Gt 1) { # Exclude idle or nearly idle drives

        $Latency = $_ | Get-ClusterPerf -PhysicalDiskSeriesName "PhysicalDisk.Latency.Average" -TimeFrame "LastHour"
        $AvgLatency = ($Latency | Measure-Object -Property Value -Average).Average

        [PsCustomObject]@{
            "FriendlyName"  = $_.FriendlyName
            "SerialNumber"  = $_.SerialNumber
            "MediaType"     = $_.MediaType
            "AvgLatencyPopulation" = $null # Set below
            "AvgLatencyThisHDD"    = Format-Latency $AvgLatency
            "RawAvgLatencyThisHDD" = $AvgLatency
            "Deviation"            = $null # Set below
            "RawDeviation"         = $null # Set below
        }
    }
}

If ($Output.Length -Ge 3) { # Minimum population requirement

    # Find mean μ and standard deviation σ
    $μ = ($Output | Measure-Object -Property RawAvgLatencyThisHDD -Average).Average
    $d = $Output | ForEach-Object { ($_.RawAvgLatencyThisHDD - $μ) * ($_.RawAvgLatencyThisHDD - $μ) }
    $σ = [Math]::Sqrt(($d | Measure-Object -Sum).Sum / $Output.Length)

    $FoundOutlier = $False

    $Output | ForEach-Object {
        $Deviation = ($_.RawAvgLatencyThisHDD - $μ) / $σ
        $_.AvgLatencyPopulation = Format-Latency $μ
        $_.Deviation = Format-StandardDeviation $Deviation
        $_.RawDeviation = $Deviation
        # If distribution is Normal, expect >99% within 3σ
        If ($Deviation -Gt 3) {
            $FoundOutlier = $True
        }
    }

    If ($FoundOutlier) {
        Write-Host -BackgroundColor Black -ForegroundColor Red "Oh no! There's an HDD significantly slower than the others."
    }
    Else {
        Write-Host -BackgroundColor Black -ForegroundColor Green "Good news! No outlier found."
    }

    $Output | Sort-Object RawDeviation -Descending | Format-Table FriendlyName, SerialNumber, MediaType, AvgLatencyPopulation, AvgLatencyThisHDD, Deviation

}
Else {
    Write-Warning "There aren't enough active drives to look for outliers right now."
}
```

## <a name="sample-3-noisy-neighbor-thats-write"></a>サンプル 3: 雑音の多い近隣 これで書き込みが可能です。

パフォーマンス履歴は、*現時点*でも質問に回答できます。 新しい測定値は、10秒ごとにリアルタイムで使用できます。 このサンプルでは、`MostRecent` の期間の `VHD.Iops.Total` シリーズを使用して、クラスター内のすべてのホストで最も多くの記憶域 IOPS を消費している仮想マシン ("noisiest" など) を特定し、それらのアクティビティの読み取り/書き込みの内訳を表示します。

### <a name="screenshot"></a>Screenshot

次のスクリーンショットでは、記憶域アクティビティ別の上位10個の仮想マシンが表示されています。

![PowerShell のスクリーンショット](media/performance-history/Show-TopIopsVMs.png)

### <a name="how-it-works"></a>方法

`Get-PhysicalDisk`とは異なり、`Get-VM` コマンドレットはクラスターに対応していません。ローカルサーバー上の Vm のみが返されます。 すべてのサーバーから並列でクエリを実行するには、`Invoke-Command (Get-ClusterNode).Name { ... }`で呼び出しをラップします。 すべての VM に対して、`VHD.Iops.Total`、`VHD.Iops.Read`、および `VHD.Iops.Write` の測定値を取得します。 `-TimeFrame` パラメーターを指定しないと、それぞれに対して1つの `MostRecent` データポイントが取得されます。

   > [!TIP]
   > これらのシリーズは、すべての VHD/VHDX ファイルに対するこの VM のアクティビティの合計を反映しています。 この例では、パフォーマンス履歴が自動的に集計されています。 VHD/VHDX の内訳を取得するために、個々の `Get-VHD` を VM ではなく `Get-ClusterPerf` にパイプすることができます。

すべてのサーバーの結果が `$Output`としてまとめられ、`Sort-Object` して `Select-Object -First 10`できます。 装飾の結果は、その元の場所を示す `PsComputerName` プロパティを使用して `Invoke-Command` します。これは、VM が実行されている場所を知るために印刷できます。

### <a name="script"></a>スクリプト

スクリプトは次のようになります。

```
$Output = Invoke-Command (Get-ClusterNode).Name {
    Function Format-Iops {
        Param (
            $RawValue
        )
        $i = 0 ; $Labels = (" ", "K", "M", "B", "T") # Thousands, millions, billions, trillions...
        Do { if($RawValue -Gt 1000){$RawValue /= 1000 ; $i++ } } While ( $RawValue -Gt 1000 )
        # Return
        [String][Math]::Round($RawValue) + " " + $Labels[$i]
    }

    Get-VM | ForEach-Object {
        $IopsTotal = $_ | Get-ClusterPerf -VMSeriesName "VHD.Iops.Total"
        $IopsRead  = $_ | Get-ClusterPerf -VMSeriesName "VHD.Iops.Read"
        $IopsWrite = $_ | Get-ClusterPerf -VMSeriesName "VHD.Iops.Write"
        [PsCustomObject]@{
            "VM" = $_.Name
            "IopsTotal" = Format-Iops $IopsTotal.Value
            "IopsRead"  = Format-Iops $IopsRead.Value
            "IopsWrite" = Format-Iops $IopsWrite.Value
            "RawIopsTotal" = $IopsTotal.Value # For sorting...
        }
    }
}

$Output | Sort-Object RawIopsTotal -Descending | Select-Object -First 10 | Format-Table PsComputerName, VM, IopsTotal, IopsRead, IopsWrite
```

## <a name="sample-4-as-they-say-25-gig-is-the-new-10-gig"></a>サンプル 4: 「25 gb は新しい 10 gb」と言います。

このサンプルでは、`LastDay` の期間の `NetAdapter.Bandwidth.Total` シリーズを使用して、理論的な最大帯域幅の90% の > として定義されているネットワーク飽和状態を探します。 クラスター内のすべてのネットワークアダプターについて、過去1日の監視されている帯域幅の最大使用量が、示されているリンク速度と比較されます。

### <a name="screenshot"></a>Screenshot

次のスクリーンショットでは、1つの*FABRIKAM NX-4 Pro #2*最後の日にピークされていることがわかります。

![PowerShell のスクリーンショット](media/performance-history/Show-NetworkSaturation.png)

### <a name="how-it-works"></a>方法

上記の `Invoke-Command` トリックを繰り返して、すべてのサーバーとパイプを `Get-ClusterPerf`に `Get-NetAdapter` します。 その過程で、2つの関連するプロパティを取得します。たとえば、"10 Gbps" のような `LinkSpeed` 文字列と、100億のような生の `Speed` 整数です。 `Measure-Object` を使用して、過去1日の平均とピークを取得します (リマインダー: `LastDay` 期間内の各測定値は5分)、1バイトあたり8ビットで乗算して、りんごからの比較を取得します。

   > [!NOTE]
   > Chelsio などの一部のベンダーは、*ネットワークアダプター*のパフォーマンスカウンターにリモートダイレクトメモリアクセス (RDMA) アクティビティを含めているため、`NetAdapter.Bandwidth.Total` シリーズに含まれています。 Mellanox のような他の人は、そうでない場合があります。 ベンダでない場合は、このスクリプトのバージョンで `NetAdapter.Bandwidth.RDMA.Total` シリーズを追加するだけです。

### <a name="script"></a>スクリプト

スクリプトは次のようになります。

```
$Output = Invoke-Command (Get-ClusterNode).Name {

    Function Format-BitsPerSec {
        Param (
            $RawValue
        )
        $i = 0 ; $Labels = ("bps", "kbps", "Mbps", "Gbps", "Tbps", "Pbps") # Petabits, just in case!
        Do { $RawValue /= 1000 ; $i++ } While ( $RawValue -Gt 1000 )
        # Return
        [String][Math]::Round($RawValue) + " " + $Labels[$i]
    }

    Get-NetAdapter | ForEach-Object {

        $Inbound = $_ | Get-ClusterPerf -NetAdapterSeriesName "NetAdapter.Bandwidth.Inbound" -TimeFrame "LastDay"
        $Outbound = $_ | Get-ClusterPerf -NetAdapterSeriesName "NetAdapter.Bandwidth.Outbound" -TimeFrame "LastDay"

        If ($Inbound -Or $Outbound) {

            $InterfaceDescription = $_.InterfaceDescription
            $LinkSpeed = $_.LinkSpeed
    
            $MeasureInbound = $Inbound | Measure-Object -Property Value -Maximum
            $MaxInbound = $MeasureInbound.Maximum * 8 # Multiply to bits/sec
    
            $MeasureOutbound = $Outbound | Measure-Object -Property Value -Maximum
            $MaxOutbound = $MeasureOutbound.Maximum * 8 # Multiply to bits/sec
    
            $Saturated = $False
    
            # Speed property is Int, e.g. 10000000000
            If (($MaxInbound -Gt (0.90 * $_.Speed)) -Or ($MaxOutbound -Gt (0.90 * $_.Speed))) {
                $Saturated = $True
                Write-Warning "In the last day, adapter '$InterfaceDescription' on server '$Env:ComputerName' exceeded 90% of its '$LinkSpeed' theoretical maximum bandwidth. In general, network saturation leads to higher latency and diminished reliability. Not good!"
            }
    
            [PsCustomObject]@{
                "NetAdapter"  = $InterfaceDescription
                "LinkSpeed"   = $LinkSpeed
                "MaxInbound"  = Format-BitsPerSec $MaxInbound
                "MaxOutbound" = Format-BitsPerSec $MaxOutbound
                "Saturated"   = $Saturated
            }
        }
    }
}

$Output | Sort-Object PsComputerName, InterfaceDescription | Format-Table PsComputerName, NetAdapter, LinkSpeed, MaxInbound, MaxOutbound, Saturated
```

## <a name="sample-5-make-storage-trendy-again"></a>サンプル 5: ストレージの trendy を再度作成します。

マクロの傾向を確認するために、パフォーマンス履歴は最大1年間保持されます。 このサンプルでは、`LastYear` の期間の `Volume.Size.Available` シリーズを使用して、ストレージがいっぱいになったときの割合を判断し、それがいっぱいになったときに見積もります。

### <a name="screenshot"></a>Screenshot

次のスクリーンショットでは、*バックアップ*ボリュームが1日あたり約 15 GB を追加していることがわかります。

![PowerShell のスクリーンショット](media/performance-history/Show-StorageTrend.png)

この料金が発生すると、別の42日以内に容量に達します。

### <a name="how-it-works"></a>方法

`LastYear` の期間には1日あたり1つのデータポイントがあります。 傾向線に合わせるために必要なポイントは厳密に2つだけですが、実際には、14日など、さらに多くの点が必要になります。 ここでは、範囲 [1, 14] の*x*の配列 *(x、y)* を設定するために `Select-Object -Last 14` を使用します。 これらのポイントでは、単純な[線形最小二乗アルゴリズム](http://mathworld.wolfram.com/LeastSquaresFitting.html)を実装して、最適な行の*y = ax + b*をパラメーター化する `$A` と `$B` を検索します。 この後も、高校にようこそ。

ボリュームの `SizeRemaining` プロパティを傾向 (傾斜 `$A`) で除算すると、ボリュームがいっぱいになるまで、現在の記憶域の増加率で crudely を見積もることができます。 `Format-Bytes`、`Format-Trend`、および `Format-Days` ヘルパー関数は、出力を整形します。

   > [!IMPORTANT]
   > この見積もりは線形的で、最新の14日単位の測定値に基づいています。 より洗練された正確な手法があります。 優れた略しを使用して、ストレージの拡張に投資するかどうかを判断するために、このスクリプトだけに依存しないでください。 ここでは、教育目的でのみ提供されています。

### <a name="script"></a>スクリプト

スクリプトは次のようになります。

```

Function Format-Bytes {
    Param (
        $RawValue
    )
    $i = 0 ; $Labels = ("B", "KB", "MB", "GB", "TB", "PB", "EB", "ZB", "YB")
    Do { $RawValue /= 1024 ; $i++ } While ( $RawValue -Gt 1024 )
    # Return
    [String][Math]::Round($RawValue) + " " + $Labels[$i]
}

Function Format-Trend {
    Param (
        $RawValue
    )
    If ($RawValue -Eq 0) {
        "0"
    }
    Else {
        If ($RawValue -Gt 0) {
            $Sign = "+"
        }
        Else {
            $Sign = "-"
        }
        # Return
        $Sign + $(Format-Bytes [Math]::Abs($RawValue)) + "/day"
    }
}

Function Format-Days {
    Param (
        $RawValue
    )
    [Math]::Round($RawValue)
}

$CSV = Get-Volume | Where-Object FileSystem -Like "*CSV*"

$Output = $CSV | ForEach-Object {

    $N = 14 # Require 14 days of history

    $Data = $_ | Get-ClusterPerf -VolumeSeriesName "Volume.Size.Available" -TimeFrame "LastYear" | Sort-Object Time | Select-Object -Last $N

    If ($Data.Length -Ge $N) {

        # Last N days as (x, y) points
        $PointsXY = @()
        1..$N | ForEach-Object {
            $PointsXY += [PsCustomObject]@{ "X" = $_ ; "Y" = $Data[$_-1].Value }
        }

        # Linear (y = ax + b) least squares algorithm
        $MeanX = ($PointsXY | Measure-Object -Property X -Average).Average
        $MeanY = ($PointsXY | Measure-Object -Property Y -Average).Average
        $XX = $PointsXY | ForEach-Object { $_.X * $_.X }
        $XY = $PointsXY | ForEach-Object { $_.X * $_.Y }
        $SSXX = ($XX | Measure-Object -Sum).Sum - $N * $MeanX * $MeanX
        $SSXY = ($XY | Measure-Object -Sum).Sum - $N * $MeanX * $MeanY
        $A = ($SSXY / $SSXX)
        $B = ($MeanY - $A * $MeanX)
        $RawTrend = -$A # Flip to get daily increase in Used (vs decrease in Remaining)
        $Trend = Format-Trend $RawTrend

        If ($RawTrend -Gt 0) {
            $DaysToFull = Format-Days ($_.SizeRemaining / $RawTrend)
        }
        Else {
            $DaysToFull = "-"
        }
    }
    Else {
        $Trend = "InsufficientHistory"
        $DaysToFull = "-"
    }

    [PsCustomObject]@{
        "Volume"     = $_.FileSystemLabel
        "Size"       = Format-Bytes ($_.Size)
        "Used"       = Format-Bytes ($_.Size - $_.SizeRemaining)
        "Trend"      = $Trend
        "DaysToFull" = $DaysToFull
    }
}

$Output | Format-Table
```

## <a name="sample-6-memory-hog-you-can-run-but-you-cant-hide"></a>サンプル 6: メモリオートバイは実行できますが、非表示にすることはできません。

パフォーマンス履歴はクラスター全体に対して一元的に収集されて保存されるため、ホスト間で Vm が何回移動するかに関係なく、異なるコンピューターのデータを結合する必要はありません。 このサンプルでは、`LastMonth` 期間の `VM.Memory.Assigned` シリーズを使用して、過去35日間に最も多くのメモリを消費している仮想マシンを特定します。

### <a name="screenshot"></a>Screenshot

次のスクリーンショットでは、過去1か月間のメモリ使用量別の上位10個の仮想マシンが表示されています。

![PowerShell のスクリーンショット](media/performance-history/Show-TopMemoryVMs.png)

### <a name="how-it-works"></a>方法

上記の `Invoke-Command` トリックを繰り返して、すべてのサーバーで `Get-VM` します。 `Measure-Object -Average` を使用して、すべての VM の月単位の平均を取得し、`Sort-Object` 後に `Select-Object -First 10` して、スコアボードを取得します。 (または、これが*最も必要*なリストかもしれません)。

### <a name="script"></a>スクリプト

スクリプトは次のようになります。

```
$Output = Invoke-Command (Get-ClusterNode).Name {
    Function Format-Bytes {
        Param (
            $RawValue
        )
        $i = 0 ; $Labels = ("B", "KB", "MB", "GB", "TB", "PB", "EB", "ZB", "YB")
        Do { if( $RawValue -Gt 1024 ){ $RawValue /= 1024 ; $i++ } } While ( $RawValue -Gt 1024 )
        # Return
        [String][Math]::Round($RawValue) + " " + $Labels[$i]
    }
    
    Get-VM | ForEach-Object {
        $Data = $_ | Get-ClusterPerf -VMSeriesName "VM.Memory.Assigned" -TimeFrame "LastMonth"
        If ($Data) {
            $AvgMemoryUsage = ($Data | Measure-Object -Property Value -Average).Average
            [PsCustomObject]@{
                "VM" = $_.Name
                "AvgMemoryUsage" = Format-Bytes $AvgMemoryUsage.Value
                "RawAvgMemoryUsage" = $AvgMemoryUsage.Value # For sorting...
            }
        }
    }
}

$Output | Sort-Object RawAvgMemoryUsage -Descending | Select-Object -First 10 | Format-Table PsComputerName, VM, AvgMemoryUsage
```

以上で終わりです。 これらのサンプルを使用すると、作業を開始するのに役立ちます。 パフォーマンスの履歴と強力なスクリプトに対応した `Get-ClusterPerf` コマンドレットを使用して、回答を記憶域スペースダイレクトことができます。 – Windows Server 2019 インフラストラクチャを管理および監視する際の複雑な質問。

## <a name="see-also"></a>参照

- [Windows PowerShell の概要](https://docs.microsoft.com/powershell/scripting/getting-started/getting-started-with-windows-powershell)
- [記憶域スペースダイレクトの概要](storage-spaces-direct-overview.md)
- [パフォーマンス履歴](performance-history.md)
