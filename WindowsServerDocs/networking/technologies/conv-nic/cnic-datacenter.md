---
title: 収束の NIC チーミングされた NIC 構成では (データ センター)
description: このトピックで提供していますコンバージド NIC をチーミングされた NIC 構成でスイッチ埋め込みチーミング (SET) でデプロイする手順。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: f01546f8-c495-4055-8492-8806eee99862
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/17/2018
ms.openlocfilehash: 5f99600e24c62da9bdf674897dbadde9246b7bb7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59821033"
---
# <a name="converged-nic-in-a-teamed-nic-configuration-datacenter"></a>収束の NIC チーミングされた NIC 構成では (データ センター)

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックで提供していますスイッチ埋め込みチーミング NIC のチーミングの構成で収束の NIC をデプロイする手順\(設定\)します。 

このトピックの例の構成には、2 つの HYPER-V ホストがについて説明します**HYPER-V Host 1**と**HYPER-V Host 2**します。 両方のホストには、2 つのネットワーク アダプターがあります。 各ホストでは、1 つのアダプターが、192.168.1.x/24 サブネットに接続されているし、192.168.2.x/24 サブネットに 1 つのアダプターが接続されています。

![Hyper-V ホスト](../../media/Converged-NIC/1-datacenter-test-conn.jpg)

## <a name="step-1-test-the-connectivity-between-source-and-destination"></a>手順 1. ソースとターゲットの間の接続をテストします。

物理 NIC に接続できること、移行先ホストを確認します。  このテストでは、レイヤー 3 を使用して接続を示します\(L3\) - または - IP 層だけでなく、レイヤー 2 \(L2\)仮想ローカル エリア ネットワーク\(VLAN\)します。

1. 最初のネットワーク アダプターのプロパティを表示します。

   ```PowerShell
   Get-NetAdapter -Name "Test-40G-1" | ft -AutoSize
   ```
  
   _**結果:**_

   |名前|InterfaceDescription|ifIndex|状況|Mac アドレス|%Linkspeed|
   |-----|--------------------|-------|-----|----------|---------|
   |テスト-40 G-1|Mellanox connectx-3 Pro イーサネット アダプター|11|Up|E4-1D-2D-07-43-D0|40 Gbps|
   ---
   
2. 最初のアダプターで IP アドレスなどの追加のプロパティを表示します。 

   ```PowerShell
   Get-NetIPAddress -InterfaceAlias "Test-40G-1"
   Get-NetIPAddress -InterfaceAlias "TEST-40G-1" | Where-Object {$_.AddressFamily -eq "IPv4"} | fl InterfaceAlias,IPAddress
   ```
   
   _**結果:**_

   |パラメーター|値|
   |---------|-----|
   |IPAddress| 192.168.1.3|
   |InterfaceIndex|11|
   |InterfaceAlias|テスト-40 G-1|
   |AddressFamily|IPv4|
   |種類| ユニキャスト|
   |PrefixLength|24|
   ---

3. 2 番目のネットワーク アダプターのプロパティを表示します。

   ```PowerShell
   Get-NetAdapter -Name "Test-40G-2" | ft -AutoSize
   ```
   
   _**結果:**_

   |名前 |InterfaceDescription |ifIndex |状況 |Mac アドレス |%Linkspeed|
   |----|--------------------|-------|------|----------|---------|
   |TEST-40G-2 |Mellanox connectx-3 Pro イーサネット ファブリック 2 |13 |Up |E4-1D-2D-07-40-70 |40 Gbps|
   ---
   
4. IP アドレスを含む、2 つ目のアダプターの追加のプロパティを表示します。

   ```PowerShell
   Get-NetIPAddress -InterfaceAlias "Test-40G-2"
   Get-NetIPAddress -InterfaceAlias "Test-40G-2" | Where-Object {$_.AddressFamily -eq "IPv4"} | fl InterfaceAlias,IPAddress
   ```
   
   _**結果:**_

   |パラメーター|Value|
   |---------|-----|
   |IPAddress|192.168.2.3|
   |InterfaceIndex|13|
   |InterfaceAlias|TEST-40G-2|
   |AddressFamily|IPv4|
   |種類|ユニキャスト|
   |PrefixLength|24|
   ---

5. その他の NIC チームまたはセット メンバー pNICs が有効な IP アドレスを確認します。<p>別のサブネットを使用して、\(です。 **。2**.xxx vs です。 **。1**.xxx\)先にこのアダプターから送信を容易にします。 それ以外の場合、両方 pNICs 同じサブネット上で特定する場合、インターフェイス間での Windows の TCP/IP スタックの負荷を分散し、単純な検証が複雑になります。


## <a name="step-2-ensure-that-source-and-destination-can-communicate"></a>手順 2.  ソースと変換先が通信できることを確認します。

この手順で使用して、 **Test-netconnection**場合を使用できますが、Windows PowerShell コマンド、 **ping**場合コマンドします。 

