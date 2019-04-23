---
title: アクセス制御リスト (Acl) をデータ センターのネットワーク トラフィック フローを管理するには
description: このトピックでは、アクセス制御リスト (Acl) をデータ センターのファイアウォールおよび Acl の仮想サブネットを使用したデータのトラフィック フローの管理を構成する方法について説明します。 有効にし、仮想サブネットまたはネットワーク インターフェイスに適用される Acl を作成してデータ センターのファイアウォールを構成します。
manager: dougkim
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6a7ac5af-85e9-4440-a631-6a3a38e9015d
ms.author: pashort
author: shortpatti
ms.date: 08/27/2018
ms.openlocfilehash: 1364261f7ab1e732ac77b7c90d49c245aa8cbc25
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861423"
---
# <a name="use-access-control-lists-acls-to-manage-datacenter-network-traffic-flow"></a>アクセス制御リスト (Acl) をデータ センターのネットワーク トラフィック フローを管理するには

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは、アクセス制御リスト (Acl) をデータ センターのファイアウォールおよび Acl の仮想サブネットを使用したデータのトラフィック フローの管理を構成する方法について説明します。 有効にし、仮想サブネットまたはネットワーク インターフェイスに適用される Acl を作成してデータ センターのファイアウォールを構成します。   
  
このトピックの次の例では、Windows PowerShell を使用して、これらの Acl を作成する方法を示します。  
  
## <a name="configure-datacenter-firewall-to-allow-all-traffic"></a>すべてのトラフィックを許可するデータ センターのファイアウォールを構成します。  
  
SDN を展開すると、新しい環境で基本的なネットワーク接続をテストする必要があります。  これを実現するには、制限なくすべてのネットワーク トラフィックを許可するデータ センターのファイアウォールのルールを作成します。   
  
次の表に、エントリを使用して、すべての受信および送信ネットワーク トラフィックを許可する規則のセットを作成します。
  
|Source IP|宛先 IP|プロトコル|Source Port|宛先ポート|Direction|アクション|Priority |   
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|*    |   *      |   すべての      |    *     |      *   |     受信    |   許可      |   100  |      
|*    |     *    |     すべての    |     *    |     *    |   送信      |  許可       |  110  |
---       
  
### <a name="example-create-an-acl"></a>以下に例を示します。ACL を作成します。 
この例では、2 つの規則を ACL を作成します。
  
1. **AllowAll_Inbound** -この ACL が構成されているネットワーク インターフェイスに渡すすべてのネットワーク トラフィックを許可します。    
2. **AllowAllOutbound** -ネットワーク インターフェイスの外部に渡すへのすべてのトラフィックを許可します。 リソース id「AllowAll 1」で識別される、この ACL は、仮想サブネットとネットワーク インターフェイスで使用する準備ができました。  
  
次のスクリプト例からエクスポートされた Windows PowerShell コマンドを使用して、 **NetworkController**モジュールをこの ACL を作成します。  
  
  
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
>ネットワーク コント ローラー用の Windows PowerShell コマンド リファレンスは、トピックにある[ネットワーク コント ローラー コマンドレット](https://technet.microsoft.com/library/mt576401.aspx)します。  
  
## <a name="use-acls-to-limit-traffic-on-a-subnet"></a>Acl を使用して、サブネット上のトラフィックを制限するには  
この例では、192.168.0.0/24 サブネット内で互いと通信するから Vm を防止する ACL を作成します。 この種類の ACL は、サブネットの外部からの要求を受信するだけでなく他のサブネット上の他のサービスと通信するために Vm を許可する一方、サブネット内で横断的に分散する、攻撃者の能力を制限するために便利です。   
  
  
|Source IP|宛先 IP|プロトコル|Source Port|宛先ポート|Direction|アクション|Priority |  
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|  
|192.168.0.1    | * | すべての | * | * | 受信|   許可      |   100        |
|* |192.168.0.1 | すべての | * | * | 送信|  許可       |  101         |
|192.168.0.0/24 | * | すべての | * | * | 受信| ブロック | 102  |
|* | 192.168.0.0/24 |すべての| * | * | 送信 | ブロック |103  |
|* | *  |すべての| * | * | 受信 | 許可 |104  |
|* | *  |すべての| * | * | 送信 | 許可 |105  |
--- 

ACL が以下の例のスクリプトによって作成されたリソース id で識別される**サブネット-192-168-0-0**、「192.168.0.0/24」サブネットのアドレスを使用する仮想ネットワーク サブネットに適用できるようになりました。  自動的にその仮想ネットワーク サブネットに関連付けられているすべてのネットワーク インターフェイスは、適用される上記の ACL ルールを取得します。  
  
Windows Powershell コマンドを使用して、ネットワーク コント ローラーの REST API を使用してこの ACL を作成するスクリプトの例を次に示します。  
  
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
  
