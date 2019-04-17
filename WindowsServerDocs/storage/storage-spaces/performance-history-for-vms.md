---
title: 仮想マシンのパフォーマンスの履歴
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 09/07/2018
Keywords: Storage Spaces Direct
ms.localizationpriority: medium
ms.openlocfilehash: f8072ab5fc853248f2eedd26019956ec864a891d
ms.sourcegitcommit: d31e266130b3b082372f7af4024e6089cb347d74
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "4239219"
---
# 仮想マシンのパフォーマンスの履歴

> Windows Server Insider Preview の適用対象:

[記憶域スペース ダイレクトのパフォーマンスの履歴](performance-history.md)のサブこのトピックでは、パフォーマンスの履歴が仮想マシン (VM) の収集を詳しく説明します。 すべてを実行しているクラスター化された VM のパフォーマンスの履歴で利用できます。

   > [!NOTE]
   > コレクションの新規作成または名前が変更された Vm を開始するには数分かかる場合があります。

## 一連の名前と単位

対象となるすべての VM に対してこれらの系列が収集されます。

| シリーズ                            | Unit             |
|-----------------------------------|------------------|
| `vm.cpu.usage`                    | %          |
| `vm.memory.assigned`              |  バイト            |
| `vm.memory.available`             |  バイト            |
| `vm.memory.maximum`               |  バイト            |
| `vm.memory.minimum`               |  バイト            |
| `vm.memory.pressure`              | -                |
| `vm.memory.startup`               |  バイト            |
| `vm.memory.total`                 |  バイト            |
| `vmnetworkadapter.bandwidth.inbound`  | 1 秒あたりのビット |
| `vmnetworkadapter.bandwidth.outbound` | 1 秒あたりのビット |
| `vmnetworkadapter.bandwidth.total`    | 1 秒あたりのビット |

さらに、すべての仮想ハード_ディスク (VHD) 系列よう`vhd.iops.total`、VM に接続されているすべての VHD の集計されます。

## 解釈する方法


| シリーズ                            | 説明                                                                                                  |
|-----------------------------------|--------------------------------------------------------------------------------------------------------------|
| `vm.cpu.usage`                    | そのホスト サーバーのプロセッサの仮想マシンの割合が使用されています。                                   |
| `vm.memory.assigned`              | 仮想マシンに割り当てられたメモリの数量。                                                      |
| `vm.memory.available`             | 割り当てられている金額の利用可能なメモリの数量。                                       |
| `vm.memory.maximum`               | 動的メモリを使用する場合は、仮想マシンに割り当てることができるメモリの最大数です。 |
| `vm.memory.minimum`               | 動的メモリを使用する場合は、仮想マシンに割り当てることができるメモリの最小数です。 |
| `vm.memory.pressure`              | 仮想マシンに割り当てられたメモリを仮想マシンによって要求されたメモリの比率です。            |
| `vm.memory.startup`               | 仮想マシンを開始するために必要なメモリの数量。                                            |
| `vm.memory.total`                 | メモリの合計。 |
| `vmnetworkadapter.bandwidth.inbound`  | 仮想マシン間のすべての仮想ネットワーク アダプターで受信するデータの数です。                        |
| `vmnetworkadapter.bandwidth.outbound` | 仮想マシンでのすべての仮想ネットワーク アダプターの間で送信されるデータの数です。                            |
| `vmnetworkadapter.bandwidth.total`    | データの合計レートの受信または仮想マシンでそのすべての仮想ネットワーク アダプターの間で送信します。          |

   > [!NOTE]
   > カウンターは、サンプリングされたいない全体の間隔で測定されます。 たとえば、VM がアイドル状態に 9 秒ですがスパイク 10 秒間、ホストの CPU の 50% を使用する場合、`vm.cpu.usage`この 10 秒間の平均 5% として記録されます。 これにより、パフォーマンスの履歴は、すべてのアクティビティをキャプチャでき、ノイズに堅牢です。

## PowerShell の使用状況

[GET-VM](https://docs.microsoft.com/powershell/module/hyper-v/get-vm)コマンドレットを使います。

```PowerShell
Get-VM <Name> | Get-ClusterPerf
```

   > [!NOTE]
   > GET-VM コマンドレットはのみ、クラスター間ではなく、ローカル (または指定した) のサーバー上の仮想マシンを返します。

## 関連項目

- [記憶域スペース ダイレクトのパフォーマンスの履歴](performance-history.md)