1. 双方向通信を確認します。

   ```PowerShell
   Test-NetConnection 192.168.1.5
   ```
   
   _**結果:**_

   |パラメーター|Value|
   |---------|-----|
   |ComputerName|192.168.1.5|
   |リモート アドレス|192.168.1.5|
   |InterfaceAlias|テスト-40 G-1|
   |発信元アドレス|192.168.1.3|
   |PingSucceeded|False|
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
   
   
4. さらに Nic の接続を確認します。 チーム NIC またはセットに含まれるすべての後続 pNICs の前の手順を繰り返します。

   ```PowerShell    
   Test-NetConnection 192.168.2.5
   ```
   
   _**結果:**_

   |パラメーター|値|
   |---------|-----|
   |ComputerName|192.168.2.5|
   |リモート アドレス|192.168.2.5|
   |InterfaceAlias|テスト-40 G-2|
   |発信元アドレス|192.168.2.3|
   |PingSucceeded|False|
   |PingReplyDetails \(RTT\)|0 ミリ秒|
   ---

## <a name="step-3-configure-the-vlan-ids-for-nics-installed-in-your-hyper-v-hosts"></a>手順 3. VLAN Id を HYPER-V ホストにインストールされている Nic の構成します。

多くのネットワーク構成の Vlan を使用することし、ネットワークの Vlan を使用しようとしている場合は、Vlan の構成で、前のテストを繰り返す必要があります。

この手順では、Nic が内**アクセス**モード。 ただし、HYPER-V 仮想スイッチを作成する\(vSwitch\) vSwitch ポート レベルで、このガイドの後半で VLAN プロパティが適用されます。 

スイッチは、複数の Vlan をホストできる、ので、ラック上の必要は\(ToR\)物理スイッチ ポート トランク モードで構成するホストが接続されていること。

>[!NOTE]
>トランク モード スイッチを構成する方法の詳細については、ToR スイッチのドキュメントを参照してください。

次の図は、各を VLAN 101 とネットワーク アダプターのプロパティで構成されている VLAN 102 を持つ 2 つのネットワーク アダプターの 2 つの HYPER-V ホストを示しています。

![仮想ローカル エリア ネットワークを構成します。](../../media/Converged-NIC/2-datacenter-configure-vlans.jpg)


>[!TIP]
>Institute の Electrical and Electronics Engineers に従って\(IEEE\)ネットワーク標準は、サービスの品質\(QoS\)埋め込まれている、802.1 p ヘッダーに基づいて、物理 NIC でのプロパティ802.1 q \(VLAN\) VLAN ID を構成するときにヘッダー

1. 最初の NIC のテスト-40 G-1 では、VLAN ID を構成します。

   ```PowerShell    
   Set-NetAdapterAdvancedProperty -Name "Test-40G-1" -RegistryKeyword VlanID -RegistryValue "101"
   Get-NetAdapterAdvancedProperty -Name "Test-40G-1" | Where-Object {$_.RegistryKeyword -eq "VlanID"} | ft -AutoSize
   ```

   _**結果:**_   

   |名前 |DisplayName| 値| RegistryKeyword |RegistryValue|
   |----|-----------|------------|---------------|-------------|
   |テスト-40 G-1|VLAN ID|101|VlanID|{101}|
   ---

2. VLAN ID を適用するネットワーク アダプターを再起動します。

   ```PowerShell
   Restart-NetAdapter -Name "Test-40G-1"
   ```
   
3. 状態が確認**を**します。

   ```PowerShell
   Get-NetAdapter -Name "Test-40G-1" | ft -AutoSize
   ```
   
   _**結果:**_

   |名前|InterfaceDescription|ifIndex| 状況|Mac アドレス|%Linkspeed|
   |----|--------------------|-------|------|----------| ---------|
   |テスト-40 G-1|Mellanox connectx-3 Pro イーサネット Ada.|11|Up|E4-1D-2D-07-43-D0|40 Gbps|
   ---
    
4. テスト-40 G 2、2 番目の NIC で VLAN ID を構成します。

   ```PowerShell    
   Set-NetAdapterAdvancedProperty -Name "Test-40G-2" -RegistryKeyword VlanID -RegistryValue "102"
   Get-NetAdapterAdvancedProperty -Name "Test-40G-2" | Where-Object {$_.RegistryKeyword -eq "VlanID"} | ft -AutoSize
   ``` 

   _**結果:**_

   |名前 |DisplayName| 値| RegistryKeyword |RegistryValue|
   |----|-----------|------------|---------------|-------------|
   |TEST-40G-2|VLAN ID|102|VlanID|{102}|
   ---
   
5. VLAN ID を適用するネットワーク アダプターを再起動します。

   ```PowerShell
   Restart-NetAdapter -Name "Test-40G-2" 
   ```
   
6. 状態が確認**を**します。

   ```PowerShell
   Get-NetAdapter -Name "Test-40G-1" | ft -AutoSize
   ```
   
   _**結果:**_

   |名前|InterfaceDescription|ifIndex| 状況|Mac アドレス|%Linkspeed|
   |----|--------------------|-------|------|----------| ---------|
   |テスト-40 G-2 |Mellanox connectx-3 Pro イーサネット Ada. |11 |Up |E4-1D-2D-07-43-D1 |40 Gbps|
   ---

   >[!IMPORTANT]
   >再起動し、ネットワーク上で利用可能になるデバイスに数秒かかる場合があります。 
   
7. 最初の NIC のテスト-40 G-1 の接続を確認します。<p>接続に失敗した場合は、スイッチ、同じ VLAN の VLAN の構成または変換先への参加を調べます。 

   ```PowerShell
   Test-NetConnection 192.168.1.5
   ```

   _**結果:**_   

   |パラメーター|Value|
   |---------|-----|
   |ComputerName|192.168.1.5|
   |リモート アドレス|192.168.1.5|
   |InterfaceAlias|テスト-40 G-1|
   |発信元アドレス|192.168.1.5|
   |PingSucceeded|True|
   |PingReplyDetails \(RTT\)|0 ミリ秒|
   ---
   
