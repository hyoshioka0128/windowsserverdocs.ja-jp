---
title: 仮想ネットワークでのゲスト クラスタリング
description: 仮想ネットワークに接続された仮想マシンはネットワーク コント ローラーがネットワークで通信するために割り当てられている IP アドレスを使用するのみ許可されます。  Microsoft フェールオーバー クラスタ リングなど、floating IP アドレスを必要とするクラスタ リング テクノロジでは、正常に機能する特別な手順が必要です。
manager: dougkim
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8e9e5c81-aa61-479e-abaf-64c5e95f90dc
ms.author: grcusanz
author: shortpatti
ms.date: 08/26/2018
ms.openlocfilehash: 97c20fd07d06b609686daf4d6308a9f248873036
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446341"
---
# <a name="guest-clustering-in-a-virtual-network"></a>仮想ネットワークでのゲスト クラスタリング

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

仮想ネットワークに接続された仮想マシンはネットワーク コント ローラーがネットワークで通信するために割り当てられている IP アドレスを使用するのみ許可されます。  Microsoft フェールオーバー クラスタ リングなど、floating IP アドレスを必要とするクラスタ リング テクノロジでは、正常に機能する特別な手順が必要です。

到達可能な floating IP を作成する方法は、ソフトウェア ロード バランサーを使用する\(SLB\)仮想 IP \(VIP\)します。  SLB は、現在その IP を持つマシンにトラフィックを送信できるように、その ip ポートでの正常性プローブでソフトウェア ロード バランサーを構成する必要があります。


## <a name="example-load-balancer-configuration"></a>以下に例を示します。ロード バランサーの構成

