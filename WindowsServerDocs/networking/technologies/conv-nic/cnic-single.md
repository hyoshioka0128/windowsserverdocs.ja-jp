---
title: 1 つのネットワーク アダプターに収束の NIC の構成
description: このトピックで提供しています、HYPER-V ホストの nic が 1 つの収束の NIC を構成する手順について。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: eed5c184-fa55-43a8-a879-b1610ebc70ca
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/14/2018
ms.openlocfilehash: 7777278f374984f242e44fd8a8fa94388df88a30
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59836473"
---
# <a name="converged-nic-configuration-with-a-single-network-adapter"></a>1 つのネットワーク アダプターに収束の NIC の構成

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックで提供しています、HYPER-V ホストの nic が 1 つの収束の NIC を構成する手順について。

このトピックの例の構成には、2 つの HYPER-V ホストがについて説明します **、HYPER-V ホスト A**、および **、HYPER-V ホスト B**します。両方のホストがインストールされている場合、単一物理 NIC (pNIC) があるし、Nic は、トップ オブ ラック型に接続している\(ToR\)物理スイッチ。 さらに、ホストが、同じサブネット上にある、192.168.1.x/24 であります。

![Hyper-V ホスト](../../media/Converged-NIC/1-single-test-conn.jpg)


## <a name="step-1-test-the-connectivity-between-source-and-destination"></a>手順 1. ソースとターゲットの間の接続をテストします。

物理 NIC に接続できること、移行先ホストを確認します。 このテストでは、レイヤー 3 を使用して接続を示します\(L3\) - または、IP レイヤー、レイヤー 2 と\(L2\)します。

1. ネットワーク アダプターのプロパティを表示します。

   ```PowerShell
   Get-NetAdapter
   ```
   
   _**結果:**_  

   |名前|InterfaceDescription|IfIndex|状況|Mac アドレス|%Linkspeed|
   |-----|--------------------|-------|-----|----------|---------|
   |M1|Mellanox connectx-3 Pro.| 4| Up|7C-FE-90-93-8F-A1|40 Gbps|
   ---

2. IP アドレスなど、追加のアダプターのプロパティを表示します。

   ```PowerShell
   Get-NetAdapter M1 | fl *
   ```

   _**結果:**_

   ```PowerShell   
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
   ``` 

## <a name="step-2-ensure-that-source-and-destination-can-communicate"></a>手順 2.  ソースと変換先が通信できることを確認します。

この手順で使用して、 **Test-netconnection**場合を使用できますが、Windows PowerShell コマンド、 **ping**場合コマンドします。 

>[!TIP]
>ホストが互いと通信できることがない場合は、この手順をスキップすることができます。

1. 双方向通信を確認します。

   ```PowerShell
   Test-NetConnection 192.168.1.5
   ```
   
   _**結果:**_

   |パラメーター|値|
   |---------|-----|
   |ComputerName|192.168.1.5|
   |リモート アドレス|192.168.1.5|
   |InterfaceAlias|M1|
   |発信元アドレス|192.168.1.3|
   |PingSucceeded|True|
   |PingReplyDetails \(RTT\)|0 ミリ秒|
   ---
   
   場合によっては、このテストを正常に実行するセキュリティが強化された Windows ファイアウォールを無効にする必要もあります。 ファイアウォールを無効にした場合、セキュリティに留意し、構成が組織のセキュリティ要件を満たしていることを確認します。

2. すべてのファイアウォール プロファイルを無効にします。

   ```PowerShell
   Set-NetFirewallProfile -All -Enabled False
   ```
    
3. ファイアウォール プロファイルを無効にした後、もう一度接続をテストします。 

   ```PowerShell
   Test-NetConnection 192.168.1.5
   ```

   _**結果:**_

   |パラメーター|値|
   |---------|-----|
   |ComputerName|192.168.1.5|
   |リモート アドレス|192.168.1.5|
   |InterfaceAlias|テスト-40 G-1|
   |発信元アドレス|192.168.1.3|
   |PingSucceeded|False|
   |PingReplyDetails \(RTT\)|0 ミリ秒|
   ---



## <a name="step-3-optional-configure-the-vlan-ids-for-nics-installed-in-your-hyper-v-hosts"></a>手順 3. (省略可能)VLAN Id を HYPER-V ホストにインストールされている Nic の構成します。

多くのネットワーク構成の Vlan を使用することし、ネットワークの Vlan を使用しようとしている場合は、Vlan の構成で、前のテストを繰り返す必要があります。 また、RDMA サービス RoCE を使用しようとしている場合、Vlan を有効にする必要があります。

