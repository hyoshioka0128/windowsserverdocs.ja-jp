---
title: ボリュームのパフォーマンス履歴
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: e8e8b6ce7a6ab676e1fca32f360370180b38eae2
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474649"
---
# <a name="performance-history-for-volumes"></a>ボリュームのパフォーマンス履歴

> 適用対象:Windows Server 2019

[記憶域スペースダイレクトのパフォーマンス履歴](performance-history.md)のこのサブトピックでは、ボリュームに対して収集されたパフォーマンス履歴の詳細について説明します。 パフォーマンス履歴は、クラスター内のすべてのクラスターの共有ボリューム (CSV) で利用できます。 ただし、OS ブートボリュームまたはその他の非 CSV ストレージでは使用できません。

   > [!NOTE]
   > 新しく作成された、または名前が変更されたボリュームの収集が開始されるまでに数分かかる場合があります。

## <a name="series-names-and-units"></a>系列の名前と単位

これらのシリーズは、対象となるすべてのボリュームについて収集されます。

| 系列                    | ユニット             |
|---------------------------|------------------|
| `volume.iops.read`        | 1秒あたり       |
| `volume.iops.write`       | 1秒あたり       |
| `volume.iops.total`       | 1秒あたり       |
| `volume.throughput.read`  | 1秒あたりのバイト数 |
| `volume.throughput.write` | 1秒あたりのバイト数 |
| `volume.throughput.total` | 1秒あたりのバイト数 |
| `volume.latency.read`     | seconds          |
| `volume.latency.write`    | seconds          |
| `volume.latency.average`  | seconds          |
| `volume.size.total`       | バイト            |
| `volume.size.available`   | バイト            |

## <a name="how-to-interpret"></a>解釈する方法

| 系列                    | 解釈する方法                                                              |
|---------------------------|-------------------------------------------------------------------------------|
| `volume.iops.read`        | このボリュームで1秒間に実行された読み取り操作の数。                |
| `volume.iops.write`       | このボリュームで1秒あたりに完了した書き込み操作の数。               |
| `volume.iops.total`       | このボリュームによって完了された1秒あたりの読み取りまたは書き込み操作の合計数。 |
| `volume.throughput.read`  | このボリュームから読み取られたデータの1秒あたりの数。                            |
| `volume.throughput.write` | このボリュームに書き込まれたデータの1秒あたりの数。                           |
| `volume.throughput.total` | このボリュームから読み取られた、または1秒あたりに書き込まれたデータの合計量。        |
| `volume.latency.read`     | このボリュームからの読み取り操作の平均待機時間。                          |
| `volume.latency.write`    | このボリュームへの書き込み操作の平均待機時間。                           |
| `volume.latency.average`  | このボリュームとの間のすべての操作の平均待機時間。                     |
| `volume.size.total`       | ボリュームの合計記憶域容量。                                     |
| `volume.size.available`   | ボリュームの使用可能な記憶域容量。                                 |

## <a name="where-they-come-from"></a>どこから来ているか

`iops.*`、 `throughput.*` 、およびの各 `latency.*` 系列は、 `Cluster CSVFS` パフォーマンスカウンターセットから収集されます。 クラスター内のすべてのサーバーは、所有権に関係なく、すべての CSV ボリュームにインスタンスを持ちます。 ボリュームについて記録されたパフォーマンス履歴 `MyVolume` は、 `MyVolume` クラスター内のすべてのサーバー上のインスタンスの集計です。

| 系列                    | ソースカウンター         |
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
   > カウンターは、サンプリングされるのではなく、間隔全体にわたって測定されます。 たとえば、ボリュームが9秒間アイドル状態で、30秒間 30 Io が完了した場合、 `volume.iops.total` この10秒間に平均で1秒あたり 3 io として記録されます。 これにより、パフォーマンス履歴がすべてのアクティビティをキャプチャし、ノイズに対して堅牢になります。

   > [!TIP]
   > これらは、一般的な[VM](https://github.com/Microsoft/diskspd/blob/master/Frameworks/VMFleet/watch-cluster.ps1)車両ベンチマークフレームワークで使用されるものと同じカウンターです。

シリーズは、 `size.*` WMI のクラスから収集され `MSFT_Volume` ます。ボリュームごとに1つのインスタンスがあります。

| 系列                    | Source プロパティ |
|---------------------------|-----------------|
| `volume.size.total`       | `Size`          |
| `volume.size.available`   | `SizeRemaining` |

## <a name="usage-in-powershell"></a>PowerShell での使用法

[Get Volume](https://docs.microsoft.com/powershell/module/storage/get-volume)コマンドレットを使用します。

```PowerShell
Get-Volume -FriendlyName <FriendlyName> | Get-ClusterPerf
```

## <a name="additional-references"></a>その他のリファレンス

- [記憶域スペース ダイレクトのパフォーマンス履歴](performance-history.md)
