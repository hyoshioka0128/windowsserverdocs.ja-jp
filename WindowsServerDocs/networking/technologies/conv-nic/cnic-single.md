---
title: 単一のネットワーク アダプターに収束の NIC 構成
description: このトピックは、Windows Server 2016 での単一のネットワーク アダプターに収束の NIC を展開する方法を説明します。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: eed5c184-fa55-43a8-a879-b1610ebc70ca
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d6663a966026afb301a4bad90a9573d16fc82875
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="converged-nic-configuration-with-a-single-network-adapter"></a>単一のネットワーク アダプターに収束の NIC 構成

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

次のセクションで、Hyper-v ホストで 1 つの NIC を持つ集約型の NIC を構成するための手順を提供します。

このガイドで構成の例は、次の 2 つの Hyper-V ホストを示しています。**Hyper-v ホスト A**、および**Hyper-v ホスト B**します。

## <a name="test-connectivity-between-source-and-destination"></a>移行元と送信先の間の接続をテストします。

このセクションでは、ソースと宛先の Hyper-v ホストの間の接続をテストするために必要な手順を示します。

次の図は、次の 2 つの Hyper-V ホストを示しています。**Hyper-v ホスト A**と**Hyper-v ホスト B**します。 

両方のサーバーがインストールされている場合、単一物理 NIC (pNIC) があるし、Nic は、トップ オブ ラック型 \(ToR\) 物理スイッチに接続しています。 さらに、サーバーが、同じサブネット上にある、192.168.1.x/24 です。

![Hyper-V ホスト](../../media/Converged-NIC/1-single-test-conn.jpg)


### <a name="test-nic-connectivity-to-the-hyper-v-virtual-switch"></a>Hyper\ V 仮想スイッチに NIC の接続をテストします。

この手順を使用して、Hyper\ V 仮想スイッチを作成、後で、物理 NIC を移行先ホストに接続できることを確認することができます。 

このテストでは、レイヤー 3 \(L3\) - や、IP レイヤーだけでなくレイヤー 2 \(L2\) を使用して接続を示します。

次の Windows PowerShell コマンドを使用して、ネットワーク アダプターのプロパティを取得することができます。

    Get-NetAdapter
     
このコマンドの結果の例を次に示します。

|名|InterfaceDescription|ifIndex|ステータス|MacAddress|LinkSpeed|
|-----|--------------------|-------|-----|----------|---------|
|
|M1|Mellanox connectx-3 Pro.| 4| アップ|7C-FE-90-93-8F-A1|40 gb/秒|

IP アドレスなど、追加のアダプターのプロパティを取得するのにには、次のコマンドのいずれかを使用します。

    Get-NetAdapter M1 | fl *

このコマンドの結果を編集した例を次に示します。
    
    MacAddress   : 7C-FE-90-93-8F-A1
    Status   : Up
    LinkSpeed: 40 Gbps
    MediaType: 802.3
    PhysicalMediaType: 802.3
    AdminStatus  : Up
    MediaConnectionState : Connected
    DriverInformation: Driver Date 2016-08-28 Version 5.25.12665.0 NDIS 6.60
    DriverFileName   : mlx4eth63.sys
    NdisVersion  : 6.60
    ifOperStatus : Up
    ifAlias  : M1
    InterfaceAlias   : M1
    ifIndex  : 4
    ifDesc   : Mellanox ConnectX-3 Pro Ethernet Adapter
    ifName   : ethernet_32773
    DriverVersion: 5.25.12665.0
    LinkLayerAddress : 7C-FE-90-93-8F-A1
    Caption  :
    Description  :
    ElementName  :
    InstanceID   : {39B58B4C-8833-4ED2-A2FD-E105E7146D43}
    CommunicationStatus  :
    DetailedStatus   :
    HealthState  :
    InstallDate  :
    Name : M1
    OperatingStatus  :
    OperationalStatus:
    PrimaryStatus:
    StatusDescriptions   :
    AvailableRequestedStates :
    EnabledDefault   : 2
    EnabledState : 5
    OtherEnabledState:
    RequestedState   : 12
    TimeOfLastStateChange:
    TransitioningToState : 12
    AdditionalAvailability   :
    Availability :
    CreationClassName: MSFT_NetAdapter
    