この手順では、Nic が内**アクセス**モード。 ただし、HYPER-V 仮想スイッチを作成する\(vSwitch\) vSwitch ポート レベルで、このガイドの後半で VLAN プロパティが適用されます。 

スイッチは、複数の Vlan をホストできる、ので、ラック上の必要は\(ToR\)物理スイッチ ポート トランク モードで構成するホストが接続されていること。

>[!NOTE]
>トランク モード スイッチを構成する方法の詳細については、ToR スイッチのドキュメントを参照してください。

次の図は、それぞれに 1 つの物理ネットワーク アダプターでは、2 つの HYPER-V ホストと VLAN 101 上で通信する各を構成します。

![仮想ローカル エリア ネットワークを構成します。](../../media/Converged-NIC/2-single-configure-vlans.jpg)


>[!IMPORTANT]
>ローカルと宛先の両方のサーバーでは、これを実行します。 かどうか、移行先サーバーが同じ VLAN id のローカル サーバーとして構成されていない、2 つは通信できません。


1. HYPER-V ホストにインストールされている Nic の VLAN ID を構成します。

   >[!IMPORTANT]
   >コマンドを実行しないでこの場合は、このインターフェイス経由でリモート ホストに接続をホストにアクセスできなくなるので。
    
   ```PowerShell
   Set-NetAdapterAdvancedProperty -Name M1 -RegistryKeyword VlanID -RegistryValue "101"
   Get-NetAdapterAdvancedProperty -Name M1 | Where-Object {$_.RegistryKeyword -eq "VlanID"} 
   ```

   _**結果:**_

   |名前 |DisplayName| 値| RegistryKeyword |RegistryValue|
   |----|-----------|------------|---------------|-------------|
   |M1|VLAN ID|101|VlanID|{101}|
   ---

2. VLAN ID を適用するネットワーク アダプターを再起動します。

   ```PowerShell
   Restart-NetAdapter -Name "M1"
   ```

3. 状態が確認**を**します。

   ```PowerShell
   Get-NetAdapter -Name "M1"
   ```
   
   _**結果:**_

   |名前|InterfaceDescription|IfIndex| 状況|Mac アドレス|%Linkspeed|
   |----|--------------------|-------|------|----------| ---------|
   |M1|Mellanox connectx-3 Pro イーサネット Ada.|4|Up|7C-FE-90-93-8F-A1|40 Gbps|
   ---

   >[!IMPORTANT]
   >再起動し、ネットワーク上で利用可能になるデバイスに数秒かかる場合があります。 

4. 接続を確認します。<p>接続に失敗した場合は、スイッチ、同じ VLAN の VLAN の構成または変換先への参加を調べます。 

   ```PowerShell
   Test-NetConnection 192.168.1.5
   ```
    
## <a name="step-4-configure-quality-of-service-qos"></a>手順 4. 構成サービスの品質\(QoS\)

>[!NOTE]
>互いに通信するためのものがすべてのホストでは、DCB と QoS の構成手順を次のすべてを実行する必要があります。

1. データ センター ブリッジング インストール\(DCB\)各 HYPER-V ホストでします。

   - **省略可能な**iWarp RDMA サービスを使用して、ネットワーク構成。
   - **必要な**RoCE を使用しているネットワーク構成\(任意のバージョン\)RDMA サービス。

   ```PowerShell
   Install-WindowsFeature Data-Center-Bridging
   ```

2. SMB ダイレクトの QoS ポリシーを設定します。

   - **省略可能な**iWarp を使用しているネットワーク構成。
   - **必要な**RoCE を使用しているネットワーク構成。
   
   次の例のコマンドでは、値「3」は任意です。 QoS ポリシーの構成全体で同じ値を一貫して使用する限り、1 から 7 までの値を使用することができます。

   ```PowerShell
   New-NetQosPolicy "SMB" -NetDirectPortMatchCondition 445 -PriorityValue8021Action 3
   ```

   _**結果:**_

   |パラメーター|値|
   |---------|-----|
   |名前 |SMB|
   |所有者|グループ ポリシー\(マシン\)|
   |NetworkProfile|すべての|
   |優先度|127|
   |JobObject|&nbsp;| 
   |NetDirectPort|445 |
   |PriorityValue|3 |
 ---

