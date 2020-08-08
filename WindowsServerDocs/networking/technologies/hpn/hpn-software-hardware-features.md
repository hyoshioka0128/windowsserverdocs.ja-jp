---
title: ソフトウェアとハードウェア (SH) の統合された機能とテクノロジ
description: これらの機能には、ソフトウェアとハードウェアの両方のコンポーネントがあります。 このソフトウェアは、この機能が動作するために必要なハードウェア機能に深くされています。 これらの例には、VMMQ、VMQ、送信側 IPv4 チェックサムオフロード、RSS などがあります。
ms.topic: article
ms.assetid: 0cafb1cc-5798-42f5-89b6-3ffe7ac024ba
manager: dougkim
ms.author: lizross
author: eross-msft
ms.date: 09/12/2018
ms.openlocfilehash: 3c1b414acaf7487b0a435cfea2891903646c869f
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87995267"
---
# <a name="software-and-hardware-sh-integrated-features-and-technologies"></a>ソフトウェアとハードウェア (SH) の統合された機能とテクノロジ

これらの機能には、ソフトウェアとハードウェアの両方のコンポーネントがあります。 このソフトウェアは、この機能が動作するために必要なハードウェア機能に深くされています。 これらの例には、VMMQ、VMQ、送信側 IPv4 チェックサムオフロード、RSS などがあります。

>[!TIP]
>インストールされている NIC でサポートされている場合は、SH およびホー機能を使用できます。 以下の機能の説明では、NIC が機能をサポートしているかどうかを確認する方法について説明します。

## <a name="converged-nic"></a>収束済み NIC

収束 NIC は、Hyper-v ホストの仮想 Nic が RDMA サービスをホストプロセスに公開できるようにするテクノロジです。 Windows Server 2016 では、RDMA 用に個別の Nic が必要なくなりました。 収束 NIC 機能を使用すると、ホストパーティション (vNICs) 内の仮想 Nic は、rdma をホストパーティションに公開し、RDMA トラフィックと VM 間の Nic の帯域幅とその他の TCP/UDP トラフィックを公平かつ管理しやすい方法で共有できます。

![SDN を使用した収束 NIC](../../media/Converged-NIC/conv-nic-sdn.png)

収束 NIC 操作は、VMM または Windows PowerShell を使用して管理できます。 PowerShell コマンドレットは、RDMA に使用されるコマンドレットと同じです (下記参照)。

収束 NIC 機能を使用するには、次のようにします。

1.  DCB のホストを設定するようにしてください。

2.  NIC で RDMA が有効になっていること、またはセットチームの場合は、Nic が Hyper-v スイッチにバインドされていることを確認します。

3.  ホストで RDMA 用に指定された vNICs で RDMA が有効になっていることを確認します。

RDMA と SET の詳細については、「[リモートダイレクトメモリアクセス (rdma)」および「スイッチ埋め込みチーミング (set)](../../../virtualization/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming.md)」を参照してください。

## <a name="data-center-bridging-dcb"></a>Data Center Bridging (DCB)

DCB は、データセンターでの集約型ファブリックを実現する米国国立の電気およびエレクトロニクスエンジニア (IEEE) 標準のスイートです。 DCB は、隣接するスイッチと連携して、ホストでハードウェアキューベースの帯域幅管理を提供します。 ストレージ、データネットワーク、クラスターのプロセス間通信 (IPC)、および管理のすべてのトラフィックは、同じイーサネットネットワークインフラストラクチャを共有します。 Windows Server 2016 では、DCB は、個々の NIC と、Hyper-v スイッチにバインドされている Nic に適用できます。

DCB の場合、Windows Server は、IEEE 802.1 Qbb で標準化された優先度ベースのフロー制御 (PFC) を使用します。 PFC は、トラフィッククラス内でオーバーフローを防ぐことによって、(ほぼ) ロスレスネットワークファブリックを作成します。 また、Windows Server では、IEEE 802.1 Qaz で標準化された高度な転送の選択 (送信) も使用します。 これにより、最大8つのクラスのトラフィックに対して、帯域幅を予約された部分に分割できるようになります。 各 traffic クラスには独自の送信キューがあり、PFC を使用することにより、クラス内での送信を開始および停止できます。

