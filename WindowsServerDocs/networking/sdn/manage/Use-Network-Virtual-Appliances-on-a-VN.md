---
title: 仮想ネットワーク上でネットワーク仮想アプライアンスを使用する
description: このトピックでは、テナントの仮想ネットワークでネットワーク仮想アプライアンスをデプロイする方法について説明します。 ユーザー定義ルーティングし、ポート ミラーリングの関数を実行するネットワークには、ネットワーク仮想アプライアンスを追加できます。
manager: dougkim
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
ms.date: 08/30/2018
ms.openlocfilehash: e715a782651a5b9867f3b45251fd6ea6e4a9e4f7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847373"
---
# <a name="use-network-virtual-appliances-on-a-virtual-network"></a>仮想ネットワーク上でネットワーク仮想アプライアンスを使用する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは、テナントの仮想ネットワークでネットワーク仮想アプライアンスをデプロイする方法について説明します。 ユーザー定義ルーティングし、ポート ミラーリングの関数を実行するネットワークには、ネットワーク仮想アプライアンスを追加できます。

## <a name="types-of-network-virtual-appliances"></a>ネットワーク仮想アプライアンスの種類

仮想アプライアンスの 2 種類のいずれかを使用できます。

1. **ユーザー定義ルーティング**-仮想ネットワーク上の分散ルーターを仮想アプライアンスのルーティングの機能に置き換えます。  ユーザー定義ルーティングが、仮想アプライアンスに、仮想ネットワーク上の仮想サブネット間のルーターとして使用されます。

2. **ポート ミラーリング**すべてのネットワークに入るトラフィック - または監視対象のポートを離れることは複製や分析のための仮想アプライアンスに送信します。 


## <a name="deploying-a-network-virtual-appliance"></a>ネットワーク仮想アプライアンスを展開します。

ネットワーク仮想アプライアンスをデプロイするには、まず、アプライアンスを含む VM を作成し、適切な仮想ネットワーク サブネットに VM を接続する必要があります。 詳細については、次を参照してください。[テナント VM とテナントの仮想ネットワークまたは VLAN への接続を作成](Create-a-Tenant-VM.md)です。

いくつかのアプライアンスには、複数の仮想ネットワーク アダプターが必要です。 1 つのネットワーク アダプターは通常が追加のアダプターは、トラフィックを処理している間には、アプライアンスの管理専用です。  アプライアンスは、複数のネットワーク アダプターを必要とする場合は、ネットワーク コント ローラーで各ネットワーク インターフェイスを作成する必要があります。 各ホストの別の仮想サブネット上にある追加のアダプターのインターフェイス ID を割り当てる必要があります。

ネットワーク仮想アプライアンスをデプロイすると、定義されたルーティング、移植ミラーリング、またはその両方のアプライアンスを使用できます。 


## <a name="example-user-defined-routing"></a>以下に例を示します。ユーザー定義のルーティング

ほとんどの環境、仮想ネットワークの分散ルーターによって既に定義されているシステム ルートだけでかまいません。 ただし、ルーティング テーブルを作成しなどの特定の場合、1 つまたは複数のルートを追加する必要があります。

- オンプレミス ネットワークを介したインターネットへのトンネリングを強制します。
- 環境内の仮想アプライアンスを使用します。

これらのシナリオについては、ルーティング テーブルを作成し、テーブルにユーザー定義ルートを追加する必要があります。 複数のルーティング テーブルがあることができ、同じルーティング テーブルを 1 つまたは複数のサブネットに関連付けることができます。 各サブネット 1 つのルーティング テーブルにのみ関連付けることができます。 サブネット内のすべての Vm は、サブネットに関連付けられているルーティング テーブルを使用します。

サブネットは、ルーティング テーブルをサブネットに関連付けられている取得されるまで、システム ルートに依存します。 アソシエーションが存在する後に基づいてルーティングが実行に最長プレフィックス一致 (LPM) 間でユーザー定義ルートとシステム ルート。 同じ LPM マッチの複数のルートがある場合、ユーザー定義のルートが選択されて最初のシステム ルートの前にします。
 
**手順:**

1. ルートを作成、テーブルのプロパティをすべてのユーザー定義ルートが含まれています。<p>システム ルートは、引き続き、上記で定義された規則に従って適用されます。

   ```PowerShell
    $routetableproperties = new-object Microsoft.Windows.NetworkController.RouteTableProperties
   ```

2. ルーティング テーブルのプロパティには、ルートを追加します。<p>12.0.0.0/8 サブネット宛てのルートは 192.168.1.10 で仮想アプライアンスにルーティングされます。 アプライアンスには、仮想ネットワーク アダプターがその ip アドレスのネットワーク インターフェイスに割り当てられている仮想ネットワークに接続されている必要があります。

   ```PowerShell
    $route = new-object Microsoft.Windows.NetworkController.Route
    $route.ResourceID = "0_0_0_0_0"
    $route.properties = new-object Microsoft.Windows.NetworkController.RouteProperties
    $route.properties.AddressPrefix = "0.0.0.0/0"
    $route.properties.nextHopType = "VirtualAppliance"
    $route.properties.nextHopIpAddress = "192.168.1.10"
    $routetableproperties.routes += $route
   ```
   >[!TIP]
   >複数のルートを追加する場合は、各ルートを定義するこの手順を繰り返します。

