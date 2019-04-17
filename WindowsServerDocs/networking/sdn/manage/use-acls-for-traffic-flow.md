---
title: アクセス制御リスト (Acl) を使用して、データ センター ネットワーク トラフィック フローを管理するには
description: このトピックでは、テナント ワークロードを管理および Windows Server 2016 での仮想ネットワークに方法について、ソフトウェア定義ネットワーク ガイドの一部です。
manager: brianlic
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
ms.openlocfilehash: 64b7e1abf1ddb8132a8c6692fe82521c589f32df
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="use-access-control-lists-acls-to-manage-datacenter-network-traffic-flow"></a>アクセス制御リスト (Acl) を使用して、データ センター ネットワーク トラフィック フローを管理するには

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、データ センターのファイアウォールと Acl を使用して、仮想サブネット上のデータ トラフィック フローを管理するのにアクセス制御リストを構成するのに方法について説明します。  
  
有効にして、仮想サブネットまたはネットワーク インターフェイスに適用される Acl を作成することでデータ センターのファイアウォールを構成することができます。  
  
次の例では、Windows PowerShell を使用して、これらの Acl を作成する方法を示します。  
  
## <a name="configure-datacenter-firewall-to-allow-all-traffic"></a>すべてのトラフィックを許可するように、データ センターのファイアウォールを構成します。  
  
SDN を展開した後、新しい環境では、基本的なネットワーク接続をテストすることをお勧めします。  
  
これを行うには、制限なしのすべてのネットワーク トラフィックを許可するデータ センターのファイアウォールの規則を作成できます。   
  
次の表に、エントリを使用すると、すべての受信と送信ネットワーク トラフィックを許可する規則のセットを作成します。  
  
  
  
IP のソース|宛先 IP|プロトコル|発信元ポート|宛先ポート|方向|アクション|優先順位   
---------|---------|---------|---------|---------|---------|---------|---------  
*    |   *      |   すべての      |    *     |      *   |     受信    |   許可します。      |   100        
*    |     *    |     すべての    |     *    |     *    |   送信      |  許可します。       |  110         
  
  
このスクリプト例では、次の 2 つのルールが含まれる ACL を作成します。    
- "AllowAll_Inbound"の最初のルールは、この ACL が構成されているネットワーク インターフェイスに渡すときにすべてのネットワーク トラフィックを許可します。    
- 第 2 の規則では、"AllowAllOutbound"に渡すネットワーク インターフェイスからすべてのトラフィックを許可します。  
この ACL は、「すべて許可が次 1」リソース id によって識別されるは、仮想サブネットとのネットワーク インターフェイスで使用する準備ができました。  
  
次のスクリプト例からエクスポートされた Windows PowerShell コマンドを使用して、 **NetworkController**モジュールをこの ACL を作成します。  
  
  
```  
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
>ネットワーク コント ローラーの Windows PowerShell コマンド リファレンス」トピックの「ある[ネットワーク コント ローラー コマンドレット](https://technet.microsoft.com/library/mt576401.aspx)します。  
  
## <a name="use-acls-to-limit-traffic-on-a-subnet"></a>Acl を使用して、サブネット上のトラフィックを制限するには  
  
この例は、相互に通信してから、192.168.0.0/24 サブネット内を仮想マシン (Vm) を妨げる ACL を作成するのに使用できます。   
  
この種類の ACL は、サブネットの外部からの要求を受信するだけでなく他のサブネット上の他のサービスと通信するために Vm 許可しながら、サブネット内でを横方向に拡散するため、攻撃者の機能を制限するのに便利です。  
  
  
IP のソース|宛先 IP|プロトコル|発信元ポート|宛先ポート|方向|アクション|優先順位   
---------|---------|---------|---------|---------|---------|---------|---------  
192.168.0.1    | * | すべての | * | * | 受信|   許可します。      |   100        
* |192.168.0.1 | すべての | * | * | 送信|  許可します。       |  101         
192.168.0.0/24 | * | すべての | * | * | 受信| ブロック | 102  
* | 192.168.0.0/24 |すべての| * | * | 送信 | ブロック |103  
* | *  |すべての| * | * | 受信 | 許可します。 |104  
* | *  |すべての| * | * | 送信 | 許可します。 |105  
  
ACL が以下の例のスクリプトによって作成されたリソース id によって識別される**サブネット-192-168-0-0**、「192.168.0.0/24」サブネット アドレスを使用する仮想ネットワーク サブネットに適用できるようになりました。  自動的にその仮想ネットワーク サブネットに接続されている任意のネットワーク インターフェイスでは、上記に適用される ACL 規則を取得します。  
  
Windows Powershell コマンドを使用して、ネットワーク コント ローラー REST API を使用してこの ACL を作成するスクリプトの例を次に示します。  
  
```  
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
  