8. 最初の NIC のテスト-40 G-2 の接続を確認します。<p>接続に失敗した場合は、スイッチ、同じ VLAN の VLAN の構成または変換先への参加を調べます。

   ```PowerShell    
   Test-NetConnection 192.168.2.5
   ```

   _**結果:**_    

   |パラメーター|値|
   |---------|-----|
   |ComputerName|192.168.2.5|
   |リモート アドレス|192.168.2.5|
   |InterfaceAlias|テスト-40 G-2|
   |発信元アドレス|192.168.2.3|
   |PingSucceeded|True|
   |PingReplyDetails \(RTT\)|0 ミリ秒|
   ---
   
   >[!IMPORTANT]
   >珍しくありません、 **Test-netconnection**またはを実行した後すぐに発生する ping 失敗**再起動 NetAdapter**します。  ネットワーク アダプターを完全に初期化するまで待機してからやり直してください。
   >
   >VLAN 101 接続するには、VLAN 102 接続がない場合は、問題場合、スイッチが、必要な VLAN のポートのトラフィックを許可するように構成する必要があることがあります。 この一時的に障害が発生したアダプターに VLAN 101、設定と接続のテストを繰り返しで確認できます。

   
   次の図では、Vlan を正常に構成した後、HYPER-V ホストを示します。

   ![サービスの品質を構成します。](../../media/Converged-NIC/3-datacenter-configure-qos.jpg)
   
   
## <a name="step-4-configure-quality-of-service-qos"></a>手順 4. 構成サービスの品質\(QoS\)

>[!NOTE]
>互いに通信するためのものがすべてのホストでは、DCB と QoS の構成手順を次のすべてを実行する必要があります。

1. データ センター ブリッジング インストール\(DCB\)各 HYPER-V ホストでします。

   - **省略可能な**iWarp を使用しているネットワーク構成。
   - **必要な**RoCE を使用しているネットワーク構成\(任意のバージョン\)RDMA サービス。

   ```PowerShell
   Install-WindowsFeature Data-Center-Bridging
   ```

   _**結果:**_

   |成功 |再起動が必要です。 |終了コード|機能の結果|
   |------- |-------------- |--------- |-------------- |
   |True |X |成功| {0} のデータ センター ブリッジング}|
   ---
   
2. SMB ダイレクトの QoS ポリシーを設定します。

   - **省略可能な**iWarp を使用しているネットワーク構成。
   - **必要な**RoCE を使用しているネットワーク構成\(任意のバージョン\)RDMA サービス。
   
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
   |NetDirectPort|445
   |PriorityValue|3
   ---

3. インターフェイスでは、その他のトラフィックの QoS ポリシーの追加を設定します。   

   ```PowerShell
   New-NetQosPolicy "DEFAULT" -Default -PriorityValue8021Action 0
   ```

   _**結果:**_   

   |パラメーター|Value|
   |---------|-----|
   |名前 | DEFAULT|
   |所有者|グループ ポリシー\(マシン\)|
   |NetworkProfile|すべての|
   |優先度|127|
   |テンプレート| Default|
   |JobObject| &nbsp;|
   |PriorityValue|0|
   ---
   
4. オンにする**優先度のフロー制御**SMB トラフィックは、これは必要ありません iWarp の場合。

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
   |3 |True |グローバル|&nbsp;|&nbsp;|
   |4 |False |グローバル|&nbsp;|&nbsp;|
   |5 |False |グローバル|&nbsp;|&nbsp;|
   |6 |False |グローバル|&nbsp;|&nbsp;|
   |7 |False |グローバル|&nbsp;|&nbsp;|
   ---
   
   >**重要な**、結果では、これらの結果が一致しない 3 以外のアイテムが有効値は True、無効にした**FlowControl**これらのクラス。
   >
   >```PowerShell
   >Disable-NetQosFlowControl -priority 0,1,2,4,5,6,7
   >Get-NetQosFlowControl
   >```
   >複雑な構成は、他のトラフィック クラスはこれらのシナリオは、このガイドの範囲外ですがフローの制御を必要があります。


5. 最初の NIC のテスト-40 G-1 の QoS を有効にします。

   ```PowerShell
   Enable-NetAdapterQos -InterfaceAlias "Test-40G-1"
   Get-NetAdapterQos -Name "Test-40G-1"

   Name: TEST-40G-1 
   Enabled: True
   ```
   _**機能**:_   

   |パラメーター|ハードウェア|現在の|
   |---------|--------|-------|
   |MacSecBypass|NotSupported|NotSupported|
   |DcbxSupport|なし|なし|
   |NumTCs(Max/ETS/PFC)|8/8/8|8/8/8|
   ---
 
   _**OperationalTrafficClasses**:_    

   |TC|TSA|帯域幅|優先順位|
   |----|-----|--------|-------|
   |0| 厳密|&nbsp;|0-7|
   ---

   _**OperationalFlowControl**:_  

   優先順位 3 が有効になっています。  

   _**OperationalClassifications**:_  

   |プロトコル|ポートの種類/|Priority|
   |--------|---------|--------|
   |Default|&nbsp;|0|
   |NetDirect| 445|3|
   ---
   
