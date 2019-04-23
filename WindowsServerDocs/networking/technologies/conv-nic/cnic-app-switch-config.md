---
title: 収束の NIC の物理スイッチの構成
description: このトピックで提供していますガイドライン、物理スイッチを構成するためです。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 6d53c797-fb67-4b9e-9066-1c9a8b76d2aa
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/14/2018
ms.openlocfilehash: e31d7b83fee84d9055d938f77b49389205786244
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829403"
---
# <a name="physical-switch-configuration-for-converged-nic"></a>収束の NIC の物理スイッチの構成

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックで提供していますガイドライン、物理スイッチを構成するためです。 


これらは、コマンドとその用途; のみ環境内での Nic が接続されているポートを決定する必要があります。 

>[!IMPORTANT]
>SMB を構成する優先度の VLAN と非ドロップ ポリシーを設定することを確認します。

## <a name="arista-switch-dcs-7050s-64-eos-4137m"></a>Arista スイッチ\(dc\-7050s\-64、EOS\-4.13.7M\)

1.  en\(管理者モードに移動し、通常、パスワードの確認\)
2.  config \(to enter into configuration mode\)
3.  実行の表示\(現在実行中の構成を示しています。\)
4.  Nic が接続するスイッチのポートを確認します。 これらの例では 14/1,15/1,16/1,17/1 です。
5.  int eth 14/1,15/1,16/1,17/1\(これらのポートの構成モードに切り替わります\)
6.  dcbx モード ieee
7.  優先度のフロー制御モード
8.  switchport トランク ネイティブ vlan 225
9.  switchport トランク vlan 100 ~ 225 台の許可
10. switchport モード トランク
11. フロー制御の優先度の優先順位 3 非ドロップ
12. qos 信頼 cos
13. 実行の表示\(その構成が、ポートに正しくセットアップであることを確認\)
14. wr\(設定を行うには、スイッチの再起動をまたいで維持\)

### <a name="tips"></a>ヒント:
1.  Command # 否定コマンドなし
2.  新しい VLAN を追加する方法: int vlan 100\(記憶域ネットワークが VLAN 100 にある場合\)
3.  既存の Vlan を確認する方法: vlan を表示します。
4.  Arista スイッチの構成の詳細については、オンラインで検索します。Arista EOS 手動
5.  このコマンドを使用して、PFC 設定を確認する: フロー制御の優先度のカウンターの詳細を表示します。

--- 

## <a name="dell-switch-s4810-ftos-99-00"></a>Dell スイッチ\(S4810、FTOS 9.9 \(0.0\)\)

    
    !
    dcb enable
    ! put pfc control on qos class 3
    configure
    dcb-map dcb-smb
    priority group 0 bandwidth 90 pfc on
    priority group 1 bandwidth 10 pfc off
    priority-pgid 1 1 1 0 1 1 1 1
    exit
    ! apply map to ports 0-31
    configure
    interface range ten 0/0-31
    dcb-map dcb-smb
    exit
    
--- 

## <a name="cisco-switch-nexus-3132-version-602u61"></a>Cisco のスイッチ\(Nexus 3132、バージョン 6.0\(2\)U6\(1\)\)

### <a name="global"></a>グローバル
    
    class-map type qos match-all RDMA
    match cos 3
    class-map type queuing RDMA
    match qos-group 3
    policy-map type qos QOS_MARKING
    class RDMA
    set qos-group 3
    class class-default
    policy-map type queuing QOS_QUEUEING
    class type queuing RDMA
    bandwidth percent 50
    class type queuing class-default
    bandwidth percent 50
    class-map type network-qos RDMA
    match qos-group 3
    policy-map type network-qos QOS_NETWORK
    class type network-qos RDMA
    mtu 2240
    pause no-drop
    class type network-qos class-default
    mtu 9216
    system qos
    service-policy type qos input QOS_MARKING
    service-policy type queuing output QOS_QUEUEING
    service-policy type network-qos QOS_NETWORK
    

### <a name="port-specific"></a>特定のポート

    
    switchport mode trunk
    switchport trunk native vlan 99
    switchport trunk allowed vlan 99,2000,2050   çuse VLANs that already exists
    spanning-tree port type edge
    flowcontrol receive on (not supported with PFC in Cisco NX-OS)
    flowcontrol send on (not supported with PFC in Cisco NX-OS)
    no shutdown
    priority-flow-control mode on
    
--- 

## <a name="related-topics"></a>関連トピック

- [1 つのネットワーク アダプターに収束の NIC の構成](cnic-single.md)
- [収束の NIC チーミングされた NIC の構成](cnic-datacenter.md)
- [集約型のない NIC 構成のトラブルシューティング](cnic-app-troubleshoot.md)

--- 