---
title: テナント VM のネットワーク アダプターのサービスの品質 (QoS) を構成します。
description: データ センター ブリッジングの間の選択肢があるテナント VM ネットワーク アダプターに対する QoS を構成するときに\(DCB\)ソフトウェアによるネットワーク制御または\(SDN\) QoS します。
manager: dougkim
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
ms.date: 08/23/2018
ms.openlocfilehash: 0b9ce318c3d249b23d7560e0b6bb90a83e60d64d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880603"
---
# <a name="configure-quality-of-service-qos-for-a-tenant-vm-network-adapter"></a>テナント VM のネットワーク アダプターのサービスの品質 (QoS) を構成します。

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

データ センター ブリッジングの間の選択肢があるテナント VM ネットワーク アダプターに対する QoS を構成するときに\(DCB\)ソフトウェアによるネットワーク制御または\(SDN\) QoS します。

1.  **DCB**します。 DCB は、Windows PowerShell NetQoS コマンドレットを使用して構成できます。 例については、トピックの「を有効にするデータ センター ブリッジング」セクションを参照してください。[リモート ダイレクト メモリ アクセス (RDMA) とスイッチ埋め込みチーミング (SET)](../../../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)します。

2.  **SDN QoS**します。 高トラフィックの VM が他のユーザーをブロックするを防ぐために仮想インターフェイス上の帯域幅の制限を設定できるネットワーク コント ローラーを使用して SDN QoS を有効にすることができます。  特定の VM がネットワーク トラフィックの量に関係なくアクセスできることを確認する VM の帯域幅の容量を予約する SDN QoS を構成することもできます。  

ネットワーク インターフェイスのプロパティのポート設定を使用してすべての SDN QoS 設定を適用します。 詳細については、次の表を参照してください。

|要素名|説明|
|------------|-----------| 
|macSpoofing| ソース メディア アクセス コントロールを変更する Vm は、 \(MAC\) VM に割り当てられていない MAC アドレスへの送信パケットのアドレス。<p>指定可能な値:<ul><li>有効化-別の MAC アドレスを使用します。</li><li>無効 – は、割り当てられた MAC アドレスのみを使用します。</li></ul>|
|arpGuard| ARP guard のポートを通過する ArpFilter で指定されたアドレスだけを使用できます。<p>指定可能な値:<ul><li>有効になっている - 許可されています。</li><li>無効 – 許可されていません</li></ul>|
|dhcpGuard| 許可または DHCP サーバーがあることを要求する VM からすべての DHCP メッセージを削除します。 <p>指定可能な値:<ul><li>有効化-削除 DHCP メッセージを仮想化された DHCP サーバーは信頼されていないと見なされるためです。</li><li>無効 – 仮想化された DHCP サーバーが信頼できると見なされるために受信するメッセージを許可します。</li></ul>|
|stormLimit| もう 1 つは VM あたりのパケット数 (ブロードキャスト、マルチキャスト、未知のユニキャスト) の数は、仮想ネットワーク アダプターを介して送信できるのです。 その 1 秒間隔中に制限を超えるパケットは破棄を取得します。 値が 0 の\(0\)制限がないことを意味します.|
|portFlowLimit| ポートの実行を許可フローの最大数。 空白の値または 0 \(0\)制限がないことを意味します。 |
|vmqWeight| 相対的な重みには、仮想マシン キュー (VMQ) を使用する仮想ネットワーク アダプターのアフィニティがについて説明します。 値の範囲は、0 ~ 100 です。<p>指定可能な値:<ul><li>0 – には、仮想ネットワーク アダプターで VMQ が無効にします。</li><li>1-100-仮想ネットワーク アダプターで VMQ できるようにします。</li></ul>|
|iovWeight| 相対的な重みが割り当てられたシングル ルート I/O 仮想化を仮想ネットワーク アダプターのアフィニティを設定\(SR-IOV\)仮想関数。 <p>指定可能な値:<ul><li>0 – 無効になります、SR-IOV 仮想ネットワーク アダプターにします。</li><li>1 ~ 100 – により、SR-IOV 仮想ネットワーク アダプターにします。</li></ul>|
|iovInterruptModeration|<p>指定可能な値:<ul><li>既定: 物理ネットワーク アダプター ベンダーの設定は、値を決定します。</li><li>アダプティブ- </li><li>オフ </li><li>low</li><li>中</li><li>high</li></ul><p>選択した場合**既定**、物理ネットワーク アダプター ベンダーの設定値を決定します。  選択した場合、**アダプティブ**、ランタイム トラフィック パターン、割り込み節度レートを示します。|
|iovQueuePairsRequested| SR-IOV 対応の仮想関数に割り当てられているハードウェア キュー ペアの数。 場合、受信側のスケーリング\(RSS\)は必須であり、場合は、仮想スイッチにバインドする物理ネットワーク アダプター RSS の SR-IOV 仮想機能がサポートしている 1 つ以上のキュー ペアが必要です。 <p>指定可能な値:1 ~ 4294967295 です。|
|QosSettings| 省略可能なすべてが、次の Qos 設定を構成するには。 <ul><li>**outboundReservedValue** - 場合 outboundReservedMode"absolute"、値は、帯域幅、転送 (送信) の仮想ポートに保証 (mbps) を示します。 OutboundReservedMode が"weight"の場合、値は保証帯域幅の重み付けの部分を示します。</li><li>**outboundMaximumMbps** -最大値 (mbps) は、仮想ポート (送信) の送信側の帯域幅を指定することを示します。</li><li>**InboundMaximumMbps** -許可された受信側の帯域幅 (mbps) は、仮想ポート (受信) の最大値を示します。</li></ul> |

---