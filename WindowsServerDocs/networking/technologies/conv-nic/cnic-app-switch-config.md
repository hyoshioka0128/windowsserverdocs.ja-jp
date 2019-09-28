---
title: 収束 NIC の物理スイッチ構成
description: このトピックでは、物理スイッチを構成するためのガイドラインを提供します。
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 6d53c797-fb67-4b9e-9066-1c9a8b76d2aa
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/14/2018
ms.openlocfilehash: d10e8ca6e4689b89a8b9532f77613f17280282b1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355475"
---
# <a name="physical-switch-configuration-for-converged-nic"></a>収束 NIC の物理スイッチ構成

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、物理スイッチを構成するためのガイドラインを提供します。 


コマンドとその用途は次のとおりです。Nic が接続されている環境のポートを確認する必要があります。 

>[!IMPORTANT]
>VLAN および非ドロップポリシーが、SMB が構成されている優先順位に設定されていることを確認します。

## <a name="arista-switch-dcs-7050s-64-eos-4137m"></a>Arista スイッチ \(dcs @ no__t-17050s @ no__t-264, EOS @ no__t-34.13.7 M @ no__t-4

1.  en \(go モードに移行します。通常はパスワード @ no__t-1 を入力するように求められます。
2.  構成 \(to enter a configuration mode @ no__t-1
3.  実行 @no__t を表示する-0shows running 構成 @ no__t-1
4.  Nic が接続されているスイッチポートを見つけます。 これらの例では、14/1、15/1、16/1、17/1 です。
5.  int eth 14/1、15/1、16/1、17/1 \( これらのポートの構成モード @ no__t
6.  dcbx モード ieee
7.  優先順位-フロー制御モードオン
8.  switchport トランクネイティブ vlan 225
9.  switchport トランクが許可された vlan 100-225
10. switchport モードのトランク
11. 優先順位フロー制御優先順位3×ドロップ
12. qos 信頼 cos
13. 実行 @no__t を表示する-0verify がポート @ no__t-1 で正しく設定されていることを確認します。
14. wr \(to の再起動で設定を保持するには、@ no__t-1

### <a name="tips"></a>テクニック
1.  No #command # はコマンドを否定します。
2.  新しい VLAN を追加する方法: int vlan 100 \( (ストレージネットワークが VLAN 100 @ no__t にある場合)
3.  既存の Vlan を確認する方法: vlan を表示する
4.  Arista スイッチの構成の詳細については、オンラインで次のものを検索してください。Arista EOS 手動
5.  次のコマンドを使用して、PFC 設定を確認します: 優先順位フロー制御カウンターの詳細を表示します。

--- 

## <a name="dell-switch-s4810-ftos-99-00"></a>Dell スイッチ \(S4810、FTOS 9.9 \(0.0 @ no__t @ no__t

    
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

## <a name="cisco-switch-nexus-3132-version-602u61"></a>Cisco スイッチ \(Nexus 3132, version 6.0 @ no__t-2U6 @ no__t-31 @ no__t-4 @ no__t-5

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
    

### <a name="port-specific"></a>ポート固有

    
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

- [単一のネットワークアダプターを使用した収束 NIC 構成](cnic-single.md)
- [収束 NIC チーミング NIC 構成](cnic-datacenter.md)
- [収束 NIC 構成のトラブルシューティング](cnic-app-troubleshoot.md)

--- 