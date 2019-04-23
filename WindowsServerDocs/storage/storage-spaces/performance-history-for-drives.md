---
title: ドライブのパフォーマンス履歴
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
Keywords: 記憶域スペース ダイレクト
ms.localizationpriority: medium
ms.openlocfilehash: d162275a885dac79e7efe749328ebdca471fcad1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879193"
---
# <a name="performance-history-for-drives"></a>ドライブのパフォーマンス履歴

> 適用先:Windows Server Insider Preview

このサブ トピックの[記憶域スペース ダイレクトのパフォーマンスの履歴](performance-history.md)ドライブ用に収集されたパフォーマンスの履歴の詳細について説明します。 パフォーマンス履歴がバスに関係なく、クラスターの記憶域サブシステム内の各ドライブの使用可能なまたはメディアの種類します。 ただし、OS ブート ドライブのご利用いただけません。

   > [!NOTE]
   > 停止しているサーバーのドライブのパフォーマンスの履歴を収集できません。 コレクションは、ときに、サーバーが復帰自動的に再開されます。

## <a name="series-names-and-units"></a>系列名とユニット

これらの系列は、すべての対象となるドライブに収集されます。

| シリーズ                          | Unit             |
|---------------------------------|------------------|
| `physicaldisk.iops.read`        | 1 秒あたり       |
| `physicaldisk.iops.write`       | 1 秒あたり       |
| `physicaldisk.iops.total`       | 1 秒あたり       |
| `physicaldisk.throughput.read`  | 1 秒あたりのバイト数 |
| `physicaldisk.throughput.write` | 1 秒あたりのバイト数 |
| `physicaldisk.throughput.total` | 1 秒あたりのバイト数 |
| `physicaldisk.latency.read`     | 秒数          |
| `physicaldisk.latency.write`    | 秒数          |
| `physicaldisk.latency.average`  | 秒数          |
| `physicaldisk.size.total`       | バイト数            |
| `physicaldisk.size.used`        | バイト数            |

## <a name="how-to-interpret"></a>解釈する方法

| シリーズ                          | 解釈する方法                                                            |
|---------------------------------|-----------------------------------------------------------------------------|
| `physicaldisk.iops.read`        | ドライブによって完了した 1 秒あたりの読み取り操作の数。                |
| `physicaldisk.iops.write`       | ドライブによって完了した 1 秒あたりの書き込み操作の数。               |
| `physicaldisk.iops.total`       | 合計数は、読み取りまたは書き込みドライブによって完了した 1 秒あたりの操作。 |
| `physicaldisk.throughput.read`  | データの量は、1 秒あたりのディスクから読み取る。                            |
| `physicaldisk.throughput.write` | 1 秒あたりのドライブに書き込まれたデータの量。                           |
| `physicaldisk.throughput.total` | データの読み取りまたは書き込みを 1 秒あたりのドライブの合計数量。        |
| `physicaldisk.latency.read`     | ドライブからの読み取り操作の平均待機時間。                          |
| `physicaldisk.latency.write`    | ドライブへの書き込み操作の平均待機時間。                           |
| `physicaldisk.latency.average`  | ドライブとの間のすべての操作の平均待機時間。                     |
| `physicaldisk.size.total`       | ドライブの記憶域の合計容量。                                    |
| `physicaldisk.size.used`        | ドライブの使用されているストレージの容量。                                     |

## <a name="where-they-come-from"></a>来た

`iops.*`、 `throughput.*`、および`latency.*`シリーズがから収集された、`Physical Disk`ドライブが接続されているサーバーで設定するパフォーマンス カウンター、ドライブあたりの 1 つのインスタンス。 これらのカウンターによって測定は`partmgr.sys`Windows ソフトウェア スタックの多くも任意のネットワーク ホップが含まれていません。 デバイス ハードウェアのパフォーマンスの代表です。

| シリーズ                          | ソースのカウンター           |
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
   > カウンターは、サンプリングされなかった、全体の間隔で測定されます。 たとえば、ドライブがアイドル状態の場合は 9 秒が完了すると 30 IOs 10 日の 2 番目の`physicaldisk.iops.total`この 10 秒間に平均で 1 秒あたりの 3 つの IOs として記録されます。 これにより、そのパフォーマンス履歴がすべてのアクティビティをキャプチャしがノイズに堅牢になりました。

`size.*`シリーズがから収集された、 `MSFT_PhysicalDisk` WMI、ドライブあたりの 1 つのインスタンスのクラス。

| シリーズ                          | Source プロパティ        |
|---------------------------------|------------------------|
| `physicaldisk.size.total`       | `Size`                 |
| `physicaldisk.size.used`        | `VirtualDiskFootprint` |

## <a name="usage-in-powershell"></a>PowerShell での使用法

使用して、 [Get-physicaldisk](https://docs.microsoft.com/powershell/module/storage/get-physicaldisk)コマンドレット。

```PowerShell
Get-PhysicalDisk -SerialNumber <SerialNumber> | Get-ClusterPerf
```

## <a name="see-also"></a>関連項目

- [記憶域スペース ダイレクトのパフォーマンスの履歴](performance-history.md)
