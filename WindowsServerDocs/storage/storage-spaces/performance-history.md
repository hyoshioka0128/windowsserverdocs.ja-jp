---
title: 記憶域スペース ダイレクトのパフォーマンス履歴
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: ce984d3a88f46b77773c524e5b75135930e1bb03
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86961794"
---
# <a name="performance-history-for-storage-spaces-direct"></a>記憶域スペース ダイレクトのパフォーマンス履歴

> 適用対象:Windows Server 2019

パフォーマンス履歴は、ホストサーバー、ドライブ、ボリューム、仮想マシンなどの過去のコンピューティング、メモリ、ネットワーク、およびストレージの測定に、[記憶域スペースダイレクト](storage-spaces-direct-overview.md)管理者が簡単にアクセスできるようにする新しい機能です。 パフォーマンス履歴は、最大1年間、自動的に収集され、クラスターに格納されます。

   > [!IMPORTANT]
   > この機能は、Windows Server 2019 で新しく追加された機能です。 Windows Server 2016 では使用できません。

## <a name="get-started"></a>はじめに

パフォーマンス履歴は、Windows Server 2019 の記憶域スペースダイレクトと共に既定で収集されます。 すべてをインストール、構成、または開始する必要はありません。 インターネット接続は必要ありません。 System Center は必要ありません。また、外部データベースは必要ありません。

クラスターのパフォーマンス履歴をグラフィカルに表示するには、 [Windows 管理センター](../../manage/windows-admin-center/overview.md)を使用します。

![Windows 管理センターのパフォーマンス履歴](media/performance-history/perf-history-in-wac.png)

