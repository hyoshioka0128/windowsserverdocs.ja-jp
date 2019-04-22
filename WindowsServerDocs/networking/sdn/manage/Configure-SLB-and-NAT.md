---
title: 負荷分散およびネットワーク アドレス変換 (NAT) のためのソフトウェア ロード バランサーを構成する
description: このトピックでは、方法をテナントのワークロードの管理と Windows Server 2016 での仮想ネットワークへのソフトウェアによるネットワーク制御のガイドの一部です。
manager: dougkim
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 73bff8ba-939d-40d8-b1e5-3ba3ed5439c3
ms.author: pashort
author: shortpatti
ms.date: 08/23/2018
ms.openlocfilehash: 55847bfbc0362887497514009f6efe1312d79906
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819353"
---
# <a name="configure-the-software-load-balancer-for-load-balancing-and-network-address-translation-nat"></a>負荷分散およびネットワーク アドレス変換 (NAT) のためのソフトウェア ロード バランサーを構成する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックを使用するには、ソフトウェア定義ネットワークを使用する方法について\(SDN\)ソフトウェア ロード バランサー \(SLB\)発信ネットワーク アドレス変換を提供する\(NAT\)、受信 NAT、またはアプリケーションの複数のインスタンス間の負荷分散します。

## <a name="software-load-balancer-overview"></a>ソフトウェア ロード バランサーの概要

SDN ソフトウェア ロード バランサー \(SLB\)をアプリケーションに高可用性とネットワークのパフォーマンスを提供します。 レイヤー 4 は\(TCP、UDP\)ロード バランサーでクラウド サービスまたはロード バランサーのセットで定義されている仮想マシンの正常なサービス インスタンス間で着信トラフィックを分散します。

SLB には、次を構成します。

- 着信トラフィックを負荷分散の仮想マシンに仮想ネットワークの外部\(Vm\)、パブリック VIP の負荷分散とも呼ばれます。
- 着信トラフィックを負荷分散仮想ネットワーク内の Vm 間、クラウド サービス内の Vm 間、または、オンプレミス コンピューターとクロスプレミス仮想ネットワーク内の Vm の間。 
- VM ネットワーク トラフィックを仮想ネットワークから送信 NAT. とも呼ばれるネットワーク アドレス変換 (NAT) を使用して外部の送信先に転送します。
- 受信 NAT. とも呼ばれる特定の VM に外部トラフィックを転送します。




## <a name="example-create-a-public-vip-for-load-balancing-a-pool-of-two-vms-on-a-virtual-network"></a>以下に例を示します。負荷分散、仮想ネットワーク上の 2 つの Vm のプールのパブリック VIP を作成します。

この例では VIP に要求を処理するプールのメンバーとしてパブリック VIP と 2 つの Vm とロード バランサーのオブジェクトを作成します。 このコード例では、プール メンバーの 1 つが応答していないかどうかを検出するために、HTTP の正常性プローブも追加します。

1. ロード バランサー オブジェクトを準備します。

   ```PowerShell
    import-module NetworkController

    $URI = "https://sdn.contoso.com"

    $LBResourceId = "LB2"

    $LoadBalancerProperties = new-object Microsoft.Windows.NetworkController.LoadBalancerProperties
   ```

2. 一般的に呼ばれる仮想 IP (VIP) として、フロント エンド IP アドレスを割り当てます。<p>未使用の ip アドレスをロード バランサー マネージャーに指定された論理ネットワークの IP プールのいずれかから VIP があります。 

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

3. Vm の負荷分散セットのメンバーを構成する動的 Ip (Dip) を含むバック エンド アドレス プールを割り当てます。 

   ```PowerShell 
    $BackEndAddressPool = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPool
    $BackEndAddressPool.ResourceId = "BE1"
    $BackEndAddressPool.ResourceRef = "/loadBalancers/$LBResourceId/backendAddressPools/$($BackEndAddressPool.ResourceId)"

    $BackEndAddressPool.Properties = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPoolProperties

    $LoadBalancerProperties.backendAddressPools += $BackEndAddressPool
   ```

