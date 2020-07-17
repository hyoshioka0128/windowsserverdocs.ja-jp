---
title: ソフトウェアのみ (SO) の機能とテクノロジ
description: これらの機能は OS の一部として実装され、基になる NIC からは独立しています。 場合によっては、最適な操作のために NIC のチューニングが必要になることがあります。 これらの例としては、仮想マシンのサービス品質 (vmQoS)、Access Control リスト (Acl)、NIC チーミングなどの Hyper-v 以外の機能などの Hyper-v 機能が挙げられます。
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 0cafb1cc-5798-42f5-89b6-3ffe7ac024ba
manager: dougkim
ms.author: lizross
author: eross-msft
ms.date: 09/20/2018
ms.openlocfilehash: a83a36ce7a47f0ebde35bf93bdca20796dd37a28
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80316879"
---
# <a name="software-only-so-features-and-technologies"></a>ソフトウェアのみ (SO) の機能とテクノロジ
ソフトウェアのみの機能は OS の一部として実装され、基になる NIC からは独立しています。 場合によっては、最適な操作のために NIC のチューニングが必要になることがあります。 これらの例としては、仮想マシンのサービス品質 (vmQoS)、Access Control リスト (Acl)、NIC チーミングなどの Hyper-v 以外の機能などの Hyper-v 機能が挙げられます。

## <a name="access-control-lists-acls"></a>Access Control リスト (Acl)

