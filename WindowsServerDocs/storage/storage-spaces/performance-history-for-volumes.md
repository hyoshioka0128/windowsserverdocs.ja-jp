---
title: ボリュームのパフォーマンス履歴
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/09/2018
Keywords: 記憶域スペース ダイレクト
ms.localizationpriority: medium
ms.openlocfilehash: fea1d3d67ab96d95b1699e8ac0129dba698477fe
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882953"
---
# <a name="performance-history-for-volumes"></a>ボリュームのパフォーマンス履歴

> 適用先:Windows Server Insider Preview

このサブ トピックの[記憶域スペース ダイレクトのパフォーマンスの履歴](performance-history.md)ボリューム用に収集されたパフォーマンスの履歴の詳細について説明します。 パフォーマンス履歴をすべてクラスター共有ボリューム (CSV)、クラスターで使用することができます。 ただし、OS の使用がないボリュームやその他の非 CSV 記憶域を起動します。

   > [!NOTE]
   > コレクションの新規作成または名前が変更されたボリュームを開始するまで数分かかる場合があります。

## <a name="series-names-and-units"></a>系列名とユニット

これらの系列が対象となるボリュームごとに収集されます。

| シリーズ                    | Unit             |
|---------------------------|------------------|
| `volume.iops.read`        | 1 秒あたり       |
| `volume.iops.write`       | 1 秒あたり       |
| `volume.iops.total`       | 1 秒あたり       |
| `volume.throughput.read`  | 1 秒あたりのバイト数 |
| `volume.throughput.write` | 1 秒あたりのバイト数 |
| `volume.throughput.total` | 1 秒あたりのバイト数 |
| `volume.latency.read`     | 秒数          |
| `volume.latency.write`    | 秒数          |
| `volume.latency.average`  | 秒数          |
| `volume.size.total`       | バイト数            |
| `volume.size.available`   | バイト数            |

## <a name="how-to-interpret"></a>解釈する方法

| シリーズ                    | 解釈する方法                                                              |
|---------------------------|-------------------------------------------------------------------------------|
| `volume.iops.read`        | このボリュームで完了した 1 秒あたりの読み取り操作の数。                |
| `volume.iops.write`       | このボリュームで完了した 1 秒あたりの書き込み操作の数。               |
| `volume.iops.total`       | 合計数は、読み取りまたは書き込みこのボリュームで完了した 1 秒あたりの操作。 |
| `volume.throughput.read`  | 1 秒間には、このボリュームからの読み取りデータの量。                            |
| `volume.throughput.write` | 1 秒間には、このボリュームに書き込まれたデータの量。                           |
| `volume.throughput.total` | データの読み取りまたは書き込みを 1 秒間には、このボリュームの合計数量。        |
| `volume.latency.read`     | このボリュームからの読み取り操作の平均待機時間。                          |
| `volume.latency.write`    | このボリュームへの書き込み操作の平均待機時間。                           |
| `volume.latency.average`  | このボリュームの間のすべての操作の平均待機時間。                     |
| `volume.size.total`       | ボリュームの記憶域の合計容量。                                     |
| `volume.size.available`   | ボリュームの使用可能記憶域容量。                                 |

## <a name="where-they-come-from"></a>来た

`iops.*`、 `throughput.*`、および`latency.*`シリーズがから収集された、`Cluster CSVFS`パフォーマンス カウンターのセット。 所有権に関わらず、すべての CSV ボリュームのインスタンスが実行されて、クラスター内のすべてのサーバー。 ボリュームのパフォーマンス履歴が記録された`MyVolume`の集計、`MyVolume`クラスター内のすべてのサーバー上のインスタンス。

| シリーズ                    | ソースのカウンター         |
|---------------------------|------------------------|
| `volume.iops.read`        | `Reads/sec`            |
| `volume.iops.write`       | `Writes/sec`           |
| `volume.iops.total`       | *上記の合計*     |
| `volume.throughput.read`  | `Read bytes/sec`       |
| `volume.throughput.write` | `Write bytes/sec`      |
| `volume.throughput.total` | *上記の合計*     |
| `volume.latency.read`     | `Avg. sec/Read`        |
| `volume.latency.write`    | `Avg. sec/Write`       |
| `volume.latency.average`  | *上記の平均* |

   > [!NOTE]
   > カウンターは、サンプリングされなかった、全体の間隔で測定されます。 たとえば、ボリュームがアイドル状態の場合は 9 秒が完了すると 30 IOs 10 日の 2 番目の`volume.iops.total`この 10 秒間に平均で 1 秒あたりの 3 つの IOs として記録されます。 これにより、そのパフォーマンス履歴がすべてのアクティビティをキャプチャしがノイズに堅牢になりました。

   > [!TIP]
   > これらは、人気のあるによって使用される同じカウンター [VM Fleet](https://github.com/Microsoft/diskspd/blob/master/Frameworks/VMFleet/watch-cluster.ps1)ベンチマーク フレームワーク。

`size.*`シリーズがから収集された、 `MSFT_Volume` WMI、ボリュームごとの 1 つのインスタンスのクラス。

| シリーズ                    | Source プロパティ |
|---------------------------|-----------------|
| `volume.size.total`       | `Size`          |
| `volume.size.available`   | `SizeRemaining` |

## <a name="usage-in-powershell"></a>PowerShell での使用法

使用して、 [Get-volume](https://docs.microsoft.com/powershell/module/storage/get-volume)コマンドレット。

```PowerShell
Get-Volume -FriendlyName <FriendlyName> | Get-ClusterPerf
```

## <a name="see-also"></a>関連項目

- [記憶域スペース ダイレクトのパフォーマンスの履歴](performance-history.md)
