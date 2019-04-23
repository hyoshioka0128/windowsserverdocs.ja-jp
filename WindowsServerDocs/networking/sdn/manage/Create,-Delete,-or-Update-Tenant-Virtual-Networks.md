---
title: 作成、削除、またはテナントの仮想ネットワークの更新
description: このトピックでは、作成、削除、およびソフトウェア定義ネットワーク (SDN) を展開した後、HYPER-V ネットワーク仮想化の仮想ネットワークを更新する方法について説明します。 HYPER-V ネットワーク仮想化では、各テナント ネットワークが個別のエンティティをあるように、テナント ネットワークを分離できます。 ワークロードのパブリック アクセスを構成しない限り、各エンティティは相互接続する可能性がありません。
manager: dougkim
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
ms.date: 08/24/2018
ms.openlocfilehash: a125ec220b4769a57a6be30f1425283afb7f0fe6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838353"
---
# <a name="create-delete-or-update-tenant-virtual-networks"></a>テナントの仮想ネットワークを作成、削除、または更新する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは、作成、削除、およびソフトウェア定義ネットワーク (SDN) を展開した後、HYPER-V ネットワーク仮想化の仮想ネットワークを更新する方法について説明します。 HYPER-V ネットワーク仮想化では、各テナント ネットワークが個別のエンティティをあるように、テナント ネットワークを分離できます。 ワークロードのパブリック アクセスを構成しない限り、各エンティティは相互接続する可能性がありません。   
  
## <a name="create-a-new-virtual-network"></a>新しい仮想ネットワークを作成します。  
テナントの仮想ネットワークを作成すると、HYPER-V ホスト上の一意のルーティング ドメイン内で配置します。 すべての仮想ネットワークでは、下にある少なくとも 1 つの仮想サブネットがあります。 仮想サブネットは、IP プレフィックスで定義を取得し、以前に定義された ACL を参照します。  

新しい仮想ネットワークを作成する手順は次のとおりです。

1. 仮想サブネットを作成する IP アドレスのプレフィックスを特定します。   
2. テナント トラフィックをトンネリングするプロバイダーの論理ネットワークを識別します。   
3. 手順 1. で特定した各 IP プレフィックスの少なくとも 1 つの仮想サブネットを作成します。 
4. (省略可能)仮想サブネットを以前に作成された Acl を追加するか、テナントのゲートウェイの接続を追加します。 

次の表には、架空の 2 つのテナント用の例のサブネット Id とプレフィックスが含まれます。 テナントの Fabrikam の 2 つの仮想サブネットでは、Contoso テナントがある 3 つの仮想サブネットです。  
 
  
テナント名  |仮想サブネット ID  |仮想サブネットのプレフィックス    
---------|---------|---------  
Fabrikam    |5001         |24.30.1.0/24           
Fabrikam     |5002         | 24.30.2.0/20          
Contoso    |6001         |  24.30.1.0/24         
Contoso    | 6002        |  24.30.2.0/24         
Contoso     | 6003        | 24.30.3.0/24          
  
次のスクリプト例からエクスポートされた Windows PowerShell コマンドを使用して、 **NetworkController** Contoso の仮想ネットワークと 1 つのサブネットを作成するモジュール。   
  
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
  
## <a name="modify-an-existing-virtual-network"></a>既存の仮想ネットワークを変更します。  
Windows PowerShell を使用して、既存の仮想サブネットまたはネットワークを更新することができます。   
  
次のサンプル スクリプトを実行すると更新リソースが同じリソース ID を持つネットワーク コント ローラーに簡単に言えば Contoso テナントの仮想ネットワークに新しい仮想サブネット (24.30.2.0/24) を追加する場合、または Contoso の管理者は、次のスクリプトを使用できます。  
  
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
  
## <a name="delete-a-virtual-network"></a>仮想ネットワークを削除します。  
  
Windows PowerShell を使用して、仮想ネットワークを削除することができます。  
  
次の Windows PowerShell の例では、リソースのリソース ID の URI に、HTTP delete を発行してテナント仮想ネットワークを削除します。  

```PowerShell  
Remove-NetworkControllerVirtualNetwork -ResourceId "Contoso_Vnet1" -ConnectionUri $uri  
```

