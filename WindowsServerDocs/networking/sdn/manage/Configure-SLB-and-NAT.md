---
title: 負荷分散ソフトウェア ロード バランサーを構成し、ネットワーク アドレス変換 (NAT)
description: このトピックでは、テナント ワークロードを管理および Windows Server 2016 での仮想ネットワークに方法について、ソフトウェア定義ネットワーク ガイドの一部です。
manager: brianlic
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
ms.openlocfilehash: 7f0393db564061caa0bc8f18b1d623f24749b46c
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="configure-the-software-load-balancer-for-load-balancing-and-network-address-translation-nat"></a>負荷分散ソフトウェア ロード バランサーを構成し、ネットワーク アドレス変換 (NAT)

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、ソフトウェア定義ネットワーク \(SDN\) ソフトウェア ロード バランサーを使用する方法について \(SLB\) 発信ネットワーク アドレス変換 NAT、受信の NAT を提供、またはアプリケーションの複数のインスタンス間の負荷分散します。

このトピックには、次のセクションが含まれています。

- [ソフトウェア ロード バランサーの概要](#bkmk_slbover)
- [例: 負荷分散プールの仮想ネットワーク上の 2 つの Vm のパブリック VIP を作成します。](#bkmk_publicvip)
- [出力方向の NAT の使用 SLB 例:](#bkmk_obnat)
- [例: ネットワーク インターフェイスをバックエンド プールに追加します。](#bkmk_backend)
- [例: トラフィックを転送するため、ソフトウェア ロード バランサーを使用します。](#bkmk_forward)

## <a name="bkmk_slbover"></a>ソフトウェア ロード バランサーの概要

SDN のソフトウェア ロード バランサー \(SLB\) は、アプリケーションに高可用性とネットワークのパフォーマンスを提供します。 値がレイヤー 4 \ (TCP、UDP\) のロード バランサーがクラウド サービスまたはロード バランサーのセットで定義されている仮想マシンの正常なサービス インスタンス間での着信トラフィックを分散します。

SLB には、次を構成することができます。

* 負荷分散の着信トラフィックの外部の仮想マシン \(VMs\) への仮想ネットワークにします。 これには、パブリック VIP 負荷分散は呼び出されます。
* 負荷分散着信トラフィック仮想ネットワーク内のバーチャル マシンの間で、クラウド サービスでの Vm 間、または、社内のコンピューターとクロスプレミスの仮想ネットワーク内のバーチャル マシン間でします。 
* ネットワーク アドレス変換 (NAT) を使用して外部の送信先に仮想ネットワークからの VM ネットワークのトラフィックを転送します。  これは発信 NAT. と呼ばれます
* 特定の VM に外部のトラフィックを転送します。  これは受信 NAT. と呼ばれます

>[!IMPORTANT]
>既知の問題では、NetworkController の Windows PowerShell モジュールでは、ロード バランサー オブジェクトが Windows Server 2016 5 では正しく動作しなくなります。 回避策では、動的なハッシュ テーブルと Invoke-webrequest を代わりに使用します。 このメソッドは、次の例で示されます。


## <a name="bkmk_publicvip"></a>例: 負荷分散プールの仮想ネットワーク上の 2 つの Vm のパブリック VIP を作成します。

この例は、VIP を要求を処理するプールのメンバーとしてのパブリック VIP と 2 つの Vm でロード バランサー オブジェクトを作成するを使用することができます。  次のコード例では、プールのメンバーのいずれかが、応答しなくなるかどうかを検出するために HTTP 正常性プローブも追加されます。

###<a name="step-1-prepare-the-load-balancer-object"></a>手順 1: ロード バランサー オブジェクトを準備します。
次の例を使用すると、ロード バランサー オブジェクトを準備します。

    $lbresourceId = "LB2"

    $lbproperties = @{}
    $lbproperties.frontendipconfigurations = @()
    $lbproperties.backendAddressPools = @()
    $lbproperties.probes = @()
    $lbproperties.loadbalancingRules = @()
    $lbproperties.OutboundNatRules = @()

###<a name="step-2-assign-a-front-end-ip"></a>手順 2: は、フロント エンド IP を割り当てる
フロント エンド IP、一般として仮想 IP (VIP)。  VIP は、以前にロード バランサー マネージャーに割り当てられた IP プールの論理ネットワークのいずれかで未使用の IP から取得する必要があります。

次の例を使用して、フロント エンド IP アドレスを割り当てることができます。

    $vipip = "10.127.132.5"
    $vipln = get-networkcontrollerlogicalnetwork -ConnectionUri $uri -resourceid "f8f67956-3906-4303-94c5-09cf91e7e311"

    $fe = @{}
    $fe.resourceId = "FE1"
    $fe.resourceRef = "/loadBalancers/$lbresourceId/frontendIPConfigurations/$($fe.resourceId)"
    $fe.properties = @{}
    $fe.properties.subnet = @{}
    $fe.properties.subnet.ResourceRef = $vipln.properties.Subnets[0].ResourceRef
    $fe.properties.privateIPAddress = $vipip
    $fe.properties.privateIPAllocationMethod = "Static"
    $lbproperties.frontendipconfigurations += $fe

###<a name="step-3-allocate-a-backend-address-pool"></a>手順 3: バックエンド アドレス プールを割り当てる
バックエンド アドレス プールには、バーチャル マシンの負荷分散のセットのメンバーを構成する動的 Ip (Dip) が含まれています。 この手順でのみを割り当てる、プール。IP 構成は、後の手順で追加されます。

次の例を使用して、バック エンド アドレス プールを割り当てることができます。
 
    $backend = @{}
    $backend.resourceId = "BE1"
    $backend.resourceRef = "/loadBalancers/$lbresourceId/backendAddressPools/$($backend.resourceId)"
    $lbproperties.backendAddressPools += $backend

###<a name="step-4-define-a-health-probe"></a>手順 4: 正常性プローブを定義します。
正常性プローブは、バックエンド プールのメンバーのヘルス状態を確認するロード バランサーで使用されます。 この例では、定義するクエリを実行するための HTTP プローブの RequestPath に"/health.htm"です。  クエリは IntervalInSeconds プロパティによって指定されている、5 秒ごとに実行されます。

正常性プローブが正常にバックエンド IP を考慮すべきプローブの連続するクエリは、11 200 の HTTP 応答コードを受け取る必要があります。 バックエンド IP が正常でない、ロード バランサーは、ip トラフィックを送信しないします。

>[!Note]
>プローブの供給元ポイントであるため、アクセス制御リスト バック エンド IP に適用することはブロックしないこと、サブネット内の最初の IP との間のトラフィックが重要です。

次の例を使用して、正常性プローブを定義することができます。
 
    $lbprobe = @{}
    $lbprobe.ResourceId = "Probe1"
    $lbprobe.resourceRef = "/loadBalancers/$lbresourceId/Probes/$($lbprobe.resourceId)"
    $lbprobe.properties = @{}
    $lbprobe.properties.protocol = "HTTP"
    $lbprobe.properties.port = "80"
    $lbprobe.properties.RequestPath = "/health.htm"
    $lbprobe.properties.IntervalInSeconds = 5
    $lbprobe.properties.NumberOfProbes = 11
    $lbproperties.probes += $lbprobe

###<a name="step-5-define-a-load-balancing-rule"></a>手順 5: は、負荷分散の規則を定義します。
この負荷分散のルールは、フロント エンド IP に到着するトラフィックがバックエンド ip アドレスに送信する方法を定義します。  この例では、TCP ポート 80 のトラフィックがバックエンド プールに送信されます。

次の例を使用するには、負荷分散の規則を定義します。

    $lbrule = @{}
    $lbrule.ResourceId = "webserver1"
    $lbrule.properties = @{}
    $lbrule.properties.FrontEndIPConfigurations = @()
    $lbrule.properties.FrontEndIPConfigurations += $fe
    $lbrule.properties.backendaddresspool = $backend 
    $lbrule.properties.protocol = "TCP"
    $lbrule.properties.frontendPort = 80
    $lbrule.properties.Probe = $lbprobe
    $lbproperties.loadbalancingRules += $lbrule

###<a name="step-6-add-the-load-balancer-configuration-to-network-controller"></a>手順 6: ネットワーク コント ローラーにロード バランサーの構成を追加します。
これまでこの例では、作成されたすべてのオブジェクトは、Windows PowerShell セッションのメモリには。 この手順では、ネットワーク コント ローラーをオブジェクトを追加します。

次の例を使用して、ネットワーク コント ローラーにロード バランサーの構成を追加することができます。

    $lb = @{}
    $lb.ResourceId = $lbresourceid
    $lb.properties = $lbproperties

    $body = convertto-json $lb -Depth 100

    Invoke-WebRequest -Headers @{"Accept"="application/json"} -ContentType "application/json; charset=UTF-8" -Method "Put" -Uri "$uri/Networking/v1/loadbalancers/$lbresourceid" -Body $body -DisableKeepAlive -UseBasicParsing

このステップの後は、このバックエンド プールに、ネットワーク インターフェイスを追加する次の例に従う必要があります。

## <a name="bkmk_obnat"></a>出力方向の NAT の使用 SLB 例:

この例を使用すると、SLB、インターネットへの送信に到達するのに仮想ネットワークのプライベート アドレス空間上の VM の送信の NAT 機能を提供するためのバックエンド プールを構成します。

###<a name="step-1-create-the-loadbalancer-properties-front-end-ip-and-backend-pool"></a>手順 1: loadbalancer プロパティ、フロント エンド サーバーの IP とバックエンド プールを作成します。
Loadbalancer プロパティ、フロント エンド サーバーの IP とバックエンド プールを作成するのに次の例を使用することができます。

    $lbresourceId = "OutboundNATMembers"
    $vipip = "10.127.132.7"

    $vipln = get-networkcontrollerlogicalnetwork -ConnectionUri $uri -resourceid "f8f67956-3906-4303-94c5-09cf91e7e311"

    $lbproperties = @{}
    $lbproperties.frontendipconfigurations = @()
    $lbproperties.backendAddressPools = @()
    $lbproperties.probes = @()
    $lbproperties.loadbalancingRules = @()
    $lbproperties.OutboundNatRules = @()

    $fe = @{}
    $fe.resourceId = "FE1"
    $fe.resourceRef = "/loadBalancers/$lbresourceId/frontendIPConfigurations/$($fe.resourceId)"
    $fe.properties = @{}
    $fe.properties.subnet = @{}
    $fe.properties.subnet.ResourceRef = $vipln.properties.Subnets[0].ResourceRef
    $fe.properties.privateIPAddress = $vipip
    $fe.properties.privateIPAllocationMethod = "Static"
    $lbproperties.frontendipconfigurations += $fe

    $backend = @{}
    $backend.resourceId = "BE1"
    $backend.resourceRef = "/loadBalancers/$lbresourceId/backendAddressPools/$($backend.resourceId)"
    $lbproperties.backendAddressPools += $backend

###<a name="step-2-define-the-outbound-nat-rule"></a>手順 2: 送信の NAT 規則を定義します。
次の例を使用して、送信の NAT 規則を定義することができます。 

    $onat = @{}
    $onat.ResourceId = "onat1"
    $onat.properties = @{}
    $onat.properties.frontendipconfigurations = @()
    $onat.properties.frontendipconfigurations += $fe
    $onat.properties.backendaddresspool = $backend
    $onat.properties.protocol = "ALL"
    $lbproperties.OutboundNatRules += $onat

###<a name="step-3-add-the-load-balancer-object-in-network-controller"></a>手順 3: ネットワーク コント ローラーで、ロード バランサー オブジェクトを追加します。
次の例を使用して、ネットワーク コント ローラーで、ロード バランサー オブジェクトを追加することができます。

    $lb = @{}
    $lb.ResourceId = $lbresourceid
    $lb.properties = $lbproperties

    $body = convertto-json $lb -Depth 100

    Invoke-WebRequest -Headers @{"Accept"="application/json"} -ContentType "application/json; charset=UTF-8" -Method "Put" -Uri "$uri/Networking/v1/loadbalancers/$lbresourceid" -Body $body -DisableKeepAlive -UseBasicParsing

次の手順では、インターネット アクセスを提供するネットワーク インターフェイスを追加できます。

## <a name="bkmk_backend"></a>例: ネットワーク インターフェイスをバックエンド プールに追加します。
この例を使用すると、ネットワーク インターフェイスのバックエンド プールに追加します。

この手順を処理できる各ネットワーク インターフェイスの要求が、VIP に行われるを繰り返す必要があります。 また複数のロード バランサー オブジェクトに追加する 1 つのネットワーク インターフェイスでは、このプロセスを繰り返すことができます。 たとえば、Web サーバー VIP のロード バランサー オブジェクトと発信 NAT. を提供する別のロード バランサー オブジェクトがある場合
    
### <a name="step-1-get-the-load-balancer-object-containing-the-back-end-pool-to-which-you-will-add-a-network-interface"></a>手順 1: ネットワーク インターフェイスを追加するバックエンド プールが含まれているロード バランサー オブジェクトを取得します。
次の例を使用すると、ロード バランサー オブジェクトを取得します。

    $lbresourceid = "LB2"
    $lb = (Invoke-WebRequest -Headers @{"Accept"="application/json"} -ContentType "application/json; charset=UTF-8" -Method "Get" -Uri "$uri/Networking/v1/loadbalancers/$lbresourceid" -DisableKeepAlive -UseBasicParsing).content | convertfrom-json 

### <a name="step-2-get-the-network-interface-and-add-the-backendaddress-pool-to-the-loadbalancerbackendaddresspools-array"></a>手順 2: は、ネットワーク インターフェイスを取得し、loadbalancerbackendaddresspools 配列に backendaddress プールを追加します。
次の例を使用して、ネットワーク インターフェイスを取得し、loadbalancerbackendaddresspools 配列に backendaddress プールを追加することができます。

    $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06
    $nic.properties.IpConfigurations[0].properties.LoadBalancerBackendAddressPools += $lb.properties.backendaddresspools[0]
    
### <a name="step-3-put-the-network-interface-to-apply-the-change"></a>手順 3: 配置変更を適用するネットワーク インターフェイス
次の例を使用すると、変更を適用するのにネットワーク インターフェイスを配置します。

    new-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06 -properties $nic.properties -force
 
## <a name="bkmk_forward"></a>例: トラフィックを転送するため、ソフトウェア ロード バランサーを使用します。
を個々 のポートを定義することがなく仮想 ip アドレスを仮想ネットワーク上の単一のネットワーク インターフェイスにマップする必要がある場合は、L3 転送ルールを作成できます。  このルールは、割り当て済みの VIP は、PublicIPAddress オブジェクトに含まれている必要があります経由で VM からすべてのトラフィックを転送します。

VIP と DIP が同じサブネットに定義されている場合、これは、NAT. せず L3 転送を実行するには

>[!NOTE]
>このプロセスでは、ロード バランサー オブジェクトを作成する必要はありません。  ネットワーク インターフェイスに、PublicIPAddress を割り当てることは、その構成を実行するソフトウェア ロード バランサーのための十分な情報です。

###<a name="step-1-create-a-public-ip-object-to-contain-the-vip"></a>手順 1: VIP を格納するパブリック IP オブジェクトを作成します。
次の例を使用して、パブリック IP オブジェクトを作成することができます。

    $publicIPProperties = new-object Microsoft.Windows.NetworkController.PublicIpAddressProperties
    $publicIPProperties.ipaddress = "10.127.132.6"
    $publicIPProperties.PublicIPAllocationMethod = "static"
    $publicIPProperties.IdleTimeoutInMinutes = 4
    $publicIP = New-NetworkControllerPublicIpAddress -ResourceId "MyPIP" -Properties $publicIPProperties -ConnectionUri $uri

####<a name="step-2-assign-the-publicipaddress-to-a-network-interface"></a>手順 2: ネットワーク インターフェイスに、PublicIPAddress を割り当てる
次の例を使用して、ネットワーク インターフェイスに、PublicIPAddress を割り当てることができます。

    $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06
    $nic.properties.IpConfigurations[0].Properties.PublicIPAddress = $publicIP
    New-NetworkControllerNetworkInterface -ConnectionUri $uri -ResourceId $nic.ResourceId -Properties $nic.properties



 