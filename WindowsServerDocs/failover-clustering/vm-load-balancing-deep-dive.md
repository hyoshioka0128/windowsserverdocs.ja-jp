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
ms.openlocfilehash: f90802a8e77ade0b9f282730e7cb61c73a246018
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853423"
---
# <a name="virtual-machine-load-balancing-deep-dive"></a>仮想マシンの負荷分散の詳細を確認

> 適用対象:Windows Server 2016 の Windows Server (半期チャネル)

Windows Server 2016 で導入、[仮想マシンの負荷分散機能](vm-load-balancing-overview.md)フェールオーバー クラスター内のノードの使用率を最適化します。 このドキュメントは、構成および制御する方法を説明します<abbr title="仮想マシン">VM</abbr>負荷分散します。 

## <a id="heuristics-for-balancing"></a>分散のためのヒューリスティック
<abbr title="仮想マシン">VM</abbr>次のヒューリスティックに基づくノードの負荷を評価する仮想マシンに負荷分散します。
1. 現在**メモリ不足**:メモリは、HYPER-V ホスト上で最も一般的なリソースの制約
2. <abbr title="中央処理装置">CPU</abbr> **使用率**の 5 分間の平均ノード。過剰コミット状態になるクラスター内のノードを軽減します。

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

## <a name="controlling-abbr-titlevirtual-machinevmabbr-load-balancing"></a>制御<abbr title="仮想マシン">VM</abbr>負荷分散
<abbr title="仮想マシン">VM</abbr>既定で有効になっている負荷分散と負荷分散の発生時に、クラスターの一般的なプロパティ 'AutoBalancerMode' で構成できます。 タイミングを制御するには、は、ノードの公平性は、クラスターのバランスをとります。

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

## <a name="abbr-titlevirtual-machinevmabbr-load-balancing-vs-system-center-virtual-machine-manager-dynamic-optimization"></a><abbr title="バーチャル マシン">VM</abbr> vs の負荷分散します。System Center Virtual Machine Manager の動的最適化
ノードの公平性機能せず、System Center Virtual Machine Manager の展開が対象とする組み込み機能を提供します (<abbr title="System Center Virtual Machine Manager">SCVMM</abbr>)。 <abbr title="System Center Virtual Machine Manager">SCVMM</abbr>動的最適化は、推奨されるメカニズムで、クラスターの仮想マシンの負荷を分散<abbr title="System Center Virtual Machine Manager">SCVMM</abbr>展開します。 <abbr title="System Center Virtual Machine Manager">SCVMM</abbr> Windows Server を自動的に無効に<abbr title="仮想マシン">VM</abbr>負荷分散の動的最適化が有効にするとします。

## <a name="see-also"></a>関連項目
* [仮想マシンの負荷分散の概要](vm-load-balancing-overview.md)
* [フェールオーバー クラスタ リング](failover-clustering-overview.md)
* [HYPER-V の概要](../virtualization/hyper-v/Hyper-V-on-Windows-Server.md)
