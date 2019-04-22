---
title: 記憶域スペース ダイレクトのパフォーマンスの履歴を使用したスクリプト
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 05/15/2018
Keywords: 記憶域スペース ダイレクト
ms.localizationpriority: medium
ms.openlocfilehash: cc8ebcaaf7cc39cfadb0ebcec71ed573b436b466
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816323"
---
# <a name="scripting-with-powershell-and-storage-spaces-direct-performance-history"></a>PowerShell と記憶域スペース ダイレクトのパフォーマンスの履歴を使用したスクリプト

> 適用先:Windows Server Insider Preview ビルド 17692 以降

Windows Server の 2019 で[記憶域スペース ダイレクト](storage-spaces-direct-overview.md)レコードとストアの広範な[パフォーマンス履歴](performance-history.md)仮想マシン、サーバー、ドライブ、ボリューム、ネットワーク アダプター、および詳細。 すばやく移動するため、パフォーマンス履歴がクエリおよび PowerShell でのプロセスに簡単*生データ*に*の実際の回答*ような質問をします。

1. CPU スパイク過去 1 週間がありますか。
2. 任意の物理ディスクに異常な待機時間が発生しているでしょうか。
3. Vm ストレージの IOPS が最もを今すぐ消費しているでしょうか。
4. マイ ネットワーク帯域幅が飽和状態でしょうか。
5. このボリュームは空き領域の外で実行されると
6. 過去 1 か月間は、Vm は、最も多くのメモリを使用しますか。

`Get-ClusterPerf`コマンドレットはスクリプトを実行して構築されています。 などのコマンドレットからの入力を受け取って`Get-VM`または`Get-PhysicalDisk`などのユーティリティ コマンドレットに、その出力のパイプ処理でくと、関連付けを処理するために、パイプラインによって`Sort-Object`、 `Where-Object`、および`Measure-Object`強力なクエリをすばやく作成します。

**このトピックでは、提供し、上記の 6 つの質問に回答する 6 のサンプル スクリプトについて説明します。** ピーク時の検索、平均値を検索、傾向線のプロット、外れ値を検出、および詳細は、さまざまなデータと期間の間で実行に使用できるパターンはも提供します。 コピー、拡張、および再利用するための無料スターター コードとして提供されます。

   > [!NOTE]
   > 簡潔にするために、サンプル スクリプトは、高品質の PowerShell コードの考えられるエラーの処理などを省略します。 インスピレーションおよび教育機関向けの主なことは想定されて運用環境ではなくを使用します。

## <a name="sample-1-cpu-i-see-you"></a>サンプル 1:CPU、表示します。

このサンプルでは、`ClusterNode.Cpu.Usage`シリーズから、`LastWeek`クラスター内の最大値 ("high watermark")、すべてのサーバーの最小値、および平均の CPU 使用率を表示する期間。 数時間の CPU 使用率が 25% を表示する単純な四分位数の分析もは 50%、過去 8 日間で 75% です。

### <a name="screenshot"></a>Screenshot

表示する次のスクリーン ショット*サーバー-02*予期しない急増を過去 1 週間必要があります。

![PowerShell のスクリーン ショット](media/performance-history/Show-CpuMinMaxAvg.png)

### <a name="how-it-works"></a>方法

出力`Get-ClusterPerf`組み込みに適切にパイプ`Measure-Object`コマンドレットだけ指定します、`Value`プロパティ。 その`-Maximum`、 `-Minimum`、および`-Average`フラグ、`Measure-Object`により最初の 3 つの列は、ほとんどの無料。 四分位数の分析にパイプできます`Where-Object`値の数がカウントと`-Gt`(より大きい) 25、50、または 75 です。 美化の最後の手順は`Format-Hours`と`Format-Percent`確かに省略可能: ヘルパー関数。

### <a name="script"></a>スクリプト

スクリプトを次に示します。

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

## <a name="sample-2-fire-fire-latency-outlier"></a>サンプル 2:火災、火災、外れ値の待機時間

このサンプルでは、`PhysicalDisk.Latency.Average`データ系列を`LastHour`統計の外れ値を検索する期間を 1 時間あたりの平均待機時間を超える + 3σ ドライブとして定義されている (次の 3 つの標準偏差)、母集団の平均値を超える。

   > [!IMPORTANT]
   > 簡潔にするため、このスクリプトは低差異の保護機能を実装していません、欠落している部分のデータを処理しない、モデルやファームウェアなどでは識別しません。適切な判断を練習してくださいとハード ディスクを交換するかどうかを判断するには、単独でこのスクリプトに依存しません。 説明を行うためここで表示されます。

### <a name="screenshot"></a>Screenshot

