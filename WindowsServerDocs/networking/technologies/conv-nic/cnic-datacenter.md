---
title: 収束の NIC チーム化された NIC の構成
description: このトピックでは、Windows Server 2016 でのデータ センター構成で収束の NIC を構成する方法の手順を示します。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: f01546f8-c495-4055-8492-8806eee99862
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1ac6c2915301b1cf64486f24c197ebbf22bb5e2e
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="converged-nic-teamed-nic-configuration"></a>収束の NIC チーム化された NIC の構成

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

次のセクションでは、スイッチ埋め込みチーミング \(SET\) の NIC のチーム化された構成で収束の NIC を展開する手順についてを提供します。 このガイドで構成の例は、次の 2 つの Hyper-V ホスト、Hyper-V ホスト 1 では、および Hyper-V ホスト 2 を示しています。

## <a name="test-connectivity-between-source-and-destination"></a>移行元と送信先の間の接続をテストします。

このセクションでは、ソースと宛先の Hyper-V ホスト間の接続をテストするために必要な手順を示します。

次の図は、次の 2 つの Hyper-V ホストを示しています。**Hyper-v Host 1**と**Hyper-v Host 2**します。 

両方の Hyper-V ホストでは、次の 2 つのネットワーク アダプターがあります。 各ホスト上で 1 つのアダプターが、192.168.1.x/24 サブネットに接続されている、192.168.2.x/24 サブネットに 1 つのアダプターが接続されています。

![Hyper-V ホスト](../../media/Converged-NIC/1-datacenter-test-conn.jpg)

### <a name="test-nic-connectivity-to-the-hyper-v-virtual-switch"></a>Hyper-V 仮想スイッチに NIC の接続をテストします。

この手順を使用すると、移行先ホストに、Hyper-V 仮想スイッチを作成、後で、物理 NIC が接続できることを確認することができます。 

このテストは、レイヤー 3 \(L3\) - または - IP レイヤーだけでなく、レイヤー 2 \(L2\) 仮想ローカル エリア ネットワークを使用して接続を示しています \(VLAN\) します。

次の Windows PowerShell コマンドを使用して、ネットワーク アダプターのプロパティを取得することができます。

    Get-NetAdapter -Name "Test-40G-1" | ft -AutoSize
     
このコマンドの結果の例を次に示します。

|名|InterfaceDescription|ifIndex|ステータス|MacAddress|LinkSpeed|
|-----|--------------------|-------|-----|----------|---------|
|
|テスト-40 G-1|Mellanox connectx-3 Pro イーサネット アダプター|11|アップ|E4-1D-2D-07-43-D0|40 gb/秒|

IP アドレスなど、追加のアダプターのプロパティを取得するのにには、次のコマンドのいずれかを使用します。

    Get-NetIPAddress -InterfaceAlias "Test-40G-1"

    Get-NetIPAddress -InterfaceAlias "TEST-40G-1" | Where-Object {$_.AddressFamily -eq "IPv4"} | fl InterfaceAlias,IPAddress
    
これらのコマンドの例の結果を次に示します。

|パラメーター|値|
|---------|-----|
|
|Ip アドレス| 192.168.1.3|
|InterfaceIndex|11|
|InterfaceAlias|テスト-40 G-1|
|アドレスファ ・ リ|IPv4|
|種類| ユニキャスト|
|PrefixLength|24|

### <a name="verify-that-nic-team-member-has-a-valid-ip-address"></a>有効な IP アドレスを NIC チームのメンバーがあることを確認します。

ことができますこのステップを使用していることを確認他の NIC チームもスイッチ埋め込みチーム \(SET\) メンバー物理 Nic \(pNICs\) も有効な IP アドレス。

この手順では、個別のサブネットを使用することができます \ (xxx.xxx**。2**.xxx vs xxx.xxx します。**1**. xxx\)、このアダプターから宛先に送信しやすくします。 

それ以外の場合、両方 pNICs を見つけるには、同じサブネット上、インターフェイス間で、Windows TCP/IP スタックの負荷を分散し、単純な検証が複雑になります。

次の Windows PowerShell コマンドを使用すると、2 つ目のネットワーク アダプターのプロパティを取得します。

    Get-NetAdapter -Name "Test-40G-2" | ft -AutoSize

このコマンドの結果の例を次に示します。

|名 |InterfaceDescription |ifIndex |ステータス |MacAddress |LinkSpeed|
|----|--------------------|-------|------|----------|---------|
|
|テスト-40 G-2 |Mellanox connectx-3 Pro イーサネット A.... \ #2 |13 |アップ |E4-1D-2D-07-40-70 |40 gb/秒|

IP アドレスなど、追加のアダプターのプロパティを取得するのにには、次のコマンドのいずれかを使用します。

    Get-NetIPAddress -InterfaceAlias "Test-40G-2"

    Get-NetIPAddress -InterfaceAlias "Test-40G-2" | Where-Object {$\_.AddressFamily -eq "IPv4"} | fl InterfaceAlias,IPAddress

これらのコマンドの例の結果を次に示します。

|パラメーター|値|
|---------|-----|
|
|Ip アドレス|192.168.2.3|
|InterfaceIndex|13|
|InterfaceAlias|テスト-40 G-2|
|アドレスファ ・ リ|IPv4|
|種類|ユニキャスト|
|PrefixLength|24|

### <a name="verify-that-additional-nics-have-valid-ip-addresses"></a>追加の Nic が有効な IP アドレスがあることを確認します。

この手順を使用すると、その他の NIC が有効な IP アドレスを持っていることを確認します。

この手順では、個別のサブネットを使用することができます \ (xxx.xxx**。2**.xxx vs xxx.xxx します。**1**. xxx\)、このアダプターから宛先に送信しやすくします。 

それ以外の場合、両方 pNICs を見つけるには、同じサブネット上、インターフェイス間で、Windows TCP/IP スタックの負荷を分散し、単純な検証が複雑になります。

次の Windows PowerShell コマンドを使用すると、2 つ目のネットワーク アダプターのプロパティを取得します。

    Get-NetAdapter -Name "Test-40G-2" | ft -AutoSize

このコマンドの結果の例を次に示します。

|名 |InterfaceDescription |ifIndex |ステータス |MacAddress |LinkSpeed|
|----|--------------------|-------|------|----------|---------|
|
|テスト-40 G-2 |Mellanox connectx-3 Pro イーサネット A.... \ #2 |13 |アップ |E4-1D-2D-07-40-70 |40 gb/秒|

IP アドレスなど、追加のアダプターのプロパティを取得するのにには、次のコマンドのいずれかを使用します。
    
    Get-NetIPAddress -InterfaceAlias "Test-40G-2"

    Get-NetIPAddress -InterfaceAlias "Test-40G-2" | Where-Object {$_.AddressFamily -eq "IPv4"} | fl InterfaceAlias,IPAddress

これらのコマンドの例の結果を次に示します。

|パラメーター|値|
|---------|-----|
|
|Ip アドレス|192.168.2.3|
|InterfaceIndex|13|
|InterfaceAlias|テスト-40 G-2|
|アドレスファ ・ リ|IPv4|
|種類|ユニキャスト|
|PrefixLength|24|

### <a name="ensure-that-source-and-destination-can-communicate"></a>移行元と移行先が通信できることを確認します。

この手順を使用するを双方向通信を確認 \ (移行先およびその逆を行うを両方 \ ping ソースから)。  次の例では、**テスト NetConnection**場合は、使用することができますが、Windows PowerShell コマンドを使用、**ping**コマンド。 

    Test-NetConnection 192.168.1.5

このコマンドの結果の例を次に示します。

|パラメーター|値|
|---------|-----|
|
|コンピューター名|192.168.1.5|
|RemoteAddress|192.168.1.5|
|InterfaceAlias|テスト-40 G-1|
|発信元アドレス|192.168.1.3|
|PingSucceeded|False|
|PingReplyDetails \(RTT\)|0 ms|

場合によっては、このテストを正常に実行するセキュリティが強化された Windows ファイアウォールを無効にする必要があります。 ファイアウォールを無効にした場合は、セキュリティに留意してくださいし、構成が、組織のセキュリティ要件を満たしていることを確認します。