3. RoCE の展開を有効にする**優先度のフロー制御**SMB トラフィックは、これは必要ありません iWarp の場合。

   ```PowerShell
   Enable-NetQosFlowControl -priority 3
   Get-NetQosFlowControl
   ```

   _**結果:**_

   |Priority|有効|PolicySet|IfIndex|ifAlias|
   |---------|-----|--------- |-------| -------|
   |0 |False |グローバル|&nbsp;|&nbsp;|
   |1 |False |グローバル|&nbsp;|&nbsp;|
   |2 |False |グローバル|&nbsp;|&nbsp;|
   |3 |True  |グローバル|&nbsp;|&nbsp;|
   |4 |False |グローバル|&nbsp;|&nbsp;|
   |5 |False |グローバル|&nbsp;|&nbsp;|
   |6 |False |グローバル|&nbsp;|&nbsp;|
   |7 |False |グローバル|&nbsp;|&nbsp;|
   ---

4. ローカルと移行先ネットワーク アダプターに対して QoS を有効にします。

   - **必要ない**iWarp を使用しているネットワーク構成。
   - **必要な**RoCE を使用しているネットワーク構成。

   ```PowerShell
   Enable-NetAdapterQos -InterfaceAlias "M1"
   Get-NetAdapterQos -Name "M1"
   ```

   _**結果:**_

   **名前**:M1  
   **Enabled**:True  

   _**機能:**_   

   |パラメーター|ハードウェア|現在の|
   |---------|--------|-------|
   |MacSecBypass|NotSupported|NotSupported|
   |DcbxSupport|なし|なし|
   |NumTCs(Max/ETS/PFC)|8/8/8|8/8/8|
   ---
 
   _**OperationalTrafficClasses:**_ 

   |TC|TSA|帯域幅|優先順位|
   |----|-----|--------|-------|
   |0| ETS|70%|0-2,4-7|
   |1|ETS|30%|3 |
   ---

   _**OperationalFlowControl:**_  
   
   優先順位 3 が有効になっています。  

   _**OperationalClassifications:**_  

   |プロトコル|ポートの種類/|Priority|
   |--------|---------|--------|
   |Default|&nbsp;|0|
   |NetDirect| 445|3|
   ---

5. SMB ダイレクトの帯域幅の割合を予約\(RDMA\)します。

    この例では、30% の帯域幅予約を使用します。 記憶域トラフィックが必要です。 期待を表す値を選択する必要があります。 

   ```PowerShell
   New-NetQosTrafficClass "SMB" -Priority 3 -BandwidthPercentage 30 -Algorithm ETS
   ```

   _**結果:**_

   |名前|アルゴリズム |Bandwidth(%)| Priority |PolicySet |IfIndex |ifAlias |
   |----|---------| ------------ |--------| ---------|------- |------- |
   |SMB | ETS     | 30 |3 |グローバル |&nbsp;|&nbsp;|
   ---                                      

6. 帯域幅予約の設定を表示します。  

   ```PowerShell
   Get-NetQosTrafficClass
   ```

   _**結果:**_
 
   |名前|アルゴリズム |Bandwidth(%)| Priority |PolicySet |IfIndex |ifAlias |
   |----|---------| ------------ |--------| ---------|------- |------- |
   |[Default]|ETS|70 |0-2,4-7| グローバル|&nbsp;|&nbsp;| 
   |SMB      |ETS|30 |3 |グローバル|&nbsp;|&nbsp;| 
   ---

## <a name="step-5-optional-resolve-the-mellanox-adapter-debugger-conflict"></a>手順 5. (省略可能)Mellanox アダプター デバッガーの競合を解決します。 

Mellanox アダプターを使用する場合、既定では、アタッチされたデバッガーは、これは既知の問題を NetQos にブロックします。 そのため、Mellanox からアダプターを使用してデバッガーをアタッチする場合、次のコマンドの解決をこの問題使用します。 デバッガーをアタッチしない場合、または Mellanox アダプターを使用していない場合、この手順は必要ありません。

   ```PowerShell    
   Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 –Force
   ``` 

## <a name="step-6-verify-the-rdma-configuration-native-host"></a>手順 6. RDMA 構成 (ネイティブ ホスト) を確認します。

VSwitch を作成して、RDMA (コンバージド NIC) に移行する前に、ファブリックが正しく構成されていることを確認するには。 

次の図は、HYPER-V ホストの現在の状態を示します。

![RDMA のテスト](../../media/Converged-NIC/4-single-test-rdma.jpg)

1. RDMA 構成を確認します。

   ```PowerShell
   Get-NetAdapterRdma
   ```
   _**結果:**_

   |名前 |InterfaceDescription |有効|
   |----|--------------------|-------|
   |M1| Mellanox connectx-3 Pro イーサネット アダプター |True|
   ---

