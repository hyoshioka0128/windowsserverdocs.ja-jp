---
title: RAS ゲートウェイ GRE トンネルのスループットとパフォーマンス
description: このトピックでは、情報テクノロジ (IT) プロフェッショナルを対象には、RAS ゲートウェイ Generic Routing Encapsulation (GRE) トンネルのスループット パフォーマンスに関する情報を提供します。
manager: brianlic
ms.prod: windows-server-threshold
ms.date: ''
ms.technology: networking-ras
ms.topic: article
ms.assetid: c051b2ec-de0f-49d1-82b9-5742b259cd7c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 73ae4e573d926f4a77b076c880c1d74ed69f032d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880763"
---
# <a name="ras-gateway-gre-tunnel-throughput-and-performance"></a>RAS ゲートウェイ GRE トンネルのスループットとパフォーマンス

>適用対象:Windows Server\(半期チャネル\)

このトピックを使用するには、リモート アクセス サーバーの詳細について\(RAS\)ゲートウェイの Generic Routing Encapsulation \(GRE\)トンネルで Windows Server バージョン 1709 で、以外のソフトウェアによるネットワーク制御パフォーマンス\(SDN\)ベースのテスト環境です。

RAS ゲートウェイは、ソフトウェア ルーターとシングル テナント モードまたはマルチ テナント モードのいずれかで使用できるゲートウェイです。 このトピックでは、シングル テナント モード、フェールオーバー クラスタ リングと高可用性構成について説明します。 このトピックで説明されている GRE トンネルのパフォーマンスの統計情報は、RAS ゲートウェイ singele テナントとマルチ テナント モードの両方で有効です。

>[!NOTE]
>フェールオーバー クラスタ リングとは、フォールト トレラント クラスターに複数のサーバーをグループ化することができます、Windows Server 機能です。 詳細については、次を参照してください[フェールオーバー クラスタ リング。](../../../failover-clustering/failover-clustering-overview.md)

シングル テナント モードで、外部またはインターネットとして、ゲートウェイを展開するには、あらゆる規模の組織は、\-edge の仮想プライベート ネットワークに接続する\(VPN\)サーバー。 シングル テナント モードでは、物理サーバーまたは仮想マシンで RAS ゲートウェイを展開できます\(VM\)します。 このトピックでは、2 つの仮想マシンで RAS ゲートウェイの展開をについて説明します\(Vm\)フェールオーバー クラスターで構成されています。

>[!IMPORTANT]
>GRE トンネルでは、カプセル化がない暗号化を提供するためには、RAS ゲートウェイとインターネットのエッジ ゲートウェイ GRE を使用しないでください。 GRE トンネルを使用した RAS ゲートウェイの最適な使用方法の詳細について、次を参照してください。 [Windows Server の GRE トンネリング](gre-tunneling-windows-server.md)します。

GRE は軽量のトンネリング プロトコルのさまざまな仮想ポイントの内部ネットワーク層プロトコルをカプセル化できる\-に\-インターネット プロトコル インターネットワーク上のリンクをポイントします。 Microsoft GRE 実装には、IPv4 と IPv6 の両方がカプセル化します。

