---
title: 単一のネットワークアダプターを使用した収束 NIC 構成
description: このトピックでは、Hyper-v ホストで1つの NIC を使用して収束 NIC を構成する手順について説明します。
ms.topic: article
ms.assetid: eed5c184-fa55-43a8-a879-b1610ebc70ca
manager: dougkim
ms.author: lizross
author: eross-msft
ms.date: 09/14/2018
ms.openlocfilehash: 7c936d12d1d3025c6b3f6fcd104658dcad1407b0
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87949266"
---
# <a name="converged-nic-configuration-with-a-single-network-adapter"></a>単一のネットワークアダプターを使用した収束 NIC 構成

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、Hyper-v ホストで1つの NIC を使用して収束 NIC を構成する手順について説明します。

このトピックの構成例では、2つの Hyper-v ホスト、 **Hyper-v ホスト A**、および**hyper-v ホスト B**について説明します。両方のホストに1つの物理 NIC (pNIC) が取り付けられており、Nic はラック ToR 物理スイッチの上に接続されてい \( \) ます。 さらに、ホストは同じサブネット (192.168.1. x/24) に配置されます。

![Hyper-V ホスト](../../media/Converged-NIC/1-single-test-conn.jpg)


## <a name="step-1-test-the-connectivity-between-source-and-destination"></a>手順 1. ソースとターゲットの間の接続をテストする

物理 NIC が宛先ホストに接続できることを確認します。 このテストでは、レイヤー 3 L3 を使用した接続と \( \) 、レイヤー 2 L2 を使用した接続を示し \( \) ます。

1. ネットワークアダプターのプロパティを表示します。

   ```PowerShell
   Get-NetAdapter
   ```

   _**生じ**_


   | 名前 |    InterfaceDescription     | ifIndex | Status |    MacAddress     | LinkSpeed |
   |------|-----------------------------|---------|--------|-------------------|-----------|
   |  M1  | Mellanox/3 Pro... |    4    |   上へ   | 7C-FE-90-93-8F-A1 |  40 Gbps  |

   ---

2. IP アドレスを含む追加のアダプターのプロパティを表示します。

   ```PowerShell
   Get-NetAdapter M1 | fl *
   ```

   _**生じ**_

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

## <a name="step-2-ensure-that-source-and-destination-can-communicate"></a>手順 2. 転送元と転送先が通信できることを確認する

このステップでは、 **Test NetConnection** Windows PowerShell コマンドを使用しますが、必要に応じて**ping**コマンドを使用することもできます。

>[!TIP]
>ホストが相互に通信できることがわかっている場合は、この手順を省略できます。

1. 双方向通信を確認します。

   ```PowerShell
   Test-NetConnection 192.168.1.5
   ```

   _**生じ**_


   |        パラメーター         |    値    |
   |--------------------------|-------------|
   |       [ComputerName]       | 192.168.1.5 |
   |      RemoteAddress       | 192.168.1.5 |
   |      InterfaceAlias      |     M1      |
   |      SourceAddress       | 192.168.1.3 |
   |      Ping 成功       |    True     |
   | PingReplyDetails \( RTT\) |    0 ミリ秒     |

   ---

   このテストを正常に実行するには、セキュリティが強化された Windows ファイアウォールを無効にすることが必要になる場合があります。 ファイアウォールを無効にした場合は、セキュリティを考慮して、構成が組織のセキュリティ要件を満たしていることを確認してください。

2. すべてのファイアウォールプロファイルを無効にします。

   ```PowerShell
   Set-NetFirewallProfile -All -Enabled False
   ```

3. ファイアウォールプロファイルを無効にした後、接続をもう一度テストします。

   ```PowerShell
   Test-NetConnection 192.168.1.5
   ```

   _**生じ**_


   |        パラメーター         |    値    |
   |--------------------------|-------------|
   |       [ComputerName]       | 192.168.1.5 |
   |      RemoteAddress       | 192.168.1.5 |
   |      InterfaceAlias      | テスト-40G-1  |
   |      SourceAddress       | 192.168.1.3 |
   |      Ping 成功       |    False    |
   | PingReplyDetails \( RTT\) |    0 ミリ秒     |

   ---