次のコマンド例では、すべてのファイアウォール プロファイルを無効にすることができます。

    Set-NetFirewallProfile -All -Enabled False
    
ファイアウォールを無効にした後、次のコマンドを使用して接続をテストすることができます。

    Test-NetConnection 192.168.1.5

このコマンドの結果の例を次に示します。

|パラメーター|値|
|---------|-----|
|
|コンピューター名|192.168.1.5|
|RemoteAddress|192.168.1.5|
|InterfaceAlias|テスト-40 G-1|
|発信元アドレス|192.168.1.3|
|PingSucceeded|False|
|PingReplyDetails \(RTT\)|0 ms|

### <a name="verify-connectivity-for-additional-nics"></a>追加の Nic の接続を検証します。

このステップでは、NIC またはセットのチームに含まれているすべての後続 pNICs の前の手順を繰り返すことができます。

次のコマンドを使用して、接続をテストすることができます。
    
    Test-NetConnection 192.168.2.5

このコマンドの結果の例を次に示します。

|パラメーター|値|
|---------|-----|
|
|コンピューター名|192.168.2.5|
|RemoteAddress|192.168.2.5|
|InterfaceAlias|テスト-40 G-2|
|発信元アドレス|192.168.2.3|
|PingSucceeded|False|
|PingReplyDetails \(RTT\)|0 ms|


## <a name="configure-vlans"></a>Vlan を構成します。

Nic がこの手順で**アクセス**モード。 ただしこのガイドの後半で Hyper-V 仮想スイッチ \(vSwitch\) を作成するときに、VLAN のプロパティは、vSwitch ポート レベルで適用されます。 

スイッチは、複数の Vlan をホストできる、ので、ラックの上部 \(ToR\) 物理スイッチそのポートをトランク モードで構成する必要があります。

スイッチのトランク モードを構成する方法の詳細については、ToR スイッチのドキュメントを参照してください。

以下に示す各を VLAN 101 を持つ 2 つのネットワーク アダプターを 2 つの Hyper-V ホストと、ネットワーク アダプターのプロパティで構成されている VLAN 102 します。

![仮想ローカル エリア ネットワークを構成します。](../../media/Converged-NIC/2-datacenter-configure-vlans.jpg)

### <a name="configure-the-vlan-ids-for-both-nics"></a>両方の Nic の VLAN ID を構成します。

このステップを使用して、Hyper-V ホストにインストールされている Nic の VLAN ID を構成することができます。

に従って、Institute of Electrical と標準のネットワーク Electronics Engineers \(IEEE\) 物理サービスの品質 \(QoS\) プロパティ NIC 動作、802.1 q 内に埋め込まれた、802.1 p ヘッダーで VLAN ID を構成するときに \(VLAN\) ヘッダー

#### <a name="configure-nic-test-40g-1"></a>NIC テスト 40 G 1 を構成します。

次のコマンドでは、構成の結果として得られる表示し、最初の NIC、テスト-40 G-1 の VLAN ID を構成します。

    
    Set-NetAdapterAdvancedProperty -Name "Test-40G-1" -RegistryKeyword VlanID -RegistryValue "101"
    Get-NetAdapterAdvancedProperty -Name "Test-40G-1" | Where-Object {$_.RegistryKeyword -eq "VlanID"} | ft -AutoSize
    
このコマンドの結果の例を次に示します。

|名 |DisplayName| 値| RegistryKeyword |RegistryValue|
|----|-----------|------------|---------------|-------------|
|
|テスト-40 G-1|VLAN ID|101|VlanID|{101}|


VLAN ID は、効果のネットワーク アダプターの実装から独立して、次のコマンドを使用して、ネットワーク アダプターを再起動することを確認します。

    Restart-NetAdapter -Name "Test-40G-1"

次のコマンドを使用するには、ネットワーク アダプタの状態があることを確認する**を**続行する前にします。

    Get-NetAdapter -Name "Test-40G-1" | ft -AutoSize

このコマンドの結果の例を次に示します。

|名|InterfaceDescription|ifIndex| ステータス|MacAddress|LinkSpeed|
|----|--------------------|-------|------|----------| ---------|
|
|テスト-40 G-1|Mellanox connectx-3 Pro イーサネット Ada.|11|アップ|E4-1D-2D-07-43-D0|40 gb/秒|

#### <a name="configure-nic-test-40g-2"></a>NIC 2 40 G テストを構成します。

次のコマンドでは、構成の結果として得られる表示し、2 つ目の NIC、テスト-40 G-2 の VLAN ID を構成します。

    
    Set-NetAdapterAdvancedProperty -Name "Test-40G-2" -RegistryKeyword VlanID -RegistryValue "102"
    Get-NetAdapterAdvancedProperty -Name "Test-40G-2" | Where-Object {$_.RegistryKeyword -eq "VlanID"} | ft -AutoSize
    

このコマンドの結果の例を次に示します。

|名 |DisplayName| 値| RegistryKeyword |RegistryValue|
|----|-----------|------------|---------------|-------------|
|
|テスト-40 G-2|VLAN ID|102|VlanID|{102}|

VLAN ID は、効果のネットワーク アダプターの実装から独立して、次のコマンドを使用して、ネットワーク アダプターを再起動することを確認します。

`Restart-NetAdapter -Name "Test-40G-2"  `              

次のコマンドを使用するには、ネットワーク アダプタの状態があることを確認する**を**続行する前にします。

    Get-NetAdapter -Name "Test-40G-1" | ft -AutoSize

このコマンドの結果の例を次に示します。

|名|InterfaceDescription|ifIndex| ステータス|MacAddress|LinkSpeed|
|----|--------------------|-------|------|----------| ---------|
|
|テスト-40 G-2 |Mellanox connectx-3 Pro イーサネット Ada. |11 |アップ |E4-1D-2D-07-43-D1 |40 gb/秒|


### <a name="verify-connectivity"></a>接続を確認します。

このセクションを使用すると、ネットワーク アダプターを再起動した後、接続を確認します。 両方のアダプターに VLAN タグを適用した後、接続を確認できます。 接続に失敗した場合は、スイッチ、同じ VLAN の VLAN 構成または移行先への参加を検査できます。 

>[!IMPORTANT]
>前のセクションの手順を実行した後は、数秒デバイスを再起動し、ネットワーク上で利用可能になるがかかる場合があります。

#### <a name="verify-connectivity-for-nic-test-40g-1"></a>NIC テスト-40 G-1 の接続を確認します。

最初の NIC の接続を確認するには、次のコマンドを実行できます。

    Test-NetConnection 192.168.1.5
    
このコマンドの結果の例を次に示します。

|パラメーター|値|
|---------|-----|
|
|コンピューター名|192.168.1.5|
|RemoteAddress|192.168.1.5|
|InterfaceAlias|テスト-40 G-1|
|発信元アドレス|192.168.1.5|
|PingSucceeded|場合は true。|
|PingReplyDetails \(RTT\)|0 ms|

#### <a name="verify-connectivity-for-nic-test-40g-2"></a>NIC テスト-40 G-2 の接続を確認します。

このセクションを使用すると、NIC テスト-40 G-2 の接続をテストします。

次のコマンドを使用するには 2 つ目の NIC の接続をテストするには
    
    Test-NetConnection 192.168.2.5
    
このコマンドの結果の例を次に示します。

|パラメーター|値|
|---------|-----|
|
|コンピューター名|192.168.2.5|
|RemoteAddress|192.168.2.5|
|InterfaceAlias|テスト-40 G-2|
|発信元アドレス|192.168.2.3|
|PingSucceeded|場合は true。|
|PingReplyDetails \(RTT\)|0 ms|

A**テスト NetConnection**またはを実行する直後後に発生した ping 障害**再起動 NetAdapter**は珍しくありません、ので、ネットワーク アダプターを完全に初期化するまで待機し、もう一度やり直してください。

VLAN 101 接続するには、VLAN 102 接続が動作しない場合は、問題があります、スイッチが必要な VLAN のポートのトラフィックを許可するように構成する必要があること。 これを一時的に障害が発生したアダプターに VLAN 101 を設定し、接続のテストを繰り返すことで確認できます。

