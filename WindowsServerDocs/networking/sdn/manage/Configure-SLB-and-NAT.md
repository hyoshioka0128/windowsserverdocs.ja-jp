---
title: 負荷分散およびネットワーク アドレス変換 (NAT) のためのソフトウェア ロード バランサーを構成する
description: このトピックは、Windows Server 2016 でテナントのワークロードと仮想ネットワークを管理する方法について、ソフトウェアで定義されたネットワークガイドに含まれています。
manager: grcusanz
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 73bff8ba-939d-40d8-b1e5-3ba3ed5439c3
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/23/2018
ms.openlocfilehash: 8728ea8732c762003a2bd356d00b9776c82eb481
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854545"
---
# <a name="configure-the-software-load-balancer-for-load-balancing-and-network-address-translation-nat"></a>負荷分散およびネットワーク アドレス変換 (NAT) のためのソフトウェア ロード バランサーを構成する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、ソフトウェアで定義されたネットワーク \(SDN\) ソフトウェアロードバランサー \(SLB\) を使用して、アプリケーションの複数のインスタンス間で送信ネットワークアドレス変換 \(NAT\)、受信 NAT、または負荷分散を行う方法について説明します。

## <a name="software-load-balancer-overview"></a>ソフトウェアの Load Balancer の概要

SDN ソフトウェア Load Balancer \(SLB\) は、高可用性とネットワークパフォーマンスをアプリケーションに提供します。 これは、ロードバランサーセットで定義されているクラウドサービスまたは仮想マシンの正常なサービスインスタンス間で着信トラフィックを分散するレイヤー 4 \(TCP、UDP\) ロードバランサーです。

SLB を構成して、次の操作を実行します。

- 仮想ネットワークの外部の受信トラフィックを仮想マシン \(Vm\)に負荷分散します (パブリック VIP 負荷分散とも呼ばれます)。
- 仮想ネットワーク内の Vm 間、クラウドサービス内の Vm 間、またはクロスプレミス仮想ネットワーク内のオンプレミスコンピューターと Vm 間で着信トラフィックを負荷分散します。 
- ネットワークアドレス変換 (NAT) を使用して、仮想ネットワークから外部送信先に VM ネットワークトラフィックを転送します。これは、送信 NAT とも呼ばれます。
- 外部トラフィックを特定の VM に転送する (受信 NAT とも呼ばれます)。




## <a name="example-create-a-public-vip-for-load-balancing-a-pool-of-two-vms-on-a-virtual-network"></a>例: 仮想ネットワーク上の2つの Vm のプールを負荷分散するためのパブリック VIP を作成する

この例では、パブリック VIP を持つロードバランサーオブジェクトを作成し、VIP への要求を処理するプールメンバーとして2つの Vm を作成します。 このコード例では、いずれかのプールメンバーが応答しなくなったかどうかを検出する HTTP 正常性プローブも追加されています。

1. ロードバランサーオブジェクトを準備します。

   ```PowerShell
    import-module NetworkController

    $URI = "https://sdn.contoso.com"

    $LBResourceId = "LB2"

    $LoadBalancerProperties = new-object Microsoft.Windows.NetworkController.LoadBalancerProperties
   ```

2. フロントエンド IP アドレス (一般に仮想 IP (VIP) と呼ばれます) を割り当てます。<p>VIP は、ロードバランサーマネージャーに与えられているいずれかの論理ネットワーク IP プールの未使用の IP からのものである必要があります。 

   ```PowerShell
    $VIPIP = "10.127.134.5"
    $VIPLogicalNetwork = get-networkcontrollerlogicalnetwork -ConnectionUri $uri -resourceid "PublicVIP" -PassInnerException
    
    $FrontEndIPConfig = new-object Microsoft.Windows.NetworkController.LoadBalancerFrontendIpConfiguration
    $FrontEndIPConfig.ResourceId = "FE1"
    $FrontEndIPConfig.ResourceRef = "/loadBalancers/$LBResourceId/frontendIPConfigurations/$($FrontEndIPConfig.ResourceId)"

    $FrontEndIPConfig.Properties = new-object Microsoft.Windows.NetworkController.LoadBalancerFrontendIpConfigurationProperties
    $FrontEndIPConfig.Properties.Subnet = new-object Microsoft.Windows.NetworkController.Subnet
    $FrontEndIPConfig.Properties.Subnet.ResourceRef = $VIPLogicalNetwork.Properties.Subnets[0].ResourceRef
    $FrontEndIPConfig.Properties.PrivateIPAddress = $VIPIP
    $FrontEndIPConfig.Properties.PrivateIPAllocationMethod = "Static"
      
    $LoadBalancerProperties.FrontEndIPConfigurations += $FrontEndIPConfig
   ```

