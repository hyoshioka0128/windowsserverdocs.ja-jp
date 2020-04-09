---
title: テナント仮想ネットワークを作成、削除、または更新します。
description: このトピックでは、ソフトウェア定義ネットワーク (SDN) を展開した後に、Hyper-v ネットワーク仮想化仮想ネットワークを作成、削除、および更新する方法について説明します。 Hyper-v ネットワーク仮想化は、各テナントネットワークが個別のエンティティであるように、テナントネットワークを分離するのに役立ちます。 パブリックアクセスワークロードを構成する場合を除き、各エンティティにはクロス接続の可能性がありません。
manager: grcusanz
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 6a820826-e829-4ef2-9a20-f74235f8c25b
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/24/2018
ms.openlocfilehash: acb663cd33d015c1ce96241abffd4ca260cc5559
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854525"
---
# <a name="create-delete-or-update-tenant-virtual-networks"></a>テナントの仮想ネットワークを作成、削除、または更新する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、ソフトウェア定義ネットワーク (SDN) を展開した後に、Hyper-v ネットワーク仮想化仮想ネットワークを作成、削除、および更新する方法について説明します。 Hyper-v ネットワーク仮想化は、各テナントネットワークが個別のエンティティであるように、テナントネットワークを分離するのに役立ちます。 パブリックアクセスワークロードを構成する場合を除き、各エンティティにはクロス接続の可能性がありません。   
  
## <a name="create-a-new-virtual-network"></a>新しい仮想ネットワークを作成する  
テナントの仮想ネットワークを作成すると、Hyper-v ホスト上の一意のルーティングドメイン内に配置されます。 すべての仮想ネットワークの下に、少なくとも1つの仮想サブネットがあります。 仮想サブネットは IP プレフィックスで定義され、以前に定義された ACL を参照します。  

新しい仮想ネットワークを作成する手順は次のとおりです。

1. 仮想サブネットを作成する IP アドレスのプレフィックスを指定します。   
2. テナントトラフィックがトンネリングされる論理プロバイダーネットワークを特定します。   
3. 手順1で特定した IP プレフィックスごとに、少なくとも1つの仮想サブネットを作成します。 
4. Optional以前に作成した Acl を仮想サブネットに追加するか、テナントのゲートウェイ接続を追加します。 

次の表には、2つの架空のテナントのサブネット Id とプレフィックスの例が含まれています。 テナント Fabrikam には、2つの仮想サブネットがありますが、Contoso テナントには3つの仮想サブネットがあります。  
 
  
テナント名  |仮想サブネット ID  |仮想サブネットプレフィックス    
---------|---------|---------  
Fabrikam Fiber Web サイト    |5001         |24.30.1.0/24           
Fabrikam Fiber Web サイト     |5002         | 24.30.2.0/20          
Contoso    |6001         |  24.30.1.0/24         
Contoso    | 6002        |  24.30.2.0/24         
Contoso     | 6003        | 24.30.3.0/24          
  
次のスクリプト例では、 **NetworkController**モジュールからエクスポートされた Windows PowerShell コマンドを使用して、Contoso の仮想ネットワークと1つのサブネットを作成します。   
  
```Powershell  
import-module networkcontroller  
$URI = "https://ncrest.contoso.local"  
  
#Find the HNV Provider Logical Network  
  
$logicalnetworks = Get-NetworkControllerLogicalNetwork -ConnectionUri $uri  
foreach ($ln in $logicalnetworks) {  
   if ($ln.Properties.NetworkVirtualizationEnabled -eq "True") {  
      $HNVProviderLogicalNetwork = $ln  
   }  
}   
  
#Find the Access Control List to user per virtual subnet  
  
$acllist = Get-NetworkControllerAccessControlList -ConnectionUri $uri -ResourceId "AllowAll"  
  
#Create the Virtual Subnet  
  
$vsubnet = new-object Microsoft.Windows.NetworkController.VirtualSubnet  
$vsubnet.ResourceId = "Contoso_WebTier"  
$vsubnet.Properties = new-object Microsoft.Windows.NetworkController.VirtualSubnetProperties  
$vsubnet.Properties.AccessControlList = $acllist  
$vsubnet.Properties.AddressPrefix = "24.30.1.0/24"  
  
#Create the Virtual Network  
  
$vnetproperties = new-object Microsoft.Windows.NetworkController.VirtualNetworkProperties  
$vnetproperties.AddressSpace = new-object Microsoft.Windows.NetworkController.AddressSpace  
$vnetproperties.AddressSpace.AddressPrefixes = @("24.30.1.0/24")  
$vnetproperties.LogicalNetwork = $HNVProviderLogicalNetwork  
$vnetproperties.Subnets = @($vsubnet)  
New-NetworkControllerVirtualNetwork -ResourceId "Contoso_VNet1" -ConnectionUri $uri -Properties $vnetproperties  
  
```  
  
## <a name="modify-an-existing-virtual-network"></a>既存の Virtual Network を変更する  
Windows PowerShell を使用して、既存の仮想サブネットまたはネットワークを更新できます。   
  
次のサンプルスクリプトを実行すると、更新されたリソースは単に同じリソース ID のネットワークコントローラーに配置されます。 テナント Contoso が仮想ネットワークに新しい仮想サブネット (24.30.2.0/24) を追加する必要がある場合、ユーザーまたは Contoso の管理者は次のスクリプトを使用できます。  
  
```PowerShell  
$acllist = Get-NetworkControllerAccessControlList -ConnectionUri $uri -ResourceId "AllowAll"  
  
$vnet = Get-NetworkControllerVirtualNetwork -ResourceId "Contoso_VNet1" -ConnectionUri $uri  
  
$vnet.properties.AddressSpace.AddressPrefixes += "24.30.2.0/24"  
  
$vsubnet = new-object Microsoft.Windows.NetworkController.VirtualSubnet  
$vsubnet.ResourceId = "Contoso_DBTier"  
$vsubnet.Properties = new-object Microsoft.Windows.NetworkController.VirtualSubnetProperties  
$vsubnet.Properties.AccessControlList = $acllist  
$vsubnet.Properties.AddressPrefix = "24.30.2.0/24"  
  
$vnet.properties.Subnets += $vsubnet  
  
New-NetworkControllerVirtualNetwork -ResourceId "Contoso_VNet1" -ConnectionUri $uri -properties $vnet.properties  
  
```  
  
## <a name="delete-a-virtual-network"></a>仮想ネットワークの削除  
  
Windows PowerShell を使用して、Virtual Network を削除できます。  
  
次の Windows PowerShell の例では、リソース ID の URI に HTTP delete を発行して、テナント Virtual Network を削除します。  

```PowerShell  
Remove-NetworkControllerVirtualNetwork -ResourceId "Contoso_Vnet1" -ConnectionUri $uri  
```