## <a name="step-3-optional-configure-the-vlan-ids-for-nics-installed-in-your-hyper-v-hosts"></a>手順 3. OptionalHyper-v ホストにインストールされている Nic の VLAN Id を構成する

多くのネットワーク構成では、Vlan を利用しています。また、ネットワークで Vlan を使用する予定がある場合は、Vlan が構成されている前のテストを繰り返す必要があります。 また、RDMA サービスに RoCE を使用する予定がある場合は、Vlan を有効にする必要があります。

この手順では、Nic は**アクセス**モードになっています。 ただし、このガイドの後半で Hyper-v 仮想スイッチ vSwitch を作成する場合、 \( \) VLAN プロパティは vSwitch ポートレベルで適用されます。

スイッチは複数の Vlan をホストできるため、ラック ToR 物理スイッチの上部に、ホストが接続されている \( \) ポートをトランクモードで構成する必要があります。

>[!NOTE]
>スイッチでトランクモードを構成する方法については、ToR スイッチのドキュメントを参照してください。

次の図は、それぞれが1つの物理ネットワークアダプターを備え、VLAN 101 で通信するように構成されている2つの Hyper-v ホストを示しています。

![仮想ローカルエリアネットワークを構成する](../../media/Converged-NIC/2-single-configure-vlans.jpg)


>[!IMPORTANT]
>この操作は、ローカルサーバーと移行先サーバーの両方で実行します。 移行先サーバーがローカルサーバーと同じ VLAN ID で構成されていない場合、2つは通信できません。


1. Hyper-v ホストにインストールされている Nic の VLAN ID を構成します。

   >[!IMPORTANT]
   >このインターフェイスを介してリモートでホストに接続している場合は、このコマンドを実行しないでください。ホストへのアクセスが失われるためです。

   ```PowerShell
   Set-NetAdapterAdvancedProperty -Name M1 -RegistryKeyword VlanID -RegistryValue "101"
   Get-NetAdapterAdvancedProperty -Name M1 | Where-Object {$_.RegistryKeyword -eq "VlanID"}
   ```

   _**生じ**_


   | 名前 | DisplayName | DisplayValue | RegistryKeyword | RegistryValue |
   |------|-------------|--------------|-----------------|---------------|
   |  M1  |   VLAN ID   |     101      |     VlanID      |     {101}     |

   ---

2. ネットワークアダプターを再起動して、VLAN ID を適用します。

   ```PowerShell
   Restart-NetAdapter -Name "M1"
   ```

