---
title: 記憶域スペース ダイレクトのパフォーマンスの履歴
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 09/07/2018
Keywords: Storage Spaces Direct
ms.localizationpriority: medium
ms.openlocfilehash: 828a3265c9770bab0158067c4f856866d03e3d42
ms.sourcegitcommit: d31e266130b3b082372f7af4024e6089cb347d74
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "4239259"
---
# 記憶域スペース ダイレクトのパフォーマンスの履歴

> 適用対象: Windows Server 2019

パフォーマンスの履歴は、ホスト サーバー、ドライブ、ボリューム、仮想マシンをまたがる履歴コンピューティング、メモリ、ネットワーク、および記憶域の測定値を[記憶域スペース ダイレクト](storage-spaces-direct-overview.md)管理者簡単にアクセスを提供する新しい機能です。 パフォーマンスの履歴が自動的に収集され、最大 1 年間のクラスターに保存されています。

   > [!IMPORTANT]
   > この機能は、Windows Server 2019 の新機能です。 Windows Server 2016 で利用可能ではありません。

## はじめに

記憶域スペース ダイレクトでは、Windows Server 2019 の既定では、パフォーマンスの履歴が収集されます。 インストール、構成、または何かを開始する必要はありません。 インターネット接続が必要ないと、System Center は必要ありません外部データベースが必須ではありません。

クラスターのパフォーマンスの履歴を視覚的に確認するには、 [Windows Admin Center](../../manage/windows-admin-center/understand/windows-admin-center.md)を使用します。

![Windows Admin Center でパフォーマンスの履歴](media/performance-history/perf-history-in-wac.png)

