---
title: 収束の NIC の物理スイッチの構成
description: このトピックでは、集約型の NIC 構成ガイドの Windows Server 2016 の一部です。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 6d53c797-fb67-4b9e-9066-1c9a8b76d2aa
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 98a2e249aea38bd4d07dc1bcbc9b1ca98b98b6d6
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="physical-switch-configuration-for-converged-nic"></a>収束の NIC の物理スイッチの構成

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

次のセクションでは、物理スイッチを構成するためのガイドラインとして使用できます。

これらは、のみコマンドとその使用方法です。環境内での Nic が接続されているポートを決定する必要があります。 

>[!IMPORTANT]
>SMB が構成されているどの優先順位の VLAN と非ドロップ ポリシーが設定されていることを確認します。

## <a name="arista-switch-dcs-7050s-64-eos-4137m"></a>Arista スイッチ \ (dcs\ 7050s\-64、EOS\-4.13.7M\)

1.  En \ (管理モードに移動、通常は password\ を要求する)
2.  Config \ (に入力する構成 mode\)
3.  実行の表示 \ (現在実行されている configuration \ の表示)
4.  スイッチ ポートにする、Nic が接続されているを確認します。 これらの例では 14/1,15/1,16/1,17/1 です。
5.  Int eth 14/1,15/1,16/1,17/1 \ (ports\ これらの構成モードに入る)
6.  Dcbx モード ieee
7.  優先度のフロー制御モード
8.  Switchport トランク ネイティブの vlan 225
9.  Switchport トランク vlan 100-225 を許可します。
10. Switchport モード トランク
11. 3 フロー制御を優先度の優先順位いいえアンド ドロップ
12. Qos cos の信頼します。
13. 実行の表示 \ (その構成が正常にセットアップ、ports\ ことを確認する)
14. Wr \ (設定を行うことが引き続き発生するスイッチ reboot\ 間)

### <a name="tips"></a>ヒント:
1.  [Command] を無効にないコマンド
2.  新しい VLAN を追加する方法: int vlan 100 \ (記憶域ネットワークの VLAN 100\ の場合)
3.  既存の Vlan を確認する方法: vlan を表示します。
4.  Arista スイッチの構成の詳細については、オンラインで検索: Arista EOS 手動
5.  このコマンドを使用して、PFC 設定を確認する: 優先度のフロー制御カウンターの詳細を表示します。

## <a name="dell-switch-s4810-ftos-99-00"></a>Dell スイッチ \ (S4810、FTOS 9.9 \(0.0\)\)

    
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
    

## <a name="cisco-switch-nexus-3132-version-602u61"></a>Cisco スイッチ \ (Nexus 3132、バージョン 6.0\(2\)U6\(1\)\)

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
    

## <a name="all-topics-in-this-guide"></a>このガイドのすべてのトピック

このガイドには、次のトピックが含まれています。

- [単一のネットワーク アダプターに収束の NIC 構成](cnic-single.md)
- [収束の NIC チーム化された NIC の構成](cnic-datacenter.md)
- [収束の NIC の物理スイッチの構成](cnic-app-switch-config.md)
- [集約型の NIC 構成のトラブルシューティング](cnic-app-troubleshoot.md)
