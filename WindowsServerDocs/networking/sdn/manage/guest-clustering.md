---
title: ゲストの仮想ネットワークでのクラスタ リング
description: このトピックでは、テナント ワークロードを管理および Windows Server 2016 での仮想ネットワークに方法について、ソフトウェア定義ネットワーク ガイドの一部です。
manager: brianlic
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
ms.openlocfilehash: 5cab7e7c0ca0af848b4b58362388701cc4357860
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="guest-clustering-in-a-virtual-network"></a>ゲストの仮想ネットワークでのクラスタ リング

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

仮想ネットワークに接続されている仮想マシンは、ネットワーク コント ローラーがネットワーク上で通信するために割り当てられている IP アドレスを使用する限定されます。  これは、クラスタ リング テクノロジ Microsoft フェールオーバー クラスタ リングなど、浮動 IP アドレスが必要、正しく機能するためにいくつか追加の手順を必要とすることを意味します。

到達可能な浮動 IP を行うためのメソッドは、ソフトウェア ロード バランサー \(SLB\) を使用する仮想 IP \(VIP\) します。  ソフトウェア ロード バランサーは、その IP を現在持っているマシンへのトラフィックを送信する SLB できるように、その ip ポートでの正常性プローブに構成する必要があります。

## <a name="example-load-balancer-configuration"></a>例: ロード バランサーの構成