クエリを処理をプログラムでは、新しい使用`Get-ClusterPerf`コマンドレットします。 [PowerShell の使用状況](#usage-in-powershell)を参照してください。

## 収集されるもの

7 種類のオブジェクトのパフォーマンスの履歴が収集されます。

![オブジェクトの種類](media/performance-history/types-of-object.png)

各オブジェクトの種類が多くシリーズ: たとえば、`ClusterNode.Cpu.Usage`サーバーごとに収集します。

各オブジェクトの種類について何収集され、それらを解釈する方法の詳細については、これらのサブ トピックを参照してください。

| オブジェクト             | シリーズ                                                                               |
|--------------------|--------------------------------------------------------------------------------------|
| ドライブ             | [ドライブの内容が収集されます。](performance-history-for-drives.md)                     |
| ネットワーク アダプター   | [ネットワーク アダプターの収集がどのような](performance-history-for-network-adapters.md) |
| サーバー            | [どのようなサーバーを収集します。](performance-history-for-servers.md)                   |
| 仮想ハード_ディスク | [仮想ハード_ディスクの収集がどのような](performance-history-for-vhds.md)           |
| バーチャル マシン   | [仮想マシン用に収集される内容](performance-history-for-vms.md)              |
| ボリューム            | [どのようなボリュームを収集します。](performance-history-for-volumes.md)                   |
| クラスター           | [クラスターの内容が収集されます。](performance-history-for-clusters.md)                 |

一連の多くがピア オブジェクトを親ウィンドウ全体にわたって集計された: たとえば、`NetAdapter.Bandwidth.Inbound`ネットワーク アダプターごとに個別に収集され、全体的なサーバーにわたって集計されました。同様に`ClusterNode.Cpu.Usage`をクラスター全体にわたって集計されました。などなど。

## 期間

パフォーマンスの履歴は、最大で 1 年間の粒度の減少と共に格納されます。 最新の時間の測定値は 10 秒ごとできます。 その後、インテリジェントにマージされます (平均または合計と、必要に応じて) より多くの時間にまたがる細かくシリーズにします。 直近の日付の測定値を利用できます。 5 分ごと最新の週 15 分などなど。

Windows Admin Center では、右、グラフの上までの期間を選択できます。

![Windows Admin Center での期間](media/performance-history/timeframes-in-honolulu.png)

PowerShell で、使用、`-TimeFrame`パラメーター。

利用可能な期間を以下に示します。

| 期間   | 測定頻度 | 保持 |
|-------------|-----------------------|--------------|
| `LastHour`  | 10 秒ごと         | 1 時間       |
| `LastDay`   | 5 分ごと       | 25 時間     |
| `LastWeek`  | 15 分ごと      | 8 日       |
| `LastMonth` | 1 時間ごと          | 35 日      |
| `LastYear`  | すべての 1 日           | 400 日間     |

## PowerShell の使用状況

使用して、`Get-ClusterPerformanceHistory`コマンドレット PowerShell でクエリとプロセスのパフォーマンスの履歴をします。

```PowerShell
Get-ClusterPerformanceHistory
```

   > [!TIP]
   > **Get ClusterPerf**エイリアスを使用すると、いくつかのキー入力を保存できます。

### 例

過去 1 時間の仮想マシン*MyVM*の CPU 使用率を取得します。

```PowerShell
Get-VM "MyVM" | Get-ClusterPerf -VMSeriesName "VM.Cpu.Usage" -TimeFrame LastHour
```

高度な例については、ピーク時の値を検索、平均を計算、トレンドをプロット、検出、および複数のような特殊なを実行するコードをスターター公開済みの[サンプル スクリプト](performance-history-scripting.md)を参照してください。

### オブジェクトを指定します。

パイプラインによってオブジェクトを指定することができます。 これは、7 種類のオブジェクトで動作します。

| パイプラインからオブジェクトします。 | 例     |
|----------------------|-------------|
| `Get-PhysicalDisk`   | <code>Get-PhysicalDisk -SerialNumber "XYZ456" &#124; Get-ClusterPerf</code>         |
| `Get-NetAdapter`     | <code>Get-NetAdapter "Ethernet" &#124; Get-ClusterPerf</code>                       |
| `Get-ClusterNode`    | <code>Get-ClusterNode "Server123" &#124; Get-ClusterPerf</code>                     |
| `Get-VHD`            | <code>Get-VHD "C:\ClusterStorage\MyVolume\MyVHD.vhdx" &#124; Get-ClusterPerf</code> |
| `Get-VM`             | <code>Get-VM "MyVM" &#124; Get-ClusterPerf</code>                                   |
| `Get-Volume`         | <code>Get-Volume -FriendlyName "MyVolume"  &#124; Get-ClusterPerf</code>            |
| `Get-Cluster`        | <code>Get-Cluster "MyCluster" &#124; Get-ClusterPerf</code>                         |

を指定しない場合は、クラスターの全体的なパフォーマンスの履歴が返されます。

### 一連を指定します。

これらのパラメーターを使用系列を指定できます。


| パラメーター                 | 例                       | リスト                                                                                 |
|---------------------------|-------------------------------|--------------------------------------------------------------------------------------|
| `-PhysicalDiskSeriesName` | `"PhysicalDisk.Iops.Read"`    | [ドライブの内容が収集されます。](performance-history-for-drives.md)                     |
| `-NetAdapterSeriesName`   | `"NetAdapter.Bandwidth.Outbound"` | [ネットワーク アダプターの収集がどのような](performance-history-for-network-adapters.md) |
| `-ClusterNodeSeriesName`  | `"ClusterNode.Cpu.Usage"`     | [どのようなサーバーを収集します。](performance-history-for-servers.md)                   |
| `-VHDSeriesName`          | `"Vhd.Size.Current"`          | [仮想ハード_ディスクの収集がどのような](performance-history-for-vhds.md)           |
| `-VMSeriesName`           | `"Vm.Memory.Assigned"`        | [仮想マシン用に収集される内容](performance-history-for-vms.md)              |
| `-VolumeSeriesName`       | `"Volume.Latency.Write"`      | [どのようなボリュームを収集します。](performance-history-for-volumes.md)                   |
| `-ClusterSeriesName`      | `"PhysicalDisk.Size.Total"`   | [クラスターの内容が収集されます。](performance-history-for-clusters.md)                 |


   > [!TIP]
   > 利用可能な一連の検出にタブ補完を使用します。

を指定しない場合は、指定したオブジェクトで利用可能なすべての系列が返されます。

### 時間枠を指定します。

履歴の期間を指定する、`-TimeFrame`パラメーター。

   > [!TIP]
   > 利用可能な期間を検出するのにには、タブ補完を使用します。

を指定しない場合、`MostRecent`測定値が返されます。

## 動作の仕組み

### 履歴記憶域のパフォーマンス

記憶域スペース ダイレクトを有効にした後すぐ、約 10 GB ボリュームがという名前`ClusterPerformanceHistory`が作成される拡張可能な記憶域エンジン (Microsoft ジェットとも呼ばれます) のインスタンスがあるプロビジョニングされたとします。 この軽量なデータベースでは、管理者の関与や管理を加えなくてもパフォーマンスの履歴を保存します。

![ボリュームのパフォーマンスの履歴のストレージ](media/performance-history/perf-history-volume.png)

ボリュームでは、記憶域スペースは、対応し、シンプルで双方向のミラーまたはクラスター内のノードの数に応じて、3 方向ミラーリングの回復性のいずれかを使用します。 後ドライブまたはサーバー エラーと同様に、他の記憶域スペース ダイレクトでボリュームを修復します。

ボリュームは、ReFS を使用して、クラスター グループ所有者ノードでのみが表示されるように、クラスター共有ボリューム (CSV) ではありません。 自動的に作成されている以外は何もありませんこのボリュームについて特別な: 表示、参照、サイズを変更または削除 (非推奨)。 問題が生じた場合は、[トラブルシューティング](#troubleshooting)を参照してください。 

### オブジェクトの検出とデータの収集

パフォーマンスの履歴は自動的に任意の場所で、クラスター内の仮想マシンなどの関連するオブジェクトを検出し、パフォーマンス カウンターのストリーミングを開始します。 カウンターにわたって集計された、同期されると、およびデータベースに挿入します。 ストリーミングおり、実行を継続し、最小限のシステムへの影響の最適化されています。

コレクションは高度に利用可能なヘルス サービスによって処理されます: が実行されているノードに障害が発生した場合が再開モーメント、クラスター内の後で別のノード。 パフォーマンスの履歴の中に一時的に可能性がありますが、それが自動的に再開されます。 ヘルス サービスとその所有者ノードを実行して確認できます`Get-ClusterResource Health`PowerShell でします。

### 測定ギャップを処理します。

測定値は[期間](#Timeframes)で説明したようより多くの時間をまたがる細かくシリーズ マージ、不足しているデータの期間は除外されます。 たとえば、サーバーが 30 分間ダウン場合、し、実行されている 50 %cpu 使用率で 30 分間、`ClusterNode.Cpu.Usage`平均時間は 50% (25% ではない) として正しく記録されます。

### 拡張機能とカスタマイズ

パフォーマンスの履歴は、スクリプトの実行に対応します。 PowerShell の使用を自動的にレポートを構築または保管の履歴をエクスポートするアラート、データベースから直接、利用可能な履歴をプル, など、独自の視覚エフェクトをロールバックします。役立つスターター コードについては、公開された[サンプル スクリプト](performance-history-scripting.md)を参照してください。

その他のオブジェクト、期間、または一連の履歴を収集することはできません。

測定の頻度と保存期間では、現在構成できません。

## 開始または停止するパフォーマンスの履歴

### この機能を有効にする方法

しない限りする`Stop-ClusterPerformanceHistory`、パフォーマンスの履歴が既定で有効にします。

それを再度有効にするには、管理者としてこの PowerShell コマンドレットを実行します。

```PowerShell
Start-ClusterPerformanceHistory
```

### この機能を無効にする方法

パフォーマンスの履歴の収集を停止するには、管理者としてこの PowerShell コマンドレットを実行します。

```PowerShell
Stop-ClusterPerformanceHistory
```

既存の測定値を削除するのには、使用、`-DeleteHistory`フラグ。

```PowerShell
Stop-ClusterPerformanceHistory -DeleteHistory
```

   > [!TIP]
   > 初期展開中にことを防ぐパフォーマンスの履歴を設定して以降は、`-CollectPerformanceHistory`のパラメーター`Enable-ClusterStorageSpacesDirect`に`$False`します。

## トラブルシューティング

### このコマンドレットは機能しません

「*' Get ClusterPerf' がコマンドレットの名前として認識されないという用語は、*」機能を意味するようなエラー メッセージは、利用可能なまたはインストールすることはありません。 Windows Server Insider Preview ビルド 17692 以降、フェールオーバー クラスタ リングを実行している記憶域スペース ダイレクトをインストールしたことを確認します。

   > [!NOTE]
   > この機能は、Windows Server 2016 で利用可能なまたはそれ以前ではありません。

### 利用可能なデータがないです。 

グラフでは、図「*データがない*」が表示される場合は、トラブルシューティングする方法を以下に示します。

![利用可能なデータがないです。](media/performance-history/no-data-available.png)

1. オブジェクトが新しく追加されたり、作成、するまで待機する (15 分単位) を検出します。

2. ページを更新するか、次のバック グラウンド更新 (最大 30 秒) を待ちます。

3. 特定の特別なオブジェクトは、パフォーマンスの履歴: たとえば、クラスター化されていない、仮想マシン、クラスター共有ボリューム (CSV) ファイル システムを使用していないボリュームから除外されます。 オブジェクトの種類などの[ボリュームのパフォーマンスの履歴](performance-history-for-volumes.md), 細かい印刷用のサブ トピックを確認します。

4. 問題が解決しない場合は、実行して、管理者として PowerShell を開き、`Get-ClusterPerf`コマンドレットします。 このコマンドレットには、トラブルシューティングの一般的な問題を識別するためのロジックが含まれています。 場合など、ClusterPerformanceHistory ボリュームがないと修復手順について説明します。

5. 前の手順で、コマンドは、何も返された場合を実行して (これは、パフォーマンスの履歴を収集) ヘルス サービスを再起動してみてくださいできる`Stop-ClusterResource Health ; Start-ClusterResource Health`PowerShell でします。

## 関連項目

- [記憶域スペース ダイレクトの概要](storage-spaces-direct-overview.md)
