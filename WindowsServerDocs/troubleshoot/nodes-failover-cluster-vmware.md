---
title: アクティブなフェールオーバー クラスターのメンバーシップからノードを削除する
description: この記事では、アクティブなフェールオーバークラスターのメンバーシップから削除されたノードを検索する際の問題について説明します。
ms.date: 05/28/2020
author: Deland-Han
ms.author: delhan
ms.openlocfilehash: da46b39f853476676a06bcaaa20338dd1a178586
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87935572"
---
# <a name="nodes-being-removed-from-failover-cluster-membership-on-vmware-esx"></a>VMWare ESX のフェールオーバークラスターメンバーシップから削除されているノード

この記事では、ノードが VMWare ESX でホストされている場合に、アクティブフェールオーバークラスターのメンバーシップから削除されたノードを見つける問題に対処します。

## <a name="symptom"></a>症状

この問題が発生すると、イベントビューアーのシステムイベントログにが表示されます。

![イベント1135](media/nodes-failover-cluster-vmware/1135.png)

## <a name="resolution"></a>解決方法

1つの問題として、受信バッファーが低すぎるために大量のトラフィックを処理するように設定されているため、VMXNET3 アダプターが受信ネットワークパケットを削除していることが挙げられます。 パフォーマンスモニターを使用して、"Network Interface\Packets Received が破棄されました" というカウンターを確認することで、この問題が発生しているかどうかを簡単に確認できます。

![カウンターの追加](media/nodes-failover-cluster-vmware/0527.png)

このカウンターを追加したら、平均値、最小値、および最大値を確認し、0より大きい値の場合は受信バッファーをアダプター用に調整する必要があります。 この問題については、VMWare のサポート技術情報 ( [ESXi 5.x の VMXNET3 vNIC のゲスト OS レベルでの大きなパケット損失](https://kb.vmware.com/s/article/2039495)) に記載されています。
