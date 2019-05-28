---
title: 記憶域スペース ダイレクトのパフォーマンスの履歴
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 09/07/2018
Keywords: 記憶域スペース ダイレクト
ms.localizationpriority: medium
ms.openlocfilehash: 1916d2d5e4d1fc846bec19826437b200afe36f42
ms.sourcegitcommit: 4ff3d00df3148e4bea08056cea9f1c3b52086e5d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64772215"
---
# <a name="performance-history-for-storage-spaces-direct"></a>記憶域スペース ダイレクトのパフォーマンスの履歴

> 適用対象:Windows Server 2019

パフォーマンス履歴が提供する新しい機能[記憶域スペース ダイレクト](storage-spaces-direct-overview.md)管理者と、ホスト サーバー、ドライブ、ボリューム、仮想マシン間で、コンピューティング、メモリ、ネットワーク、およびストレージの値を履歴に簡単にアクセスします。 パフォーマンス履歴が自動的に収集され、最大 1 年間、クラスターに格納されています。

   > [!IMPORTANT]
   > この機能は、Windows Server 2019 の新機能です。 Windows Server 2016 でご利用いただけません。

## <a name="get-started"></a>作業開始

既定では、Storage Spaces Direct in Windows Server 2019 のパフォーマンスの履歴が収集されます。 インストール、構成、または何も起動する必要はありません。 インターネット接続は必要ありません、System Center は必要ありません、および外部のデータベースは必要ありません。

クラスターのパフォーマンス履歴をグラフィカルに表示するには、次のように使用します[Windows Admin Center](../../manage/windows-admin-center/understand/windows-admin-center.md):。

![Windows Admin Center でのパフォーマンスの履歴](media/performance-history/perf-history-in-wac.png)

