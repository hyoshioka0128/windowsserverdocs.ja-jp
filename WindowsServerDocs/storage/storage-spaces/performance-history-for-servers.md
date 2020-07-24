---
title: サーバーのパフォーマンス履歴
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 15f6e68f613dea03631d1ce6be53f6cb9d854fc1
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86954104"
---
# <a name="performance-history-for-servers"></a>サーバーのパフォーマンス履歴

> 適用対象:Windows Server 2019

[記憶域スペースダイレクトのパフォーマンス履歴](performance-history.md)のこのサブトピックでは、サーバーに対して収集されたパフォーマンス履歴の詳細について説明します。 パフォーマンス履歴は、クラスター内のすべてのサーバーで使用できます。

   > [!NOTE]
   > 停止しているサーバーのパフォーマンス履歴を収集することはできません。 コレクションは、サーバーが復帰すると自動的に再開されます。

## <a name="series-names-and-units"></a>系列の名前と単位

これらのシリーズは、対象となるすべてのサーバーについて収集されます。

| 系列                           | ユニット    |
|----------------------------------|---------|
| `clusternode.cpu.usage`          | パーセント |
| `clusternode.cpu.usage.guest`    | パーセント |
| `clusternode.cpu.usage.host`     | パーセント |
| `clusternode.memory.total`       | バイト   |
| `clusternode.memory.available`   | バイト   |
| `clusternode.memory.usage`       | バイト   |
| `clusternode.memory.usage.guest` | バイト   |
| `clusternode.memory.usage.host`  | バイト   |

さらに、サーバーに接続されている `physicaldisk.size.total` すべての対象ドライブのドライブシリーズが集計され、などのネットワークアダプターシリーズが、サーバーに接続されているすべての使用可能な `networkadapter.bytes.total` ネットワークアダプターについて集計されます。

## <a name="how-to-interpret"></a>解釈する方法

| 系列                           | 解釈する方法                                                      |
|----------------------------------|-----------------------------------------------------------------------|
| `clusternode.cpu.usage`          | アイドル状態ではないプロセッサ時間の割合。                        |
| `clusternode.cpu.usage.guest`    | ゲスト (仮想マシン) の要求に使用されたプロセッサ時間の割合。 |
| `clusternode.cpu.usage.host`     | ホストの要求に使用されたプロセッサ時間の割合。                    |
| `clusternode.memory.total`       | サーバーの物理メモリの合計。                              |
| `clusternode.memory.available`   | サーバーで使用可能なメモリ。                                   |
| `clusternode.memory.usage`       | サーバーで割り当てられている (使用できない) メモリ。                   |
| `clusternode.memory.usage.guest` | ゲスト (仮想マシン) の要求に割り当てられたメモリ。               |
| `clusternode.memory.usage.host`  | ホストの要求に割り当てられたメモリ。                                  |

## <a name="where-they-come-from"></a>どこから来ているか

シリーズは、 `cpu.*` hyper-v が有効になっているかどうかに応じて、さまざまなパフォーマンスカウンターから収集されます。

Hyper-v が有効になっている場合:

| 系列                           | ソースカウンター |
|----------------------------------|----------------|
| `clusternode.cpu.usage`          | `Hyper-V Hypervisor Logical Processor` > `_Total` > `% Total Run Time`      |
| `clusternode.cpu.usage.guest`    | `Hyper-V Hypervisor Virtual Processor` > `_Total` > `% Total Run Time`      |
| `clusternode.cpu.usage.host`     | `Hyper-V Hypervisor Root Virtual Processor` > `_Total` > `% Total Run Time` |

カウンターを使用すると、 `% Total Run Time` パフォーマンス履歴属性のすべての使用が保証されます。

Hyper-v が有効になっていない場合:

| 系列                           | ソースカウンター |
|----------------------------------|----------------|
| `clusternode.cpu.usage`          | `Processor` > `_Total` > `% Processor Time` |
| `clusternode.cpu.usage.guest`    | *回* |
| `clusternode.cpu.usage.host`     | *合計使用量と同じ* |

不完全同期の場合、 `clusternode.cpu.usage` は常に `clusternode.cpu.usage.host` + `clusternode.cpu.usage.guest` です。

同じ注意をして、 `clusternode.cpu.usage.guest` は常に `vm.cpu.usage` ホストサーバー上のすべての仮想マシンのの合計になります。

`memory.*`シリーズは (近日公開予定) です。

  > [!NOTE]
  > カウンターは、サンプリングされるのではなく、間隔全体にわたって測定されます。 たとえば、サーバーが9秒間アイドル状態で、10秒間に100% の CPU が急増している場合、その `clusternode.cpu.usage` は10秒間隔で平均で10% として記録されます。 これにより、パフォーマンス履歴がすべてのアクティビティをキャプチャし、ノイズに対して堅牢になります。

## <a name="usage-in-powershell"></a>PowerShell での使用法

[Start-clusternode](/powershell/module/failoverclusters/get-clusternode)コマンドレットを使用します。

```PowerShell
Get-ClusterNode <Name> | Get-ClusterPerf
```

## <a name="additional-references"></a>その他のリファレンス

- [記憶域スペース ダイレクトのパフォーマンス履歴](performance-history.md)
