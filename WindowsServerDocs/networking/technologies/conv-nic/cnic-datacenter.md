---
title: チーム化される NIC 構成 (datacenter) での収束 NIC
description: このトピックでは、スイッチ埋め込みチーミング (SET) を使用して、チーム化された NIC 構成で収束 NIC を展開する手順について説明します。
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: f01546f8-c495-4055-8492-8806eee99862
manager: dougkim
ms.author: lizross
author: eross-msft
ms.date: 09/17/2018
ms.openlocfilehash: 54471446fb9eab6dc5dc20043c7cb651766a59a9
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80309647"
---
# <a name="converged-nic-in-a-teamed-nic-configuration-datacenter"></a>チーム化される NIC 構成 (datacenter) での収束 NIC

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、スイッチ埋め込みチーミング \(SET\)を使用して、チーム化された NIC 構成で収束 NIC を展開する手順について説明します。 

このトピックの構成例では、2つの hyper-v ホスト ( **Hyper-v ホスト 1**と**hyper-v ホスト 2**) について説明します。 両方のホストに2つのネットワークアダプターがあります。 各ホストでは、1つのアダプターが 192.168.1. x/24 サブネットに接続され、1つのアダプターが 192.168.2/24 サブネットに接続されます。

![Hyper-V ホスト](../../media/Converged-NIC/1-datacenter-test-conn.jpg)

## <a name="step-1-test-the-connectivity-between-source-and-destination"></a>手順 1. ソースとターゲットの間の接続をテストする

物理 NIC が宛先ホストに接続できることを確認します。  このテストでは、レイヤー 3 \(L3\) または IP レイヤーに加えて、レイヤー 2 \(L2\) 仮想ローカルエリアネットワーク \(VLAN\)を使用して接続をデモンストレーションします。

1. 最初のネットワークアダプターのプロパティを表示します。

   ```PowerShell
   Get-NetAdapter -Name "Test-40G-1" | ft -AutoSize
   ```

   _**生じ**_


   |    Name    |           InterfaceDescription           | ifIndex | 状態 |    Mac     | LinkSpeed |
   |------------|------------------------------------------|---------|--------|-------------------|-----------|
   | テスト-40G-1 | Mellanox/3 Pro イーサネットアダプター |   11    |   上へ   | E4-1D-07-43-D0 |  40 Gbps  |

   ---

2. 最初のアダプターの追加のプロパティ (IP アドレスを含む) を表示します。 

   ```PowerShell
   Get-NetIPAddress -InterfaceAlias "Test-40G-1"
   Get-NetIPAddress -InterfaceAlias "TEST-40G-1" | Where-Object {$_.AddressFamily -eq "IPv4"} | fl InterfaceAlias,IPAddress
   ```

   _**生じ**_


   |   パラメーター    |    値    |
   |----------------|-------------|
   |   IPAddress    | 192.168.1.3 |
   | InterfaceIndex |     11      |
   | InterfaceAlias | テスト-40G-1  |
   | AddressFamily  |    IPv4     |
   |      種類      |   ユニキャスト   |
   |  プレフィックス  |     24      |

   ---

3. 2番目のネットワークアダプターのプロパティを表示します。

   ```PowerShell
   Get-NetAdapter -Name "Test-40G-2" | ft -AutoSize
   ```

   _**生じ**_


   |    Name    |          InterfaceDescription           | ifIndex | 状態 |    Mac     | LinkSpeed |
   |------------|-----------------------------------------|---------|--------|-------------------|-----------|
   | テスト-40G-2 | Mellanox/3 Pro イーサネット A... #2 |   13    |   上へ   | E4-1D-2D-07-40-70 |  40 Gbps  |

   ---

4. 2番目のアダプターの追加のプロパティ (IP アドレスを含む) を表示します。

   ```PowerShell
   Get-NetIPAddress -InterfaceAlias "Test-40G-2"
   Get-NetIPAddress -InterfaceAlias "Test-40G-2" | Where-Object {$_.AddressFamily -eq "IPv4"} | fl InterfaceAlias,IPAddress
   ```

   _**生じ**_


   |   パラメーター    |    値    |
   |----------------|-------------|
   |   IPAddress    | 192.168.2.3 |
   | InterfaceIndex |     13      |
   | InterfaceAlias | テスト-40G-2  |
   | AddressFamily  |    IPv4     |
   |      種類      |   ユニキャスト   |
   |  プレフィックス  |     24      |

   ---

5. 他の NIC チームまたは SET member pNICs に有効な IP アドレスがあることを確認します。<p>別のサブネットを使用して、xxx.xxx \(します。**2**. xxx vs xxx.xxx。**1**. xxx\)、このアダプターから宛先への送信を容易にします。 そうしないと、両方の2つの pNICs を同じサブネットに配置すると、Windows TCP/IP stack のインターフェイス間の負荷分散と、単純な検証がより複雑になります。


## <a name="step-2-ensure-that-source-and-destination-can-communicate"></a>手順 2. 転送元と転送先が通信できることを確認する

このステップでは、 **Test NetConnection** Windows PowerShell コマンドを使用しますが、必要に応じて**ping**コマンドを使用することもできます。 

1. 双方向通信を確認します。

   ```PowerShell
   Test-NetConnection 192.168.1.5
   ```

   _**生じ**_


   |        パラメーター         |    値    |
   |--------------------------|-------------|
   |       ComputerName       | 192.168.1.5 |
   |      リモート アドレス       | 192.168.1.5 |
   |      InterfaceAlias      | テスト-40G-1  |
   |      SourceAddress       | 192.168.1.3 |
   |      Ping 成功       |    False    |
   | PingReplyDetails \(RTT\) |    0 ミリ秒     |

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
   |       ComputerName       | 192.168.1.5 |
   |      リモート アドレス       | 192.168.1.5 |
   |      InterfaceAlias      | テスト-40G-1  |
   |      SourceAddress       | 192.168.1.3 |
   |      Ping 成功       |    False    |
   | PingReplyDetails \(RTT\) |    0 ミリ秒     |

   ---


