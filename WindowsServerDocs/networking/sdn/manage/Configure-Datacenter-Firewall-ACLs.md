---
title: データ センターのファイアウォール アクセス制御リスト (Acl) を構成します。
description: このトピックでは、テナント ワークロードを管理および Windows Server 2016 での仮想ネットワークに方法について、ソフトウェア定義ネットワーク ガイドの一部です。
manager: brianlic
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
ms.openlocfilehash: d5f7c4baad24a720e073857cb6c835167e5b419b
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="configure-datacenter-firewall-access-control-lists-acls"></a>データ センターのファイアウォール アクセス制御リスト (Acl) を構成します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

ネットワーク インターフェイスには、特定の Acl を適用できます。  Acl は、ネットワーク インターフェイスが接続されている仮想サブネットで設定されても、Acl が適用されると、両方が仮想サブネット Acl の上、ネットワーク インターフェイスの Acl が優先します。

このトピックには、次のセクションが含まれています。

- [例: ネットワーク インターフェイスに ACL を追加します。](#bkmk_addacl)
- [例: Windows Powershell とネットワーク コント ローラー REST API を使用して、ネットワーク インターフェイスから ACL を削除します。](#bkmk_removeacl)

##<a name="bkmk_addacl"></a>例: ネットワーク インターフェイスに ACL を追加します。

トピックの「[使用アクセス制御リスト (Acl) の管理データ センター ネットワーク トラフィック フローを](Use-Access-Control-Lists--ACLs--to-Manage-Datacenter-Network-Traffic-Flow.md)ACL を作成すると、仮想サブネットに割り当てる方法を説明しました。  場合によっては、ただし、する場合があります virtaul のサブネットの個々 のネットワーク インターフェイスの特定の ACL ではその既定 ACL を上書きします。  仮想ネットワークではなく、Vlan に接続されているネットワーク インターフェイスに直接 Acl を適用する必要があります。

この例では、仮想ネットワークに ACL を追加する方法を示します。 

>[!NOTE]
>ネットワーク インターフェイスを作成するのと同時に ACL を追加することもできます。

###<a name="step-1-get-or-create-the-network-interface-to-which-you-will-add-the-acl"></a>手順 1: 取得または ACL を追加するネットワーク インターフェイスを作成します。

    $nic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "MyVM_Ethernet1"

###<a name="step-2-get-or-create-the-acl-you-will-add-to-the-network-interface"></a>手順 2: 取得またはネットワーク インターフェイスに追加する ACL を作成します。
次のコマンド例を使用して、取得または ACL を作成することができます。 

    $acl = get-networkcontrolleraccesscontrollist -ConnectionUri $uri -resourceid "AllowAllACL"

###<a name="step-3-assign-the-acl-to-the-accesscontrollist-property-of-the-network-interface"></a>手順 3: は、ネットワーク インターフェイスの AccessControlList プロパティに ACL を割り当てる
次のコマンド例を使用して、ACL を AccessControlList プロパティに割り当てることができます。

    $nic.properties.ipconfigurations[0].properties.AccessControlList = $acl

###<a name="step-4-add-the-network-interface-in-network-controller"></a>手順 4: ネットワーク コント ローラーで、ネットワーク インターフェイスを追加します。
次のコマンド例を使用して、ネットワーク コント ローラーで、ネットワーク インターフェイスを追加することができます。

    new-networkcontrollernetworkinterface -ConnectionUri $uri -Properties $nic.properties -ResourceId $nic.resourceid


##<a name="bkmk_removeacl"></a>例: Windows Powershell とネットワーク コント ローラー REST API を使用して、ネットワーク インターフェイスから ACL を削除します。
ACL を削除する場合は、次の例を使用できます。 ACL を削除すると、既定の規則のセットは、ネットワーク インターフェイスに適用されます。

既定の規則のセットはにより、すべての送信トラフィックですが、すべての着信トラフィックをブロックします。

>[!NOTE]
>すべての受信トラフィックを許可する場合は、すべての受信と送信のすべてのトラフィックを許可する ACL を追加する前の例に従ってください。

###<a name="step-1-get-the-network-interface-from-which-you-will-remove-the-acl"></a>手順 1: は、ACL を削除するが、ネットワーク インターフェイスを取得します。
次のコマンド例を使用すると、ネットワーク インターフェイスを取得します。

    $nic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "MyVM_Ethernet1"

###<a name="step-2-assign-null-to-the-accesscontrollist-property-of-the-ipconfiguration"></a>手順 2: は、ip 構成の AccessControlList プロパティに $NULL を割り当てる
次のコマンド例を使用して、$NULL を AccessControlList プロパティに割り当てることができます。

    $nic.properties.ipconfigurations[0].properties.AccessControlList = $null

###<a name="step-3-add-the-network-interface-object-in-network-controller"></a>手順 3: ネットワーク コント ローラーでネットワーク インターフェイスのオブジェクトを追加します。
次のコマンド例を使用するには、ネットワーク コント ローラーでネットワーク インターフェイスのオブジェクトを追加するには

    new-networkcontrollernetworkinterface -ConnectionUri $uri -Properties $nic.properties -ResourceId $nic.resourceid