2. 確認、 **ifIndex**対象アダプターの値。<p>ダウンロードしたスクリプトを実行するときに、以降の手順でこの値を使用します。

   ```PowerShell
   Get-NetIPConfiguration -InterfaceAlias "M*" | ft InterfaceAlias,InterfaceIndex,IPv4Address
   ```

   _**結果:**_ 

   |InterfaceAlias |InterfaceIndex |IPv4Address|
   |-------------- |-------------- |-----------|
   |M2 |14 |{192.168.1.5}|
   ---

3. ダウンロード、 [DiskSpd.exe ユーティリティ](https://aka.ms/diskspd)C:\TEST に抽出\.

4. ダウンロード、 [powershell スクリプトのテスト RDMA](https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1) C:\TEST など、ローカル ドライブ上のテスト フォルダーを\.

5. 実行、**テスト Rdma.ps1** ifIndex 値を同じ VLAN 上のリモートのアダプターの IP アドレスと共に、スクリプトに渡す、PowerShell スクリプト。<p>この例では、スクリプトを渡します、 **ifIndex**リモート ネットワーク アダプターの IP アドレス 192.168.1.5 で 14 文字の値。
   
   ```PowerShell
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
   ```

   >[!NOTE]
   >RDMA のトラフィックが失敗した場合、RoCE ケースを具体的には、ホストの設定に一致する必要があります PFC/ETS の適切な設定を ToR スイッチの構成を参照してください。 参照値は、このドキュメントで QoS セクションを参照してください。

## <a name="step-7-remove-the-access-vlan-setting"></a>手順 7. アクセス VLAN 設定を削除します。

Hyper-v ホストを作成するための準備で切り替えると、上にインストールした VLAN 設定を削除する必要があります。  

1. アクセス VLAN 設定を NIC が不適切な VLAN ID を持つエグレス トラフィックを自動でタグ付けするを防ぐために物理 NIC から削除します。<p>この設定の削除もできないアクセス VLAN ID とも一致しない受信トラフィックをフィルター処理
    
   ```PowerShell
   Set-NetAdapterAdvancedProperty -Name M1 -RegistryKeyword VlanID -RegistryValue "0"
   ```    

2. いることを確認、 **VlanID 設定**0 として VLAN ID の値が表示されます。

   ```PowerShell    
   Get-NetAdapterAdvancedProperty -name m1 | Where-Object {$_.RegistryKeyword -eq 'VlanID'} 
   ```  


## <a name="step-8-create-a-hyper-v-vswitch-on-your-hyper-v-hosts"></a>手順 8 です。 HYPER-V ホスト上の HYPER-V vSwitch を作成します。

次の図では、vSwitch を HYPER-V ホスト 1 を表しています。

![HYPER-V 仮想スイッチを作成します。](../../media/Converged-NIC/5-single-create-vswitch.jpg)


1. HYPER-V ホスト A 上の HYPER-V で外部の HYPER-V vSwitch を作成します。 <p>この例では、スイッチを VMSTEST と呼びます。 パラメーターではまた、 **AllowManagementOS**物理 NIC の MAC と IP アドレスを継承するホスト vNIC を作成します

   ```PowerShell
   New-VMSwitch -Name VMSTEST -NetAdapterName "M1" -AllowManagementOS $true
   ```
   _**結果:**_

   |名前 |SwitchType |NetAdapterInterfaceDescription|
   |---- |---------- |------------------------------|
   |VMSTEST |外部リンク |Mellanox connectx-3 Pro イーサネット アダプター|
   ---

2. ネットワーク アダプターのプロパティを表示します。

   ```PowerShell
   Get-NetAdapter | ft -AutoSize
   ```

   _**結果:**_

   |名前 |InterfaceDescription | IfIndex |状況 |Mac アドレス |%Linkspeed|
   |---- |-------------------- |-------| ------|----------|---------|
   |vEthernet \(VMSTEST\) |HYPER-V 仮想イーサネット アダプター #2|27 |Up |E4-1D-2D-07-40-71 |40 Gbps|
   ---

3. 2 つの方法のいずれかでホスト vNIC を管理します。 

   - **NetAdapter**表示動作に基づいて、"vEthernet \(VMSTEST\)"の名前。 すべてのネットワーク アダプターのプロパティは、このビューで表示します。
   - **VMNetworkAdapter**ビューは、"vEthernet"プレフィックスを削除し、vmswitch の名前を使用します。 (推奨) 

   ```PowerShell
   Get-VMNetworkAdapter –ManagementOS | ft -AutoSize
   ```

   _**結果:**_

   |名前 |IsManagementOs |VMName |SwitchName |Mac アドレス |状況 |Ip アドレス|
   |----|-------------- |------ |----------|----------|------ |-----------|
   |CORP の外部スイッチ |True |CORP の外部スイッチ| 001B785768AA |{0} [ok]} |&nbsp;|
   |VMSTEST |True |VMSTEST | E41D2D074071| {0} [ok]} | &nbsp;| 
   ---