6. 2 つ目の NIC のテスト-40 G-2 の QoS を有効にします。

   ```PowerShell
   Enable-NetAdapterQos -InterfaceAlias "Test-40G-2"
   Get-NetAdapterQos -Name "Test-40G-2"

   Name: TEST-40G-2 
   Enabled: True 
   ```

   _**機能**:_ 

   |パラメーター|ハードウェア|現在の|
   |---------|--------|-------|
   |MacSecBypass|NotSupported|NotSupported|
   |DcbxSupport|なし|なし|
   |NumTCs(Max/ETS/PFC)|8/8/8|8/8/8|
   ---

   _**OperationalTrafficClasses**:_  

   |TC|TSA|帯域幅|優先順位|
   |----|-----|--------|-------|
   |0| 厳密|&nbsp;|0-7|
   ---
   
    _**OperationalFlowControl**:_  

    優先順位 3 が有効になっています。  
   
   _**OperationalClassifications**:_  

   |プロトコル|ポートの種類/|Priority|
   |--------|---------|--------|
   |Default|&nbsp;|0|
   |NetDirect| 445|3|
   ---

   
7. SMB ダイレクトを半分の帯域幅が予約\(RDMA\)

   ```PowerShell
   New-NetQosTrafficClass "SMB" -priority 3 -bandwidthpercentage 50 -algorithm ETS
   ```
   
   _**結果:**_  
   
   |名前|アルゴリズム |Bandwidth(%)| Priority |PolicySet |IfIndex |ifAlias |
   |----|---------| ------------ |--------| ---------|------- |------- |
   |SMB | ETS     | 50 |3 |グローバル |&nbsp;|&nbsp;|   
   ---

8. 帯域幅予約の設定を表示するには。   

   ```PowerShell
   Get-NetQosTrafficClass | ft -AutoSize
   ```
   
   _**結果:**_  

   |名前|アルゴリズム |Bandwidth(%)| Priority |PolicySet |IfIndex |ifAlias |
   |----|---------| ------------ |--------| ---------|------- |------- |
   |[Default]| ETS|50 |0-2,4-7|  グローバル|&nbsp;|&nbsp;| 
   |SMB |ETS|50 |3 |グローバル|&nbsp;|&nbsp;| 
   ---
   
9. (省略可能)テナントの IP トラフィックの 2 つの余分なトラフィック クラスを作成します。 

   >[!TIP]
   >"IP1"と"IP2"の値を省略することができます。

   ```PowerShell
   New-NetQosTrafficClass "IP1" -Priority 1 -bandwidthpercentage 10 -algorithm ETS
   ```
   
   _**結果:**_
   
   |名前|アルゴリズム |Bandwidth(%)| Priority |PolicySet |IfIndex |ifAlias |
   |----|---------| ------------ |--------| ---------|------- |------- |
   |IP1 |ETS |10 |1 |グローバル|&nbsp;|&nbsp;|
   ---
   
   ```PowerShell
   New-NetQosTrafficClass "IP2" -Priority 2 -bandwidthpercentage 10 -algorithm ETS
   ```
   
   _**結果:**_

   |名前|アルゴリズム |Bandwidth(%)| Priority |PolicySet |IfIndex |ifAlias |
   |----|---------| ------------ |--------| ---------|------- |------- |
   |IP2 |ETS |10 |2 |グローバル|&nbsp;|&nbsp;|
   ---
   
10. QoS のトラフィック クラスを表示します。

    ```PowerShell
    Get-NetQosTrafficClass | ft -AutoSize
    ```
    
    _**結果:**_

    |名前|アルゴリズム |Bandwidth(%)| Priority |PolicySet |IfIndex |ifAlias |
    |----|---------| ------------ |--------| ---------|------- |------- |
    |[Default] |ETS |30 |0,4-7 |グローバル|&nbsp;|&nbsp;|
    |SMB |ETS |50 |3 |グローバル|&nbsp;|&nbsp;|
    |IP1 |ETS |10 |1 |グローバル|&nbsp;|&nbsp;|
    |IP2 |ETS |10 |2 |グローバル|&nbsp;|&nbsp;|
    ---
   
11. (省略可能)デバッガーをオーバーライドします。<p>既定では、アタッチされたデバッガーは NetQos をブロックします。 

    ```PowerShell
    Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 –Force
    Get-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" | ft AllowFlowControlUnderDebugger
    ```

    _**結果:**_  

    ```
    AllowFlowControlUnderDebugger
    -----------------------------
    1
    ```

## <a name="step-5-verify-the-rdma-configuration-mode-1"></a>手順 5. RDMA 構成を確認する\(モード 1\) 

VSwitch を作成して、RDMA に移行する前に、ファブリックが正しく構成されていることを確認する\(モード 2\)します。

次の図は、HYPER-V ホストの現在の状態を示します。

![RDMA のテスト](../../media/Converged-NIC/4-datacenter-test-rdma.jpg)


1. RDMA 構成を確認します。

   ```PowerShell
   Get-NetAdapterRdma | ft -AutoSize
   ```
   
   _**結果:**_

   |名前 |InterfaceDescription |有効|
   |----|--------------------|-------|
   |テスト-40 G-1| Mellanox ConnectX 4 VPI アダプター #2 |True|
   |TEST-40G-2| Mellanox ConnectX 4 VPI アダプター |True|
   ---