## <a name="configure-quality-of-service-qos"></a>サービス \(QoS\) の品質を構成します。

次の手順では、データ センター ブリッジング \(DCB\) Windows Server 2016 の機能を最初にインストールすることを必要とするサービスの品質 \(QoS\) を構成します。

次の図は、前の手順で Vlan を正常に構成した後、Hyper-V ホストを示しています。

![サービスの品質を構成します。](../../media/Converged-NIC/3-datacenter-configure-qos.jpg)

### <a name="install-data-center-bridging-dcb"></a>データ センター ブリッジング \(DCB\) をインストールします。

このステップを使用して、インストールして DCB を有効にすることができます。 ほとんどの場合、この手順は省略 iWarp 実装では、がファブリックの規模でクロス ラック シナリオなど必要があります。

次のコマンドは、DCB を使用して、Hyper-V ホストの各インストールを使用することができます。 

    Install-WindowsFeature Data-Center-Bridging

このコマンドの結果の例を次に示します。

|成功 |再起動が必要です。 |終了コード|機能の結果|
|------- |-------------- |--------- |-------------- |
|
|場合は true。 |違います |成功| {データ センター ブリッジング}|

### <a name="set-the-qos-policies-for-smb-direct"></a>SMB ダイレクトの QoS ポリシーを設定します。 

次のコマンドを使用して、SMB ダイレクトの QoS ポリシーを構成することができます。

    New-NetQosPolicy "SMB" -NetDirectPortMatchCondition 445 -PriorityValue8021Action 3

このコマンドの結果の例を次に示します。

|パラメーター|値|
|---------|-----|
|
|名 |SMB|
|所有者|グループ ポリシー \(Machine\)|
|NetworkProfile|すべての|
|優先順位|127|
|JobObject|&nbsp;| 
|NetDirectPort|445
|PriorityValue|3

### <a name="set-policies-for-other-traffic-on-the-interface"></a>他のトラフィックをインターフェイス上のポリシーを設定します。 

次のコマンドを使用して、追加の QoS ポリシーを設定することができます。

    New-NetQosPolicy "DEFAULT" -Default -PriorityValue8021Action 0
 
このコマンドの結果の例を次に示します。

|パラメーター|値|
|---------|-----|
|
|名 | 既定値|
|所有者|グループ ポリシー \(Machine\)|
|NetworkProfile|すべての|
|優先順位|127|
|テンプレート| 既定値|
|JobObject| &nbsp;|
|PriorityValue|0|

### <a name="turn-on-flow-control-for-smb"></a>SMB のフロー制御を有効にします。 

SMB のフロー制御を有効にして、結果を表示する、次のコマンドを使用することができます。

    Enable-NetQosFlowControl -priority 3
    Get-NetQosFlowControl

このコマンドの結果の例を次に示します。

|優先順位|有効になっています。|PolicySet|IfIndex|IfAlias|
|---------|-----|--------- |-------| -------|
|
|0 |False |グローバル|&nbsp;|&nbsp;|
|1 |False |グローバル|&nbsp;|&nbsp;|
|2 |False |グローバル|&nbsp;|&nbsp;|
|3 |場合は true。 |グローバル|&nbsp;|&nbsp;|
|4 |False |グローバル|&nbsp;|&nbsp;|
|5 |False |グローバル|&nbsp;|&nbsp;|
|6 |False |グローバル|&nbsp;|&nbsp;|
|7 |False |グローバル|&nbsp;|&nbsp;|

結果では、これらの結果が一致しない 3 以外の項目がある有効な値が True のため、次の手順を実行する必要があります。 結果、これらの例の結果の一致、唯一の項目 3 有効値が True の場合は、次を実行する必要はありません、ステップ実行し、下にスキップできる**を有効にするために QoS をターゲットと移行先ネットワーク アダプター**します。

### <a name="ensure-flow-control-is-disabled-for-other-traffic-classes-optional"></a>その他のトラフィック クラス \(Optional\) のフロー制御が無効になっていることを確認します。

この手順を実行する必要はありません**FlowControl** 0,1,2,4,5,6、および 7 トラフィック クラスを無効になっています。

場合**FlowControl** 3 よりも他のクラスのすべてのトラフィックに対して既に有効になって \ (0,1,2,4,5,6、および 7\)、無効にする必要があります**FlowControl**これらのクラス。 

>[!NOTE]
>複雑な構成は、下にあるその他のトラフィック クラスをただし、このシナリオは、このガイドの範囲外のフロー制御を必要があります。

トラフィック クラス 0,1,2,4,5,6、および 7 での SMB のフロー制御を無効にして、結果を表示するのには、次のコマンドを使用できます。

    Disable-NetQosFlowControl -priority 0,1,2,4,5,6,7
    Get-NetQosFlowControl

このコマンドの結果の例を次に示します。

|優先順位|有効になっています。|PolicySet|IfIndex|IfAlias|
|---------|-----|--------- |-------| -------|
|
|0 |False |グローバル|&nbsp;|&nbsp;|
|1 |False |グローバル|&nbsp;|&nbsp;|
|2 |False |グローバル|&nbsp;|&nbsp;|
|3 |場合は true。 |グローバル|&nbsp;|&nbsp;|
|4 |False |グローバル|&nbsp;|&nbsp;|
|5 |False |グローバル|&nbsp;|&nbsp;|
|6 |False |グローバル|&nbsp;|&nbsp;|
|7 |False |グローバル|&nbsp;|&nbsp;|

### <a name="enable-qos-for-the-local-and-destination-network-adapters"></a>ローカルと移行先ネットワーク アダプターに対して QoS を有効にします。 

この手順では、ローカルと宛先の両方のネットワーク アダプターの QoS を有効にできます。 これらのコマンドは、Hyper-V ホストの両方で実行することを確認します。

#### <a name="enable-qos-for-nic-test-40g-1"></a>NIC テスト 40 G 1 の QoS を有効にします。

次のコマンドを使用して、QoS を有効にして、構成の結果を表示することができます。

    Enable-NetAdapterQos -InterfaceAlias "Test-40G-1"
    Get-NetAdapterQos -Name "Test-40G-1"

このコマンドの結果の例を次に示します。

**名前**: test1 40 G**有効になっている**: True**機能**:   

|パラメーター|ハードウェア|現在の|
|---------|--------|-------|
|
|MacSecBypass|サポートされて|サポートされて|
|DcbxSupport|[なし]|[なし]|
|NumTCs(Max/ETS/PFC)|8/8/8|8/8/8|
 
**OperationalTrafficClasses**: 

|TC|TSA|帯域幅|優先順位|
|----|-----|--------|-------|
|
|0| 厳密です|&nbsp;|0-7|

**OperationalFlowControl**: 有効になっている 3 の優先順位**OperationalClassifications**:

|プロトコル|/ポートの種類|優先順位|
|--------|---------|--------|
|
|既定値|&nbsp;|0|
|NetDirect| 445|3|

#### <a name="enable-qos-for-nic-test-40g-2"></a>NIC テスト-40 G-2 の QoS を有効にします。

次のコマンドを使用して、QoS を有効にして、構成の結果を表示することができます。

    Enable-NetAdapterQos -InterfaceAlias "Test-40G-2"
    Get-NetAdapterQos -Name "Test-40G-2"

 
このコマンドの結果の例を次に示します。

**名前**: テスト-40 G-2**有効になっている**: True**機能**:   

|パラメーター|ハードウェア|現在の|
|---------|--------|-------|
|
|MacSecBypass|サポートされて|サポートされて|
|DcbxSupport|[なし]|[なし]|
|NumTCs(Max/ETS/PFC)|8/8/8|8/8/8|
 
**OperationalTrafficClasses**: 

|TC|TSA|帯域幅|優先順位|
|----|-----|--------|-------|
|
|0| 厳密です|&nbsp;|0-7|

**OperationalFlowControl**: 有効になっている 3 の優先順位**OperationalClassifications**:

