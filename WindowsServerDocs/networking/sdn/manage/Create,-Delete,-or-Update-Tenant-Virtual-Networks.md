---
title: 作成、削除、またはテナントの仮想ネットワークの更新
description: このトピックでは、テナント ワークロードを管理および Windows Server 2016 での仮想ネットワークに方法について、ソフトウェア定義ネットワーク ガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6a820826-e829-4ef2-9a20-f74235f8c25b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6ef30dcc31593e15c36f846cf6d64afcd4b85f19
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="create-delete-or-update-tenant-virtual-networks"></a>作成、削除、またはテナントの仮想ネットワークの更新

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、作成、削除、およびソフトウェアによるネットワーク制御 (SDN) を展開した後、HYPER-V ネットワーク仮想化の仮想ネットワークを更新するのに方法について説明します。  
  
されるよう各テナント ネットワークを完全に別個のエンティティで相互接続がない可能性へのパブリック アクセス ワークロードを構成しない限りは、HYPER-V ネットワーク仮想化を使用して、テナント ネットワークを分離できます。  
  
テナント用に新しい仮想ネットワークを作成することができます、既存の仮想ネットワークを変更することができますおよびテナントが不要になった特定のリソースを必要とする場合、またはテナントは、お客様が不要になった場合は、テナントの仮想ネットワークを削除することができます。  
  
## <a name="create-a-new-virtual-network"></a>新しい仮想ネットワークを作成します。  
  
テナントの仮想ネットワークを作成するときに、HYPER-V ホスト上で一意のルーティング ドメイン内に置かれます。  
  
新しい仮想ネットワークを作成する手順を次に示します。  
  
1. 仮想サブネットを作成する IP アドレス プレフィックスを特定します。   
2. テナント トラフィックをトンネリングするプロバイダーの論理ネットワークを識別します。   
3. 各 IP のプレフィックス手順 1 で定義されているは、少なくとも 1 つの仮想サブネットを作成します。   
  
>[!NOTE]  
>すべての仮想ネットワークの下にある少なくとも 1 つの仮想サブネットがあります。 仮想サブネットは、IP プレフィックスによって定義され、以前に定義されたアクセス制御リストを参照します。  
  
必要に応じて、次の手順を完了した後も、仮想サブネットを以前に作成したアクセス制御リストを追加したり、テナントのゲートウェイ接続を追加できます。    
  
次の表には、架空の 2 つのテナント用の例のサブネット Id およびプレフィックスが含まれています。 Contoso テナントがある 3 つの仮想サブネットのときに、テナント Fabrikam は 2 つの仮想サブネットがします。  
  
  
  
テナント名  |仮想サブネット ID  |仮想サブネットのプレフィックス    
---------|---------|---------  
Fabrikam    |5001         |24.30.1.0/24           
Fabrikam     |5002         | 24.30.2.0/20          
Contoso    |6001         |  24.30.1.0/24         
Contoso    | 6002        |  24.30.2.0/24         
Contoso     | 6003        | 24.30.3.0/24          
  
次のスクリプト例からエクスポートされた Windows PowerShell コマンドを使用して、 **NetworkController** Contoso の仮想ネットワークと 1 つのサブネットを作成するモジュール。   
  
```  
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
  
## <a name="modify-an-existing-virtual-network"></a>既存の仮想ネットワークを変更します。  
Windows PowerShell を使用して、既存の仮想サブネットまたはネットワークを更新することができます。   
  
次のスクリプト例を実行すると、更新されたリソースが同じリソース ID を持つネットワーク コント ローラーに簡単に言えば Contoso テナントが仮想ネットワークに新しい仮想サブネット (24.30.2.0/24) を追加しようとすると、ユーザーまたは Contoso 管理者は、次のスクリプトを使用できます。  
  
```  
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
  
## <a name="delete-a-virtual-network"></a>仮想ネットワークを削除します。  
  
Windows PowerShell を使用して、仮想ネットワークを削除することができます。  
  
次の Windows PowerShell の例は、HTTP delete をリソースのリソースの ID の URI に発行することによってテナント仮想ネットワークを削除します。  
  
    Remove-NetworkControllerVirtualNetwork -ResourceId "Contoso_Vnet1" -ConnectionUri $uri  


