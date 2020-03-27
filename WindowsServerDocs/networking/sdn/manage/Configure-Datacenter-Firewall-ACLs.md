---
title: データセンターのファイアウォール アクセス制御リスト (ACL) を構成する
description: 特定の Acl をネットワークインターフェイスに適用できます。  ネットワークインターフェイスが接続されている仮想サブネット上で Acl も設定されている場合、両方の Acl が適用されますが、ネットワークインターフェイスの Acl は仮想サブネット Acl の上位に優先されます。
manager: dougkim
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 25f18927-a63e-44f3-b02a-81ed51933187
ms.author: lizross
author: eross-msft
ms.date: 08/23/2018
ms.openlocfilehash: fdf9f7dbe8fb9541cc8f77cfbce014c5210296d5
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80317664"
---
# <a name="configure-datacenter-firewall-access-control-lists-acls"></a>データセンターのファイアウォール Access Control リスト (Acl) の構成

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

ACL を作成して仮想サブネットに割り当てたら、仮想サブネット上の既定の ACL を個々のネットワークインターフェイス用に特定の ACL で上書きすることができます。  この場合は、仮想ネットワークではなく、Vlan に接続されているネットワークインターフェイスに特定の Acl を直接適用します。 ネットワークインターフェイスに接続された仮想サブネットに Acl が設定されている場合、両方の Acl が適用され、仮想サブネット Acl の上にネットワークインターフェイス Acl が優先されます。

>[!IMPORTANT]
>ACL を作成して仮想ネットワークに割り当てていない場合は、「 [Access Control リスト (acl) を使用してデータセンターのネットワークトラフィックフローを管理](Use-Access-Control-Lists--ACLs--to-Manage-Datacenter-Network-Traffic-Flow.md)し、acl を作成して仮想サブネットに割り当てる」を参照してください。  

このトピックでは、ネットワークインターフェイスに ACL を追加する方法について説明します。 また、Windows PowerShell とネットワークコントローラー REST API を使用してネットワークインターフェイスから ACL を削除する方法についても説明します。

- [例: ネットワークインターフェイスに ACL を追加する](#example-add-an-acl-to-a-network-interface)
- [例: Windows Powershell とネットワークコントローラーを使用してネットワークインターフェイスから ACL を削除する REST API](#example-remove-an-acl-from-a-network-interface-by-using-windows-powershell-and-the-network-controller-rest-api)


## <a name="example-add-an-acl-to-a-network-interface"></a>例: ネットワークインターフェイスに ACL を追加する
この例では、仮想ネットワークに ACL を追加する方法について説明します。 

>[!TIP]
>また、ネットワークインターフェイスを作成するときに ACL を追加することもできます。

1. ACL を追加するネットワークインターフェイスを取得または作成します。
 
   ```PowerShell
   $nic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "MyVM_Ethernet1"
   ```
 
2. ネットワークインターフェイスに追加する ACL を取得または作成します。
 
   ```PowerShell
   $acl = get-networkcontrolleraccesscontrollist -ConnectionUri $uri -resourceid "AllowAllACL"
   ```
 
3. ネットワークインターフェイスの AccessControlList プロパティに ACL を割り当てます。
 
   ```PowerShell
    $nic.properties.ipconfigurations[0].properties.AccessControlList = $acl
   ```
 
4. ネットワークコントローラーにネットワークインターフェイスを追加する
 
   ```
   new-networkcontrollernetworkinterface -ConnectionUri $uri -Properties $nic.properties -ResourceId $nic.resourceid
   ```
 
## <a name="example-remove-an-acl-from-a-network-interface-by-using-windows-powershell-and-the-network-controller-rest-api"></a>例: Windows Powershell とネットワークコントローラーを使用してネットワークインターフェイスから ACL を削除する REST API
この例では、ACL を削除する方法について説明します。 ACL を削除すると、既定のルールセットがネットワークインターフェイスに適用されます。 既定のルールセットは、すべての送信トラフィックを許可しますが、すべての受信トラフィックをブロックします。

>[!NOTE]
>すべての受信トラフィックを許可する場合は、前の[例](#example-add-an-acl-to-a-network-interface)に従って、すべての受信トラフィックとすべての送信トラフィックを許可する ACL を追加する必要があります。


1. ACL を削除するネットワークインターフェイスを取得します。<br>
   ```PowerShell
   $nic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "MyVM_Ethernet1"
   ```
 
2. Ip 構成の AccessControlList プロパティに $NULL を割り当てます。<br>
   ```PowerShell
   $nic.properties.ipconfigurations[0].properties.AccessControlList = $null
   ```
 
3. ネットワークコントローラーにネットワークインターフェイスオブジェクトを追加します。<br>
   ```PowerShell
   new-networkcontrollernetworkinterface -ConnectionUri $uri -Properties $nic.properties -ResourceId $nic.resourceid
   ```