3. 状態が [**稼働**中」になっていることを確認します。

   ```PowerShell
   Get-NetAdapter -Name "M1"
   ```

   _**生じ**_


   | 名前 |          InterfaceDescription           | ifIndex | Status |    MacAddress     | LinkSpeed |
   |------|-----------------------------------------|---------|--------|-------------------|-----------|
   |  M1  | Mellanox: 3 Pro イーサネット Ada... |    4    |   上へ   | 7C-FE-90-93-8F-A1 |  40 Gbps  |

   ---

   >[!IMPORTANT]
   >デバイスが再起動され、ネットワーク上で使用可能になるまで数秒かかることがあります。

4. 接続を確認します。<p>接続に失敗した場合は、スイッチ VLAN 構成または移行先が同じ VLAN に参加していることを確認します。

   ```PowerShell
   Test-NetConnection 192.168.1.5
   ```

## <a name="step-4-configure-quality-of-service-qos"></a>手順 4. サービス品質 QoS の構成 \(\)

>[!NOTE]
>相互に通信することを目的としたすべてのホストで、次の DCB と QoS の構成手順をすべて実行する必要があります。

1. \( \) 各 hyper-v ホストに Data Center ブリッジング DCB をインストールします。

   - RDMA サービスに iWarp を使用するネットワーク構成の場合は**省略可能**。
   - RDMA サービスに RoCE any バージョンを使用するネットワーク構成に**必要です** \( \) 。

   ```PowerShell
   Install-WindowsFeature Data-Center-Bridging
   ```

2. SMB ダイレクトの QoS ポリシーを設定します。

   - IWarp を使用するネットワーク構成の場合は**省略可能**。
   - RoCE を使用するネットワーク構成に**必要です**。

   次の例のコマンドでは、値 "3" は任意です。 QoS ポリシーの構成全体で同じ値を常に使用する場合は、1 ~ 7 の任意の値を使用できます。

   ```PowerShell
   New-NetQosPolicy "SMB" -NetDirectPortMatchCondition 445 -PriorityValue8021Action 3
   ```

   _**生じ**_


   |   パラメーター    |          値           |
   |----------------|--------------------------|
   |      名前      |           SMB            |
   |     所有者      | グループポリシー \( マシン\) |
   | NetworkProfile |           すべて            |
   |   優先順位   |           127            |
   |   JobObject    |          &nbsp;          |
   | NetDirectPort  |           445            |
   | PriorityValue  |            3             |

   ---

3. RoCE の展開では、iWarp では不要な SMB トラフィックの**優先順位フロー制御**を有効にします。

   ```PowerShell
   Enable-NetQosFlowControl -priority 3
   Get-NetQosFlowControl
   ```

   _**生じ**_


   | Priority | Enabled | PolicySet | IfIndex | IfAlias |
   |----------|---------|-----------|---------|---------|
   |    0     |  False  |  グローバル   | &nbsp;  | &nbsp;  |
   |    1     |  False  |  グローバル   | &nbsp;  | &nbsp;  |
   |    2     |  False  |  グローバル   | &nbsp;  | &nbsp;  |
   |    3     |  True   |  グローバル   | &nbsp;  | &nbsp;  |
   |    4     |  False  |  グローバル   | &nbsp;  | &nbsp;  |
   |    5     |  False  |  グローバル   | &nbsp;  | &nbsp;  |
   |    6     |  False  |  グローバル   | &nbsp;  | &nbsp;  |
   |    7     |  False  |  グローバル   | &nbsp;  | &nbsp;  |

   ---

4. ローカルおよび宛先のネットワークアダプターに対して QoS を有効にします。

   - IWarp を使用するネットワーク構成には**必要ありません**。
   - RoCE を使用するネットワーク構成に**必要です**。

   ```PowerShell
   Enable-NetAdapterQos -InterfaceAlias "M1"
   Get-NetAdapterQos -Name "M1"
   ```

   _**生じ**_

   **名前**: M1 **Enabled**: True

   _**機能**_


   |      パラメーター      |   ハードウェア   |   [現在]    |
   |---------------------|--------------|--------------|
   |    MacSecBypass     | NotSupported | NotSupported |
   |     DcbxSupport     |     None     |     None     |
   | NumTCs (Max////PFC) |    8/8/8     |    8/8/8     |

   ---

   _**OperationalTrafficClasses:**_


   | TC | TSA | 帯域幅 | 優先順位 |
   |----|-----|-----------|------------|
   | 0  | ETS |    70%    |  0 ~ 2、4-7   |
   | 1  | ETS |    30%    |     3      |

   ---

   _**OperationalFlowControl:**_

   優先度3が有効

   _**OperationalClassifications:**_


   | Protocol  | ポート/種類 | Priority |
   |-----------|-----------|----------|
   |  Default  |  &nbsp;   |    0     |
   | NetDirect |    445    |    3     |

   ---

5. SMB ダイレクト RDMA の帯域幅の割合を予約し \( \) ます。

    この例では、30% の帯域幅予約が使用されています。 ストレージトラフィックに必要なものを表す値を選択する必要があります。

   ```PowerShell
   New-NetQosTrafficClass "SMB" -Priority 3 -BandwidthPercentage 30 -Algorithm ETS
   ```

   _**生じ**_


   | 名前 | アルゴリズム | 帯域幅 (%) | Priority | PolicySet | IfIndex | IfAlias |
   |------|-----------|--------------|----------|-----------|---------|---------|
   | SMB  |    ETS    |      30      |    3     |  グローバル   | &nbsp;  | &nbsp;  |

   ---

6. 帯域幅予約の設定を表示します。

   ```PowerShell
   Get-NetQosTrafficClass
   ```

   _**生じ**_


   |   名前    | アルゴリズム | 帯域幅 (%) | Priority | PolicySet | IfIndex | IfAlias |
   |-----------|-----------|--------------|----------|-----------|---------|---------|
   | [Default] |    ETS    |      70      | 0 ~ 2、4-7  |  グローバル   | &nbsp;  | &nbsp;  |
   |    SMB    |    ETS    |      30      |    3     |  グローバル   | &nbsp;  | &nbsp;  |

   ---

## <a name="step-5-optional-resolve-the-mellanox-adapter-debugger-conflict"></a>手順 5. OptionalMellanox adapter デバッガーの競合を解決する

既定では、Mellanox アダプターを使用すると、アタッチされたデバッガーが NetQos をブロックします。これは既知の問題です。 このため、Mellanox からアダプターを使用し、デバッガーをアタッチする場合は、次のコマンドを使用してこの問題を解決します。 デバッガーをアタッチしない場合、または Mellanox アダプターを使用していない場合は、この手順は必要ありません。

   ```PowerShell
   Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 –Force
   ```

## <a name="step-6-verify-the-rdma-configuration-native-host"></a>手順 6. RDMA 構成 (ネイティブホスト) を確認する

VSwitch を作成し、RDMA (収束 NIC) に移行する前に、ファブリックが正しく構成されていることを確認する必要があります。

次の図は、Hyper-v ホストの現在の状態を示しています。

![RDMA をテストする](../../media/Converged-NIC/4-single-test-rdma.jpg)

1. RDMA の構成を確認します。

   ```PowerShell
   Get-NetAdapterRdma
   ```
   _**生じ**_


   | 名前 |           InterfaceDescription           | Enabled |
   |------|------------------------------------------|---------|
   |  M1  | Mellanox/3 Pro イーサネットアダプター |  True   |

   ---

2. ターゲットアダプターの**ifIndex**値を確認します。<p>この値は、ダウンロードしたスクリプトを実行するときに、後続の手順で使用します。

   ```PowerShell
   Get-NetIPConfiguration -InterfaceAlias "M*" | ft InterfaceAlias,InterfaceIndex,IPv4Address
   ```

   _**生じ**_


   | InterfaceAlias | InterfaceIndex |  IPv4Address  |
   |----------------|----------------|---------------|
   |       M2       |       14       | 192.168.1.5 |

   ---

3. [DiskSpd.exe ユーティリティ](https://aka.ms/diskspd)をダウンロードし、C:\TEST に抽出する\.

4. [テスト RDMA powershell スクリプト](https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1)をローカルドライブ上のテストフォルダー (C:\TEST など) にダウンロードします。\.

5. **Test-Rdma.ps1** PowerShell スクリプトを実行して、ifIndex 値を同じ VLAN 上のリモートアダプターの IP アドレスと共にスクリプトに渡します。<p>この例では、スクリプトはリモートネットワークアダプターの IP アドレス192.168.1.5 に**ifIndex**値14を渡します。

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
   >RDMA トラフィックが失敗した場合、特別なケースについては、ToR スイッチの構成でホストの設定と一致する必要がある適切な PFC/設定を確認してください。 参照値については、このドキュメントの「QoS」セクションを参照してください。

## <a name="step-7-remove-the-access-vlan-setting"></a>手順 7. アクセス VLAN 設定を削除します。

Hyper-v スイッチを作成するための準備として、上でインストールした VLAN 設定を削除する必要があります。

1. NIC が間違った VLAN ID で送信トラフィックの自動タグ付けを行わないように、物理 NIC からアクセス VLAN 設定を削除します。<p>この設定を削除すると、アクセス VLAN ID と一致しない受信トラフィックをフィルターで除外することもできなくなります。

   ```PowerShell
   Set-NetAdapterAdvancedProperty -Name M1 -RegistryKeyword VlanID -RegistryValue "0"
   ```

2. **VlanID の設定**で、VLAN ID の値が0と表示されていることを確認します。

   ```PowerShell
   Get-NetAdapterAdvancedProperty -name m1 | Where-Object {$_.RegistryKeyword -eq 'VlanID'}
   ```


## <a name="step-8-create-a-hyper-v-vswitch-on-your-hyper-v-hosts"></a>手順 8. Hyper-v ホストに Hyper-v vSwitch を作成する

次の図は、Hyper-v ホスト1と vSwitch を示しています。

![Hyper-v 仮想スイッチを作成する](../../media/Converged-NIC/5-single-create-vswitch.jpg)


1. Hyper-v ホスト A の Hyper-v で外部 Hyper-v vSwitch を作成します。 <p>この例では、スイッチには VMSTEST という名前が付けられています。 また、 **AllowManagementOS**パラメーターを指定すると、物理 NIC の MAC アドレスと IP アドレスを継承するホスト vNIC が作成されます。

   ```PowerShell
   New-VMSwitch -Name VMSTEST -NetAdapterName "M1" -AllowManagementOS $true
   ```
   _**生じ**_


   |  名前   | SwitchType |      NetAdapterInterfaceDescription      |
   |---------|------------|------------------------------------------|
   | VMSTEST |  外部  | Mellanox/3 Pro イーサネットアダプター |

   ---

2. ネットワークアダプターのプロパティを表示します。

   ```PowerShell
   Get-NetAdapter | ft -AutoSize
   ```

   _**生じ**_


   |         名前          |        InterfaceDescription         | ifIndex | Status |    MacAddress     | LinkSpeed |
   |-----------------------|-------------------------------------|---------|--------|-------------------|-----------|
   | VeVMSTEST Net \(\) | Hyper-v 仮想イーサネットアダプターの #2 |   27    |   上へ   | E4-1D-2D-07-40-71 |  40 Gbps  |

   ---

3. 次の2つの方法のいずれかでホスト vNIC を管理します。

   - **Netadapter**ビューは、"VeVMSTEST net の名前" に基づいて動作 \( \) します。 すべてのネットワークアダプターのプロパティがこのビューに表示されるわけではありません。
   - **VMNetworkAdapter** view は、"Veruncommand net" プレフィックスを削除し、単に vmswitch 名を使用します。 (推奨)

   ```PowerShell
   Get-VMNetworkAdapter –ManagementOS | ft -AutoSize
   ```

   _**生じ**_


   |         名前         | IsManagementOs |        VMName        |  SwitchName  | MacAddress | Status | IPAddresses |
   |----------------------|----------------|----------------------|--------------|------------|--------|-------------|
   | CORP-外部スイッチ |      True      | CORP-外部スイッチ | 001B785768AA |    Ok] を    | &nbsp; |             |
   |       VMSTEST        |      True      |       VMSTEST        | E41D2D074071 |    Ok] を    | &nbsp; |             |

   ---

4. 接続をテストします。

   ```Powershell
   Test-NetConnection 192.168.1.5
   ```

   _**生じ**_

   ```
    ComputerName   : 192.168.1.5
    RemoteAddress  : 192.168.1.5
    InterfaceAlias : vEthernet (CORP-External-Switch)
    SourceAddress  : 192.168.1.3
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms
   ```

5. ネットワークアダプターの VLAN 設定を割り当てて表示します。

   ```PowerShell
   Set-VMNetworkAdapterVlan -VMNetworkAdapterName "VMSTEST" -VlanId "101" -Access -ManagementOS
   Get-VMNetworkAdapterVlan -ManagementOS -VMNetworkAdapterName "VMSTEST"
   ```

   _**生じ**_


   | VMName | Vmnetworkadaptername は |  モード  | VlanList |
   |--------|----------------------|--------|----------|
   | &nbsp; |       VMSTEST        | Access |   101    |

   ---

6. 接続をテストします。<p>他のアダプターに対して正常に ping を実行するには、完了までに数秒かかることがあります。

   ```PowerShell
   Test-NetConnection 192.168.1.5
   ```

   _**生じ**_

   ```
    ComputerName   : 192.168.1.5
    RemoteAddress  : 192.168.1.5
    InterfaceAlias : vEthernet (VMSTEST)
    SourceAddress  : 192.168.1.3
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms
   ```

## <a name="step-9-test-hyper-v-virtual-switch-rdma-mode-2"></a>手順 9. Hyper-v 仮想スイッチ RDMA (モード 2) のテスト

次の図は、hyper-v ホストの現在の状態を示しています。 hyper-v ホスト1の vSwitch を含みます。

![Hyper-v 仮想スイッチをテストする](../../media/Converged-NIC/6-single-test-vswitch-rdma.jpg)


1. ホスト vNIC で優先順位のタグ付けを設定します。

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -Name "VMSTEST" -IeeePriorityTag on
   Get-VMNetworkAdapter -ManagementOS -Name "VMSTEST" | fl Name,IeeePriorityTag
   ```

   _**生じ**_

    名前: VMSTEST Ieeeの優先順位タグ: On


2. ネットワークアダプターの RDMA 情報を表示します。

   ```PowerShell
   Get-NetAdapterRdma
   ```

   _**生じ**_


   |         名前          |        InterfaceDescription         | Enabled |
   |-----------------------|-------------------------------------|---------|
   | VeVMSTEST Net \(\) | Hyper-v 仮想イーサネットアダプターの #2 |  False  |

   ---

   >[!NOTE]
   >**有効になっ**ているパラメーターの値が**False**の場合は、RDMA が有効になっていないことを示します。


3. ネットワークアダプターの情報を表示します。

   ```PowerShell
   Get-NetAdapter
   ```

   _**生じ**_


   |        名前         |        InterfaceDescription         | ifIndex | Status |    MacAddress     | LinkSpeed |
   |---------------------|-------------------------------------|---------|--------|-------------------|-----------|
   | Veruncommand Net (VMSTEST) | Hyper-v 仮想イーサネットアダプターの #2 |   27    |   上へ   | E4-1D-2D-07-40-71 |  40 Gbps  |

   ---


4. ホスト vNIC で RDMA を有効にします。

   ```PowerShell
   Enable-NetAdapterRdma -Name "vEthernet (VMSTEST)"
   Get-NetAdapterRdma -Name "vEthernet (VMSTEST)"
   ```

   _**生じ**_


   |         名前          |        InterfaceDescription         | Enabled |
   |-----------------------|-------------------------------------|---------|
   | VeVMSTEST Net \(\) | Hyper-v 仮想イーサネットアダプターの #2 |  True   |

   ---

   >[!NOTE]
   >**有効になっ**ているパラメーターの値が**True**の場合は、RDMA が有効になっていることを意味します。

5. RDMA トラフィックテストを実行します。

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

この出力の最後の行である "RDMA トラフィックテストが成功しました: RDMA トラフィックは192.168.1.5 に送信されました" と表示されます。これは、アダプターに収束 NIC を正常に構成したことを示しています。

## <a name="related-topics"></a>関連トピック
- [収束 NIC チーミング NIC 構成](cnic-datacenter.md)
- [収束 NIC の物理スイッチ構成](cnic-app-switch-config.md)
- [収束 NIC 構成のトラブルシューティング](cnic-app-troubleshoot.md)
