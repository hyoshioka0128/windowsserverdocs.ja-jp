---
title: ドライブのパフォーマンス履歴
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: a6c6065b8d7963ada5d80844b270fe088eaa6e56
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859455"
---
# <a name="performance-history-for-drives"></a>ドライブのパフォーマンス履歴

> 適用対象: Windows Server 2019

[記憶域スペースダイレクトのパフォーマンス履歴](performance-history.md)のこのサブトピックでは、ドライブ用に収集されたパフォーマンス履歴の詳細について説明します。 パフォーマンス履歴は、バスやメディアの種類に関係なく、クラスター記憶域サブシステムのすべてのドライブで使用できます。 ただし、OS ブートドライブでは使用できません。

   > [!NOTE]
   > ダウンしているサーバーのドライブのパフォーマンス履歴を収集することはできません。 コレクションは、サーバーが復帰すると自動的に再開されます。

## <a name="series-names-and-units"></a>系列の名前と単位

これらのシリーズは、対象となるすべてのドライブについて収集されます。

| 系列                          | Unit             |
|---------------------------------|------------------|
| `physicaldisk.iops.read`        | 1秒あたり       |
| `physicaldisk.iops.write`       | 1秒あたり       |
| `physicaldisk.iops.total`       | 1秒あたり       |
| `physicaldisk.throughput.read`  | 1秒あたりのバイト数 |
| `physicaldisk.throughput.write` | 1秒あたりのバイト数 |
| `physicaldisk.throughput.total` | 1秒あたりのバイト数 |
| `physicaldisk.latency.read`     | 秒          |
| `physicaldisk.latency.write`    | 秒          |
| `physicaldisk.latency.average`  | 秒          |
| `physicaldisk.size.total`       | バイト            |
| `physicaldisk.size.used`        | バイト            |

## <a name="how-to-interpret"></a>解釈する方法

| 系列                          | 解釈する方法                                                            |
|---------------------------------|-----------------------------------------------------------------------------|
| `physicaldisk.iops.read`        | ドライブによって完了した1秒あたりの読み取り操作の数。                |
| `physicaldisk.iops.write`       | ドライブによって完了した1秒あたりの書き込み操作の数。               |
| `physicaldisk.iops.total`       | ドライブによって完了した1秒あたりの読み取りまたは書き込み操作の合計数。 |
| `physicaldisk.throughput.read`  | ドライブから読み取られたデータの1秒あたりの数。                            |
| `physicaldisk.throughput.write` | ドライブに書き込まれたデータの1秒あたりの数。                           |
| `physicaldisk.throughput.total` | ドライブとの間で読み取られた、または1秒あたりに書き込まれたデータの合計量。        |
| `physicaldisk.latency.read`     | ドライブからの読み取り操作の平均待機時間。                          |
| `physicaldisk.latency.write`    | ドライブへの書き込み操作の平均待機時間。                           |
| `physicaldisk.latency.average`  | ドライブとの間のすべての操作の平均待機時間。                     |
| `physicaldisk.size.total`       | ドライブの合計記憶域容量。                                    |
| `physicaldisk.size.used`        | ドライブの使用済み記憶域容量。                                     |

## <a name="where-they-come-from"></a>どこから来ているか

`iops.*`、`throughput.*`、および `latency.*` シリーズは、ドライブが接続されているサーバー上の `Physical Disk` パフォーマンスカウンターセットから収集されます。これは、ドライブごとに1つのインスタンスです。 これらのカウンターは `partmgr.sys` によって測定され、Windows ソフトウェアスタックやネットワークホップの多くは含まれません。 デバイスハードウェアのパフォーマンスの代表的なものです。

| 系列                          | ソースカウンター           |
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
   > カウンターは、サンプリングされるのではなく、間隔全体にわたって測定されます。 たとえば、ドライブが9秒間アイドル状態で、30秒間 30 Io が完了した場合、その `physicaldisk.iops.total` は、この10秒間に平均で1秒あたり 3 Io として記録されます。 これにより、パフォーマンス履歴がすべてのアクティビティをキャプチャし、ノイズに対して堅牢になります。

`size.*` シリーズは、WMI の `MSFT_PhysicalDisk` クラスから収集されます。1つのドライブにつき1つのインスタンスです。

| 系列                          | Source プロパティ        |
|---------------------------------|------------------------|
| `physicaldisk.size.total`       | `Size`                 |
| `physicaldisk.size.used`        | `VirtualDiskFootprint` |

## <a name="usage-in-powershell"></a>PowerShell での使用法

[Get PhysicalDisk](https://docs.microsoft.com/powershell/module/storage/get-physicaldisk)コマンドレットを使用します。

```PowerShell
Get-PhysicalDisk -SerialNumber <SerialNumber> | Get-ClusterPerf
```

## <a name="see-also"></a>参照

- [記憶域スペースダイレクトのパフォーマンス履歴](performance-history.md)
