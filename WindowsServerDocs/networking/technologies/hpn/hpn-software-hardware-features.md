---
title: ソフトウェアとハードウェア (SH) の統合された機能とテクノロジ
description: これらの機能には、ソフトウェアとハードウェアの両方のコンポーネントがあります。 ソフトウェアは密接機能を使用するために必要なハードウェア機能に関連付けられています。 これらの例には、VMMQ、VMQ、送信側 IPv4 チェックサム オフロード、および RSS が含まれます。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 0cafb1cc-5798-42f5-89b6-3ffe7ac024ba
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/12/2018
ms.openlocfilehash: a58d1e14dc8f543f25ef241f2a65054599136031
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817393"
---
# <a name="software-and-hardware-sh-integrated-features-and-technologies"></a>ソフトウェアとハードウェア (SH) の統合された機能とテクノロジ

これらの機能には、ソフトウェアとハードウェアの両方のコンポーネントがあります。 ソフトウェアは密接機能を使用するために必要なハードウェア機能に関連付けられています。 これらの例には、VMMQ、VMQ、送信側 IPv4 チェックサム オフロード、および RSS が含まれます。

>[!TIP]
>SH とホストの機能はインストールされている NIC がサポートされている場合に使用です。 次の機能の説明では、NIC がこの機能をサポートしているかを確認する方法を説明します。

## <a name="converged-nic"></a>収束の NIC 

収束の NIC は、RDMA サービス ホスト プロセスを公開する HYPER-V ホストの仮想 Nic をできるようにするテクノロジです。 Windows Server 2016 では、RDMA 用の個別の Nic が不要になったが必要です。 コンバージド NIC 機能では、ホストのパーティションに RDMA を公開および公正で管理しやすい方法で RDMA のトラフィックと、VM とその他の TCP または UDP トラフィックの間の Nic の帯域幅を共有するホスト パーティション (Vnic) の仮想 Nic ができます。

![Sdn の収束の NIC](../../media/Converged-NIC/conv-nic-sdn.png)

VMM または Windows PowerShell での収束の NIC 操作を管理することができます。 PowerShell コマンドレットでは、同じコマンドレット RDMA (下記参照) の使用を示します。

収束の NIC 機能を使用するには。

1.  DCB のためにホストを設定することを確認します。

2.  NIC で RDMA を有効にすることを確認するか、Nic がバインドされている場合は、セット チームを HYPER-V スイッチにします。 

3.  ホストで RDMA 用に指定された Vnic で RDMA を有効にすることを確認します。 

詳細については、RDMA、SET は、次を参照してください。[リモート ダイレクト メモリ アクセス (RDMA) とスイッチ埋め込みチーミング (SET)](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming)します。

## <a name="data-center-bridging-dcb"></a>データ センター ブリッジング (DCB) 

DCB は、一連の Institute of Electrical and Electronics Engineers (IEEE) 標準のデータ センターにおいてファブリックの集約を有効にします。 DCB は、隣接するスイッチからの協力を持つホストのハードウェア キュー ベースの帯域幅の管理を提供します。 記憶域のすべてのトラフィック、ネットワーク、プロセス間通信 (IPC) クラスター、管理共有データで同じイーサネット ネットワーク インフラストラクチャ。 Windows Server 2016 では、DCB は個別に任意の NIC に適用することができ、Hyper-v ホストにバインドされている Nic に切り替えます。

DCB には、Windows Server は優先度に基づくフロー制御 (PFC)、IEEE 802.1 qbb で標準化されたを使用します。 PFC は、トラフィック クラス内のオーバーフローを防ぐことによって、ロスレス (ほぼ) ネットワーク ファブリックを作成します。 Windows Server では、Enhanced Transmission Selection (ETS)、IEEE 802.1 qaz で標準化も使用します。 ETS では、帯域幅のトラフィックの最大 8 つのクラスの予約済みの部分に分割できるようにします。 トラフィック クラスごとに独自の送信キュー、および PFC を使用することできますを起動し、クラス内での伝送を停止します。

