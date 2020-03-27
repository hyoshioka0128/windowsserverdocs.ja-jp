---
title: アクセス制御リスト (Acl) を使用してデータセンターのネットワークトラフィックフローを管理する
description: このトピックでは、データセンターのファイアウォールと仮想サブネットの Acl を使用して、データトラフィックフローを管理するためのアクセス制御リスト (Acl) を構成する方法について説明します。 データセンターのファイアウォールを有効にして構成するには、仮想サブネットまたはネットワークインターフェイスに適用される Acl を作成します。
manager: dougkim
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6a7ac5af-85e9-4440-a631-6a3a38e9015d
ms.author: lizross
author: eross-msft
ms.date: 08/27/2018
ms.openlocfilehash: 1f18ad9ddb0ea1a7575f6fcb26189f36f818ada2
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80317484"
---
# <a name="use-access-control-lists-acls-to-manage-datacenter-network-traffic-flow"></a>アクセス制御リスト (Acl) を使用してデータセンターのネットワークトラフィックフローを管理する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、データセンターのファイアウォールと仮想サブネットの Acl を使用して、データトラフィックフローを管理するためのアクセス制御リスト (Acl) を構成する方法について説明します。 データセンターのファイアウォールを有効にして構成するには、仮想サブネットまたはネットワークインターフェイスに適用される Acl を作成します。   

このトピックの次の例では、Windows PowerShell を使用してこれらの Acl を作成する方法を示します。  

## <a name="configure-datacenter-firewall-to-allow-all-traffic"></a>すべてのトラフィックを許可するようにデータセンターのファイアウォールを構成する  

SDN をデプロイしたら、新しい環境で基本的なネットワーク接続をテストする必要があります。  これを実現するには、制限なしですべてのネットワークトラフィックを許可するデータセンターのファイアウォールの規則を作成します。   

次の表のエントリを使用して、すべての受信および送信ネットワークトラフィックを許可する規則のセットを作成します。


| Source IP | 宛先 IP | [プロトコル] | Source Port | 宛先ポート | Direction | 操作 | 優先順位 |
|:---------:|:--------------:|:--------:|:-----------:|:----------------:|:---------:|:------:|:--------:|
|    \*     |       \*       |   [すべて]    |     \*      |        \*        |  受信  | 許可  |   100    |
|    \*     |       \*       |   [すべて]    |     \*      |        \*        | 送信  | 許可  |   110    |

---       

### <a name="example-create-an-acl"></a>例: ACL の作成 
この例では、次の2つの規則を持つ ACL を作成します。

1. **AllowAll_Inbound** -この ACL が構成されているネットワークインターフェイスにすべてのネットワークトラフィックが渡されることを許可します。    
2. **Allowalloutbound** -すべてのトラフィックがネットワークインターフェイスから渡されることを許可します。 リソース id "AllowAll-1" によって識別されたこの ACL は、仮想サブネットとネットワークインターフェイスで使用できるようになりました。  

次のスクリプト例では、 **NetworkController**モジュールからエクスポートされた Windows PowerShell コマンドを使用して、この ACL を作成します。  


```PowerShell
$ruleproperties = new-object Microsoft.Windows.NetworkController.AclRuleProperties  
$ruleproperties.Protocol = "All"  
$ruleproperties.SourcePortRange = "0-65535"  
$ruleproperties.DestinationPortRange = "0-65535"  
$ruleproperties.Action = "Allow"  
$ruleproperties.SourceAddressPrefix = "*"  
$ruleproperties.DestinationAddressPrefix = "*"  
$ruleproperties.Priority = "100"  
$ruleproperties.Type = "Inbound"  
$ruleproperties.Logging = "Enabled"  
$aclrule1 = new-object Microsoft.Windows.NetworkController.AclRule  
$aclrule1.Properties = $ruleproperties  
$aclrule1.ResourceId = "AllowAll_Inbound"  
$ruleproperties = new-object Microsoft.Windows.NetworkController.AclRuleProperties  
$ruleproperties.Protocol = "All"  
$ruleproperties.SourcePortRange = "0-65535"  
$ruleproperties.DestinationPortRange = "0-65535"  
$ruleproperties.Action = "Allow"  
$ruleproperties.SourceAddressPrefix = "*"  
$ruleproperties.DestinationAddressPrefix = "*"  
$ruleproperties.Priority = "110"  
$ruleproperties.Type = "Outbound"  
$ruleproperties.Logging = "Enabled"  
$aclrule2 = new-object Microsoft.Windows.NetworkController.AclRule  
$aclrule2.Properties = $ruleproperties  
$aclrule2.ResourceId = "AllowAll_Outbound"  
$acllistproperties = new-object Microsoft.Windows.NetworkController.AccessControlListProperties  
$acllistproperties.AclRules = @($aclrule1, $aclrule2)  
New-NetworkControllerAccessControlList -ResourceId "AllowAll" -Properties $acllistproperties -ConnectionUri <NC REST FQDN>  
```  

