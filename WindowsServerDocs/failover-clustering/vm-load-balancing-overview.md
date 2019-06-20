---
ms.assetid: f0d4cecc-5a03-448c-bef9-86c4730b4eb0
title: 仮想マシンの負荷分散の概要
ms.prod: windows-server-threshold
ms.technology: storage-failover-clustering
ms.topic: article
author: bhattacharyaz
manager: eldenc
ms.author: subhatt
ms.date: 09/19/2016
ms.openlocfilehash: 125dd7421cc1876c07983016498a9689d8a507ac
ms.sourcegitcommit: a3c9a7718502de723e8c156288017de465daaf6b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2019
ms.locfileid: "65475988"
---
# <a name="virtual-machine-load-balancing-overview"></a>仮想マシンの負荷分散の概要

> 適用対象:Windows Server 2019、Windows Server 2016

プライベート クラウド展開向けの重要な考慮事項は、設備投資 (です。<abbr title="設備投資">資本支出</abbr>) を運用環境に移動するために必要です。 運用環境でのトラフィックのピーク時に容量の不足を回避するためにプライベート クラウド環境に冗長性を追加する非常に一般的ですが、これが増加 <abbr title="設備投資">資本支出</abbr>. 冗長性の必要性は、いくつかのノードが複数の仮想マシン (をホストが不均衡のプライベート クラウドによって決まります<abbr title="仮想マシン">VM</abbr>) (再起動されたばかりのサーバー) など他のユーザーは過小使用とします。

<strong>簡単なビデオ概要</strong><br>(6 分)<br>
> [!VIDEO https://channel9.msdn.com/Blogs/windowsserver/Virtual-Machine-Load-Balancing-in-Windows-Server-2016/player]

## <a id="what-is-vm-load-balancing"></a>仮想マシンの負荷分散とは
<abbr title="仮想マシン">VM</abbr> 負荷分散は、Windows Server 2019 および Windows Server 2016 フェールオーバー クラスター内のノードの使用率を最適化するためのボックスの機能です。 "過剰コミット"ノードを識別し、再配布 <abbr title="仮想マシン">VM</abbr> コミット済みのノードにこれらのノードから。 この機能の主要な特徴のいくつか次に示します。

* *ダウンタイムのソリューションは*: <abbr title="バーチャル マシン">VM</abbr> アイドル状態のノードにライブ移行されます。
* *既存のクラスター環境とのシームレスな統合*:失敗ポリシーなどのアンチ アフィニティ、障害ドメインおよび実行可能な所有者が受け入れられます。
* *分散のためのヒューリスティック*: <abbr title="仮想マシン">VM</abbr> メモリ不足とノードの CPU 使用率。
* *詳細な制御*:既定で有効になっています。 オンデマンドまたは定期的な間隔でアクティブにできます。
* *強度しきい値*:次の 3 つのしきい値使用可能な配置の特性に基づいて。

## <a id="feature-in-action"></a>機能の動作
### <a id="new-node-added"></a>新しいノードが、フェールオーバー クラスターに追加されます。
![フェールオーバー クラスターに追加される新しいノードのグラフィック](media/vm-load-balancing/overview-VM-load-balancing-1.png)

新しい容量をフェールオーバー クラスターに追加すると、 <abbr title="バーチャル マシン">VM</abbr> 負荷分散機能では、容量を既存のノードから次の順序で新しく追加されたノードに自動的に分散します。

1. 圧力は、フェールオーバー クラスターで既存のノードで評価されます。
2. しきい値を超えるすべてのノードが識別されます。
3. 分散の優先順位を決定する高い負荷を持つノードが識別されます。
4. <abbr title="バーチャル マシン">VM</abbr> ライブ移行 (でダウンタイムなく) フェールオーバー クラスターで新しく追加されたノードにしきい値を超えるノードです。

### <a id="recurring-load-balancing"></a>定期的な負荷分散
![定期的な VM の負荷分散のグラフィック](media/vm-load-balancing/overview-VM-load-balancing-2.png)

で定期的な分散を構成して、クラスター ノードで負荷が分散 30 分ごとに評価されます。 または、圧力はオンデマンドで評価を指定できます。 手順の流れを次に示します。

1. 圧力は、プライベート クラウドのすべてのノードで評価されます。
2. しきい値を下回るとしきい値を超えるすべてのノードが識別されます。
3. 分散の優先順位を決定する高い負荷を持つノードが識別されます。
4. <abbr title="バーチャル マシン">VM</abbr> ライブ移行 (ダウンタイムなし) で、ノードの最小しきい値より下のノードにしきい値を超えた場合です。

## <a name="see-also"></a>関連項目
* [仮想マシンの負荷分散の詳細](vm-load-balancing-deep-dive.md)
* [フェールオーバー クラスタリング](failover-clustering-overview.md)
* [HYPER-V の概要](../virtualization/hyper-v/Hyper-V-on-Windows-Server.md)
