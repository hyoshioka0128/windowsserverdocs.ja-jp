---
title: Hyper-V のアーキテクチャ
description: Hyper-v アーキテクチャ condsiderations パフォーマンス チューニング
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Asmahi; SandySp; JoPoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: fcc87b04698a44e115c8f49150fe33443f8e6a88
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890283"
---
# <a name="hyper-v-architecture"></a>Hyper-V のアーキテクチャ

HYPER-V には、タイプ 1 ハイパーバイザー ベースのアーキテクチャが機能します。 ハイパーバイザーでは、プロセッサとメモリを仮想化し、子パーティション (仮想マシン) を管理し、仮想マシンへの I/O デバイスなどのサービスを公開するには、ルート パーティション内の仮想化スタックのメカニズムを提供します。

ルート パーティションでは、所有し、物理 I/O デバイスに直接アクセスします。 ルート パーティション内の仮想化スタックでは、仮想マシン、管理 Api、および仮想化された I/O デバイスのメモリ マネージャーを提供します。 統合デバイス electronics (IDE) のディスク コント ローラーと ps/2 入力デバイスのポートとパフォーマンスの向上のハイパー V 固有の統合デバイスをサポートし、負荷の減少など、エミュレートされたデバイスも実装します。

![hyper-v ハイパーバイザー ベースのアーキテクチャ](../../media/perftune-guide-hyperv-arch.png)

ハイパー V 固有の I/O のアーキテクチャは、ルート パーティションと仮想化サービス内のクライアント (Vsc)、子パーティションでの仮想化サービス プロバイダー (Vsp) で構成されます。 各サービスは、デバイスとして、VMBus、I/O バスとして機能し、共有メモリなどのメカニズムを使用する仮想マシン間の高パフォーマンス通信を介して公開されます。 ゲスト オペレーティング システムのプラグ アンド プレイのマネージャーは、VMBus を含め、これらのデバイスを列挙し、適切なデバイス ドライバー (仮想サービス クライアント) を読み込みます。 I/O 以外のサービスは、このアーキテクチャを通じても公開されます。

Windows Server 2008 での仮想マシンで実行されているときに、その動作を最適化するためにオペレーティング システム機能啓発開始しています。 利点には、メモリ仮想化、マルチコアのスケーラビリティの向上と、バック グラウンドのゲスト オペレーティング システムの CPU 使用率を減らすのコストの削減が含まれます。

次のセクションでは、Hyper-v の役割を実行するサーバーでパフォーマンスの向上を生成するためのベスト プラクティスをお勧めします。

## <a name="see-also"></a>関連項目

-   [HYPER-V 用語](terminology.md)

-   [HYPER-V サーバーの構成](configuration.md)

-   [HYPER-V のプロセッサのパフォーマンス](processor-performance.md)

-   [HYPER-V でメモリのパフォーマンス](memory-performance.md)

-   [HYPER-V ストレージの I/O パフォーマンス](storage-io-performance.md)

-   [HYPER-V ネットワークの I/O パフォーマンス](network-io-performance.md)

-   [仮想化環境のボトルネックの検出](detecting-virtualized-environment-bottlenecks.md)

-   [Linux 仮想マシン](linux-virtual-machine-considerations.md)