プログラムを使用してクエリを実行し、処理するには、新しいコマンドレットを使用し `Get-ClusterPerf` ます。 「 [PowerShell での使用方法」を](#usage-in-powershell)参照してください。

## <a name="whats-collected"></a>収集される内容

次の7種類のオブジェクトについて、パフォーマンス履歴が収集されます。

![オブジェクトの種類](media/performance-history/types-of-object.png)

各オブジェクトの種類には多くの系列があります。たとえば、 `ClusterNode.Cpu.Usage` 各サーバーのが収集されます。

オブジェクトの種類ごとに収集される情報とその解釈方法の詳細については、次のサブトピックを参照してください。

| Object             | 系列                                                                               |
|--------------------|--------------------------------------------------------------------------------------|
| ドライブ             | [ドライブの収集内容](performance-history-for-drives.md)                     |
| ネットワーク アダプター   | [ネットワークアダプターについて収集される情報](performance-history-for-network-adapters.md) |
| サーバー            | [サーバーについて収集される情報](performance-history-for-servers.md)                   |
| バーチャル ハード ディスク | [バーチャルハードディスクの収集対象](performance-history-for-vhds.md)           |
| 仮想マシン   | [仮想マシンについて収集される情報](performance-history-for-vms.md)              |
| ボリューム            | [ボリュームについて収集される情報](performance-history-for-volumes.md)                   |
| クラスター           | [クラスターについて収集される情報](performance-history-for-clusters.md)                 |

多くの系列はピアオブジェクト間で集計されます。たとえば、 `NetAdapter.Bandwidth.Inbound` はネットワークアダプターごとに個別に収集され、サーバー全体に集計されます。同様に、 `ClusterNode.Cpu.Usage` クラスター全体に集計されます。

## <a name="timeframes"></a>枠内

パフォーマンス履歴は最大1年間保存され、粒度が低下します。 過去1時間に、測定は10秒ごとに使用できます。 その後は、より多くの時間にわたって、より詳細なシリーズに (必要に応じて平均または合計することによって) インテリジェントにマージされます。 最新の日の場合、測定は5分ごとに使用できます。過去1週間、15分ごとなどなど。

Windows 管理センターでは、グラフの上の右上にある期間を選択できます。

![Windows 管理センターの期間](media/performance-history/timeframes-in-honolulu.png)

PowerShell では、パラメーターを使用し `-TimeFrame` ます。

利用可能な期間は次のとおりです。

| 期間   | 測定の頻度 | 保持期間 |
|-------------|-----------------------|--------------|
| `LastHour`  | 10秒ごと         | 1 時間       |
| `LastDay`   | 5 分おき       | 25 時間     |
| `LastWeek`  | 15分ごと      | 8 日       |
| `LastMonth` | 1時間ごと          | 35 日      |
| `LastYear`  | 1日ごと           | 400日     |

## <a name="usage-in-powershell"></a>PowerShell での使用法

`Get-ClusterPerformanceHistory`コマンドレットを使用して、PowerShell でパフォーマンス履歴のクエリと処理を行います。

```PowerShell
Get-ClusterPerformanceHistory
```

   > [!TIP]
   > 一部のキーストロークを保存するには、 **Get ClusterPerf**エイリアスを使用します。

### <a name="example"></a>例

過去1時間の仮想マシン*Myvm*の CPU 使用率を取得します。

```PowerShell
Get-VM "MyVM" | Get-ClusterPerf -VMSeriesName "VM.Cpu.Usage" -TimeFrame LastHour
```

より高度な例については、公開されている[サンプルスクリプト](performance-history-scripting.md)を参照してください。ピーク値の検索、平均の計算、傾向線のプロット、外れ値検出の実行などを行うためのスタートコードが用意されています。

### <a name="specify-the-object"></a>オブジェクトを指定する

パイプラインによって必要なオブジェクトを指定できます。 これは、7種類のオブジェクトで使用できます。

| パイプラインからのオブジェクト | 例     |
|----------------------|-------------|
| `Get-PhysicalDisk`   | <code>Get-PhysicalDisk -SerialNumber "XYZ456" &#124; Get-ClusterPerf</code>         |
| `Get-NetAdapter`     | <code>Get-NetAdapter "Ethernet" &#124; Get-ClusterPerf</code>                       |
| `Get-ClusterNode`    | <code>Get-ClusterNode "Server123" &#124; Get-ClusterPerf</code>                     |
| `Get-VHD`            | <code>Get-VHD "C:\ClusterStorage\MyVolume\MyVHD.vhdx" &#124; Get-ClusterPerf</code> |
| `Get-VM`             | <code>Get-VM "MyVM" &#124; Get-ClusterPerf</code>                                   |
| `Get-Volume`         | <code>Get-Volume -FriendlyName "MyVolume"  &#124; Get-ClusterPerf</code>            |
| `Get-Cluster`        | <code>Get-Cluster "MyCluster" &#124; Get-ClusterPerf</code>                         |

を指定しない場合、クラスター全体のパフォーマンス履歴が返されます。

### <a name="specify-the-series"></a>系列の指定

次のパラメーターを使用して、必要な系列を指定できます。


| パラメーター                 | 例                       | List                                                                                 |
|---------------------------|-------------------------------|--------------------------------------------------------------------------------------|
| `-PhysicalDiskSeriesName` | `"PhysicalDisk.Iops.Read"`    | [ドライブの収集内容](performance-history-for-drives.md)                     |
| `-NetAdapterSeriesName`   | `"NetAdapter.Bandwidth.Outbound"` | [ネットワークアダプターについて収集される情報](performance-history-for-network-adapters.md) |
| `-ClusterNodeSeriesName`  | `"ClusterNode.Cpu.Usage"`     | [サーバーについて収集される情報](performance-history-for-servers.md)                   |
| `-VHDSeriesName`          | `"Vhd.Size.Current"`          | [バーチャルハードディスクの収集対象](performance-history-for-vhds.md)           |
| `-VMSeriesName`           | `"Vm.Memory.Assigned"`        | [仮想マシンについて収集される情報](performance-history-for-vms.md)              |
| `-VolumeSeriesName`       | `"Volume.Latency.Write"`      | [ボリュームについて収集される情報](performance-history-for-volumes.md)                   |
| `-ClusterSeriesName`      | `"PhysicalDisk.Size.Total"`   | [クラスターについて収集される情報](performance-history-for-clusters.md)                 |


   > [!TIP]
   > 使用可能な系列を検出するには、タブ補完を使用します。

を指定しない場合は、指定したオブジェクトで使用可能なすべての系列が返されます。

### <a name="specify-the-timeframe"></a>期間を指定する

パラメーターを使用して、履歴の期間を指定でき `-TimeFrame` ます。

   > [!TIP]
   > 使用可能な期間を検出するには、タブ補完を使用します。

を指定しない場合、 `MostRecent` 測定値が返されます。

## <a name="how-it-works"></a>しくみ

### <a name="performance-history-storage"></a>パフォーマンス履歴の記憶域

記憶域スペースダイレクトが有効になるとすぐに、という名前の約 10 GB ボリュームが `ClusterPerformanceHistory` 作成され、拡張可能な記憶域エンジン (MICROSOFT JET とも呼ばれます) のインスタンスがそこにプロビジョニングされます。 このライトウェイトデータベースには、管理者の関与も管理もせずに、パフォーマンス履歴が格納されます。

![パフォーマンス履歴記憶域のボリューム](media/performance-history/perf-history-volume.png)

ボリュームは記憶域スペースによってバックアップされ、クラスター内のノードの数に応じて、単純な双方向ミラーまたは3方向ミラー回復性のいずれかを使用します。 記憶域スペースダイレクトの他のボリュームと同様に、ドライブまたはサーバーの障害が発生した後に修復されます。

ボリュームは ReFS を使用しますが、クラスターの共有ボリューム (CSV) ではないため、クラスターグループの所有者ノードにのみ表示されます。 自動的に作成されるだけでなく、このボリュームに関して特別なことはありません。これは、表示、参照、サイズ変更、または削除 (推奨されません) です。 問題が発生した場合は、「[トラブルシューティング](#troubleshooting)」を参照してください。

### <a name="object-discovery-and-data-collection"></a>オブジェクト検出とデータ収集

パフォーマンス履歴は、仮想マシンなどの関連するオブジェクトをクラスター内の任意の場所で自動的に検出し、パフォーマンスカウンターのストリーミングを開始します。 カウンターが集計され、同期されて、データベースに挿入されます。 ストリーミングは継続的に実行され、システムへの影響を最小限に抑えるために最適化されています。

コレクションは、高可用性を備えたヘルスサービスによって処理されます。これは、実行されているノードがダウンした場合、クラスター内の別のノードでしばらく後に再開されます。 パフォーマンス履歴が短時間で期限切れになる場合がありますが、自動的に再開されます。 PowerShell でを実行すると、ヘルスサービスとその所有者ノードを確認でき `Get-ClusterResource Health` ます。

### <a name="handling-measurement-gaps"></a>測定ギャップの処理

期間で説明されているよう[に、測定](#timeframes)値をより詳細な系列にマージすると、不足しているデータの期間は除外されます。 たとえば、サーバーが30分間停止し、次の30分間に50% の CPU で実行されている場合、 `ClusterNode.Cpu.Usage` その時間の平均は 50% (25%) として正しく記録されます。

### <a name="extensibility-and-customization"></a>拡張性とカスタマイズ

パフォーマンス履歴はスクリプトに適しています。 PowerShell を使用して、データベースから使用可能な履歴を直接取得し、自動レポートまたはアラートを構築したり、保管のためのエクスポート履歴を作成したり、独自の視覚エフェクトをロールしたりできます。便利なスタートコードについては、公開されている[サンプルスクリプト](performance-history-scripting.md)を参照してください。

追加のオブジェクト、期間、または系列の履歴を収集することはできません。

測定頻度と保有期間は現在構成できません。

## <a name="start-or-stop-performance-history"></a>パフォーマンス履歴の開始または停止

### <a name="how-do-i-enable-this-feature"></a>この機能を有効に操作方法ますか?

`Stop-ClusterPerformanceHistory`パフォーマンス履歴は、既定では有効になっていません。

再度有効にするには、次の PowerShell コマンドレットを管理者として実行します。

```PowerShell
Start-ClusterPerformanceHistory
```

### <a name="how-do-i-disable-this-feature"></a>この機能を無効に操作方法には

パフォーマンス履歴の収集を停止するには、次の PowerShell コマンドレットを管理者として実行します。

```PowerShell
Stop-ClusterPerformanceHistory
```

既存の測定値を削除するには、フラグを使用し `-DeleteHistory` ます。

```PowerShell
Stop-ClusterPerformanceHistory -DeleteHistory
```

   > [!TIP]
   > 初期デプロイ中は、 `-CollectPerformanceHistory` のパラメーターをに設定することによって、パフォーマンス履歴が開始されないようにすることができます `Enable-ClusterStorageSpacesDirect` `$False` 。

## <a name="troubleshooting"></a>トラブルシューティング

### <a name="the-cmdlet-doesnt-work"></a>コマンドレットが機能しない

"" と*いう用語は、コマンドレットの名前として認識されません*"というエラーメッセージが表示されます。これは、機能が使用できないか、インストールされていないことを意味します。 Windows Server Insider Preview ビルド17692以降がインストールされていること、および記憶域スペースダイレクト実行していることを確認します。

   > [!NOTE]
   > この機能は、Windows Server 2016 以前では使用できません。

### <a name="no-data-available"></a>利用できるデータはありません。

図に示すように "*使用できるデータがありません*" と表示されている場合は、トラブルシューティングの方法を次に示します。

![利用できるデータはありません。](media/performance-history/no-data-available.png)

1. オブジェクトが新しく追加または作成された場合は、検出されるまで待機します (最大15分)。

2. ページを最新の情報に更新するか、次のバックグラウンド更新 (最大30秒) 待ちます。

3. 一部の特殊なオブジェクトは、クラスター化されていない仮想マシンや、クラスターの共有ボリューム (CSV) ファイルシステムを使用しないボリュームなど、パフォーマンス履歴から除外されます。 詳細については、「[ボリュームのパフォーマンス履歴](performance-history-for-volumes.md)」など、オブジェクトの種類のサブトピックを確認してください。

4. 問題が引き続き発生する場合は、管理者として PowerShell を開き、コマンドレットを実行し `Get-ClusterPerf` ます。 このコマンドレットには、Clusterパフォーマンス履歴ボリュームが見つからない場合など、一般的な問題を特定するトラブルシューティングロジックが含まれており、修復の手順が示されています。

5. 前の手順のコマンドで何も返されない場合は、PowerShell でを実行して、ヘルスサービス (パフォーマンス履歴を収集する) を再起動することができ `Stop-ClusterResource Health ; Start-ClusterResource Health` ます。

## <a name="additional-references"></a>その他のリファレンス

- [記憶域スペースダイレクトの概要](storage-spaces-direct-overview.md)