### <a name="ensure-that-source-and-destination-can-communicate"></a>移行元と移行先が通信できることを確認します。

この手順を使用するを双方向通信を確認 \ (移行先およびその逆を行うを両方 \ ping ソースから)。  次の例では、**テスト NetConnection**場合は、使用することができますが、Windows PowerShell コマンドを使用、**ping**コマンド。 

>[!NOTE]
>ホストが相互に通信できることがいる場合は、この手順を省略できます。

    Test-NetConnection 192.168.1.5

このコマンドの結果の例を次に示します。

|パラメーター|値|
|---------|-----|
|
|コンピューター名|192.168.1.5|
|RemoteAddress|192.168.1.5|
|InterfaceAlias|M1|
|発信元アドレス|192.168.1.3|
|PingSucceeded|場合は true。|
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

## <a name="configure-vlans-optional"></a>Vlan \(Optional\) を構成します。

多くのネットワーク構成は、Vlan を使用してください。 ネットワークの Vlan を使用する計画している場合、構成されている Vlan で前のテストを繰り返す必要があります。 \ (RoCE を RDMA サービスの使用を計画している場合、Vlan を有効にする必要があります \)。

Nic がこの手順で**アクセス**モード。 ただしこのガイドの後半で Hyper-V 仮想スイッチ \(vSwitch\) を作成するときに、VLAN のプロパティは、vSwitch ポート レベルで適用されます。 

スイッチは、複数の Vlan をホストできる、ので、ラックの上部 \(ToR\) 物理スイッチのポートがホストに接続しているトランク モードで構成する必要があります。

>[!NOTE]
>スイッチのトランク モードを構成する方法の詳細については、ToR スイッチのドキュメントを参照してください。

次の図は、それぞれが 1 つの物理ネットワーク アダプターを持つ 2 つの Hyper-V ホストを示していて、VLAN 101 上で通信する各ように構成します。

![仮想ローカル エリア ネットワークを構成します。](../../media/Converged-NIC/2-single-configure-vlans.jpg)

### <a name="configure-the-vlan-id"></a>VLAN ID を構成します。

このステップを使用して、Hyper-V ホストにインストールされている Nic の VLAN ID を構成することができます。

#### <a name="configure-nic-m1"></a>NIC M1 を構成します。

次のコマンドを使用して最初の nic M1、VLAN ID を構成し、構成の結果を確認します。

>[!IMPORTANT]
>コマンドを実行しないでこの場合は、このインターフェイスを経由でリモート ホストに接続するのにでは、アクセス権の損失をホストするためです。
    
    Set-NetAdapterAdvancedProperty -Name M1 -RegistryKeyword VlanID -RegistryValue "101"
    Get-NetAdapterAdvancedProperty -Name M1 | Where-Object {$_.RegistryKeyword -eq "VlanID"} 
    
このコマンドの結果の例を次に示します。

|名 |DisplayName| 値| RegistryKeyword |RegistryValue|
|----|-----------|------------|---------------|-------------|
|
|M1|VLAN ID|101|VlanID|{101}|


VLAN ID は、効果のネットワーク アダプターの実装から独立して、次のコマンドを使用して、ネットワーク アダプターを再起動することを確認します。

    Restart-NetAdapter -Name "M1"

次のコマンドを使用するには、ネットワーク アダプタの状態があることを確認する**を**続行する前にします。

    Get-NetAdapter -Name "M1"

このコマンドの結果の例を次に示します。

|名|InterfaceDescription|ifIndex| ステータス|MacAddress|LinkSpeed|
|----|--------------------|-------|------|----------| ---------|
|
|M1|Mellanox connectx-3 Pro イーサネット Ada.|4|アップ|7C-FE-90-93-8F-A1|40 gb/秒|

ローカルと宛先の両方のサーバー上でこの手順を実行することを確認します。 かどうか、移行先サーバーが構成されていないローカル サーバーと同じ VLAN ID を持つ 2 つは通信できません。