詳細については、「[データセンターブリッジング」 (DCB)](../dcb/dcb-top.md)を参照してください。

## <a name="hyper-v-network-virtualization"></a>Hyper-V ネットワーク仮想化

|                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **v1 (HNVv1)**       |                     Windows Server 2012 で導入された Hyper-v ネットワーク仮想化 (HNV) を使用すると、共有の物理ネットワークインフラストラクチャ上にある顧客ネットワークを仮想化することができます。 HNV では、物理ネットワークファブリックに必要な変更を最小限に抑えて、サービスプロバイダーは、サービスプロバイダークラウド、プライベートクラウド、または Microsoft Azure パブリッククラウドの3つのクラウド全体で、テナントのワークロードをデプロイおよび移行する機敏性を提供します。                     |
| **v2 NVGRE (HNVv2 NVGRE)** | Windows Server 2016 および System Center Virtual Machine Manager では、Microsoft は、RAS ゲートウェイ、ソフトウェアの負荷分散、ネットワークコントローラーなどを含むエンドツーエンドのネットワーク仮想化ソリューションを提供します。 詳細については、「 [Windows Server 2016 での Hyper-v ネットワーク仮想化の概要](../../sdn/technologies/hyper-v-network-virtualization/hyperv-network-virtualization-overview-windows-server.md)」を参照してください。 |
| **v2 VxLAN (HNVv2 VxLAN)** |                                                                                                                                                                                        Windows Server 2016 では、は、ネットワークコントローラーを介して管理する SDN 拡張機能の一部です。                                                                                                                                                                                        |

---

## <a name="ipsec-task-offload-ipsecto"></a>IPsec タスク オフロード (IPsecTO)

IPsec タスクオフロードは、オペレーティングシステムが NIC のプロセッサを IPsec 暗号化の処理に使用できるようにするための NIC 機能です。

>[!IMPORTANT]
>IPsec タスクオフロードは、ほとんどのネットワークアダプターではサポートされていない従来のテクノロジであり、存在する場合は既定で無効になっています。

## <a name="private-virtual-local-area-network-pvlan"></a>プライベート仮想ローカルエリアネットワーク (PVLAN)。

PVLANs では、同じ仮想化サーバー上の仮想マシン間でのみ通信を行うことができます。 プライベート仮想ネットワークは、物理ネットワークアダプターにバインドされていません。 プライベート仮想ネットワークは、仮想化サーバー上のすべての外部ネットワークトラフィックと、管理オペレーティングシステムと外部ネットワーク間のネットワークトラフィックから分離されます。 この種類のネットワークは、隔離されたテスト ドメインなど、隔離されたネットワーク環境を構築する必要がある場合に役立ちます。 Hyper-v および SDN スタックは、PVLAN 分離ポートモードのみをサポートしています。

