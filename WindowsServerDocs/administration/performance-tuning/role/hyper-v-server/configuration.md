---
title: Hyper-V の構成
description: パフォーマンス チューニングの HYPER-V の構成に関する考慮事項
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Asmahi; SandySp; JoPoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: baea091482818c581414ba1d9c1c01db2a52e3d7
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66435665"
---
# <a name="hyper-v-configuration"></a>Hyper-V の構成

## <a name="hardware-selection"></a>ハードウェアの選択

一般に、HYPER-V を実行しているサーバーのハードウェアの考慮事項では、サーバーの非仮想化のと似ていますが、HYPER-V を実行しているサーバーは、CPU 使用率の増加を示すより多くのメモリを消費する、およびサーバーの統合のため I/O 帯域幅が大きい必要があります。

-   **プロセッサ**

    Windows Server 2016 では、HYPER-V では、アクティブな各仮想マシンに 1 つまたは複数の仮想プロセッサと論理プロセッサを表示します。 HYPER-V には、Extended Page テーブル (EPT) や Nested Page テーブル (NPT) などの Second Level Address Translation (SLAT) テクノロジをサポートするプロセッサが必要になりました。

-   **Cache**

    HYPER-V は、特に大規模な作業メモリと仮想プロセッサと論理プロセッサの比率が高にする仮想マシンの構成設定の読み込みの場合、サイズの大きいプロセッサのキャッシュを利用できます。

-   **メモリ**

    物理サーバーでは、ルートと子の両方のパーティションのための十分なメモリが必要です。 ルート パーティションには、仮想マシンと仮想マシンのスナップショットなどの操作のための I/o を効率的に実行するためのメモリが必要です。 HYPER-V により、十分なメモリが、ルート パーティションがあるし、子パーティションに割り当てられるメモリの残りことができます。 子パーティションは、各仮想マシンの予想される負荷ニーズに基づいてサイズ設定する必要があります。

-   **ストレージ**

    記憶域ハードウェアは十分な I/O 帯域幅が必要し、する容量、現在および将来のニーズに合わせて仮想マシン、物理サーバーのホスト。 記憶域コント ローラーとディスクを選択して、RAID の構成を選択すると、これらの要件を検討してください。 別の物理ディスクへの高度なディスクが集中するワークロードを持つ仮想マシンの配置しても、全体的なパフォーマンスは向上可能性があります。 たとえば、4 つの仮想マシンが 1 つのディスクを共有して、積極的にそれを使用している場合、各仮想マシンはそのディスクの帯域幅の 25% のみを生成できます。

## <a name="power-plan-considerations"></a>電源プランに関する考慮事項

コア テクノロジとしては、仮想化は、サーバー ワークロード密度の向上、データ センターで必要な物理サーバーの数を減らす、運用効率の向上および電力消費コストを削減に役立つ強力なツールです。 電源管理は、cost management の重要です。 

理想的なデータ センター環境では、電力消費量がビジー状態でいるほとんどの場合、まで、マシン上に作業を統合して、アイドル状態のマシンをオフによって管理されます。 このアプローチが実用的でない場合、管理者は、必要に応じてより多くの電力を消費しないようにする物理ホストの電源プランを利用できます。 

サーバーの電源管理の手法が付属してコストをテナントとして特にワークロードが、ホスト側の物理インフラストラクチャについてポリシーを音声入力に信頼されていません。 ホスト レイヤー ソフトウェアは、電力消費量を最小限に抑えながらスループットを最大化する方法を推測するままです。 ほとんどの場合、アイドル状態のマシンでその、中程度の電力の消費が適切であるそれ以外の場合より遅く実行されている個々 のテナントのワークロードで結果を完了するまでに物理インフラストラクチャができます。

Windows Server では、さまざまなシナリオで仮想化を使用します。 比較的ビジー状態の SQL サーバーに負荷が低い IIS サーバーから Hyper-v を使用したクラウドのホストに何百ものサーバーごとの仮想マシンを実行します。 これらの各シナリオには、一意のハードウェア、ソフトウェア、およびパフォーマンスの要件があります。 既定値や Windows Server の使用をお勧めしますが、**バランス**CPU 使用率に基づいて、プロセッサのパフォーマンスのスケーリングにより、電源の節約する電源プラン。

**バランス**電源プラン、電源状態の最も高い (およびテナントのワークロードの最下位の応答待機時間) を物理ホストが比較的ビジー状態のときにのみ適用されます。 すべてのテナントのワークロードの決定論的、低待機時間の応答を重視する場合は、既定値からの切り替えを検討してください**バランス**電源プラン、**高性能**電源プラン。 **高性能**電源プラン実行プロセッサ最高速度ですべての時間とその他の電源管理手法では、要求ベースの切り替えが無効にされ省電力経由でパフォーマンスを最適化します。

