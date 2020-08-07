---
title: Hyper-v ネットワーク i/o パフォーマンス
description: Hyper-v のパフォーマンスチューニングに関するネットワーク i/o のパフォーマンスに関する考慮事項
ms.topic: article
ms.author: asmahi; sandysp; jopoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: b21ed45b97b1bc657b8a77ac7731dd32f5090c3d
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87896101"
---
# <a name="hyper-v-network-io-performance"></a>Hyper-v ネットワーク i/o パフォーマンス

サーバー2016には、Hyper-v のネットワークパフォーマンスを最適化するための改善点と新機能がいくつか含まれています。  ネットワークパフォーマンスを最適化する方法に関するドキュメントは、この記事の将来のバージョンに含まれています。

## <a name="live-migration"></a>ライブ マイグレーション

ライブマイグレーションを使用すると、ネットワーク接続が切断されたり、ダウンタイムが発生したりすることなく、フェールオーバークラスターの1つのノードから同じクラスター内の別のノードに、実行中の仮想マシンを透過的に移動できます。

> [!NOTE]
> フェールオーバークラスタリングには、クラスターノードの共有記憶域が必要です。

実行中の仮想マシンを移動するプロセスは、2つの主要なフェーズに分けることができます。 最初のフェーズでは、仮想マシンのメモリを現在のホストから新しいホストにコピーします。 2番目のフェーズでは、バーチャルマシンの状態を現在のホストから新しいホストに転送します。 2つのフェーズの期間は、現在のホストから新しいホストにデータを転送できる速度によって大幅に決まります。

ライブマイグレーショントラフィック専用のネットワークを提供すると、ライブマイグレーションを完了するために必要な時間を最小限に抑えることができ、移行時間が一貫して維持されます。

![hyper-v のライブマイグレーションの構成例](../../media/perftune-guide-live-migration.png)

さらに、移行に関係する各ネットワークアダプターの送信バッファーと受信バッファーの数を増やすと、移行のパフォーマンスが向上します。

Windows Server 2012 R2 では、ネットワーク経由で転送する前にメモリを圧縮したり、ハードウェアでサポートされている場合はリモートダイレクトメモリアクセス (RDMA) を使用して、ライブマイグレーションを高速化するオプションが導入されました。

## <a name="additional-references"></a>その他の参照情報

-   [Hyper-V の用語](terminology.md)

-   [Hyper-V のアーキテクチャ](architecture.md)

-   [Hyper-V サーバーの構成](configuration.md)

-   [Hyper-V プロセッサのパフォーマンス](processor-performance.md)

-   [Hyper-V メモリのパフォーマンス](memory-performance.md)

-   [Hyper-V 記憶域の I/O のパフォーマンス](storage-io-performance.md)

-   [仮想化環境のボトルネックの検出](detecting-virtualized-environment-bottlenecks.md)

-   [Linux 仮想マシン](linux-virtual-machine-considerations.md)
