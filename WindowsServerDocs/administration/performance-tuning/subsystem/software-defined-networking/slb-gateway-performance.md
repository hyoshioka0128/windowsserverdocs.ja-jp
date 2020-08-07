---
title: ソフトウェア定義ネットワークでの SLB ゲートウェイのパフォーマンスチューニング
description: SDN ネットワークに関する SLB ゲートウェイのパフォーマンスチューニングガイドライン
ms.topic: article
ms.author: grcusanz; anpaul
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 64d045a270b8762d0d269055c8c65d1e40a71d63
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87895937"
---
# <a name="slb-gateway-performance-tuning-in-software-defined-networks"></a>ソフトウェア定義ネットワークでの SLB ゲートウェイのパフォーマンスチューニング

ソフトウェア負荷分散は、ネットワークコントローラー Vm のロードバランサーマネージャー、Hyper-v 仮想スイッチ、および一連の Load Balancer Multixplexor (Mux) Vm の組み合わせによって提供されます。

以下で説明するように、ネットワークコントローラーまたは Hyper-v ホストの負荷分散を構成するために、追加のパフォーマンスチューニングは必要ありません。[このセクションで](index.md)は、次に説明するように、sr-iov に sr-iov を使用する場合を除きます。

## <a name="slb-mux-vm-configuration"></a>SLB Mux VM 構成

SLB Mux 仮想マシンは、アクティブ/アクティブ構成で展開されます。  これは、ネットワークコントローラーにデプロイされて追加されたすべての Mux VM が受信要求を処理できることを意味します。  このため、すべての接続の合計スループットは、デプロイした Mux Vm の数によってのみ制限されます。

仮想 IP (VIP) への個々の接続は、常に同じ Mux に送信されます。これは、muxes の数が一定のままであることを前提としています。その結果、スループットは単一の Mux VM のスループットに制限されます。  Muxes は、VIP 宛ての受信トラフィックのみを処理します。  応答パケットは、応答をクライアントに転送する物理スイッチに送信している VM から直接送られます。

場合によっては、要求のソースが、VIP を管理する同じネットワークコントローラーに追加された SDN ホストから送信された場合、要求の受信パスをさらに最適化することで、ほとんどのパケットをクライアントからサーバーに直接移動して、Mux VM 全体をバイパスすることができます。  この最適化を行うには、追加の構成は必要ありません。

各 SLB Mux VM のサイズは、「[ソフトウェア定義ネットワークインフラストラクチャの計画](../../../../networking/sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md)」トピックの「SDN インフラストラクチャ仮想マシンロールの要件」セクションに記載されているガイドラインに従って設定する必要があります。

## <a name="single-root-io-virtualization-sr-iov"></a>シングルルート IO 仮想化 (sr-iov)

40Gbit ビットイーサネットを使用する場合、Mux VM のパケットを処理する仮想スイッチの機能が、Mux VM のスループットの制限要因になります。  このため、仮想スイッチがボトルネックにならないように、SLB VM の VM ネットワークアダプターで sr-iov を有効にすることをお勧めします。

Sr-iov を有効にするには、仮想スイッチを作成するときに仮想スイッチで有効にする必要があります。  この例では、スイッチ埋め込みチーミング (SET) と SR-IOV を使用して仮想スイッチを作成します。
``` syntax
    new-vmswitch -Name SDNSwitch -EnableEmbeddedTeaming $true -NetAdapterName @("NIC1", "NIC2") -EnableIOV $true
```
次に、データトラフィックを処理する SLB Mux VM の仮想ネットワークアダプターで有効にする必要があります。  この例では、すべてのアダプターで sr-iov が有効になっています。
``` syntax
    get-vmnetworkadapter -VMName SLBMUX1 | set-vmnetworkadapter -IovWeight 50
```