VM のセキュリティを管理するための Hyper-v と SDNv1 の機能。 この機能は、仮想化されていない Hyper-v スタックと HVNv1 スタックに適用されます。 [Get-vmnetworkadapteracl](https://docs.microsoft.com/powershell/module/hyper-v/add-vmnetworkadapteracl?view=win10-ps)と[get-vmnetworkadapteracl](https://docs.microsoft.com/powershell/module/hyper-v/remove-vmnetworkadapteracl?view=win10-ps) PowerShell コマンドレットを使用して、hyper-v スイッチ acl を管理できます。

## <a name="extended-acls"></a>拡張 Acl

Hyper-v 仮想スイッチ拡張 Acl を使用すると、Hyper-v 仮想スイッチ拡張ポート Acl を構成して、ファイアウォールによる保護を提供し、データセンター内のテナント Vm にセキュリティポリシーを適用することができます。 ポート Acl は Vm 内ではなく Hyper-v 仮想スイッチで構成されるため、管理者はマルチテナント環境のすべてのテナントのセキュリティポリシーを管理できます。

[Add-vmnetworkadapterextendedacl](https://docs.microsoft.com/powershell/module/hyper-v/add-vmnetworkadapterextendedacl?view=win10-ps)と[add-vmnetworkadapterextendedacl](https://docs.microsoft.com/powershell/module/hyper-v/remove-vmnetworkadapteracl?view=win10-ps) PowerShell コマンドレットを使用して、hyper-v スイッチ拡張 acl を管理できます。

>[!TIP] 
>この機能は HNVv1 スタックに適用されます。 SDN スタックの Acl については、以下の「Software Defined Network SDN) Acl」を参照してください。

このライブラリの拡張ポート Access Control リストの詳細については、「[拡張ポート Access Control リストを使用したセキュリティポリシーの作成](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/Create-Security-Policies-with-Extended-Port-Access-Control-Lists)」を参照してください。

## <a name="nic-teaming"></a>NIC チーミング

Nic チーミングは NIC 結合とも呼ばれ、1つのエンティティに複数の NIC ポートを集約したもので、ホストは1つの NIC ポートとして認識します。 NIC チーミングは、1つの NIC ポート (または接続されているケーブル) の障害から保護します。 また、スループットを向上させるためにネットワークトラフィックを集約します。 詳細については、「 [NIC チーミング](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming)」を参照してください。

Windows Server 2016 では、次の2つの方法でチーミングを行うことができます。

1.  Windows Server 2012 チーミングソリューション

2.  Windows Server 2016 スイッチ埋め込みチーミング (SET)


## <a name="rsc-in-the-vswitch"></a>VSwitch 内の RSC

VSwitch 内の受信セグメント合体 (RSC) は、同じストリームの一部であり、ネットワーク割り込み間に到着するパケットを取得し、それらをオペレーティングシステムに配信する前に1つのパケットにまとめる機能です。 Windows Server 2019 の仮想スイッチには、この機能があります。 この機能の詳細については、「 [vSwitch でのセグメント結合の受信](https://docs.microsoft.com/windows-server/networking/technologies/hpn/rsc-in-the-vswitch)」を参照してください。

## <a name="software-defined-networking-sdn-acls"></a>ソフトウェア定義ネットワーク (SDN) Acl

Windows Server 2016 の SDN 拡張機能により、Acl をサポートする方法が改善されました。 Windows Server 2016 SDN v2 スタックでは、Acl および拡張 Acl ではなく SDN Acl が使用されます。 ネットワークコントローラーを使用して SDN Acl を管理できます。 

## <a name="sdn-quality-of-service-qos"></a>SDN サービスの品質 (QoS)

Windows Server 2016 の SDN 拡張機能では、5組の帯域幅制御 (送信予約、送信制限、受信制限) を実現する方法が改善されました。 通常、これらのポリシーは、vNIC または vmNIC レベルで適用されますが、さらに具体的なものにすることができます。 Windows Server 2016 SDN v2 スタックでは、vmQoS ではなく SDN QoS が使用されます。 ネットワークコントローラーを使用して SDN QoS を管理できます。

## <a name="switch-embedded-teaming-set"></a>スイッチが埋め込まれたチーミング (設定)

セットは、Hyper-v ホストと、ソフトウェアによるネットワーク制御 (SDN) スタックを Windows Server 2016 に含まれる環境で使用できる代替 NIC チーミング ソリューションです。 セットは、HYPER-V 仮想スイッチにいくつかの NIC チーミング機能を統合します。 このライブラリのスイッチ埋め込みチーミングの詳細については、「[リモートダイレクトメモリアクセス (RDMA)」と「スイッチ埋め込みチーミング (SET)](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming)」を参照してください。

## <a name="virtual-receive-side-scaling-vrss"></a>Virtual Receive Side Scaling (vRSS)

ソフトウェア vRSS は、vm の複数の論理プロセッサ (LPs) にわたって、VM の着信トラフィックを分散するために使用されます。 ソフトウェア vRSS は、1つの LP が処理できるよりも多くのネットワークトラフィックを VM に処理する機能を提供します。 詳細については、「[仮想 Receive Side Scaling (vRSS)](https://docs.microsoft.com/windows-server/networking/technologies/vrss/vrss-top)」を参照してください。

## <a name="virtual-machine-quality-of-service-vmqos"></a>バーチャルマシンのサービスの品質 (vmQoS)

バーチャルマシンのサービスの品質は、スイッチが各 VM によって生成されるトラフィックの制限を設定できるようにする Hyper-v 機能です。 また、VM が外部ネットワーク接続の帯域幅を予約して、1つの VM が帯域幅用に別の VM に接続できないようにすることもできます。 Windows Server 2016 SDN v2 スタックでは、SDN QoS は vmQoS に代わるものです。

vmQoS では、送信制限と送信予約を設定できます。 Hyper-v スイッチを作成する前に、送信予約モード (相対的な重みまたは絶対帯域幅) を決定する必要があります。

-  新しい VMSwitch PowerShell コマンドレットの– MinimumBandwidthMode パラメーターを使用して、送信予約モードを決定します。

-  VMNetworkAdapter PowerShell コマンドレットの– MaximumBandwidth 幅パラメーターを使用して、送信制限の値を設定します。

-  Set VMNetworkAdapter PowerShell コマンドレットの次のいずれかのパラメーターを使用して、送信予約の値を設定します。

   -  新しい VMSwitch コマンドレットの– MinimumBandwidthMode パラメーターが Absolute の場合は、Set VMNetworkAdapter コマンドレットで– MinimumBandwidthAbsolute パラメーターを設定します。

   -  新しい VMSwitch コマンドレットの– MinimumBandwidthMode パラメーターが Weight の場合は、Set VMNetworkAdapter コマンドレットで– MinimumBandwidthWeight パラメーターを設定します。

この機能で使用されるアルゴリズムには制限があるため、最大の重みまたは絶対帯域幅を最小の重みまたは絶対的な帯域幅の20倍以下にすることをお勧めします。 より詳細な制御が必要な場合は、SDN スタックと SDN QoS 機能の使用を検討してください。


---