4. 追加の Nic の接続を確認します。 NIC またはセットチームに含まれる後続のすべての pNICs に対して、前の手順を繰り返します。

   ```PowerShell    
   Test-NetConnection 192.168.2.5
   ```

   _**生じ**_


   |        パラメーター         |    値    |
   |--------------------------|-------------|
   |       ComputerName       | 192.168.2.5 |
   |      リモート アドレス       | 192.168.2.5 |
   |      InterfaceAlias      | テスト-40G-2  |
   |      SourceAddress       | 192.168.2.3 |
   |      Ping 成功       |    False    |
   | PingReplyDetails \(RTT\) |    0 ミリ秒     |

   ---

## <a name="step-3-configure-the-vlan-ids-for-nics-installed-in-your-hyper-v-hosts"></a>手順 3. Hyper-v ホストにインストールされている Nic の VLAN Id を構成する

多くのネットワーク構成では、Vlan を利用しています。また、ネットワークで Vlan を使用する予定がある場合は、Vlan が構成されている前のテストを繰り返す必要があります。

この手順では、Nic は**アクセス**モードになっています。 ただし、このガイドの後半で Hyper-v 仮想スイッチ \(vSwitch\) を作成すると、vSwitch ポートレベルで VLAN プロパティが適用されます。 

スイッチは複数の Vlan をホストできるため、ラックの上部 \(ToR\) 物理スイッチが、ホストが接続されているポートをトランクモードで構成する必要があります。

>[!NOTE]
>スイッチでトランクモードを構成する方法については、ToR スイッチのドキュメントを参照してください。

次の図は、ネットワークアダプターのプロパティで VLAN 101 と VLAN 102 が構成されている2つのネットワークアダプターを持つ2つの Hyper-v ホストを示しています。

![仮想ローカルエリアネットワークを構成する](../../media/Converged-NIC/2-datacenter-configure-vlans.jpg)


