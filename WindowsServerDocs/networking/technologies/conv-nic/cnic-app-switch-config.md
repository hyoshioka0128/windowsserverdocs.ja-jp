---
title: 収束 NIC の物理スイッチ構成
description: このトピックでは、物理スイッチを構成するためのガイドラインを提供します。
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 6d53c797-fb67-4b9e-9066-1c9a8b76d2aa
manager: dougkim
ms.author: lizross
author: eross-msft
ms.date: 09/14/2018
ms.openlocfilehash: 57fc944461254e78635913ac298bacc26a0789f2
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80309614"
---
# <a name="physical-switch-configuration-for-converged-nic"></a>収束 NIC の物理スイッチ構成

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、物理スイッチを構成するためのガイドラインを提供します。 


コマンドとその用途は次のとおりです。Nic が接続されている環境のポートを確認する必要があります。 

>[!IMPORTANT]
>VLAN および非ドロップポリシーが、SMB が構成されている優先順位に設定されていることを確認します。

## <a name="arista-switch-dcs-7050s-64-eos-4137m"></a>Arista スイッチ \(dc\-7050s\-64、EOS\-4.13.7 M\)

1.  en \(管理者モードに移行すると、通常はパスワードの入力が求められ\)
2.  構成モードに入るように構成 \(\)
3.  実行中の構成を表示して現在実行中の構成を表示 \(\)
4.  Nic が接続されているスイッチポートを見つけます。 これらの例では、14/1、15/1、16/1、17/1 です。
5.  int eth 14/1、15/1、16/1、17/1 \(これらのポートの構成モードに入り\)
6.  dcbx モード ieee
7.  優先順位-フロー制御モードオン
8.  switchport トランクネイティブ vlan 225
9.  switchport トランクが許可された vlan 100-225
10. switchport モードのトランク
11. 優先順位フロー制御優先順位3×ドロップ
12. qos 信頼 cos
13. [実行 \(表示] ポートで構成が正しくセットアップされていることを確認し\)
14. スイッチを再起動する間に設定を維持するには、wr \(\)

### <a name="tips"></a>ヒント:
1.  No #command # はコマンドを否定します。
2.  新しい VLAN を追加する方法: ストレージネットワークが VLAN 100 にある場合は、int vlan 100 \(\)
3.  既存の Vlan を確認する方法: vlan を表示する
4.  Arista スイッチの構成の詳細については、次を参照してください: Arista EOS 手動
5.  次のコマンドを使用して、PFC 設定を確認します: 優先順位フロー制御カウンターの詳細を表示します。

--- 

## <a name="dell-switch-s4810-ftos-99-00"></a>Dell スイッチ \(S4810、FTOS 9.9 \(0.0\)\)

    
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

## <a name="cisco-switch-nexus-3132-version-602u61"></a>Cisco スイッチ 3132 \(、バージョン 6.0\(2\)U6\(1\)\)

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