3. バックエンドアドレスプールを割り当てます。これには、負荷分散された Vm のセットのメンバーを構成する動的 Ip (Dip) が含まれます。 

   ```PowerShell 
    $BackEndAddressPool = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPool
    $BackEndAddressPool.ResourceId = "BE1"
    $BackEndAddressPool.ResourceRef = "/loadBalancers/$LBResourceId/backendAddressPools/$($BackEndAddressPool.ResourceId)"

    $BackEndAddressPool.Properties = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPoolProperties

    $LoadBalancerProperties.backendAddressPools += $BackEndAddressPool
   ```

4. バックエンドプールメンバーの正常性状態を判断するためにロードバランサーが使用する正常性プローブを定義します。<p>この例では、RequestPath "/health.htm." に対してクエリを行う HTTP プローブを定義します。  クエリは、IntervalInSeconds プロパティで指定されているように、5秒ごとに実行されます。<p>正常性プローブは、バックエンド IP が正常であると判断するために、11個の連続したクエリに対して HTTP 応答コード200を受信する必要があります。 バックエンド IP が正常でない場合は、ロードバランサーからのトラフィックを受信しません。

   >[!IMPORTANT]
   >バックエンド IP に適用する任意の Access Control リスト (Acl) に対して、サブネット内の最初の IP との間のトラフィックをブロックしないでください。これは、プローブの発信ポイントであるためです。

   正常性プローブを定義するには、次の例を使用します。

   ```PowerShell
    $Probe = new-object Microsoft.Windows.NetworkController.LoadBalancerProbe
    $Probe.ResourceId = "Probe1"
    $Probe.ResourceRef = "/loadBalancers/$LBResourceId/Probes/$($Probe.ResourceId)"

    $Probe.properties = new-object Microsoft.Windows.NetworkController.LoadBalancerProbeProperties
    $Probe.properties.Protocol = "HTTP"
    $Probe.properties.Port = "80"
    $Probe.properties.RequestPath = "/health.htm"
    $Probe.properties.IntervalInSeconds = 5
    $Probe.properties.NumberOfProbes = 11

    $LoadBalancerProperties.Probes += $Probe
   ```

5. フロントエンド IP で受信したトラフィックをバックエンド IP に送信する負荷分散規則を定義します。  この例では、バックエンドプールは TCP トラフィックをポート80に受信します。<p>負荷分散規則を定義するには、次の例を使用します。

   ```PowerShell
   $Rule = new-object Microsoft.Windows.NetworkController.LoadBalancingRule
   $Rule.ResourceId = "webserver1"

   $Rule.Properties = new-object Microsoft.Windows.NetworkController.LoadBalancingRuleProperties
   $Rule.Properties.FrontEndIPConfigurations += $FrontEndIPConfig
   $Rule.Properties.backendaddresspool = $BackEndAddressPool 
   $Rule.Properties.protocol = "TCP"
   $Rule.Properties.FrontEndPort = 80
   $Rule.Properties.BackEndPort = 80
   $Rule.Properties.IdleTimeoutInMinutes = 4
   $Rule.Properties.Probe = $Probe

   $LoadBalancerProperties.loadbalancingRules += $Rule
   ```

6. ロードバランサーの構成をネットワークコントローラーに追加します。<p>ロードバランサーの構成をネットワークコントローラーに追加するには、次の例を使用します。

   ```PowerShell
    $LoadBalancerResource = New-NetworkControllerLoadBalancer -ConnectionUri $URI -ResourceId $LBResourceId -Properties $LoadBalancerProperties -Force -PassInnerException
   ```

7. 次の例に従って、このバックエンドプールにネットワークインターフェイスを追加します。


## <a name="example-use-slb-for-outbound-nat"></a>例: 送信 NAT に SLB を使用する

この例では、仮想ネットワークのプライベートアドレス空間上の VM にインターネットへの送信に接続するために、バックエンドプールを使用して SLB を構成します。 

