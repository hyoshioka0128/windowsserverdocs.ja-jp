---
ms.assetid: f0d4cecc-5a03-448c-bef9-86c4730b4eb0
title: 仮想マシンの負荷分散の概要
ms.prod: windows-server
ms.technology: storage-failover-clustering
ms.topic: article
author: bhattacharyaz
manager: eldenc
ms.author: subhatt
ms.date: 09/19/2016
ms.openlocfilehash: 1fea9e6297399a5081eb8fef1876f1b11d23c745
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71360980"
---
# <a name="virtual-machine-load-balancing-overview"></a>仮想マシンの負荷分散の概要

> 適用対象:Windows Server 2019、Windows Server 2016

プライベートクラウドの展開に関する重要な考慮事項は、資本支出 (<abbr title="資本支出">CapEx</abbr>) を運用環境に移行するために必要です。 実稼働環境でのピークトラフィック中は容量が少ないことを避けるために、プライベートクラウドのデプロイに冗長性を追加するのは非常に一般的ですが、 <abbr title="資本支出">CapEx</abbr>. 冗長性の必要性は、一部のノードがより多くの Virtual Machines をホストしている、不均衡なプライベートクラウドによって促進されます (<abbr title="仮想マシン">VM</abbr>) が使用されていない場合もあります (新しく再起動されたサーバーなど)。

<strong>クイックビデオの概要</strong><br>(6 分)<br>
> [!VIDEO https://channel9.msdn.com/Blogs/windowsserver/Virtual-Machine-Load-Balancing-in-Windows-Server-2016/player]

## <a id="what-is-vm-load-balancing"></a>仮想マシンの負荷分散とは
<abbr title="仮想マシン">VM</abbr> 負荷分散は、フェールオーバークラスター内のノードの使用を最適化することができる Windows Server 2019 および Windows Server 2016 のインボックス機能です。 過剰コミットされたノードを識別し、再配布します。 <abbr title="仮想マシン">VM</abbr> これらのノードから、コミットされていないノードにします。 この機能には、次のような特徴があります。

* *ダウンタイムなしのソリューション*です。 <abbr title="仮想マシン">VM</abbr> アイドル状態のノードにライブ移行されます。
* *既存のクラスター環境とのシームレスな統合*:障害ポリシー (アンチアフィニティ、障害ドメイン、実行可能な所有者など) は受け入れられます。
* *分散のヒューリスティック*: <abbr title="仮想マシン">VM</abbr> ノードのメモリ負荷と CPU 使用率。
* *詳細な制御*:既定で有効になっています。 オンデマンドで、または一定の間隔でアクティブ化できます。
* *強度しきい値*:デプロイの特性に基づいて、3つのしきい値を利用できます。

## <a id="feature-in-action"></a>動作中の機能
### <a id="new-node-added"></a>新しいノードがフェールオーバークラスターに追加されます。
![フェールオーバークラスターに新しいノードが追加されているグラフィック](media/vm-load-balancing/overview-VM-load-balancing-1.png)

フェールオーバークラスターに新しい容量を追加すると、 <abbr title="仮想マシン">VM</abbr> 負荷分散機能では、次の順序で、既存のノードから新しく追加されたノードに容量が自動的に分散されます。

1. 負荷は、フェールオーバークラスター内の既存のノードで評価されます。
2. しきい値を超えるすべてのノードが識別されます。
3. 負荷の優先順位を決定するために、負荷の高いノードが特定されます。
4. <abbr title="仮想マシン">VM</abbr> フェールオーバークラスター内の新しく追加されたノードに対して、しきい値を超えたノードからライブ移行されます (ダウンタイムはありません)。

### <a id="recurring-load-balancing"></a>定期的な負荷分散
![定期的な VM 負荷分散の図](media/vm-load-balancing/overview-VM-load-balancing-2.png)

定期的に分散するように構成すると、クラスターノードの負荷は30分ごとに評価されます。 また、必要に応じて圧力を評価することもできます。 ステップのフローを次に示します。

1. 負荷は、プライベートクラウド内のすべてのノードで評価されます。
2. しきい値を超えるすべてのノードとしきい値を下回るすべてのノードが識別されます。
3. 負荷の優先順位を決定するために、負荷の高いノードが特定されます。
4. <abbr title="仮想マシン">VM</abbr> [最小しきい値] の下のノードに対して、しきい値を超えるノードからライブ移行されます (ダウンタイムはありません)。

## <a name="see-also"></a>関連項目
* [仮想マシンの負荷分散の詳細](vm-load-balancing-deep-dive.md)
* [フェールオーバー クラスタリング](failover-clustering-overview.md)
* [Hyper-v の概要](../virtualization/hyper-v/Hyper-V-on-Windows-Server.md)
