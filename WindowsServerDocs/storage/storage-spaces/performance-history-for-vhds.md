---
title: 仮想ハード ディスクのパフォーマンス履歴
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/09/2018
Keywords: Storage Spaces Direct
ms.localizationpriority: medium
ms.openlocfilehash: 7a0d8d132b6a5ff42cbe78a22c67dd9fec397184
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/01/2018
ms.locfileid: "1589723"
---
# <a name="performance-history-for-virtual-hard-disks"></a>仮想ハード ディスクのパフォーマンス履歴

> 対象アプリケーション: Windows Server 内部のプレビュー

[記憶域スペースの直接のパフォーマンス履歴](performance-history.md)のサブこのトピックは、仮想ハード_ディスク (VHD) ファイルのパフォーマンスの履歴を収集するために詳しく説明します。 パフォーマンスの履歴は、実行中、集合仮想マシンに接続されているすべての VHD 利用できます。 パフォーマンスの履歴では利用 VHD と VHDX の両方の形式では、共有 VHDX ファイルに対応することはできません。

   > [!NOTE]
   > コレクション VHD ファイルを新しく作成または移動するまでに数分かかる場合があります。

## <a name="series-names-and-units"></a>系列の名前と単位

すべての対象になる仮想ハード_ディスク上は、これらの連続データが収集されます。

| 連続データ                    | Unit             |
|---------------------------|------------------|
| `vhd.iops.read`           | 1 秒間       |
| `vhd.iops.write`          | 1 秒間       |
| `vhd.iops.total`          | 1 秒間       |
| `vhd.throughput.read`     | バイト/秒 |
| `vhd.throughput.write`    | バイト/秒 |
| `vhd.throughput.total`    | バイト/秒 |
| `vhd.latency.average`     | 秒数          |
| `vhd.size.current`        |  バイト            |
| `vhd.size.maximum`        |  バイト            |

## <a name="how-to-interpret"></a>内容を理解する方法

| 連続データ                    | 内容を理解する方法                                                                                                 |
|---------------------------|------------------------------------------------------------------------------------------------------------------|
| `vhd.iops.read`           | 2 番目の仮想ハード ディスクが完了したあたりの読み取り操作の数です。                                         |
| `vhd.iops.write`          | 仮想ハード ディスクが完了した 1 秒あたりの書き込み処理の数です。                                        |
| `vhd.iops.total`          | 数の合計の読み取りまたは書き込み操作/秒バーチャル ハード ディスクを完了します。                          |
| `vhd.throughput.read`     | データの量は、1 秒間仮想ハード ディスクからお読みください。                                                     |
| `vhd.throughput.write`    | 1 秒間仮想ハード ディスクに書き込むデータの量。                                                    |
| `vhd.throughput.total`    | 総数のデータを 1 秒間仮想ハード ディスクに書き込みます。                                 |
| `vhd.latency.average`     | 仮想ハード_ディスク上のすべての操作の平均待機時間。                                              |
| `vhd.size.current`        | 仮想のハード ディスクを動的に展開する場合の現在のファイル サイズです。 固定] の場合は、定期的なアイテムは収集されません。 |
| `vhd.size.maximum`        | 仮想のハード ディスクを動的に展開する場合の最大サイズ。 固定] の場合のサイズにします。                  |

## <a name="where-they-come-from"></a>どこから取得します。

`iops.*`、`throughput.*`と`latency.*`系列がから収集された、`Hyper-V Virtual Storage Device`実行、VHD または VHDX ごとに 1 つのインスタンスの仮想マシンのあるサーバーのパフォーマンスを設定します。

| 連続データ                    | ソース反対         |
|---------------------------|------------------------|
| `vhd.iops.read`           | `Read Operations/Sec`  |
| `vhd.iops.write`          | `Write Operations/Sec` |
| `vhd.iops.total`          | *上記の合計を計算します。*     |
| `vhd.throughput.read`     | `Read Bytes/sec`       |
| `vhd.throughput.write`    | `Write Bytes/sec`      |
| `vhd.throughput.total`    | *上記の合計を計算します。*     |
| `vhd.latency.average`     | `Latency`              |

   > [!NOTE]
   > カウンターがないサンプル、全体の間隔で表されます。 たとえば、VHD がアクティブな場合 9 秒は 30 IOs で完了 10 の 2 番目は、その`vhd.iops.total`この 10 秒間隔で平均/秒の 3 つの IOs として記録されます。 これにより、そのパフォーマンス履歴は、すべての作業を収集し、ノイズ堅牢なされます。

## <a name="usage-in-powershell"></a>PowerShell での使用

[Get VHD](https://docs.microsoft.com/powershell/module/hyper-v/get-vhd)コマンドレットを使用します。

```PowerShell
Get-VHD <Path> | Get-ClusterPerf
```

仮想マシンからすべて VHD のパスを取得します。

```PowerShell
(Get-VM <Name>).HardDrives | Select Path
```

   > [!NOTE]
   > Get VHD コマンドレットでは、ファイル パスを指定する必要があります。 列挙はサポートしません。

## <a name="see-also"></a>関連項目

- [記憶域スペースの直接のパフォーマンス履歴](performance-history.md)
