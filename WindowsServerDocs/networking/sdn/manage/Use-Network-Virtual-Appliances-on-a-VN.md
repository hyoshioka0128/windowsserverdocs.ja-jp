---
title: 仮想ネットワーク上でネットワーク仮想アプライアンスを使用する
description: このトピックでは、テナントの仮想ネットワークにネットワーク仮想アプライアンスを展開する方法について説明します。 ネットワーク仮想アプライアンスは、ユーザー定義のルーティング機能とポートミラーリング機能を実行するネットワークに追加できます。
manager: dougkim
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.prod: windows-server
ms.technology: networking-sdn
ms.assetid: 3c361575-1050-46f4-ac94-fa42102f83c1
ms.author: lizross
author: eross-msft
ms.date: 08/30/2018
ms.openlocfilehash: db634af114610cce0bdbcacd58986ceb5f00dd99
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80317586"
---
# <a name="use-network-virtual-appliances-on-a-virtual-network"></a>仮想ネットワーク上でネットワーク仮想アプライアンスを使用する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、テナントの仮想ネットワークにネットワーク仮想アプライアンスを展開する方法について説明します。 ネットワーク仮想アプライアンスは、ユーザー定義のルーティング機能とポートミラーリング機能を実行するネットワークに追加できます。

## <a name="types-of-network-virtual-appliances"></a>ネットワーク仮想アプライアンスの種類

次の2種類の仮想アプライアンスのいずれかを使用できます。

1. **ユーザー定義のルーティング**-仮想ネットワーク上の分散ルーターを仮想アプライアンスのルーティング機能に置き換えます。  ユーザー定義ルーティングを使用すると、仮想アプライアンスは仮想ネットワーク上の仮想サブネット間のルーターとして使用されます。

2. **ポートミラーリング**-監視対象のポートを出入りするすべてのネットワークトラフィックが複製され、分析のために仮想アプライアンスに送信されます。 


## <a name="deploying-a-network-virtual-appliance"></a>ネットワーク仮想アプライアンスを展開する

ネットワーク仮想アプライアンスをデプロイするには、まずアプライアンスを含む VM を作成してから、VM を適切な仮想ネットワークサブネットに接続する必要があります。 詳細については、「[テナント VM の作成とテナント Virtual Network または VLAN への接続](Create-a-Tenant-VM.md)」を参照してください。

アプライアンスによっては、複数の仮想ネットワークアダプターが必要になる場合があります。 通常、1つのネットワークアダプターはアプライアンス管理専用で、追加のアダプターはトラフィックを処理します。  アプライアンスに複数のネットワークアダプターが必要な場合は、ネットワークコントローラーで各ネットワークインターフェイスを作成する必要があります。 また、異なる仮想サブネット上にある追加のアダプターごとに、各ホストでインターフェイス ID を割り当てる必要があります。

ネットワーク仮想アプライアンスをデプロイしたら、アプライアンスを使用して、定義済みのルーティング、ミラーリングの移植、またはその両方を行うことができます。 


## <a name="example-user-defined-routing"></a>例: ユーザー定義ルーティング

ほとんどの環境では、仮想ネットワークの分散ルーターによって既に定義されているシステムルートのみが必要です。 ただし、次のように、ルーティングテーブルを作成し、特定のケースで1つ以上のルートを追加することが必要になる場合があります。

- オンプレミスネットワーク経由でインターネットへのトンネリングを強制します。
- 環境内での仮想アプライアンスの使用。

これらのシナリオでは、ルーティングテーブルを作成し、ユーザー定義のルートをテーブルに追加する必要があります。 複数のルーティングテーブルを持つことができ、同じルーティングテーブルを1つまたは複数のサブネットに関連付けることができます。 各サブネットは1つのルーティングテーブルにのみ関連付けることができます。 サブネット内のすべての Vm は、サブネットに関連付けられているルーティングテーブルを使用します。

サブネットは、ルーティングテーブルがサブネットに関連付けられるまで、システムルートに依存します。 関連付けが存在すると、ユーザー定義のルートとシステムルートの両方で最長プレフィックス一致 (LPM) に基づいてルーティングが実行されます。 同じ LPM 一致のルートが複数ある場合は、システムルートの前にユーザー定義ルートが最初に選択されます。
 
**作業**

1. すべてのユーザー定義ルートを含むルートテーブルのプロパティを作成します。<p>システムルートは、上記で定義した規則に従って適用されます。

   ```PowerShell
    $routetableproperties = new-object Microsoft.Windows.NetworkController.RouteTableProperties
   ```

