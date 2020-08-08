---
ms.assetid: 5b5bab7a-727b-47ce-8efa-1d37a9639cba
title: 仮想マシンの負荷分散の詳細
ms.topic: article
author: bhattacharyaz
manager: eldenc
ms.author: subhatt
ms.date: 09/19/2016
ms.openlocfilehash: cebdc8c192abd737478c3b7a0c3db3e4a2bc8091
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87957149"
---
# <a name="virtual-machine-load-balancing-deep-dive"></a>仮想マシンの負荷分散の詳細

> 適用先:Windows Server 2019、Windows Server 2016

[仮想マシンの負荷分散機能](vm-load-balancing-overview.md)により、フェールオーバークラスター内のノードの使用率が最適化されます。 このドキュメントでは、VM の負荷分散を構成および制御する方法について説明します。

## <a name="heuristics-for-balancing"></a><a id="heuristics-for-balancing"></a>分散のヒューリスティック
仮想マシンの負荷分散は、次のヒューリスティックに基づいてノードの負荷を評価します。
1. 現在の**メモリ不足**: メモリは、hyper-v ホスト上の最も一般的なリソース制約です。
2. ノードの CPU**使用率**が5分間で平均化されている: クラスター内のノードが過剰コミット状態になるのを軽減します。

## <a name="controlling-the-aggressiveness-of-balancing"></a><a id="controlling-aggressiveness-of-balancing"></a>分散の強度を制御する
メモリと CPU のヒューリスティックに基づく分散の強度は、クラスターの共通プロパティ ' AutoBalancerLevel ' を使用して構成できます。 強度を制御するには、PowerShell で次のように実行します。

```PowerShell
(Get-Cluster).AutoBalancerLevel = <value>
```

| AutoBalancerLevel | 強度 | 動作 |
|-------------------|----------------|----------|
| 1 (既定) | 低 | ホストの負荷が80% を超えたときに移動する |
| 2 | Medium | ホストの負荷が70% を超えたときに移動する |
| 3 | 高 | 平均ノード数とホストの平均が5% を超えた場合の移動 |

![分散の強度を構成するための PowerShell のグラフィック](media/vm-load-balancing/detailed-VM-load-balancing-1.jpg)

## <a name="controlling-vm-load-balancing"></a>VM の負荷分散の制御
VM の負荷分散は、既定で有効になっており、負荷分散が発生したときに、クラスター共通プロパティ ' AutoBalancerMode ' によって構成できます。 ノードがクラスターを公平に分散するタイミングを制御するには、次の操作を行います。

### <a name="using-failover-cluster-manager"></a>フェールオーバークラスターマネージャーの使用:
1. クラスター名を右クリックし、[ ![ クラスターのプロパティの選択] の [プロパティ] オプショングラフィックを選択しフェールオーバークラスターマネージャー](media/vm-load-balancing/detailed-VM-load-balancing-2.jpg)

2.  から [バランサー] オプションを選択するための "バランサー" ペインのグラフィックを選択し ![ フェールオーバークラスターマネージャー](media/vm-load-balancing/detailed-VM-load-balancing-3.jpg)

### <a name="using-powershell"></a>PowerShell の使用:
次のコマンドレットを実行します。
```powershell
(Get-Cluster).AutoBalancerMode = <value>
```

|AutoBalancerMode |動作|
|:----------------:|:----------:|
|0| 無効|
|1| ノード結合の負荷分散|
|2 (既定値)| ノード結合と30分ごとの負荷分散 |

## <a name="vm-load-balancing-vs-system-center-virtual-machine-manager-dynamic-optimization"></a>VM の負荷分散と System Center Virtual Machine Manager の動的最適化
ノードの公平性機能には、インボックス機能が用意されており、System Center Virtual Machine Manager (SCVMM) を使用しない展開を対象としています。 Scvmm の動的最適化は、SCVMM デプロイのためにクラスターで仮想マシンの負荷を分散するために推奨されるメカニズムです。 動的最適化を有効にすると、Windows Server VM の負荷分散が自動的に無効になります。

## <a name="see-also"></a>参照
* [仮想マシンの負荷分散の概要](vm-load-balancing-overview.md)
* [フェールオーバー クラスタリング](failover-clustering-overview.md)
* [Hyper-v の概要](../virtualization/hyper-v/Hyper-V-on-Windows-Server.md)
