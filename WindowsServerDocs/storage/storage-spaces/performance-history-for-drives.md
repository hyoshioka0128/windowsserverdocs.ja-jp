---
title: ドライブのパフォーマンス履歴
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
Keywords: Storage Spaces Direct
ms.localizationpriority: medium
ms.openlocfilehash: d162275a885dac79e7efe749328ebdca471fcad1
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/01/2018
ms.locfileid: "1589757"
---
# <a name="performance-history-for-drives"></a>ドライブのパフォーマンス履歴

> 対象アプリケーション: Windows Server 内部のプレビュー

[記憶域スペースの直接のパフォーマンス履歴](performance-history.md)のサブこのトピックは、ドライブのパフォーマンスの履歴を収集するために詳しく説明します。 クラスター記憶域サブシステムのバスに関係なく、すべてのドライブに利用可能なパフォーマンスの履歴を使用するか、メディアの種類します。 ただし、OS 起動ドライブに対応はありません。

   > [!NOTE]
   > 下にあるサーバーのドライブにパフォーマンスの履歴を収集することはできません。 コレクションとサーバーが復帰自動的に再開します。

## <a name="series-names-and-units"></a>系列の名前と単位

すべての有効なドライブには、これらの連続データが収集されます。

| 連続データ                          | Unit             |
|---------------------------------|------------------|
| `physicaldisk.iops.read`        | 1 秒間       |
| `physicaldisk.iops.write`       | 1 秒間       |
| `physicaldisk.iops.total`       | 1 秒間       |
| `physicaldisk.throughput.read`  | バイト/秒 |
| `physicaldisk.throughput.write` | バイト/秒 |
| `physicaldisk.throughput.total` | バイト/秒 |
| `physicaldisk.latency.read`     | 秒数          |
| `physicaldisk.latency.write`    | 秒数          |
| `physicaldisk.latency.average`  | 秒数          |
| `physicaldisk.size.total`       |  バイト            |
| `physicaldisk.size.used`        |  バイト            |

## <a name="how-to-interpret"></a>内容を理解する方法

| 連続データ                          | 内容を理解する方法                                                            |
|---------------------------------|-----------------------------------------------------------------------------|
| `physicaldisk.iops.read`        | 2 番目のドライブに完了したあたりの読み取り操作の数です。                |
| `physicaldisk.iops.write`       | 1 秒間のドライブに完了した書き込み処理の数です。               |
| `physicaldisk.iops.total`       | 数の合計の読み取りまたは書き込み操作/秒ドライブを完了します。 |
| `physicaldisk.throughput.read`  | データの量は、1 秒間ドライブからお読みください。                            |
| `physicaldisk.throughput.write` | 1 秒間ドライブに書き込まれたデータの量。                           |
| `physicaldisk.throughput.total` | 読み取り/書き込み/秒ドライブのデータ量の合計。        |
| `physicaldisk.latency.read`     | ドライブからの読み取り操作の平均待機時間。                          |
| `physicaldisk.latency.write`    | ドライブへの書き込み処理の平均待機時間。                           |
| `physicaldisk.latency.average`  | ドライブのすべての操作の平均待機時間。                     |
| `physicaldisk.size.total`       | ドライブの合計ストレージ容量。                                    |
| `physicaldisk.size.used`        | ドライブの使用されているストレージ容量。                                     |

## <a name="where-they-come-from"></a>どこから取得します。

`iops.*`、`throughput.*`と`latency.*`系列がから収集された、`Physical Disk`パフォーマンス ドライブが接続されているサーバーの設定、ドライブごとに 1 つのインスタンスします。 これらのカウンター評価`partmgr.sys`Windows ソフトウェア スタックの量やネットワーク ホップが含まれていません。 ハードウェア デバイスのパフォーマンスの代表者いること。

| 連続データ                          | ソース反対           |
|---------------------------------|--------------------------|
| `physicaldisk.iops.read`        | `Disk Reads/sec`         |
| `physicaldisk.iops.write`       | `Disk Writes/sec`        |
| `physicaldisk.iops.total`       | `Disk Transfers/sec`     |
| `physicaldisk.throughput.read`  | `Disk Read Bytes/sec`    |
| `physicaldisk.throughput.write` | `Disk Write Bytes/sec`   |
| `physicaldisk.throughput.total` | `Disk Bytes/sec`         |
| `physicaldisk.latency.read`     | `Avg. Disk sec/Read`     |
| `physicaldisk.latency.write`    | `Avg. Disk sec/Writes`   |
| `physicaldisk.latency.average`  | `Avg. Disk sec/Transfer` |

   > [!NOTE]
   > カウンターがないサンプル、全体の間隔で表されます。 たとえば、ドライブがアイドル状態の場合は 9 秒ですが 30 IOs で完了 10 の 2 番目は、その`physicaldisk.iops.total`この 10 秒間隔で平均/秒の 3 つの IOs として記録されます。 これにより、そのパフォーマンス履歴は、すべての作業を収集し、ノイズ堅牢なされます。

`size.*`系列がから収集された、 `MSFT_PhysicalDisk` WMI では、ドライブごとに 1 つのインスタンスのクラスします。

| 連続データ                          | Source プロパティ        |
|---------------------------------|------------------------|
| `physicaldisk.size.total`       | `Size`                 |
| `physicaldisk.size.used`        | `VirtualDiskFootprint` |

## <a name="usage-in-powershell"></a>PowerShell での使用

[Get PhysicalDisk](https://docs.microsoft.com/powershell/module/storage/get-physicaldisk)コマンドレットを使用します。

```PowerShell
Get-PhysicalDisk -SerialNumber <SerialNumber> | Get-ClusterPerf
```

## <a name="see-also"></a>関連項目

- [記憶域スペースの直接のパフォーマンス履歴](performance-history.md)
