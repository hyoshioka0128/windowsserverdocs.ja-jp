---
title: Hyper-V のアーキテクチャ
description: パフォーマンスチューニングのための hyper-v アーキテクチャ condsiderations
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Asmahi; SandySp; JoPoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 7ed8522ec34e9e262f835530a248567ebbd0ddc9
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70866667"
---
# <a name="hyper-v-architecture"></a>Hyper-V のアーキテクチャ

Hyper-v は、種類1のハイパーバイザーベースのアーキテクチャを特徴としています。 ハイパーバイザーは、プロセッサとメモリを仮想化し、ルートパーティション内の仮想化スタックが子パーティション (仮想マシン) を管理し、i/o デバイスなどのサービスを仮想マシンに公開するメカニズムを提供します。

ルートパーティションはを所有し、物理 i/o デバイスに直接アクセスします。 ルートパーティションの仮想化スタックは、仮想マシン、管理 Api、および仮想化 i/o デバイス用のメモリマネージャーを提供します。 また、統合されたデバイスエレクトロニクス (IDE) ディスクコントローラーや PS/2 入力デバイスポートなどのエミュレートされたデバイスを実装します。また、パフォーマンスを向上させ、オーバーヘッドを削減するために、Hyper-v 固有の統合デバイスをサポートしています。

![hyper-v ハイパーバイザーベースのアーキテクチャ](../../media/perftune-guide-hyperv-arch.png)

Hyper-v 固有の i/o アーキテクチャは、子パーティションのルートパーティションおよび仮想化サービスクライアント (VSCs) の仮想化サービスプロバイダー (.Vsps) で構成されています。 各サービスは、VMBus 経由でデバイスとして公開されます。これは、i/o バスとして機能し、共有メモリなどのメカニズムを使用する仮想マシン間の高パフォーマンスの通信を可能にします。 ゲストオペレーティングシステムのプラグアンドプレイ manager は、このようなデバイス (VMBus を含む) を列挙し、適切なデバイスドライバー (仮想サービスクライアント) を読み込みます。 I/o 以外のサービスも、このアーキテクチャを通じて公開されます。

Windows Server 2008 以降では、オペレーティングシステムの機能は、仮想マシンで実行されているときの動作を最適化するために enlightenments しています。 利点としては、メモリの仮想化コストの削減、マルチコアのスケーラビリティの向上、ゲストオペレーティングシステムのバックグラウンド CPU 使用率の削減などがあります。

以下のセクションでは、Hyper-v の役割を実行しているサーバーのパフォーマンスを向上させるベストプラクティスについて説明します。

## <a name="see-also"></a>関連項目

-   [Hyper-V の用語](terminology.md)

-   [Hyper-V サーバーの構成](configuration.md)

-   [Hyper-V プロセッサのパフォーマンス](processor-performance.md)

-   [Hyper-V メモリのパフォーマンス](memory-performance.md)

-   [Hyper-V 記憶域の I/O のパフォーマンス](storage-io-performance.md)

-   [Hyper-V ネットワークの I/O のパフォーマンス](network-io-performance.md)

-   [仮想化環境のボトルネックの検出](detecting-virtualized-environment-bottlenecks.md)

-   [Linux 仮想マシン](linux-virtual-machine-considerations.md)
