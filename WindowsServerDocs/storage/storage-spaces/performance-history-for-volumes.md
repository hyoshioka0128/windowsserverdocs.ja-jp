---
title: ボリュームのパフォーマンスの履歴
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/09/2018
Keywords: Storage Spaces Direct
ms.localizationpriority: medium
ms.openlocfilehash: fea1d3d67ab96d95b1699e8ac0129dba698477fe
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/01/2018
ms.locfileid: "1589706"
---
# <a name="performance-history-for-volumes"></a>ボリュームのパフォーマンスの履歴

> 対象アプリケーション: Windows Server 内部のプレビュー

[記憶域スペースの直接のパフォーマンス履歴](performance-history.md)のサブこのトピックは、ボリュームのパフォーマンスの履歴を収集するために詳しく説明します。 パフォーマンスの履歴では、各クラスター共有ボリューム (CSV) クラスターで使用することができます。 ただしは利用できません。 OS のボリュームやその他の CSV 以外の記憶域を起動します。

   > [!NOTE]
   > 新しく作成または名前が変更されたボリュームを開始するコレクション、数分かかる場合があります。

## <a name="series-names-and-units"></a>系列の名前と単位

対象のボリュームごとには、これらの連続データが収集されます。

| 連続データ                    | Unit             |
|---------------------------|------------------|
| `volume.iops.read`        | 1 秒間       |
| `volume.iops.write`       | 1 秒間       |
| `volume.iops.total`       | 1 秒間       |
| `volume.throughput.read`  | バイト/秒 |
| `volume.throughput.write` | バイト/秒 |
| `volume.throughput.total` | バイト/秒 |
| `volume.latency.read`     | 秒数          |
| `volume.latency.write`    | 秒数          |
| `volume.latency.average`  | 秒数          |
| `volume.size.total`       |  バイト            |
| `volume.size.available`   |  バイト            |

## <a name="how-to-interpret"></a>内容を理解する方法

| 連続データ                    | 内容を理解する方法                                                              |
|---------------------------|-------------------------------------------------------------------------------|
| `volume.iops.read`        | この音量を完了した 1 秒あたりの読み取り操作の数です。                |
| `volume.iops.write`       | この音量を完了した 1 秒あたりの書き込み処理の数です。               |
| `volume.iops.total`       | 数の合計の読み取りまたは書き込み操作/秒この音量を完了します。 |
| `volume.throughput.read`  | データの量は、この/秒からお読みください。                            |
| `volume.throughput.write` | この 1 秒間に書き込まれたデータの量。                           |
| `volume.throughput.total` | データの読み取り/書き込み/秒この総数です。        |
| `volume.latency.read`     | このボリュームからの読み取り操作の平均待機時間。                          |
| `volume.latency.write`    | このへの書き込み処理の平均待機時間。                           |
| `volume.latency.average`  | このとの間のすべての操作の平均待機時間。                     |
| `volume.size.total`       | ボリュームの合計ストレージ容量。                                     |
| `volume.size.available`   | 音量の利用可能なストレージ容量。                                 |

## <a name="where-they-come-from"></a>どこから取得します。

`iops.*`、`throughput.*`と`latency.*`系列がから収集された、`Cluster CSVFS`パフォーマンス反対セットします。 クラスター内のすべてのサーバーの所有者に関係なく、すべての CSV ボリュームのインスタンスがあります。 ボリュームのパフォーマンスの履歴を記録`MyVolume`の集計、`MyVolume`クラスター内のすべてのサーバー上にあるインスタンスします。

| 連続データ                    | ソース反対         |
|---------------------------|------------------------|
| `volume.iops.read`        | `Reads/sec`            |
| `volume.iops.write`       | `Writes/sec`           |
| `volume.iops.total`       | *上記の合計を計算します。*     |
| `volume.throughput.read`  | `Read bytes/sec`       |
| `volume.throughput.write` | `Write bytes/sec`      |
| `volume.throughput.total` | *上記の合計を計算します。*     |
| `volume.latency.read`     | `Avg. sec/Read`        |
| `volume.latency.write`    | `Avg. sec/Write`       |
| `volume.latency.average`  | *上記の平均値* |

   > [!NOTE]
   > カウンターがないサンプル、全体の間隔で表されます。 たとえば、ボリュームがアイドル状態である場合 9 秒ですが完了すると 30 の IOs 10 日目の`volume.iops.total`この 10 秒間隔で平均/秒の 3 つの IOs として記録されます。 これにより、そのパフォーマンス履歴は、すべての作業を収集し、ノイズ堅牢なされます。

   > [!TIP]
   > これらは、一般的な[VM 機体](https://github.com/Microsoft/diskspd/blob/master/Frameworks/VMFleet/watch-cluster.ps1)ベンチマーク フレームワークで使用されているカウンターと同じです。

`size.*`系列がから収集された、 `MSFT_Volume` WMI では、ボリュームごとに 1 つのインスタンスのクラスします。

| 連続データ                    | Source プロパティ |
|---------------------------|-----------------|
| `volume.size.total`       | `Size`          |
| `volume.size.available`   | `SizeRemaining` |

## <a name="usage-in-powershell"></a>PowerShell での使用

[Get ボリューム](https://docs.microsoft.com/powershell/module/storage/get-volume)コマンドレットを使用します。

```PowerShell
Get-Volume -FriendlyName <FriendlyName> | Get-ClusterPerf
```

## <a name="see-also"></a>関連項目

- [記憶域スペースの直接のパフォーマンス履歴](performance-history.md)
