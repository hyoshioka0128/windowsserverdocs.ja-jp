---
title: Windows Server 2016 での Hyper-v ネットワーク仮想化の新機能
description: このトピックでは、Windows Server 2016 での Hyper-v ネットワーク仮想化の新機能について説明します。
manager: grcusanz
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 0254275a-0a77-40a9-b68a-1029284c03fe
ms.author: anpaul
author: AnirbanPaul
ms.date: 03/19/2018
ms.openlocfilehash: 6178ca0913ef27f656a566ffdb39a957ab743733
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85471707"
---
# <a name="whats-new-in-hyper-v-network-virtualization-in-windows-server-2016"></a>Windows Server 2016 での Hyper-v ネットワーク仮想化の新機能

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、Windows Server 2016 で新しく追加または変更された Hyper-v ネットワーク仮想化 (HNV) の機能について説明します。

## <a name="updates-in-hnv"></a><a name="BKMK_IPAM2012R2"></a>HNV の更新プログラム
HNV は、次の領域で拡張サポートを提供します。

|機能|新機能か強化された機能か|説明|
|--------------------------|-------------------|---------------|
|[プログラミング可能な Hyper-v スイッチ](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#SDN)|新規|HNV ポリシーは、Microsoft ネットワークコントローラーを介してプログラミングできます。|
|[VXLAN のカプセル化のサポート](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#VXLAN)|新規|HNV で VXLAN カプセル化がサポートされるようになりました。|
|[ソフトウェア Load Balancer (SLB) の相互運用性](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#SLB)|新規|HNV は、Microsoft ソフトウェア Load Balancer と完全に統合されています。|
|[準拠している IEEE イーサネットヘッダー](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#L2)|強化しました|IEEE イーサネット標準に準拠|

### <a name="programmable-hyper-v-switch"></a><a name="SDN"></a>プログラミング可能な Hyper-v スイッチ
HNV は、Microsoft が更新したソフトウェアによるネットワーク制御 (SDN) ソリューションの基本的な構成要素であり、SDN スタックに完全に統合されています。

Microsoft の新しいネットワークコントローラーは、SouthBound インターフェイス (SBI) として Open vSwitch Database Management Protocol (Interface) を使用して、各ホストで実行されているホストエージェントに HNV ポリシーをプッシュします。 ホストエージェントは、 [Vtep スキーマ](https://github.com/openvswitch/ovs/blob/master/vtep/vtep.ovsschema)のカスタマイズを使用してこのポリシーを保存し、複雑なフロールールを hyper-v スイッチのパフォーマンスの高いフローエンジンにプログラムします。

Hyper-v スイッチ内のフローエンジンは Microsoft Azure で使用されるのと同じエンジンであり、 &trade; Microsoft Azure パブリッククラウドのハイパースケールで実証されています。 さらに、ネットワークコントローラー全体の SDN スタックとネットワークリソースプロバイダー (近日公開予定) は Microsoft Azure と一貫性があるため、Microsoft Azure パブリッククラウドの能力をエンタープライズおよびホスティングサービスプロバイダーのお客様に提供します。

> [!NOTE]
> 詳細については、「 [RFC 7047](https://www.rfc-editor.org/info/rfc7047)」を参照してください。

Hyper-v スイッチでは、Microsoft のフローエンジン内の単純な ' match action ' に基づくステートレスおよびステートフルフロールールの両方がサポートされています。

![Windows Server 2016 Hyper-v スイッチ](../../../media/what-s-new-in-hyper-v-network-virtualization-in-windows-server/HNVOverview.png)

### <a name="vxlan-encapsulation-support"></a><a name="VXLAN"></a>VXLAN のカプセル化のサポート
仮想拡張可能なローカルエリアネットワーク (VXLAN- [RFC 7348](https://www.rfc-editor.org/info/rfc7348)) プロトコルは、Cisco、Brocade、DELL、HP などのベンダーからのサポートを通じて、マーケットプレースで広く採用されています。 また、HNV は、Microsoft ネットワークコントローラーを介した MAC 配布モードを使用したこのカプセル化スキームをサポートし、テナントオーバーレイネットワーク IP アドレス (カスタマーアドレス、または CA) と物理アンダーレイネットワーク IP アドレス (プロバイダーアドレス、または PA) とのマッピングをプログラミングできるようになりました。 NVGRE と VXLAN タスクのオフロードは両方とも、サードパーティのドライバーによるパフォーマンスの向上のためにサポートされています。

### <a name="software-load-balancer-slb-interoperability"></a><a name="SLB"></a>ソフトウェア Load Balancer (SLB) の相互運用性
Windows Server 2016 には、仮想ネットワークトラフィックを完全にサポートするソフトウェアロードバランサー (SLB) と HNV とのシームレスな対話機能が含まれています。 SLB は、data plane v スイッチのパフォーマンスの高いフローエンジンによって実装され、仮想 IP (VIP)/動的 IP (DIP) のマッピングのためにネットワークコントローラーによって制御されます。

### <a name="compliant-ieee-ethernet-headers"></a><a name="L2"></a>準拠している IEEE イーサネットヘッダー
HNV は、業界標準のプロトコルに依存するサードパーティの仮想および物理アプライアンスとの相互運用性を確保するために、正しい L2 イーサネットヘッダーを実装します。 Microsoft では、この相互運用性を確保するために、すべての送信パケットに準拠した値があることを保証します。 さらに、物理 L2 ネットワークでのジャンボフレーム (MTU > 1780) のサポートは、nVirtual Network NV に接続されているゲスト Virtual Machines が 1514 MTU を維持していることを確認するために、カプセル化プロトコル (NVGRE、VXLAN) によって導入されたパケットオーバーヘッドを考慮する必要があります。

## <a name="additional-references"></a>その他のリファレンス

-   [Hyper-V ネットワーク仮想化の概要](hyperv-network-virtualization-overview-windows-server.md)

-   [Hyper-V ネットワーク仮想化の技術的な詳細](hyperv-network-virtualization-technical-details-windows-server.md)

-   [ソフトウェアによるネットワーク](../../Software-Defined-Networking--SDN-.md)
