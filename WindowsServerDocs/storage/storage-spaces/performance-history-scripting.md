---
title: 記憶域スペースダイレクトパフォーマンス履歴を使用したスクリプト作成
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 53a5f2aa403c83d24acde1fc57e793141175d9b6
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474719"
---
# <a name="scripting-with-powershell-and-storage-spaces-direct-performance-history"></a>PowerShell と記憶域スペースダイレクトパフォーマンス履歴を使用したスクリプト

> 適用対象:Windows Server 2019

Windows Server 2019 では、[記憶域スペースダイレクト](storage-spaces-direct-overview.md)は、仮想マシン、サーバー、ドライブ、ボリューム、ネットワークアダプターなどのさまざまな[パフォーマンス履歴](performance-history.md)を記録して格納します。 パフォーマンス履歴は PowerShell でのクエリと処理が簡単であるため、*生データ*から次*のような質問にすばやく*アクセスできます。

1. 先週、CPU のスパイクが発生しましたか?
2. 物理ディスクに異常な待機時間が発生しているか。
3. 現時点で最も多くのストレージ IOPS を消費しているのはどの Vm ですか。
4. ネットワーク帯域幅が飽和状態になっていますか。
5. このボリュームの空き領域がなくなるのはいつですか?
6. 過去1か月間、どの Vm で最も多くのメモリが使用されていましたか。

`Get-ClusterPerf`コマンドレットは、スクリプト作成用に構築されています。 またはのようなコマンドレットからの入力を `Get-VM` `Get-PhysicalDisk` 使用してアソシエーションを処理し、その出力を、、などのユーティリティコマンドレットに渡して `Sort-Object` 、 `Where-Object` 強力な `Measure-Object` クエリをすばやく作成することができます。

**このトピックでは、上記6つの質問に回答する6つのサンプルスクリプトについて説明します。** さまざまなデータや期間にわたって、ピークの検索、平均の検索、傾向線のプロット、外れ値検出の実行などを行うために適用できるパターンが用意されています。 これらのファイルは、コピー、拡張、再利用のための無料のスタートコードとして提供されています。

   > [!NOTE]
   > 簡潔にするため、サンプルスクリプトでは、高品質の PowerShell コードを想定しているようなエラー処理を省略しています。 これらは、主に運用環境ではなく、インスピレーションと教育を目的としています。

## <a name="sample-1-cpu-i-see-you"></a>サンプル 1: CPU、ご確認ください。

このサンプルでは、タイムフレームのシリーズを使用して、 `ClusterNode.Cpu.Usage` `LastWeek` クラスター内の各サーバーの最大 CPU 使用率を表示します。 また、過去8日間の CPU 使用率が25%、50%、75% を超えた時間を示す単純な四分の分析も行います。

### <a name="screenshot"></a>Screenshot

次のスクリーンショットでは、*サーバー-02*に先週のスパイクがあることがわかります。

![PowerShell のスクリーンショット](media/performance-history/Show-CpuMinMaxAvg.png)

### <a name="how-it-works"></a>しくみ

`Get-ClusterPerf`パイプから組み込みコマンドレットに適切に出力すると、 `Measure-Object` プロパティを指定するだけ `Value` です。 、、およびの各フラグを使用すると `-Maximum` `-Minimum` `-Average` 、 `Measure-Object` 最初の3つの列がほぼ無料で提供されます。 四分の分析を行うには、パイプを使用 `Where-Object` して、 `-Gt` 25、50、または75の値の数をカウントします。 最後の手順では、 `Format-Hours` とヘルパー関数を整形します。これは確かに `Format-Percent` オプションです。

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

このサンプルでは、タイムフレームのシリーズを使用して `PhysicalDisk.Latency.Average` `LastHour` 、母集団平均を超える +3 σ (3 つの標準偏差) を超える時間単位の平均待機時間を持つドライブとして定義された統計外れ値を探します。

   > [!IMPORTANT]
   > 簡潔にするために、このスクリプトは低レベルの分散に対するセーフガードを実装しておらず、部分的な欠損データを処理せず、モデルやファームウェアなどを区別しません。適切な略しを使用してください。ハードディスクを交換するかどうかを判断するために、このスクリプトだけに依存しないでください。 ここでは、教育目的でのみ提供されています。

