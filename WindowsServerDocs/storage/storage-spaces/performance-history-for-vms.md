---
title: 仮想マシンのパフォーマンス履歴
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 09/07/2018
Keywords: 記憶域スペース ダイレクト
ms.localizationpriority: medium
ms.openlocfilehash: f8072ab5fc853248f2eedd26019956ec864a891d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890873"
---
# <a name="performance-history-for-virtual-machines"></a>仮想マシンのパフォーマンス履歴

> 適用先:Windows Server Insider Preview

このサブ トピックの[記憶域スペース ダイレクトのパフォーマンスの履歴](performance-history.md)仮想マシン (VM) の収集されたパフォーマンスの履歴の詳細について説明します。 すべてを実行するため、クラスター化された VM のパフォーマンスの履歴があります。

   > [!NOTE]
   > コレクションを新しく作成または名前を変更した Vm の開始まで数分かかる場合があります。

## <a name="series-names-and-units"></a>系列名とユニット

すべての対象となる VM のこれらの系列が収集されます。

| シリーズ                            | Unit             |
|-----------------------------------|------------------|
| `vm.cpu.usage`                    | %          |
| `vm.memory.assigned`              | バイト数            |
| `vm.memory.available`             | バイト数            |
| `vm.memory.maximum`               | バイト数            |
| `vm.memory.minimum`               | バイト数            |
| `vm.memory.pressure`              | -                |
| `vm.memory.startup`               | バイト数            |
| `vm.memory.total`                 | バイト数            |
| `vmnetworkadapter.bandwidth.inbound`  | 1 秒あたりのビット数 |
| `vmnetworkadapter.bandwidth.outbound` | 1 秒あたりのビット数 |
| `vmnetworkadapter.bandwidth.total`    | 1 秒あたりのビット数 |

さらに、すべての仮想ハード_ディスク (VHD) 系列など`vhd.iops.total`VM に接続されている VHD ごとに集計されます。

## <a name="how-to-interpret"></a>解釈する方法


| シリーズ                            | 説明                                                                                                  |
|-----------------------------------|--------------------------------------------------------------------------------------------------------------|
| `vm.cpu.usage`                    | 仮想マシンの割合は、そのホスト サーバーのプロセッサの使用されています。                                   |
| `vm.memory.assigned`              | 仮想マシンに割り当てられたメモリの量。                                                      |
| `vm.memory.available`             | 使用可能、割り当てられている量のメモリの数量。                                       |
| `vm.memory.maximum`               | 動的メモリを使用している場合は、仮想マシンに割り当てることができるメモリの最大数量です。 |
| `vm.memory.minimum`               | 動的メモリを使用している場合は、仮想マシンに割り当てることができるメモリの最小数量です。 |
| `vm.memory.pressure`              | 仮想マシンに割り当てられたメモリを仮想マシンで必要なメモリの比率です。            |
| `vm.memory.startup`               | 仮想マシンを起動に必要なメモリの数量。                                            |
| `vm.memory.total`                 | メモリの合計。 |
| `vmnetworkadapter.bandwidth.inbound`  | 仮想マシンでそのすべての仮想ネットワーク アダプター間で受信したデータの比率。                        |
| `vmnetworkadapter.bandwidth.outbound` | 仮想マシンでそのすべての仮想ネットワーク アダプターを介して送信されるデータの比率。                            |
| `vmnetworkadapter.bandwidth.total`    | 送受信のすべての仮想ネットワーク アダプター間で仮想マシンから送信されたデータの合計の割合。          |

   > [!NOTE]
   > カウンターは、サンプリングされなかった、全体の間隔で測定されます。 たとえば、VM がホストの CPU の 50% を使用して、10 日の 2 番目の 9 秒ですが急増のアイドル状態の`vm.cpu.usage`この 10 秒間に平均で 5% として記録されます。 これにより、そのパフォーマンス履歴がすべてのアクティビティをキャプチャしがノイズに堅牢になりました。

## <a name="usage-in-powershell"></a>PowerShell での使用法

使用して、 [GET-VM](https://docs.microsoft.com/powershell/module/hyper-v/get-vm)コマンドレット。

```PowerShell
Get-VM <Name> | Get-ClusterPerf
```

   > [!NOTE]
   > GET-VM コマンドレットはのみ、クラスター全体ではなく、ローカル (または指定された) サーバー上の仮想マシンを返します。

## <a name="see-also"></a>関連項目

- [記憶域スペース ダイレクトのパフォーマンスの履歴](performance-history.md)