詳細については、セクションをご覧ください。 **RAS ゲートウェイの展開シナリオ**、トピックの「 [RAS ゲートウェイ](https://docs.microsoft.com/windows-server/remote/remote-access/ras-gateway/ras-gateway#bkmk_deploy)します。 

測定されるトラフィック フローは、次の図に示されているように、このテスト シナリオで、組織のイントラネット 1 を組織のイントラネットの 2 から移動します。 テナントのワークロード Vm は、RAS ゲートウェイを使用してイントラネット 1 にイントラネット 2 からのネットワーク トラフィックを送信します。

![RAS ゲートウェイ GRE トンネルのテスト シナリオの概要](../../media/GRE-Tunnel-Perf/Gre-Infrastructure.jpg)

## <a name="test-environment-configuration"></a>テスト環境の構成

このセクションでは、テスト環境と RAS ゲートウェイの構成に関する情報を提供します。

ハイパースレッディングにテスト環境で RAS ゲートウェイの Vm が展開されている\-V ホスト フェールオーバー クラスターの高可用性を実現します。

### <a name="hyper-v-host-configuration"></a>ハイパー\-V ホストの構成

2 つのハイパースレッディング\-V ホストは、次のように、テスト シナリオをサポートするために構成されます。 

- 2 つのデュアル\-ホームの物理コンピューターが Windows Server バージョン 1709 で構成されています
- 2 つのサーバーごとの 2 つの物理ネットワーク アダプターは、組織のイントラネットのサブネットを表すいずれ - 別のサブネットワークに接続されます。 ネットワークとハードウェアのサポートの両方の 10 GBps の容量があります。
- 物理サーバーでハイパー スレッディングは無効です。 これは、物理的な Nic から最大のスループットを提供します。
- Hyper\-サーバーの役割が両方のサーバーにインストールされているし、2 つのハイパー外部で構成されている\-V 仮想スイッチの物理ネットワーク アダプターごとに 1 つ。
- 両方のサーバーは同じイントラネットに接続されている、ために、サーバーが互いと通信できます。
- Hyper\-V ホストは、イントラネット ネットワーク経由でフェールオーバー クラスターで構成されます。 

>[!NOTE]
>詳しくは、「[Hyper-V 仮想スイッチの概要](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/hyper-v-virtual-switch)」を参照してください。

### <a name="vm-configuration"></a>VM の構成

2 つの Vm は、次のように、テスト シナリオをサポートするために構成されます。

- VM があるインストールされている各サーバーでは、Windows Server バージョン 1709 を実行しています。 各 VM は、10 個のコアと 8 GB の RAM で構成されます。
- 各 VM を 2 つの仮想ネットワーク アダプターも構成します。 1 つの仮想ネットワーク アダプターが、イントラネット 1 仮想スイッチに接続されているし、その他の仮想ネットワーク アダプターが、イントラネットの 2 の仮想スイッチに接続されています。
- 各 VM にインストールされているし、GRE として構成されている、RAS ゲートウェイ\-ベースの VPN サーバー。
- ゲートウェイ Vm は、フェールオーバー クラスターで構成されます。 1 つの VM がアクティブなクラスター化されている場合と、もう一方の VM はパッシブです。

### <a name="workload-hyper-v-hosts-and-vms"></a>ワークロードのハイパー\-V ホストと Vm

このテストは、2 つのワークロードがハイパー\-V ホストは、イントラネットにインストールされており、各ホストがインストールされている 1 つの VM。 テスト環境でこのテストを複製する場合は、多くのワークロードのサーバーとは、目的に応じて適切な Vm をインストールできます。

- ワークロードのハイパースレッディング\-V ホストがある 1 つはインストールされている物理ネットワーク アダプターが組織のイントラネットに接続します。
- ハイパースレッディングで\-V 仮想スイッチ仮想スイッチは 1 つは各ホストに作成されます。 スイッチは、外部し、は、イントラネットに接続されている 1 つのネットワーク アダプターにバインドします。
- ワークロード Vm は、2 GB の RAM と 2 つのコアで構成されます。
- ワークロード Vm は、イントラネットの仮想スイッチに接続されている 1 つの仮想ネットワーク アダプターがあります。

### <a name="traffic-generator-tool"></a>トラフィック ジェネレーター ツール

このテストで使用されているトラフィック ジェネレーター ツールは、ctsTraffic ツールです。 このツールの Git リポジトリは[ https://github.com/Microsoft/ctsTraffic](https://github.com/Microsoft/ctsTraffic)します。

## <a name="ras-gateway-performance"></a>RAS ゲートウェイのパフォーマンス

このセクションの図は、複数の TCP 接続を GRE トンネルのスループットのタスク マネージャーの表示を示しています。

マルチで最大 2.0 Gbps のスループットを実現する\-GRE RAS ゲートウェイとして構成されている Vm のコアします。

### <a name="gre-tunnel-performance-with-multiple-tcp-sessions"></a>複数の TCP セッションを GRE トンネルのパフォーマンス

複数の TCP セッションでの CPU 使用率が 100% に達するし、GRE トンネルの最大スループットは 2.0 Gbps です。

次の図は、RAS ゲートウェイの Vm の両方で CPU 使用率を示しています。 RAS ゲートウェイの VM と 1 で、アクティブな VM は、左側のパッシブの VM では、RAS ゲートウェイの VM と 2 は右側です。

![ゲートウェイ VM の CPU 使用率でタスク マネージャー](../../media/GRE-Tunnel-Perf/Gre-Tunnel-01.jpg)

次の図は、RAS ゲートウェイの Vm のイーサネット ネットワーク スループットを示しています。 RAS ゲートウェイの VM と 1 で、アクティブな VM は、左側のパッシブの VM では、RAS ゲートウェイの VM と 2 は右側です。

![ゲートウェイ VM のイーサネット ネットワークのスループットでタスク マネージャー](../../media/GRE-Tunnel-Perf/Gre-Tunnel-02.jpg)


### <a name="gre-tunnel-performance-with-one-tcp-connection"></a>1 つの TCP 接続で GRE トンネルのパフォーマンス

複数の TCP セッションから 1 つの TCP セッションに変更するテスト構成では、1 つだけの CPU コア、RAS ゲートウェイの Vm で最大の容量に達した場合。

GRE トンネルの最大のスループットは 400 ~ 500 Mbps の範囲です。

次の図は、RAS ゲートウェイの Vm の両方で CPU 使用率を示しています。 RAS ゲートウェイの VM と 1 で、アクティブな VM は、左側のパッシブの VM では、RAS ゲートウェイの VM と 2 は右側です。

![ゲートウェイ VM の CPU 使用率でタスク マネージャー](../../media/GRE-Tunnel-Perf/Gre-Tunnel-03.jpg)


次の図は、RAS ゲートウェイの Vm のイーサネット ネットワーク スループットを示しています。 RAS ゲートウェイの VM と 1 で、アクティブな VM は、左側のパッシブの VM では、RAS ゲートウェイの VM と 2 は右側です。

![ゲートウェイ VM のイーサネット ネットワークのスループットでタスク マネージャー](../../media/GRE-Tunnel-Perf/Gre-Tunnel-04.jpg)

RAS ゲートウェイのパフォーマンスの詳細については、次を参照してください。[ソフトウェア定義ネットワークのゲートウェイのパフォーマンスのチューニングを HNV](https://docs.microsoft.com/windows-server/administration/performance-tuning/subsystem/software-defined-networking/hnv-gateway-performance)します。