2. ルーティングテーブルのプロパティにルートを追加します。<p>12.0.0.0/8 サブネット宛てのルートは、192.168.1.10 で仮想アプライアンスにルーティングされます。 アプライアンスには、仮想ネットワークに接続された仮想ネットワークアダプターがあり、その IP アドレスがネットワークインターフェイスに割り当てられている必要があります。

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
   >ルートをさらに追加する場合は、定義する各ルートに対してこの手順を繰り返します。

3. ネットワークコントローラーにルーティングテーブルを追加します。

   ```PowerShell
    $routetable = New-NetworkControllerRouteTable -ConnectionUri $uri -ResourceId "Route1" -Properties $routetableproperties
   ```

4. 仮想サブネットにルーティングテーブルを適用します。<p>ルートテーブルを仮想サブネットに適用すると、Tenant1_Vnet1 ネットワークの最初の仮想サブネットがルートテーブルを使用します。 必要に応じて、仮想ネットワーク内のサブネットの数にルートテーブルを割り当てることができます。

   ```PowerShell
    $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Tenant1_VNet1"
    $vnet.properties.subnets[0].properties.RouteTable = $routetable
    new-networkcontrollervirtualnetwork -connectionuri $uri -properties $vnet.properties -resourceId $vnet.resourceid
   ```

仮想ネットワークにルーティングテーブルを適用するとすぐに、トラフィックは仮想アプライアンスに転送されます。 環境に適した方法で、トラフィックを転送するように仮想アプライアンス内のルーティングテーブルを構成する必要があります。

## <a name="example-port-mirroring"></a>例: ポートミラーリング

この例では、Appliance_Ethernet1 をミラー化する MyVM_Ethernet1 のトラフィックを構成します。  2つの Vm をデプロイしているとします。1つはアプライアンス、もう1つはミラーリングで監視する VM です。 

アプライアンスは、管理のための2番目のネットワークインターフェイスを備えている必要があります。 Appliciance_Ethernet1 でターゲットとしてミラーリングを有効にした後は、そこで構成された IP インターフェイス宛てのトラフィックを受信しなくなります。


**作業**

1. Vm が配置されている仮想ネットワークを取得します。

   ```PowerShell
   $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Tenant1_VNet1"
   ```

2. ミラーリングのソースとターゲットのネットワークコントローラーのネットワークインターフェイスを取得します。

   ```PowerShell
   $dstNic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "Appliance_Ethernet1"
   $srcNic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "MyVM_Ethernet1"
   ```

3. ポートミラーリングルールと、宛先インターフェイスを表す要素を格納するために、serviceて tionproperties オブジェクトを作成します。

   ```PowerShell
   $portmirror = [Microsoft.Windows.NetworkController.ServiceInsertionProperties]::new()
   $portMirror.Priority = 1
   ```

4. トラフィックをアプライアンスに送信するために照合する必要があるルールを格納するために、serviceの、ルールオブジェクトを作成します。<p>以下で定義されている規則は、従来のミラーを表す受信と送信の両方のトラフィックに一致します。  特定のポートまたは特定の送信元/送信先をミラーリングする場合は、これらのルールを調整できます。

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

5. ミラー化されたアプライアンスのネットワークインターフェイスを格納するために、serviceます tionelements オブジェクトを作成します。

   ```PowerShell
   $portmirror.ServiceInsertionElements = [Microsoft.Windows.NetworkController.ServiceInsertionElement[]]::new(1)

   $portmirror.ServiceInsertionElements[0] = [Microsoft.Windows.NetworkController.ServiceInsertionElement]::new()
   $portmirror.ServiceInsertionElements[0].ResourceId = "Element1"
   $portmirror.ServiceInsertionElements[0].Properties = [Microsoft.Windows.NetworkController.ServiceInsertionElementProperties]::new()

   $portmirror.ServiceInsertionElements[0].Properties.Description = "Port Mirror Element"
   $portmirror.ServiceInsertionElements[0].Properties.NetworkInterface = $dstNic
   $portmirror.ServiceInsertionElements[0].Properties.Order = 1
   ```

6. ネットワークコントローラーにサービス挿入オブジェクトを追加します。<p>このコマンドを実行すると、前の手順で指定したアプライアンスネットワークインターフェイスへのすべてのトラフィックが停止します。

   ```PowerShell
   $portMirror = New-NetworkControllerServiceInsertion -ConnectionUri $uri -Properties $portmirror -ResourceId "MirrorAll"
   ```

7. ミラー化するソースのネットワークインターフェイスを更新します。

   ```PowerShell
   $srcNic.Properties.IpConfigurations[0].Properties.ServiceInsertion = $portMirror
   $srcNic = New-NetworkControllerNetworkInterface -ConnectionUri $uri  -Properties $srcNic.Properties -ResourceId $srcNic.ResourceId
   ```

これらの手順を完了すると、Appliance_Ethernet1 インターフェイスは MyVM_Ethernet1 インターフェイスからのトラフィックをミラー化します。
 
---