詳細については、次を参照してください。[データ センター ブリッジング (DCB)](https://docs.microsoft.com/windows-server/networking/technologies/dcb/dcb-top)します。

## <a name="hyper-v-network-virtualization"></a>Hyper-V ネットワーク仮想化

| | |
|---|---|
| **v1 (HNVv1)**             | Windows Server 2012 で導入された、HYPER-V ネットワーク仮想化 (HNV) は、共有の物理ネットワーク インフラストラクチャ上に顧客のネットワーク仮想化を有効します。 物理ネットワーク ファブリックのために必要な最小限の変更、HNV により、サービス プロバイダーをデプロイし、3 つのクラウド間で任意の場所テナントのワークロードを移行する機敏性: サービス プロバイダーのクラウド、プライベート クラウド、または Microsoft Azure パブリック クラウド。                                         |
| **v2 NVGRE (HNVv2 NVGRE)** | Windows Server 2016 および System Center Virtual Machine Manager では、Microsoft は、RAS ゲートウェイ、ソフトウェアの負荷分散、ネットワーク コント ローラー、および詳細を含むエンド ツー エンドのネットワーク仮想化ソリューションを提供します。 詳細については、次を参照してください。 [Windows Server 2016 で Hyper-v ネットワーク仮想化の概要](https://technet.microsoft.com/windows-server-docs/networking/sdn/technologies/hyper-v-network-virtualization/hyperv-network-virtualization-overview-windows-server)します。 |
| **v2 VxLAN (HNVv2 VxLAN)** | Windows Server 2016 で、ネットワーク コント ローラーから管理する SDN-拡張の一部です。    |
---

## <a name="ipsec-task-offload-ipsecto"></a>IPsec タスク オフロード (IPsecTO) 

IPsec タスク オフロードは、IPsec の暗号化作業の NIC で、プロセッサを使用するオペレーティング システムを有効にする NIC 機能です。

>[!IMPORTANT] 
>ほとんどのネットワーク アダプターでサポートされていないレガシ テクノロジは、IPsec Task Offload し、存在して、既定で無効です。

## <a name="private-virtual-local-area-network-pvlan"></a>プライベート仮想ローカル エリア ネットワーク (PVLAN)。 

Pvlan は、同じ仮想化サーバー上の仮想マシン間でのみ通信を許可します。 プライベート仮想ネットワークは物理ネットワーク アダプターにバインドされません。 プライベート仮想ネットワークは、管理オペレーティング システムと外部ネットワーク間のネットワーク トラフィックと同様に、仮想化サーバー上のすべての外部ネットワーク トラフィックから分離されます。 この種類のネットワークは、隔離されたテスト ドメインなど、隔離されたネットワーク環境を構築する必要がある場合に役立ちます。 Hyper-v ホストと SDN スタックは、PVLAN 分離ポート モードのみをサポートします。

詳細については、PVLAN 分離は、次を参照してください[System Center:。Virtual Machine Manager エンジニア リング ブログ](https://blogs.technet.microsoft.com/scvmm/2013/06/04/logical-networks-part-iv-pvlan-isolation/)します。

## <a name="remote-direct-memory-access-rdma"></a>リモート ダイレクト メモリ アクセス (RDMA) 

RDMA は、CPU 使用率を最小限に抑え、高スループット、低待機時間の通信を提供するネットワーク テクノロジです。 RDMA は、アプリケーション メモリに直接データを転送するネットワーク アダプターを有効にするとコピーなしのネットワークをサポートします。 Rdma 対応 NIC (物理または仮想) を RDMA を RDMA クライアントに公開することを意味します。 Rdma 対応の NIC がスタックを RDMA インターフェイスを公開することを意味その一方で、RDMA 対応します。

RDMA の詳細については、次を参照してください。[リモート ダイレクト メモリ アクセス (RDMA) とスイッチ埋め込みチーミング (SET)](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming)します。

## <a name="receive-side-scaling-rss"></a>Receive Side Scaling (RSS) 

RSS は、異なるストリームのセットを分離し、処理のための別のプロセッサに配信する NIC 機能です。 RSS は、処理、非常に高いデータ レートを拡張するホストを有効にすると、ネットワークを並列化します。 

詳細については、次を参照してください。 [Receive Side Scaling (RSS)](https://docs.microsoft.com/windows-hardware/drivers/network/introduction-to-receive-side-scaling)します。

## <a name="single-root-input-output-virtualization-sr-iov"></a>単一ルート入出力仮想化 (SR-IOV) 

SR-IOV は、HYPER-V ホストを経由せず、NIC から直接 VM に移動する VM のトラフィックを許可します。 SR-IOV は VM のパフォーマンスが大幅に向上が、そのパイプを管理するホストの機能が不足しています。 SR-IOV 対応のワークロードが信頼されている、適切に動作している場合と通常の唯一の VM をホストでのみ使用します。

SR-IOV を使用したトラフィック、HYPER-V がスイッチをバイパス、つまりすべてのポリシーでは、たとえば、Acl、または帯域幅管理は適用されません。 SR-IOV トラフィックを NV GRE または VxLAN カプセル化を適用することはできませんのでも、すべてのネットワーク仮想化の機能を介して渡されることはできません。 のみの特定の状況で適切に信頼されているワークロード、SR-IOV を使用します。 さらに、ホスト ポリシー、帯域幅管理、および仮想化テクノロジを使用することはできません。

今後は、2 つのテクノロジには、SR-IOV は許可します。一般的なフロー テーブル (GFT) とハードウェア QoS オフロード (NIC での帯域幅管理) – エコシステム内の Nic をサポートするいるとします。 これら 2 つのテクノロジの組み合わせは、ポリシー、仮想化、および適用するには、帯域幅管理規則は、SR-IOV 対応のすべての Vm の場合に便利で、でした優れた飛躍的に前進であると、一般的な SR-IOV 対応のアプリケーション。

詳細については、次を参照してください。[概要の Single Root I/O Virtualization (SR-IOV)](https://docs.microsoft.com/windows-hardware/drivers/network/overview-of-single-root-i-o-virtualization--sr-iov-)します。

## <a name="tcp-chimney-offload"></a>TCP Chimney オフロード

すべての TCP が NIC に処理をオフロードするホストをできるようにするテクノロジは、TCP Chimney オフロードとも呼ばれる TCP エンジン オフロード (TOE)、します。 Windows Server の TCP スタックは、ほとんどの場合は複数あるため、TOE エンジンよりも効率的で TCP Chimney オフロードの使用は推奨されません。

>[!IMPORTANT]
>TCP Chimney オフロードは、非推奨のテクノロジです。 使用しない TCP Chimney オフロードと Microsoft が、今後のサポートを停止する可能性がありますをお勧めします。

## <a name="virtual-local-area-network-vlan"></a>仮想ローカル エリア ネットワーク (VLAN) 

VLAN では、有効にする複数の Vlan に分割して、LAN、独自のアドレス空間を使用して各イーサネット フレーム ヘッダーの拡張機能です。 Windows Server 2016 では、Vlan、またはチームの NIC チーミングにチームのインターフェイスを設定して、HYPER-V スイッチのポートで設定します。 詳細については、次を参照してください。 [NIC チーミングおよび仮想ローカル エリア ネットワーク (Vlan)](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nict-and-vlans)します。

## <a name="virtual-machine-queue-vmq"></a>仮想マシン キュー (VMQ) 

VMQs は、VM ごとに、キューによって割り当てられる NIC 機能です。 いつでも、HYPER-V が有効になっている; があります。また、VMQ を有効にする必要があります。 Windows Server 2016 では、VMQs は、同じ機能を提供するのに NIC のスイッチ拡張を vPort に割り当てられている 1 つのキューを使用します。 詳細については、次を参照してください。[仮想 Receive Side Scaling (vRSS)](https://docs.microsoft.com/windows-server/networking/technologies/vrss/vrss-top)と[NIC チーミング](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming)します。

## <a name="virtual-machine-multi-queue-vmmq"></a>仮想マシンの複数のキュー (VMMQ) 

VMMQ は、それぞれ別の物理プロセッサによって処理される複数のキューを分散する VM のトラフィックを許可する NIC 機能です。 トラフィックは、vRSS で、VM に大量のネットワーク帯域幅を提供するためであるかのようにし、VM で複数の LPs に渡されます。

---