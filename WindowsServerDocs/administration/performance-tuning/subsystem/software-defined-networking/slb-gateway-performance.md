---
title: SLB ゲートウェイでのパフォーマンス チューニング ソフトウェア定義ネットワーク
description: SLB のゲートウェイのパフォーマンス チューニング SDN ネットワーク上のガイドライン
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: grcusanz; AnPaul
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: fede7d404ddbb4f465eff435cc340db1907ce9d2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829933"
---
# <a name="slb-gateway-performance-tuning-in-software-defined-networks"></a>SLB ゲートウェイでのパフォーマンス チューニング ソフトウェア定義ネットワーク

ソフトウェアの負荷分散は、ネットワーク コント ローラーの Vm、HYPER-V 仮想スイッチおよび一連のロード バランサー Multixplexor (マルチプレクサー) Vm でのロード バランサー マネージャーの組み合わせによって提供されます。

ネットワーク コント ローラーを構成する追加のパフォーマンス チューニングは必要ありませんまたは負荷分散機能、HYPER-V ホストでの説明、[ソフトウェアによるネットワーク制御](index.md)セクションの SR-IOV を使用していない限り、以下に示すように Muxes します。

## <a name="slb-mux-vm-configuration"></a>SLB Mux VM の構成

SLB Mux 仮想マシンは、アクティブ/アクティブ構成で展開されます。  つまり、展開され、ネットワーク コント ローラーに追加されるすべての Mux VM が受信要求を処理できます。  したがって、すべての接続の合計の総スループットは、デプロイした Mux Vm の数によってのみ制限されます。  

個々 の接続に仮想 IP (VIP) は常に送信されます、同じのマルチプレクサーを muxes の数は一定のまま、その結果、スループットは 1 つの Mux VM のスループットに制限されますと想定しています。  Mux は、VIP 宛ての受信トラフィックを処理するだけです。  応答パケットは、クライアントに転送しますが、物理スイッチへの応答を送信している VM から直接移動します。

場合によっては、VIP を管理するのと同じネットワーク コント ローラーに追加されている SDN ホストからの要求のソースが計算されたときにさらに最適化、要求の受信パスのもが実行されるほとんどのパケットがから直接移動できるように、Mux VM を完全にバイパスして、サーバーにクライアント。  追加の構成は、この最適化を行うために必要ではありません。

SDN インフラストラクチャ仮想マシン ロールの要件セクションで説明するガイドラインに従って各 SLB Mux VM のサイズを変更する必要があります、[ソフトウェア定義ネットワーク インフラストラクチャを計画](../../../../networking/sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md)トピック。

## <a name="single-root-io-virtualization-sr-iov"></a>単一ルート入出力仮想化 (SR-IOV)

40 ギガ ビット イーサネットを使用して、Mux VM のパケットを処理する仮想スイッチの機能が Mux VM のスループットの制限要因になります。  このため、仮想スイッチがボトルネックでないことを確認して、SLB VM の VM ネットワーク アダプターの SR-IOV を有効にするをお勧めします。

SR-IOV を有効にするには、必要があります有効にする仮想スイッチ、仮想スイッチの作成時にします。  この例では、スイッチ埋め込みチーミング (SET)、SR-IOV と、仮想スイッチを作成します。
``` syntax
    new-vmswitch -Name SDNSwitch -EnableEmbeddedTeaming $true -NetAdapterName @("NIC1", "NIC2") -EnableIOV $true
```
次に、データのトラフィックを処理するは SLB Mux VM の仮想ネットワーク アダプターで有効にする必要があります。  この例には、すべてのアダプターで SR-IOV を有効にされないは。
``` syntax
    get-vmnetworkadapter -VMName SLBMUX1 | set-vmnetworkadapter -IovWeight 50
```