### <a name="screenshot"></a>Screenshot

次のスクリーンショットには、外れ値がないことがわかります。

![PowerShell のスクリーンショット](media/performance-history/Show-LatencyOutlierHDD.png)

### <a name="how-it-works"></a>しくみ

まず、が一貫していることを確認して、アイドル状態またはほぼアイドル状態のドライブを除外し `PhysicalDisk.Iops.Total` `-Gt 1` ます。 アクティブな HDD ごとに、 `LastHour` 10 秒間隔で360測定で構成された時間帯をにパイプ処理して、 `Measure-Object -Average` 過去1時間の平均待機時間を取得します。 これにより、作成が設定されます。

母集団の平均と標準偏差を調べるために、[広く知ら](http://www.mathsisfun.com/data/standard-deviation.html)れている数式を実装して `μ` `σ` います。 すべてのアクティブな HDD について、平均待機時間と母集団平均を比較し、標準偏差で除算します。 生の値は保持されるので、結果は得 `Sort-Object` られますが、整形のヘルパー関数を使用して、表示される内容を確認することができ `Format-Latency` ます ( `Format-StandardDeviation` 省略可能)。

いずれかのドライブが +3 σよりも大きい場合は、 `Write-Host` 赤で点灯します。それ以外の場合は緑になります。

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

パフォーマンス履歴は、*現時点*でも質問に回答できます。 新しい測定値は、10秒ごとにリアルタイムで使用できます。 このサンプルでは、タイムフレームのシリーズを使用して、 `VHD.Iops.Total` `MostRecent` クラスター内のすべてのホスト間で最も多くの記憶域 IOPS を消費している仮想マシン ("noisiest" など) を特定し、アクティビティの読み取り/書き込みの内訳を表示します。

### <a name="screenshot"></a>Screenshot

次のスクリーンショットでは、記憶域アクティビティ別の上位10個の仮想マシンが表示されています。

![PowerShell のスクリーンショット](media/performance-history/Show-TopIopsVMs.png)

### <a name="how-it-works"></a>しくみ

とは異なり `Get-PhysicalDisk` 、 `Get-VM` コマンドレットはクラスターに対応していません。ローカルサーバー上の vm のみが返されます。 すべてのサーバーから並列でクエリを実行するには、の呼び出しをラップ `Invoke-Command (Get-ClusterNode).Name { ... }` します。 すべての VM について、、、およびの各測定値を取得し `VHD.Iops.Total` `VHD.Iops.Read` `VHD.Iops.Write` ます。 パラメーターを指定しないと `-TimeFrame` 、 `MostRecent` それぞれに対して1つのデータポイントが取得されます。

   > [!TIP]
   > これらのシリーズは、すべての VHD/VHDX ファイルに対するこの VM のアクティビティの合計を反映しています。 この例では、パフォーマンス履歴が自動的に集計されています。 VHD/VHDX の内訳を取得するには、VM ではなく、ユーザーをにパイプすることができ `Get-VHD` `Get-ClusterPerf` ます。

すべてのサーバーの結果がとしてまとめられ `$Output` 、次のことができるように `Sort-Object` `Select-Object -First 10` なります。 装飾の結果は、それがどこから来たかを示すプロパティを持つことに注意してください。これは、 `Invoke-Command` `PsComputerName` VM が実行されている場所を知るために印刷できます。

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

このサンプルでは、タイムフレームのシリーズを使用して `NetAdapter.Bandwidth.Total` `LastDay` 、理論的な最大帯域幅の >90% として定義されているネットワーク飽和状態の兆候を探します。 クラスター内のすべてのネットワークアダプターについて、過去1日の監視されている帯域幅の最大使用量が、示されているリンク速度と比較されます。

### <a name="screenshot"></a>Screenshot

次のスクリーンショットでは、1つの*FABRIKAM NX-4 Pro #2*最後の日にピークされていることがわかります。

![PowerShell のスクリーンショット](media/performance-history/Show-NetworkSaturation.png)

### <a name="how-it-works"></a>しくみ

`Invoke-Command`すべてのサーバーに対して上記のトリックを繰り返し、にパイプを実行し `Get-NetAdapter` `Get-ClusterPerf` ます。 その過程で、2つの関連するプロパティ ( `LinkSpeed` "10 Gbps" のような文字列) と、100億のような生の整数を取得します `Speed` 。 は、 `Measure-Object` 過去1日の平均とピークを取得するために使用します (リマインダー: 期間内の各測定値は `LastDay` 5 分を表します)。また、1バイトあたり8ビットずつ乗算され、りんごの比較が実現されます。

   > [!NOTE]
   > Chelsio などの一部のベンダーは、*ネットワークアダプター*のパフォーマンスカウンターにリモートダイレクトメモリアクセス (RDMA) アクティビティを含めているため、シリーズに含まれてい `NetAdapter.Bandwidth.Total` ます。 Mellanox のような他の人は、そうでない場合があります。 ベンダーがない場合は、 `NetAdapter.Bandwidth.RDMA.Total` このスクリプトのバージョンに系列を追加してください。

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

マクロの傾向を確認するために、パフォーマンス履歴は最大1年間保持されます。 このサンプルでは、タイムフレームのシリーズを使用して、ストレージがいっぱいになっ `Volume.Size.Available` `LastYear` た割合を判断し、それがいっぱいになったときに見積もります。

### <a name="screenshot"></a>Screenshot

次のスクリーンショットでは、*バックアップ*ボリュームが1日あたり約 15 GB を追加していることがわかります。

![PowerShell のスクリーンショット](media/performance-history/Show-StorageTrend.png)

この料金が発生すると、別の42日以内に容量に達します。

### <a name="how-it-works"></a>しくみ

この `LastYear` 期間には1日あたり1つのデータポイントがあります。 傾向線に合わせるために必要なポイントは厳密に2つだけですが、実際には、14日など、さらに多くの点が必要になります。 を使用して、 `Select-Object -Last 14` [1, 14] の範囲の*x*の配列 *(x, y)* を設定します。 これらのポイントを使用して、単純な[線形最小二乗アルゴリズム](http://mathworld.wolfram.com/LeastSquaresFitting.html)を実装 `$A` し、 `$B` 最も近い*y = ax + b*の行をパラメーター化します。 この後も、高校にようこそ。

ボリュームのプロパティを `SizeRemaining` 傾向 (傾斜) で割ることによって、 `$A` crudely は、ボリュームがいっぱいになるまで、現在の記憶域の増加率における日数を見積もることができます。 `Format-Bytes`、 `Format-Trend` 、および `Format-Days` ヘルパー関数は、出力を整形します。

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

パフォーマンス履歴はクラスター全体に対して一元的に収集されて保存されるため、ホスト間で Vm が何回移動するかに関係なく、異なるコンピューターのデータを結合する必要はありません。 このサンプルでは、期間のシリーズを使用して、 `VM.Memory.Assigned` `LastMonth` 過去35日間に最大メモリを消費している仮想マシンを特定します。

### <a name="screenshot"></a>Screenshot

次のスクリーンショットでは、過去1か月間のメモリ使用量別の上位10個の仮想マシンが表示されています。

![PowerShell のスクリーンショット](media/performance-history/Show-TopMemoryVMs.png)

### <a name="how-it-works"></a>しくみ

上で紹介した `Invoke-Command` トリックを `Get-VM` すべてのサーバーに対して繰り返します。 を使用し `Measure-Object -Average` て、各 VM の毎月の平均を取得し、次にを使用し `Sort-Object` て `Select-Object -First 10` スコアボードを取得します。 (または、これが*最も必要*なリストかもしれません)。

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

これで終了です。 これらのサンプルを使用すると、作業を開始するのに役立ちます。 パフォーマンスの履歴と強力なスクリプト対応のコマンドレットを使用すると、回答を得る `Get-ClusterPerf` ことができます。また、その答えについては、「」を記憶域スペースダイレクト。 – Windows Server 2019 インフラストラクチャを管理および監視する際の複雑な質問。

## <a name="additional-references"></a>その他のリファレンス

- [Windows PowerShell の概要](https://docs.microsoft.com/powershell/scripting/getting-started/getting-started-with-windows-powershell)
- [記憶域スペースダイレクトの概要](storage-spaces-direct-overview.md)
- [パフォーマンス履歴](performance-history.md)
