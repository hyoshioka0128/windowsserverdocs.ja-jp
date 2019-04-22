---
title: ソフトウェアのみ (SO) の機能とテクノロジ
description: これらの機能は、OS の一部としては実装されは基になるレベルに依存しません。 場合によってこれらの機能では、最適な操作を NIC のチューニングをいくつかが必要です。 これらの例には、仮想マシンのサービス品質 (vmQoS)、アクセス制御リスト (Acl)、NIC チーミングなどの非 HYPER-V 機能など、hyper-v の機能が含まれます。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 0cafb1cc-5798-42f5-89b6-3ffe7ac024ba
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/20/2018
ms.openlocfilehash: 504bc92971e778b468812dc4064fa6f0afff87ad
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823783"
---
# <a name="software-only-so-features-and-technologies"></a>ソフトウェアのみ (SO) の機能とテクノロジ
ソフトウェアのみの機能は、OS の一部として実装されは基になるレベルに依存しません。 場合によってこれらの機能では、最適な操作を NIC のチューニングをいくつかが必要です。 これらの例には、仮想マシンのサービス品質 (vmQoS)、アクセス制御リスト (Acl)、NIC チーミングなどの非 HYPER-V 機能など、hyper-v の機能が含まれます。

## <a name="access-control-lists-acls"></a>アクセス制御リスト (Acl)