4. 接続をテストします。

   ```Powershell    
   Test-NetConnection 192.168.1.5
   ```

   _**結果:**_ 

   ```
    ComputerName   : 192.168.1.5
    RemoteAddress  : 192.168.1.5
    InterfaceAlias : vEthernet (CORP-External-Switch)
    SourceAddress  : 192.168.1.3
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms
   ```

5. 割り当て、ネットワーク アダプターの VLAN 設定を表示します。
    
   ```PowerShell
   Set-VMNetworkAdapterVlan -VMNetworkAdapterName "VMSTEST" -VlanId "101" -Access -ManagementOS
   Get-VMNetworkAdapterVlan -ManagementOS -VMNetworkAdapterName "VMSTEST"
   ```    

   _**結果:**_

   |VMName |VMNetworkAdapterName |Mode |[Vlanlist]|
   |------ |-------------------- |---- |--------|
   |&nbsp;|VMSTEST |アクセス権 |101   |
   ---  
 
6. 接続をテストします。<p>その他のアダプターの ping を実行することが正常に完了するまでに数秒かかる場合があります。  

   ```PowerShell    
   Test-NetConnection 192.168.1.5
   ```

   _**結果:**_
     
   ```
    ComputerName   : 192.168.1.5
    RemoteAddress  : 192.168.1.5
    InterfaceAlias : vEthernet (VMSTEST)
    SourceAddress  : 192.168.1.3
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms
   ```

## <a name="step-9-test-hyper-v-virtual-switch-rdma-mode-2"></a>手順 9: HYPER-V 仮想スイッチ (モード 2) RDMA のテストします。

次の図は、HYPER-V ホスト 1 vSwitch を含む、HYPER-V ホストの現在の状態を示しています。

![HYPER-V 仮想スイッチをテストします。](../../media/Converged-NIC/6-single-test-vswitch-rdma.jpg)


1. ホスト vNIC のタグ付け、優先順位を設定します。

   ```PowerShell    
   Set-VMNetworkAdapter -ManagementOS -Name "VMSTEST" -IeeePriorityTag on
   Get-VMNetworkAdapter -ManagementOS -Name "VMSTEST" | fl Name,IeeePriorityTag
   ```  
   
   _**結果:**_

    名前:VMSTEST IeeePriorityTag:オン


2. ネットワーク アダプターの RDMA の情報を表示します。 

   ```PowerShell
   Get-NetAdapterRdma
   ```   

   _**結果:**_

   |名前 |InterfaceDescription |有効 |
   |---- |-------------------- |-------|
   |vEthernet \(VMSTEST\)| HYPER-V 仮想イーサネット アダプター #2|False|
   ---

   >[!NOTE]
   >場合、パラメーター**有効**、値を持つ**False**RDMA が有効になっていないことを意味します。
    

3. ネットワーク アダプターの情報を表示します。

   ```PowerShell
   Get-NetAdapter
   ```

   _**結果:**_   
 
   |名前 |InterfaceDescription |IfIndex |状況 |Mac アドレス |%Linkspeed|
   |----|--------------------|-------|------|----------|---------|
   |vEthernet (VMSTEST)|HYPER-V 仮想イーサネット アダプター #2|27|Up|E4-1D-2D-07-40-71|40 Gbps|
   ---


4. ホスト vNIC で RDMA を有効にします。

   ```PowerShell
   Enable-NetAdapterRdma -Name "vEthernet (VMSTEST)"
   Get-NetAdapterRdma -Name "vEthernet (VMSTEST)"
   ```

   _**結果:**_

   |名前 |InterfaceDescription |有効 |
   |---- |-------------------- |-------|
   |vEthernet \(VMSTEST\)| HYPER-V 仮想イーサネット アダプター #2|True|
   ---

   >[!NOTE]
   >場合、パラメーター**有効**、値を持つ**True**RDMA が有効になっていることを意味します。

5. RDMA のトラフィックのテストを実行します。

   ```PowerShell    
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
   ```

この出力の最後の行"RDMA のトラフィックのテスト成功。RDMA のトラフィックは、192.168.1.5 に送信された"は、アダプターに収束の NIC が正しく構成されたことを示します。

## <a name="related-topics"></a>関連トピック
- [収束の NIC チーミングされた NIC の構成](cnic-datacenter.md)
- [収束の NIC の物理スイッチの構成](cnic-app-switch-config.md)
- [集約型のない NIC 構成のトラブルシューティング](cnic-app-troubleshoot.md)