>[!NOTE]  
>ネットワークコントローラーの Windows PowerShell コマンドリファレンスについては、「[ネットワークコントローラー](https://technet.microsoft.com/library/mt576401.aspx)のコマンドレット」を参照してください。  

## <a name="use-acls-to-limit-traffic-on-a-subnet"></a>Acl を使用してサブネット上のトラフィックを制限する  
この例では、192.168.0.0/24 サブネット内の Vm が相互に通信できないようにする ACL を作成します。 この種類の ACL は、攻撃者がサブネット内で奪取を分散する能力を制限するために役立ちます。一方、Vm がサブネットの外部からの要求を受信したり、他のサブネット上の他のサービスと通信したりすることができます。   


|   Source IP    | 宛先 IP | [プロトコル] | Source Port | 宛先ポート | Direction | 操作 | 優先順位 |
|:--------------:|:--------------:|:--------:|:-----------:|:----------------:|:---------:|:------:|:--------:|
|  192.168.0.1   |       \*       |   [すべて]    |     \*      |        \*        |  受信  | 許可  |   100    |
|       \*       |  192.168.0.1   |   [すべて]    |     \*      |        \*        | 送信  | 許可  |   101    |
| 192.168.0.0/24 |       \*       |   [すべて]    |     \*      |        \*        |  受信  | [ブロック]  |   102    |
|       \*       | 192.168.0.0/24 |   [すべて]    |     \*      |        \*        | 送信  | [ブロック]  |   103    |
|       \*       |       \*       |   [すべて]    |     \*      |        \*        |  受信  | 許可  |   104    |
|       \*       |       \*       |   [すべて]    |     \*      |        \*        | 送信  | 許可  |   105    |

--- 

次のサンプルスクリプトによって作成された ACL (リソース id**サブネット-192-168-0-0**によって識別される) は、"192.168.0.0/24" サブネットアドレスを使用する仮想ネットワークサブネットに適用できるようになりました。  その仮想ネットワークサブネットに接続されているすべてのネットワークインターフェイスが、上記の ACL 規則を自動的に適用します。  

次に示すのは、Windows Powershell コマンドを使用して、ネットワークコントローラー REST API を使用してこの ACL を作成するスクリプトの例です。  

```PowerShell  
import-module networkcontroller  
$ncURI = "https://mync.contoso.local"  
$aclrules = @()  

$ruleproperties = new-object Microsoft.Windows.NetworkController.AclRuleProperties  
$ruleproperties.Protocol = "All"  
$ruleproperties.SourcePortRange = "0-65535"  
$ruleproperties.DestinationPortRange = "0-65535"  
$ruleproperties.Action = "Allow"  
$ruleproperties.SourceAddressPrefix = "192.168.0.1"  
$ruleproperties.DestinationAddressPrefix = "*"  
$ruleproperties.Priority = "100"  
$ruleproperties.Type = "Inbound"  
$ruleproperties.Logging = "Enabled"  

$aclrule = new-object Microsoft.Windows.NetworkController.AclRule  
$aclrule.Properties = $ruleproperties  
$aclrule.ResourceId = "AllowRouter_Inbound"  
$aclrules += $aclrule  

$ruleproperties = new-object Microsoft.Windows.NetworkController.AclRuleProperties  
$ruleproperties.Protocol = "All"  
$ruleproperties.SourcePortRange = "0-65535"  
$ruleproperties.DestinationPortRange = "0-65535"  
$ruleproperties.Action = "Allow"  
$ruleproperties.SourceAddressPrefix = "*"  
$ruleproperties.DestinationAddressPrefix = "192.168.0.1"  
$ruleproperties.Priority = "101"  
$ruleproperties.Type = "Outbound"  
$ruleproperties.Logging = "Enabled"  

$aclrule = new-object Microsoft.Windows.NetworkController.AclRule  
$aclrule.Properties = $ruleproperties  
$aclrule.ResourceId = "AllowRouter_Outbound"  
$aclrules += $aclrule  

$ruleproperties = new-object Microsoft.Windows.NetworkController.AclRuleProperties  
$ruleproperties.Protocol = "All"  
$ruleproperties.SourcePortRange = "0-65535"  
$ruleproperties.DestinationPortRange = "0-65535"  
$ruleproperties.Action = "Deny"  
$ruleproperties.SourceAddressPrefix = "192.168.0.0/24"  
$ruleproperties.DestinationAddressPrefix = "*"  
$ruleproperties.Priority = "102"  
$ruleproperties.Type = "Inbound"  
$ruleproperties.Logging = "Enabled"  

$aclrule = new-object Microsoft.Windows.NetworkController.AclRule  
$aclrule.Properties = $ruleproperties  
$aclrule.ResourceId = "DenySubnet_Inbound"  
$aclrules += $aclrule  

$ruleproperties = new-object Microsoft.Windows.NetworkController.AclRuleProperties  
$ruleproperties.Protocol = "All"  
$ruleproperties.SourcePortRange = "0-65535"  
$ruleproperties.DestinationPortRange = "0-65535"  
$ruleproperties.Action = "Deny"  
$ruleproperties.SourceAddressPrefix = "*"  
$ruleproperties.DestinationAddressPrefix = "192.168.0.0/24"  
$ruleproperties.Priority = "103"  
$ruleproperties.Type = "Outbound"  
$ruleproperties.Logging = "Enabled"  

$aclrule = new-object Microsoft.Windows.NetworkController.AclRule  
$aclrule.Properties = $ruleproperties  
$aclrule.ResourceId = "DenySubnet_Outbound"  

$ruleproperties = new-object Microsoft.Windows.NetworkController.AclRuleProperties  
$ruleproperties.Protocol = "All"  
$ruleproperties.SourcePortRange = "0-65535"  
$ruleproperties.DestinationPortRange = "0-65535"  
$ruleproperties.Action = "Allow"  
$ruleproperties.SourceAddressPrefix = "*"  
$ruleproperties.DestinationAddressPrefix = "*"  
$ruleproperties.Priority = "104"  
$ruleproperties.Type = "Inbound"  
$ruleproperties.Logging = "Enabled"  

$aclrule = new-object Microsoft.Windows.NetworkController.AclRule  
$aclrule.Properties = $ruleproperties  
$aclrule.ResourceId = "AllowAll_Inbound"  
$aclrules += $aclrule  

$ruleproperties = new-object Microsoft.Windows.NetworkController.AclRuleProperties  
$ruleproperties.Protocol = "All"  
$ruleproperties.SourcePortRange = "0-65535"  
$ruleproperties.DestinationPortRange = "0-65535"  
$ruleproperties.Action = "Allow"  
$ruleproperties.SourceAddressPrefix = "*"  
$ruleproperties.DestinationAddressPrefix = "*"  
$ruleproperties.Priority = "105"  
$ruleproperties.Type = "Outbound"  
$ruleproperties.Logging = "Enabled"  

$aclrule = new-object Microsoft.Windows.NetworkController.AclRule  
$aclrule.Properties = $ruleproperties  
$aclrule.ResourceId = "AllowAll_Outbound"  
$aclrules += $aclrule  

$acllistproperties = new-object Microsoft.Windows.NetworkController.AccessControlListProperties  
$acllistproperties.AclRules = $aclrules  

New-NetworkControllerAccessControlList -ResourceId "Subnet-192-168-0-0" -Properties $acllistproperties -ConnectionUri $ncURI   
```  

