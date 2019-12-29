---
title: 仮想ネットワーク ピアリングの構成
description: 仮想ネットワークピアリングの構成には、ピアリングされる2つの仮想ネットワークの作成が含まれます。
manager: dougkim
ms.prod: windows-server
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: ''
ms.author: pashort
author: shortpatti
ms.date: 08/08/2018
ms.openlocfilehash: 4d35501b8d876f2a178a4744d495125dea8da6c7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405815"
---
# <a name="configure-virtual-network-peering"></a>仮想ネットワーク ピアリングの構成

>適用対象:Windows Server

この手順では、Windows PowerShell を使用して、それぞれ1つのサブネットを持つ2つの仮想ネットワークを作成します。 次に、2つの仮想ネットワーク間のピアリングを構成して、両者間の接続を有効にします。

- [手順 1.最初の仮想ネットワークを作成する](#step-1-create-the-first-virtual-network)

- [手順 2.2番目の仮想ネットワークを作成する](#step-2-create-the-second-virtual-network)

- [手順 3.最初の仮想ネットワークから2番目の仮想ネットワークへのピアリングを構成する](#step-3-configure-peering-from-the-first-virtual-network-to-the-second-virtual-network)

- [手順 4.2番目の仮想ネットワークから1つ目の仮想ネットワークへのピアリングを構成する](#step-4-configure-peering-from-the-second-virtual-network-to-the-first-virtual-network)


>[!IMPORTANT]
>環境に合わせてプロパティを更新してください。

## <a name="step-1-create-the-first-virtual-network"></a>手順 1. 最初の仮想ネットワークを作成する

この手順では、Windows PowerShell を使用して HNV プロバイダーの論理ネットワークを検索し、1つのサブネットを持つ最初の仮想ネットワークを作成します。 次のサンプルスクリプトでは、1つのサブネットを含む Contoso の仮想ネットワークを作成します。

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

## <a name="step-2-create-the-second-virtual-network"></a>手順 2. 2番目の仮想ネットワークを作成する

この手順では、1つのサブネットを含む2つ目の仮想ネットワークを作成します。 次のサンプルスクリプトは、1つのサブネットを持つ Woodgrove の仮想ネットワークを作成します。

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

## <a name="step-3-configure-peering-from-the-first-virtual-network-to-the-second-virtual-network"></a>手順 3. 最初の仮想ネットワークから2番目の仮想ネットワークへのピアリングを構成する

この手順では、最初の仮想ネットワークと、前の2つの手順で作成した2番目の仮想ネットワークとの間のピアリングを構成します。 次のスクリプト例では、 **Contoso_vnet1**から**Woodgrove_vnet1**への仮想ネットワークピアリングを確立します。

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
>このピアリングを作成すると、vnet の状態が **[開始]** と表示されます。

## <a name="step-4-configure-peering-from-the-second-virtual-network-to-the-first-virtual-network"></a>手順 4. 2番目の仮想ネットワークから1つ目の仮想ネットワークへのピアリングを構成する

この手順では、2番目の仮想ネットワークと、上記の手順 1. と 2. で作成した最初の仮想ネットワークとの間のピアリングを構成します。 次のスクリプト例では、 **Woodgrove_vnet1**から**Contoso_vnet1**への仮想ネットワークピアリングを確立します。

```PowerShell
$peeringProperties = New-Object Microsoft.Windows.NetworkController.VirtualNetworkPeeringProperties 
$vnet2=Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Contoso_VNet1"
$peeringProperties.remoteVirtualNetwork = $vnet2 

# Indicates whether communication between the two virtual networks is allowed 
$peeringProperties.allowVirtualnetworkAccess = $true 

# Indicates whether forwarded traffic will be allowed across the vnets
$peeringProperties.allowForwardedTraffic = $true 

# Indicates whether the peer virtual network can access this virtual network's gateway
$peeringProperties.allowGatewayTransit = $false 

# Indicates whether this virtual network will use peer virtual network's gateway
$peeringProperties.useRemoteGateways =$false 

New-NetworkControllerVirtualNetworkPeering -ConnectionUri $uri -VirtualNetworkId “Woodgrove_vnet1” -ResourceId “WoodgrovetoContoso” -Properties $peeringProperties 

```

このピアリングを作成した後、両方のピアで vnet ピアリングの状態が [接続中] と表示**さ**れます。 現在、1つの仮想ネットワーク内の仮想マシンは、ピアリングされた仮想ネットワーク内の仮想マシンと通信できます。

---