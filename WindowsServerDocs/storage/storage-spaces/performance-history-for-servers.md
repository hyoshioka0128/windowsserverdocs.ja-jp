---
title: サーバーのパフォーマンス履歴
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/0s/2018
Keywords: 記憶域スペース ダイレクト
ms.localizationpriority: medium
ms.openlocfilehash: 33fd62376e9769c23fc6b00eefde9a9b95eb4650
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820593"
---
# <a name="performance-history-for-servers"></a>サーバーのパフォーマンス履歴

> 適用先:Windows Server Insider Preview

このサブ トピックの[記憶域スペース ダイレクトのパフォーマンスの履歴](performance-history.md)サーバー用に収集されたパフォーマンスの履歴の詳細について説明します。 パフォーマンスの履歴はすべてのサーバー クラスターで使用できます。

   > [!NOTE]
   > 停止しているサーバーのパフォーマンスの履歴を収集できません。 コレクションは、ときに、サーバーが復帰自動的に再開されます。

## <a name="series-names-and-units"></a>系列名とユニット

これらの系列は、すべての対象となるサーバーで収集されます。

| シリーズ                           | Unit    |
|----------------------------------|---------|
| `clusternode.cpu.usage`          | % |
| `clusternode.cpu.usage.guest`    | % |
| `clusternode.cpu.usage.host`     | % |
| `clusternode.memory.total`       | バイト数   |
| `clusternode.memory.available`   | バイト数   |
| `clusternode.memory.usage`       | バイト数   |
| `clusternode.memory.usage.guest` | バイト数   |
| `clusternode.memory.usage.host`  | バイト数   |

さらに、ドライブの系列のなど`physicaldisk.size.total`などのネットワーク アダプターの系列、サーバーに接続されているすべての対象となるドライブごとに集計`networkadapter.bytes.total`サーバーに接続されているすべての対象となるネットワーク アダプターごとに集計します。

## <a name="how-to-interpret"></a>解釈する方法

| シリーズ                           | 解釈する方法                                                      |
|----------------------------------|-----------------------------------------------------------------------|
| `clusternode.cpu.usage`          | アイドル プロセッサ時間の割合。                        |
| `clusternode.cpu.usage.guest`    | ゲスト (仮想マシン) の要求時に使用されるプロセッサ時間の割合。 |
| `clusternode.cpu.usage.host`     | ホストの要求時に使用されるプロセッサ時間の割合。                    |
| `clusternode.memory.total`       | サーバーの物理メモリの合計。                              |
| `clusternode.memory.available`   | サーバーの使用可能なメモリ。                                   |
| `clusternode.memory.usage`       | サーバーの割り当てられたメモリを (使用できません)。                   |
| `clusternode.memory.usage.guest` | ゲスト (仮想マシン) の要求時に割り当てられたメモリ。               |
| `clusternode.memory.usage.host`  | ホストの要求時に割り当てられたメモリ。                                  |

## <a name="where-they-come-from"></a>来た

`cpu.*`シリーズは、HYPER-V が有効になっているかどうかに応じてさまざまなパフォーマンス カウンターから収集されます。

場合は、HYPER-V が有効になります。

| シリーズ                           | ソースのカウンター |
|----------------------------------|----------------|
| `clusternode.cpu.usage`          | `Hyper-V Hypervisor Logical Processor` > `_Total` > `% Total Run Time`      |
| `clusternode.cpu.usage.guest`    | `Hyper-V Hypervisor Virtual Processor` > `_Total` > `% Total Run Time`      |
| `clusternode.cpu.usage.host`     | `Hyper-V Hypervisor Root Virtual Processor` > `_Total` > `% Total Run Time` |

使用して、`% Total Run Time`カウンターにより、パフォーマンスの履歴がすべての使用量を属性します。

場合は、HYPER-V が有効になっていません。

| シリーズ                           | ソースのカウンター |
|----------------------------------|----------------|
| `clusternode.cpu.usage`          | `Processor` > `_Total` > `% Processor Time` |
| `clusternode.cpu.usage.guest`    | *zero* |
| `clusternode.cpu.usage.host`     | *使用率の合計と同じ* |

不完全な同期は、本`clusternode.cpu.usage`は常に`clusternode.cpu.usage.host`plus`clusternode.cpu.usage.guest`します。

同じ注意点があります`clusternode.cpu.usage.guest`の合計は、常に`vm.cpu.usage`のすべてのバーチャル マシン ホスト サーバーにします。

`memory.*`シリーズは、(近日)。

  > [!NOTE]
  > カウンターは、サンプリングされなかった、全体の間隔で測定されます。 たとえば、サーバーがアイドル状態 9 秒ですが 100% の CPU に急増の 10 日の 1 秒間その`clusternode.cpu.usage`この 10 秒間に平均で 10% として記録されます。 これにより、そのパフォーマンス履歴がすべてのアクティビティをキャプチャしがノイズに堅牢になりました。

## <a name="usage-in-powershell"></a>PowerShell での使用法

使用して、 [Get-clusternode](https://docs.microsoft.com/powershell/module/failoverclusters/get-clusternode)コマンドレット。

```PowerShell
Get-ClusterNode <Name> | Get-ClusterPerf
```

## <a name="see-also"></a>関連項目

- [記憶域スペース ダイレクトのパフォーマンスの履歴](performance-history.md)