使用してクエリをプログラムで処理は、新しい`Get-ClusterPerf`コマンドレット。 参照してください[PowerShell での使用状況](#usage-in-powershell)します。

## <a name="whats-collected"></a>収集される情報

パフォーマンス履歴の 7 種類のオブジェクトが収集されます。

![オブジェクトの種類](media/performance-history/types-of-object.png)

オブジェクトの種類ごとに多くのシリーズ: たとえば、`ClusterNode.Cpu.Usage`サーバーごとに収集されます。

オブジェクトの種類ごとに収集される情報とその解釈方法の詳細については、これらのサブ トピックを参照してください。

| オブジェクト             | シリーズ                                                                               |
|--------------------|--------------------------------------------------------------------------------------|
| ドライブ             | [ドライブの収集される情報](performance-history-for-drives.md)                     |
| ネットワーク アダプター   | [ネットワーク アダプター用に収集される情報](performance-history-for-network-adapters.md) |
| サーバー            | [サーバー用に収集される情報](performance-history-for-servers.md)                   |
| バーチャル ハード ディスク | [仮想ハード_ディスクに対して収集される情報](performance-history-for-vhds.md)           |
| バーチャル マシン   | [仮想マシン用に収集される情報](performance-history-for-vms.md)              |
| Volumes            | [ボリュームに対して収集される情報](performance-history-for-volumes.md)                   |
| クラスター           | [クラスター用に収集される情報](performance-history-for-clusters.md)                 |

多くのシリーズは、ピア オブジェクトを親にわたって集計されます: たとえば、`NetAdapter.Bandwidth.Inbound`はネットワーク アダプターごとに個別に収集され、全体的なサーバーに集計されます同様に`ClusterNode.Cpu.Usage`; クラスター全体に集計がこれに。

## <a name="timeframes"></a>期間

パフォーマンス履歴は、減少の粒度で最大 1 年間格納されます。 最新の時間の測定値は 10 秒ごとです。 その後、適切にマージされます (平均または合計すること、必要に応じてより多くの時間にわたるシリーズの詳細度の低い。 最新の日の単位が使用可能です。 5 分ごと最新の週。 15 分ごとになどなど。

Windows Admin Center では、右、グラフの上までの期間を選択できます。

![Windows Admin Center での期間](media/performance-history/timeframes-in-honolulu.png)

PowerShell を使用して、`-TimeFrame`パラメーター。

使用可能な期間を次に示します。

| タイムフレーム   | 測定の頻度 | 保持されます。 |
|-------------|-----------------------|--------------|
| `LastHour`  | 10 秒ごと         | 1 時間       |
| `LastDay`   | 5 分ごと       | 25 時間     |
| `LastWeek`  | 15 分ごと      | 8 日       |
| `LastMonth` | 1 時間ごと          | 35 日間      |
| `LastYear`  | 1 日ごと           | 400 日間     |

## <a name="usage-in-powershell"></a>PowerShell での使用法

使用して、`Get-ClusterPerformanceHistory`コマンドレット PowerShell でのクエリと処理のパフォーマンス履歴を使用します。

```PowerShell
Get-ClusterPerformanceHistory
```

   > [!TIP]
   > 使用して、 **Get ClusterPerf**エイリアスをいくつかのキー入力を保存します。

### <a name="example"></a>例

仮想マシンの CPU 使用率の取得*MyVM*過去 1 時間。

```PowerShell
Get-VM "MyVM" | Get-ClusterPerf -VMSeriesName "VM.Cpu.Usage" -TimeFrame LastHour
```

高度な例については、参照、公開された[サンプル スクリプト](performance-history-scripting.md)ピーク値を見つける、平均を計算、傾向線のプロット、外れ値を実行し、検出、スタート コードを提供します。

### <a name="specify-the-object"></a>オブジェクトを指定します。

パイプラインによって対象のオブジェクトを指定できます。 これは、7 種類のオブジェクトで動作します。

| パイプラインからオブジェクトします。 | 例     |
|----------------------|-------------|
| `Get-PhysicalDisk`   | <code>Get-PhysicalDisk -SerialNumber "XYZ456" &#124; Get-ClusterPerf</code>         |
| `Get-NetAdapter`     | <code>Get-NetAdapter "Ethernet" &#124; Get-ClusterPerf</code>                       |
| `Get-ClusterNode`    | <code>Get-ClusterNode "Server123" &#124; Get-ClusterPerf</code>                     |
| `Get-VHD`            | <code>Get-VHD "C:\ClusterStorage\MyVolume\MyVHD.vhdx" &#124; Get-ClusterPerf</code> |
| `Get-VM`             | <code>Get-VM "MyVM" &#124; Get-ClusterPerf</code>                                   |
| `Get-Volume`         | <code>Get-Volume -FriendlyName "MyVolume"  &#124; Get-ClusterPerf</code>            |
| `Get-Cluster`        | <code>Get-Cluster "MyCluster" &#124; Get-ClusterPerf</code>                         |

を指定しない場合は、クラスター全体のパフォーマンス履歴が返されます。

### <a name="specify-the-series"></a>系列を指定します。

これらのパラメーターを使用系列を指定できます。


| パラメーター                 | 例                       | 一覧                                                                                 |
|---------------------------|-------------------------------|--------------------------------------------------------------------------------------|
| `-PhysicalDiskSeriesName` | `"PhysicalDisk.Iops.Read"`    | [ドライブの収集される情報](performance-history-for-drives.md)                     |
| `-NetAdapterSeriesName`   | `"NetAdapter.Bandwidth.Outbound"` | [ネットワーク アダプター用に収集される情報](performance-history-for-network-adapters.md) |
| `-ClusterNodeSeriesName`  | `"ClusterNode.Cpu.Usage"`     | [サーバー用に収集される情報](performance-history-for-servers.md)                   |
| `-VHDSeriesName`          | `"Vhd.Size.Current"`          | [仮想ハード_ディスクに対して収集される情報](performance-history-for-vhds.md)           |
| `-VMSeriesName`           | `"Vm.Memory.Assigned"`        | [仮想マシン用に収集される情報](performance-history-for-vms.md)              |
| `-VolumeSeriesName`       | `"Volume.Latency.Write"`      | [ボリュームに対して収集される情報](performance-history-for-volumes.md)                   |
| `-ClusterSeriesName`      | `"PhysicalDisk.Size.Total"`   | [クラスター用に収集される情報](performance-history-for-clusters.md)                 |


   > [!TIP]
   > 使用可能な系列を検出するのにには、タブ補完を使用します。

を指定しない場合は、指定したオブジェクトの使用可能なすべての系列が返されます。

### <a name="specify-the-timeframe"></a>時間枠を指定します。

履歴で希望の時間枠を指定することができます、`-TimeFrame`パラメーター。

   > [!TIP]
   > 使用可能な期間を検出するのにには、タブ補完を使用します。

を指定しない場合、`MostRecent`測定値が返されます。

## <a name="how-it-works"></a>方法

### <a name="performance-history-storage"></a>パフォーマンス履歴ストレージ

という名前を約 10 GB のボリュームの記憶域スペース ダイレクトを有効にした後すぐ`ClusterPerformanceHistory`が作成され、Extensible Storage Engine (Microsoft JET とも呼ばれます) のインスタンスのプロビジョニングがあります。 この軽量のデータベースには、管理者の関与または管理なしのパフォーマンスの履歴が格納されます。

![パフォーマンス履歴の記憶域のボリューム](media/performance-history/perf-history-volume.png)

ボリュームは記憶域スペースでサポートし、シンプルで双方向ミラー、またはクラスター内のノードの数によっては、3 方向ミラー回復性のいずれかを使用します。 ドライブまたはサーバーのエラーと同様に、他の記憶域スペース ダイレクトのボリュームがあると、修復です。

ボリュームは ReFS を使用するが、クラスター グループの所有者ノードでのみが表示されるように、クラスター共有ボリューム (CSV) ではありません。 自動的に作成されるだけでなく何もないこのボリュームに関する特別な: 表示、参照、サイズを変更または削除 (推奨されません)。 問題が発生した場合は、次を参照してください。[トラブルシューティング](#troubleshooting)します。

### <a name="object-discovery-and-data-collection"></a>オブジェクトの検出とデータの収集

パフォーマンス履歴は自動的にクラスター内の任意の場所の仮想マシンなどの関連するオブジェクトを検出し、そのパフォーマンス カウンターのストリーミングを開始します。 カウンターの集計、同期、およびデータベースに挿入していること。 ストリーミングでは、継続的に実行され、最小限のシステムへの影響は最適化されています。

コレクションが、これは高可用性、ヘルス サービスによって処理されます。 後でもう 1 つのノード クラスターでモーメントを再開にはが実行されているノードがダウンした場合。 パフォーマンス履歴を簡単に、失効可能性がありますが、自動的に再開します。 ヘルス サービスとその所有者ノードを実行して参照できる`Get-ClusterResource Health`powershell。

### <a name="handling-measurement-gaps"></a>測定値のギャップを処理します。

」の説明に従って、多くの時間にわたる一連の詳細度の低いに測定値をマージするときに[期間](#timeframes)、欠落しているデータの期間を除外します。 などの場合は、サーバーは、30 分間ダウンが、実行、50% CPU 30 分間、`ClusterNode.Cpu.Usage`平均時間は 50% (25% ではない) として正しく記録されます。

### <a name="extensibility-and-customization"></a>機能拡張とカスタマイズ

パフォーマンス履歴では、スクリプトに適したです。 PowerShell を使用して、プル、使用可能な履歴を自動的にレポートをビルドまたは保管のために履歴をエクスポートするアラート、データベースから直接、独自の視覚エフェクトなどのロールします。パブリッシュされたを参照してください[サンプル スクリプト](performance-history-scripting.md)の便利なスタート コード。

その他のオブジェクト、期間、または一連の履歴を収集することはできません。

測定の頻度と保有期間では、現在構成できません。

## <a name="start-or-stop-performance-history"></a>開始または停止のパフォーマンスの履歴

### <a name="how-do-i-enable-this-feature"></a>この機能を有効にする方法

しない限りする`Stop-ClusterPerformanceHistory`パフォーマンスの履歴が既定で有効にします。

これを再度有効にするには、管理者として次の PowerShell コマンドレットを実行します。

```PowerShell
Start-ClusterPerformanceHistory
```

### <a name="how-do-i-disable-this-feature"></a>この機能を無効にする方法は?

パフォーマンス履歴の収集を停止するには、管理者として次の PowerShell コマンドレットを実行します。

```PowerShell
Stop-ClusterPerformanceHistory
```

既存の測定値を削除するには、使用、`-DeleteHistory`フラグ。

```PowerShell
Stop-ClusterPerformanceHistory -DeleteHistory
```

   > [!TIP]
   > 初期のデプロイ時にパフォーマンスの履歴を防ぐ以降を設定してから、`-CollectPerformanceHistory`パラメーターの`Enable-ClusterStorageSpacesDirect`に`$False`します。

## <a name="troubleshooting"></a>トラブルシューティング

### <a name="the-cmdlet-doesnt-work"></a>このコマンドレットは機能しません

などのエラー メッセージ" *' Get ClusterPerf' という用語は、コマンドレットの名前として認識されません*"機能が利用できないかインストールされていることを意味します。 17692 またはそれ以降の Windows Server Insider プレビュー ビルドが、フェールオーバー クラスタ リング、および実行している記憶域スペース ダイレクトがインストールされたことを確認します。

   > [!NOTE]
   > この機能は、Windows Server 2016 で使用可能なまたはそれ以前ではありません。

### <a name="no-data-available"></a>データがありません。 

グラフが表示されている場合"*データがありません*"のトラブルシューティングを行う方法を次に示します図示。

![データがありません。](media/performance-history/no-data-available.png)

1. オブジェクトは、新しく追加または作成された場合、するまで待機する (最大 15 分) を検出します。

2. ページを更新するか、[次へ] のバック グラウンド更新 (最大 30 秒) を待ちます。

3. 特定の特殊なオブジェクトは、クラスター化されていない仮想マシンとクラスター共有ボリューム (CSV) ファイル システムを使用していないボリュームなどのパフォーマンス履歴から除外されます。 オブジェクトの種類のサブトピック「のような確認[ボリュームのパフォーマンス履歴](performance-history-for-volumes.md)内蔵マイクの。

4. 問題が解決しない場合は、実行管理者として PowerShell を開き、`Get-ClusterPerf`コマンドレット。 コマンドレットには、トラブルシューティングの一般的な問題を識別するためのロジックが含まれています。 場合など、ClusterPerformanceHistory ボリュームが見つからないか、と修復の手順について説明します。

5. 場合は、前の手順のコマンドは、何も返さないを実行して (これはパフォーマンスの履歴を収集します)、正常性サービスを再起動してみてくださいできます`Stop-ClusterResource Health ; Start-ClusterResource Health`powershell。

## <a name="see-also"></a>関連項目

- [記憶域スペース ダイレクトの概要](storage-spaces-direct-overview.md)
