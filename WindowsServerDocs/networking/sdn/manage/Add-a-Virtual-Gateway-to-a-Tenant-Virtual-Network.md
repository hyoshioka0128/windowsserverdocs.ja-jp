---
title: テナントの仮想ネットワークに仮想ゲートウェイを追加します。
description: このトピックでは、テナント ワークロードを管理および Windows Server 2016 での仮想ネットワークに方法について、ソフトウェア定義ネットワーク ガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b9552054-4eb9-48db-a6ce-f36ae55addcd
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 351cafd1466c4b3c20e907ea221c9f58129b3443
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="add-a-virtual-gateway-to-a-tenant-virtual-network"></a>テナントの仮想ネットワークに仮想ゲートウェイを追加します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、テナント サイト間の接続とインターネットへの組織のサイトに、テナントの仮想ネットワークを提供するために Windows PowerShell コマンドレットとスクリプトを使用して、仮想ゲートウェイを構成するのに方法について説明します。   
  
RAS ゲートウェイは、各テナントによって使用される帯域幅に応じて、最大 100 個のテナントをサポートしています。 テナントのゲートウェイ プールのメンバーである RAS ゲートウェイのインスタンスに仮想ゲートウェイを追加するのにには、ネットワーク コントローラーを使用します。 ネットワーク コントローラーは、テナントの新しい仮想ゲートウェイを展開するときに使用する最適な RAS ゲートウェイを自動的に決定します。  
  
各仮想ゲートウェイは、特定のテナントに対応し、1 つ以上 (サイト間 VPN トンネル) のネットワーク接続と、必要に応じて、ボーダー ゲートウェイ プロトコル (BGP) 接続で構成されます。 これにより、お客様に、テナントの仮想ネットワークを外部ネットワークとテナントのエンタープライズ ネットワークなど、サービス プロバイダー ネットワーク、またはインターネットに接続できます。  
  
テナント仮想ゲートウェイを展開するときに、次の構成オプションがあります。  
  
**ネットワーク接続オプション**  
- IPSec、サイト間の仮想プライベート ネットワーク (VPN)   
- 汎用ルーティング カプセル化(GRE)   
- レイヤー 3 の転送  
  
**BGP の構成オプション**  
- BGP ルーターの構成  
- BGP ピアの構成  
- BGP ルーティング ポリシーの構成  
  
Windows PowerShell スクリプトの例とこのトピック内のコマンドは、これらの各オプションで RAS ゲートウェイのテナント仮想ゲートウェイを展開する方法を説明します。  
  
このトピックには、次のセクションが含まれています。  
  
