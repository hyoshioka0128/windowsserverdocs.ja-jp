---
title: 記憶域スペース ダイレクトのパフォーマンスの履歴とスクリプトの実行
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 05/15/2018
Keywords: Storage Spaces Direct
ms.localizationpriority: medium
ms.openlocfilehash: cc8ebcaaf7cc39cfadb0ebcec71ed573b436b466
ms.sourcegitcommit: 78ecb64cac789751abf9fd3f55b4a1fcbbe4dad2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2018
ms.locfileid: "8843110"
---
# PowerShell と記憶域スペース ダイレクトのパフォーマンスの履歴とスクリプトの実行

> 17692 以降の Windows Server Insider Preview ビルドに適用されます。

Windows Server 2019 では、[記憶域スペース ダイレクト](storage-spaces-direct-overview.md)を記録で仮想マシン、サーバー、ドライブ、ボリューム、ネットワーク アダプターの広範な[パフォーマンスの履歴](performance-history.md)を格納します。 パフォーマンスの履歴は、すばやくなどの質問に対する*回答を実際*に*生データ*から移動するようにクエリと PowerShell でプロセスを簡単です。

1. 任意の CPU スパイク先週しましたがありますか。
2. 任意の物理ディスクに異常な待機時間が発生しているかどうか。
3. どの Vm が最も IOPS 記憶域を今すぐ消費しているかどうか。
4. 自分のネットワーク帯域幅が飽和状態かどうか。
5. このボリュームが空き領域外で実行される場合
6. 過去の 1 か月では、どの Vm は、最も多くのメモリを使用しますか。

`Get-ClusterPerf`コマンドレットはスクリプトを実行して構築されています。 コマンドレットからの入力を受け取って`Get-VM`または`Get-PhysicalDisk`の関連付けを処理するパイプラインによってパイプその出力のようなユーティリティ コマンドレットに`Sort-Object`、 `Where-Object`、および`Measure-Object`すばやく強力なクエリを作成します。

**このトピックを提供し、上記の 6 つの質問に回答 6 のサンプル スクリプトを説明します。** あるパターン山頂を検索を平均値を検索、プロット トレンドを実行するような特殊な検出、および詳細は、さまざまなデータと期間を適用することができます。 これらは、コピー、拡張、および再利用するための無料スターター コードとして提供されます。

   > [!NOTE]
   > 簡潔にするために、サンプル スクリプトは、考えられる高品質な PowerShell コードのエラー処理などを省略します。 主に、インスピレーションと教育機関向けのもの運用環境ではなくを使用します。

## 例 1: CPU、表示します。

このサンプルを使用して、`ClusterNode.Cpu.Usage`からシリーズ、`LastWeek`サポート期間中、クラスター内の最大値 (「高水マーク」)、すべてのサーバーの最小値、および平均の CPU 使用率を表示します。 これも 25% の単純な分析を数時間 CPU 使用率は 25% を表示するには 50%、過去の 8 日以内に 75% です。

### Screenshot

次のスクリーン ショットでは、*サーバー 02*であること、予期しないスパイク先週します参照してください。

![PowerShell のスクリーン ショット](media/performance-history/Show-CpuMinMaxAvg.png)

### 動作の仕組み

出力`Get-ClusterPerf`組み込みにパイプ`Measure-Object`コマンドレットだけを指定します、`Value`プロパティ。 その`-Maximum`、 `-Minimum`、および`-Average`フラグ、`Measure-Object`により、最初の 3 つの列ほとんどの空きします。 パイプして分析するには、25%、`Where-Object`し、値の数が数`-Gt`(より大きい) 25、50、または 75 します。 美化と最後の手順では`Format-Hours`と`Format-Percent`ヘルパー関数 – 確実に省略可能です。

### スクリプト

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

## 例 2: ファイア、ファイア、待機時間のような特殊な

このサンプルを使用して、`PhysicalDisk.Latency.Average`からシリーズ、`LastHour`統計異常値は、検索するには、サポート期間中は、1 時間ごとの平均待機時間を超える + 3σ でドライブとして定義されている (3 つの標準誤差) 母集団の平均値を超えるします。

   > [!IMPORTANT]
   > 簡潔にするため、このスクリプトは低差異安全対策を実装していない、不足しているデータの一部しか処理しない、モデルまたはファームウェアなどでは区別されません。適切な判断を実行してくださいと、ハード ディスクを交換するかどうかを判断するには、単独では、このスクリプトに頼らないでください。 教育用にのみここで表示されます。