お客様は、物理サーバーの数を減らすことによるコスト削減に問題がなければの仮想化されたワークロードに対する最大のパフォーマンスを達成することを確認する、ユーザーを使用してを考慮する必要があります、**高性能**電源プラン。

追加の推奨事項と、インフラストラクチャを最適化するために電源プランの利用に関する分析情報では、「[推奨分散電源プラン パラメーター クイックの応答時間](../../hardware/power/recommended-balanced-plan-parameters.md)



## <a name="server-core-installation-option"></a>Server Core インストール オプション

Windows Server 2016 の機能を Server Core インストール オプションです。 Server Core では、選択された一連の HYPER-V を含むサーバーの役割をホストするための最低限の環境を提供します。 ホスト OS では、ディスク フット プリントより小さいと小さく攻撃と画面をサービス機能があります。 そのため、HYPER-V 仮想化サーバーが Server Core インストール オプションを使用することを強くお勧めします。

Server Core インストールは、ユーザーがログオンしますが、HYPER-V などのリモート管理機能を公開する場合にだけ、コンソール ウィンドウを提供[Windows Powershell](https://technet.microsoft.com/library/hh848559.aspx)管理者がリモートで管理できるようにします。

## <a name="dedicated-server-role"></a>専用のサーバーの役割

ルート パーティションは、HYPER-V の専用必要があります。 追加のサーバーの役割を HYPER-V を実行しているサーバーで実行されていることができますパフォーマンスが低下、仮想化サーバーの CPU、メモリ、または I/O 帯域幅が大幅に消費する場合に特にです。 ルート パーティションでサーバーの役割を最小限に抑えるには、攻撃対象領域の削減などの他の特典があります。

システム管理者は、ルート パーティションにどのようなソフトウェアがインストールされているソフトウェアによって悪影響を与える、HYPER-V を実行しているサーバーの全体的なパフォーマンスに影響を与えるため、慎重に検討する必要があります。

## <a name="guest-operating-systems"></a>ゲスト オペレーティング システム

HYPER-V をサポートし、さまざまなさまざまなゲスト オペレーティング システム用に調整されています。 ゲストごとにサポートされている仮想プロセッサの数は、ゲスト オペレーティング システムによって異なります。 サポートされているゲスト オペレーティング システムの一覧では、次を参照してください。 [Hyper-v 概要](https://technet.microsoft.com/library/hh831531.aspx)します。

## <a name="cpu-statistics"></a>CPU の統計情報

HYPER-V では、仮想化サーバーの動作の特徴やリソースの使用状況を報告するパフォーマンス カウンターを発行します。 表示でき、HYPER-V のパフォーマンス カウンターを記録するパフォーマンス モニターおよび Logman.exe、標準の Windows パフォーマンス カウンターを表示するためのツールのセットが含まれます。 関連するカウンター オブジェクトの名前が付いて**HYPER-V**します。

常に、HYPER-V ハイパーバイザーの論理プロセッサのパフォーマンス カウンターを使用して、物理システムの CPU 使用率を測定する必要があります。 CPU 使用率カウンター、ルートでそのタスク マネージャー、およびパフォーマンス モニターのレポートと、子パーティションでは、実際の物理 CPU 使用率が反映されていません。 パフォーマンスを監視するのにには、次のパフォーマンス カウンターを使用します。

- **HYPER-V ハイパーバイザーの論理プロセッサ (\*)\\合計実行時間の割合**論理プロセッサの合計の非アイドル時間

- **HYPER-V ハイパーバイザーの論理プロセッサ (\*)\\ゲストの実行時間の割合**ゲストまたはホスト内で実行中のサイクルにかかった時間

- **HYPER-V ハイパーバイザーの論理プロセッサ (\*)\\ハイパーバイザーの実行時間の割合**ハイパーバイザー内で実行中に費やした時間

- **HYPER-V ハイパーバイザーのルートの仮想プロセッサ (\*)\\\\** * ルート パーティションの CPU 使用率を測定します。

- **HYPER-V ハイパーバイザーの仮想プロセッサ (\*)\\\\** * ゲスト パーティションの CPU 使用率を測定します。


## <a name="see-also"></a>関連項目

-   [Hyper-V の用語](terminology.md)

-   [Hyper-V のアーキテクチャ](architecture.md)

-   [Hyper-V プロセッサのパフォーマンス](processor-performance.md)

-   [Hyper-V メモリのパフォーマンス](memory-performance.md)

-   [Hyper-V 記憶域の I/O のパフォーマンス](storage-io-performance.md)

-   [Hyper-V ネットワークの I/O のパフォーマンス](network-io-performance.md)

-   [仮想化環境のボトルネックの検出](detecting-virtualized-environment-bottlenecks.md)

-   [Linux 仮想マシン](linux-virtual-machine-considerations.md)