### <a name="verify-connectivity"></a>接続を確認します。

このセクションを使用すると、ネットワーク アダプターを再起動した後、接続を確認します。 両方のアダプターに VLAN タグを適用した後、接続を確認できます。 接続に失敗した場合は、スイッチ、同じ VLAN の VLAN 構成または移行先への参加を検査できます。 

>[!IMPORTANT]
>前のセクションの手順を実行した後は、数秒デバイスを再起動し、ネットワーク上で利用可能になるがかかる場合があります。

#### <a name="verify-connectivity-for-nic-test-40g-1"></a>NIC テスト-40 G-1 の接続を確認します。

最初の NIC の接続を確認するには、次のコマンドを実行できます。

    Test-NetConnection 192.168.1.5
    
## <a name="configure-data-center-bridging-dcb"></a>データ センター ブリッジング \(DCB\) を構成します。

次の手順では、まず、Windows Server 2016 の機能 DCB をインストールすることが必要です。DCB とサービスの品質 \(QoS\) を構成します。

>[!NOTE]
>相互に通信するためには、すべてのサーバー上でのすべての次の DCB と QoS の構成手順を実行する必要があります。

### <a name="install-data-center-bridging-dcb"></a>データ センター ブリッジング \(DCB\) をインストールします。

このステップを使用して、インストールして DCB を有効にすることができます。 

>[!IMPORTANT]
>- インストールと構成の DCB は**オプション**RDMA サービスに加えて、iWarp を使用しているネットワーク構成します。
>- インストールと構成の DCB は**必要**RDMA サービスの RoCE \(any version\) を使用しているネットワーク構成します。


次のコマンドは、DCB を使用して、Hyper-V ホストの各インストールを使用することができます。 

    Install-WindowsFeature Data-Center-Bridging

### <a name="set-the-qos-policies-for-smb-direct"></a>SMB ダイレクトの QoS ポリシーを設定します。 

次のコマンドを使用して、SMB ダイレクトの QoS ポリシーを構成することができます。

>[!IMPORTANT]
>- この手順では、iWarp を使用しているネットワーク構成オプションです。
>- この手順は、RoCE を使用しているネットワーク構成に必要です。
>- 次の例のコマンドでは、値「3」は任意です。 一貫して QoS ポリシーの構成全体で同じ値を使用する限り、1 ~ 7 の間の任意の値を使用することができます。

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

### <a name="for-roce-deployments-turn-on-priority-flow-control-for-smb-traffic"></a>RoCE の展開は SMB トラフィックの優先度のフロー制御を有効にするため 

RoCE、RDMA サービスを使用している場合は、SMB のフロー制御を有効にして、結果を表示するに次のコマンドを使用できます。 優先度のフロー制御しますが、必要です、RoCE に対して iWarp を使用している場合は必要ありません。

    Enable-NetQosFlowControl -priority 3
    Get-NetQosFlowControl

例の結果を次に示します、**Get NetQosFlowControl**コマンド。

|優先順位|有効になっています。|PolicySet|IfIndex|IfAlias|
|---------|-----|--------- |-------| -------|
|
|0 |False |グローバル|&nbsp;|&nbsp;|
|1 |False |グローバル|&nbsp;|&nbsp;|
|2 |False |グローバル|&nbsp;|&nbsp;|
|3 |場合は true。  |グローバル|&nbsp;|&nbsp;|
|4 |False |グローバル|&nbsp;|&nbsp;|
|5 |False |グローバル|&nbsp;|&nbsp;|
|6 |False |グローバル|&nbsp;|&nbsp;|
|7 |False |グローバル|&nbsp;|&nbsp;|

### <a name="enable-qos-for-the-local-and-destination-network-adapters"></a>ローカルと移行先ネットワーク アダプターに対して QoS を有効にします。
この手順では、特定のネットワーク アダプターの DCB を有効にできます。

>[!IMPORTANT]
>-  この手順は、iWarp を使用しているネットワーク構成は必要ありません。
>-  この手順は、RoCE を使用しているネットワーク構成に必要です。




#### <a name="enable-qos-for-nic-m1"></a>NIC M1 の QoS を有効にします。

