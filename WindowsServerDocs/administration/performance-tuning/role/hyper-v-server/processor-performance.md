---
title: Hyper V のプロセッサのパフォーマンス
description: HYPER-V のパフォーマンス チューニングのプロセッサ パフォーマンスに関する考慮事項
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Asmahi; SandySp; JoPoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: f16ee9cff9c244a8c579e008bced1e90b1a20673
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66435591"
---
# <a name="hyper-v-processor-performance"></a>Hyper V のプロセッサのパフォーマンス


## <a name="virtual-machine-integration-services"></a>バーチャル マシン統合サービス

仮想マシンの Integration Services には、CPU をエミュレートされたデバイスと比較した I/O のオーバーヘッドが大幅に減少するハイパー V 固有の I/O デバイスの有効化されたドライバーが含まれます。 サポートされているすべての仮想マシンでは、仮想マシンの Integration Services の最新バージョンをインストールする必要があります。 アイドル状態から、ゲストの CPU 使用率が高いゲストにサービスの減少は、ゲストを使用し、I/O スループットが向上します。 これは、HYPER-V を実行しているサーバーのパフォーマンスのチューニングは、最初の手順です。 サポートされるゲスト オペレーティング システムの一覧は、次を参照してください。 [Hyper-v 概要](https://technet.microsoft.com/library/hh831531.aspx)します。

## <a name="virtual-processors"></a>仮想プロセッサの数

Windows Server 2016 で HYPER-V 仮想マシンあたり 240 の仮想プロセッサの最大数をサポートします。 負荷の処理を要する CPU ではない仮想マシンは、1 つの仮想プロセッサを使用するように構成する必要があります。 これは、ゲスト オペレーティング システムで追加の同期のコストなど、複数の仮想プロセッサに関連付けられている追加のオーバーヘッドが原因です。

仮想マシンには、ピーク時の負荷の処理の 1 つ以上の CPU が必要な場合は、仮想プロセッサの数を増やします。

## <a name="background-activity"></a>バック グラウンド アクティビティ

バック グラウンド アクティビティがアイドル状態の仮想マシンで最小限に抑えることは、他の仮想マシンで別の場所で使用できる CPU サイクルを解放します。 Windows ゲストは、アイドル状態になった通常 1 つの CPU の 1% 未満を使用します。 バック グラウンドの仮想マシンの CPU 使用率を最小限に抑えるためのいくつかのベスト プラクティスを次に示します。

-   仮想マシンの Integration Services の最新バージョンをインストールします。

-   仮想マシンの設定 ダイアログ ボックス (使用して、マイクロソフト ハイパー V 固有のアダプター) を通じてエミュレートされたネットワーク アダプターを削除します。

-   未使用のデバイスなど、CD-ROM および COM ポートを削除するか、該当するメディアを切断します。

-   使用されていないとき、サインイン画面で、Windows ゲスト オペレーティング システムを維持し、スクリーン セーバーを無効にします。

-   スケジュールされたタスクと既定で有効になっているサービスを確認します。

-   確認を実行して既定では上にある ETW トレース プロバイダー **logman.exe-ets のクエリ**

-   (タイマー) などの定期的な処理を減らすためにサーバー アプリケーションを向上します。

-   ホストとゲストの両方のオペレーティング システムでは、サーバー マネージャーを閉じます。

-   仮想マシンのサムネイルを絶えず更新されますので、HYPER-V マネージャーが実行されているままにしないでください。

構成するための他のベスト プラクティスを次に、*クライアント バージョン*の全体的な CPU 使用率を削減する仮想マシンでの Windows:

-   SuperFetch、Windows Search などのバック グラウンド サービスを無効にします。

-   スケジュールされた最適化などのスケジュールされたタスクを無効にします。

## <a name="virtual-numa"></a>仮想 NUMA

大規模なスケール アップ ワークロードを仮想化を有効にする、Windows Server 2016 での HYPER-V には、仮想マシンのスケール制限が拡張されました。 単一の仮想マシンは、最大 240 の仮想プロセッサと 12 TB のメモリに割り当てることができます。 このような大規模な仮想マシンを作成するときに、ホスト システム上の複数の NUMA ノードからメモリが使用可能性があります。 このような仮想マシンの構成仮想プロセッサとメモリが、同じ NUMA ノードから割り当てられていないワークロードに NUMA の最適化を活用することができないのため、不適切なパフォーマンスがある可能性があります。

Windows Server 2016 では、HYPER-V は仮想マシンに仮想 NUMA トポロジを表示します。 既定では、この仮想 NUMA トポロジは基になっているホスト コンピューターの NUMA トポロジと一致するように最適化されます。 仮想 NUMA トポロジを仮想マシンに公開すると、仮想マシンで実行しているゲスト オペレーティング システムおよび NUMA 対応のアプリケーションは、物理コンピューターで実行しているときと同じように、NUMA パフォーマンスの最適化を利用できます。

ワークロードの観点からは、仮想と物理の NUMA の間に違いはありません。 仮想マシン内では、ワークロードがローカル メモリをデータに割り当てて、同じ NUMA ノード内でそのデータにアクセスすると、基になっている物理システムで高速のローカル メモリ アクセスが行われます。 リモート メモリ アクセスによるパフォーマンスの低下は回避されます。 VNUMA の NUMA 対応のアプリケーションのみを利用できます。

Microsoft SQL Server は、NUMA 対応のアプリケーションの例です。 詳細については、次を参照してください。[について、non-uniform Memory Access](https://technet.microsoft.com/library/ms178144.aspx)します。

仮想 NUMA 機能と動的メモリ機能を同時に使用することはできません。 動的メモリを有効にしている仮想マシンの仮想 NUMA ノードは、実質、1 つだけです。仮想 NUMA の設定に関係なく、NUMA トポロジは仮想マシンに提示されません。

仮想 NUMA の詳細については、次を参照してください。 [、Hyper-v 仮想 NUMA の概要](https://technet.microsoft.com/library/dn282282.aspx)します。

## <a name="see-also"></a>関連項目

-   [Hyper-V の用語](terminology.md)

-   [Hyper-V のアーキテクチャ](architecture.md)

-   [Hyper-V サーバーの構成](configuration.md)

-   [Hyper-V メモリのパフォーマンス](memory-performance.md)

-   [Hyper-V 記憶域の I/O のパフォーマンス](storage-io-performance.md)

-   [Hyper-V ネットワークの I/O のパフォーマンス](network-io-performance.md)

-   [仮想化環境のボトルネックの検出](detecting-virtualized-environment-bottlenecks.md)

-   [Linux 仮想マシン](linux-virtual-machine-considerations.md)
