---
title: 新機能 Windows Server 2016 で HYPER-V ネットワーク仮想化の新機能
description: このトピックでは、Windows Server 2016 で HYPER-V ネットワーク仮想化の新機能に関する情報を提供します。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0254275a-0a77-40a9-b68a-1029284c03fe
ms.author: pashort
author: shortpatti
ms.date: 03/19/2018
ms.openlocfilehash: c87ccfba7b9ccc77646f58ade2853766524e67b1
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284039"
---
# <a name="whats-new-in-hyper-v-network-virtualization-in-windows-server-2016"></a>新機能 Windows Server 2016 で HYPER-V ネットワーク仮想化の新機能

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは、新しいまたは Windows Server 2016 で変更された HYPER-V ネットワーク仮想化 (HNV) の機能について説明します。  
  
## <a name="BKMK_IPAM2012R2"></a>HNV の更新プログラム  
HNV は、次の領域で拡張サポートを提供します。  
  
|機能|新機能か強化された機能か|説明|  
|--------------------------|-------------------|---------------|  
|[プログラミング可能な HYPER-V スイッチ](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#SDN)|新規|HNV のポリシーは、Microsoft ネットワーク コント ローラーを使用してプログラミングできます。|  
|[VXLAN のカプセル化のサポート](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#VXLAN)|新規|HNV では、VXLAN のカプセル化できるようになりました。|  
|[ソフトウェア ロード バランサー (SLB) の相互運用性](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#SLB)|新規|HNV は、Microsoft ソフトウェア ロード バランサーに完全に統合します。|  
|[準拠の IEEE イーサネット ヘッダー](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#L2)|強化された機能|イーサネットの IEEE 標準に準拠|  
  
### <a name="SDN"></a>プログラミング可能な HYPER-V スイッチ  
HNV は、Microsoft の最新のソフトウェア定義ネットワーク (SDN) ソリューションの基本的なビルディング ブロックし、SDN スタックに完全に統合されます。  
  
Microsoft の新しいネットワーク コント ローラーは、HNV ポリシーまで Open vSwitch Database Management Protocol (OVSDB) として、SouthBound Interface (SBI) を使用する各ホストで実行されるホスト エージェントをプッシュします。 ホスト エージェントのカスタマイズを使用してこのポリシーを格納する、 [VTEP スキーマ](https://github.com/openvswitch/ovs/blob/master/vtep/vtep.ovsschema)と HYPER-V スイッチでのパフォーマンスの高いフロー エンジンに複雑なフロー ルールをプログラムします。  
  
HYPER-V スイッチ内のフロー エンジンは、Microsoft Azure で使用されるものと同じエンジン&trade;、これが Microsoft Azure パブリック クラウドでのハイパー スケールで実証されています。 さらに、SDN スタック全体をネットワーク コント ローラーとネットワーク リソース プロバイダー (詳細は近日公開予定) は、企業やホスティング サービスを Microsoft Azure パブリック クラウドの能力に引き下げの Microsoft Azure との一貫性プロバイダーの顧客です。  
  
> [!NOTE]  
> OVSDB の詳細については、次を参照してください。 [RFC 7047](https://www.rfc-editor.org/info/rfc7047)します。  
  
HYPER-V スイッチには、単純なフロー エンジンの Microsoft の社内で ' 同じアクション' に基づくステートレスおよびステートフルなフロー ルールの両方がサポートしています。  
 
![Windows Server 2016 の HYPER-V スイッチ](../../../media/what-s-new-in-hyper-v-network-virtualization-in-windows-server/HNVOverview.png)  
  
### <a name="VXLAN"></a>VXLAN のカプセル化のサポート  
仮想拡張可能なローカル エリア ネットワーク (VXLAN - [RFC 7348](https://www.rfc-editor.org/info/rfc7348)) プロトコルが Cisco、Brocade、Dell、HP などのベンダーからのサポートを市場で広く採用されています。 HNV は、テナント オーバーレイ ネットワークの IP アドレス (カスタマー アドレス、または CA)、物理アンダーレイ ネットワーク IP アドレス (プロバイダーへのプログラムのマッピングに Microsoft ネットワーク コント ローラーから MAC の分散モードを使用してこのカプセル化スキームもサポートしています。アドレス、または PA)。 サード パーティ製のドライバーによるパフォーマンスの向上には、NVGRE と VXLAN タスク オフロードの両方がサポートされています。  
  
### <a name="SLB"></a>ソフトウェア ロード バランサー (SLB) の相互運用性  
Windows Server 2016 には、仮想ネットワークのトラフィックと HNV とのシームレスな対話を完全サポート ソフトウェア ロード バランサー (SLB) が含まれています。 SLB のデータ プレーンの v スイッチで、パフォーマンスの高いフロー エンジンによって実装および仮想 IP (VIP) の/動的にネットワーク コント ローラーによって制御される IP (DIP) のマッピング。  
  
### <a name="L2"></a>準拠の IEEE イーサネット ヘッダー  
HNV は、業界標準のプロトコルに依存するサード パーティ製の仮想および物理アプライアンスとの相互運用性を確実に正しい L2 イーサネット ヘッダーを実装します。 Microsoft では、すべての転送されたパケットがあるすべてのフィールドをこの相互運用性を確実に準拠の値により確保されます。 さらに、サポートとしてのジャンボ フレーム (MTU > 1780) L2 の物理ネットワークではオーバーヘッドがゲストの HNV の仮想ネットワークに接続された仮想マシンを維持しながらのプロトコルのカプセル化 (NVGRE、VXLAN) で導入されたパケットのアカウントに必要になります、1514 MTU です。  
  
## <a name="see-also"></a>関連項目  
  
-   [Hyper-V ネットワーク仮想化の概要](hyperv-network-virtualization-overview-windows-server.md)  
  
-   [Hyper-V ネットワーク仮想化の技術的な詳細](hyperv-network-virtualization-technical-details-windows-server.md)  
  
-   [ソフトウェア定義ネットワーク](../../Software-Defined-Networking--SDN-.md)  
  