次のコマンドを使用して、QoS を有効にして、構成の結果を表示することができます。

    Enable-NetAdapterQos -InterfaceAlias "M1"
    Get-NetAdapterQos -Name "M1"

このコマンドの結果の例を次に示します。

**名前**: M1**有効になっている**: True**機能**:   

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
|0| ETS|70%|0-2,4-7|
|1|ETS|30%|3

**OperationalFlowControl**: 有効になっている 3 の優先順位**OperationalClassifications**:

|プロトコル|/ポートの種類|優先順位|
|--------|---------|--------|
|
|既定値|&nbsp;|0|
|NetDirect| 445|3|

### <a name="reserve-a-percentage-of-the-bandwidth-for-smb-direct-rdma"></a>SMB ダイレクト \(RDMA\) 用の帯域幅の割合を予約します。

次のコマンドを使用すると、SMB ダイレクト用の帯域幅の割合を予約します。  

この例では 30% の帯域幅予約を使用します。 予想したもので、記憶域トラフィックが必要であることを表す値を選択する必要があります。 値、**- bandwidthpercentage**パラメーターが 10% の倍数にする必要があります。

    New-NetQosTrafficClass "SMB" -Priority 3 -BandwidthPercentage 30 -Algorithm ETS

このコマンドの結果の例を次に示します。

|名|アルゴリズム |Bandwidth(%)| 優先順位 |PolicySet |IfIndex |IfAlias |
|----|---------| ------------ |--------| ---------|------- |------- |
|
|SMB | ETS     | 30 |3 |グローバル |&nbsp;|&nbsp;|                                      
 
次のコマンドを使用して、帯域幅予約情報を表示することができます。

    Get-NetQosTrafficClass

このコマンドの結果の例を次に示します。
 
|名|アルゴリズム |Bandwidth(%)| 優先順位 |PolicySet |IfIndex |IfAlias |
|----|---------| ------------ |--------| ---------|------- |------- |
|
|[既定値]|ETS|70 |0-2,4-7| グローバル|&nbsp;|&nbsp;| 
|SMB      |ETS|30 |3 |グローバル|&nbsp;|&nbsp;| 

## <a name="remove-debugger-conflict-mellanox-adapter-only"></a>デバッガーの競合を削除する \(Mellanox adapter only\)

Mellanox アダプターを使用している場合は、デバッガーを構成するのには、この手順を実行する必要があります。 既定では、Mellanox アダプターを使用すると、接続されているデバッガーは NetQos をブロックします。 次のコマンドを使用して、デバッガーを上書きすることができます。

    
    Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 –Force
    

## <a name="test-rdma-native-host"></a>テスト RDMA (ネイティブ ホスト)

このステップを使用して、vSwitch を作成および RDMA \(Converged NIC\) に移行する前に、ファブリックが正しく構成されていることを確認することができます。

次の図は、Hyper-V ホストの現在の状態を示しています。

![RDMA のテスト](../../media/Converged-NIC/4-single-test-rdma.jpg)

RDMA 構成を確認するには、次のコマンドを実行できます。

    Get-NetAdapterRdma

このコマンドの結果の例を次に示します。

|名 |InterfaceDescription |有効になっています。|
|----|--------------------|-------|
|
|M1| Mellanox connectx-3 Pro イーサネット アダプター |場合は true。|

### <a name="download-diskspdexe-and-a-powershell-script"></a>DiskSpd.exe と PowerShell スクリプトをダウンロードします。

続けるには、まず、次の項目をダウンロードする必要があります。

