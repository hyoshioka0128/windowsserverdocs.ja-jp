---
title: バーチャルハードディスクのパフォーマンス履歴
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: d917c2d75c1e4078438b94e8aa4a6f921019af5a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856165"
---
# <a name="performance-history-for-virtual-hard-disks"></a>バーチャルハードディスクのパフォーマンス履歴

> 適用対象: Windows Server 2019

[記憶域スペースダイレクトのパフォーマンス履歴](performance-history.md)のこのサブトピックでは、仮想ハードディスク (VHD) ファイルについて収集されるパフォーマンス履歴の詳細について説明します。 パフォーマンス履歴は、実行中のクラスター化された仮想マシンに接続されているすべての VHD で利用できます。 パフォーマンス履歴は、VHD 形式と VHDX 形式の両方で使用できますが、共有 VHDX ファイルでは使用できません。

   > [!NOTE]
   > 新しく作成または移動した VHD ファイルの収集が開始されるまでに数分かかる場合があります。

## <a name="series-names-and-units"></a>系列の名前と単位

これらのシリーズは、対象となるすべての仮想ハードディスクについて収集されます。

| 系列                    | Unit             |
|---------------------------|------------------|
| `vhd.iops.read`           | 1秒あたり       |
| `vhd.iops.write`          | 1秒あたり       |
| `vhd.iops.total`          | 1秒あたり       |
| `vhd.throughput.read`     | 1秒あたりのバイト数 |
| `vhd.throughput.write`    | 1秒あたりのバイト数 |
| `vhd.throughput.total`    | 1秒あたりのバイト数 |
| `vhd.latency.average`     | 秒          |
| `vhd.size.current`        | バイト            |
| `vhd.size.maximum`        | バイト            |

## <a name="how-to-interpret"></a>解釈する方法

| 系列                    | 解釈する方法                                                                                                 |
|---------------------------|------------------------------------------------------------------------------------------------------------------|
| `vhd.iops.read`           | バーチャルハードディスクで1秒間に実行された読み取り操作の数。                                         |
| `vhd.iops.write`          | バーチャルハードディスクによって1秒あたりに完了した書き込み操作の数。                                        |
| `vhd.iops.total`          | 仮想ハードディスクによって完了された1秒あたりの読み取りまたは書き込み操作の合計数。                          |
| `vhd.throughput.read`     | 仮想ハードディスクから読み取られたデータの1秒あたりの数。                                                     |
| `vhd.throughput.write`    | 1秒あたりに仮想ハードディスクに書き込まれたデータの量。                                                    |
| `vhd.throughput.total`    | 仮想ハードディスクから読み取った、または1秒あたりに書き込まれたデータの合計量。                                 |
| `vhd.latency.average`     | バーチャルハードディスクに対するすべての操作の平均待機時間。                                              |
| `vhd.size.current`        | 動的に拡張する場合は、仮想ハードディスクの現在のファイルサイズ。 固定されている場合、系列は収集されません。 |
| `vhd.size.maximum`        | 動的に拡張する場合は、仮想ハードディスクの最大サイズ。 固定されている場合、はサイズになります。                  |

## <a name="where-they-come-from"></a>どこから来ているか

`iops.*`、`throughput.*`、および `latency.*` シリーズは、仮想マシンが実行されているサーバー上の `Hyper-V Virtual Storage Device` パフォーマンスカウンターセットから、VHD または VHDX ごとに1つのインスタンスとして収集されます。

| 系列                    | ソースカウンター         |
|---------------------------|------------------------|
| `vhd.iops.read`           | `Read Operations/Sec`  |
| `vhd.iops.write`          | `Write Operations/Sec` |
| `vhd.iops.total`          | *上記の合計*     |
| `vhd.throughput.read`     | `Read Bytes/sec`       |
| `vhd.throughput.write`    | `Write Bytes/sec`      |
| `vhd.throughput.total`    | *上記の合計*     |
| `vhd.latency.average`     | `Latency`              |

   > [!NOTE]
   > カウンターは、サンプリングされるのではなく、間隔全体にわたって測定されます。 たとえば、VHD が9秒間非アクティブで、30秒以内に 30 Io が完了した場合、その `vhd.iops.total` は、この10秒間に平均で1秒あたり 3 Io として記録されます。 これにより、パフォーマンス履歴がすべてのアクティビティをキャプチャし、ノイズに対して堅牢になります。

## <a name="usage-in-powershell"></a>PowerShell での使用法

[GET VHD](https://docs.microsoft.com/powershell/module/hyper-v/get-vhd)コマンドレットを使用します。

```PowerShell
Get-VHD <Path> | Get-ClusterPerf
```

仮想マシンからすべての VHD のパスを取得するには、次のようにします。

```PowerShell
(Get-VM <Name>).HardDrives | Select Path
```

   > [!NOTE]
   > Get VHD コマンドレットを使用するには、ファイルパスを指定する必要があります。 列挙体はサポートされていません。

## <a name="see-also"></a>参照

- [記憶域スペースダイレクトのパフォーマンス履歴](performance-history.md)