3. ネットワーク コント ローラーにルーティング テーブルを追加します。

   ```PowerShell
    $routetable = New-NetworkControllerRouteTable -ConnectionUri $uri -ResourceId "Route1" -Properties $routetableproperties
   ```

4. 仮想サブネットにルーティング テーブルを適用します。<p>仮想サブネットにルート テーブルを適用すると、Tenant1_Vnet1 ネットワーク内の最初の仮想サブネットは、ルート テーブルを使用します。 必要に応じて、多くの仮想ネットワーク内のサブネットにルート テーブルを割り当てることができます。

   ```PowerShell
    $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Tenant1_VNet1"
    $vnet.properties.subnets[0].properties.RouteTable = $routetable
    new-networkcontrollervirtualnetwork -connectionuri $uri -properties $vnet.properties -resourceId $vnet.resourceid
   ```

仮想ネットワークにルーティング テーブルを適用するとすぐには、トラフィックが仮想アプライアンスに転送を取得します。 環境に適した方法で、トラフィックを転送するように仮想アプライアンスでは、ルーティング テーブルを構成する必要があります。

## <a name="example-port-mirroring"></a>以下に例を示します。ポート ミラーリング

この例ではミラー Appliance_Ethernet1 に MyVM_Ethernet1 のトラフィックを構成します。  として、アプライアンス、ミラーリングを監視する VM ともう 1 つ、2 つの Vm をデプロイしたと想定しています。 

アプライアンスには、管理用の 2 つ目のネットワーク インターフェイスが必要です。 Appliciance_Ethernet1 上の宛先としてミラーリングを有効にした後に構成されている IP インターフェイスのトラフィックを受信しません。


**手順:**

1. Vm が配置されている仮想ネットワークを取得します。

   ```PowerShell
   $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Tenant1_VNet1"
   ```

2. ミラーリングのソースとターゲットのネットワーク コント ローラーのネットワーク インターフェイスを取得します。

   ```PowerShell
   $dstNic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "Appliance_Ethernet1"
   $srcNic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "MyVM_Ethernet1"
   ```

3. ポート ミラーリングのルールと変換先のインターフェイスを表す要素を含む serviceinsertionproperties オブジェクトを作成します。

   ```PowerShell
   $portmirror = [Microsoft.Windows.NetworkController.ServiceInsertionProperties]::new()
   $portMirror.Priority = 1
   ```

4. アプライアンスに送信されるトラフィックの順序に従う必要があるルールが含まれる serviceinsertionrules オブジェクトを作成します。<p>ルールは、一致の下のすべてのトラフィックを受信および送信の両方を表す従来のミラーを定義します。  特定のポートまたは送信元/送信先の特定のミラーリングに関心がある場合は、これらのルールを調整できます。

   ```PowerShell
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
   ```

5. ミラー化されたアプライアンスのネットワーク インターフェイスを格納する serviceinsertionelements オブジェクトを作成します。

   ```PowerShell
   $portmirror.ServiceInsertionElements = [Microsoft.Windows.NetworkController.ServiceInsertionElement[]]::new(1)

   $portmirror.ServiceInsertionElements[0] = [Microsoft.Windows.NetworkController.ServiceInsertionElement]::new()
   $portmirror.ServiceInsertionElements[0].ResourceId = "Element1"
   $portmirror.ServiceInsertionElements[0].Properties = [Microsoft.Windows.NetworkController.ServiceInsertionElementProperties]::new()

   $portmirror.ServiceInsertionElements[0].Properties.Description = "Port Mirror Element"
   $portmirror.ServiceInsertionElements[0].Properties.NetworkInterface = $dstNic
   $portmirror.ServiceInsertionElements[0].Properties.Order = 1
   ```

6. ネットワーク コント ローラーで、サービスの挿入オブジェクトを追加します。<p>このコマンドを発行するときに、前の手順の終了位置の指定されたインターフェイスがネットワーク アプライアンスにすべてのトラフィック。

   ```PowerShell
   $portMirror = New-NetworkControllerServiceInsertion -ConnectionUri $uri -Properties $portmirror -ResourceId "MirrorAll"
   ```

7. ミラー化するソースのネットワーク インターフェイスを更新します。

   ```PowerShell
   $srcNic.Properties.IpConfigurations[0].Properties.ServiceInsertion = $portMirror
   $srcNic = New-NetworkControllerNetworkInterface -ConnectionUri $uri  -Properties $srcNic.Properties -ResourceId $srcNic.ResourceId
   ```

次の手順を完了すると、Appliance_Ethernet1 インターフェイスには、MyVM_Ethernet1 インターフェイスからのトラフィックがミラー化します。
 
---