PVLAN 分離の詳細については、「 [System Center: Virtual Machine Manager Engineering のブログ](https://blogs.technet.microsoft.com/scvmm/2013/06/04/logical-networks-part-iv-pvlan-isolation/)」を参照してください。

## <a name="remote-direct-memory-access-rdma"></a>リモート ダイレクト メモリ アクセス (RDMA)

RDMA は、CPU 使用率を最小限に抑える高スループットで低待機時間の通信を実現するネットワークテクノロジです。 RDMA は、ネットワークアダプターがアプリケーションメモリとの間でデータを直接転送できるようにすることで、ゼロコピーのネットワークをサポートします。 RDMA 対応とは、NIC (物理または仮想) が rdma クライアントに RDMA を公開できることを意味します。 一方、RDMA 対応の NIC では、rdma インターフェイスがスタック上に公開されています。

RDMA の詳細については、「[リモートダイレクトメモリアクセス (rdma) とスイッチ埋め込みチーミング (SET)](../../../virtualization/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming.md)」を参照してください。

## <a name="receive-side-scaling-rss"></a>Receive Side Scaling (RSS)

RSS は、さまざまなストリームのセットを分離、処理のために異なるプロセッサに配信する NIC 機能です。 RSS は、ネットワーク処理を並列化し、ホストが非常に高いデータ速度に拡張できるようにします。

詳細については、「 [Receive Side Scaling (RSS)](/windows-hardware/drivers/network/introduction-to-receive-side-scaling)」を参照してください。

## <a name="single-root-input-output-virtualization-sr-iov"></a>シングルルート入力-出力仮想化 (SR-IOV)

Sr-iov を使用すると、VM トラフィックを Hyper-v ホストを経由せずに NIC から VM に直接移動できます。 SR-IOV は VM のパフォーマンスを大幅に向上させるものですが、ホストがそのパイプを管理する機能がありません。 SR-IOV は、ワークロードが正常に動作し、信頼されており、ホスト内の唯一の VM である場合にのみ使用してください。

Sr-iov を使用するトラフィックは、Hyper-v スイッチをバイパスします。これは、Acl や帯域幅管理など、すべてのポリシーが適用されないことを意味します。 SR-IOV トラフィックは、ネットワーク仮想化機能を使用して渡すこともできないため、NV GRE または VxLAN カプセル化は適用できません。 特定の状況では、信頼できるワークロードに対してのみ SR-IOV を使用します。 また、ホストポリシー、帯域幅管理、および仮想化テクノロジを使用することはできません。

将来、2つのテクノロジによって SR-IOV: 汎用フローテーブル (GFT) とハードウェア QoS オフロード (NIC での帯域幅管理) が可能になり、エコシステムの Nic によってサポートされるようになります。 これら2つのテクノロジを組み合わせることにより、すべての Vm に対して sr-iov が有効になり、ポリシー、仮想化、帯域幅管理ルールを適用できるようになるため、sr-iov の一般的なアプリケーションに飛躍を進めることができます。

詳細については、「[シングルルート I/o 仮想化 (sr-iov) の概要](/windows-hardware/drivers/network/overview-of-single-root-i-o-virtualization--sr-iov-)」を参照してください。

## <a name="tcp-chimney-offload"></a>TCP Chimney オフロード

Tcp Chimney オフロード (TCP エンジンオフロード (TOE) とも呼ばれます) は、ホストがすべての TCP 処理を NIC にオフロードできるテクノロジです。 Windows Server TCP スタックは、TOE エンジンよりもほぼ常に効率的であるため、TCP Chimney オフロードを使用することはお勧めしません。

>[!IMPORTANT]
>TCP Chimney オフロードは、非推奨のテクノロジです。 TCP Chimney オフロードを使用しないことをお勧めします。これは、Microsoft が将来のサポートを停止する可能性があるためです。

## <a name="virtual-local-area-network-vlan"></a>仮想ローカルエリアネットワーク (VLAN)

VLAN は、イーサネットフレームヘッダーの拡張機能であり、LAN を複数の Vlan に分割し、それぞれが独自のアドレス空間を使用するようにします。 Windows Server 2016 では、Vlan は Hyper-v スイッチのポートに設定されるか、NIC チーミングチームのチームインターフェイスを設定することによって設定されます。 詳細については、「 [NIC チーミングと仮想ローカルエリアネットワーク (vlan)](../nic-teaming/nic-teaming.md)」を参照してください。

## <a name="virtual-machine-queue-vmq"></a>仮想マシン キュー (VMQ)

VMQs は、各 VM のキューを割り当てる NIC 機能です。 Hyper-v が有効になっている場合また、VMQ を有効にする必要があります。 Windows Server 2016 では、VMQs は、同じ機能を提供するために、Vports に割り当てられた単一のキューで NIC スイッチ vPorts を使用します。 詳細については、「[仮想 Receive Side Scaling (vRSS)](../vrss/vrss-top.md) 」および「 [NIC チーミング](../nic-teaming/nic-teaming.md)」を参照してください。

## <a name="virtual-machine-multi-queue-vmmq"></a>バーチャルマシンのマルチキュー (VMMQ)

VMMQ は、VM のトラフィックを複数のキューに分散し、それぞれが異なる物理プロセッサによって処理されるようにするための NIC 機能です。 このトラフィックは、vRSS の場合と同じように、VM 内の複数の LPs に渡されます。これにより、VM に対するネットワーク帯域幅が大幅に配信されます。

---