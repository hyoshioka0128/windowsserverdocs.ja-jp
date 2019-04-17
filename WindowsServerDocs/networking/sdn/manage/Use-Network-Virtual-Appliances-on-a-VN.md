---
title: 仮想ネットワーク上のネットワーク仮想アプライアンスを使用します。
description: このトピックでは、テナント ワークロードを管理および Windows Server 2016 での仮想ネットワークに方法について、ソフトウェア定義ネットワーク ガイドの一部です。
manager: brianlic
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.assetid: 3c361575-1050-46f4-ac94-fa42102f83c1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: db46189931263d230f013431f319eb2497589dee
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="use-network-virtual-appliances-on-a-virtual-network"></a>仮想ネットワーク上のネットワーク仮想アプライアンスを使用します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、テナントの仮想ネットワーク上のネットワーク仮想アプライアンスを展開するのに方法について説明します。

ネットワーク仮想アプライアンスは、ユーザー定義のルーティングとポート ミラーリングの機能を実行するネットワークを追加できます。

このトピックには、次のセクションが含まれています。

- [ネットワーク仮想アプライアンスの種類](#bkmk_types)
- [ネットワークの仮想アプライアンスを展開します。](#bkmk_deploy)
- [例: ユーザー定義のルーティング](#bkmk_routing)
- [例: ポート ミラーリング](#bkmk_port)

## <a name="bkmk_types"></a>ネットワーク仮想アプライアンスの種類

仮想ネットワーク上の仮想アプライアンスの 2 つの種類があります。

1. **ユーザー定義のルーティング**します。 ユーザー定義のルーティングすると、仮想ネットワーク上の分散ルーターを仮想アプライアンスのルーティング機能に置き換えます。  ユーザー定義のルーティング、仮想アプライアンスは、仮想ネットワーク上の仮想サブネット間のルーターとして使用されます。
2. **ポート ミラーリング**します。 ポート ミラーリングを入力するか、監視対象のポートを退出するすべてのネットワーク トラフィックが重複してし、分析のための仮想アプライアンスに送信します。 
## <a name="bkmk_deploy"></a>ネットワークの仮想アプライアンスを展開します。

仮想アプライアンスを展開するには、まず、アプライアンスを含む仮想マシン (VM) を作成し、適切な仮想ネットワークのサブネットに VM を接続する必要があります。

>[!NOTE]
>詳細については、次を参照してください[テナント VM とテナントの仮想ネットワークまたは VLAN に接続を作成します。](Create-a-Tenant-VM.md)

一部のアプライアンスは、複数の仮想ネットワーク アダプターが必要です。 その他のアダプターがトラフィックを処理するために使用するときに通常 1 つのネットワーク アダプターを専用アプライアンス管理にします。 

アプライアンスは、複数のネットワーク アダプターを必要とする場合、ネットワーク コント ローラーの各ネットワーク インターフェイスを作成します。 

各ホストの異なる仮想サブネット上にあるその他のアダプターのインターフェイス ID を割り当てる必要があります。

ネットワーク仮想アプライアンスの展開を完了すると、ユーザー定義のルーティング、ポート ミラーリング、またはその両方のアプライアンスを使用できます。

##<a name="bkmk_routing"></a>例: ユーザー定義のルーティング

ほとんどの環境は、仮想ネットワークの分散ルーターによって既に定義されているシステム ルートのみ必要があります。 ただし、ルーティング テーブルを作成しなど、場合によっては、1 つまたは複数のルートを追加する必要があります。

* 強制トンネリング、オンプレミス ネットワーク経由でインターネットにします。
* 環境内で仮想アプライアンスを使用します。

これらのシナリオについては、ルート テーブルを作成し、ユーザー定義のルートをテーブルに追加する必要があります。 複数のルーティング テーブルをあり、同じルート テーブルが 1 つまたは複数のサブネットに関連付けることができます。 

各サブネットは単一のルーティング テーブルに関連付けられている場合のみできます。 サブネット内のすべての Vm では、そのサブネットに関連付けられているルーティング テーブルを使用します。

サブネットは、ルーティング テーブルがサブネットに関連付けられるまで、システムのルートに依存します。 アソシエーションが存在した後のルーティングがの最長プレフィックス一致 (ほか) ユーザー定義のルートとルートのシステムの両方の間でに基づいて行われます。 

同じほかと一致する複数のルートがある場合、ユーザー定義されているルートが最初に選択 - システム ルートする前にします。 

###<a name="step-1-create-the-route-table-properties"></a>手順 1: は、ルートのテーブルのプロパティを作成します。

このルート テーブルは、すべてのユーザー定義のルートが含まれます。  システム ルートは、上記で定義した規則に従って引き続き適用されます。

次の例のコマンドを使用して、ルーティング テーブルのプロパティを作成することができます。

    $routetableproperties = new-object Microsoft.Windows.NetworkController.RouteTableProperties

###<a name="step-2-add-a-route-to-the-route-table-properties"></a>手順 2: は、ルーティング テーブルのプロパティにルートを追加します。

このルートという 12.0.0.0/8 サブネットに送信されるすべてのトラフィックを送信を取得する必要があることをルーティングする 192.168.1.10 で仮想アプライアンスします。  アプライアンスがその ip アドレスのネットワーク インターフェイスに割り当てられている仮想ネットワークに接続されている仮想ネットワーク アダプターを持つことが重要です。

次の例のコマンドを使用すると、ルーティング テーブルのプロパティにルートを追加します。

    $route = new-object Microsoft.Windows.NetworkController.Route
    $route.ResourceID = "0_0_0_0_0"
    $route.properties = new-object Microsoft.Windows.NetworkController.RouteProperties
    $route.properties.AddressPrefix = "0.0.0.0/0"
    $route.properties.nextHopType = "VirtualAppliance"
    $route.properties.nextHopIpAddress = "192.168.1.10"
    $routetableproperties.routes += $route

追加のルートを追加するには、定義する各ルートにこの手順を繰り返します。
s
###<a name="step-3-add-the-route-table-to-network-controller"></a>手順 3: ネットワーク コント ローラーにルーティング テーブルを追加します。
次の例のコマンドを使用すると、ネットワーク コント ローラーにルーティング テーブルを追加します。

    $routetable = New-NetworkControllerRouteTable -ConnectionUri $uri -ResourceId "Route1" -Properties $routetableproperties

###<a name="step-4-apply-the-route-table-to-the-virtual-subnet"></a>手順 4: 仮想サブネットをルーティング テーブルを適用します。
 
仮想サブネットをルーティング テーブルを適用すると、Tenant1_Vnet1 ネットワーク内の最初の仮想サブネットは、ルーティング テーブルを使用します。 必要に応じて、仮想ネットワークのサブネットのルートの表を割り当てることができます。

次の例のコマンドを使用して、仮想サブネットをルーティング テーブルを適用することができます。

    $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Tenant1_VNet1"
    $vnet.properties.subnets[0].properties.RouteTable = $routetable
    new-networkcontrollervirtualnetwork -connectionuri $uri -properties $vnet.properties -resourceId $vnet.resourceid

仮想ネットワークにルーティング テーブルを適用するとすぐに仮想アプライアンスにトラフィックが転送されます。 環境に適した方法で、トラフィックを転送するように、仮想アプライアンスで、ルーティング テーブルを構成する必要があります。

##<a name="bkmk_port"></a>例: ポート ミラーリング

この例では、トラフィックが Appliance_Ethernet1 にミラー化できるように、MyVM_Ethernet1 のトラフィックを構成することができます。

この例では、アプライアンスとして 1 つ、ミラーリングを使用して監視するために VM としてもう 1 つの 2 つの Vm が既に展開されていることを前提としています。

アプライアンスが管理のための 2 つ目のネットワーク インターフェイスが構成されている IP インターフェイスのトラフィックが受信は不要になった Appliance_Ethernet1 上の宛先としてミラーリングを有効にすると、ために重要です。

###<a name="step-1-get-the-virtual-network-on-which-your-vms-are-located"></a>手順 1: Vm がある仮想ネットワークを取得します。
次のコマンド例を使用して、仮想ネットワークを取得することができます。

    $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Tenant1_VNet1"

###<a name="step-2-get-the-network-controller-network-interfaces-for-the-mirroring-source-and-destination"></a>手順 2: ミラーリングのソースとターゲットのネットワーク コント ローラーのネットワーク インターフェイスを取得します。
次の例のコマンドを使用すると、ソースと宛先のミラーリングのネットワーク コント ローラーのネットワーク インターフェイスを取得します。

    $dstNic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "Appliance_Ethernet1"
    $srcNic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "MyVM_Ethernet1"

###<a name="step-3-create-a-serviceinsertionproperties-object-to-contain-the-port-mirroring-rules-and-the-element-which-represents-the-destination-interface"></a>手順 3: ポート ミラーリング規則と、移行先のインターフェイスを表す要素が含まれている serviceinsertionproperties オブジェクトを作成します。
次の例のコマンドを使用すると、移行先 serviceinsertionproperties オブジェクトを作成します。

    $portmirror = [Microsoft.Windows.NetworkController.ServiceInsertionProperties]::new()
    $portMirror.Priority = 1

###<a name="step-4-create-a-serviceinsertionrules-object-to-contain-the-rules-that-must-be-matched-in-order-for-the-traffic-to-be-sent-to-the-appliance"></a>手順 4: アプライアンスに送信されるトラフィックのために一致する必要があるルールが含まれている serviceinsertionrules オブジェクトを作成します。

すべてのトラフィックを受信と送信、従来のミラーを表す、マッチの下の規則が定義されます。  ミラーリングを特定のポートまたは特定のソース/宛先に興味がある場合は、これらのルールを調整できます。

次の例のコマンドを使用して、serviceinsertionproperties オブジェクトを作成することができます。

    $portmirror.ServiceInsertionRules = [Microsoft.Windows.NetworkController.ServiceInsertionRule[]]::new(1)

    $portmirror.ServiceInsertionRules[0] = [Microsoft.Windows.NetworkController.ServiceInsertionRule]::new()
    $portmirror.ServiceInsertionRules[0].ResourceId = "Rule1"
    $portmirror.ServiceInsertionRules[0].Properties = [Microsoft.Windows.NetworkController.ServiceInsertionRuleProperties]::new()

    $portmirror.ServiceInsertionRules[0].Properties.Description = "Port Mirror Rule"
    $portmirror.ServiceInsertionRules[0].Properties.Protocol = "All"
    $portmirror.ServiceInsertionRules[0].Properties.SourcePortRangeStart = "0"
    $portmirror.ServiceInsertionRules[0].Properties.SourcePortRangeEnd = "65535"
    $portmirror.ServiceInsertionRules[0].Properties.DestinationPortRangeStart = "0"
    $portmirror.ServiceInsertionRules[0].Properties.DestinationPortRangeEnd = "65535"
    $portmirror.ServiceInsertionRules[0].Properties.SourceSubnets = "*"
    $portmirror.ServiceInsertionRules[0].Properties.DestinationSubnets = "*"

###<a name="step-5-create-a-serviceinsertionelements-object-to-contain-the-network-interface-of-the-appliance-you-are-mirroring-to"></a>手順 5: は、ミラーリングをアプライアンスのネットワーク インターフェイスが含まれている serviceinsertionelements オブジェクトを作成します。
次の例のコマンドを使用して、ネットワーク インターフェイス serviceinsertionelements オブジェクトを作成することができます。

    $portmirror.ServiceInsertionElements = [Microsoft.Windows.NetworkController.ServiceInsertionElement[]]::new(1)

    $portmirror.ServiceInsertionElements[0] = [Microsoft.Windows.NetworkController.ServiceInsertionElement]::new()
    $portmirror.ServiceInsertionElements[0].ResourceId = "Element1"
    $portmirror.ServiceInsertionElements[0].Properties = [Microsoft.Windows.NetworkController.ServiceInsertionElementProperties]::new()

    $portmirror.ServiceInsertionElements[0].Properties.Description = "Port Mirror Element"
    $portmirror.ServiceInsertionElements[0].Properties.NetworkInterface = $dstNic
    $portmirror.ServiceInsertionElements[0].Properties.Order = 1

###<a name="step-6-add-the-service-insertion-object-in-network-controller"></a>手順 6: ネットワーク コント ローラーで、サービスの挿入オブジェクトを追加します。
このコマンドを発行したときに、前の手順で指定されたアプライアンス ネットワーク インターフェイスにすべてのトラフィックは停止します。

次の例のコマンドを使用して、ネットワーク コント ローラーで、サービスの挿入オブジェクトを追加することができます。

    $portMirror = New-NetworkControllerServiceInsertion -ConnectionUri $uri -Properties $portmirror -ResourceId "MirrorAll"

###<a name="step-7-update-the-network-interface-of-the-source-to-be-mirrored"></a>手順 7: 左右反転するソースのネットワーク インターフェイスを更新します。
次の例のコマンドを使用して、ネットワーク インターフェイスを更新することができます。

    $srcNic.Properties.IpConfigurations[0].Properties.ServiceInsertion = $portMirror
    $srcNic = New-NetworkControllerNetworkInterface -ConnectionUri $uri  -Properties $srcNic.Properties -ResourceId $srcNic.ResourceId

次の手順を完了すると、MyVM_Ethernet1 インターフェイスからのトラフィックは Appliance_Ethernet1 インターフェイスでミラー化されています。
 