この例では、クラスター ノードになり、それらを仮想ネットワークに接続する Vm を既に作成したことを前提としています。  ガイダンスについてを参照してください[VM とテナントの仮想ネットワークまたは VLAN への接続を作成](https://technet.microsoft.com/windows-server-docs/networking/sdn/manage/create-a-tenant-vm)です。  

この例では、クラスターの floating IP アドレスを表す仮想 IP アドレス (192.168.2.100) を作成し、TCP ポート 59999 のどのノードがアクティブであることを確認するを監視する正常性プローブを構成します。

1. VIP を選択します。<p>クラスター ノードと同じサブネット内のすべての未使用または予約済みアドレス、VIP の IP アドレスを割り当てることで準備します。  VIP は、クラスターの浮動小数点のアドレスに一致する必要があります。

   ```PowerShell
   $VIP = "192.168.2.100"
   $subnet = "Subnet2"
   $VirtualNetwork = "MyNetwork"
   $ResourceId = "MyNetwork_InternalVIP"
   ```

2. ロード バランサーのプロパティ オブジェクトを作成します。

   ```PowerShell
   $LoadBalancerProperties = new-object Microsoft.Windows.NetworkController.LoadBalancerProperties
   ```

3. 作成、前面\-終了 IP アドレス。

   ```PowerShell
   $LoadBalancerProperties.frontendipconfigurations += $FrontEnd = new-object Microsoft.Windows.NetworkController.LoadBalancerFrontendIpConfiguration
   $FrontEnd.properties = new-object Microsoft.Windows.NetworkController.LoadBalancerFrontendIpConfigurationProperties
   $FrontEnd.resourceId = "Frontend1"
   $FrontEnd.resourceRef = "/loadBalancers/$ResourceId/frontendIPConfigurations/$($FrontEnd.resourceId)"
   $FrontEnd.properties.subnet = new-object Microsoft.Windows.NetworkController.Subnet
   $FrontEnd.properties.subnet.ResourceRef = "/VirtualNetworks/MyNetwork/Subnets/Subnet2"
   $FrontEnd.properties.privateIPAddress = $VIP
   $FrontEnd.properties.privateIPAllocationMethod = "Static"
   ```

4. バックアップの作成\-クラスター ノードを格納するプールを終了します。

   ```PowerShell
   $BackEnd = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPool
   $BackEnd.properties = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPoolProperties
   $BackEnd.resourceId = "Backend1"
   $BackEnd.resourceRef = "/loadBalancers/$ResourceId/backendAddressPools/$($BackEnd.resourceId)"
   $LoadBalancerProperties.backendAddressPools += $BackEnd
   ```

5. 浮動小数点のアドレスが上で現在アクティブ クラスター ノードを検出するためにプローブを追加します。 

   >[!NOTE]
   >以下に定義されたポートでの VM の永続的なアドレスに対してプローブ クエリ。  ポートは、アクティブ ノードでだけ応答する必要があります。 

   ```PowerShell
   $LoadBalancerProperties.probes += $lbprobe = new-object Microsoft.Windows.NetworkController.LoadBalancerProbe
   $lbprobe.properties = new-object Microsoft.Windows.NetworkController.LoadBalancerProbeProperties

   $lbprobe.ResourceId = "Probe1"
   $lbprobe.resourceRef = "/loadBalancers/$ResourceId/Probes/$($lbprobe.resourceId)"
   $lbprobe.properties.protocol = "TCP"
   $lbprobe.properties.port = "59999"
   $lbprobe.properties.IntervalInSeconds = 5
   $lbprobe.properties.NumberOfProbes = 11
   ```

6. 負荷分散規則の TCP ポート 1433 を追加します。<p>プロトコルとポートが必要に応じて変更できます。  できますもこの手順を繰り返します複数回追加のポートとプロトコルでは、この VIP 用です。  この場所に元の VIP を持つノードにパケットを送信するロード バランサーに指示するために、EnableFloatingIP が $true に設定されているが重要です。

   ```PowerShell
   $LoadBalancerProperties.loadbalancingRules += $lbrule = new-object Microsoft.Windows.NetworkController.LoadBalancingRule
   $lbrule.properties = new-object Microsoft.Windows.NetworkController.LoadBalancingRuleProperties
   $lbrule.ResourceId = "Rules1"

   $lbrule.properties.frontendipconfigurations += $FrontEnd
   $lbrule.properties.backendaddresspool = $BackEnd 
   $lbrule.properties.protocol = "TCP"
   $lbrule.properties.frontendPort = $lbrule.properties.backendPort = 1433 
   $lbrule.properties.IdleTimeoutInMinutes = 4
   $lbrule.properties.EnableFloatingIP = $true
   $lbrule.properties.Probe = $lbprobe
   ```

7. ネットワーク コント ローラーで、ロード バランサーを作成します。

   ```PowerShell
   $lb = New-NetworkControllerLoadBalancer -ConnectionUri $URI -ResourceId $ResourceId -Properties $LoadBalancerProperties -Force
   ```

8. バックエンド プールにクラスター ノードを追加します。<p>クラスターに必要な多くのノードをプールに追加できます。

   ```PowerShell
   # Cluster Node 1

   $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid "ClusterNode1_Network-Adapter"
   $nic.properties.IpConfigurations[0].properties.LoadBalancerBackendAddressPools += $lb.properties.backendaddresspools[0]
   $nic = new-networkcontrollernetworkinterface  -connectionuri $uri -resourceid $nic.resourceid -properties $nic.properties -force

    # Cluster Node 2

   $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid "ClusterNode2_Network-Adapter"
   $nic.properties.IpConfigurations[0].properties.LoadBalancerBackendAddressPools += $lb.properties.backendaddresspools[0]
   $nic = new-networkcontrollernetworkinterface  -connectionuri $uri -resourceid $nic.resourceid -properties $nic.properties -force
   ```

   ロード バランサーを作成し、バックエンド プールにネットワーク インターフェイスを追加、したら、クラスターを構成する準備ができます。  

9. (省略可能)Microsoft フェールオーバー クラスターを使用している場合は、次の例を続行します。 

## <a name="example-2-configuring-a-microsoft-failover-cluster"></a>例 2:Microsoft フェールオーバー クラスターの構成

フェールオーバー クラスターを構成するのには、次の手順を使用することができます。

1. インストールし、フェールオーバー クラスターのプロパティを構成します。

   ```PowerShell
   add-windowsfeature failover-clustering -IncludeManagementTools
   Import-module failoverclusters

   $ClusterName = "MyCluster"
   
   $ClusterNetworkName = "Cluster Network 1"
   $IPResourceName =  
   $ILBIP = “192.168.2.100” 

   $nodes = @("DB1", "DB2")
   ```

2. 1 つのノードでクラスターを作成します。

   ```PowerShell
   New-Cluster -Name $ClusterName -NoStorage -Node $nodes[0]
   ```

3. クラスター リソースを停止します。

   ```PowerShell
   Stop-ClusterResource "Cluster Name" 
   ```

4. クラスターの ip アドレスとプローブ ポートを設定します。<p>IP アドレスは、前の例で使用されるフロント エンド ip アドレスと一致する必要があり、プローブ ポートは、前の例でプローブ ポートと一致する必要があります。

   ```PowerShell
   Get-ClusterResource "Cluster IP Address" | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```

5. クラスター リソースを開始します。

   ```PowerShell
    Start-ClusterResource "Cluster IP Address"  -Wait 60 
    Start-ClusterResource "Cluster Name"  -Wait 60 
   ```

6. 残りのノードを追加します。

   ```PowerShell
   Add-ClusterNode $nodes[1]
   ```

_**クラスターはアクティブです。** _ トラフィックは、指定したポートで、VIP は、アクティブなノードに送られます。

---