|プロトコル|/ポートの種類|優先順位|
|--------|---------|--------|
|
|既定値|&nbsp;|0|
|NetDirect| 445|3|


### <a name="allocate-50-of-the-bandwidth-reservation-to-smb-direct-rdma"></a>SMB ダイレクト \(RDMA\) に帯域幅予約の 50% を割り当てる

SMB ダイレクトに帯域幅予約の半分を割り当てるには、次のコマンドを使用できます。

    New-NetQosTrafficClass "SMB" -priority 3 -bandwidthpercentage 50 -algorithm ETS

このコマンドの結果の例を次に示します。

|名|アルゴリズム |Bandwidth(%)| 優先順位 |PolicySet |IfIndex |IfAlias |
|----|---------| ------------ |--------| ---------|------- |------- |
|
|SMB | ETS     | 50 |3 |グローバル |&nbsp;|&nbsp;|                                      
 
次のコマンドを使用して、帯域幅予約情報を表示することができます。

    Get-NetQosTrafficClass | ft -AutoSize

このコマンドの結果の例を次に示します。
 
|名|アルゴリズム |Bandwidth(%)| 優先順位 |PolicySet |IfIndex |IfAlias |
|----|---------| ------------ |--------| ---------|------- |------- |
|
|[既定値]| ETS|50 |0-2,4-7|  グローバル|&nbsp;|&nbsp;| 
SMB |ETS|50 |3 |グローバル|&nbsp;|&nbsp;| 

### <a name="create-traffic-classes-for-tenant-ip-traffic-optional"></a>IP トラフィックのテナントのトラフィック クラスを作成する \(optional\)

この手順を使用して、テナント IP トラフィックの 2 つの追加トラフィック クラスを作成することができます。 

次の例のコマンドを実行する場合は、したい場合に、"IP1"と"IP2"の値を省略できます。

    New-NetQosTrafficClass "IP1" -Priority 1 -bandwidthpercentage 10 -algorithm ETS

このコマンドの結果の例を次に示します。

|名|アルゴリズム |Bandwidth(%)| 優先順位 |PolicySet |IfIndex |IfAlias |
|----|---------| ------------ |--------| ---------|------- |------- |
|
|IP1 |ETS |10 |1 |グローバル|&nbsp;|&nbsp;|


    New-NetQosTrafficClass "IP2" -Priority 2 -bandwidthpercentage 10 -algorithm ETS

このコマンドの結果の例を次に示します。

|名|アルゴリズム |Bandwidth(%)| 優先順位 |PolicySet |IfIndex |IfAlias |
|----|---------| ------------ |--------| ---------|------- |------- |
|
|IP2 |ETS |10 |2 |グローバル|&nbsp;|&nbsp;|

次のコマンドを使用して、QoS トラフィック クラスを表示することができます。

    Get-NetQosTrafficClass | ft -AutoSize

このコマンドの結果の例を次に示します。

|名|アルゴリズム |Bandwidth(%)| 優先順位 |PolicySet |IfIndex |IfAlias |
|----|---------| ------------ |--------| ---------|------- |------- |
|
|[既定値] |ETS |30 |0,4-7 |グローバル|&nbsp;|&nbsp;|
|SMB |ETS |50 |3 |グローバル|&nbsp;|&nbsp;|
|IP1 |ETS |10 |1 |グローバル|&nbsp;|&nbsp;|
|IP2 |ETS |10 |2 |グローバル|&nbsp;|&nbsp;|

## <a name="configure-debugger-optional"></a>デバッガー \(Optional\) を構成します。

このステップを使用して、デバッガーを構成することができます。

既定では、接続されているデバッガーは NetQos をブロックします。 デバッガーを上書きし、結果を表示するには、次のコマンドを使用できます。

    Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 –Force
    
    Get-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" | ft AllowFlowControlUnderDebugger

このコマンドの結果の例を次に示します。

    AllowFlowControlUnderDebugger
    -----------------------------
    1

## <a name="test-rdma-mode-1"></a>RDMA \(Mode 1\) をテストします。

このステップを使用して、vSwitch を作成および RDMA \(Mode 2\) に移行する前に、ファブリックが正しく構成されていることを確認することができます。

次の図は、Hyper-V ホストの現在の状態を示しています。

![RDMA のテスト](../../media/Converged-NIC/4-datacenter-test-rdma.jpg)

RDMA 構成を確認するには、次のコマンドを実行できます。

    Get-NetAdapterRdma | ft -AutoSize

このコマンドの結果の例を次に示します。

|名 |InterfaceDescription |有効になっています。|
|----|--------------------|-------|
|
|テスト-40 G-1| Mellanox ConnectX 4 VPI Adapter #2 |場合は true。|
|テスト-40 G-2| Mellanox ConnectX 4 VPI アダプター |場合は true。|


### <a name="determine-the-ifindex-value-of-your-target-adapter"></a>対象アダプターの ifIndex 値を決定します。

次のコマンドを使用すると、ターゲット アダプターの ifIndex 値を検出します。

    Get-NetIPConfiguration -InterfaceAlias "TEST*" | ft InterfaceAlias,InterfaceIndex,IPv4Address

このコマンドの結果の例を次に示します。

|InterfaceAlias |InterfaceIndex |IPv4Address|
|-------------- |-------------- |-----------|
|テスト-40 G-1 |14 |{192.168.1.3}|
|テスト-40 G-2 | 13 |{192.168.2.3}|

### <a name="download-diskspdexe-and-a-powershell-script"></a>DiskSpd.exe と PowerShell スクリプトをダウンロードします。

続けるには、まず、次の項目をダウンロードする必要があります。

