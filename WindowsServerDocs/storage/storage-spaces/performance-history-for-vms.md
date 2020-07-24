---
title: 仮想マシンのパフォーマンス履歴
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6077e72ba36c0ef2d0d34da4768aaf9fa5137fbe
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86955224"
---
# <a name="performance-history-for-virtual-machines"></a>仮想マシンのパフォーマンス履歴

> 適用対象:Windows Server 2019

[記憶域スペースダイレクトのパフォーマンス履歴](performance-history.md)のこのサブトピックでは、仮想マシン (VM) について収集されたパフォーマンス履歴の詳細について説明します。 パフォーマンス履歴は、実行中のクラスター化された VM ごとに使用できます。

   > [!NOTE]
   > 新しく作成または名前が変更された Vm の収集が開始されるまでに数分かかる場合があります。

## <a name="series-names-and-units"></a>系列の名前と単位

これらのシリーズは、対象となるすべての VM について収集されます。

| 系列                            | ユニット             |
|-----------------------------------|------------------|
| `vm.cpu.usage`                    | パーセント          |
| `vm.memory.assigned`              | バイト            |
| `vm.memory.available`             | バイト            |
| `vm.memory.maximum`               | バイト            |
| `vm.memory.minimum`               | バイト            |
| `vm.memory.pressure`              | -                |
| `vm.memory.startup`               | バイト            |
| `vm.memory.total`                 | バイト            |
| `vmnetworkadapter.bandwidth.inbound`  | 1秒あたりのビット数 |
| `vmnetworkadapter.bandwidth.outbound` | 1秒あたりのビット数 |
| `vmnetworkadapter.bandwidth.total`    | 1秒あたりのビット数 |

また、などのすべての仮想ハードディスク (VHD) シリーズ `vhd.iops.total` は、VM に接続されているすべての vhd について集計されます。

## <a name="how-to-interpret"></a>解釈する方法


| 系列                            | 説明                                                                                                  |
|-----------------------------------|--------------------------------------------------------------------------------------------------------------|
| `vm.cpu.usage`                    | バーチャルマシンがホストサーバーのプロセッサを使用している割合。                                   |
| `vm.memory.assigned`              | 仮想マシンに割り当てられているメモリの量。                                                      |
| `vm.memory.available`             | 割り当てられた容量について、使用可能なメモリの量。                                       |
| `vm.memory.maximum`               | 動的メモリを使用する場合は、仮想マシンに割り当てることができる最大メモリ量です。 |
| `vm.memory.minimum`               | 動的メモリを使用する場合は、仮想マシンに割り当てることができるメモリの最小量です。 |
| `vm.memory.pressure`              | 仮想マシンに割り当てられたメモリに対する仮想マシンのメモリの割合。            |
| `vm.memory.startup`               | 仮想マシンを起動するために必要なメモリの量。                                            |
| `vm.memory.total`                 | メモリの合計。 |
| `vmnetworkadapter.bandwidth.inbound`  | 仮想マシンがすべての仮想ネットワークアダプターで受信したデータの比率。                        |
| `vmnetworkadapter.bandwidth.outbound` | 仮想マシンが仮想ネットワークアダプターを介して送信したデータの比率。                            |
| `vmnetworkadapter.bandwidth.total`    | 仮想マシンが仮想ネットワークアダプター全体で受信または送信したデータの合計速度。          |

   > [!NOTE]
   > カウンターは、サンプリングされるのではなく、間隔全体にわたって測定されます。 たとえば、VM が9秒間アイドル状態であるにもかかわらず、ホスト CPU の50% が10秒間に使用されるスパイクである場合、 `vm.cpu.usage` この10秒間隔で平均で5% として記録されます。 これにより、パフォーマンス履歴がすべてのアクティビティをキャプチャし、ノイズに対して堅牢になります。

## <a name="usage-in-powershell"></a>PowerShell での使用法

[GET VM](/powershell/module/hyper-v/get-vm)コマンドレットを使用します。

```PowerShell
Get-VM <Name> | Get-ClusterPerf
```

   > [!NOTE]
   > Get VM コマンドレットは、クラスター全体ではなく、ローカルサーバーまたは指定されたサーバー上のバーチャルマシンのみを返します。

## <a name="additional-references"></a>その他のリファレンス

- [記憶域スペース ダイレクトのパフォーマンス履歴](performance-history.md)
