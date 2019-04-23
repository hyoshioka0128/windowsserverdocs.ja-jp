---
title: 仮想ハード_ディスクのパフォーマンス履歴
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/09/2018
Keywords: 記憶域スペース ダイレクト
ms.localizationpriority: medium
ms.openlocfilehash: 7a0d8d132b6a5ff42cbe78a22c67dd9fec397184
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880403"
---
# <a name="performance-history-for-virtual-hard-disks"></a>仮想ハード_ディスクのパフォーマンス履歴

> 適用先:Windows Server Insider Preview

このサブ トピックの[記憶域スペース ダイレクトのパフォーマンスの履歴](performance-history.md)仮想ハード_ディスク (VHD) ファイルの収集されたパフォーマンスの履歴の詳細について説明します。 パフォーマンスの履歴は、実行中のクラスター化された仮想マシンに接続された VHD をすべて使用できます。 パフォーマンス履歴が、共有 VHDX ファイルの使用可能なことはできません、VHD および VHDX の両方の形式の使用可能です。

   > [!NOTE]
   > コレクションの VHD ファイルを新しく作成または移動を開始するまで数分かかる場合があります。

## <a name="series-names-and-units"></a>系列名とユニット

対象となるすべての仮想ハード ディスクではこれらの系列が収集されます。

| シリーズ                    | Unit             |
|---------------------------|------------------|
| `vhd.iops.read`           | 1 秒あたり       |
| `vhd.iops.write`          | 1 秒あたり       |
| `vhd.iops.total`          | 1 秒あたり       |
| `vhd.throughput.read`     | 1 秒あたりのバイト数 |
| `vhd.throughput.write`    | 1 秒あたりのバイト数 |
| `vhd.throughput.total`    | 1 秒あたりのバイト数 |
| `vhd.latency.average`     | 秒数          |
| `vhd.size.current`        | バイト数            |
| `vhd.size.maximum`        | バイト数            |

## <a name="how-to-interpret"></a>解釈する方法

| シリーズ                    | 解釈する方法                                                                                                 |
|---------------------------|------------------------------------------------------------------------------------------------------------------|
| `vhd.iops.read`           | 仮想ハード_ディスクで完了した 1 秒あたりの読み取り操作の数。                                         |
| `vhd.iops.write`          | 仮想ハード_ディスクで完了した 1 秒あたりの書き込み操作の数。                                        |
| `vhd.iops.total`          | 合計数は、読み取りまたは書き込み、バーチャル ハード_ディスクで完了した 1 秒あたりの操作。                          |
| `vhd.throughput.read`     | 1 秒あたりの仮想ハード ディスクから読み取られたデータの量。                                                     |
| `vhd.throughput.write`    | 1 秒あたりの仮想ハード ディスクに書き込まれたデータの量。                                                    |
| `vhd.throughput.total`    | データの読み取りまたは書き込みを 1 秒あたりの仮想ハード_ディスクの合計数量。                                 |
| `vhd.latency.average`     | 仮想ハード ディスクとの間のすべての操作の平均待機時間。                                              |
| `vhd.size.current`        | 仮想ハード ディスク、動的に拡張される場合の現在のファイルのサイズ。 固定である場合、系列は収集されません。 |
| `vhd.size.maximum`        | 仮想ハード ディスク、動的に拡張される場合の最大サイズ。 固定である場合、サイズです。                  |

## <a name="where-they-come-from"></a>来た

`iops.*`、 `throughput.*`、および`latency.*`シリーズがから収集された、`Hyper-V Virtual Storage Device`仮想マシンが実行中、VHD または VHDX あたり 1 つのインスタンスをサーバーでパフォーマンス カウンターを設定します。

| シリーズ                    | ソースのカウンター         |
|---------------------------|------------------------|
| `vhd.iops.read`           | `Read Operations/Sec`  |
| `vhd.iops.write`          | `Write Operations/Sec` |
| `vhd.iops.total`          | *上記の合計*     |
| `vhd.throughput.read`     | `Read Bytes/sec`       |
| `vhd.throughput.write`    | `Write Bytes/sec`      |
| `vhd.throughput.total`    | *上記の合計*     |
| `vhd.latency.average`     | `Latency`              |

   > [!NOTE]
   > カウンターは、サンプリングされなかった、全体の間隔で測定されます。 たとえば、VHD でアクティブでない場合 9 秒が完了すると 30 IOs 10 日の 1 秒間その`vhd.iops.total`この 10 秒間に平均で 1 秒あたりの 3 つの IOs として記録されます。 これにより、そのパフォーマンス履歴がすべてのアクティビティをキャプチャしがノイズに堅牢になりました。

## <a name="usage-in-powershell"></a>PowerShell での使用法

使用して、 [GET-VHD](https://docs.microsoft.com/powershell/module/hyper-v/get-vhd)コマンドレット。

```PowerShell
Get-VHD <Path> | Get-ClusterPerf
```

仮想マシンからすべての VHD のパスを取得します。

```PowerShell
(Get-VM <Name>).HardDrives | Select Path
```

   > [!NOTE]
   > GET-VHD コマンドレットでは、ファイルのパスを指定する必要があります。 列挙型はサポートしません。

## <a name="see-also"></a>関連項目

- [記憶域スペース ダイレクトのパフォーマンスの履歴](performance-history.md)
