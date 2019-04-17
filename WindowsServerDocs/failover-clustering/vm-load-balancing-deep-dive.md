---
ms.assetid: 5b5bab7a-727b-47ce-8efa-1d37a9639cba
title: "仮想マシンの負荷分散詳細"
ms.prod: windows-server-threshold
ms.technology: storage-failover-clustering
ms.topic: article
author: bhattacharyaz
manager: eldenc
ms.author: subhatt
ms.date: 09/19/2016
ms.openlocfilehash: 6ee092a2e51e2181a2203bc263377c4a8ec60246
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="virtual-machine-load-balancing-deep-dive"></a>仮想マシンの負荷分散詳細

> 適用対象: Windows Server (半期チャネル)、Windows Server 2016

Windows Server 2016 が導入されています、[仮想マシンの負荷分散機能](vm-load-balancing-overview.md)フェールオーバー クラスター内のノードの使用率を最適化します。 このドキュメントは、構成および管理する方法を説明<abbr title="仮想マシン">VM</abbr>負荷を分散します。 

## <a id="heuristics-for-balancing"></a>分散ヒューリスティック
<abbr title="仮想マシン">VM</abbr>ノードの負荷が次のヒューリスティックに基づくバーチャル マシン負荷分散が評価します。
1. 現在**メモリ不足**: メモリは、HYPER-V ホスト上の最も一般的なリソース制約
2. <abbr title="中央処理装置">CPU</abbr> **使用率**平均で 5 分間のウィンドウの上のノードの: 過剰コミット状態になるクラスター内のノードの軽減

## <a id="controlling-aggressiveness-of-balancing"></a>分散の強度を制御します。
使用して分散メモリと CPU のヒューリスティックに基づくの強度を構成することができます、クラスター共通プロパティ 'AutoBalancerLevel' でします。 PowerShell で次のコマンド実行の強度を制御するには。

```PowerShell
(Get-Cluster).AutoBalancerLevel = <value>
```

| AutoBalancerLevel | 強度 | 動作 |
|-------------------|----------------|----------|
| 1 (既定) | 低 | ホストが 80% 以上が読み込まれたときに移動します。 |
| 2 | [中] | ホストが 70% 以上が読み込まれたときに移動します。 |
| 3 | 高 | ホストが読み込まれる 60% 以上である場合、移動します。 | 

![分散の強度を構成する PowerShell のグラフィック](media/vm-load-balancing/detailed-VM-load-balancing-1.jpg)

## <a name="controlling-abbr-titlevirtual-machinevmabbr-load-balancing"></a>制御<abbr title="仮想マシン">VM</abbr>負荷分散
<abbr title="仮想マシン">VM</abbr>負荷分散は既定で有効にして、負荷分散が発生した場合は、クラスター共通プロパティ 'AutoBalancerMode' して構成できます。 タイミングを制御するには、残高、クラスターのノードの公平性。

### <a name="using-failover-cluster-manager"></a>フェールオーバー クラスター マネージャーを使用します。
1. クラスター名を右クリックし、[プロパティ] をオンにします。  
    ![フェールオーバー クラスター マネージャーでクラスターのプロパティを選択するグラフィック](media/vm-load-balancing/detailed-VM-load-balancing-2.jpg)

2.  「バランサー」ウィンドウを選択します  
    ![フェールオーバー クラスター マネージャーを使ってバランサー オプションを選択するグラフィック](media/vm-load-balancing/detailed-VM-load-balancing-3.jpg)

### <a name="using-powershell"></a>PowerShell を使用します。
次を実行します。
```powershell
(Get-Cluster).AutoBalancerMode = <value>
```

|AutoBalancerMode |動作| 
|:----------------:|:----------:|
|0| 無効になっています。| 
|1| 負荷を分散ノードへの参加| 
|2 (既定)| 負荷を分散ノードへの参加と 30 分ごと |

## <a name="abbr-titlevirtual-machinevmabbr-load-balancing-vs-system-center-virtual-machine-manager-dynamic-optimization"></a><abbr title="仮想マシン">VM</abbr>負荷分散と System Center Virtual Machine Manager の動的最適化の比較
ノードの公平性機能、機能を提供ボックスで、System Center Virtual Machine Manager なしの展開が対象としている (<abbr title="System Center Virtual Machine Manager">SCVMM</abbr>)。 <abbr title="System Center Virtual Machine Manager">SCVMM</abbr>動的最適化は、クラスター内の仮想マシンの負荷を分散するための推奨手段<abbr title="System Center Virtual Machine Manager">SCVMM</abbr>展開します。 <abbr title="System Center Virtual Machine Manager">SCVMM</abbr> Windows サーバーを自動的に無効化<abbr title="仮想マシン">VM</abbr>負荷分散の動的最適化が有効にするとします。

## <a name="see-also"></a>参照してください。
* [仮想マシンの負荷分散の概要](vm-load-balancing-overview.md)
* [フェールオーバー クラスタ リング](failover-clustering-overview.md)
* [HYPER-V の概要](../virtualization/hyper-v/Hyper-V-on-Windows-Server.md)