- DiskSpd.exe ユーティリティをダウンロードして抽出 C:\TEST\ にユーティリティ[http://tinyurl.com/z68h3rc](http://tinyurl.com/z68h3rc)

- C:\TEST\ に Test-RDMA powershell スクリプトをダウンロードします。[https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1](https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1)

### <a name="run-the-powershell-script"></a>PowerShell スクリプトを実行します。

Test-Rdma .ps1 Windows PowerShell スクリプトを実行すると、同じ vlan リモート アダプターの IP アドレスと共に、スクリプトに ifIndex 値を渡すことができます。

次のコマンド例を使用すると、ネットワーク アダプター 192.168.1.5 で、ifIndex 14 にスクリプトを実行します。
    
    C:\TEST\Test-RDMA.PS1 -IfIndex 14 -IsRoCE $true -RemoteIpAddress 192.168.1.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
    
    VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\\diskspd.exe
    VERBOSE: The adapter TEST-40G-1 is a physical adapter
    VERBOSE: Underlying adapter is RoCE. Checking if QoS/DCB/PFC is configured on each physical adapter(s)
    VERBOSE: QoS/DCB/PFC configuration is correct.
    VERBOSE: RDMA configuration is correct.
    VERBOSE: Checking if remote IP address, 192.168.1.5, is reachable.
    VERBOSE: Remote IP 192.168.1.5 is reachable.
    VERBOSE: Disabling RDMA on adapters that are not part of this test. RDMA will be enabled on them later.
    VERBOSE: Testing RDMA traffic now for. Traffic will be sent in a parallel job. Job details:
    VERBOSE: 0 RDMA bytes written per second
    VERBOSE: 0 RDMA bytes sent per second
    VERBOSE: 662979201 RDMA bytes written per second
    VERBOSE: 37561021 RDMA bytes sent per second
    VERBOSE: 1023098948 RDMA bytes written per second
    VERBOSE: 8901349 RDMA bytes sent per second
    VERBOSE: Enabling RDMA on adapters that are not part of this test. RDMA was disabled on them prior to sending RDMA traffic.
    VERBOSE: RDMA traffic test SUCCESSFUL: RDMA traffic was sent to 192.168.1.5
    

>[!NOTE]
>RDMA のトラフィックが失敗した場合、RoCE 大文字と小文字を具体的には、ホストの設定が一致している適切な PFC/ETS 設定に対して、ToR スイッチの構成を参照してください。 参照の値は、このドキュメントの QoS のセクションを参照してください。

### <a name="determine-the-ifindex-value-of-your-target-adapter"></a>対象アダプターの ifIndex 値を決定します。

次のコマンドを使用すると、ターゲット アダプターの ifIndex 値を検出します。

    Get-NetIPConfiguration -InterfaceAlias "TEST*" | ft InterfaceAlias,InterfaceIndex,IPv4Address

このコマンドの結果の例を次に示します。

|InterfaceAlias |InterfaceIndex |IPv4Address|
|-------------- |-------------- |-----------|
|テスト-40 G-1 |14 |{192.168.1.3}|
|テスト-40 G-2 | 13 |{192.168.2.3}|

次のコマンド例を使用して、13、ifIndex で 192.168.2.5 のネットワーク アダプターのスクリプトを実行することができます。

    
    C:\TEST\Test-RDMA.PS1 -IfIndex 13 -IsRoCE $true -RemoteIpAddress 192.168.2.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
    VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\\diskspd.exe
    VERBOSE: The adapter TEST-40G-2 is a physical adapter
    VERBOSE: Underlying adapter is RoCE. Checking if QoS/DCB/PFC is configured on each physical adapter(s)
    VERBOSE: QoS/DCB/PFC configuration is correct.
    VERBOSE: RDMA configuration is correct.
    VERBOSE: Checking if remote IP address, 192.168.2.5, is reachable.
    VERBOSE: Remote IP 192.168.2.5 is reachable.
    VERBOSE: Disabling RDMA on adapters that are not part of this test. RDMA will be enabled on them later.
    VERBOSE: Testing RDMA traffic now for. Traffic will be sent in a parallel job. Job details:
    VERBOSE: 0 RDMA bytes written per second
    VERBOSE: 0 RDMA bytes sent per second
    VERBOSE: 541185606 RDMA bytes written per second
    VERBOSE: 34821478 RDMA bytes sent per second
    VERBOSE: 954717307 RDMA bytes written per second
    VERBOSE: 35040816 RDMA bytes sent per second
    VERBOSE: Enabling RDMA on adapters that are not part of this test. RDMA was disabled on them prior to sending RDMA traffic.
    VERBOSE: RDMA traffic test SUCCESSFUL: RDMA traffic was sent to 192.168.2.5
    

## <a name="create-a-hyper-v-virtual-switch"></a>Hyper-V 仮想スイッチを作成します。

このセクションを使用すると、Hyper-V ホスト上で Hyper-V 仮想スイッチ \(vSwitch\) を作成します。

次の図は、vSwitch で Hyper-V ホスト 1 を示しています。

![Hyper-V 仮想スイッチを作成します。](../../media/Converged-NIC/5-datacenter-create-vswitch.jpg)

### <a name="create-a-vswitch-in-switch-embedded-teaming-set-mode"></a>スイッチ埋め込みチーミング \(SET\) モードで、vSwitch を作成します。

次のコマンド例を使用するには名前付きセット スイッチ非依存チームを作成する**VMSTEST**を Hyper-V ホスト 1 です。 このコマンドでセット チームにテスト-40 G-1 とテスト-40 G-2 は、このコンピューター上のネットワーク アダプターの両方に追加されます。
    
    New-VMSwitch –Name "VMSTEST" –NetAdapterName "TEST-40G-1","TEST-40G-2" -EnableEmbeddedTeaming $true -AllowManagementOS $true
    
このコマンドの結果の例を次に示します。

|名 |SwitchType |NetAdapterInterfaceDescription|
|---- |---------- |------------------------------|
|VMSTEST |外部 |チーム化されたインターフェイス|

セット内の物理アダプターのチームを表示するのには、このコマンドを使用することができます。

    Get-VMSwitchTeam -Name "VMSTEST" | fl

このコマンドの結果の例を次に示します。

**名前**: VMSTEST **Id**: ad9bb542-dda2-4450-a00e-f96d44bdfbec **NetAdapterInterfaceDescription**: {Mellanox connectx-3 Pro イーサネット アダプター, Mellanox connectx-3 Pro イーサネット アダプター #2} **TeamingMode**: SwitchIndependent **LoadBalancingAlgorithm**: 動的

#### <a name="display-two-views-of-the-host-vnic"></a>ホスト vNIC の 2 つのビューを表示します。

次の 2 つのコマンドは、ホスト vNIC の 2 つのビューを使用できます。

このコマンドを使用すると、ホスト vNIC のプロパティを表示します。

    Get-NetAdapter

このコマンドの結果の例を次に示します。

|Name |InterfaceDescription | ifIndex |ステータス |MacAddress |LinkSpeed | |------|---|---|---|---| | | vEthernet (VMSTEST) |Hyper-V仮想イーサネット アダプター #2 | 28 |セットアップ |E4-1D-2D-07-40-71|80 Gbps |

このコマンドを使用すると、ホスト vNIC の他のプロパティを表示します。

    Get-VMNetworkAdapter -ManagementOS

このコマンドの結果の例を次に示します。

|名 |IsManagementOs |VMName |SwitchName |MacAddress |ステータス |Ip アドレス|
|----|--------------|------|----------|----------|------|-----------|
|
|VMSTEST|場合は true。 |VMSTEST |E41D2D074071| {OK}|&nbsp;|

#### <a name="test-the-network-connection-to-the-remote-vlan-101-adapter"></a>リモート VLAN 101 アダプターにネットワーク接続をテストします。

このコマンドを使用すると、リモート VLAN 101 アダプターへの接続をテストします。

`Test-NetConnection 192.168.1.5` 

このコマンドの結果の例を次に示します。

    WARNING: Ping to 192.168.1.5 failed -- Status: DestinationHostUnreachable
    
    ComputerName   : 192.168.1.5
    RemoteAddress  : 192.168.1.5
    InterfaceAlias : vEthernet (CORP-External-Switch)
    SourceAddress  : 10.199.48.170
    PingSucceeded  : False
    PingReplyDetails (RTT) : 0 ms
    
### <a name="reconfigure-vlans"></a>Vlan を再構成します。

物理 NIC からアクセス VLAN 設定を削除して、vSwitch を使用して VLANID を設定するのには、この手順を使用できます。

両方の自動タグ付け、正しくない VLAN ID を持つ出口トラフィックを防ぐために、アクセス VLAN 設定を削除し、アクセスの VLAN ID が一致しないトラフィックの受信をフィルター処理から必要があります。

次のコマンドを使用すると、アクセス VLAN 設定を削除します。
    
    Set-NetAdapterAdvancedProperty -Name "Test-40G-1" -RegistryKeyword VlanID -RegistryValue "0"
    Set-NetAdapterAdvancedProperty -Name "Test-40G-2" -RegistryKeyword VlanID -RegistryValue "0"
    

VSwitch の特定の Windows PowerShell コマンドを使用して VLANID を設定して、このアクションの結果を表示する、次のコマンドを使用することができます。

    
    Set-VMNetworkAdapterVlan -VMNetworkAdapterName "VMSTEST" -VlanId "101" -Access -ManagementOS
    Get-VMNetworkAdapterVlan -ManagementOS -VMNetworkAdapterName "VMSTEST"
    

このコマンドの結果の例を次に示します。

VMName VMNetworkAdapterName モード [vlanlist]
------ -------------------- ----   --------
       VMSTEST              Access 101     

ネットワーク接続をテストし、結果を表示するには、次のコマンドを使用できます。

    Test-NetConnection 192.168.1.5
    
    ComputerName   : 192.168.1.5
    RemoteAddress  : 192.168.1.5
    InterfaceAlias : vEthernet (VMSTEST)
    SourceAddress  : 192.168.1.3
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms
    

結果はのような例ではないと、メッセージで ping が失敗する場合は、"警告: 192.168.1.5 への Ping に失敗しました - 状態: DestinationHostUnreachable、""vEthernet (VMSTEST)"の次のコマンドを実行して、適切な IP アドレスがあることを確認します。

    
    Get-NetIPAddress -InterfaceAlias "vEthernet (VMSTEST)"
    

IP アドレスが設定されていない場合、次のコマンドを使用して、問題を修正し、アクションの結果を表示することができます。

    
    New-NetIPAddress -InterfaceAlias "vEthernet (VMSTEST)" -IPAddress 192.168.1.3 -PrefixLength 24
    
    IPAddress : 192.168.1.3
    InterfaceIndex: 37
    InterfaceAlias: vEthernet (VMSTEST)
    AddressFamily : IPv4
    Type  : Unicast
    PrefixLength  : 24
    PrefixOrigin  : Manual
    SuffixOrigin  : Manual
    AddressState  : Tentative
    ValidLifetime : Infinite ([TimeSpan]::MaxValue)
    PreferredLifetime : Infinite ([TimeSpan]::MaxValue)
    SkipAsSource  : False
    PolicyStore   : ActiveStore
    
#### <a name="rename-the-management-nic"></a>管理 NIC の名前を変更します。

このセクションを使用して、管理 NIC の名前を変更し、RDMA 用の別のホスト vNIC のインスタンスを後で使用できます。

管理 NIC の名前を変更し、いくつかの NIC のプロパティを表示するには、次のコマンドを実行することができます。

    Rename-VMNetworkAdapter -ManagementOS -Name “VMSTEST” -NewName “MGT”
    Get-VMNetworkAdapter -ManagementOS

このコマンドの結果の例を次に示します。

|名 |IsManagementOs |VMName |SwitchName |MacAddress |ステータス |Ip アドレス
|----|--------------|------|----------|----------|------|-----------|
|
|CORP の外部スイッチ |場合は true。 |&nbsp;|CORP の外部スイッチ |001B785768AA |{OK}|&nbsp;|
|管理 |場合は true。 |&nbsp;|VMSTEST |E41D2D074071 |{OK}|&nbsp;|

いくつか追加の NIC プロパティを表示するのには、次のコマンドを実行することができます。

    Get-NetAdapter

このコマンドの結果の例を次に示します。

|名 |InterfaceDescription |ifIndex |ステータス |MacAddress |LinkSpeed|
|----|--------------------|------|----------|---------|------|
|
|vEthernet (管理) |Hyper-V 仮想イーサネット アダプター #2 |28 |アップ | E4-1D-2D-07-40-71 |80 gb/秒|

## <a name="test-hyper-v-virtual-switch-rdma"></a>Hyper-V 仮想スイッチを RDMA をテストします。

次の図は、Hyper-V ホスト 1 vSwitch を含む、Hyper-V ホストの現在の状態を示しています。

![Hyper-V 仮想スイッチをテストします。](../../media/Converged-NIC/6-datacenter-test-vswitch-rdma.jpg)

### <a name="set-priority-tagging-on-the-host-vnic-to-complement-the-previous-vlan-settings"></a>以前の VLAN 設定を補完するためにホスト vNIC のタグ付け優先順位を設定します。

次の例のコマンドを使用して、ホスト vNIC のタグ付けの優先順位を設定し、アクションの結果を表示することができます。
    
    Set-VMNetworkAdapter -ManagementOS -Name "MGT" -IeeePriorityTag on
    Get-VMNetworkAdapter -ManagementOS -Name "MGT" | fl Name,IeeePriorityTag
    

    Name: MGT
    IeeePriorityTag : On
    
### <a name="create-two-host-vnics-for-rdma"></a>RDMA 用の 2 つのホスト Vnic を作成します。

次の例のコマンドを使用して、RDMA 用の 2 つのホスト Vnic を作成し、vSwitch VMSTEST に接続することができます。
    
    Add-VMNetworkAdapter –SwitchName "VMSTEST" –Name SMB1 –ManagementOS
    Add-VMNetworkAdapter –SwitchName "VMSTEST" –Name SMB2 –ManagementOS
    
管理 NIC プロパティを表示するのに次のコマンド例を使用することができます。
    
    Get-VMNetworkAdapter -ManagementOS
    
このコマンドの結果の例を次に示します。

|名 |IsManagementOs |VMName |SwitchName |MacAddress |ステータス |Ip アドレス|
|----|--------------|------|----------|----------|------|-----------|
|
|CORP の外部スイッチ |場合は true。 |CORP の外部スイッチ |001B785768AA|{OK} |&nbsp;| 
|管理 |場合は true。 |VMSTEST |E41D2D074071 |{OK} |&nbsp;|
|SMB1 |場合は true。 |VMSTEST |00155D30AA00 |{OK} |&nbsp;|
|SMB2 |場合は true。 |VMSTEST |00155D30AA01 |{OK} |&nbsp;|

### <a name="assign-an-ip-address-to-the-smb-host-vnics"></a>SMB ホスト Vnic に IP アドレスを割り当てる

このセクションを使用するにに割り当てる IP addressrd SMB ホスト Vnic vEthernet \(SMB1\) と vEthernet \(SMB2\) します。

テスト-40 G-1 とテスト-40 G-2 の物理アダプターでも、アクセス VLAN 101 および 102 が構成されているがあります。 このため、アダプターのトラフィックにタグを付けるし、ping が成功した場合します。

以前は、0、両方の pNIC VLAN ID を構成し、VLAN 101 VMSTEST vSwitch を設定します。 その後、引き続きは、管理 vNIC を使用して、リモート VLAN 101 アダプタに ping を実行できたにもかかわらず VLAN 102 メンバーは現在ありません。

アクセスの VLAN ID と一致しないので、次のコマンド例を使用して、両方の自動タグ付け、正しくない VLAN ID を持つ出口トラフィックを防止し、受信トラフィックをフィルタ リングすることを防ぐことは、物理 NIC からアクセス VLAN 設定を削除することができます。

インターフェイスの vEthernet (SMB1) への新しい IP アドレスを追加するでこれらの目標を達成する次のコマンド例を使用して、結果を表示できます。

    
    New-NetIPAddress -InterfaceAlias "vEthernet (SMB1)" -IPAddress 192.168.2.111 -PrefixLength 24
    
    IPAddress : 192.168.2.111
    InterfaceIndex: 40
    InterfaceAlias: vEthernet (SMB1)
    AddressFamily : IPv4
    Type  : Unicast
    PrefixLength  : 24
    PrefixOrigin  : Manual
    SuffixOrigin  : Manual
    AddressState  : Invalid
    ValidLifetime : Infinite ([TimeSpan]::MaxValue)
    PreferredLifetime : Infinite ([TimeSpan]::MaxValue)
    SkipAsSource  : False
    PolicyStore   : PersistentStore
    

次のコマンド例を使用して、リモート VLAN 102 アダプターをテストし、結果を表示することができます。
    
    Test-NetConnection 192.168.2.5 
    
    ComputerName   : 192.168.2.5
    RemoteAddress  : 192.168.2.5
    InterfaceAlias : vEthernet (SMB1)
    SourceAddress  : 192.168.2.111
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms
    
インターフェイス vEthernet の新しい IP アドレスを追加する、次の例のコマンドを使用することができます、\(SMB2\) し、結果を表示します。
    
    New-NetIPAddress -InterfaceAlias "vEthernet (SMB2)" -IPAddress 192.168.2.222 -PrefixLength 24 
    
    IPAddress : 192.168.2.222
    InterfaceIndex: 44
    InterfaceAlias: vEthernet (SMB2)
    AddressFamily : IPv4
    Type  : Unicast
    PrefixLength  : 24
    PrefixOrigin  : Manual
    SuffixOrigin  : Manual
    AddressState  : Invalid
    ValidLifetime : Infinite ([TimeSpan]::MaxValue)
    PreferredLifetime : Infinite ([TimeSpan]::MaxValue)
    SkipAsSource  : False
    PolicyStore   : PersistentStore
    
通信が確立されるため、もう一度接続をテストする必要はありません。

### <a name="place-the-rdma-host-vnics-on-vlan-102"></a>VLAN 102 に RDMA ホスト Vnic を配置します。

VLAN 102 に RDMA ホスト Vnic を割り当てるには、このセクションを使用できます。

「管理」ホスト vNIC は VLAN 101 上にある、ためには、既存の VLAN 102 に RDMA ホスト Vnic を配置し、アクションの結果を表示、次の例のコマンドを使用できます。

    
    Set-VMNetworkAdapterVlan -VMNetworkAdapterName "SMB1" -VlanId "102" -Access -ManagementOS
    Set-VMNetworkAdapterVlan -VMNetworkAdapterName "SMB2" -VlanId "102" -Access -ManagementOS
    
    Get-VMNetworkAdapterVlan -ManagementOS
    
    VMName VMNetworkAdapterName Mode VlanList
    ------ -------------------- ---- --------
       SMB1 Access   102 
       Mgt  Access   101 
       SMB2 Access   102 
       CORP-External-Switch Untagged
    
### <a name="inspect-the-mapping-of-smb1-and-smb2-to-the-underlying-physical-nics"></a>SMB1 のマッピングと SMB2 基になる物理 Nic を調べるには

このセクションを使用すると、SMB1 と SMB2 vSwitch チームの設定の下の基になる物理 Nic へのマッピングを検査します。  物理 Nic をホスト vNIC の関連付けは、ランダムな作成と破棄の中に再分配の対象とします。

このような状況での現在の関連付けを確認するのに間接のメカニズムを使用することができます。

SMB1 と SMB2 の MAC アドレスは、テスト-40 G-2 NIC チームのメンバーに関連付けられます。 これは、テスト-40 G-1 が関連付けられている SMB ホスト vNIC を可能になりしない、RDMA のトラフィックの使用率、リンク経由で、SMB ホスト vNIC にマップされるまでためには適していません。

次の例のコマンドを使用して、この情報を表示することができます。

    
    Get-NetAdapterVPort (Preferred)
    
    Get-NetAdapterVmqQueue
    
    Name   QueueID MacAddressVlanID Processor VmFriendlyName
    ----   ------- ---------------- --------- --------------
    TEST-40G-1 1   E4-1D-2D-07-40-71 1010:17
    TEST-40G-2 1   00-15-5D-30-AA-00 1020:17
    TEST-40G-2 2   00-15-5D-30-AA-01 1020:17
    
    Get-VMNetworkAdapter -ManagementOS
    
    Name IsManagementOs VMName SwitchName   MacAddress   Status IPAddresses
    ---- -------------- ------ ----------   ----------   ------ -----------
    CORP-External-Switch True  CORP-External-Switch 001B785768AA {Ok}  
    Mgt  True  VMSTEST  E41D2D074071 {Ok}  
    SMB1 True  VMSTEST  00155D30AA00 {Ok}  
    SMB2 True  VMSTEST  00155D30AA01 {Ok}  
    

以下のコマンドでは両方必要がありますを返さない情報マッピングを実行していないためです。
    
    Get-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName SMB1
    Get-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName SMB2
    
次の例のコマンドを使用すると、SMB1 と SMB2 は、操作の結果を表示してのに、物理 NIC チームのメンバーを個別にマップします。

>[!IMPORTANT]
>進む前に、この手順を完了するか、実装が失敗することを確認します。
    
    Set-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName "SMB1" -PhysicalNetAdapterName "Test-40G-1"
    Set-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName "SMB2" -PhysicalNetAdapterName "Test-40G-2"
    
    Get-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST
    
    NetAdapterName : Test-40G-1
    NetAdapterDeviceId : {BAA9A00F-A844-4740-AA93-6BD838F8CFBA}
    ParentAdapter  : VMInternalNetworkAdapter, Name = 'SMB1'
    IsTemplate : False
    CimSession : CimSession: .
    ComputerName   : 27-3145G0803
    IsDeleted  : False
    
    NetAdapterName : Test-40G-2
    NetAdapterDeviceId : {B7AB5BB3-8ACB-444B-8B7E-BC882935EBC8}
    ParentAdapter  : VMInternalNetworkAdapter, Name = 'SMB2'
    IsTemplate : False
    CimSession : CimSession: .
    ComputerName   : 27-3145G0803
    IsDeleted  : False
    
### <a name="confirm-the-mac-associations"></a>MAC の関連付けを確認します。

次の例のコマンドを使用すると、以前に作成した MAC の関連付けを確認します。
    
    Get-NetAdapterVmqQueue
    
    Name   QueueID MacAddressVlanID Processor VmFriendlyName
    ----   ------- ---------------- --------- --------------
    TEST-40G-1 1   E4-1D-2D-07-40-71 1010:17
    TEST-40G-1 2   00-15-5D-30-AA-00 1020:17
    TEST-40G-2 1   00-15-5D-30-AA-01 1020:17
    

両方のホスト Vnic が同じサブネット上に存在して、同じ VLAN ID \(102\) があるため、リモート システムからの通信を検証し、アクションの結果を表示できます。

>[!IMPORTANT]
>リモート コンピューターで、次のコマンドを実行します。

    
    Test-NetConnection 192.168.2.111
    
    
    ComputerName   : 192.168.2.111
    RemoteAddress  : 192.168.2.111
    InterfaceAlias : Test-40G-2
    SourceAddress  : 192.168.2.5
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms
    
    Test-NetConnection 192.168.2.222
    
    ComputerName   : 192.168.2.222
    RemoteAddress  : 192.168.2.222
    InterfaceAlias : Test-40G-2
    SourceAddress  : 192.168.2.5
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms 
    
        
    Set-VMNetworkAdapter -ManagementOS -Name "SMB1" -IeeePriorityTag on
    Set-VMNetworkAdapter -ManagementOS -Name "SMB2" -IeeePriorityTag on
    Get-VMNetworkAdapter -ManagementOS -Name "SMB*" | fl Name,SwitchName,IeeePriorityTag,Status
    
    Name: SMB1
    SwitchName  : VMSTEST
    IeeePriorityTag : On
    Status  : {Ok}
    
    Name: SMB2
    SwitchName  : VMSTEST
    IeeePriorityTag : On
    Status  : {Ok}
    

    Get-NetAdapterRdma -Name "vEthernet*" | sort Name | ft -AutoSize
    
    Name  InterfaceDescription Enabled
    ----  -------------------- -------
    vEthernet (SMB2)  Hyper-V Virtual Ethernet Adapter #4  False  
    vEthernet (SMB1)  Hyper-V Virtual Ethernet Adapter #3  False  
    vEthernet (MGT)   Hyper-V Virtual Ethernet Adapter #2  False   
    
    
    Enable-NetAdapterRdma -Name "vEthernet (SMB1)"
    Enable-NetAdapterRdma -Name "vEthernet (SMB2)"
    Get-NetAdapterRdma -Name "vEthernet*" | sort Name | fl *
    
    
    Name  InterfaceDescription Enabled
    ----  -------------------- -------
    vEthernet (SMB2)  Hyper-V Virtual Ethernet Adapter #4  True   
    vEthernet (SMB1)  Hyper-V Virtual Ethernet Adapter #3  True  
    vEthernet (MGT)   Hyper-V Virtual Ethernet Adapter #2  False
      

### <a name="validate-rdma-functionality-from-the-remote-system"></a>リモート システムからの RDMA 機能を検証します。

このセクションを使用すると、それによって vSwitch セット チームのメンバーである両方のアダプターをテスト、vSwitch には、ローカル システムに、リモート システムからの RDMA 機能を検証します。

両方のホスト Vnic \ (SMB1 と SMB2\) が VLAN 102 に割り当てられている、リモート システムで VLAN 102 アダプターを選択することができます。  

このプロセスで NIC テスト-40 G-2 は、RDMA SMB1 (192.168.2.111) と SMB2 (192.168.2.222)。

省略可能: このシステム上のファイアウォールを無効にする必要があります。  詳細については、ファブリックのポリシーを参照してください。

    
    Set-NetFirewallProfile -All -Enabled False
    
    Get-NetAdapterAdvancedProperty -Name "Test-40G-2"
    
    Name  DisplayNameDisplayValue   RegistryKeyword RegistryValue  
    ----  -----------------------   --------------- -------------  
    .
    .
    Test-40G-2VLAN ID102VlanID  {102} 
    
    Get-NetAdapter
    
    Name  InterfaceDescriptionifIndex Status   MacAddress LinkSpeed
    ----  --------------------------- ------   ---------- ---------
    Test-40G-2Mellanox ConnectX-3 Pro Ethernet A...#3   3 Up   E4-1D-2D-07-43-D140 Gbps
    
    
    Get-NetAdapterRdma
    
    Name  InterfaceDescription Enabled
    ----  -------------------- -------
    Test-40G-2Mellanox ConnectX-3 Pro Ethernet Adap... True   
    
    
    C:\TEST\Test-RDMA.PS1 -IfIndex 3 -IsRoCE $true -RemoteIpAddress 192.168.2.111 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
    VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\\diskspd.exe
    VERBOSE: The adapter Test-40G-2 is a physical adapter
    VERBOSE: Underlying adapter is RoCE. Checking if QoS/DCB/PFC is configured on each physical adapter(s)
    VERBOSE: QoS/DCB/PFC configuration is correct.
    VERBOSE: RDMA configuration is correct.
    VERBOSE: Checking if remote IP address, 192.168.2.111, is reachable.
    VERBOSE: Remote IP 192.168.2.111 is reachable.
    VERBOSE: Disabling RDMA on adapters that are not part of this test. RDMA will be enabled on them later.
    VERBOSE: Testing RDMA traffic now for. Traffic will be sent in a parallel job. Job details:
    VERBOSE: 34251744 RDMA bytes sent per second
    VERBOSE: 967346308 RDMA bytes written per second
    VERBOSE: 35698177 RDMA bytes sent per second
    VERBOSE: 976601842 RDMA bytes written per second
    VERBOSE: Enabling RDMA on adapters that are not part of this test. RDMA was disabled on them prior to sending RDMA traffic.
    VERBOSE: RDMA traffic test SUCCESSFUL: RDMA traffic was sent to 192.168.2.111
    
    
    C:\TEST\Test-RDMA.PS1 -IfIndex 3 -IsRoCE $true -RemoteIpAddress 192.168.2.222 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
    VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\\diskspd.exe
    VERBOSE: The adapter Test-40G-2 is a physical adapter
    VERBOSE: Underlying adapter is RoCE. Checking if QoS/DCB/PFC is configured on each physical adapter(s)
    VERBOSE: QoS/DCB/PFC configuration is correct.
    VERBOSE: RDMA configuration is correct.
    VERBOSE: Checking if remote IP address, 192.168.2.222, is reachable.
    VERBOSE: Remote IP 192.168.2.222 is reachable.
    VERBOSE: Disabling RDMA on adapters that are not part of this test. RDMA will be enabled on them later.
    VERBOSE: Testing RDMA traffic now for. Traffic will be sent in a parallel job. Job details:
    VERBOSE: 0 RDMA bytes written per second
    VERBOSE: 0 RDMA bytes sent per second
    VERBOSE: 485137693 RDMA bytes written per second
    VERBOSE: 35200268 RDMA bytes sent per second
    VERBOSE: 939044611 RDMA bytes written per second
    VERBOSE: 34880901 RDMA bytes sent per second
    VERBOSE: Enabling RDMA on adapters that are not part of this test. RDMA was disabled on them prior to sending RDMA traffic.
    VERBOSE: RDMA traffic test SUCCESSFUL: RDMA traffic was sent to 192.168.2.222
    
### <a name="test-for-rdma-traffic-from-the-local-to-the-remote-computer"></a>リモート コンピューターにローカルの RDMA のトラフィックのテスト

このセクションでは、リモート コンピューターに、RDMA のトラフィックが、ローカル コンピューターから送信されたことを確認できます。

テストし、トラフィック フローを表示、次の例のコマンドを使用することができます。

    
    Get-NetAdapter | ft –AutoSize
    
    Name  InterfaceDescriptionifIndex Status   MacAddress LinkSpeed
    ----  --------------------------- ------   ---------- ---------
    vEthernet (SMB2)  Hyper-V Virtual Ethernet Adapter #4  45 Up   00-15-5D-30-AA-0380 Gbps
    vEthernet (SMB1)  Hyper-V Virtual Ethernet Adapter #3  41 Up   00-15-5D-30-AA-0280 Gbps
    
    
    C:\TEST\Test-RDMA.PS1 -IfIndex 41 -IsRoCE $true -RemoteIpAddress 192.168.2.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
    VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\\diskspd.exe
    VERBOSE: The adapter vEthernet (SMB1) is a virtual adapter
    VERBOSE: Retrieving vSwitch bound to the virtual adapter
    VERBOSE: Found vSwitch: VMSTEST
    VERBOSE: Found the following physical adapter(s) bound to vSwitch: TEST-40G-1, TEST-40G-2
    VERBOSE: Underlying adapter is RoCE. Checking if QoS/DCB/PFC is configured on each physical adapter(s)
    VERBOSE: QoS/DCB/PFC configuration is correct.
    VERBOSE: RDMA configuration is correct.
    VERBOSE: Checking if remote IP address, 192.168.2.5, is reachable.
    VERBOSE: Remote IP 192.168.2.5 is reachable.
    VERBOSE: Disabling RDMA on adapters that are not part of this test. RDMA will be enabled on them later.
    VERBOSE: Testing RDMA traffic now for. Traffic will be sent in a parallel job. Job details:
    VERBOSE: 0 RDMA bytes written per second
    VERBOSE: 0 RDMA bytes sent per second
    VERBOSE: 0 RDMA bytes written per second
    VERBOSE: 15250197 RDMA bytes sent per second
    VERBOSE: 896320913 RDMA bytes written per second
    VERBOSE: 33947559 RDMA bytes sent per second
    VERBOSE: 912160540 RDMA bytes written per second
    VERBOSE: 34091930 RDMA bytes sent per second
    VERBOSE: Enabling RDMA on adapters that are not part of this test. RDMA was disabled on them prior to sending RDMA traffic.
    VERBOSE: RDMA traffic test SUCCESSFUL: RDMA traffic was sent to 192.168.2.5
    
    
    C:\TEST\Test-RDMA.PS1 -IfIndex 45 -IsRoCE $true -RemoteIpAddress 192.168.2.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
    VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\\diskspd.exe
    VERBOSE: The adapter vEthernet (SMB2) is a virtual adapter
    VERBOSE: Retrieving vSwitch bound to the virtual adapter
    VERBOSE: Found vSwitch: VMSTEST
    VERBOSE: Found the following physical adapter(s) bound to vSwitch: TEST-40G-1, TEST-40G-2
    VERBOSE: Underlying adapter is RoCE. Checking if QoS/DCB/PFC is configured on each physical adapter(s)
    VERBOSE: QoS/DCB/PFC configuration is correct.
    VERBOSE: RDMA configuration is correct.
    VERBOSE: Checking if remote IP address, 192.168.2.5, is reachable.
    VERBOSE: Remote IP 192.168.2.5 is reachable.
    VERBOSE: Disabling RDMA on adapters that are not part of this test. RDMA will be enabled on them later.
    VERBOSE: Testing RDMA traffic now for. Traffic will be sent in a parallel job. Job details:
    VERBOSE: 0 RDMA bytes written per second
    VERBOSE: 0 RDMA bytes sent per second
    VERBOSE: 385169487 RDMA bytes written per second
    VERBOSE: 33902277 RDMA bytes sent per second
    VERBOSE: 907354685 RDMA bytes written per second
    VERBOSE: 33923662 RDMA bytes sent per second
    VERBOSE: Enabling RDMA on adapters that are not part of this test. RDMA was disabled on them prior to sending RDMA traffic.
    VERBOSE: RDMA traffic test SUCCESSFUL: RDMA traffic was sent to 192.168.2.5
    
この出力の最後の行"RDMA のトラフィック テスト成功: 192.168.2.5 に RDMA のトラフィックが送信された"は、アダプターに収束の NIC が正しく構成されたことを示しています。

## <a name="all-topics-in-this-guide"></a>このガイドのすべてのトピック

このガイドには、次のトピックが含まれています。

- [単一のネットワーク アダプターに収束の NIC 構成](cnic-single.md)
- [収束の NIC チーム化された NIC の構成](cnic-datacenter.md)
- [収束の NIC の物理スイッチの構成](cnic-app-switch-config.md)
- [集約型の NIC 構成のトラブルシューティング](cnic-app-troubleshoot.md)