2. 確認、 **ifIndex**ターゲットのアダプターの値。<p>ダウンロードしたスクリプトを実行するときに、以降の手順でこの値を使用します。   

   ```PowerShell
   Get-NetIPConfiguration -InterfaceAlias "TEST*" | ft InterfaceAlias,InterfaceIndex,IPv4Address
   ```
   
   _**結果:**_

   |InterfaceAlias |InterfaceIndex |IPv4Address|
   |-------------- |-------------- |-----------|
   |テスト-40 G-1 |14 |{192.168.1.3}|
   |TEST-40G-2 | 13 |{192.168.2.3}|
   ---
   
3. ダウンロード、 [DiskSpd.exe ユーティリティ](https://aka.ms/diskspd)C:\TEST に抽出\.

4. ダウンロード、[テスト RDMA の PowerShell スクリプト](https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1)C:\TEST など、ローカル ドライブ上のテスト フォルダーを\.

5. 実行、**テスト Rdma.ps1** ifIndex 値を同じ vlan の最初のリモート アダプターの IP アドレスと共に、スクリプトに渡す、PowerShell スクリプト。<p>この例では、スクリプトを渡します、 **ifIndex**リモート ネットワーク アダプターの IP アドレス 192.168.1.5 で 14 文字の値。
   
   ```PowerShell
   C:\TEST\Test-RDMA.PS1 -IfIndex 14 -IsRoCE $true -RemoteIpAddress 192.168.1.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```

   _**結果:**_ 
   
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
   >RDMA のトラフィックが失敗した場合、RoCE ケースを具体的には、ホストの設定に一致する必要があります PFC/ETS の適切な設定を ToR スイッチの構成を参照してください。 参照値は、このドキュメントで QoS セクションを参照してください。

6. 実行、**テスト Rdma.ps1** ifIndex 値を同じ vlan の 2 つ目のリモート アダプターの IP アドレスと共に、スクリプトに渡す、PowerShell スクリプト。<p>この例では、スクリプトを渡します、 **ifIndex**リモート ネットワーク アダプターの IP アドレス 192.168.2.5 で 13 の値。

   ```PowerShell
   C:\TEST\Test-RDMA.PS1 -IfIndex 13 -IsRoCE $true -RemoteIpAddress 192.168.2.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```

   _**結果:**_ 
   
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

## <a name="step-6-create-a-hyper-v-vswitch-on-your-hyper-v-hosts"></a>手順 6. HYPER-V ホスト上の HYPER-V vSwitch を作成します。


次の図では、vSwitch で HYPER-V ホスト 1 を示します。

![HYPER-V 仮想スイッチを作成します。](../../media/Converged-NIC/5-datacenter-create-vswitch.jpg)

1. HYPER-V ホスト 1 上のモードの設定で、vSwitch を作成します。

   ```PowerShell
   New-VMSwitch –Name "VMSTEST" –NetAdapterName "TEST-40G-1","TEST-40G-2" -EnableEmbeddedTeaming $true -AllowManagementOS $true
   ```
   
   _**結果:**_

   |名前 |SwitchType |NetAdapterInterfaceDescription|
   |---- |---------- |------------------------------|
   |VMSTEST |外部リンク |チーム化されたインターフェイス|
   ---
   
2. セット内の物理アダプターのチームを表示します。

   ```PowerShell
   Get-VMSwitchTeam -Name "VMSTEST" | fl
   ```
   
   _**結果:**_  
   
   ```
   Name: VMSTEST  
   Id: ad9bb542-dda2-4450-a00e-f96d44bdfbec  
   NetAdapterInterfaceDescription: {Mellanox ConnectX-3 Pro Ethernet Adapter, Mellanox ConnectX-3 Pro Ethernet Adapter #2}  
   TeamingMode: SwitchIndependent  
   LoadBalancingAlgorithm: Dynamic   
   ```
   
3. ホスト vNIC の 2 つのビューを表示します。

   ```PowerShell
    Get-NetAdapter
   ```
   
   _**結果:**_

   |名前 |InterfaceDescription |ifIndex |状況 |Mac アドレス |%Linkspeed|
   |---- |--------------------|-------|------|----------|---------|
   |vEthernet (VMSTEST)|HYPER-V 仮想イーサネット アダプター #2 |28 |Up|E4-1D-2D-07-40-71|80 Gbps|
   ---
   
4. ホスト vNIC の追加のプロパティを表示します。 

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS
   ```
   
   _**結果:**_

   |名前 |IsManagementOs |VMName |SwitchName |Mac アドレス |状況 |Ip アドレス|
   |----|--------------|------|----------|----------|------|-----------|
   |VMSTEST|True |VMSTEST |E41D2D074071| {0} [ok]}|&nbsp;|
   ---
   

5. リモートの VLAN 101 アダプターへのネットワーク接続をテストします。

   ```PowerShell
   Test-NetConnection 192.168.1.5 
   ```
   
   _**結果:**_  
   
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

この手順で物理 NIC からと vSwitch を使用して VLANID を設定するアクセス VLAN 設定を削除します。

両方の自動タグ付けが正しくない VLAN ID を持つエグレス トラフィックを防ぐために、アクセス VLAN 設定を削除し、アクセス VLAN ID と一致しません、トラフィックの受信をフィルター処理から必要があります。

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
   
   _**結果:**_  
   
   ```
   VMName VMNetworkAdapterName Mode   VlanList
   ------ -------------------- ----   --------
          VMSTEST              Access 101     
   ```
   
   
3. ネットワーク接続をテストします。

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

   >**重要な**場合は、結果が結果の例に類似していないと、ping は失敗し、メッセージ"警告。192.168.1.5 への Ping に失敗しました - 状態。DestinationHostUnreachable、""vEthernet (VMSTEST)"に適切な IP アドレスがいることを確認します。
   >
   >```PowerShell
   >Get-NetIPAddress -InterfaceAlias "vEthernet (VMSTEST)"
   >```
   >
   >IP アドレスが設定されていない場合は、問題を修正します。
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
   

4. 管理用の NIC の名前を変更します。

   ```PowerShell
   Rename-VMNetworkAdapter -ManagementOS -Name “VMSTEST” -NewName “MGT”
   Get-VMNetworkAdapter -ManagementOS
   ```
   
   _**結果:**_ 
   
   |名前 |IsManagementOs |VMName |SwitchName |Mac アドレス |状況 |Ip アドレス
   |----|--------------|------|----------|----------|------|-----------|
   |CORP の外部スイッチ |True |&nbsp;|CORP の外部スイッチ |001B785768AA |{0} [ok]}|&nbsp;|
   |管理 |True |&nbsp;|VMSTEST |E41D2D074071 |{0} [ok]}|&nbsp;|
   ---
   
5. NIC の追加のプロパティを表示します。

   ```PowerShell
   Get-NetAdapter
   ```
   
   _**結果:**_

   |名前 |InterfaceDescription |ifIndex |状況 |Mac アドレス |%Linkspeed|
   |----|--------------------|------|----------|---------|------|
   |vEthernet (管理) |HYPER-V 仮想イーサネット アダプター #2 |28 |Up | E4-1D-2D-07-40-71 |80 Gbps|
   ---
   
## <a name="step-8-test-hyper-v-vswitch-rdma"></a>手順 8 です。 HYPER-V vSwitch RDMA をテストします。

次の図は、HYPER-V ホスト 1 vSwitch を含む、HYPER-V ホストの現在の状態を示します。

![HYPER-V 仮想スイッチをテストします。](../../media/Converged-NIC/6-datacenter-test-vswitch-rdma.jpg)

1. 以前の VLAN 設定を補完するホスト vNIC のタグ付け、優先順位を設定します。

   ```PowerShell    
   Set-VMNetworkAdapter -ManagementOS -Name "MGT" -IeeePriorityTag on
   Get-VMNetworkAdapter -ManagementOS -Name "MGT" | fl Name,IeeePriorityTag
   ```
   
   _**結果:**_  
      
   名:管理  
   IeeePriorityTag:オン  
    
2. RDMA の 2 つのホスト Vnic を作成し、vSwitch VMSTEST に接続します。

   ```PowerShell    
   Add-VMNetworkAdapter –SwitchName "VMSTEST" –Name SMB1 –ManagementOS
   Add-VMNetworkAdapter –SwitchName "VMSTEST" –Name SMB2 –ManagementOS
   ```
   
3. 管理 NIC のプロパティを表示します。

   ```PowerShell    
   Get-VMNetworkAdapter -ManagementOS
   ```
   
   _**結果:**_ 

   |名前 |IsManagementOs |VMName |SwitchName |Mac アドレス |状況 |Ip アドレス|
   |----|--------------|------|----------|----------|------|-----------|
   |CORP の外部スイッチ |True |CORP の外部スイッチ |001B785768AA|{0} [ok]} |&nbsp;| 
   |管理 |True |VMSTEST |E41D2D074071 |{0} [ok]} |&nbsp;|
   |SMB1 |True |VMSTEST |00155D30AA00 |{0} [ok]} |&nbsp;|
   |SMB2 |True |VMSTEST |00155D30AA01 |{0} [ok]} |&nbsp;|
   ---
   
## <a name="step-9-assign-an-ip-address-to-the-smb-host-vnics-vethernet-smb1-and-vethernet-smb2"></a>手順 9: SMB ホスト Vnic の vEthernet に IP アドレスを割り当てる\(SMB1\)と vEthernet \(SMB2\)

テスト-40 G-1 と 2-テスト-40 G の物理アダプターは、アクセス VLAN 101 と 102 が構成されているがあります。 このため、アダプターは、タグのトラフィックと ping が成功するとします。 以前は、両方の pNIC VLAN Id を 0 に設定し、VLAN 101 に VMSTEST vSwitch を設定します。 その後、まだは管理の vNIC を使用して、リモートの VLAN 101 アダプターに対して ping を実行できたが現在 VLAN 102 メンバーはありません。



1. アクセス VLAN 設定を両方の自動タグ付けが正しくない VLAN ID を持つエグレス トラフィックを防ぐために、アクセス VLAN ID とも一致しない受信トラフィックをフィルター処理を防ぐためには、物理 NIC から削除します。

   ```PowerShell    
   New-NetIPAddress -InterfaceAlias "vEthernet (SMB1)" -IPAddress 192.168.2.111 -PrefixLength 24
   ```

   _**結果:**_  

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

2. リモートの VLAN 102 アダプターをテストします。
    
   ```PowerShell
   Test-NetConnection 192.168.2.5 
   ```
   
   _**結果:**_  
   
   ```
   ComputerName   : 192.168.2.5
   RemoteAddress  : 192.168.2.5
   InterfaceAlias : vEthernet (SMB1)
   SourceAddress  : 192.168.2.111
   PingSucceeded  : True
   PingReplyDetails (RTT) : 0 ms
   ```
    
3. インターフェイス vEthernet の新しい IP アドレスを追加\(SMB2\)します。

   ```PowerShell
   New-NetIPAddress -InterfaceAlias "vEthernet (SMB2)" -IPAddress 192.168.2.222 -PrefixLength 24 
   ```
   
   _**結果:**_ 
   
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
   
4. もう一度接続をテストします。    


5. 既存の VLAN 102 RDMA ホスト Vnic を配置します。

   ```PowerShell
   Set-VMNetworkAdapterVlan -VMNetworkAdapterName "SMB1" -VlanId "102" -Access -ManagementOS
   Set-VMNetworkAdapterVlan -VMNetworkAdapterName "SMB2" -VlanId "102" -Access -ManagementOS
    
   Get-VMNetworkAdapterVlan -ManagementOS
   ```

   _**結果:**_ 

   ```   
   VMName VMNetworkAdapterName Mode VlanList
   ------ -------------------- ---- --------
      SMB1 Access   102 
      Mgt  Access   101 
      SMB2 Access   102 
      CORP-External-Switch Untagged
   ```
   
6. SMB1 と vSwitch チームの設定 基になる物理 Nic に SMB2 のマッピングを確認します。<p>物理 Nic にホスト vNIC の関連付けは、ランダムの作成と破棄中に再調整対象とします。 このような状況での現在の関連付けを確認するのに間接のメカニズムを使用できます。 SMB1 と SMB2 の MAC アドレスは、テスト-40 G 2 NIC チームのメンバーに関連付けられます。 これは、テスト-40 G-1 が、関連付けられている SMB ホスト vNIC を持たないためが許可されていない RDMA のトラフィックの使用率、リンクを経由して、SMB ホスト vNIC がマップされるまでには適していません。

   ```PowerShell    
   Get-NetAdapterVPort (Preferred)
    
   Get-NetAdapterVmqQueue
   ```
   
   _**結果:**_ 
   
   ```
   Name   QueueID MacAddressVlanID Processor VmFriendlyName
   ----   ------- ---------------- --------- --------------
   TEST-40G-1 1   E4-1D-2D-07-40-71 1010:17
   TEST-40G-2 1   00-15-5D-30-AA-00 1020:17
   TEST-40G-2 2   00-15-5D-30-AA-01 1020:17
   ```

7. VM ネットワーク アダプターのプロパティを表示します。

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS
   ```
   
   _**結果:**_ 
   
   ```
   Name IsManagementOs VMName SwitchName   MacAddress   Status IPAddresses
   ---- -------------- ------ ----------   ----------   ------ -----------
   CORP-External-Switch True  CORP-External-Switch 001B785768AA {Ok}  
   Mgt  True  VMSTEST  E41D2D074071 {Ok}  
   SMB1 True  VMSTEST  00155D30AA00 {Ok}  
   SMB2 True  VMSTEST  00155D30AA01 {Ok}  
   ```

8. ネットワーク アダプター チームのマッピングを表示します。<p>結果ではマッピングを実行していないため、情報は返されません。
    
   ```PowerShell
   Get-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName SMB1
   Get-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName SMB2
   ```
   
   
9. SMB1 と SMB2 は、物理 NIC チームのメンバーを分離して、アクションの結果を表示するマップします。

   >[!IMPORTANT]
   >進む前に、この手順を完了するか、実装が失敗したことを確認してください。
    
   ```PowerShell
   Set-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName "SMB1" -PhysicalNetAdapterName "Test-40G-1"
   Set-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName "SMB2" -PhysicalNetAdapterName "Test-40G-2"
    
   Get-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST
   ```

   _**結果:**_ 
   
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
   
10. 以前に作成する MAC の関連付けを確認します。

    ```PowerShell    
    Get-NetAdapterVmqQueue
    ```

    _**結果:**_ 
   
    ```   
    Name   QueueID MacAddressVlanID Processor VmFriendlyName
    ----   ------- ---------------- --------- --------------
    TEST-40G-1 1   E4-1D-2D-07-40-71 1010:17
    TEST-40G-1 2   00-15-5D-30-AA-00 1020:17
    TEST-40G-2 1   00-15-5D-30-AA-01 1020:17
    ```


11. 両方のホスト Vnic が同じサブネット上に存在し、VLAN ID が同じであるため、リモート システムからの接続をテスト\(102\)します。

    ```PowerShell 
    Test-NetConnection 192.168.2.111
    ```

    _**結果:**_   

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

    _**結果:**_   

    ```
    ComputerName   : 192.168.2.222
    RemoteAddress  : 192.168.2.222
    InterfaceAlias : Test-40G-2
    SourceAddress  : 192.168.2.5
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms 
    ```
12. 名前、スイッチの名前、および優先順位のタグを設定します。   

    ```PowerShell
    Set-VMNetworkAdapter -ManagementOS -Name "SMB1" -IeeePriorityTag on
    Set-VMNetworkAdapter -ManagementOS -Name "SMB2" -IeeePriorityTag on
    Get-VMNetworkAdapter -ManagementOS -Name "SMB*" | fl Name,SwitchName,IeeePriorityTag,Status
    ```

    _**結果:**_   
    
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

13. VEthernet ネットワーク アダプターのプロパティを表示します。
    
    ```PowerShell
    Get-NetAdapterRdma -Name "vEthernet*" | sort Name | ft -AutoSize
    ```

    _**結果:**_   

    ```
    Name  InterfaceDescription Enabled
    ----  -------------------- -------
    vEthernet (SMB2)  Hyper-V Virtual Ethernet Adapter #4  False  
    vEthernet (SMB1)  Hyper-V Virtual Ethernet Adapter #3  False  
    vEthernet (MGT)   Hyper-V Virtual Ethernet Adapter #2  False   
    ```

14. VEthernet のネットワーク アダプターを有効にします。  
    
    ```PowerShell
    Enable-NetAdapterRdma -Name "vEthernet (SMB1)"
    Enable-NetAdapterRdma -Name "vEthernet (SMB2)"
    Get-NetAdapterRdma -Name "vEthernet*" | sort Name | fl *
    ```

    _**結果:**_   
    
    ```
    Name  InterfaceDescription Enabled
    ----  -------------------- -------
    vEthernet (SMB2)  Hyper-V Virtual Ethernet Adapter #4  True   
    vEthernet (SMB1)  Hyper-V Virtual Ethernet Adapter #3  True  
    vEthernet (MGT)   Hyper-V Virtual Ethernet Adapter #2  False
    ```

## <a name="step-10-validate-the-rdma-functionality"></a>手順 10 です。 RDMA 機能を検証します。

VSwitch セット チームの両方のメンバーに、vSwitch が、ローカル システムをリモート システムから、RDMA 機能を検証するには。<p>ため、両方のホスト Vnic \(SMB1 と SMB2\)割り当てられている VLAN 102 には、リモート システム上の VLAN 102 アダプターを選択できます。 <p>この例で、NIC テスト-40 G-2 では RDMA SMB1 に (192.168.2.111) と SMB2 (192.168.2.222)。

>[!TIP]
>このシステム上のファイアウォールを無効にする必要があります。  詳細については、fabric ポリシーを参照してください。
>
>```PowerShell
>Set-NetFirewallProfile -All -Enabled False
>    
>Get-NetAdapterAdvancedProperty -Name "Test-40G-2"
>```
>
>_**結果:**_ 
>   
>```
>Name  DisplayNameDisplayValue   RegistryKeyword RegistryValue  
>----  -----------------------   --------------- -------------  
> .
> .
>Test-40G-2VLAN ID102VlanID  {102} 
>```
    
1. ネットワーク アダプターのプロパティを表示します。

   ```PowerShell
   Get-NetAdapter
   ```
    
   _**結果:**_ 
    
   ```
   Name  InterfaceDescriptionifIndex Status   MacAddress LinkSpeed
   ----  --------------------------- ------   ---------- ---------
   Test-40G-2Mellanox ConnectX-3 Pro Ethernet A...#3   3 Up   E4-1D-2D-07-43-D140 Gbps
   ```
   
2. ネットワーク アダプターの RDMA の情報を表示します。

   ```PowerShell
   Get-NetAdapterRdma
   ```
    
   _**結果:**_  
    
   ```
   Name  InterfaceDescription Enabled
   ----  -------------------- -------
   Test-40G-2Mellanox ConnectX-3 Pro Ethernet Adap... True   
   ```

3. 最初の物理アダプターの RDMA のトラフィックのテストを実行します。

   ```PowerShell 
   C:\TEST\Test-RDMA.PS1 -IfIndex 3 -IsRoCE $true -RemoteIpAddress 192.168.2.111 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```
    
   _**結果:**_ 
    
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

4. 2 番目の物理アダプターの RDMA のトラフィックのテストを実行します。

   ```PowerShell
   C:\TEST\Test-RDMA.PS1 -IfIndex 3 -IsRoCE $true -RemoteIpAddress 192.168.2.222 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```
    
   _**結果:**_ 
    
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
    
5. リモート コンピューターにローカルの RDMA のトラフィックをテストします。

    ```PowerShell
    Get-NetAdapter | ft –AutoSize
    ```
    
    _**結果:**_ 
    
    ```
    Name  InterfaceDescriptionifIndex Status   MacAddress LinkSpeed
    ----  --------------------------- ------   ---------- ---------
    vEthernet (SMB2)  Hyper-V Virtual Ethernet Adapter #4  45 Up   00-15-5D-30-AA-0380 Gbps
    vEthernet (SMB1)  Hyper-V Virtual Ethernet Adapter #3  41 Up   00-15-5D-30-AA-0280 Gbps
    ```

6. 最初の仮想アダプターの RDMA のトラフィックのテストを実行します。    
    
   ```
   C:\TEST\Test-RDMA.PS1 -IfIndex 41 -IsRoCE $true -RemoteIpAddress 192.168.2.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```
    
   _**結果:**_ 
    
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

7. 2 つ目の仮想アダプターの RDMA のトラフィックのテストを実行します。

   ```PowerShell
   C:\TEST\Test-RDMA.PS1 -IfIndex 45 -IsRoCE $true -RemoteIpAddress 192.168.2.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```
    
   _**結果:**_ 
    
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
    
この出力の最後の行"RDMA のトラフィックのテスト成功。RDMA のトラフィックは、192.168.2.5 に送信された"は、アダプターに収束の NIC が正しく構成されたことを示します。

## <a name="related-topics"></a>関連トピック 

- [1 つのネットワーク アダプターに収束の NIC の構成](cnic-single.md)
- [収束の NIC の物理スイッチの構成](cnic-app-switch-config.md)
- [集約型のない NIC 構成のトラブルシューティング](cnic-app-troubleshoot.md)
