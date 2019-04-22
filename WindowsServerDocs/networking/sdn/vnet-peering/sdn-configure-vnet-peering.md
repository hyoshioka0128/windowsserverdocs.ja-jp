---
title: 仮想ネットワーク ピアリングの構成
description: 仮想ネットワーク ピアリングを構成するには、取得、ピアリングされた 2 つの仮想ネットワークを作成する必要があります。
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: ''
ms.author: pashort
author: shortpatti
ms.date: 08/08/2018
ms.openlocfilehash: 3ef3db879080e3372e7b287dcc55ae052c1fe109
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816393"
---
# <a name="configure-virtual-network-peering"></a>仮想ネットワーク ピアリングの構成

>適用対象:Windows Server

この手順では、Windows PowerShell を使用して、それぞれ 1 つのサブネットを持つ 2 つの仮想ネットワークを作成します。 次に、それらの間の接続を有効にする 2 つの仮想ネットワーク間のピアリングを構成します。

- [手順 1 です。最初の仮想ネットワークを作成します。](#step-1-create-the-first-virtual-network)

- [手順 2 です。2 つ目の仮想ネットワークを作成します。](#step-2-create-the-second-virtual-network)

- [手順 3 です。2 つ目の仮想ネットワークに最初の仮想ネットワークからピアリングを構成します。](#step-3-configure-peering-from-the-first-virtual-network-to-the-second-virtual-network)

- [手順 4 です。最初の仮想ネットワークに 2 つ目の仮想ネットワークからピアリングを構成します。](#step-4-configure-peering-from-the-second-virtual-network-to-the-first-virtual-network)


>[!IMPORTANT]
>環境のプロパティを更新してください。

## <a name="step-1-create-the-first-virtual-network"></a>手順 1. 最初の仮想ネットワークを作成します。

この手順でする検索を使用して Windows PowerShell、HNV プロバイダー論理ネットワークを 1 つのサブネットで最初の仮想ネットワークを作成します。 次のスクリプトの例では、1 つのサブネットで Contoso の仮想ネットワークを作成します。

``` PowerShell
#Find the HNV Provider Logical Network  

$logicalnetworks = Get-NetworkControllerLogicalNetwork -ConnectionUri $uri  
foreach ($ln in $logicalnetworks) {  
   if ($ln.Properties.NetworkVirtualizationEnabled -eq "True") {  
      $HNVProviderLogicalNetwork = $ln  
   }  
}   

#Create the Virtual Subnet  

$vsubnet = new-object Microsoft.Windows.NetworkController.VirtualSubnet  
$vsubnet.ResourceId = "Contoso"  
$vsubnet.Properties = new-object Microsoft.Windows.NetworkController.VirtualSubnetProperties  
$vsubnet.Properties.AddressPrefix = "24.30.1.0/24"
$uri=”https://restserver”  

#Create the Virtual Network  

$vnetproperties = new-object Microsoft.Windows.NetworkController.VirtualNetworkProperties  
$vnetproperties.AddressSpace = new-object Microsoft.Windows.NetworkController.AddressSpace  
$vnetproperties.AddressSpace.AddressPrefixes = @("24.30.1.0/24")  
$vnetproperties.LogicalNetwork = $HNVProviderLogicalNetwork  
$vnetproperties.Subnets = @($vsubnet)  
New-NetworkControllerVirtualNetwork -ResourceId "Contoso_VNet1" -ConnectionUri $uri -Properties $vnetproperties
```

## <a name="step-2-create-the-second-virtual-network"></a>手順 2.  2 つ目の仮想ネットワークを作成します。

この手順では、1 つのサブネットを持つ 2 つ目の仮想ネットワークを作成します。 次のスクリプトの例では、1 つのサブネットを持つ Woodgrove の仮想ネットワークを作成します。

``` PowerShell

#Create the Virtual Subnet  

$vsubnet = new-object Microsoft.Windows.NetworkController.VirtualSubnet  
$vsubnet.ResourceId = "Woodgrove"  
$vsubnet.Properties = new-object Microsoft.Windows.NetworkController.VirtualSubnetProperties  
$vsubnet.Properties.AddressPrefix = "24.30.2.0/24"  
$uri=”https://restserver”

#Create the Virtual Network  

$vnetproperties = new-object Microsoft.Windows.NetworkController.VirtualNetworkProperties  
$vnetproperties.AddressSpace = new-object Microsoft.Windows.NetworkController.AddressSpace  
$vnetproperties.AddressSpace.AddressPrefixes = @("24.30.2.0/24")  
$vnetproperties.LogicalNetwork = $HNVProviderLogicalNetwork  
$vnetproperties.Subnets = @($vsubnet)  
New-NetworkControllerVirtualNetwork -ResourceId "Woodgrove_VNet1" -ConnectionUri $uri -Properties $vnetproperties
```

## <a name="step-3-configure-peering-from-the-first-virtual-network-to-the-second-virtual-network"></a>手順 3. 2 つ目の仮想ネットワークに最初の仮想ネットワークからピアリングを構成します。

この手順では、最初の仮想ネットワークと前の 2 つの手順で作成した 2 つ目の仮想ネットワーク間のピアリングを構成します。 次のスクリプトの例から仮想ネットワークのピアリングは確立**Contoso_vnet1**に**Woodgrove_vnet1**します。

```PowerShell
$peeringProperties = New-Object Microsoft.Windows.NetworkController.VirtualNetworkPeeringProperties
$vnet2 = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Woodgrove_VNet1"
$peeringProperties.remoteVirtualNetwork = $vnet2

#Indicate whether communication between the two virtual networks
$peeringProperties.allowVirtualnetworkAccess = $true

#Indicates whether forwarded traffic is allowed across the vnets
$peeringProperties.allowForwardedTraffic = $true

#Indicates whether the peer virtual network can access this virtual networks gateway
$peeringProperties.allowGatewayTransit = $false

#Indicates whether this virtual network uses peer virtual networks gateway
$peeringProperties.useRemoteGateways =$false

New-NetworkControllerVirtualNetworkPeering -ConnectionUri $uri -VirtualNetworkId “Contoso_vnet1” -ResourceId “ContosotoWoodgrove” -Properties $peeringProperties

```

>[!IMPORTANT]
>このピアリングを作成した後、vnet の状態を示しています**Initiated**します。

## <a name="step-4-configure-peering-from-the-second-virtual-network-to-the-first-virtual-network"></a>手順 4. 最初の仮想ネットワークに 2 つ目の仮想ネットワークからピアリングを構成します。

この手順では、2 つ目の仮想ネットワークと、次の手順 1. および 2. を上記で作成した最初の仮想ネットワーク間のピアリングを構成します。 次のスクリプトの例から仮想ネットワークのピアリングは確立**Woodgrove_vnet1**に**Contoso_vnet1**します。

```PowerShell
$peeringProperties = New-Object Microsoft.Windows.NetworkController.VirtualNetworkPeeringProperties 
$vnet2=Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Contoso_VNet1"
$peeringProperties.remoteVirtualNetwork = $vnet2 

# Indicates whether communication between the two virtual networks is allowed 
$peeringProperties.allowVirtualnetworkAccess = $true 

# Indicates whether forwarded traffic will be allowed across the vnets
$peeringProperties.allowForwardedTraffic = $true 

# Indicates whether the peer virtual network can access this virtual network’s gateway
$peeringProperties.allowGatewayTransit = $false 

# Indicates whether this virtual network will use peer virtual network’s gateway
$peeringProperties.useRemoteGateways =$false 

New-NetworkControllerVirtualNetworkPeering -ConnectionUri $uri -VirtualNetworkId “Woodgrove_vnet1” -ResourceId “WoodgrovetoContoso” -Properties $peeringProperties 

```

Vnet ピアリングの状態をこのピアリングを作成した後、表示**接続**両方のピアにします。 ここで、1 つの仮想ネットワーク内の仮想マシンは、ピアリングされた仮想ネットワーク内の仮想マシンと通信できます。

---