4. ロード バランサーを使用して、バックエンド プール メンバーのヘルス状態を判断する正常性プローブを定義します。<p>クエリを実行する HTTP プローブの RequestPath は、この例で定義する"/health.htm"。  クエリでは、5 秒ごと、IntervalInSeconds プロパティで指定されたを実行します。<p>正常性プローブが正常バック エンド IP を考慮するプローブの連続したクエリを 11 の 200 の HTTP 応答コードを受け取る必要があります。 バック エンド IP が正常でない場合は、ロード バランサーからトラフィックを受け取ることはしません。

   >[!IMPORTANT]
   >任意のアクセス制御リスト (Acl) のプローブの発生ポイントであるためです: バックエンド IP に適用するため、サブネット内の最初の IP との間のトラフィックをブロックしません。

   次の例を使用すると、正常性プローブを定義します。

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

5.  負荷分散をバック エンド IP フロント エンド IP に到着したトラフィックを送信する規則を定義します。  この例では、バックエンド プールは、ポート 80 への TCP トラフィックを受け取ります。<p>負荷分散規則を定義するのにには、次の例を使用します。

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

6. ネットワーク コント ローラーには、ロード バランサーの構成を追加します。<p>次の例を使用すると、ネットワーク コント ローラーにロード バランサーの構成を追加します。

   ```PowerShell
    $LoadBalancerResource = New-NetworkControllerLoadBalancer -ConnectionUri $URI -ResourceId $LBResourceId -Properties $LoadBalancerProperties -Force -PassInnerException
   ```

7. このバックエンド プールにネットワーク インターフェイスを追加する次の例に従います。


## <a name="example-use-slb-for-outbound-nat"></a>以下に例を示します。SLB を使用して、アウト バウンド nat

この例では、インターネットへの送信に到達する仮想ネットワークのプライベート アドレス空間上の VM に対して送信の NAT 機能を提供するためのバックエンド プールを SLB を構成します。 

1. ロード バランサーのプロパティ、フロント エンド IP、およびバック エンド プールを作成します。

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

3. ネットワーク コント ローラーで、ロード バランサー オブジェクトを追加します。

   ```PowerShell
    $LoadBalancerResource = New-NetworkControllerLoadBalancer -ConnectionUri $URI -ResourceId $LBResourceId -Properties $LoadBalancerProperties -Force -PassInnerException
   ```

4. インターネット アクセスを提供するネットワーク インターフェイスを追加する次の例に従います。

## <a name="example-add-network-interfaces-to-the-back-end-pool"></a>以下に例を示します。バックエンド プールにネットワーク インターフェイスを追加します。
この例では、バックエンド プールにネットワーク インターフェイスを追加します。  各ネットワーク インターフェイスの VIP に対して行われた要求を処理できるは、この手順を繰り返す必要があります。 

複数のロード バランサーのオブジェクトに追加する 1 つのネットワーク インターフェイスでは、このプロセスを繰り返すこともできます。 たとえば、web サーバーの VIP のロード バランサーのオブジェクトと送信 NAT. を提供する別のロード バランサーのオブジェクトがある場合
    
1. ネットワーク インターフェイスを追加するバックエンド プールを含むロード バランサーのオブジェクトを取得します。

   ```PowerShell
   $lbresourceid = "LB2"
   $lb = get-networkcontrollerloadbalancer -connectionuri $uri -resourceID $LBResourceId -PassInnerException
  ```

2. ネットワーク インターフェイスを取得し、loadbalancerbackendaddresspools 配列に backendaddress プールを追加します。

   ```PowerShell
   $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06 -PassInnerException
   $nic.properties.IpConfigurations[0].properties.LoadBalancerBackendAddressPools += $lb.properties.backendaddresspools[0]
   ```  

3. 変更を適用するネットワーク インターフェイスを配置します。 

   ```PowerShell
   new-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06 -properties $nic.properties -force -PassInnerException
   ``` 


