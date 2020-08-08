---
title: 仮想ネットワークでのゲスト クラスタリング
description: 仮想ネットワークに接続されている仮想マシンは、ネットワークコントローラーが割り当てた IP アドレスのみを使用してネットワーク上の通信を行うことができます。  Microsoft フェールオーバークラスタリングなど、floating IP アドレスを必要とするクラスタリングテクノロジでは、いくつかの追加の手順を正しく機能させる必要があります。
manager: grcusanz
ms.topic: article
ms.assetid: 8e9e5c81-aa61-479e-abaf-64c5e95f90dc
ms.author: grcusanz
author: AnirbanPaul
ms.date: 08/26/2018
ms.openlocfilehash: 6d597d4ced923c751e54ed4678ffb2d956a7b471
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87994768"
---
# <a name="guest-clustering-in-a-virtual-network"></a>仮想ネットワークでのゲスト クラスタリング

>適用先:Windows Server (半期チャネル)、Windows Server 2016

仮想ネットワークに接続されている仮想マシンは、ネットワークコントローラーが割り当てた IP アドレスのみを使用してネットワーク上の通信を行うことができます。  Microsoft フェールオーバークラスタリングなど、floating IP アドレスを必要とするクラスタリングテクノロジでは、いくつかの追加の手順を正しく機能させる必要があります。

Floating IP を到達可能にする方法は、ソフトウェア Load Balancer \( SLB \) 仮想 IP VIP を使用することです \( \) 。  ソフトウェアロードバランサーは、その IP 上のポートに対する正常性プローブを使用して構成する必要があります。これにより、SLB は、現在その IP を使用しているコンピューターにトラフィックを送信します。


## <a name="example-load-balancer-configuration"></a>例: ロードバランサーの構成

この例では、クラスターノードとなる Vm を既に作成し、それらを Virtual Network にアタッチしていることを前提としています。  ガイダンスについて[は、VM を作成し、テナント Virtual Network または VLAN に接続](./create-a-tenant-vm.md)する方法に関する説明を参照してください。

この例では、クラスターの floating IP アドレスを表す仮想 IP アドレス (192.168.2.100) を作成し、TCP ポート59999を監視する正常性プローブを構成して、アクティブなノードを特定します。

1. VIP を選択します。<p>VIP IP アドレスを割り当てることによって準備します。これは、クラスターノードと同じサブネット内の未使用または予約済みのアドレスにすることができます。  VIP はクラスターの floating アドレスと一致している必要があります。

   ```PowerShell
   $VIP = "192.168.2.100"
   $subnet = "Subnet2"
   $VirtualNetwork = "MyNetwork"
   $ResourceId = "MyNetwork_InternalVIP"
   ```

2. ロードバランサーのプロパティオブジェクトを作成します。

   ```PowerShell
   $LoadBalancerProperties = new-object Microsoft.Windows.NetworkController.LoadBalancerProperties
   ```

3. フロント \- エンド IP アドレスを作成します。

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

4. \-クラスターノードを格納するバックエンドプールを作成します。

   ```PowerShell
   $BackEnd = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPool
   $BackEnd.properties = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPoolProperties
   $BackEnd.resourceId = "Backend1"
   $BackEnd.resourceRef = "/loadBalancers/$ResourceId/backendAddressPools/$($BackEnd.resourceId)"
   $LoadBalancerProperties.backendAddressPools += $BackEnd
   ```

5. フローティングアドレスが現在アクティブになっているクラスターノードを検出するプローブを追加します。

   >[!NOTE]
   >以下で定義されているポートでの VM の恒久アドレスに対するプローブクエリ。  ポートはアクティブノードでのみ応答する必要があります。

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

6. TCP ポート1433の負荷分散規則を追加します。<p>必要に応じて、プロトコルとポートを変更できます。  この VIP では、追加のポートと protcols に対してこの手順を複数回繰り返すこともできます。  は enablefloatingip が $true に設定されていることが重要です。これは、元の VIP が配置されているノードにパケットを送信するようにロードバランサーに指示するためです。

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

7. ネットワークコントローラーにロードバランサーを作成します。

   ```PowerShell
   $lb = New-NetworkControllerLoadBalancer -ConnectionUri $URI -ResourceId $ResourceId -Properties $LoadBalancerProperties -Force
   ```

8. クラスターノードをバックエンドプールに追加します。<p>クラスターに必要な数のノードをプールに追加できます。

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

   ロードバランサーを作成し、そのネットワークインターフェイスをバックエンドプールに追加したら、クラスターを構成することができます。

9. OptionalMicrosoft フェールオーバークラスターを使用している場合は、次の例に進んでください。

## <a name="example-2-configuring-a-microsoft-failover-cluster"></a>例 2: Microsoft フェールオーバークラスターの構成

フェールオーバークラスターを構成するには、次の手順に従います。

1. フェールオーバークラスターのプロパティをインストールして構成します。

   ```PowerShell
   add-windowsfeature failover-clustering -IncludeManagementTools
   Import-module failoverclusters

   $ClusterName = "MyCluster"

   $ClusterNetworkName = "Cluster Network 1"
   $IPResourceName =
   $ILBIP = "192.168.2.100"

   $nodes = @("DB1", "DB2")
   ```

2. 1つのノードにクラスターを作成します。

   ```PowerShell
   New-Cluster -Name $ClusterName -NoStorage -Node $nodes[0]
   ```

3. クラスターリソースを停止します。

   ```PowerShell
   Stop-ClusterResource "Cluster Name" 
   ```

4. クラスター IP とプローブポートを設定します。<p>この IP アドレスは、前の例で使用したフロントエンド ip アドレスと一致している必要があります。また、プローブポートは、前の例のプローブポートと一致している必要があります。

   ```PowerShell
   Get-ClusterResource "Cluster IP Address" | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```

5. クラスターリソースを開始します。

   ```PowerShell
    Start-ClusterResource "Cluster IP Address"  -Wait 60 
    Start-ClusterResource "Cluster Name"  -Wait 60 
   ```

6. 残りのノードを追加します。

   ```PowerShell
   Add-ClusterNode $nodes[1]
   ```

_**クラスターはアクティブです。**_ 指定されたポートで VIP に送信されるトラフィックは、アクティブノードに送られます。

---