>[!TIP]
>IEEE\) ネットワーク標準 \(IEEE の電気およびエレクトロニクスエンジニアによれば、物理 NIC のサービス品質 \(QoS\) プロパティは、VLAN ID を構成するときに、802.1 Q \(VLAN\) ヘッダーに埋め込まれている 802.1 p ヘッダーで動作します。

1. 最初の NIC の VLAN ID を構成します。

   ```PowerShell    
   Set-NetAdapterAdvancedProperty -Name "Test-40G-1" -RegistryKeyword VlanID -RegistryValue "101"
   Get-NetAdapterAdvancedProperty -Name "Test-40G-1" | Where-Object {$_.RegistryKeyword -eq "VlanID"} | ft -AutoSize
   ```

   _**生じ**_   


   |    Name    | DisplayName | DisplayValue | RegistryKeyword | RegistryValue |
   |------------|-------------|--------------|-----------------|---------------|
   | テスト-40G-1 |   VLAN ID   |     101      |     VlanID      |     {101}     |

   ---

2. ネットワークアダプターを再起動して、VLAN ID を適用します。

   ```PowerShell
   Restart-NetAdapter -Name "Test-40G-1"
   ```

3. 状態が **稼働**中」になっていることを確認します。

   ```PowerShell
   Get-NetAdapter -Name "Test-40G-1" | ft -AutoSize
   ```

   _**生じ**_


   |    Name    |          InterfaceDescription           | ifIndex | 状態 |    Mac     | LinkSpeed |
   |------------|-----------------------------------------|---------|--------|-------------------|-----------|
   | テスト-40G-1 | Mellanox: 3 Pro イーサネット Ada... |   11    |   上へ   | E4-1D-07-43-D0 |  40 Gbps  |

   ---

4. 2番目の NIC の VLAN ID を構成します。テスト-40G-2

   ```PowerShell    
   Set-NetAdapterAdvancedProperty -Name "Test-40G-2" -RegistryKeyword VlanID -RegistryValue "102"
   Get-NetAdapterAdvancedProperty -Name "Test-40G-2" | Where-Object {$_.RegistryKeyword -eq "VlanID"} | ft -AutoSize
   ``` 

   _**生じ**_


   |    Name    | DisplayName | DisplayValue | RegistryKeyword | RegistryValue |
   |------------|-------------|--------------|-----------------|---------------|
   | テスト-40G-2 |   VLAN ID   |     102      |     VlanID      |     {102}     |

   ---

5. ネットワークアダプターを再起動して、VLAN ID を適用します。

   ```PowerShell
   Restart-NetAdapter -Name "Test-40G-2" 
   ```

6. 状態が **稼働**中」になっていることを確認します。

   ```PowerShell
   Get-NetAdapter -Name "Test-40G-1" | ft -AutoSize
   ```

   _**生じ**_


   |    Name    |          InterfaceDescription           | ifIndex | 状態 |    Mac     | LinkSpeed |
   |------------|-----------------------------------------|---------|--------|-------------------|-----------|
   | テスト-40G-2 | Mellanox: 3 Pro イーサネット Ada... |   11    |   上へ   | E4-1D-07-43-D1 |  40 Gbps  |

   ---

   >[!IMPORTANT]
   >デバイスが再起動され、ネットワーク上で使用可能になるまで数秒かかることがあります。 

7. 最初の NIC の接続を確認し、テスト-40G-1 を使用します。<p>接続に失敗した場合は、スイッチ VLAN 構成または移行先が同じ VLAN に参加していることを確認します。 

   ```PowerShell
   Test-NetConnection 192.168.1.5
   ```

   _**生じ**_   


   |        パラメーター         |    値    |
   |--------------------------|-------------|
   |       ComputerName       | 192.168.1.5 |
   |      リモート アドレス       | 192.168.1.5 |
   |      InterfaceAlias      | テスト-40G-1  |
   |      SourceAddress       | 192.168.1.5 |
   |      Ping 成功       |    True     |
   | PingReplyDetails \(RTT\) |    0 ミリ秒     |

   ---

8. 最初の NIC の接続を確認し、テスト-40G-2 を行います。<p>接続に失敗した場合は、スイッチ VLAN 構成または移行先が同じ VLAN に参加していることを確認します。

   ```PowerShell    
   Test-NetConnection 192.168.2.5
   ```

   _**生じ**_    


   |        パラメーター         |    値    |
   |--------------------------|-------------|
   |       ComputerName       | 192.168.2.5 |
   |      リモート アドレス       | 192.168.2.5 |
   |      InterfaceAlias      | テスト-40G-2  |
   |      SourceAddress       | 192.168.2.3 |
   |      Ping 成功       |    True     |
   | PingReplyDetails \(RTT\) |    0 ミリ秒     |

   ---

   >[!IMPORTANT]
   >**再起動 Netconnection**を実行した直後に、**テスト netconnection**または ping エラーが発生することは珍しくありません。  ネットワークアダプターが完全に初期化されるのを待ってから、もう一度やり直してください。
   >
   >VLAN 101 接続が機能していても、VLAN 102 接続が機能していない場合は、目的の VLAN でポートトラフィックを許可するようにスイッチを構成する必要があるという問題があります。 これを確認するには、障害が発生しているアダプターを一時的に VLAN 101 に設定し、接続テストを繰り返します。


   次の図は、Vlan を正常に構成した後の Hyper-v ホストを示しています。

   ![サービスの品質の構成](../../media/Converged-NIC/3-datacenter-configure-qos.jpg)


## <a name="step-4-configure-quality-of-service-qos"></a>手順 4. QoS\) \(サービスの品質を構成する

>[!NOTE]
>相互に通信することを目的としたすべてのホストで、次の DCB と QoS の構成手順をすべて実行する必要があります。

1. 各 Hyper-v ホストにデータセンターブリッジング \(DCB\) をインストールします。

   - IWarp を使用するネットワーク構成の場合は**省略可能**。
   - RoCE \(RDMA サービスのすべてのバージョン\) を使用するネットワーク構成に**必要です**。

   ```PowerShell
   Install-WindowsFeature Data-Center-Bridging
   ```

   _**生じ**_


   | 成功 | 再起動が必要 | 終了コード |     機能の結果     |
   |---------|----------------|-----------|------------------------|
   |  True   |       いいえ       |  成功  | {データセンターブリッジング} |

   ---

2. SMB ダイレクトの QoS ポリシーを設定します。

   - IWarp を使用するネットワーク構成の場合は**省略可能**。
   - RoCE \(RDMA サービスのすべてのバージョン\) を使用するネットワーク構成に**必要です**。

   次の例のコマンドでは、値 "3" は任意です。 QoS ポリシーの構成全体で同じ値を常に使用する場合は、1 ~ 7 の任意の値を使用できます。

   ```PowerShell
   New-NetQosPolicy "SMB" -NetDirectPortMatchCondition 445 -PriorityValue8021Action 3
   ```

   _**生じ**_


   |   パラメーター    |          値           |
   |----------------|--------------------------|
   |      Name      |           SMB            |
   |     所有者      | グループポリシー \(マシン\) |
   | NetworkProfile |           [すべて]            |
   |   ［優先順位］   |           127            |
   |   JobObject    |          &nbsp;          |
   | NetDirectPort  |           445            |
   | PriorityValue  |            3             |

   ---

3. インターフェイス上の他のトラフィックに対して追加の QoS ポリシーを設定します。   

   ```PowerShell
   New-NetQosPolicy "DEFAULT" -Default -PriorityValue8021Action 0
   ```

   _**生じ**_   


   |   パラメーター    |          値           |
   |----------------|--------------------------|
   |      Name      |         DEFAULT          |
   |     所有者      | グループポリシー \(マシン\) |
   | NetworkProfile |           [すべて]            |
   |   ［優先順位］   |           127            |
   |    テンプレート    |         既定値          |
   |   JobObject    |          &nbsp;          |
   | PriorityValue  |            0             |

   ---

4. SMB トラフィックの**優先順位フロー制御**を有効にします。これは iwarp には必要ありません。

   ```PowerShell
   Enable-NetQosFlowControl -priority 3
   Get-NetQosFlowControl
   ```

   _**生じ**_


   | 優先順位 | 有効 | PolicySet | ifIndex | IfAlias |
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

   >**重要**3以外の項目で Enabled 値が True に設定されているために結果がこれらの結果と一致しない場合は、これらのクラスに対して**Flowcontrol**を無効にする必要があります。
   >
   >```PowerShell
   >Disable-NetQosFlowControl -priority 0,1,2,4,5,6,7
   >Get-NetQosFlowControl
   >```
   >より複雑な構成では、他のトラフィッククラスにフロー制御が必要になる場合がありますが、これらのシナリオはこのガイドでは説明しません。


5. 最初の NIC で QoS を有効にし、テスト-40G-1 を有効にします。

   ```PowerShell
   Enable-NetAdapterQos -InterfaceAlias "Test-40G-1"
   Get-NetAdapterQos -Name "Test-40G-1"

   Name: TEST-40G-1 
   Enabled: True
   ```
   _**機能**:_   


   |      パラメーター      |   ハードウェア   |   現在    |
   |---------------------|--------------|--------------|
   |    MacSecBypass     | NotSupported | NotSupported |
   |     DcbxSupport     |     なし     |     なし     |
   | NumTCs (Max////PFC) |    8/8/8     |    8/8/8     |

   ---

   _**OperationalTrafficClasses**:_    


   | フィールド |  TSA   | 帯域幅 | 主 |
   |----|--------|-----------|------------|
   | 0  | Strict |  &nbsp;   |    0-7     |

   ---

   _**OperationalFlowControl**:_  

   優先度3が有効  

   _**OperationalClassifications**:_  


   | [プロトコル]  | ポート/種類 | 優先順位 |
   |-----------|-----------|----------|
   |  既定値  |  &nbsp;   |    0     |
   | NetDirect |    445    |    3     |

   ---

6. 2番目の NIC の QoS を有効にします。テスト-40G-2。

   ```PowerShell
   Enable-NetAdapterQos -InterfaceAlias "Test-40G-2"
   Get-NetAdapterQos -Name "Test-40G-2"

   Name: TEST-40G-2 
   Enabled: True 
   ```

   _**機能**:_ 


   |      パラメーター      |   ハードウェア   |   現在    |
   |---------------------|--------------|--------------|
   |    MacSecBypass     | NotSupported | NotSupported |
   |     DcbxSupport     |     なし     |     なし     |
   | NumTCs (Max////PFC) |    8/8/8     |    8/8/8     |

   ---

   _**OperationalTrafficClasses**:_  


   | フィールド |  TSA   | 帯域幅 | 主 |
   |----|--------|-----------|------------|
   | 0  | Strict |  &nbsp;   |    0-7     |

   ---

    _**OperationalFlowControl**:_  

    優先度3が有効  

   _**OperationalClassifications**:_  


   | [プロトコル]  | ポート/種類 | 優先順位 |
   |-----------|-----------|----------|
   |  既定値  |  &nbsp;   |    0     |
   | NetDirect |    445    |    3     |

   ---


7. SMB ダイレクト \(RDMA\) に帯域幅の半分を確保する

   ```PowerShell
   New-NetQosTrafficClass "SMB" -priority 3 -bandwidthpercentage 50 -algorithm ETS
   ```

   _**生じ**_  


   | Name | アルゴリズム | 帯域幅 (%) | 優先順位 | PolicySet | ifIndex | IfAlias |
   |------|-----------|--------------|----------|-----------|---------|---------|
   | SMB  |    ETS    |      50      |    3     |  グローバル   | &nbsp;  | &nbsp;  |

   ---

8. 帯域幅予約の設定を表示します。   

   ```PowerShell
   Get-NetQosTrafficClass | ft -AutoSize
   ```

   _**生じ**_  


   |   Name    | アルゴリズム | 帯域幅 (%) | 優先順位 | PolicySet | ifIndex | IfAlias |
   |-----------|-----------|--------------|----------|-----------|---------|---------|
   | [Default] |    ETS    |      50      | 0 ~ 2、4-7  |  グローバル   | &nbsp;  | &nbsp;  |
   |    SMB    |    ETS    |      50      |    3     |  グローバル   | &nbsp;  | &nbsp;  |

   ---

9. Optionalテナント IP トラフィック用に2つの追加のトラフィッククラスを作成します。 

   >[!TIP]
   >"IP1" と "IP2" の値は省略できます。

   ```PowerShell
   New-NetQosTrafficClass "IP1" -Priority 1 -bandwidthpercentage 10 -algorithm ETS
   ```

   _**生じ**_


   | Name | アルゴリズム | 帯域幅 (%) | 優先順位 | PolicySet | ifIndex | IfAlias |
   |------|-----------|--------------|----------|-----------|---------|---------|
   | IP1  |    ETS    |      10      |    1     |  グローバル   | &nbsp;  | &nbsp;  |

   ---

   ```PowerShell
   New-NetQosTrafficClass "IP2" -Priority 2 -bandwidthpercentage 10 -algorithm ETS
   ```

   _**生じ**_


   | Name | アルゴリズム | 帯域幅 (%) | 優先順位 | PolicySet | ifIndex | IfAlias |
   |------|-----------|--------------|----------|-----------|---------|---------|
   | IP2  |    ETS    |      10      |    2     |  グローバル   | &nbsp;  | &nbsp;  |

   ---

10. QoS トラフィッククラスを表示します。

    ```PowerShell
    Get-NetQosTrafficClass | ft -AutoSize
    ```

    _**生じ**_


    |   Name    | アルゴリズム | 帯域幅 (%) | 優先順位 | PolicySet | ifIndex | IfAlias |
    |-----------|-----------|--------------|----------|-----------|---------|---------|
    | [Default] |    ETS    |      30      |  0、4-7   |  グローバル   | &nbsp;  | &nbsp;  |
    |    SMB    |    ETS    |      50      |    3     |  グローバル   | &nbsp;  | &nbsp;  |
    |    IP1    |    ETS    |      10      |    1     |  グローバル   | &nbsp;  | &nbsp;  |
    |    IP2    |    ETS    |      10      |    2     |  グローバル   | &nbsp;  | &nbsp;  |

    ---

11. Optionalデバッガーをオーバーライドします。<p>既定では、アタッチされたデバッガーは NetQos をブロックします。 

    ```PowerShell
    Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 –Force
    Get-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" | ft AllowFlowControlUnderDebugger
    ```

    _**生じ**_  

    ```
    AllowFlowControlUnderDebugger
    -----------------------------
    1
    ```

## <a name="step-5-verify-the-rdma-configuration-mode-1"></a>手順 5. RDMA 構成 \(モード 1\) を確認してください 

VSwitch を作成して RDMA \(モード 2\)に移行する前に、ファブリックが正しく構成されていることを確認する必要があります。

次の図は、Hyper-v ホストの現在の状態を示しています。

![RDMA をテストする](../../media/Converged-NIC/4-datacenter-test-rdma.jpg)


1. RDMA の構成を確認します。

   ```PowerShell
   Get-NetAdapterRdma | ft -AutoSize
   ```

   _**生じ**_


   |    Name    |        InterfaceDescription        | 有効 |
   |------------|------------------------------------|---------|
   | テスト-40G-1 | Mellanox/4 VPI Adapter #2 |  True   |
   | テスト-40G-2 |  Mellanox の送信-4 VPI Adapter   |  True   |

   ---

2. ターゲットアダプターの**ifIndex**値を確認します。<p>この値は、ダウンロードしたスクリプトを実行するときに、後続の手順で使用します。   

   ```PowerShell
   Get-NetIPConfiguration -InterfaceAlias "TEST*" | ft InterfaceAlias,InterfaceIndex,IPv4Address
   ```

   _**生じ**_


   | InterfaceAlias | InterfaceIndex |  IPv4Address  |
   |----------------|----------------|---------------|
   |   テスト-40G-1   |       14       | {192.168.1.3} |
   |   テスト-40G-2   |       13       | {192.168.2.3} |

   ---

3. [Diskspd .exe ユーティリティ](https://aka.ms/diskspd)をダウンロードし、C:\TEST に抽出し\.

4. [テスト RDMA PowerShell スクリプト](https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1)をローカルドライブ上のテストフォルダーにダウンロードします (例: C:\TEST\.

5. **Test-Rdma** PowerShell スクリプトを実行して、ifIndex の値を、同じ VLAN 上の最初のリモートアダプターの IP アドレスと共にスクリプトに渡します。<p>この例では、スクリプトはリモートネットワークアダプターの IP アドレス192.168.1.5 に**ifIndex**値14を渡します。

   ```PowerShell
   C:\TEST\Test-RDMA.PS1 -IfIndex 14 -IsRoCE $true -RemoteIpAddress 192.168.1.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```

   _**生じ**_ 

   ```   
   VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\diskspd.exe
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

6. **Test-Rdma** PowerShell スクリプトを実行して、ifIndex の値を、同じ VLAN 上の2番目のリモートアダプターの IP アドレスと共にスクリプトに渡します。<p>この例では、スクリプトはリモートネットワークアダプターの IP アドレス192.168.2.5 に13の**ifIndex**値を渡します。

   ```PowerShell
   C:\TEST\Test-RDMA.PS1 -IfIndex 13 -IsRoCE $true -RemoteIpAddress 192.168.2.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```

   _**生じ**_ 

   ```   
   VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\diskspd.exe
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
   ``` 

## <a name="step-6-create-a-hyper-v-vswitch-on-your-hyper-v-hosts"></a>手順 6. Hyper-v ホストに Hyper-v vSwitch を作成する


次の図は、Hyper-v ホスト1と vSwitch を示しています。

![Hyper-v 仮想スイッチを作成する](../../media/Converged-NIC/5-datacenter-create-vswitch.jpg)

1. Hyper-v ホスト1で設定モードで vSwitch を作成します。

   ```PowerShell
   New-VMSwitch –Name "VMSTEST" –NetAdapterName "TEST-40G-1","TEST-40G-2" -EnableEmbeddedTeaming $true -AllowManagementOS $true
   ```

   _**結果**_


   |  Name   | SwitchType | NetAdapterInterfaceDescription |
   |---------|------------|--------------------------------|
   | VMSTEST |  外部リンク  |        チーム化-インターフェイス        |

   ---

2. 設定されている物理アダプターチームを表示します。

   ```PowerShell
   Get-VMSwitchTeam -Name "VMSTEST" | fl
   ```

   _**生じ**_  

   ```
   Name: VMSTEST  
   Id: ad9bb542-dda2-4450-a00e-f96d44bdfbec  
   NetAdapterInterfaceDescription: {Mellanox ConnectX-3 Pro Ethernet Adapter, Mellanox ConnectX-3 Pro Ethernet Adapter #2}  
   TeamingMode: SwitchIndependent  
   LoadBalancingAlgorithm: Dynamic   
   ```

3. ホスト vNIC の2つのビューを表示します。

   ```PowerShell
    Get-NetAdapter
   ```

   _**生じ**_


   |        Name         |        InterfaceDescription         | ifIndex | 状態 |    Mac     | LinkSpeed |
   |---------------------|-------------------------------------|---------|--------|-------------------|-----------|
   | Veruncommand Net (VMSTEST) | Hyper-v 仮想イーサネットアダプターの #2 |   28    |   上へ   | E4-1D-2D-07-40-71 |  80 Gbps  |

   ---

4. ホスト vNIC のその他のプロパティを表示します。 

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS
   ```

   _**生じ**_


   |  Name   | IsManagementOs | VMName  |  SwitchName  | Mac | 状態 | IPAddresses |
   |---------|----------------|---------|--------------|------------|--------|-------------|
   | VMSTEST |      True      | VMSTEST | E41D2D074071 |    Ok を    | &nbsp; |             |

   ---


5. リモート VLAN 101 アダプターへのネットワーク接続をテストします。

   ```PowerShell
   Test-NetConnection 192.168.1.5 
   ```

   _**生じ**_  

   ```
   WARNING: Ping to 192.168.1.5 failed -- Status: DestinationHostUnreachable

   ComputerName   : 192.168.1.5
   RemoteAddress  : 192.168.1.5
   InterfaceAlias : vEthernet (CORP-External-Switch)
   SourceAddress  : 10.199.48.170
   PingSucceeded  : False
   PingReplyDetails (RTT) : 0 ms
   ```

## <a name="step-7-remove-the-access-vlan-setting"></a>手順 7. アクセス VLAN 設定を削除します。

この手順では、物理 NIC からアクセス VLAN 設定を削除し、vSwitch を使用して VLANID を設定します。

間違った VLAN ID の送信トラフィックを自動でタグ付けしたり、アクセス VLAN ID と一致しない受信トラフィックをフィルター処理したりしないように、アクセス VLAN 設定を削除する必要があります。

1. 設定を削除します。

   ```PowerShell
   Set-NetAdapterAdvancedProperty -Name "Test-40G-1" -RegistryKeyword VlanID -RegistryValue "0"
   Set-NetAdapterAdvancedProperty -Name "Test-40G-2" -RegistryKeyword VlanID -RegistryValue "0"
   ```

2. VLAN ID を設定します。

   ```PowerShell
   Set-VMNetworkAdapterVlan -VMNetworkAdapterName "VMSTEST" -VlanId "101" -Access -ManagementOS
   Get-VMNetworkAdapterVlan -ManagementOS -VMNetworkAdapterName "VMSTEST"
   ```

   _**生じ**_  

   ```
   VMName VMNetworkAdapterName Mode   VlanList
   ------ -------------------- ----   --------
          VMSTEST              Access 101     
   ```


3. ネットワーク接続をテストします。

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

   >**重要**結果が例の結果と類似していない場合、"WARNING: Ping to 192.168.1.5 failed--Status: DestinationHostUnreachable できません" というメッセージが表示されて ping が失敗する場合は、"Ve Net (VMSTEST)" に適切な IP アドレスがあることを確認してください。
   >
   >```PowerShell
   >Get-NetIPAddress -InterfaceAlias "vEthernet (VMSTEST)"
   >```
   >
   >IP アドレスが設定されていない場合は、問題を解決します。
   >
   >```PowerShell
   >New-NetIPAddress -InterfaceAlias "vEthernet (VMSTEST)" -IPAddress 192.168.1.3 -PrefixLength 24
   >
   >IPAddress : 192.168.1.3
   >InterfaceIndex: 37
   >InterfaceAlias: vEthernet (VMSTEST)
   >AddressFamily : IPv4
   >Type  : Unicast
   >PrefixLength  : 24
   >PrefixOrigin  : Manual
   >SuffixOrigin  : Manual
   >AddressState  : Tentative
   >ValidLifetime : Infinite ([TimeSpan]::MaxValue)
   >PreferredLifetime : Infinite ([TimeSpan]::MaxValue)
   >SkipAsSource  : False
   >PolicyStore   : ActiveStore
   >```  


4. 管理 NIC の名前を変更します。

   ```PowerShell
   Rename-VMNetworkAdapter -ManagementOS -Name “VMSTEST” -NewName “MGT”
   Get-VMNetworkAdapter -ManagementOS
   ```

   _**生じ**_ 


   |         Name         | IsManagementOs | VMName |      SwitchName      |  Mac  | 状態 | IPAddresses |
   |----------------------|----------------|--------|----------------------|--------------|--------|-------------|
   | CORP-外部スイッチ |      True      | &nbsp; | CORP-外部スイッチ | 001B785768AA |  Ok を  |   &nbsp;    |
   |         管理          |      True      | &nbsp; |       VMSTEST        | E41D2D074071 |  Ok を  |   &nbsp;    |

   ---

5. 追加の NIC プロパティを表示します。

   ```PowerShell
   Get-NetAdapter
   ```

   _**生じ**_


   |      Name       |        InterfaceDescription         | ifIndex | 状態 |    Mac     | LinkSpeed |
   |-----------------|-------------------------------------|---------|--------|-------------------|-----------|
   | Ve・ Net (の場合) | Hyper-v 仮想イーサネットアダプターの #2 |   28    |   上へ   | E4-1D-2D-07-40-71 |  80 Gbps  |

   ---

## <a name="step-8-test-hyper-v-vswitch-rdma"></a>手順 8. Hyper-v vSwitch RDMA のテスト

次の図は、hyper-v ホストの現在の状態を示しています (hyper-v ホスト1の vSwitch を含む)。

![Hyper-v 仮想スイッチをテストする](../../media/Converged-NIC/6-datacenter-test-vswitch-rdma.jpg)

1. ホスト vNIC の優先順位のタグ付けを設定して、以前の VLAN 設定を補完します。

   ```PowerShell    
   Set-VMNetworkAdapter -ManagementOS -Name "MGT" -IeeePriorityTag on
   Get-VMNetworkAdapter -ManagementOS -Name "MGT" | fl Name,IeeePriorityTag
   ```

   _**生じ**_  

   名前: 「」  
   Ieee優先順位タグ: オン  

2. RDMA 用に2つのホスト vNICs を作成し、vSwitch VMSTEST に接続します。

   ```PowerShell    
   Add-VMNetworkAdapter –SwitchName "VMSTEST" –Name SMB1 –ManagementOS
   Add-VMNetworkAdapter –SwitchName "VMSTEST" –Name SMB2 –ManagementOS
   ```

3. 管理 NIC のプロパティを表示します。

   ```PowerShell    
   Get-VMNetworkAdapter -ManagementOS
   ```

   _**生じ**_ 


   |         Name         | IsManagementOs |        VMName        |  SwitchName  | Mac | 状態 | IPAddresses |
   |----------------------|----------------|----------------------|--------------|------------|--------|-------------|
   | CORP-外部スイッチ |      True      | CORP-外部スイッチ | 001B785768AA |    Ok を    | &nbsp; |             |
   |         管理          |      True      |       VMSTEST        | E41D2D074071 |    Ok を    | &nbsp; |             |
   |         SMB1         |      True      |       VMSTEST        | 00155D30AA00 |    Ok を    | &nbsp; |             |
   |         SMB2         |      True      |       VMSTEST        | 00155D30AA01 |    Ok を    | &nbsp; |             |

   ---

## <a name="step-9-assign-an-ip-address-to-the-smb-host-vnics-vethernet-smb1-and-vethernet-smb2"></a>手順 9. IP アドレスを SMB ホスト vNICs VeSMB2 に割り当てます。このとき、\(SMB1\) と Veand Net \(\)

テスト-40G-1 とテスト-40G-2 物理アダプターでも、101と102のアクセス VLAN が構成されています。 このため、アダプターはトラフィックにタグを付け、ping は成功します。 以前は、2つの pNIC VLAN Id をゼロに構成し、VMSTEST vSwitch を VLAN 101 に設定しました。 その後、vNIC を使用してリモート VLAN 101 アダプターに ping を実行できますが、現在のところ、VLAN 102 のメンバーはありません。



1. 間違った VLAN ID で送信トラフィックの自動タグ付けを行わず、アクセス VLAN ID と一致しない受信トラフィックをフィルターで除外しないように、物理 NIC からアクセス VLAN 設定を削除します。

   ```PowerShell    
   New-NetIPAddress -InterfaceAlias "vEthernet (SMB1)" -IPAddress 192.168.2.111 -PrefixLength 24
   ```

   _**生じ**_  

   ```   
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
   ```

2. リモート VLAN 102 アダプターをテストします。

   ```PowerShell
   Test-NetConnection 192.168.2.5 
   ```

   _**生じ**_  

   ```
   ComputerName   : 192.168.2.5
   RemoteAddress  : 192.168.2.5
   InterfaceAlias : vEthernet (SMB1)
   SourceAddress  : 192.168.2.111
   PingSucceeded  : True
   PingReplyDetails (RTT) : 0 ms
   ```

3. インターフェイス Ve\(SMB2\)の新しい IP アドレスを追加します。

   ```PowerShell
   New-NetIPAddress -InterfaceAlias "vEthernet (SMB2)" -IPAddress 192.168.2.222 -PrefixLength 24 
   ```

   _**生じ**_ 

   ```
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
   ```

4. 接続をもう一度テストします。    


5. RDMA ホスト vNICs を既存の VLAN 102 に配置します。

   ```PowerShell
   Set-VMNetworkAdapterVlan -VMNetworkAdapterName "SMB1" -VlanId "102" -Access -ManagementOS
   Set-VMNetworkAdapterVlan -VMNetworkAdapterName "SMB2" -VlanId "102" -Access -ManagementOS

   Get-VMNetworkAdapterVlan -ManagementOS
   ```

   _**生じ**_ 

   ```   
   VMName VMNetworkAdapterName Mode VlanList
   ------ -------------------- ---- --------
      SMB1 Access   102 
      Mgt  Access   101 
      SMB2 Access   102 
      CORP-External-Switch Untagged
   ```

6. VSwitch セットチーム内の基になる物理 Nic への SMB1 と SMB2 のマッピングを調べます。<p>ホスト vNIC と物理 Nic の関連付けはランダムであり、作成時と破棄時に再調整される可能性があります。 この状況では、間接的なメカニズムを使用して現在の関連付けを確認できます。 SMB1 と SMB2 の MAC アドレスは、NIC チームメンバーのテスト-40G-2 に関連付けられています。 これは、テスト-40G-1 には関連する SMB ホスト vNIC がないため、この方法は理想的ではありません。 SMB ホスト vNIC がマップされるまで、リンク経由で RDMA トラフィックを使用することはできません。

   ```PowerShell    
   Get-NetAdapterVPort (Preferred)

   Get-NetAdapterVmqQueue
   ```

   _**生じ**_ 

   ```
   Name   QueueID MacAddressVlanID Processor VmFriendlyName
   ----   ------- ---------------- --------- --------------
   TEST-40G-1 1   E4-1D-2D-07-40-71 1010:17
   TEST-40G-2 1   00-15-5D-30-AA-00 1020:17
   TEST-40G-2 2   00-15-5D-30-AA-01 1020:17
   ```

7. VM ネットワークアダプターのプロパティを表示します。

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS
   ```

   _**生じ**_ 

   ```
   Name IsManagementOs VMName SwitchName   MacAddress   Status IPAddresses
   ---- -------------- ------ ----------   ----------   ------ -----------
   CORP-External-Switch True  CORP-External-Switch 001B785768AA {Ok}  
   Mgt  True  VMSTEST  E41D2D074071 {Ok}  
   SMB1 True  VMSTEST  00155D30AA00 {Ok}  
   SMB2 True  VMSTEST  00155D30AA01 {Ok}  
   ```

8. ネットワークアダプターチームマッピングを表示します。<p>マッピングをまだ実行していないため、結果は情報を返しません。

   ```PowerShell
   Get-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName SMB1
   Get-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName SMB2
   ```


9. SMB1 と SMB2 を別々の物理 NIC チームメンバーにマップし、アクションの結果を表示します。

   >[!IMPORTANT]
   >続行する前にこの手順を完了していることを確認してください。使用しない場合は、実装に失敗します。

   ```PowerShell
   Set-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName "SMB1" -PhysicalNetAdapterName "Test-40G-1"
   Set-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName "SMB2" -PhysicalNetAdapterName "Test-40G-2"

   Get-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST
   ```

   _**生じ**_ 

   ```   
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
   ```

10. 以前に作成した MAC アソシエーションを確認します。

    ```PowerShell    
    Get-NetAdapterVmqQueue
    ```

    _**生じ**_ 

    ```   
    Name   QueueID MacAddressVlanID Processor VmFriendlyName
    ----   ------- ---------------- --------- --------------
    TEST-40G-1 1   E4-1D-2D-07-40-71 1010:17
    TEST-40G-1 2   00-15-5D-30-AA-00 1020:17
    TEST-40G-2 1   00-15-5D-30-AA-01 1020:17
    ```


11. 両方のホスト vNICs が同じサブネット上に存在し、同じ VLAN ID \(102\)であるため、リモートシステムからの接続をテストします。

    ```PowerShell 
    Test-NetConnection 192.168.2.111
    ```

    _**生じ**_   

    ```
    ComputerName   : 192.168.2.111
    RemoteAddress  : 192.168.2.111
    InterfaceAlias : Test-40G-2
    SourceAddress  : 192.168.2.5
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms
    ```

    ```PowerShell   
    Test-NetConnection 192.168.2.222
    ```

    _**生じ**_   

    ```
    ComputerName   : 192.168.2.222
    RemoteAddress  : 192.168.2.222
    InterfaceAlias : Test-40G-2
    SourceAddress  : 192.168.2.5
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms 
    ```
12. 名前、スイッチ名、および優先度タグを設定します。   

    ```PowerShell
    Set-VMNetworkAdapter -ManagementOS -Name "SMB1" -IeeePriorityTag on
    Set-VMNetworkAdapter -ManagementOS -Name "SMB2" -IeeePriorityTag on
    Get-VMNetworkAdapter -ManagementOS -Name "SMB*" | fl Name,SwitchName,IeeePriorityTag,Status
    ```

    _**生じ**_   

    ```
    Name: SMB1
    SwitchName  : VMSTEST
    IeeePriorityTag : On 
    Status  : {Ok}

    Name: SMB2
    SwitchName  : VMSTEST
    IeeePriorityTag : On
    Status  : {Ok}
    ```

13. Venetwork ネットワークアダプターのプロパティを表示します。

    ```PowerShell
    Get-NetAdapterRdma -Name "vEthernet*" | sort Name | ft -AutoSize
    ```

    _**生じ**_   

    ```
    Name  InterfaceDescription Enabled
    ----  -------------------- -------
    vEthernet (SMB2)  Hyper-V Virtual Ethernet Adapter #4  False  
    vEthernet (SMB1)  Hyper-V Virtual Ethernet Adapter #3  False  
    vEthernet (MGT)   Hyper-V Virtual Ethernet Adapter #2  False   
    ```

14. Venetwork アダプターを有効にします。  

    ```PowerShell
    Enable-NetAdapterRdma -Name "vEthernet (SMB1)"
    Enable-NetAdapterRdma -Name "vEthernet (SMB2)"
    Get-NetAdapterRdma -Name "vEthernet*" | sort Name | fl *
    ```

    _**生じ**_   

    ```
    Name  InterfaceDescription Enabled
    ----  -------------------- -------
    vEthernet (SMB2)  Hyper-V Virtual Ethernet Adapter #4  True   
    vEthernet (SMB1)  Hyper-V Virtual Ethernet Adapter #3  True  
    vEthernet (MGT)   Hyper-V Virtual Ethernet Adapter #2  False
    ```

## <a name="step-10-validate-the-rdma-functionality"></a>手順 10. RDMA 機能を検証します。

Vswitch セットチームの両方のメンバーに対して、リモートシステムから vSwitch を持つローカルシステムへの RDMA 機能を検証します。<p>\(SMB1 と SMB2\) の両方のホスト vNICs が VLAN 102 に割り当てられているため、リモートシステムで VLAN 102 アダプターを選択できます。 <p>この例では、NIC テスト-40G-2 は RDMA から SMB1 (192.168.2.111) および SMB2 (192.168.2.222) になります。

>[!TIP]
>このシステムでは、ファイアウォールを無効にすることが必要になる場合があります。  詳細については、ファブリックポリシーを参照してください。
>
>```PowerShell
>Set-NetFirewallProfile -All -Enabled False
>    
>Get-NetAdapterAdvancedProperty -Name "Test-40G-2"
>```
>
>_**生じ**_ 
>   
>```
>Name  DisplayNameDisplayValue   RegistryKeyword RegistryValue  
>----  -----------------------   --------------- -------------  
> .
> .
>Test-40G-2VLAN ID102VlanID  {102} 
>```

1. ネットワークアダプターのプロパティを表示します。

   ```PowerShell
   Get-NetAdapter
   ```

   _**生じ**_ 

   ```
   Name  InterfaceDescriptionifIndex Status   MacAddress LinkSpeed
   ----  --------------------------- ------   ---------- ---------
   Test-40G-2Mellanox ConnectX-3 Pro Ethernet A...#3   3 Up   E4-1D-2D-07-43-D140 Gbps
   ```

2. ネットワークアダプターの RDMA 情報を表示します。

   ```PowerShell
   Get-NetAdapterRdma
   ```

   _**生じ**_  

   ```
   Name  InterfaceDescription Enabled
   ----  -------------------- -------
   Test-40G-2Mellanox ConnectX-3 Pro Ethernet Adap... True   
   ```

3. 最初の物理アダプターで RDMA トラフィックテストを実行します。

   ```PowerShell 
   C:\TEST\Test-RDMA.PS1 -IfIndex 3 -IsRoCE $true -RemoteIpAddress 192.168.2.111 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```

   _**生じ**_ 

   ```
   VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\diskspd.exe
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
   ```

4. 2番目の物理アダプターで RDMA トラフィックテストを実行します。

   ```PowerShell
   C:\TEST\Test-RDMA.PS1 -IfIndex 3 -IsRoCE $true -RemoteIpAddress 192.168.2.222 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```

   _**生じ**_ 

   ```
   VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\diskspd.exe
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
   ```

5. ローカルからリモートコンピューターへの RDMA トラフィックをテストします。

    ```PowerShell
    Get-NetAdapter | ft –AutoSize
    ```

    _**生じ**_ 

    ```
    Name  InterfaceDescriptionifIndex Status   MacAddress LinkSpeed
    ----  --------------------------- ------   ---------- ---------
    vEthernet (SMB2)  Hyper-V Virtual Ethernet Adapter #4  45 Up   00-15-5D-30-AA-0380 Gbps
    vEthernet (SMB1)  Hyper-V Virtual Ethernet Adapter #3  41 Up   00-15-5D-30-AA-0280 Gbps
    ```

6. 最初の仮想アダプターで RDMA トラフィックテストを実行します。    

   ```
   C:\TEST\Test-RDMA.PS1 -IfIndex 41 -IsRoCE $true -RemoteIpAddress 192.168.2.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```

   _**生じ**_ 

   ```
   VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\diskspd.exe
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
   ```

7. 2番目の仮想アダプターで RDMA トラフィックテストを実行します。

   ```PowerShell
   C:\TEST\Test-RDMA.PS1 -IfIndex 45 -IsRoCE $true -RemoteIpAddress 192.168.2.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```

   _**生じ**_ 

   ```
   VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\diskspd.exe
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
   ```

この出力の最後の行である "RDMA トラフィックテストが成功しました: RDMA トラフィックは192.168.2.5 に送信されました" と表示されます。これは、アダプターに収束 NIC を正常に構成したことを示しています。

## <a name="related-topics"></a>関連トピック 

- [単一のネットワークアダプターを使用した収束 NIC 構成](cnic-single.md)
- [収束 NIC の物理スイッチ構成](cnic-app-switch-config.md)
- [収束 NIC 構成のトラブルシューティング](cnic-app-troubleshoot.md)
