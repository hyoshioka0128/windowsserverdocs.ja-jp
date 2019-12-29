---
title: テナント VM ネットワークアダプターのサービス品質 (QoS) の構成
description: テナント VM ネットワークアダプターの QoS を構成する場合は、データセンター \(ブリッジング DCB\)と、ソフトウェアで定義された\(ネットワーク\) SDN QoS のどちらかを選択できます。
manager: dougkim
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6d783ff6-7dd5-496c-9ed9-5c36612c6859
ms.author: pashort
author: shortpatti
ms.date: 08/23/2018
ms.openlocfilehash: 1074525abe375e78ab0d2065ce8e98f894f50c61
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355846"
---
# <a name="configure-quality-of-service-qos-for-a-tenant-vm-network-adapter"></a>テナント VM ネットワークアダプターのサービス品質 (QoS) の構成

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

テナント VM ネットワークアダプターの QoS を構成する場合は、データセンター \(ブリッジング DCB\)と、ソフトウェアで定義された\(ネットワーク\) SDN QoS のどちらかを選択できます。

1.  **DCB**。 Windows PowerShell NetQoS コマンドレットを使用して DCB を構成できます。 例については、「[リモートダイレクトメモリアクセス (RDMA) とスイッチ埋め込みチーミング (SET)](../../../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)」の「データセンターブリッジングの有効化」セクションを参照してください。

2.  **SDN QoS**。 ネットワークコントローラーを使用して SDN QoS を有効にすることができます。これは、高トラフィックの VM が他のユーザーをブロックするのを防ぐために、仮想インターフェイスの帯域幅を制限するように設定できます。  また、ネットワークトラフィックの量に関係なく VM がアクセス可能であることを確認するために、SDN QoS を構成して、VM に特定の帯域幅を確保することもできます。  

ネットワークインターフェイスのプロパティのポート設定を使用して、すべての SDN QoS 設定を適用します。 詳細については、次の表を参照してください。

|要素名|説明|
|------------|-----------| 
|macSpoofing| Vm が、送信パケットのソースメディアアクセス\(制御\)の mac アドレスを、vm に割り当てられていない mac アドレスに変更できるようにします。<p>指定可能な値:<ul><li>有効-別の MAC アドレスを使用します。</li><li>[無効]: 割り当てられている MAC アドレスのみを使用します。</li></ul>|
|arpGuard| ArpFilter に指定されている ARP ガードのみのアドレスがポートを通過できるようにします。<p>指定可能な値:<ul><li>有効-許可</li><li>Disabled –許可されていません</li></ul>|
|dhcpGuard| DHCP サーバーとして要求される VM からの DHCP メッセージを許可または削除します。 <p>指定可能な値:<ul><li>[有効]: 仮想化された DHCP サーバーは信頼されていないと見なされるため、DHCP メッセージを削除します。</li><li>[無効]: 仮想化された DHCP サーバーが信頼できると見なされるため、メッセージを受信できるようにします。</li></ul>|
|stormLimit| VM が仮想ネットワークアダプターを介して送信することが許可されている1秒あたりのパケット (ブロードキャスト、マルチキャスト、および不明なユニキャスト) の数。 この1秒間に制限を超えるパケットは破棄されます。 \(値\) 0 は、制限がないことを意味します。|
|portFlowLimit| ポートに対して実行できるフローの最大数。 値が空白または\(\) 0 の場合は、制限がないことを意味します。 |
|vmqWeight| 相対的な重みは、仮想マシンキュー (VMQ) を使用する仮想ネットワークアダプターのアフィニティを表します。 値の範囲は 0 ~ 100 です。<p>指定可能な値:<ul><li>0: 仮想ネットワークアダプターで VMQ を無効にします。</li><li>1-100 –仮想ネットワークアダプターで VMQ を有効にします。</li></ul>|
|iovWeight| 相対的な重みは、割り当てられたシングルルート i/o 仮想化\(sr-iov\)仮想機能に仮想ネットワークアダプターのアフィニティを設定します。 <p>指定可能な値:<ul><li>0: 仮想ネットワークアダプターで sr-iov を無効にします。</li><li>1-100 –仮想ネットワークアダプターで sr-iov を有効にします。</li></ul>|
|iovInterruptModeration|<p>指定可能な値:<ul><li>既定–物理ネットワークアダプターベンダーの設定によって値が決定されます。</li><li>adaptive </li><li>オフ </li><li>low</li><li>中</li><li>high</li></ul><p>**[既定]** を選択すると、物理ネットワークアダプターベンダーの設定によって値が決まります。  **[アダプティブ]** を選択した場合、ランタイムトラフィックパターンは、割り込みモデレーション率を決定します。|
|iovQueuePairsRequested| Sr-iov 仮想機能に割り当てられたハードウェアキューペアの数。 Receive side scaling \(rss\)が必要であり、仮想スイッチにバインドする物理ネットワークアダプターが sr-iov 仮想機能で rss をサポートしている場合は、複数のキューペアが必要になります。 <p>指定可能な値:1 ~ 4294967295。|
|QosSettings| 次の Qos 設定を構成します。これらはすべてオプションです。 <ul><li>**outboundReservedValue** -outboundReservedMode が "absolute" の場合、この値は、送信 (送信) 用の仮想ポートに対して保証される帯域幅 (Mbps) を示します。 OutboundReservedMode が "weight" の場合、値は、保証される帯域幅の重み付け部分を示します。</li><li>**Outboundmaximummbps** -仮想ポート (送信) に許可されている送信側の最大帯域幅 (Mbps) を示します。</li><li>**InboundMaximumMbps** -仮想ポート (受信) で許可される受信側の最大帯域幅 (Mbps) を示します。</li></ul> |

---