---
title: サーバーのパフォーマンス履歴
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/05/2018
Keywords: 記憶域スペース ダイレクト
ms.localizationpriority: medium
ms.openlocfilehash: bbfc92f7926b93f5f6716514e64672f4aa304c0f
ms.sourcegitcommit: e817a130c2ed9caaddd1def1b2edac0c798a6aa2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2019
ms.locfileid: "74945247"
---
# <a name="performance-history-for-servers"></a>サーバーのパフォーマンス履歴

> 適用対象: Windows Server 2019

[記憶域スペースダイレクトのパフォーマンス履歴](performance-history.md)のこのサブトピックでは、サーバーに対して収集されたパフォーマンス履歴の詳細について説明します。 パフォーマンス履歴は、クラスター内のすべてのサーバーで使用できます。

   > [!NOTE]
   > 停止しているサーバーのパフォーマンス履歴を収集することはできません。 コレクションは、サーバーが復帰すると自動的に再開されます。

## <a name="series-names-and-units"></a>系列の名前と単位

これらのシリーズは、対象となるすべてのサーバーについて収集されます。

| 系列                           | Unit    |
|----------------------------------|---------|
| `clusternode.cpu.usage`          | percent |
| `clusternode.cpu.usage.guest`    | percent |
| `clusternode.cpu.usage.host`     | percent |
| `clusternode.memory.total`       | バイト   |
| `clusternode.memory.available`   | バイト   |
| `clusternode.memory.usage`       | バイト   |
| `clusternode.memory.usage.guest` | バイト   |
| `clusternode.memory.usage.host`  | バイト   |

さらに、`physicaldisk.size.total` などのドライブシリーズは、サーバーに接続されているすべての対象ドライブについて集計され、`networkadapter.bytes.total` などのネットワークアダプターシリーズは、サーバーに接続されているすべての対象ネットワークアダプターについて集計されます。

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

`cpu.*` シリーズは、Hyper-v が有効になっているかどうかに応じて、さまざまなパフォーマンスカウンターから収集されます。

Hyper-v が有効になっている場合:

| 系列                           | ソースカウンター |
|----------------------------------|----------------|
| `clusternode.cpu.usage`          | `Hyper-V Hypervisor Logical Processor` > `_Total` > `% Total Run Time`      |
| `clusternode.cpu.usage.guest`    | `Hyper-V Hypervisor Virtual Processor` > `_Total` > `% Total Run Time`      |
| `clusternode.cpu.usage.host`     | `Hyper-V Hypervisor Root Virtual Processor` > `_Total` > `% Total Run Time` |

`% Total Run Time` カウンターを使用すると、パフォーマンス履歴属性のすべての使用状況が確実になります。

Hyper-v が有効になっていない場合:

| 系列                           | ソースカウンター |
|----------------------------------|----------------|
| `clusternode.cpu.usage`          | `Processor` > `_Total` > `% Processor Time` |
| `clusternode.cpu.usage.guest`    | *zero* |
| `clusternode.cpu.usage.host`     | *合計使用量と同じ* |

不完全同期の場合、`clusternode.cpu.usage` は常にプラス `clusternode.cpu.usage.guest`に `clusternode.cpu.usage.host` ます。

同じ注意をして、`clusternode.cpu.usage.guest` は常に、ホストサーバー上のすべての仮想マシンの `vm.cpu.usage` の合計になります。

`memory.*` シリーズは (近日公開予定) です。

  > [!NOTE]
  > カウンターは、サンプリングされるのではなく、間隔全体にわたって測定されます。 たとえば、サーバーが9秒間アイドル状態で、10秒間に100% の CPU が急増した場合、その `clusternode.cpu.usage` は10秒間隔で平均で10% として記録されます。 これにより、パフォーマンス履歴がすべてのアクティビティをキャプチャし、ノイズに対して堅牢になります。

## <a name="usage-in-powershell"></a>PowerShell での使用法

[Start-clusternode](https://docs.microsoft.com/powershell/module/failoverclusters/get-clusternode)コマンドレットを使用します。

```PowerShell
Get-ClusterNode <Name> | Get-ClusterPerf
```

## <a name="see-also"></a>関連項目

- [記憶域スペースダイレクトのパフォーマンス履歴](performance-history.md)
