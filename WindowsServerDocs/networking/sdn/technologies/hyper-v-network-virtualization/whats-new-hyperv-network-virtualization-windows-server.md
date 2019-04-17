---
title: Windows Server 2016 で HYPER-V ネットワーク仮想化の新機能
description: このトピックの「Windows Server 2016 で Hyper-V ネットワーク仮想化の新機能に関する情報を提供する
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0254275a-0a77-40a9-b68a-1029284c03fe
ms.author: pashort
author: shortpatti
ms.date: 03/19/2018
ms.openlocfilehash: 0954768944e44848debfbb7fb752a13ca47031c2
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="whats-new-in-hyper-v-network-virtualization-in-windows-server-2016"></a>Windows Server 2016 で HYPER-V ネットワーク仮想化の新機能

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、Hyper-V ネットワーク仮想化 (HNV) の機能を Windows Server 2016 で追加または変更について説明します。  
  
## <a name="BKMK_IPAM2012R2"></a>HNV の更新プログラム  
HNV は、次の領域で拡張サポートを提供します。  
  
|機能/|新しい、または改良されて|説明|  
|--------------------------|-------------------|---------------|  
|[プログラム可能な Hyper-V スイッチ](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#SDN)|新機能|HNV のポリシーは、Microsoft ネットワーク コントローラーによってプログラミングできます。|  
|[VXLAN カプセル化のサポート](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#VXLAN)|新機能|HNV では、VXLAN カプセル化できるようになりました。|  
|[ソフトウェア ロード バランサー (SLB) の相互運用性](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#SLB)|新機能|HNV は、Microsoft ソフトウェア ロード バランサーと完全に統合されています。|  
|[準拠の IEEE イーサネット ヘッダー](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#L2)|向上しました|イーサネットの IEEE 標準に準拠|  
  
### <a name="SDN"></a>プログラム可能な Hyper-V スイッチ  
HNV は、Microsoft の更新されたソフトウェアによるネットワーク制御 (SDN) ソリューションでは、基本的な構成要素し、SDN スタックと完全に統合します。  
  
Microsoft の新しいネットワーク コントローラーは、Open vSwitch データベース Management Protocol (OVSDB) として、SouthBound Interface (SBI) を使用する各ホストで実行されているホスト エージェントまでの HNV ポリシーをプッシュします。 ホストのエージェントのカスタマイズを使用して、このポリシーを格納する、[VTEP スキーマ](https://github.com/openvswitch/ovs/blob/master/vtep/vtep.ovsschema)と複雑なフロー ルールをプログラムでの Hyper-V スイッチ パフォーマンスの高いフロー エンジンをします。  
  
Hyper-V スイッチの内部フロー エンジンは、Microsoft Azure で使用される同じエンジン&trade;、Microsoft Azure パブリック クラウドでのハイパー大規模を実証されています。 さらに、SDN スタック全体をネットワーク コントローラー、およびネットワーク リソース プロバイダー (近日公開予定の詳細) を介してと整合性が Microsoft Azure、したがって、企業とホスティング サービス プロバイダーの顧客に Microsoft Azure パブリック クラウドの電源を戻すことです。  
  
> [!NOTE]  
> OVSDB に関する詳細については、次を参照してください。[RFC 7047](http://www.rfc-editor.org/info/rfc7047)します。  
  
Hyper-V スイッチには、単純なフロー エンジンの 'Microsoft の内で"動作と同じに基づく両方のフローのステートレスとステートフルな規則がサポートしています。  
 
![Windows Server 2016 の Hyper-V スイッチ](../../../media/what-s-new-in-hyper-v-network-virtualization-in-windows-server/HNVOverview.png)  
  
### <a name="VXLAN"></a>VXLAN カプセル化のサポート  
仮想拡張可能なローカル エリア ネットワーク (VXLAN - [RFC 7348](http://www.rfc-editor.org/info/rfc7348)) プロトコルが Cisco、Brocade、Dell、HP および他のユーザーのようなベンダーからのサポートを市場で広く受け入れられます。 HNV はそのテナント オーバーレイ ネットワークの IP アドレス、カスタマー アドレス (CA)、物理アンダーレイ ネットワークの IP アドレスに、プロバイダー アドレス (PA)、Microsoft ネットワーク コントローラー プログラムへのマッピングからを通じて MAC 配布モードを使用してこのカプセル化スキームもサポートします。 サード パーティ ドライバーによるパフォーマンスの向上は、NVGRE と VXLAN タスク オフロードの両方がサポートされています。  
  
### <a name="SLB"></a>ソフトウェア ロード バランサー (SLB) の相互運用性  
Windows Server 2016 には、仮想ネットワーク トラフィックおよび HNV とシームレスな相互作用を完全にサポートをソフトウェア ロード バランサー (SLB) が含まれています。 SLB のスイッチでは、データ平面 v-パフォーマンスの高いフロー エンジンによって実装されとの仮想 IP (VIP)]、[動的、ネットワーク コントローラーで制御されている IP (DIP) マッピングします。  
  
### <a name="L2"></a>準拠の IEEE イーサネット ヘッダー  
HNV は、業界標準プロトコルに依存しているサード パーティ製の仮想および物理アプライアンスと相互運用するための正しい L2 イーサネット ヘッダーを実装します。 Microsoft では、すべての転送されるパケットがあるすべてのフィールドにこの相互運用性を確実に準拠の値を確認します。 さらに、サポートの L2 の物理ネットワーク内のジャンボ フレーム (MTU > 1780) は、パケットは HNV の仮想ネットワークに接続された仮想マシンのゲストを確保しながらカプセル化プロトコル (NVGRE、VXLAN) で導入オーバーヘッドを考慮する必要がありますを維持 1514 MTU します。  
  
## <a name="see-also"></a>参照してください。  
  
-   [Hyper-V ネットワーク仮想化の概要](hyperv-network-virtualization-overview-windows-server.md)  
  
-   [Hyper-V ネットワーク仮想化の技術的な詳細](hyperv-network-virtualization-technical-details-windows-server.md)  
  
-   [ソフトウェア定義ネットワーク](../../Software-Defined-Networking--SDN-.md)  
  