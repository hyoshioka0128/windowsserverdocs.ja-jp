---
title: HYPER-V ネットワーク I/O のパフォーマンス
description: ネットワーク、HYPER-V のパフォーマンス チューニングの i/o パフォーマンスに関する考慮事項
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Asmahi; SandySp; JoPoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: d52c4fff6c7e06fb0a9f2b44ea51a0a790e6674d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814363"
---
# <a name="hyper-v-network-io-performance"></a>HYPER-V ネットワーク I/O のパフォーマンス

Server 2016 には、いくつかの機能強化と、HYPER-V でのネットワーク パフォーマンスを最適化するために新しい機能が含まれています。  ネットワーク パフォーマンスを最適化する方法に関するドキュメントは、この記事の将来のバージョンに含まれます。

## <a name="live-migration"></a>ライブ マイグレーション

ライブ マイグレーションでは、ネットワーク接続の切断または計画外のダウンタイムなしで同じクラスター内の別のノードにフェールオーバー クラスターの 1 つのノードから実行中の仮想マシンを透過的に移動することができます。

**注**  フェールオーバー クラスタ リング クラスター ノードの共有ストレージが必要です。

実行中の仮想マシンを移動するプロセスは、2 つの主要なフェーズに分けることができます。 最初のフェーズでは、新しいホストに現在のホストから仮想マシンのメモリをコピーします。 2 番目のフェーズでは、新しいホストに現在のホストから仮想マシンの状態を転送します。 両方のフェーズの期間は、大幅に、データが新しいホストに現在のホストから転送する速度によって決まります。

専用のネットワークを提供すると、ライブ マイグレーションのトラフィックを最小限に抑えるライブ移行の完了に必要な時間と、一貫性のある移行に要する時間になります。

![hyper-v のライブ マイグレーションの構成の例](../../media/perftune-guide-live-migration.png)

さらに、送信の数を増やすと、バッファーを受信アダプターは、移行に関係する各ネットワークの移行のパフォーマンスを向上させることができます。

Windows Server 2012 R2 では、ハードウェアがサポートされている場合、ネットワーク経由で転送する前にメモリを圧縮することで、ライブ マイグレーションを高速化、またはリモート ダイレクト メモリ アクセス (RDMA) を使用するオプションが導入されました。

## <a name="see-also"></a>関連項目

-   [HYPER-V 用語](terminology.md)

-   [HYPER-V のアーキテクチャ](architecture.md)

-   [HYPER-V サーバーの構成](configuration.md)

-   [HYPER-V のプロセッサのパフォーマンス](processor-performance.md)

-   [HYPER-V でメモリのパフォーマンス](memory-performance.md)

-   [HYPER-V ストレージの I/O パフォーマンス](storage-io-performance.md)

-   [仮想化環境のボトルネックの検出](detecting-virtualized-environment-bottlenecks.md)

-   [Linux 仮想マシン](linux-virtual-machine-considerations.md)