- DiskSpd.exe ユーティリティをダウンロードして抽出 C:\TEST\ にユーティリティ[Diskspd ユーティリティ: 堅牢な記憶域テスト ツール (置き換え SQLIO)](https://gallery.technet.microsoft.com/DiskSpd-a-robust-storage-6cd2f223)

- C:\TEST\ に Test-RDMA powershell スクリプトをダウンロードします。[https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1](https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1)

### <a name="determine-the-ifindex-value-of-your-target-adapter"></a>対象アダプターの ifIndex 値を決定します。

次のコマンドを使用すると、ターゲット アダプターの ifIndex 値を検出します。 ダウンロードしたスクリプトを実行している場合は、後続の手順でこの値を使用できます。

    Get-NetIPConfiguration -InterfaceAlias "M*" | ft InterfaceAlias,InterfaceIndex,IPv4Address

このコマンドの結果の例を次に示します。

|InterfaceAlias |InterfaceIndex |IPv4Address|
|-------------- |-------------- |-----------|
|
|M2 |14 |{192.168.1.5}|

### <a name="run-the-powershell-script"></a>PowerShell スクリプトを実行します。

Test-Rdma .ps1 Windows PowerShell スクリプトを実行すると、同じ vlan リモート アダプターの IP アドレスと共に、スクリプトに ifIndex 値を渡すことができます。

次のコマンド例を使用すると、ネットワーク アダプター 192.168.1.5 で、ifIndex 14 にスクリプトを実行します。
    
    C:\TEST\Test-RDMA.PS1 -IfIndex 14 -IsRoCE $true -RemoteIpAddress 192.168.1.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
    
    VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\\diskspd.exe
    VERBOSE: The adapter M2 is a physical adapter
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

## <a name="remove-the-access-vlan-setting"></a>アクセス VLAN 設定を削除します。

Hyper-V スイッチを作成するための準備を超えてインストールされている VLAN 設定を削除する必要があります。  次のコマンドを使用して、物理 NIC からのアクセスを VLAN 設定を削除することができます。 この操作の NIC が不適切な VLAN ID を持つ出口トラフィックを自動タグ付けするを防ぎますもできないアクセス VLAN ID が一致しない受信トラフィックをフィルタ リング

    
    Set-NetAdapterAdvancedProperty -Name M1 -RegistryKeyword VlanID -RegistryValue "0"
    

次のコマンド例を使用して、VlanID 設定を確認し、VLAN ID の値が 0 であることを示すの結果を表示することができます。

    
    Get-NetAdapterAdvancedProperty -name m1 | Where-Object {$_.RegistryKeyword -eq 'VlanID'} 
    


## <a name="create-a-hyper-v-virtual-switch"></a>Hyper-V 仮想スイッチを作成します。

このセクションを使用すると、Hyper-V ホスト上で Hyper-V 仮想スイッチ \(vSwitch\) を作成します。

次の図は、vSwitch で Hyper-V ホスト 1 を示しています。

![Hyper-V 仮想スイッチを作成します。](../../media/Converged-NIC/5-single-create-vswitch.jpg)


### <a name="create-an-external-hyper-v-virtual-switch"></a>外部の Hyper-V 仮想スイッチを作成します。

このセクションを使用して、Hyper-V ホスト A 上の Hyper-V で外部 vSwitch を作成することができます。

次のコマンド例を使用して、VMSTEST という名前のスイッチを作成することができます。

>[!NOTE]
>パラメーター **AllowManagementOS**、次のコマンドで、MAC アドレスと物理 NIC の IP アドレスを継承するホスト vNIC を作成します

    New-VMSwitch -Name VMSTEST -NetAdapterName "M1" -AllowManagementOS $true

このコマンドの結果の例を次に示します。

|名 |SwitchType |NetAdapterInterfaceDescription|
|---- |---------- |------------------------------|
|VMSTEST |外部 |Mellanox connectx-3 Pro イーサネット アダプター|

次のコマンドを使用して、ネットワーク アダプターのプロパティを表示することができます。

    Get-NetAdapter | ft -AutoSize

このコマンドの結果の例を次に示します。

|名 |InterfaceDescription | ifIndex |ステータス |MacAddress |LinkSpeed|
|---- |-------------------- |-------| ------|----------|---------|
|
|vEthernet \(VMSTEST\) |Hyper-V 仮想イーサネット アダプター #2|27 |アップ |E4-1D-2D-07-40-71 |40 gb/秒|


次の 2 つの方法でホスト vNIC を管理することができます。 1 つの方法は、**NetAdapter**表示では動作に基づいて、"vEthernet \(VMSTEST\)"名前。

その他の方法は、**VMNetworkAdapter**ビューでは、「vEthernet」プレフィックスを破棄し vmswitch 名前を使用します。

**VMNetworkAdapter**ビューに表示されていない一部のネットワーク アダプターのプロパティを表示する、**NetAdapter**コマンド。

次のコマンドを使用して、結果を表示することができます、**VMNetworkAdapter**メソッド。

    Get-VMNetworkAdapter –ManagementOS | ft -AutoSize

このコマンドの結果の例を次に示します。

|名 |IsManagementOs |VMName |SwitchName |MacAddress |ステータス |Ip アドレス|
|----|-------------- |------ |----------|----------|------ |-----------|
|
|CORP の外部スイッチ |場合は true。 |CORP の外部スイッチ| 001B785768AA |{OK} |&nbsp;|
|VMSTEST |場合は true。 |VMSTEST | E41D2D074071| {OK} | &nbsp;| 

### <a name="test-the-connection"></a>接続をテストします。

次のコマンド例を使用して、接続をテストし、結果を表示することができます。
    
    Test-NetConnection 192.168.1.5

    ComputerName   : 192.168.1.5
    RemoteAddress  : 192.168.1.5
    InterfaceAlias : vEthernet (CORP-External-Switch)
    SourceAddress  : 192.168.1.3
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms
    
次の例のコマンドを使用して、割り当てるし、ネットワーク アダプターの VLAN 設定を表示することができます。
    
    Set-VMNetworkAdapterVlan -VMNetworkAdapterName "VMSTEST" -VlanId "101" -Access -ManagementOS
    Get-VMNetworkAdapterVlan -ManagementOS -VMNetworkAdapterName "VMSTEST"
    

|VMName |VMNetworkAdapterName |モード |[Vlanlist]|
|------ |-------------------- |---- |--------|
|
|&nbsp;|VMSTEST |アクセス |101     
 
### <a name="test-the-connection"></a>接続をテストします。

変更が前に、その他のアダプターをに対して ping が正常に完了するまでしばらくかかる場合があることを思い出してください。

次のコマンド例を使用して、接続をテストし、結果を表示することができます。
    
    Test-NetConnection 192.168.1.5
     
    ComputerName   : 192.168.1.5
    RemoteAddress  : 192.168.1.5
    InterfaceAlias : vEthernet (VMSTEST)
    SourceAddress  : 192.168.1.3
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms
    

## <a name="test-hyper-v-virtual-switch-rdma-mode-2"></a>Hyper-V 仮想スイッチを RDMA (モード 2) のテストします。

次の図は、Hyper-V ホスト 1 vSwitch を含む、Hyper-V ホストの現在の状態を示しています。

![Hyper-V 仮想スイッチをテストします。](../../media/Converged-NIC/6-single-test-vswitch-rdma.jpg)


### <a name="set-priority-tagging-on-the-host-vnic"></a>ホスト vNIC のタグ付けの優先順位を設定します。

次の例のコマンドを使用して、ホスト vNIC のタグ付けの優先順位を設定し、アクションの結果を表示することができます。
    
    Set-VMNetworkAdapter -ManagementOS -Name "VMSTEST" -IeeePriorityTag on
    Get-VMNetworkAdapter -ManagementOS -Name "VMSTEST" | fl Name,IeeePriorityTag
    
    Name: VMSTEST
    IeeePriorityTag : On
    
次のコマンド例を使用して、ネットワーク アダプターの RDMA の情報を表示することができます。 結果にときに、パラメーター**有効**値を持つ**False**、RDMA が有効になっていないことを意味します。
    
    Get-NetAdapterRdma
    
|名 |InterfaceDescription |有効になっています。 |
|---- |-------------------- |-------|
|
|vEthernet \(VMSTEST\)| Hyper-V 仮想イーサネット アダプター #2|False|

### <a name="enable-rdma-on-the-host-vnic"></a>ホスト vNIC で RDMA を有効にします。

次の例のコマンドを使用するネットワーク アダプターのプロパティを表示、アダプターの RDMA を有効にし、ネットワーク アダプターの RDMA の情報を表示します。
    
    Get-NetAdapter
    
|名 |InterfaceDescription |ifIndex |ステータス |MacAddress |LinkSpeed|
|----|--------------------|-------|------|----------|---------|
|
|vEthernet (VMSTEST)|Hyper-V 仮想イーサネット アダプター #2|27|アップ|E4-1D-2D-07-40-71|40 gb/秒|

    Enable-NetAdapterRdma -Name "vEthernet (VMSTEST)"
    Get-NetAdapterRdma -Name "vEthernet (VMSTEST)"

次の結果でときに、パラメーター**有効**値を持つ**True**、RDMA が有効になっていることを意味します。

|名 |InterfaceDescription |有効になっています。 |
|---- |-------------------- |-------|
|
|vEthernet \(VMSTEST\)| Hyper-V 仮想イーサネット アダプター #2|場合は true。|


    
    Get-NetAdapter 
    

|名 |InterfaceDescription |ifIndex |ステータス |MacAddress |LinkSpeed|
|----|--------------------|-------|------|----------|---------|
|
|vEthernet (VMSTEST)|Hyper-V 仮想イーサネット アダプター #2|27|アップ|E4-1D-2D-07-40-71|40 gb/秒|

### <a name="perform-rdma-traffic-test-by-using-the-script"></a>スクリプトを使用して RDMA のトラフィックのテストを実行します。

ダウンロードしたスクリプトを実行し、結果を表示するには、次のコマンドを使用できます。
    
    C:\TEST\Test-RDMA.PS1 -IfIndex 27 -IsRoCE $true -RemoteIpAddress 192.168.1.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
    VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\\diskspd.exe
    VERBOSE: The adapter vEthernet (VMSTEST) is a virtual adapter
    VERBOSE: Retrieving vSwitch bound to the virtual adapter
    VERBOSE: Found vSwitch: VMSTEST
    VERBOSE: Found the following physical adapter(s) bound to vSwitch: TEST-40G-1
    VERBOSE: Underlying adapter is RoCE. Checking if QoS/DCB/PFC is configured on each physical adapter(s)
    VERBOSE: QoS/DCB/PFC configuration is correct.
    VERBOSE: RDMA configuration is correct.
    VERBOSE: Checking if remote IP address, 192.168.1.5, is reachable.
    VERBOSE: Remote IP 192.168.1.5 is reachable.
    VERBOSE: Disabling RDMA on adapters that are not part of this test. RDMA will be enabled on them later.
    VERBOSE: Testing RDMA traffic now for. Traffic will be sent in a parallel job. Job details:
    VERBOSE: 0 RDMA bytes written per second
    VERBOSE: 0 RDMA bytes sent per second
    VERBOSE: 0 RDMA bytes written per second
    VERBOSE: 0 RDMA bytes sent per second
    VERBOSE: 0 RDMA bytes written per second
    VERBOSE: 0 RDMA bytes sent per second
    VERBOSE: 0 RDMA bytes written per second
    VERBOSE: 9162492 RDMA bytes sent per second
    VERBOSE: 938797258 RDMA bytes written per second
    VERBOSE: 34621865 RDMA bytes sent per second
    VERBOSE: 933572610 RDMA bytes written per second
    VERBOSE: 35035861 RDMA bytes sent per second
    VERBOSE: Enabling RDMA on adapters that are not part of this test. RDMA was disabled on them prior to sending RDMA traffic.
    VERBOSE: RDMA traffic test SUCCESSFUL: RDMA traffic was sent to 192.168.1.5
    
この出力の最後の行"RDMA のトラフィック テスト成功: 192.168.1.5 に RDMA のトラフィックが送信された"は、アダプターに収束の NIC が正しく構成されたことを示しています。

## <a name="all-topics-in-this-guide"></a>このガイドのすべてのトピック

このガイドには、次のトピックが含まれています。

- [単一のネットワーク アダプターに収束の NIC 構成](cnic-single.md)
- [収束の NIC チーム化された NIC の構成](cnic-datacenter.md)
- [収束の NIC の物理スイッチの構成](cnic-app-switch-config.md)
- [集約型の NIC 構成のトラブルシューティング](cnic-app-troubleshoot.md)
