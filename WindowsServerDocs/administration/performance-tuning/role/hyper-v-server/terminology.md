---
title: HYPER-V 用語
description: HYPER-V のパフォーマンス チューニングで役に立ちます、hyper-v 用語
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Asmahi; SandySp; JoPoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: bc970633ff24827207eb3a27e282656f2486a6eb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841143"
---
# <a name="hyper-v-terminology"></a>Hyper V の用語集
このセクションでは、このパフォーマンスのチューニング トピック全体で使用される仮想マシン テクノロジに固有の重要な用語をまとめたものです。

| 用語        | 定義           |
| ------------- |:------------|
|*子パーティション* | ルート パーティションによって作成される仮想マシン。|
|*デバイスの仮想化* | により、ハードウェア リソースが抽象化され、複数のコンシューマー間で共有されます。|
|*エミュレートされたデバイス*|ゲストは、そのハードウェア デバイスの一般的なドライバーを使用できるように、実際の物理ハードウェア デバイスを模倣した仮想化されたデバイス。|
|*enlightenment*|仮想マシン環境を認識し、仮想マシンの動作を調整するゲスト オペレーティング システムを最適化します。|
|*ゲスト*|パーティションで実行されているソフトウェア。 フル機能のオペレーティング システムまたは小規模な特別な用途のカーネルを使用できます。 ハイパーバイザーは、ゲストに依存しません。|
|*ハイパーバイザー*|ハードウェア上で、1 つまたは複数のオペレーティング システムの下に位置するソフトウェア レイヤーです。 ハイパーバイザーの主な目的は、パーティションと呼ばれる分離された実行環境を提供することです。 各パーティションには、独自の (中央処理装置または CPU、メモリ、およびデバイス) の仮想化されたハードウェア リソース セット。 ハイパーバイザーは、基盤となるハードウェアへのアクセスを制御し調整します。|
|*論理プロセッサ*| 1 つのスレッドの実行 (命令ストリーム) を処理する処理単位です。 プロセッサ コアごとの 1 つまたは複数の論理プロセッサと 1 つのプロセッサ ソケット 1 つまたは複数のコアが表示されることができます。|
| *パススルー ディスクへのアクセス*|ゲスト内で仮想ディスクと物理ディスク全体の表現。 データとコマンドによって渡されますを介在する処理を実行しないと (ルート パーティションのネイティブ ストレージ スタック) を通じて、物理ディスクを仮想のスタック。|
|*ルート パーティション*|ルート パーティションをまず作成し、ハイパーバイザーはほとんどのデバイスやシステム メモリを含む、すべてのリソースを所有します。 ルート パーティションは、仮想化スタックをホストし、作成し、子パーティションを管理します。|
|*ハイパー V 固有のデバイス*|物理ハードウェアなしアナログ仮想化されたデバイスでは、そのゲストは、そのハイパー V 固有のデバイス ドライバー (仮想サービス クライアント) を必要があります。 ドライバーは、仮想マシン バス (VMBus) を使用して、ルート パーティションで仮想化されたデバイスのソフトウェアと通信します。|
|*仮想マシン*|ソフトウェア エミュレーションによって作成された、実際のコンピューターと同じ特性を持っている仮想コンピューター。|
| *仮想ネットワーク スイッチ*|(仮想スイッチとも呼ばれます)物理ネットワーク スイッチの仮想バージョン。 仮想ネットワークは、1 つ以上のバーチャル マシンにローカルまたは外部ネットワーク リソースへのアクセスを提供するように構成することができます。|
|*仮想プロセッサ*|論理プロセッサ上で実行がスケジュールされているプロセッサの仮想抽象化です。 仮想マシンには、1 つまたは複数の仮想プロセッサを持つことができます。|
|*仮想化サービス クライアント (VSC)*|リソースまたはサービスを使用するゲストが読み込まれるソフトウェア モジュールです。 I/O デバイスの場合は、仮想化サービスのクライアントは、オペレーティング システムのカーネルが読み込まれるデバイス ドライバーを指定できます。|
| *仮想化サービス プロバイダー (VSP)*|  ルート パーティション内の仮想化スタックによって公開されているプロバイダーをリソースまたは子パーティションに I/O などのサービスを提供します。|
| *仮想化スタック*|ルート パーティション内の仮想マシンをサポートするために連携するソフトウェア コンポーネントのコレクション。 仮想化スタックでは、連携して、ハイパーバイザー上に位置します。 また、管理機能も提供します。|
|*VMBus*|システムで複数のアクティブな仮想化されたパーティションのパーティション内の通信およびデバイス列挙のために使用されるチャネル ベースの通信メカニズム。 VMBus は、Hyper-V 統合サービスと共にインストールされます。|

## <a name="see-also"></a>関連項目

-   [HYPER-V のアーキテクチャ](architecture.md)

-   [HYPER-V サーバーの構成](configuration.md)

-   [HYPER-V のプロセッサのパフォーマンス](processor-performance.md)

-   [HYPER-V でメモリのパフォーマンス](memory-performance.md)

-   [HYPER-V ストレージの I/O パフォーマンス](storage-io-performance.md)

-   [HYPER-V ネットワークの I/O パフォーマンス](network-io-performance.md)

-   [仮想化環境のボトルネックの検出](detecting-virtualized-environment-bottlenecks.md)

-   [Linux 仮想マシン](linux-virtual-machine-considerations.md)