1. ロードバランサーのプロパティ、フロントエンド IP、およびバックエンドプールを作成します。

   ```PowerShell
    import-module NetworkController
    $URI = "https://sdn.contoso.com"

    $LBResourceId = "OutboundNATMMembers"
    $VIPIP = "10.127.134.6"

    $VIPLogicalNetwork = get-networkcontrollerlogicalnetwork -ConnectionUri $uri -resourceid "PublicVIP" -PassInnerException

    $LoadBalancerProperties = new-object Microsoft.Windows.NetworkController.LoadBalancerProperties

    $FrontEndIPConfig = new-object Microsoft.Windows.NetworkController.LoadBalancerFrontendIpConfiguration
    $FrontEndIPConfig.ResourceId = "FE1"
    $FrontEndIPConfig.ResourceRef = "/loadBalancers/$LBResourceId/frontendIPConfigurations/$($FrontEndIPConfig.ResourceId)"

    $FrontEndIPConfig.Properties = new-object Microsoft.Windows.NetworkController.LoadBalancerFrontendIpConfigurationProperties
    $FrontEndIPConfig.Properties.Subnet = new-object Microsoft.Windows.NetworkController.Subnet
    $FrontEndIPConfig.Properties.Subnet.ResourceRef = $VIPLogicalNetwork.Properties.Subnets[0].ResourceRef
    $FrontEndIPConfig.Properties.PrivateIPAddress = $VIPIP
    $FrontEndIPConfig.Properties.PrivateIPAllocationMethod = "Static"

    $LoadBalancerProperties.FrontEndIPConfigurations += $FrontEndIPConfig

    $BackEndAddressPool = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPool
    $BackEndAddressPool.ResourceId = "BE1"
    $BackEndAddressPool.ResourceRef = "/loadBalancers/$LBResourceId/backendAddressPools/$($BackEndAddressPool.ResourceId)"
    $BackEndAddressPool.Properties = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPoolProperties

    $LoadBalancerProperties.backendAddressPools += $BackEndAddressPool
   ```

2. 送信 NAT 規則を定義します。

   ```PowerShell
    $OutboundNAT = new-object Microsoft.Windows.NetworkController.LoadBalancerOutboundNatRule
    $OutboundNAT.ResourceId = "onat1"
    
    $OutboundNAT.properties = new-object Microsoft.Windows.NetworkController.LoadBalancerOutboundNatRuleProperties
    $OutboundNAT.properties.frontendipconfigurations += $FrontEndIPConfig
    $OutboundNAT.properties.backendaddresspool = $BackEndAddressPool
    $OutboundNAT.properties.protocol = "ALL"

    $LoadBalancerProperties.OutboundNatRules += $OutboundNAT
   ```

3. ネットワークコントローラーにロードバランサーオブジェクトを追加します。

   ```PowerShell
    $LoadBalancerResource = New-NetworkControllerLoadBalancer -ConnectionUri $URI -ResourceId $LBResourceId -Properties $LoadBalancerProperties -Force -PassInnerException
   ```

4. 次の例に従って、インターネットアクセスを提供するネットワークインターフェイスを追加します。

## <a name="example-add-network-interfaces-to-the-back-end-pool"></a>例: バックエンドプールへのネットワークインターフェイスの追加
この例では、ネットワークインターフェイスをバックエンドプールに追加します。  VIP に対して行われた要求を処理できる各ネットワークインターフェイスに対して、この手順を繰り返す必要があります。 

また、1つのネットワークインターフェイスでこのプロセスを繰り返して、複数のロードバランサーオブジェクトに追加することもできます。 たとえば、web サーバー VIP 用のロードバランサーオブジェクトと、送信 NAT を提供する別のロードバランサーオブジェクトがあるとします。
    
1. ネットワークインターフェイスを追加するために、バックエンドプールを含むロードバランサーオブジェクトを取得します。

   ```PowerShell
   $lbresourceid = "LB2"
   $lb = get-networkcontrollerloadbalancer -connectionuri $uri -resourceID $LBResourceId -PassInnerException
   ```

2. ネットワークインターフェイスを取得し、loadbalancerbackendaddresspools 配列に backendaddress プールを追加します。

   ```PowerShell
   $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06 -PassInnerException
   $nic.properties.IpConfigurations[0].properties.LoadBalancerBackendAddressPools += $lb.properties.backendaddresspools[0]
   ```  

3. 変更を適用するためのネットワークインターフェイスを配置します。 

   ```PowerShell
   new-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06 -properties $nic.properties -force -PassInnerException
   ``` 


