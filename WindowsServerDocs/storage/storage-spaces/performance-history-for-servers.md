---
title: サーバーのパフォーマンスの履歴
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/0s/2018
Keywords: Storage Spaces Direct
ms.localizationpriority: medium
ms.openlocfilehash: 33fd62376e9769c23fc6b00eefde9a9b95eb4650
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/01/2018
ms.locfileid: "1894251"
---
# <a name="performance-history-for-servers"></a>サーバーのパフォーマンスの履歴

> 対象アプリケーション: Windows Server 内部のプレビュー

[記憶域スペースの直接のパフォーマンス履歴](performance-history.md)のサブこのトピックは、サーバーのパフォーマンスの履歴を収集するために詳しく説明します。 パフォーマンスの履歴はクラスター内のすべてのサーバーで使用できます。

   > [!NOTE]
   > 下にあるサーバーのパフォーマンスの履歴を収集することはできません。 コレクションとサーバーが復帰自動的に再開します。

## <a name="series-names-and-units"></a>系列の名前と単位

対象のすべてのサーバーでは、これらの連続データが収集されます。

| 連続データ                           | Unit    |
|----------------------------------|---------|
| `clusternode.cpu.usage`          | 率 (%) |
| `clusternode.cpu.usage.guest`    | 率 (%) |
| `clusternode.cpu.usage.host`     | 率 (%) |
| `clusternode.memory.total`       |  バイト   |
| `clusternode.memory.available`   |  バイト   |
| `clusternode.memory.usage`       |  バイト   |
| `clusternode.memory.usage.guest` |  バイト   |
| `clusternode.memory.usage.host`  |  バイト   |

さらに、連続データを次のようなドライブ`physicaldisk.size.total`サーバーなどのネットワーク アダプター系列に添付されているすべての有効なドライブに集計されます`networkadapter.bytes.total`サーバーに接続されているすべての条件を満たすネットワーク アダプターに集計されます。

## <a name="how-to-interpret"></a>内容を理解する方法

| 連続データ                           | 内容を理解する方法                                                      |
|----------------------------------|-----------------------------------------------------------------------|
| `clusternode.cpu.usage`          | アイドル状態ではないプロセッサ時間の割合。                        |
| `clusternode.cpu.usage.guest`    | ゲスト (仮想マシン) の要求に使用するプロセッサ時間の割合。 |
| `clusternode.cpu.usage.host`     | ホスト要求に使用するプロセッサ時間の割合。                    |
| `clusternode.memory.total`       | サーバーの物理メモリの合計です。                              |
| `clusternode.memory.available`   | サーバーの使用可能メモリします。                                   |
| `clusternode.memory.usage`       | サーバーの割り当てられたメモリを (利用できません)。                   |
| `clusternode.memory.usage.guest` | ゲスト (仮想マシン) の要求に割り当てられたメモリします。               |
| `clusternode.memory.usage.host`  | 需要のホストに割り当てられたメモリします。                                  |

## <a name="where-they-come-from"></a>どこから取得します。

`cpu.*` HYPER-V が有効になっているかどうかによって、さまざまなパフォーマンス カウンターから連続データを収集します。

HYPER-V] がオンの場合

| 連続データ                           | ソース反対 |
|----------------------------------|----------------|
| `clusternode.cpu.usage`          | `Hyper-V Hypervisor Logical Processor` > `_Total` > `% Total Run Time`      |
| `clusternode.cpu.usage.guest`    | `Hyper-V Hypervisor Virtual Processor` > `_Total` > `% Total Run Time`      |
| `clusternode.cpu.usage.host`     | `Hyper-V Hypervisor Root Virtual Processor` > `_Total` > `% Total Run Time` |

使用して、`% Total Run Time`カウンターにより、パフォーマンスの履歴属性をすべて使用します。

HYPER-V が有効になっていない場合: 場合

| 連続データ                           | ソース反対 |
|----------------------------------|----------------|
| `clusternode.cpu.usage`          | `Processor` > `_Total` > `% Processor Time` |
| `clusternode.cpu.usage.guest`    | *ゼロ* |
| `clusternode.cpu.usage.host`     | *使用率の合計と同じ* |

不完全な同期では、本`clusternode.cpu.usage`は常に`clusternode.cpu.usage.host`と`clusternode.cpu.usage.guest`します。

ただし、同じ`clusternode.cpu.usage.guest`の合計は、常に`vm.cpu.usage`ホスト サーバー上のすべての仮想マシンのします。

`memory.*`系列は、(準備中)。

  > [!NOTE]
  > カウンターがないサンプル、全体の間隔で表されます。 たとえば、サーバーがアイドル状態 9 秒数が 100% の CPU にスパイクに 10 日目の`clusternode.cpu.usage`この 10 秒間隔で平均 10% として記録されます。 これにより、そのパフォーマンス履歴は、すべての作業を収集し、ノイズ堅牢なされます。

## <a name="usage-in-powershell"></a>PowerShell での使用

[Get ClusterNode](https://docs.microsoft.com/powershell/module/failoverclusters/get-clusternode)コマンドレットを使用します。

```PowerShell
Get-ClusterNode <Name> | Get-ClusterPerf
```

## <a name="see-also"></a>関連項目

- [記憶域スペースの直接のパフォーマンス履歴](performance-history.md)
