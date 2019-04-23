---
title: データセンターのファイアウォール アクセス制御リスト (ACL) を構成する
description: ネットワーク インターフェイスには、特定の Acl を適用できます。  Acl はネットワーク インターフェイスが接続されている仮想サブネットの設定も、Acl が適用されると、両方がネットワーク インターフェイスの Acl が仮想サブネット Acl より優先されます。
manager: dougkim
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 25f18927-a63e-44f3-b02a-81ed51933187
ms.author: pashort
author: shortpatti
ms.date: 08/23/2018
ms.openlocfilehash: 77a7706e39da265eedd65342a0ccf2174ab050ea
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853403"
---
# <a name="configure-datacenter-firewall-access-control-lists-acls"></a>データ センターのファイアウォール アクセス制御リスト (Acl) を構成します。

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

ACL を作成し、仮想サブネットに割り当てられていることとは、個々 のネットワーク インターフェイスの特定の ACL を使用して、仮想サブネットでその既定の ACL をオーバーライドすることができます。  この場合、仮想ネットワークではなく、Vlan に接続されたネットワーク インターフェイスに直接、特定の Acl を適用します。 ネットワーク インターフェイスに接続されている仮想サブネットに設定される Acl があれば、両方の Acl が適用され、ネットワーク インターフェイス上の仮想サブネットの Acl の Acl の優先順位を付けます。

>[!IMPORTANT]
>ACL を作成および仮想ネットワークに割り当てられていないが場合を参照してください。[使用へのアクセス制御リスト (Acl) を管理データ センター ネットワーク トラフィックのフローを](Use-Access-Control-Lists--ACLs--to-Manage-Datacenter-Network-Traffic-Flow.md)に ACL を作成し、仮想サブネットに割り当てます。  

このトピックで紹介するネットワーク インターフェイスに ACL を追加する方法。 紹介する Windows PowerShell とネットワーク コント ローラーの REST API を使用してネットワーク インターフェイスから ACL を削除する方法。

- [例:ネットワーク インターフェイスに ACL を追加します。](#example-add-an-acl-to-a-network-interface)
- [例:Windows Powershell とネットワーク コント ローラーの REST API を使用してネットワーク インターフェイスから ACL を削除します。](#example-remove-an-acl-from-a-network-interface-by-using-windows-powershell-and-the-network-controller-rest-api)


## <a name="example-add-an-acl-to-a-network-interface"></a>以下に例を示します。ネットワーク インターフェイスに ACL を追加します。
この例では、仮想ネットワークに ACL を追加する方法を示します。 

>[!TIP]
>ネットワーク インターフェイスを作成するのと同時に ACL を追加することもできます。

1. 取得するか、ACL を追加すると、ネットワーク インターフェイスを作成します。
 
   ```PowerShell
   $nic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "MyVM_Ethernet1"
   ```
 
2. 取得またはネットワーク インターフェイスを追加する ACL を作成します。
 
   ```PowerShell
   $acl = get-networkcontrolleraccesscontrollist -ConnectionUri $uri -resourceid "AllowAllACL"
   ```
 
3. ACL をネットワーク インターフェイスの AccessControlList プロパティに割り当てる
 
   ```PowerShell
    $nic.properties.ipconfigurations[0].properties.AccessControlList = $acl
   ```
 
4. ネットワーク コント ローラーにネットワーク インターフェイスを追加します。
 
   ```
   new-networkcontrollernetworkinterface -ConnectionUri $uri -Properties $nic.properties -ResourceId $nic.resourceid
   ```
 
## <a name="example-remove-an-acl-from-a-network-interface-by-using-windows-powershell-and-the-network-controller-rest-api"></a>以下に例を示します。Windows Powershell とネットワーク コント ローラーの REST API を使用してネットワーク インターフェイスから ACL を削除します。
この例で紹介する ACL を削除する方法。 ACL を削除すると、既定の規則セットが、ネットワーク インターフェイスに適用されます。 既定の規則セットはすべての送信トラフィックを許可しますが、すべての着信トラフィックをブロックします。

>[!NOTE]
>以前、従う必要があるすべての受信トラフィックを許可する場合は、[例](#example-add-an-acl-to-a-network-interface)にすべての受信と送信のすべてのトラフィックを許可する ACL を追加します。


1. ネットワーク インターフェイスを削除する ACL を取得します。<br>
   ```PowerShell
   $nic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "MyVM_Ethernet1"
   ```
 
2. $NULL を ip 構成の AccessControlList プロパティに割り当てます。<br>
   ```PowerShell
   $nic.properties.ipconfigurations[0].properties.AccessControlList = $null
   ```
 
3. ネットワーク コント ローラーで、ネットワーク インターフェイス オブジェクトを追加します。<br>
   ```PowerShell
   new-networkcontrollernetworkinterface -ConnectionUri $uri -Properties $nic.properties -ResourceId $nic.resourceid
   ```
