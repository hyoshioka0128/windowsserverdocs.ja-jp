---
title: 仮想ネットワークの使用状況測定の送信
description: クラウド ネットワークの収益化の基本的な側面では、ネットワーク帯域幅のエグレスです。 たとえば、送信データは、Microsoft Azure でビジネス モデルを転送します。 送信データは、特定の請求サイクルで、インターネット経由での Azure データ センターから移動するデータの合計量に基づいて課金されます。
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: ''
ms.author: pashort
author: shortpatti
ms.date: 10/02/2018
ms.openlocfilehash: ad1bed11308420e271b8e06410d5a4548181314a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59876423"
---
# <a name="egress-metering-in-a-virtual-network"></a>仮想ネットワークの使用状況測定の送信

>適用対象:Windows Server 2019


クラウド ネットワークの収益化の基本的な側面は、ネットワーク帯域幅の使用率別の請求にできることです。 送信データは、特定の請求サイクルで、インターネット経由で、データ センターから移動するデータの合計量に基づいて課金されます。

Windows Server 2019 の SDN ネットワーク トラフィックの使用状況測定エグレス送信データ転送の使用状況メーターを提供する機能を使用できます。 データ センター内に維持されますが、各仮想ネットワークがネットワーク トラフィックを追跡できますとは別にため、これは、課金の計算から除外できます。 送信データ転送の請求と未請求のアドレス範囲のいずれかに含まれていない宛先 IP アドレスにバインドされているパケットが追跡されます。

## <a name="virtual-network-unbilled-address-ranges-whitelist-of-ip-ranges"></a>未請求の仮想ネットワークのアドレス範囲 (範囲の IP のホワイト リストに登録)

未請求のアドレス範囲を見つけることができます、 **UnbilledAddressRanges**既存の仮想ネットワークのプロパティ。 既定では、追加のアドレス範囲はありません。

   ```PowerShell
   import-module NetworkController
   $uri = "https://sdn.contoso.com"

   (Get-NetworkControllerVirtualNetwork -ConnectionURI $URI -ResourceId "VNet1").properties
   ```

出力は次のようになります。
   ```
    AddressSpace           : Microsoft.Windows.NetworkController.AddressSpace
    DhcpOptions            :
    UnbilledAddressRanges  :
    ConfigurationState     :
    ProvisioningState      : Succeeded
    Subnets                : {21e71701-9f59-4ee5-b798-2a9d8c2762f0, 5f4758ef-9f96-40ca-a389-35c414e996cc,
                         29fe67b8-6f7b-486c-973b-8b9b987ec8b3}
    VirtualNetworkPeerings :
    EncryptionCredential   :
    LogicalNetwork         : Microsoft.Windows.NetworkController.LogicalNetwork
   ```


## <a name="example-manage-the-unbilled-address-ranges-of-a-virtual-network"></a>以下に例を示します。仮想ネットワークの未請求のアドレス範囲を管理します

設定して使用状況測定エグレスの課金対象から除外する IP サブネット プレフィックスのセットを管理することができます、 **UnbilledAddressRange**仮想ネットワークのプロパティ。  プレフィックスのいずれかに一致する宛先 IP アドレスで仮想ネットワーク上のネットワーク インターフェイスによって送信されたすべてのトラフィックを BilledEgressBytes プロパティに含まれていません。

1.  更新プログラム、 **UnbilledAddressRanges**プロパティにアクセスするためには課金されませんサブネットが含まれています。

    ```PowerShell
    $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceID "VNet1"
    $vnet.Properties.UnbilledAddressRanges = "10.10.2.0/24,10.10.3.0/24"
    ```
    
    >[!TIP]
    >複数の IP サブネットを追加する場合は、各 IP サブネットの間にコンマを使用します。  コンマの前後にスペースを含めないでください。

2.  変更した仮想ネットワーク リソースの更新**UnbilledAddressRanges**プロパティ。

    ```PowerShell
    New-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "VNet1" -Properties $unbilled.Properties -PassInnerException
    ```

    出力は次のようになります。
    ```
    Confirm
    Performing the operation 'New-NetworkControllerVirtualNetwork' on entities of type
    'Microsoft.Windows.NetworkController.VirtualNetwork' via
    'https://sdn.contoso.com/networking/v3/virtualNetworks/VNet1'. Are you sure you want to continue?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
    
    
    Tags             :
    ResourceRef      : /virtualNetworks/VNet1
    InstanceId       : 29654b0b-9091-4bed-ab01-e172225dc02d
    Etag             : W/"6970d0a3-3444-41d7-bbe4-36327968d853"
    ResourceMetadata :
    ResourceId       : VNet1
    Properties       : Microsoft.Windows.NetworkController.VirtualNetworkProperties
    ```


3.  仮想ネットワークを構成済みの確認**UnbilledAddressRanges**します。

    ```PowerShell
    (Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceID "VNet1").properties
    ```

    出力は次のようになります。
    ```
    AddressSpace           : Microsoft.Windows.NetworkController.AddressSpace
    DhcpOptions            :
    UnbilledAddressRanges  : 10.10.2.0/24,192.168.2.0/24
    ConfigurationState     :
    ProvisioningState      : Succeeded
    Subnets                : {21e71701-9f59-4ee5-b798-2a9d8c2762f0, 5f4758ef-9f96-40ca-a389-35c414e996cc,
                         29fe67b8-6f7b-486c-973b-8b9b987ec8b3}
    VirtualNetworkPeerings :
    EncryptionCredential   :
    LogicalNetwork         : Microsoft.Windows.NetworkController.LogicalNetwork
    ```

## <a name="check-the-billed-the-unbilled-egress-usage-of-a-virtual-network"></a>確認料金請求が発生、仮想ネットワークのエグレス未請求の使用状況

構成した後、 **UnbilledAddressRanges**プロパティ、仮想ネットワーク内の各サブネットのエグレスの課金と未請求の使用状況を確認することができます。 エグレス トラフィックは、4 つ分に 1 で、課金と未請求の範囲の合計バイト数を更新します。

各仮想サブネットに使用できるは、次のプロパティです。

-   **UnbilledEgressBytes**をこの仮想サブネットに接続されているネットワーク インターフェイスから送信された未請求のバイト数が表示されます。 未請求のバイトが含まれているアドレスの範囲に送信バイト、 **UnbilledAddressRanges**親仮想ネットワークのプロパティ。

-   **BilledEgressBytes**をこの仮想サブネットに接続されているネットワーク インターフェイスによって送信される課金対象のバイト数が表示されます。 課金対象のバイトはないアドレス範囲に送信されたバイトの一部、 **UnbilledAddressRanges**親仮想ネットワークのプロパティ。

クエリの送信の使用状況を次の例を使用します。

```PowerShell
(Get-NetworkControllerVirtualNetwork -ConnectionURI $URI -ResourceId "VNet1").properties.subnets.properties | ft AddressPrefix,BilledEgressBytes,UnbilledEgressBytes
```

出力は次のようになります。
```
AddressPrefix BilledEgressBytes UnbilledEgressBytes
------------- ----------------- -------------------
10.0.255.8/29          16827067                   0
10.0.2.0/24           781733019                   0
10.0.4.0/24                   0                   0
```
    

---