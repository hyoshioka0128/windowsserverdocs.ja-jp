---
ms.assetid: f0d4cecc-5a03-448c-bef9-86c4730b4eb0
title: "仮想マシンの負荷分散の概要"
ms.prod: windows-server-threshold
ms.technology: storage-failover-clustering
ms.topic: article
author: bhattacharyaz
manager: eldenc
ms.author: subhatt
ms.date: 09/19/2016
ms.openlocfilehash: 0a106db25d476088898b914481e6041f20ce2e9e
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="virtual-machine-load-balancing-overview"></a>仮想マシンの負荷分散の概要

> 適用対象: Windows Server (半期チャネル)、Windows Server 2016

プライベート クラウドの展開の重要な考慮事項が設備経費 (<abbr title="設備投資">CapEx</abbr>) を運用環境に移動するために必要です。 冗長性を運用環境でのピーク トラフィック時過少容量を回避するプライベート クラウドの展開に追加する非常に共通ですが、これが増加<abbr title="設備投資">CapEx</abbr>します。 冗長性の必要性は、不安定なプライベート クラウドがいくつかのノードに多くのバーチャル マシンをホストしている場所によって決まります (<abbr title="仮想マシン">Vm</abbr>) および (新たに再起動したサーバー) など他のユーザーは低くなります。

## <a id="what-is-vm-load-balancing"></a>仮想マシンの負荷分散とは?
<abbr title="仮想マシン">VM</abbr>負荷分散はボックスでの新機能では、Windows Server 2016 のフェールオーバー クラスターでノードの使用率を最適化することができます。 "過剰コミット"ノードを識別し、再配布<abbr title="仮想マシン">Vm</abbr>ノードの下にあるコミットにこれらのノードから。 この機能の注目すべき側面のとおりです。

* *ダウンタイム ソリューションです*:<abbr title="仮想マシン">Vm</abbr>がアイドル状態のノードにライブ マイグレーションします。
* *既存のクラスター環境でのシームレスな統合*: アンチ アフィニティ設定、障害ドメインおよび実行可能な所有者などの障害のポリシーが優先されます。
* *分散ヒューリスティック*:<abbr title="仮想マシン">VM</abbr>メモリ不足と、ノードの CPU 使用率。
* *より細かく制御*: 既定で有効にします。 オンデマンドでまたは定期的な間隔でアクティブことができます。
* *強度しきい値*: 展開の特性に基づいて、利用可能な 3 つのしきい値。

## <a id="feature-in-action"></a>機能の動作
### <a id="new-node-added"></a>新しいノードがフェールオーバー クラスターに追加されました。
![フェールオーバー クラスターに追加される新しいノードのグラフィック](media/vm-load-balancing/overview-VM-load-balancing-1.png)

新しい容量をフェールオーバー クラスターに追加するときに、<abbr title="仮想マシン">VM</abbr>負荷分散機能は、次の順序で新しく追加されたノードを既存のノードから容量を自動的に分散します。

1. フェールオーバー クラスターで既存のノードで、不足が評価されます。
2. しきい値を超えるすべてのノードが識別されます。
3. 分散の優先順位を決定する最も高い圧力でノードが識別されます。
4. <abbr title="仮想マシン">Vm</abbr>新しく追加されたフェールオーバー クラスター ノードにしきい値を超えるノードから (ダウンタイムなし) にライブ移行をいます。

### <a id="recurring-load-balancing"></a>定期的な負荷分散
![定期的な VM 負荷分散のグラフィック](media/vm-load-balancing/overview-VM-load-balancing-2.png)

定期的な分散を構成されているときに、クラスター ノード上の負荷が評価 30 分ごとに分散されます。 または、圧力では、オンデマンドで評価を指定できます。 次の手順のフローを示します。

1. プライベート クラウド内のすべてのノードで、不足が評価されます。
2. しきい値を下回るとしきい値を超えるすべてのノードが識別されます。
3. 分散の優先順位を決定する最も高い圧力でノードが識別されます。
4. <abbr title="仮想マシン">Vm</abbr>最小しきい値より下のノードにしきい値を超えるノードから (ダウンタイムなし) にライブ移行をいます。

## <a name="see-also"></a>参照してください。
* [仮想マシンの負荷分散の詳細](vm-load-balancing-deep-dive.md)
* [フェールオーバー クラスタ リング](failover-clustering-overview.md)
* [HYPER-V の概要](../virtualization/hyper-v/Hyper-V-on-Windows-Server.md)