- [テナントの仮想ゲートウェイを追加します。](#bkmk_addgwy)  
- [(IPsec、GRE、または L3) テナントのサイト間 VPN ネットワーク接続を追加します。](#bkmk_s2s1)  
- [ゲートウェイを BGP ルーターとして構成します。](#bkmk_bgp1)  
- [すべての接続の 3 つの種類 (IPsec、GRE、L3) で、ゲートウェイを構成および BGP](#bkmk_all3)  
- [変更または仮想ネットワークのゲートウェイを削除します。](#bkmk_modify)  
  
   
>[!IMPORTANT]  
>このトピックの「Windows PowerShell コマンドの例と提供されるスクリプトのいずれかを実行する前に値、展開に適したできるように、すべての変数値を変更する必要があります。  
  
## <a name="bkmk_addgwy"></a>テナントの仮想ゲートウェイを追加します。  
  
手順 1: は、ネットワーク コントローラーにゲートウェイ プール オブジェクトが存在することを確認します。  
```  
$uri = "https://ncrest.contoso.com"   
  
# Retrieve the Gateway Pool configuration  
$gwPool = Get-NetworkControllerGatewayPool -ConnectionUri $uri  
  
# Display in JSON format  
$gwPool | ConvertTo-Json -Depth 2   
  
  
```  
手順 2: は、テナントの仮想ネットワーク外のパケットをルーティングに使用するサブネットがネットワーク コントローラーに存在することを確認します。テナントのゲートウェイと仮想ネットワーク間のルーティングを使用するのには、仮想サブネットを取得します。  
  
```  
$uri = "https://ncrest.contoso.com"   
  
# Retrieve the Tenant Virtual Network configuration  
$Vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri  -ResourceId "Contoso_Vnet1"   
  
# Display in JSON format  
$Vnet | ConvertTo-Json -Depth 4   
  
# Retrieve the Tenant Virtual Subnet configuration  
$RoutingSubnet = Get-NetworkControllerVirtualSubnet -ConnectionUri $uri  -ResourceId "Contoso_WebTier" -VirtualNetworkID $vnet.ResourceId   
  
# Display in JSON format  
$RoutingSubnet | ConvertTo-Json -Depth 4   
  
```  
手順 3: 仮想ゲートウェイ JSON オブジェクトを作成し、ネットワーク コントローラーに追加します。  
  
```  
# Create a new object for Tenant Virtual Gateway  
$VirtualGWProperties = New-Object Microsoft.Windows.NetworkController.VirtualGatewayProperties   
  
# Update Gateway Pool reference  
$VirtualGWProperties.GatewayPools = @()   
$VirtualGWProperties.GatewayPools += $gwPool   
  
# Specify the Virtual Subnet that is to be used for routing between the gateway and Virtual Network   
$VirtualGWProperties.GatewaySubnets = @()   
$VirtualGWProperties.GatewaySubnets += $RoutingSubnet   
  
# Update the rest of the Virtual Gateway object properties  
$VirtualGWProperties.RoutingType = "Dynamic"   
$VirtualGWProperties.NetworkConnections = @()   
$VirtualGWProperties.BgpRouters = @()   
  
# Add the new Virtual Gateway for tenant   
$virtualGW = New-NetworkControllerVirtualGateway -ConnectionUri $uri  -ResourceId "Contoso_VirtualGW" -Properties $VirtualGWProperties -Force   
  
```  
  
## <a name="bkmk_s2s1"></a>(IPsec、GRE、または L3) テナントのサイト間 VPN ネットワーク接続を追加します。  
  
転送ゲートウェイの種類ごとに次の例を使用して IPsec、GRE、またはレイヤー 3 (L3) とのサイト間 VPN 接続を作成することができます。  
  
### <a name="ipsec-vpn-site-to-site-network-connection"></a>IPsec VPN サイト間のネットワーク接続  
  
ネットワーク接続の JSON オブジェクトを作成し、ネットワーク コントローラーに追加します。  
  
```  
# Create a new object for Tenant Network Connection  
$nwConnectionProperties = New-Object Microsoft.Windows.NetworkController.NetworkConnectionProperties   
  
# Update the common object properties  
$nwConnectionProperties.ConnectionType = "IPSec"   
$nwConnectionProperties.OutboundKiloBitsPerSecond = 10000   
$nwConnectionProperties.InboundKiloBitsPerSecond = 10000   
  
# Update specific properties depending on the Connection Type  
$nwConnectionProperties.IpSecConfiguration = New-Object Microsoft.Windows.NetworkController.IpSecConfiguration   
$nwConnectionProperties.IpSecConfiguration.AuthenticationMethod = "PSK"   
$nwConnectionProperties.IpSecConfiguration.SharedSecret = "P@ssw0rd"   
  
$nwConnectionProperties.IpSecConfiguration.QuickMode = New-Object Microsoft.Windows.NetworkController.QuickMode   
$nwConnectionProperties.IpSecConfiguration.QuickMode.PerfectForwardSecrecy = "PFS2048"   
$nwConnectionProperties.IpSecConfiguration.QuickMode.AuthenticationTransformationConstant = "SHA256128"   
$nwConnectionProperties.IpSecConfiguration.QuickMode.CipherTransformationConstant = "DES3"   
$nwConnectionProperties.IpSecConfiguration.QuickMode.SALifeTimeSeconds = 1233   
$nwConnectionProperties.IpSecConfiguration.QuickMode.IdleDisconnectSeconds = 500   
$nwConnectionProperties.IpSecConfiguration.QuickMode.SALifeTimeKiloBytes = 2000   
  
$nwConnectionProperties.IpSecConfiguration.MainMode = New-Object Microsoft.Windows.NetworkController.MainMode   
$nwConnectionProperties.IpSecConfiguration.MainMode.DiffieHellmanGroup = "Group2"   
$nwConnectionProperties.IpSecConfiguration.MainMode.IntegrityAlgorithm = "SHA256"   
$nwConnectionProperties.IpSecConfiguration.MainMode.EncryptionAlgorithm = "AES256"   
$nwConnectionProperties.IpSecConfiguration.MainMode.SALifeTimeSeconds = 1234   
$nwConnectionProperties.IpSecConfiguration.MainMode.SALifeTimeKiloBytes = 2000   
  
# L3 specific configuration (leave blank for IPSec)  
$nwConnectionProperties.IPAddresses = @()   
$nwConnectionProperties.PeerIPAddresses = @()   
  
# Update the IPv4 Routes that are reachable over the site-to-site VPN Tunnel  
$nwConnectionProperties.Routes = @()   
$ipv4Route = New-Object Microsoft.Windows.NetworkController.RouteInfo   
$ipv4Route.DestinationPrefix = "14.1.10.1/32"   
$ipv4Route.metric = 10   
$nwConnectionProperties.Routes += $ipv4Route   
  
# Tunnel Destination (Remote Endpoint) Address  
$nwConnectionProperties.DestinationIPAddress = "10.127.134.121"   
  
# Add the new Network Connection for the tenant  
New-NetworkControllerVirtualGatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId $virtualGW.ResourceId -ResourceId "Contoso_IPSecGW" -Properties $nwConnectionProperties -Force   
  
  
```  
### <a name="gre-vpn-site-to-site-network-connection"></a>GRE VPN サイト間のネットワーク接続  
  
ネットワーク接続の JSON オブジェクトを作成し、ネットワーク コントローラーに追加します。  
  
```  
# Create a new object for the Tenant Network Connection  
$nwConnectionProperties = New-Object Microsoft.Windows.NetworkController.NetworkConnectionProperties   
  
# Update the common object properties  
$nwConnectionProperties.ConnectionType = "GRE"   
$nwConnectionProperties.OutboundKiloBitsPerSecond = 10000   
$nwConnectionProperties.InboundKiloBitsPerSecond = 10000   
  
# Update specific properties depending on the Connection Type  
$nwConnectionProperties.GreConfiguration = New-Object Microsoft.Windows.NetworkController.GreConfiguration   
$nwConnectionProperties.GreConfiguration.GreKey = 1234   
  
# Update the IPv4 Routes that are reachable over the site-to-site VPN Tunnel  
$nwConnectionProperties.Routes = @()   
$ipv4Route = New-Object Microsoft.Windows.NetworkController.RouteInfo   
$ipv4Route.DestinationPrefix = "14.2.20.1/32"   
$ipv4Route.metric = 10   
$nwConnectionProperties.Routes += $ipv4Route   
  
# Tunnel Destination (Remote Endpoint) Address  
$nwConnectionProperties.DestinationIPAddress = "10.127.134.122"   
  
# L3 specific configuration (leave blank for GRE)  
$nwConnectionProperties.L3Configuration = New-Object Microsoft.Windows.NetworkController.L3Configuration   
$nwConnectionProperties.IPAddresses = @()   
$nwConnectionProperties.PeerIPAddresses = @()   
  
# Add the new Network Connection for the tenant  
New-NetworkControllerVirtualGatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId $virtualGW.ResourceId -ResourceId "Contoso_GreGW" -Properties $nwConnectionProperties -Force   
  
```  
### <a name="l3-forwarding-network-connection"></a>L3 転送のネットワーク接続  
  
L3 転送のネットワーク接続を構成するのには、また対応する論理ネットワークを構成する必要があります。   
  
手順 1: ネットワーク接続の転送、L3 に論理ネットワークを構成します。  
  
```  
# Create a new object for the Logical Network to be used for L3 Forwarding  
$lnProperties = New-Object Microsoft.Windows.NetworkController.LogicalNetworkProperties  
  
$lnProperties.NetworkVirtualizationEnabled = $false  
$lnProperties.Subnets = @()  
  
# Create a new object for the Logical Subnet to be used for L3 Forwarding and update properties  
$logicalsubnet = New-Object Microsoft.Windows.NetworkController.LogicalSubnet  
$logicalsubnet.ResourceId = "Contoso_L3_Subnet"  
$logicalsubnet.Properties = New-Object Microsoft.Windows.NetworkController.LogicalSubnetProperties  
$logicalsubnet.Properties.VlanID = 1001  
$logicalsubnet.Properties.AddressPrefix = "10.127.134.0/25"  
$logicalsubnet.Properties.DefaultGateways = "10.127.134.1"  
  
$lnProperties.Subnets += $logicalsubnet  
  
# Add the new Logical Network to Network Controller  
$vlanNetwork = New-NetworkControllerLogicalNetwork -ConnectionUri $uri -ResourceId "Contoso_L3_Network" -Properties $lnProperties -Force  
  
```  
手順 2: ネットワーク接続の JSON オブジェクトを作成し、ネットワーク コントローラーに追加します。  
  
```  
# Create a new object for the Tenant Network Connection  
$nwConnectionProperties = New-Object Microsoft.Windows.NetworkController.NetworkConnectionProperties   
  
# Update the common object properties  
$nwConnectionProperties.ConnectionType = "L3"   
$nwConnectionProperties.OutboundKiloBitsPerSecond = 10000   
$nwConnectionProperties.InboundKiloBitsPerSecond = 10000   
  
# GRE specific configuration (leave blank for L3)  
$nwConnectionProperties.GreConfiguration = New-Object Microsoft.Windows.NetworkController.GreConfiguration   
  
# Update specific properties depending on the Connection Type  
$nwConnectionProperties.L3Configuration = New-Object Microsoft.Windows.NetworkController.L3Configuration   
$nwConnectionProperties.L3Configuration.VlanSubnet = $vlanNetwork.properties.Subnets[0]   
  
$nwConnectionProperties.IPAddresses = @()   
$localIPAddress = New-Object Microsoft.Windows.NetworkController.CidrIPAddress   
$localIPAddress.IPAddress = "10.127.134.55"   
$localIPAddress.PrefixLength = 25   
$nwConnectionProperties.IPAddresses += $localIPAddress   
  
$nwConnectionProperties.PeerIPAddresses = @("10.127.134.65")   
  
# Update the IPv4 Routes that are reachable over the site-to-site VPN Tunnel  
$nwConnectionProperties.Routes = @()   
$ipv4Route = New-Object Microsoft.Windows.NetworkController.RouteInfo   
$ipv4Route.DestinationPrefix = "14.2.20.1/32"   
$ipv4Route.metric = 10   
$nwConnectionProperties.Routes += $ipv4Route   
  
# Add the new Network Connection for the tenant  
New-NetworkControllerVirtualGatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId $virtualGW.ResourceId -ResourceId "Contoso_L3GW" -Properties $nwConnectionProperties -Force   
  
```  
  
## <a name="bkmk_bgp1"></a>ゲートウェイを BGP ルーターとして構成します。  
  
ボーダー ゲートウェイ プロトコル (BGP) ルーターとして、ゲートウェイを構成するのには、次のサンプル スクリプトを使用できます。  
  
### <a name="add-a-bgp-router-for-the-tenant"></a>テナントの BGP ルーターを追加します。  
  
BGP ルーターの JSON オブジェクトを作成し、ネットワーク コントローラーに追加します。  
  
```  
# Create a new object for the Tenant BGP Router  
$bgpRouterproperties = New-Object Microsoft.Windows.NetworkController.VGwBgpRouterProperties   
  
# Update the BGP Router properties  
$bgpRouterproperties.ExtAsNumber = "0.64512"   
$bgpRouterproperties.RouterId = "192.168.0.2"   
$bgpRouterproperties.RouterIP = @("192.168.0.2")   
  
# Add the new BGP Router for the tenant  
$bgpRouter = New-NetworkControllerVirtualGatewayBgpRouter -ConnectionUri $uri -VirtualGatewayId $virtualGW.ResourceId -ResourceId "Contoso_BgpRouter1" -Properties $bgpRouterProperties -Force   
   
  
```  
### <a name="add-a-bgp-peer-for-this-tenant-corresponding-to-the-site-to-site-vpn-network-connection-added-above"></a>上に追加する、サイト間 VPN ネットワーク接続に対応する、このテナントの BGP ピアの追加します。  
  
BGP ピアの JSON オブジェクトを作成し、ネットワーク コントローラーに追加します。  
  
```  
# Create a new object for Tenant BGP Peer  
$bgpPeerProperties = New-Object Microsoft.Windows.NetworkController.VGwBgpPeerProperties   
  
# Update the BGP Peer properties  
$bgpPeerProperties.PeerIpAddress = "14.1.10.1"   
$bgpPeerProperties.AsNumber = 64521   
$bgpPeerProperties.ExtAsNumber = "0.64521"   
  
# Add the new BGP Peer for tenant  
New-NetworkControllerVirtualGatewayBgpPeer -ConnectionUri $uri -VirtualGatewayId $virtualGW.ResourceId -BgpRouterName $bgpRouter.ResourceId -ResourceId "Contoso_IPSec_Peer" -Properties $bgpPeerProperties -Force   
  
```  
## <a name="bkmk_all3"></a>すべての接続の 3 つの種類 (IPsec、GRE、L3) で、ゲートウェイを構成および BGP  
必要に応じて、前のすべての手順を組み合わせるし、テナントの仮想ゲートウェイ接続の 3 つのすべてのオプションを構成することができます。   
  
```  
# Create a new Virtual Gateway Properties type object  
$VirtualGWProperties = New-Object Microsoft.Windows.NetworkController.VirtualGatewayProperties  
  
# Update GatewayPool reference  
$VirtualGWProperties.GatewayPools = @()  
$VirtualGWProperties.GatewayPools += $gwPool  
  
# Specify the Virtual Subnet that is to be used for routing between GW and VNET  
$VirtualGWProperties.GatewaySubnets = @()  
$VirtualGWProperties.GatewaySubnets += $RoutingSubnet  
  
# Update some basic properties  
$VirtualGWProperties.RoutingType = "Dynamic"  
  
# Update Network Connection object(s)  
$VirtualGWProperties.NetworkConnections = @()  
  
# IPSec Connection configuration  
$ipSecConnection = New-Object Microsoft.Windows.NetworkController.NetworkConnection  
$ipSecConnection.ResourceId = "Contoso_IPSecGW"  
$ipSecConnection.Properties = New-Object Microsoft.Windows.NetworkController.NetworkConnectionProperties  
$ipSecConnection.Properties.ConnectionType = "IPSec"  
$ipSecConnection.Properties.OutboundKiloBitsPerSecond = 10000  
$ipSecConnection.Properties.InboundKiloBitsPerSecond = 10000  
  
$ipSecConnection.Properties.IpSecConfiguration = New-Object Microsoft.Windows.NetworkController.IpSecConfiguration  
  
$ipSecConnection.Properties.IpSecConfiguration.AuthenticationMethod = "PSK"  
$ipSecConnection.Properties.IpSecConfiguration.SharedSecret = "P@ssw0rd"  
  
$ipSecConnection.Properties.IpSecConfiguration.QuickMode = New-Object Microsoft.Windows.NetworkController.QuickMode  
  
$ipSecConnection.Properties.IpSecConfiguration.QuickMode.PerfectForwardSecrecy = "PFS2048"  
$ipSecConnection.Properties.IpSecConfiguration.QuickMode.AuthenticationTransformationConstant = "SHA256128"  
$ipSecConnection.Properties.IpSecConfiguration.QuickMode.CipherTransformationConstant = "DES3"  
$ipSecConnection.Properties.IpSecConfiguration.QuickMode.SALifeTimeSeconds = 1233  
$ipSecConnection.Properties.IpSecConfiguration.QuickMode.IdleDisconnectSeconds = 500  
$ipSecConnection.Properties.IpSecConfiguration.QuickMode.SALifeTimeKiloBytes = 2000  
  
$ipSecConnection.Properties.IpSecConfiguration.MainMode = New-Object Microsoft.Windows.NetworkController.MainMode  
  
$ipSecConnection.Properties.IpSecConfiguration.MainMode.DiffieHellmanGroup = "Group2"  
$ipSecConnection.Properties.IpSecConfiguration.MainMode.IntegrityAlgorithm = "SHA256"  
$ipSecConnection.Properties.IpSecConfiguration.MainMode.EncryptionAlgorithm = "AES256"  
$ipSecConnection.Properties.IpSecConfiguration.MainMode.SALifeTimeSeconds = 1234  
$ipSecConnection.Properties.IpSecConfiguration.MainMode.SALifeTimeKiloBytes = 2000  
  
$ipSecConnection.Properties.IPAddresses = @()  
$ipSecConnection.Properties.PeerIPAddresses = @()  
  
$ipSecConnection.Properties.Routes = @()  
  
$ipv4Route = New-Object Microsoft.Windows.NetworkController.RouteInfo  
$ipv4Route.DestinationPrefix = "14.1.10.1/32"  
$ipv4Route.metric = 10  
$ipSecConnection.Properties.Routes += $ipv4Route  
  
$ipSecConnection.Properties.DestinationIPAddress = "10.127.134.121"  
  
# GRE Connection configuration  
$greConnection = New-Object Microsoft.Windows.NetworkController.NetworkConnection  
$greConnection.ResourceId = "Contoso_GreGW"  
  
$greConnection.Properties = New-Object Microsoft.Windows.NetworkController.NetworkConnectionProperties  
$greConnection.Properties.ConnectionType = "GRE"  
$greConnection.Properties.OutboundKiloBitsPerSecond = 10000  
$greConnection.Properties.InboundKiloBitsPerSecond = 10000  
  
$greConnection.Properties.GreConfiguration = New-Object Microsoft.Windows.NetworkController.GreConfiguration  
$greConnection.Properties.GreConfiguration.GreKey = 1234  
  
$greConnection.Properties.IPAddresses = @()  
$greConnection.Properties.PeerIPAddresses = @()  
  
$greConnection.Properties.Routes = @()  
  
$ipv4Route = New-Object Microsoft.Windows.NetworkController.RouteInfo  
$ipv4Route.DestinationPrefix = "14.2.20.1/32"  
$ipv4Route.metric = 10  
$greConnection.Properties.Routes += $ipv4Route  
  
$greConnection.Properties.DestinationIPAddress = "10.127.134.122"  
  
$greConnection.Properties.L3Configuration = New-Object Microsoft.Windows.NetworkController.L3Configuration  
  
# L3 Forwarding connection configuration  
$l3Connection = New-Object Microsoft.Windows.NetworkController.NetworkConnection  
$l3Connection.ResourceId = "Contoso_L3GW"  
  
$l3Connection.Properties = New-Object Microsoft.Windows.NetworkController.NetworkConnectionProperties  
$l3Connection.Properties.ConnectionType = "L3"  
$l3Connection.Properties.OutboundKiloBitsPerSecond = 10000  
$l3Connection.Properties.InboundKiloBitsPerSecond = 10000  
  
$l3Connection.Properties.GreConfiguration = New-Object Microsoft.Windows.NetworkController.GreConfiguration  
$l3Connection.Properties.L3Configuration = New-Object Microsoft.Windows.NetworkController.L3Configuration  
$l3Connection.Properties.L3Configuration.VlanSubnet = $vlanNetwork.properties.Subnets[0]  
  
$l3Connection.Properties.IPAddresses = @()  
$localIPAddress = New-Object Microsoft.Windows.NetworkController.CidrIPAddress  
$localIPAddress.IPAddress = "10.127.134.55"  
$localIPAddress.PrefixLength = 25  
$l3Connection.Properties.IPAddresses += $localIPAddress  
  
$l3Connection.Properties.PeerIPAddresses = @("10.127.134.65")  
  
$l3Connection.Properties.Routes = @()  
$ipv4Route = New-Object Microsoft.Windows.NetworkController.RouteInfo  
$ipv4Route.DestinationPrefix = "14.2.20.1/32"  
$ipv4Route.metric = 10  
$l3Connection.Properties.Routes += $ipv4Route  
  
# Update BGP Router Object  
$VirtualGWProperties.BgpRouters = @()  
  
$bgpRouter = New-Object Microsoft.Windows.NetworkController.VGwBgpRouter  
$bgpRouter.ResourceId = "Contoso_BgpRouter1"  
$bgpRouter.Properties = New-Object Microsoft.Windows.NetworkController.VGwBgpRouterProperties  
  
$bgpRouter.Properties.ExtAsNumber = "0.64512"  
$bgpRouter.Properties.RouterId = "192.168.0.2"  
$bgpRouter.Properties.RouterIP = @("192.168.0.2")  
  
$bgpRouter.Properties.BgpPeers = @()  
  
# Create BGP Peer Object(s)  
# BGP Peer for IPSec Connection  
$bgpPeer_IPSec = New-Object Microsoft.Windows.NetworkController.VGwBgpPeer  
$bgpPeer_IPSec.ResourceId = "Contoso_IPSec_Peer"  
  
$bgpPeer_IPSec.Properties = New-Object Microsoft.Windows.NetworkController.VGwBgpPeerProperties  
$bgpPeer_IPSec.Properties.PeerIpAddress = "14.1.10.1"  
$bgpPeer_IPSec.Properties.AsNumber = 64521  
$bgpPeer_IPSec.Properties.ExtAsNumber = "0.64521"  
  
$bgpRouter.Properties.BgpPeers += $bgpPeer_IPSec  
  
# BGP Peer for GRE Connection  
$bgpPeer_Gre = New-Object Microsoft.Windows.NetworkController.VGwBgpPeer  
$bgpPeer_Gre.ResourceId = "Contoso_Gre_Peer"  
  
$bgpPeer_Gre.Properties = New-Object Microsoft.Windows.NetworkController.VGwBgpPeerProperties  
$bgpPeer_Gre.Properties.PeerIpAddress = "14.2.20.1"  
$bgpPeer_Gre.Properties.AsNumber = 64522  
$bgpPeer_Gre.Properties.ExtAsNumber = "0.64522"  
  
$bgpRouter.Properties.BgpPeers += $bgpPeer_Gre  
  
# BGP Peer for L3 Connection  
$bgpPeer_L3 = New-Object Microsoft.Windows.NetworkController.VGwBgpPeer  
$bgpPeer_L3.ResourceId = "Contoso_L3_Peer"  
  
$bgpPeer_L3.Properties = New-Object Microsoft.Windows.NetworkController.VGwBgpPeerProperties  
$bgpPeer_L3.Properties.PeerIpAddress = "14.3.30.1"  
$bgpPeer_L3.Properties.AsNumber = 64523  
$bgpPeer_L3.Properties.ExtAsNumber = "0.64523"  
  
$bgpRouter.Properties.BgpPeers += $bgpPeer_L3  
  
$VirtualGWProperties.BgpRouters += $bgpRouter  
  
# Finally Add the new Virtual Gateway for tenant  
New-NetworkControllerVirtualGateway -ConnectionUri $uri  -ResourceId "Contoso_VirtualGW" -Properties $VirtualGWProperties -Force  
  
```  
## <a name="bkmk_modify"></a>変更または仮想ネットワークのゲートウェイを削除します。  
  
次の例スクリプトを使用して、変更または既存のゲートウェイを削除することができます。  
  
### <a name="modify-the-configuration-of-an-existing-gateway"></a>既存のゲートウェイの構成を変更します。  
次のコマンドを使用すると、既存のゲートウェイを変更します。  
  
手順 1: コンポーネントの構成を取得し、変数に保存  
  
```  
$nwConnection = Get-NetworkControllerVirtualGatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId "Contoso_VirtualGW" -ResourceId "Contoso_IPSecGW"  
```  
手順 2: 必要なプロパティに到達し、更新プログラムの値に設定する変数の構造を移動します。  
  
```  
$nwConnection.properties.IpSecConfiguration.SharedSecret = "C0mplexP@ssW0rd"  
```  
手順 3: 構成を追加、変更後にネットワーク コントローラー上の古い構成を置き換える  
  
```  
New-NetworkControllerVirtualGatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId "Contoso_VirtualGW" -ResourceId $nwConnection.ResourceId -Properties $nwConnection.Properties -Force  
```  
### <a name="remove-a-gateway"></a>ゲートウェイを削除します。  
次の Windows PowerShell コマンドを使用して、個々 のゲートウェイ機能またはゲートウェイ全体を削除することができます。  
  
#### <a name="remove-a-network-connection"></a>ネットワーク接続を削除します。  
```  
Remove-NetworkControllerVirtualGatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId "Contoso_VirtualGW" -ResourceId "Contoso_IPSecGW" -Force  
```  
#### <a name="remove-a-bgp-peer"></a>BGP ピアを削除します。  
```  
Remove-NetworkControllerVirtualGatewayBgpPeer -ConnectionUri $uri -VirtualGatewayId "Contoso_VirtualGW" -BgpRouterName "Contoso_BgpRouter1" -ResourceId "Contoso_IPSec_Peer" -Force  
```  
#### <a name="remove-a-bgp-router"></a>BGP ルーターを削除します。  
```  
Remove-NetworkControllerVirtualGatewayBgpRouter -ConnectionUri $uri -VirtualGatewayId "Contoso_VirtualGW" -ResourceId "Contoso_BgpRouter1" -Force  
```  
#### <a name="remove-a-gateway"></a>ゲートウェイを削除します。  
```  
Remove-NetworkControllerVirtualGateway -ConnectionUri $uri -ResourceId "Contoso_VirtualGW" -Force   
```  
  
  