## <a name="example-use-the-software-load-balancer-for-forwarding-traffic"></a>例: トラフィックの転送にソフトウェア Load Balancer を使用する
個々のポートを定義せずに仮想ネットワーク上の単一のネットワークインターフェイスに仮想 IP をマップする必要がある場合は、L3 転送ルールを作成できます。  このルールは、PublicIPAddress オブジェクトに含まれる割り当て済み VIP を使用して、VM との間のすべてのトラフィックを転送します。

VIP と DIP を同じサブネットとして定義した場合、これは NAT を使用せずに L3 転送を実行するのと同じです。

>[!NOTE]
>このプロセスでは、ロードバランサーオブジェクトを作成する必要はありません。  PublicIPAddress をネットワークインターフェイスに割り当てることは、ソフトウェア Load Balancer が構成を実行するのに十分な情報です。


1. VIP を格納するパブリック IP オブジェクトを作成します。

   ```PowerShell
   $publicIPProperties = new-object Microsoft.Windows.NetworkController.PublicIpAddressProperties
   $publicIPProperties.ipaddress = "10.127.134.7"
   $publicIPProperties.PublicIPAllocationMethod = "static"
   $publicIPProperties.IdleTimeoutInMinutes = 4
   $publicIP = New-NetworkControllerPublicIpAddress -ResourceId "MyPIP" -Properties $publicIPProperties -ConnectionUri $uri -Force -PassInnerException
   ```

2. PublicIPAddress をネットワークインターフェイスに割り当てます。

   ```PowerShell
   $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06
   $nic.properties.IpConfigurations[0].Properties.PublicIPAddress = $publicIP
   New-NetworkControllerNetworkInterface -ConnectionUri $uri -ResourceId $nic.ResourceId -Properties $nic.properties -PassInnerException
   ```

## <a name="example-use-the-software-load-balancer-for-forwarding-traffic-with-a-dynamically-allocated-vip"></a>例: 動的に割り当てられた VIP でトラフィックを転送するためにソフトウェア Load Balancer を使用する
この例では、前の例と同じ操作を繰り返しますが、特定の IP アドレスを指定するのではなく、ロードバランサーの利用可能な vip プールから VIP を自動的に割り当てます。 

1. VIP を格納するパブリック IP オブジェクトを作成します。

   ```PowerShell
   $publicIPProperties = new-object Microsoft.Windows.NetworkController.PublicIpAddressProperties
   $publicIPProperties.PublicIPAllocationMethod = "dynamic"
   $publicIPProperties.IdleTimeoutInMinutes = 4
   $publicIP = New-NetworkControllerPublicIpAddress -ResourceId "MyPIP" -Properties $publicIPProperties -ConnectionUri $uri -Force -PassInnerException
   ```

2. PublicIPAddress リソースに対してクエリを実行し、どの IP アドレスが割り当てられたかを確認します。

   ```PowerShell
    (Get-NetworkControllerPublicIpAddress -ConnectionUri $uri -ResourceId "MyPIP").properties
   ```

   IpAddress プロパティには、割り当てられたアドレスが含まれます。  出力は、次のようになります。
   ```
    Counters                 : {}
    ConfigurationState       :
    IpAddress                : 10.127.134.2
    PublicIPAddressVersion   : IPv4
    PublicIPAllocationMethod : Dynamic
    IdleTimeoutInMinutes     : 4
    DnsSettings              :
    ProvisioningState        : Succeeded
    IpConfiguration          :
    PreviousIpConfiguration  :
   ```
 
3. PublicIPAddress をネットワークインターフェイスに割り当てます。

   ```PowerShell
   $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06
   $nic.properties.IpConfigurations[0].Properties.PublicIPAddress = $publicIP
   New-NetworkControllerNetworkInterface -ConnectionUri $uri -ResourceId $nic.ResourceId -Properties $nic.properties -PassInnerException
   ```
   ## <a name="example-remove-a-publicip-address-that-is-being-used-for-forwarding-traffic-and-return-it-to-the-vip-pool"></a>例: トラフィックの転送に使用されているパブリック Ip アドレスを削除し、それを VIP プールに返す
   この例では、前の例で作成した PublicIPAddress リソースを削除します。  PublicIPAddress が削除されると、PublicIPAddress への参照がネットワークインターフェイスから自動的に削除され、トラフィックが転送されなくなり、再利用のために IP アドレスがパブリック VIP プールに返されます。  

4. パブリック Ip を削除する

   ```PowerShell
   Remove-NetworkControllerPublicIPAddress -ConnectionURI $uri -ResourceId "MyPIP"
   ```

---


 