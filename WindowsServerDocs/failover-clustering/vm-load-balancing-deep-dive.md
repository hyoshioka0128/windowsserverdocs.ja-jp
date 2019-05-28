---
ms.assetid: 5b5bab7a-727b-47ce-8efa-1d37a9639cba
title: 仮想マシンの負荷分散の詳細を確認
ms.prod: windows-server-threshold
ms.technology: storage-failover-clustering
ms.topic: article
author: bhattacharyaz
manager: eldenc
ms.author: subhatt
ms.date: 09/19/2016
ms.openlocfilehash: 50213cf47c2c59f1775ae704e82ed51794715ac0
ms.sourcegitcommit: 276a480b470482cba4682caa3df4cd07ba5b7801
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66198550"
---
# <a name="virtual-machine-load-balancing-deep-dive"></a>仮想マシンの負荷分散の詳細を確認

> 適用対象:Windows Server 2019、Windows Server 2016

[仮想マシンの負荷分散機能](vm-load-balancing-overview.md)フェールオーバー クラスター内のノードの使用率を最適化します。 このドキュメントでは、構成し、VM の負荷分散を制御する方法について説明します。 

## <a id="heuristics-for-balancing"></a>分散のためのヒューリスティック
仮想マシンに負荷分散には、次のヒューリスティックに基づくノードの負荷が評価されます。
1. 現在**メモリ不足**:メモリは、HYPER-V ホスト上で最も一般的なリソースの制約
2. CPU**使用率**の 5 分間の平均ノード。過剰コミット状態になるクラスター内のノードを軽減します。

## <a id="controlling-aggressiveness-of-balancing"></a>分散の強度を制御します。
使用して、メモリと CPU のヒューリスティックに基づく分散の強度を構成できる、クラスターの一般的なプロパティ 'AutoBalancerLevel' でします。 PowerShell で実行して、次の動的最適化のレベルを制御するには。

```PowerShell
(Get-Cluster).AutoBalancerLevel = <value>
```

| AutoBalancerLevel | 動的最適化のレベル | 動作 |
|-------------------|----------------|----------|
| 1 (既定) | 低 | ホストが 80% 以上が読み込まれるときに移動します。 |
| 2 | 中 | ホストが 70% 以上が読み込まれるときに移動します。 |
| 3 | 高 | ノードの平均し、ホストが平均値を超える 5% より多くの場合、移動 | 

![分散の強度を構成するには PowerShell のグラフィック](media/vm-load-balancing/detailed-VM-load-balancing-1.jpg)

## <a name="controlling-vm-load-balancing"></a>VM の負荷分散を制御します。
既定で有効になっている VM が負荷分散と負荷分散の発生時に、クラスターの一般的なプロパティ 'AutoBalancerMode' で構成できます。 タイミングを制御するには、は、ノードの公平性は、クラスターのバランスをとります。

### <a name="using-failover-cluster-manager"></a>フェールオーバー クラスター マネージャーを使用します。
1. クラスター名を右クリックし、[プロパティ] オプションを選択します  
    ![クラスターをフェールオーバー クラスター マネージャーのプロパティを選択した場合のグラフィック](media/vm-load-balancing/detailed-VM-load-balancing-2.jpg)

2.  「バランサー」ウィンドウを選択します。  
    ![フェールオーバー クラスター マネージャーを介してバランサー オプションを選択した場合のグラフィック](media/vm-load-balancing/detailed-VM-load-balancing-3.jpg)

### <a name="using-powershell"></a>PowerShell を使用します。
次を実行します。
```powershell
(Get-Cluster).AutoBalancerMode = <value>
```

|AutoBalancerMode |動作| 
|:----------------:|:----------:|
|0| Disabled| 
|1| 結合のノードに対して負荷分散| 
|2 (既定)| 負荷分散ノードの参加と 30 分ごと |

## <a name="vm-load-balancing-vs-system-center-virtual-machine-manager-dynamic-optimization"></a>Vs の VM の負荷を分散します。System Center Virtual Machine Manager の動的最適化
ノードの公平性機能は、組み込みの機能は、System Center Virtual Machine Manager (SCVMM) なしの展開は対象を提供します。 SCVMM の動的最適化は、SCVMM のデプロイ用クラスターで仮想マシンの負荷分散の推奨されるメカニズムです。 SCVMM に自動的に無効に、Windows Server VM の負荷分散動的最適化が有効にするとします。

## <a name="see-also"></a>関連項目
* [仮想マシンの負荷分散の概要](vm-load-balancing-overview.md)
* [フェールオーバー クラスタリング](failover-clustering-overview.md)
* [HYPER-V の概要](../virtualization/hyper-v/Hyper-V-on-Windows-Server.md)