### Screenshot

次のスクリーン ショットで異常値がない参照してください。

![PowerShell のスクリーン ショット](media/performance-history/Show-LatencyOutlierHDD.png)

### 動作の仕組み

最初に、除外するアイドル状態またはほぼアイドル状態のドライブをチェックすることによって`PhysicalDisk.Iops.Total`は一貫して`-Gt 1`します。 パイプのすべてのアクティブな HDD、その`LastHour`サポート期間中、10 個の秒間隔でに 360 測定値の構成`Measure-Object -Average`過去 1 時間経っても、平均待機時間を取得します。 これは、カタログの作成を設定します。

平均を検索する[よく知られていない数式](http://www.mathsisfun.com/data/standard-deviation.html)を実装します`μ`と標準誤差`σ`母集団のします。 すべてのアクティブな HDD、します母集団の平均の平均待機時間を比較し、標準的な部分で除算します。 できるように、未処理の値を維持します`Sort-Object`使用が、結果`Format-Latency`と`Format-StandardDeviation`美化についても説明します: 確実にオプションのヘルパー関数。

すべてのドライブがある場合以上 + 3σ、お`Write-Host`赤色;緑のそうでない場合。

### スクリプト

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

## 例 3: ノイズのある近隣ノードかどうか。 書き込みは正常です。

パフォーマンスの履歴には、次のすぎるな*今すぐ*、に関する質問ことができます。 新しい測定値がリアルタイムで利用可能な 10 秒ごとにします。 この例では、`VHD.Iops.Total`からシリーズ、`MostRecent`最も高く (「もっとも」一部話す可能性のある) を識別するには、サポート期間中、最も記憶域を消費 IOPS、クラスター、およびユーザーのアクティビティの読み取り/書き込みの詳細を表示するすべてのホスト間での仮想マシンします。

### Screenshot

次のスクリーン ショットで、上部 10 仮想マシンをご覧ください記憶域の活動によって。

![PowerShell のスクリーン ショット](media/performance-history/Show-TopIopsVMs.png)

### 動作の仕組み

異なり`Get-PhysicalDisk`、`Get-VM`コマンドレットがクラスターに対応していない – ローカル サーバー上の Vm だけから返されます。 呼び出しをラップします並行してすべてのサーバーからクエリを`Invoke-Command (Get-ClusterNode).Name { ... }`します。 すべての VM の取得、 `VHD.Iops.Total`、 `VHD.Iops.Read`、および`VHD.Iops.Write`測定値。 指定しないことにより、`-TimeFrame`パラメーターを取得します、`MostRecent`ごとに 1 つのデータ ポイントします。

   > [!TIP]
   > これらの系列には、すべての VHD/VHDX ファイルにこの VM のアクティビティの合計が反映されています。 これは、例では、パフォーマンスの履歴が自動的に集計される関数です。 VHD または VHDX の詳細を取得するには、個人パイプでした`Get-VHD`に`Get-ClusterPerf`VM ではなくします。

すべてのサーバーからの結果としてまとめ`$Output`、ことが`Sort-Object`し`Select-Object -First 10`します。 いることを確認`Invoke-Command`で結果を装飾、 `PsComputerName` 、元の VM が実行されているかを理解して印刷できることを示すプロパティ。

### スクリプト

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

## 例 4: よく言わ「25 ギガビットは新しい 10 ギガビット」

この例では、`NetAdapter.Bandwidth.Total`からシリーズ、`LastDay`として定義されているサポート期間中にネットワークの彩度の兆候を探します > 理論上の最大帯域幅の 90% です。 クラスターのすべてのネットワーク アダプターのリンクが記載されている速度を最後の日に最高の観察された帯域幅の使用を比較します。

### Screenshot

次のスクリーン ショットでは、過去 1 日の間で 1 つ*Fabrikam NX 4 Pro 2*がピークすることします参照してください。

![PowerShell のスクリーン ショット](media/performance-history/Show-NetworkSaturation.png)

### 動作の仕組み

繰り返します、`Invoke-Command`を上からショー`Get-NetAdapter`すべてのサーバーとにパイプ文字で`Get-ClusterPerf`します。 沿った方法では、2 つの関連するプロパティを取得します。 その`LinkSpeed`"10 Gbps"とその生のような文字列`Speed`10000000000 などの整数です。 使用して`Measure-Object`最後の日から平均、ピークを取得する (リマインダー: で各測定、`LastDay`期間は 5 分間を表します) 公正の比較を取得するのには、バイトごとに 8 ビットの乗算します。

   > [!NOTE]
   > Chelsio などのいくつかのベンダーに含まれているため、*ネットワーク アダプター*のパフォーマンス カウンターにリモート ダイレクト メモリ アクセス (RDMA) のアクティビティを含める、`NetAdapter.Bandwidth.Total`シリーズします。 、Mellanox、などがあります。 製造元に問い合わせて、追加するだけの場合、`NetAdapter.Bandwidth.RDMA.Total`このスクリプトのバージョンの系列します。

### スクリプト

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

## 例 5: 再び記憶域 trendy!

マクロの傾向を調べるには、最大 1 年間のパフォーマンスの履歴が保持されます。 このサンプルを使用して、`Volume.Size.Available`から一連の`LastYear`完全な場合は、記憶域がいっぱいになるレートと評価を判断するには、サポート期間中です。

### Screenshot

次のスクリーン ショットでは、*バックアップ*ボリュームが 1 日あたり約 15 GB を追加します参照してください。

![PowerShell のスクリーン ショット](media/performance-history/Show-StorageTrend.png)

この速度での容量に達した別 42 日以内にします。

### 動作の仕組み

`LastYear`時間枠が 1 日あたり 1 つのデータ ポイントします。 厳密にのみ必要が 2 つのポイント傾向を示すラインに合わせて、実際にはお勧め 14 日のように、複数の操作を要求するようにします。 使用して`Select-Object -Last 14` *(x, y)* ポイント、 *x* [1, 14] の範囲内の配列を設定します。 これらの点を検索する単純な[線形の最小正方形のアルゴリズム](http://mathworld.wolfram.com/LeastSquaresFitting.html)を実装します`$A`と`$B`最適の行をパラメーター化される*y = ax + b*します。 ようこそ高校をすべてもう一度。

ボリュームの分割`SizeRemaining`傾向によってプロパティ (傾き`$A`) 明ボリュームがいっぱいになるまでの記憶域の増加、現在のレートでする日数を見積もることができます。 `Format-Bytes`、 `Format-Trend`、および`Format-Days`美化する出力のヘルパー関数。

   > [!IMPORTANT]
   > この推定値は、線形的に最新の 14 日単位の測定値のみに基づいてです。 高度な正確な手法が存在します。 適切な判断を実行してくださいと記憶域の展開に投資するかどうかを判断するには、単独では、このスクリプトに頼らないでください。 教育用にのみここで表示されます。

### スクリプト

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

## 例 6: がメモリを消費を実行できますが、非表示にすることはできません。

パフォーマンスの履歴が収集され、for パノラマ方法に関係なく、別のコンピューターからデータを何度もが必要にすることはありませんクラスター全体を一元的に格納されている Vm 間で移動ホスト。 このサンプルを使用して、`VM.Memory.Assigned`からシリーズ、`LastMonth`サポート期間中に、過去 35 日間、最もメモリを消費する仮想マシンを識別します。

### Screenshot

次のスクリーン ショットで、上部 10 仮想マシンをご覧くださいによっては、先月のメモリ使用量。

![PowerShell のスクリーン ショット](media/performance-history/Show-TopMemoryVMs.png)

### 動作の仕組み

繰り返します、`Invoke-Command`簡単な方法には、上で導入された`Get-VM`すべてのサーバーにします。 使用して`Measure-Object -Average`し、すべての VM の月次請求の平均値を取得する`Sort-Object`続く`Select-Object -First 10`、ランキングを取得します。 (または、*最も希望*list? ですね)

### スクリプト

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

以上で作業は終了です。 期待してヘルプを開始するこれらのサンプルがさせましょう。 記憶域スペース ダイレクトのパフォーマンスの履歴と、強力なスクリプトの実行に対応`Get-ClusterPerf`コマンドレット – 質問し、回答する権限を持ちます。 – 複雑な質問を管理し、Windows Server 2019 のインフラストラクチャを監視します。

## 関連項目

- [Windows PowerShell の概要](https://docs.microsoft.com/powershell/scripting/getting-started/getting-started-with-windows-powershell)
- [記憶域スペース ダイレクトの概要](storage-spaces-direct-overview.md)
- [パフォーマンス履歴](performance-history.md)