## <a name="example-use-the-software-load-balancer-for-forwarding-traffic"></a>以下に例を示します。ソフトウェア ロード バランサーを使用して、トラフィックの転送
個々 のポートを定義することがなく、仮想 IP を仮想ネットワーク上の 1 つのネットワーク インターフェイスにマップする必要がある場合は、L3 の転送ルールを作成できます。  このルールは、PublicIPAddress オブジェクトに含まれる割り当てられた VIP 経由で VM とのすべてのトラフィックを転送します。

VIP および DIP を定義した場合、同じサブネットとしてし、これに相当 NAT. せず L3 転送を実行します。

>[!NOTE]
>このプロセスでは、ロード バランサー オブジェクトを作成する必要はありません。  ソフトウェア ロード バランサーの構成を実行するのに十分な情報には、PublicIPAddress をネットワーク インターフェイスに割り当てることです。


1. VIP を格納するパブリック IP オブジェクトを作成します。

   ```PowerShell
   $publicIPProperties = new-object Microsoft.Windows.NetworkController.PublicIpAddressProperties
   $publicIPProperties.ipaddress = "10.127.134.7"
   $publicIPProperties.PublicIPAllocationMethod = "static"
   $publicIPProperties.IdleTimeoutInMinutes = 4
   $publicIP = New-NetworkControllerPublicIpAddress -ResourceId "MyPIP" -Properties $publicIPProperties -ConnectionUri $uri -Force -PassInnerException
   ```

2. ネットワーク インターフェイスには、PublicIPAddress を割り当てます。

   ```PowerShell
   $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06
   $nic.properties.IpConfigurations[0].Properties.PublicIPAddress = $publicIP
   New-NetworkControllerNetworkInterface -ConnectionUri $uri -ResourceId $nic.ResourceId -Properties $nic.properties -PassInnerException
   ```

## <a name="example-use-the-software-load-balancer-for-forwarding-traffic-with-a-dynamically-allocated-vip"></a>以下に例を示します。動的に割り当てられた VIP とトラフィックを転送するためのソフトウェア ロード バランサーの使用します。
この例の繰り返し操作は、前の例と同じですが、VIP を特定の IP アドレスを指定する代わりに、load balancer で利用可能な Vip プールから自動的に割り当てます。 

1. VIP を格納するパブリック IP オブジェクトを作成します。

   ```PowerShell
   $publicIPProperties = new-object Microsoft.Windows.NetworkController.PublicIpAddressProperties
   $publicIPProperties.PublicIPAllocationMethod = "dynamic"
   $publicIPProperties.IdleTimeoutInMinutes = 4
   $publicIP = New-NetworkControllerPublicIpAddress -ResourceId "MyPIP" -Properties $publicIPProperties -ConnectionUri $uri -Force -PassInnerException
   ```

2. IP アドレスの割り当てを判断するために、PublicIPAddress リソースのクエリを実行します。

   ```PowerShell
    (Get-NetworkControllerPublicIpAddress -ConnectionUri $uri -ResourceId "MyPIP").properties
   ```

   IpAddress プロパティには、割り当てられたアドレスが含まれています。  出力は、次のようになります。
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
 
1. ネットワーク インターフェイスには、PublicIPAddress を割り当てます。

   ```PowerShell
   $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06
   $nic.properties.IpConfigurations[0].Properties.PublicIPAddress = $publicIP
   New-NetworkControllerNetworkInterface -ConnectionUri $uri -ResourceId $nic.ResourceId -Properties $nic.properties -PassInnerException
   ```
## <a name="example-remove-a-publicip-address-that-is-being-used-for-forwarding-traffic-and-return-it-to-the-vip-pool"></a>以下に例を示します。トラフィックを転送するために使用されているパブリック Ip アドレスを削除して、VIP プールに戻します
この例では、前の例で作成された PublicIPAddress リソースを削除します。  PublicIPAddress が削除されると、ネットワーク インターフェイスからは、PublicIPAddress への参照が自動的に削除する、転送されるトラフィックは停止および IP アドレスが再利用のためのパブリック VIP プールに返されます。  

1. パブリック Ip を削除します。

   ```PowerShell
   Remove-NetworkControllerPublicIPAddress -ConnectionURI $uri -ResourceId "MyPIP"
   ```

---


 