---
ms.assetid: f15c02d7-1cbd-4eba-a571-0ea34ab93ef4
title: "データ重複除去の実行"
ms.technology: storage-deduplication
ms.prod: windows-server-threshold
ms.topic: article
author: wmgries
manager: klaasl
ms.author: wgries
ms.date: 09/15/2016
ms.openlocfilehash: e2a84799a7478e192ee50723d5c6cb7a3f4efbf9
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="running-data-deduplication"></a>データ重複除去の実行

> 適用対象: Windows Server (半期チャネル)、Windows Server 2016

## <a id="running-dedup-jobs-manually"></a>データ重複除去ジョブの手動実行

次の PowerShell コマンドレットを使用すると、すべてのスケジュールされたデータ重複除去ジョブを手動で実行することができます。
* [`Start-DedupJob`](https://technet.microsoft.com/library/hh848442.aspx): 新しいデータ重複除去ジョブを開始する
* [`Stop-DedupJob`](https://technet.microsoft.com/library/hh848439.aspx): 既に進行中のデータ重複除去ジョブを停止する (キューから削除する)
* [`Get-DedupJob`](https://technet.microsoft.com/library/hh848452.aspx): アクティブのデータ重複除去ジョブおよびキューに置かれたデータ重複除去ジョブをすべて表示する

スケジュール専用の設定を除き、[データ重複除去ジョブのスケジュール時に使用可能な設定](advanced-settings.md#modifying-job-schedules-available-settings)はすべて、ジョブを手動で開始する場合にも使用できます。 たとえば、優先度を高、CPU 使用量およびメモリ使用量を最大に設定して[最適化](understand.md#job-info-optimization)ジョブを開始するには、管理者権限で次の PowerShell コマンドを実行します。

```PowerShell
Start-DedupJob -Type Optimization -Volume <Your-Volume-Here> -Memory 100 -Cores 100 -Priority High
```

## <a id="monitoring-dedup"></a>データ重複除去の監視

### <a id="monitoring-dedup-job-successes"></a>ジョブの成功

データ重複除去では処理後のモデルが使用されることから、[データ重複除去ジョブ](understand.md#job-info)の成功が重要です。 最新のジョブの状態を確認する簡単な方法は、[`Get-DedupStatus`](https://technet.microsoft.com/library/hh848437.aspx) PowerShell コマンドレットを使用することです。 次のフィールドを定期的に確認します。

* [最適化ジョブ](understand.md#job-info-optimization)の場合は、`LastOptimizationResult`(0 = 成功)、`LastOptimizationResultMessage`、および `LastOptimizationTime` (最近である必要があります) を確認します。
* [ガベージ コレクション ジョブ](understand.md#job-info-gc)の場合は、`LastGarbageCollectionResult`(0 = 成功)、`LastGarbageCollectionResultMessage`、および `LastGarbageCollectionTime` (最近である必要があります) を確認します。
* [整合性スクラブ ジョブ](understand.md#job-info-scrubbing)の場合は、`LastScrubbingResult` (0 = 成功)、`LastScrubbingResultMessage`、および `LastScrubbingTime` (最近である必要があります) を確認します。

> [!Note]  
> ジョブの成功と失敗の詳細は、Windows イベント ビューアーの `\Applications and Services Logs\Windows\Deduplication\Operational` に示されます。

### <a id="monitoring-dedup-optimization-rates"></a>最適化率

[最適化ジョブ](understand.md#job-info-optimization)の失敗を示す指標の 1 つは、最適化率が下降傾向であることです。この場合、最適化ジョブが変更の速度 (チャーン) に対応できていない可能性があります。 [`Get-DedupStatus`](https://technet.microsoft.com/library/hh848437.aspx) PowerShell コマンドレットを使用して、最適化率を確認できます。

> [!Important]  
> `Get-DedupStatus` には、最適化率に関連する 2 つのフィールド `OptimizedFilesSavingsRate` および `SavingsRate` があります。 これらの値はどちらも追跡する必要がありますが、それぞれの意味合いは異なります。
- `OptimizedFilesSavingsRate` の対象は、最適化の '内部ポリシー' であるファイルのみです (`space used by optimized files after optimization / logical size of optimized files`).
- `SavingsRate` の対象は、ボリューム全体です (`space used by optimized files after optimization / total logical size of the optimization`)。

## <a id="disabling-dedup"></a>データ重複除去の無効化
データ重複除去を無効にするには、[非最適化ジョブ](understand.md#job-info-unoptimization)を実行します。 ボリュームの最適化を元に戻すには、次のコマンドを実行します。

```PowerShell
Start-DedupJob -Type Unoptimization -Volume <Desired-Volume>
```

> [!Important]  
> 非最適化されたデータを保持するのに十分なボリューム領域がない場合、非最適化ジョブは失敗します。

## <a id="faq"></a>よく寄せられる質問
**System Center Operations Manager 管理パックを使用して、データ重複除去を監視できますか。**  
対応 ファイル サーバーの System Center 管理パックでは、データ重複除去を監視できます。 詳細については、『[Guide for System Center Management Pack for File Server 2012 R2](http://download.microsoft.com/download/6/F/7/6F7A33B9-9383-48ED-9252-23C2C8AD1BDA/MPGuide_FileServer2012R2.doc)』(ファイル サーバー 2012 R2 向け System Center 管理パック ガイド) を参照してください。