次のスクリーン ショットでは、外れ値はありません参照してください。

![PowerShell のスクリーン ショット](media/performance-history/Show-LatencyOutlierHDD.png)

### <a name="how-it-works"></a>方法

チェック、アイドル状態またはほぼアイドル状態のドライブを除外する最初に、`PhysicalDisk.Iops.Total`が一貫して`-Gt 1`します。 パイプのアクティブな HDD はすべて、その`LastHour`時間枠、10 秒間隔でに 360 の測定の構成`Measure-Object -Average`を過去 1 時間に、平均待機時間を取得します。 これは、カタログの作成を設定します。

実装して、[広く知られていない式](http://www.mathsisfun.com/data/standard-deviation.html)、平均値を検索する`μ`と標準偏差`σ`母集団の。 すべてのアクティブな HDD、母集団の平均の平均待機時間の比較や標準偏差で除算します。 ように、生の値をおきます`Sort-Object`使用が、結果`Format-Latency`と`Format-StandardDeviation`美化についても説明します – 確かに省略可能なヘルパー関数。

任意のドライブがある場合以上 3σ、+ `Write-Host` red; でない場合は、緑色で。

### <a name="script"></a>スクリプト

スクリプトを次に示します。

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

## <a name="sample-3-noisy-neighbor-thats-write"></a>サンプル 3:迷惑な隣人でしょうか。 書き込みで完了です。

パフォーマンスの履歴に関する質問に回答できる*今*もします。 新しい値はリアルタイムで使用できる、10 秒ごとです。 このサンプルでは、`VHD.Iops.Total`データ系列を`MostRecent`期間が最もビジー (「もっとも」一部たとえば可能性があります) を識別するために、クラスター内のすべてのホスト間でストレージ IOPS を最大限に使用する仮想マシンの読み取り/書き込みの内訳を表示して、アクティビティ。

### <a name="screenshot"></a>Screenshot

次のスクリーン ショットで、上位 10 の仮想マシンを参照して記憶域のアクティビティによって。

![PowerShell のスクリーン ショット](media/performance-history/Show-TopIopsVMs.png)

### <a name="how-it-works"></a>方法

異なり`Get-PhysicalDisk`、`Get-VM`コマンドレットは、クラスターに対応していません: ローカル サーバーでのみ Vm を返します。 呼び出しのラップを並列ですべてのサーバーから照会`Invoke-Command (Get-ClusterNode).Name { ... }`します。 すべての VM の取得、 `VHD.Iops.Total`、 `VHD.Iops.Read`、および`VHD.Iops.Write`測定値。 指定しないことにより、`-TimeFrame`パラメーターを取得、`MostRecent`ごとに 1 つのデータ ポイント。

   > [!TIP]
   > これらの系列には、すべての VHD または VHDX ファイルをこの VM のアクティビティの合計が反映されます。 これがパフォーマンスの履歴は自動的に集約されての例です。 VHD または VHDX の内訳を取得するには、個人をパイプするでした`Get-VHD`に`Get-ClusterPerf`VM の代わりにします。

すべてのサーバーからの結果は一体として`$Output`、ことができる`Sort-Object`し`Select-Object -First 10`します。 注意`Invoke-Command`で結果を装飾、`PsComputerName`どこから来るか、VM が実行されているかを把握することを印刷できるかを示すプロパティ。

### <a name="script"></a>スクリプト

スクリプトを次に示します。

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

## <a name="sample-4-as-they-say-25-gig-is-the-new-10-gig"></a>サンプル 4:よく言われます「25 ギガは新しい 10 ギガ」

このサンプルでは、`NetAdapter.Bandwidth.Total`シリーズから、`LastDay`として定義されているネットワークの飽和の兆候を検索する期間 > 理論上最大帯域幅の 90%。 クラスターのすべてのネットワーク アダプターの規定されたリンクの速度をその日の最高の観測された帯域幅使用率を比較します。

### <a name="screenshot"></a>Screenshot

次のスクリーン ショットでは、1 つ表示*Fabrikam NX 4 Pro 2*最後の日のピークになっています。

![PowerShell のスクリーン ショット](media/performance-history/Show-NetworkSaturation.png)

### <a name="how-it-works"></a>方法

繰り返します、`Invoke-Command`に上記のトリック`Get-NetAdapter`すべてサーバーにパイプで`Get-ClusterPerf`します。 過程で、2 つの関連するプロパティを取得します。 その`LinkSpeed`"10 Gbps"し、その生のような文字列`Speed`10000000000 などの整数。 使用して`Measure-Object`最後の日から平均およびピークを取得する (アラーム: 各測定値で、`LastDay`期間が 5 分を表します) 公正に比較を取得するバイトあたり 8 ビットを掛けるとします。

   > [!NOTE]
   > Chelsio などの一部のベンダーは、リモート ダイレクト メモリ アクセス (RDMA) アクティビティを含める、*ネットワーク アダプター*に含まれているため、パフォーマンス カウンター、`NetAdapter.Bandwidth.Total`シリーズ。 他のユーザー、Mellanox のようなことはできません。 場合は、ベンダーは、追加するだけです、`NetAdapter.Bandwidth.RDMA.Total`シリーズでは、このスクリプトのバージョン。

### <a name="script"></a>スクリプト

スクリプトを次に示します。

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

## <a name="sample-5-make-storage-trendy-again"></a>サンプル 5:記憶域をもう一度でも最先端ください。

マクロの傾向を見て、パフォーマンスの履歴は最長 1 年間保持されます。 このサンプルでは、`Volume.Size.Available`シリーズから、`LastYear`なる完全なストレージがいっぱいになるレートと見積もりを確認する期間。

### <a name="screenshot"></a>Screenshot

次のスクリーン ショットでは、表示、*バックアップ*ボリュームが 1 日あたり約 15 GB を追加します。

![PowerShell のスクリーン ショット](media/performance-history/Show-StorageTrend.png)

この速度でその容量に達した 42 日の間で。

### <a name="how-it-works"></a>方法

`LastYear`期間が 1 日あたり 1 つのデータ ポイント。 厳密にのみ必要傾向線に合わせて 2 つのポイントは、実際にはお勧め詳細は 14 日間のように要求するようにします。 使用して`Select-Object -Last 14`の配列を設定する *(x, y)* 、ポイントの*x* [1, 14] の範囲内です。 これらの点を持つ、簡単な実装[最小二乗法の線形アルゴリズム](http://mathworld.wolfram.com/LeastSquaresFitting.html)を検索する`$A`と`$B`最適な行をパラメーター化する*y = ax+b の a*します。 へようこそ高校をもう一度です。

分割、ボリュームの`SizeRemaining`傾向によりプロパティ (傾き`$A`) により、簡単、ボリュームがいっぱいになるまで記憶域の成長の現在の速度で日の数の見積もり。 `Format-Bytes`、 `Format-Trend`、および`Format-Days`美化する出力のヘルパー関数。

   > [!IMPORTANT]
   > この見積もりは、線形および最新の 14 日単位の測定値のみに基づいてです。 高度で正確な手法があります。 適切な判断を練習してくださいと、ストレージの拡張に投資するかどうかを判断するには、単独でこのスクリプトに依存しません。 説明を行うためここで表示されます。

### <a name="script"></a>スクリプト

スクリプトを次に示します。

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

## <a name="sample-6-memory-hog-you-can-run-but-you-cant-hide"></a>例 6:メモリを消費を実行できますが、非表示にすることはできません。

パフォーマンス履歴が収集され、何度もまとめて方法に関係なく、別のマシンからデータを合成する必要がありますしないクラスター全体を一元的に格納されている Vm ホスト間を移動します。 このサンプルでは、`VM.Memory.Assigned`シリーズから、`LastMonth`過去 35 日間、最もメモリを消費する仮想マシンを特定する期間。

### <a name="screenshot"></a>Screenshot

次のスクリーン ショットで、上位 10 の仮想マシンを参照して、過去 1 か月のメモリ使用量。

![PowerShell のスクリーン ショット](media/performance-history/Show-TopMemoryVMs.png)

### <a name="how-it-works"></a>方法

繰り返します、`Invoke-Command`うまくいきますよには、上で導入された`Get-VM`すべてのサーバーにします。 使用して`Measure-Object -Average`し、すべての VM の月単位の平均値を取得する`Sort-Object`続けて`Select-Object -First 10`ランキングを取得します。 (もしかしたら、*要望の多かった*リスト?)

### <a name="script"></a>スクリプト

スクリプトを次に示します。

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

以上で作業は終了です。 これらのサンプルを啓発し、始めてさいわいです。 記憶域スペース ダイレクトのパフォーマンスの履歴と、強力なスクリプトに適した`Get-ClusterPerf`コマンドレット、– 質問し、回答を! 複雑な質問を管理して、Windows Server 2019 インフラストラクチャを監視します。

## <a name="see-also"></a>関連項目

- [Windows PowerShell の概要](https://docs.microsoft.com/powershell/scripting/getting-started/getting-started-with-windows-powershell)
- [記憶域スペース ダイレクトの概要](storage-spaces-direct-overview.md)
- [パフォーマンス履歴](performance-history.md)