この例で既に作成した Vm は、クラスター ノードになり、仮想ネットワークに接続されていることを想定しています。  ガイダンスについてを参照してください[バーチャル マシンとテナントの仮想ネットワークまたは VLAN に接続を作成する](https://technet.microsoft.com/windows-server-docs/networking/sdn/manage/create-a-tenant-vm)します。  

この例では、浮動、クラスターの IP アドレスを表す仮想 IP アドレス (192.168.2.100) を作成し、TCP ポートのどのノードがアクティブであることを確認する 59999 を監視するヘルス プローブを構成します。

### <a name="step-1-select-the-vip"></a>手順 1: は、VIP を選択します
VIP IP アドレスを割り当てるを準備します。  このアドレスは、クラスター ノードとして同じサブネット内の任意の未使用または予約アドレスを指定できます。  VIP は、クラスターの浮動アドレスと一致する必要があります。

    $VIP = "192.168.2.100"
    $subnet = "Subnet2"
    $VirtualNetwork = "MyNetwork"
    $ResourceId = "MyNetwork_InternalVIP"

### <a name="step-2-create-the-load-balancer-properties-object"></a>手順 2: ロード バランサーのプロパティのオブジェクトを作成します。

次のコマンド例を使用して、ロード バランサーのプロパティのオブジェクトを作成することができます。

    $LoadBalancerProperties = new-object Microsoft.Windows.NetworkController.LoadBalancerProperties

### <a name="step-3-create-a-front-end-ip-address"></a>手順 3: front\ 終了 IP アドレスを作成します。

次のコマンド例を使用すると、front\ 終了 IP アドレスを作成します。

    $LoadBalancerProperties.frontendipconfigurations += $FrontEnd = new-object Microsoft.Windows.NetworkController.LoadBalancerFrontendIpConfiguration
    $FrontEnd.properties = new-object Microsoft.Windows.NetworkController.LoadBalancerFrontendIpConfigurationProperties
    $FrontEnd.resourceId = "Frontend1"
    $FrontEnd.resourceRef = "/loadBalancers/$ResourceId/frontendIPConfigurations/$($FrontEnd.resourceId)"
    $FrontEnd.properties.subnet = new-object Microsoft.Windows.NetworkController.Subnet
    $FrontEnd.properties.subnet.ResourceRef = "/VirtualNetworks/MyNetwork/Subnets/Subnet2"
    $FrontEnd.properties.privateIPAddress = $VIP
    $FrontEnd.properties.privateIPAllocationMethod = "Static"

### <a name="step-4-create-a-back-end-pool-to-contain-the-cluster-nodes"></a>手順 4: クラスター ノードが含まれる back\ エンド プールを作成します。

次のコマンド例を使用するには back\ ツー エンドのプールを作成するには

    $BackEnd = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPool
    $BackEnd.properties = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPoolProperties
    $BackEnd.resourceId = "Backend1"
    $BackEnd.resourceRef = "/loadBalancers/$ResourceId/backendAddressPools/$($BackEnd.resourceId)"
    $LoadBalancerProperties.backendAddressPools += $BackEnd

### <a name="step-5-add-a-probe"></a>手順 5: プローブを追加します。
プローブは、浮動アドレスはで現在アクティブなクラスター ノードを検出する必要があります。

>[!NOTE]
>以下に定義されているポートでの VM の永続的なアドレスに対してプローブ クエリします。  ポートは、アクティブ ノードでのみ応答する必要があります。 

    $LoadBalancerProperties.probes += $lbprobe = new-object Microsoft.Windows.NetworkController.LoadBalancerProbe
    $lbprobe.properties = new-object Microsoft.Windows.NetworkController.LoadBalancerProbeProperties

    $lbprobe.ResourceId = "Probe1"
    $lbprobe.resourceRef = "/loadBalancers/$ResourceId/Probes/$($lbprobe.resourceId)"
    $lbprobe.properties.protocol = "TCP"
    $lbprobe.properties.port = "59999"
    $lbprobe.properties.IntervalInSeconds = 5
    $lbprobe.properties.NumberOfProbes = 11

### <a name="step-5-add-the-load-balancing-rules"></a>手順 5: 負荷分散の規則を追加します。
この手順では、負荷分散の TCP ポート 1433 のルールを作成します。  プロトコルとポートを必要に応じて変更できます。  できますまたこの手順を繰り返します複数回追加のポートとプロトコルでは、この VIP します。  これにより、ロード バランサーを元の場所で vip で書き直しますノードにパケットを送信するために、EnableFloatingIP を $true に設定されている必要があります。

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

### <a name="step-5-create-the-load-balancer-in-network-controller"></a>手順 5: ネットワーク コント ローラーで、ロード バランサーを作成します。

次のコマンド例を使用して、ロード バランサーを作成することができます。

    $lb = New-NetworkControllerLoadBalancer -ConnectionUri $URI -ResourceId $ResourceId -Properties $LoadBalancerProperties -Force

### <a name="step-6-add-the-cluster-nodes-to-the-backend-pool"></a>手順 6: バックエンド プールにクラスター ノードを追加します。

この例では、次の 2 つのプール メンバーを追加するが、クラスターに必要な数だけをプールにノードを追加することができます。

    # Cluster Node 1

    $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid "ClusterNode1_Network-Adapter"
    $nic.properties.IpConfigurations[0].properties.LoadBalancerBackendAddressPools += $lb.properties.backendaddresspools[0]
    $nic = new-networkcontrollernetworkinterface  -connectionuri $uri -resourceid $nic.resourceid -properties $nic.properties -force

    # Cluster Node 2

    $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid "ClusterNode2_Network-Adapter"
    $nic.properties.IpConfigurations[0].properties.LoadBalancerBackendAddressPools += $lb.properties.backendaddresspools[0]
    $nic = new-networkcontrollernetworkinterface  -connectionuri $uri -resourceid $nic.resourceid -properties $nic.properties -force

ロード バランサーを作成すると、ネットワーク インターフェイスをバックエンド プールに追加した、クラスターを構成することができます。  Microsoft フェールオーバー クラスターを使用している場合は、次の例を続行することができます。 

## <a name="example-2-configuring-a-microsoft-failover-cluster"></a>例 2: Microsoft フェールオーバー クラスターを構成します。

次の手順を使用すると、フェールオーバー クラスターを構成します。

### <a name="step-1-install-failover-clustering"></a>手順 1: フェールオーバー クラスタ リングをインストールします。

次の例のコマンドを使用して、インストールし、フェールオーバー クラスターのプロパティを構成することができます。

    add-windowsfeature failover-clustering -IncludeManagementTools
    Import-module failoverclusters

    $ClusterName = "MyCluster"
   
    $ClusterNetworkName = "Cluster Network 1"
    $IPResourceName =  
    $ILBIP = “192.168.2.100” 

    $nodes = @("DB1", "DB2")

### <a name="step-2-create-the-cluster-on-one-node"></a>手順 2: 1 つのノードでクラスターを作成します。

次のコマンド例を使用して、ノードでクラスターを作成することができます。

    New-Cluster -Name $ClusterName -NoStorage -Node $nodes[0]

### <a name="step-3-stop-the-cluster-resource"></a>手順 3: クラスター リソースを停止します。

次のコマンド例を使用して、クラスター リソースを停止することができます。

    Stop-ClusterResource "Cluster Name" 

### <a name="step-4-set-the-cluster-ip-and-probe-port"></a>手順 4: 設定、クラスター ip アドレスとプローブ ポート
IP アドレスは、前の例で使用されるフロント エンド ip アドレスと一致する必要があり、プローブ ポートは前の例では、プローブ ポートと一致する必要があります。

    Get-ClusterResource "Cluster IP Address" | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}

### <a name="step-5-start-the-cluster-resources"></a>手順 5: クラスター リソースを開始します。

次のコマンド例を使用すると、クラスター リソースを開始します。

    Start-ClusterResource "Cluster IP Address"  -Wait 60 
    Start-ClusterResource "Cluster Name"  -Wait 60 

### <a name="step-6-add-the-remaining-nodes"></a>手順 6: 残りのノードを追加します。

次のコマンド例を使用して、クラスター ノードを追加することができます。

    Add-ClusterNode $nodes[1]

最後の手順を完了したら、クラスターはアクティブです。 VIP しようとして指定したポートでトラフィックは、アクティブ ノードに送信されます。