VM のセキュリティを管理するため、HYPER-V および SDNv1 機能です。 この機能は、HYPER-V の非仮想化スタックと HVNv1 スタックに適用されます。 HYPER-V を管理することができますから Acl を切り替える[Add-vmnetworkadapteracl](https://docs.microsoft.com/powershell/module/hyper-v/add-vmnetworkadapteracl?view=win10-ps)と[Remove-vmnetworkadapteracl](https://docs.microsoft.com/powershell/module/hyper-v/remove-vmnetworkadapteracl?view=win10-ps) PowerShell コマンドレット。

## <a name="extended-acls"></a>拡張 Acl

HYPER-V 仮想スイッチ拡張 Acl を使用すると、HYPER-V 仮想スイッチ拡張ポート Acl をファイアウォール保護を提供し、データ センターでテナントの Vm のセキュリティ ポリシーを構成できます。 Vm 内ではなく、HYPER-V 仮想スイッチ ポート Acl を構成するため、管理者は、マルチ テナント環境ですべてのテナントのセキュリティ ポリシーを管理できます。

HYPER-V スイッチの拡張で Acl を管理することができます、 [Add-vmnetworkadapterextendedacl](https://docs.microsoft.com/powershell/module/hyper-v/add-vmnetworkadapterextendedacl?view=win10-ps)と[Remove-vmnetworkadapterextendedacl](https://docs.microsoft.com/powershell/module/hyper-v/remove-vmnetworkadapteracl?view=win10-ps) PowerShell コマンドレット。

>[!TIP] 
>この機能は、HNVv1 スタックに適用されます。 SDN スタックの Acl、ソフトウェア定義ネットワーク SDN を参照してください) 以下の Acl。

拡張ポート アクセス制御リストこのライブラリの詳細については、次を参照してください。[拡張ポート アクセス制御リストでのセキュリティ ポリシーの作成](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/Create-Security-Policies-with-Extended-Port-Access-Control-Lists)です。

## <a name="nic-teaming"></a>NIC チーミング

ホストが 1 つの NIC ポートとして認識エンティティに複数の NIC ポートの集計は、NIC チーミングは、NIC の結合とも呼ばれます。 NIC チーミングは、1 つの NIC ポート (またはそれに接続するケーブル) の障害から保護します。 また、高速なスループットのネットワーク トラフィックを集約します。 詳細については、次を参照してください。 [NIC チーミング](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming)します。

Windows Server 2016 では、チーミングは 2 つの方法があります。

1.  Windows Server 2012 のチーム化ソリューション

2.  Windows Server 2016 スイッチ埋め込みチーミング (SET)


## <a name="rsc-in-the-vswitch"></a>VSwitch で RSC

受信セグメント Coalescing (RSC)、vSwitch では同じの一部であるはパケット ストリームし、ネットワークの割り込みの間に到着する機能であり、オペレーティング システムに配布する前の 1 つのパケットに結合されています。 Windows Server 2019 内の仮想スイッチでは、この機能を持ちます。 この機能の詳細については、次を参照してください。 [Segment Coalescing vSwitch でに受信](https://docs.microsoft.com/windows-server/networking/technologies/hpn/rsc-in-the-vswitch)します。

## <a name="software-defined-networking-sdn-acls"></a>ソフトウェア定義ネットワーク (SDN) の Acl

Windows Server 2016 の SDN 拡張機能には、Acl をサポートする方法が向上しました。 Windows Server 2016 の SDN v2 スタックを Acl と Acl の拡張ではなく SDN Acl を使用します。 SDN の Acl を管理するのには、ネットワーク コント ローラーを使用できます。 

## <a name="sdn-quality-of-service-qos"></a>SDN サービスの品質 (QoS)

Windows Server 2016 の SDN の拡張機能には、5 タプルごとに帯域幅の制御 (エグレス予約、送信の制限、および受信の制限) を提供する方法が向上しました。 通常、vNIC または vmNIC のレベルで適用されるこれらのポリシーができるようにするはるかに詳細です。 Windows Server 2016 の SDN v2 スタックを vmQoS ではなく SDN QoS を使用します。 ネットワーク コント ローラーを使用して SDN QoS を管理することができます。

## <a name="switch-embedded-teaming-set"></a>スイッチが埋め込まれたチーミング (設定)

セットは、Hyper-v ホストと、ソフトウェアによるネットワーク制御 (SDN) スタックを Windows Server 2016 に含まれる環境で使用できる代替 NIC チーミング ソリューションです。 セットは、HYPER-V 仮想スイッチにいくつかの NIC チーミング機能を統合します。 このライブラリでのスイッチ埋め込みチーミングについては、次を参照してください。[リモート ダイレクト メモリ アクセス (RDMA) とスイッチ埋め込みチーミング (SET)](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming)します。

## <a name="virtual-receive-side-scaling-vrss"></a>Virtual Receive Side Scaling (vRSS)

ソフトウェア vRSS を使用して、複数の論理プロセッサ (LPs)、VM の VM 宛ての着信トラフィックを分散します。 ソフトウェア vRSS では、VM が 1 つの LP よりも多くのネットワーク トラフィックを処理する機能を処理することになります。 詳細については、次を参照してください。[仮想 Receive Side Scaling (vRSS)](https://docs.microsoft.com/windows-server/networking/technologies/vrss/vrss-top)します。

## <a name="virtual-machine-quality-of-service-vmqos"></a>仮想マシンのサービス品質 (vmQoS)

サービスの品質を仮想マシンは、各 VM によって生成されるトラフィックの制限を設定への切り替えを許可する HYPER-V 機能です。 また、VM を 1 つの VM は別の VM の帯域幅ができないように、外部のネットワーク接続には、帯域幅の量を予約することもできます。 Windows Server 2016 の SDN v2 スタックでは、SDN QoS は、vmQoS を置き換えます。

vmQoS には、送信の制限とエグレスの予約を設定できます。 HYPER-V スイッチを作成する前に、エグレス予約モードの (相対的な重みまたは絶対帯域幅) を決定する必要があります。

-  New-vmswitch PowerShell コマンドレットの – MinimumBandwidthMode パラメーターを持つエグレス予約モードを決定します。

-  Set-vmnetworkadapter PowerShell コマンドレットで – MaximumBandwidth パラメーターを使用して送信制限の値を設定します。

-  設定 VMNetworkAdapter PowerShell コマンドレットの次のパラメーターのいずれかでエグレス予約の値を設定します。

   -  New-vmswitch コマンドレットの – MinimumBandwidthMode パラメーターが絶対パスである場合は、VMNetworkAdapter の設定のコマンドレットで – MinimumBandwidthAbsolute パラメーターを設定します。

   -  New-vmswitch コマンドレットの – MinimumBandwidthMode パラメーターが重みである場合は、VMNetworkAdapter の設定のコマンドレットで – MinimumBandwidthWeight パラメーターを設定します。

この機能に使用されるアルゴリズムの制限により、最も高い重みまたは絶対帯域幅されないこと、最下位の重みの 20 回を超えてまたは絶対帯域幅をお勧めします。 詳細に制御が必要な場合は、SDN スタックと SDN QoS 機能を使用して検討してください。


---