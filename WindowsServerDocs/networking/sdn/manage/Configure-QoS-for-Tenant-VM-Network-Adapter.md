---
title: テナントの VM ネットワーク アダプターのサービスの品質 (QoS) を構成します。
description: このトピックでは、テナント ワークロードを管理および Windows Server 2016 での仮想ネットワークに方法について、ソフトウェア定義ネットワーク ガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6d783ff6-7dd5-496c-9ed9-5c36612c6859
ms.author: pashort
author: shortpatti
ms.openlocfilehash: cde4e21beaec58a98a5d5fbe5c4631e2f113dbf7
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="configure-quality-of-service-qos-for-a-tenant-vm-network-adapter"></a>テナントの VM ネットワーク アダプターのサービスの品質 (QoS) を構成します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

データ センター ブリッジングを選ぶ必要があるテナントの VM ネットワーク アダプターの QoS を構成するときに \ (DCB\) またはソフトウェアがネットワーク定義 \(SDN\) QoS します。

1.  **DCB**します。 DCB は、Windows PowerShell NetQoS コマンドレットを使用して構成できます。 例については、「を有効にするデータ センター ブリッジング」」セクションを参照してください。[リモート ダイレクト メモリ アクセス (RDMA) とスイッチ埋め込みチーミング (SET)](../../../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)します。

2.  **SDN QoS**します。 高トラフィックの VM が他のユーザーをブロックするを防ぐために仮想インターフェイス上の帯域幅の制限に設定できます。 ネットワーク コント ローラーを使用して、SDN QoS を有効にすることができます。  SDN QoS では、特定の VM がネットワーク トラフィックの量に関係なくアクセスできることを確認する VM の帯域幅予約を構成することもできます。  

SDN Qos のすべての設定は、次の表に従ってネットワーク インターフェイスのプロパティのポートの設定を通じて適用されます。

|要素名|説明|
|------------|-----------| 
|macSpoofing|Vm が VM に割り当てられていない MAC アドレスに送信パケットのソース メディア アクセス制御 \(MAC\) アドレスを変更できるかどうかを指定します。 値が「有効」許可 \ (異なる MAC address\ を使用する VM を許可する)「無効」と \ (it\ に割り当てられている MAC アドレスのみを使用する VM を許可) します。|
|arpGuard|ARP guard が有効になっているかどうかを指定します。  ARP guard では、ポートを通過する ArpFilter で指定されたアドレスのみ。  指定できる値は"enabled"または「無効」します。
|dhcpGuard|DHCP サーバーがあることを要求する VM から DHCP メッセージを破棄するかどうかを指定します。 指定できる値は"enabled"、DHCP メッセージを仮想化された DHCP サーバーと見なされるため、信頼されていない、または [無効] により、仮想化された DHCP サーバーが信頼できるであると見なされるために受信するのにメッセージを破棄します。
|stormLimit|1 秒間、バーチャル マシンが、指定した仮想ネットワーク アダプターから送信できるブロードキャスト、マルチキャスト、未知のユニキャスト パケットの数を指定します。 その 1 秒間隔中にこの上限を超えたブロードキャスト、マルチキャスト、未知のユニキャスト パケットは破棄されます。 値がゼロ \(0\) の制限はありませんを意味します。
|portFlowLimit|ポートに対して実行できるフローの最大数を指定します。  値は空白またはゼロ \(0\) は制限はないことを意味します。
|vmqWeight|仮想ネットワーク アダプターで仮想マシン キュー (VMQ) が有効になっているかどうかを指定します。 相対的な重みは VMQ を使用する仮想ネットワーク アダプターのアフィニティをについて説明します。 値の範囲は、0 ~ 100 です。 仮想ネットワーク アダプターで VMQ は無効にする場合は 0 を指定します。
|iovWeight|シングル ルート I/O 仮想化 \(SR-IOV\) がかどうかを指定します。 この仮想ネットワーク アダプターで有効にします。 相対的な重みは、割り当てられた SR-IOV 仮想機能を仮想ネットワーク アダプターのアフィニティを設定します。 値の範囲は、0 ~ 100 です。 仮想ネットワーク アダプターで SR-IOV を無効にする場合は 0 を指定します。 
|iovInterruptModeration|シングル ルート I/O 仮想化 \(SR-IOV\) 仮想関数の仮想ネットワーク アダプターに割り当てられている割り込み節度値を指定します。 指定できる値は、"default"、「アダプティブ」、"off"、「低」、「中」、および「高」です。   既定値を選択した場合、値は、物理ネットワーク アダプター ベンダーの設定によって決まります。  アダプティブが選ばれた場合は、割り込み節度レートはランタイム トラフィック パターンに基づきます。 
|iovQueuePairsRequested|SR-IOV 仮想機能に割り当てるハードウェア キュー ペアの数を指定します。 Receive side scaling \(RSS\) が必要な場合と、仮想スイッチにバインドする物理ネットワーク アダプターの SR-IOV 仮想 RSS をサポートしている場合、関数、複数の 1 つのキュー ペアが必要です。 値の範囲は 1 から 4294967295 までを許可します。 
|QosSettings|オプションはすべて、次の Qos 設定を構成できます。  <br/><br />**outboundReservedValue:**<br/>OutboundReservedMode が"absolute"の場合、値は仮想ポート (出口) を送信することが保証、Mbps の帯域幅を示します。 OutboundReservedMode が"weight"の場合は、値が保証されて帯域幅の重み付きの部分を示します。 <br/><br />**outboundMaximumMbps:**  <br/>最大値、Mbps で仮想ポート (出口) の送信側の帯域幅を許可することを示します。 <br/><br/>**InboundMaximumMbps:**  <br/>最大許可 Mbps で仮想ポート (受信) の受信側の帯域幅を示します。 |