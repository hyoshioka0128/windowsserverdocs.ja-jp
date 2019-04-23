---
title: Windows Server 2019 ゲートウェイのパフォーマンス
description: ''
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: ''
ms.author: pashort
author: shortpatti
ms.date: 08/22/2018
ms.openlocfilehash: a6530b29ce7ffb0d18e0266e70cb2ca45188915c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845633"
---
# <a name="windows-server-2019-gateway-performance"></a>Windows Server 2019 ゲートウェイのパフォーマンス

>適用対象:Windows Server


Windows Server 2016 では、SDN ゲートウェイの近代的なネットワークのスループット要件を満たすことができないお客様の懸念事項の 1 つでした。 IPsec と GRE トンネルのネットワーク スループットが約 300 Mbps をされている IPsec 接続を約 2.5 Gbps をされている GRE 接続の 1 つの接続のスループットで制限されていました。

改善しました。 大幅に Windows Server の 2019 で 1.8 Gbps、IPsec と GRE 接続では、15 Gbps をそれぞれソアリング番号を持つ。 すべてこれを 1 バイト、CPU 使用率がはるかに少ない極めて高パフォーマンスのスループットを高める]、[CPU サイクルを大幅に削減します。

## <a name="enable-high-performance-with-gateways-in-windows-server-2019"></a>Windows Server 2019 でゲートウェイを使用した高パフォーマンスを有効にします。

**GRE 接続**とするデプロイ/アップグレード ゲートウェイ Vm で Windows Server 2019 ビルドをパフォーマンスの向上を自動的に表示する必要があります。 手動の手順は必要ありません。

**IPsec 接続**既定では、仮想ネットワークの接続を作成するときに取得する Windows Server 2016 データのパスとパフォーマンスの数値。 Windows Server 2019 のデータ パスを有効にするには、次の操作を行います。

   1. SDN ゲートウェイ VM では、上に移動**サービス**コンソール (services.msc)。
   2. という名前のサービスを検索**Azure ゲートウェイ サービス**、スタートアップの種類を設定および**自動**します。
   3. ゲートウェイ VM を再起動します。
      このゲートウェイにフェールオーバーする冗長ゲートウェイ VM でのアクティブな接続。
   4. ゲートウェイ Vm の残りの部分には、前の手順を繰り返します。

>[!TIP]
>最適なパフォーマンスの結果、いることを確認、cipherTransformationConstant と IPsec 接続の使用方法のクイック モードの設定で authenticationTransformConstant、 **GCMAES256**暗号スイート。
>
>パフォーマンスを最大にするには、ゲートウェイのホスト ハードウェアは AES NI と PCLMULQDQ CPU 命令セットをサポートする必要があります。 これらはすべて Westmere (32nm) および AES NI が無効にされているモデルを除く以降の Intel CPU で使用可能です。 CPU に AES NI と PCLMULQDQ CPU の命令がサポートされているかどうかは、ハードウェア ベンダーのドキュメントを見ることができますを設定します。

最適なセキュリティ アルゴリズムとの IPsec 接続の REST のサンプルを次に示します。

```PowerShell
# NOTE: The virtual gateway must be created before creating the IPsec connection. More details here.
# Create a new object for Tenant Network IPsec Connection  
$nwConnectionProperties = New-Object Microsoft.Windows.NetworkController.NetworkConnectionProperties   

# Update the common object properties  
$nwConnectionProperties.ConnectionType = "IPSec"   
$nwConnectionProperties.OutboundKiloBitsPerSecond = 2000000   
$nwConnectionProperties.InboundKiloBitsPerSecond = 2000000  

# Update specific properties depending on the Connection Type  
$nwConnectionProperties.IpSecConfiguration = New-Object Microsoft.Windows.NetworkController.IpSecConfiguration   
$nwConnectionProperties.IpSecConfiguration.AuthenticationMethod = "PSK"   
$nwConnectionProperties.IpSecConfiguration.SharedSecret = "111_aaa"   

$nwConnectionProperties.IpSecConfiguration.QuickMode = New-Object Microsoft.Windows.NetworkController.QuickMode   
$nwConnectionProperties.IpSecConfiguration.QuickMode.PerfectForwardSecrecy = "PFS2048"   
$nwConnectionProperties.IpSecConfiguration.QuickMode.AuthenticationTransformationConstant = "GCMAES256"   
$nwConnectionProperties.IpSecConfiguration.QuickMode.CipherTransformationConstant = "GCMAES256"   
$nwConnectionProperties.IpSecConfiguration.QuickMode.SALifeTimeSeconds = 3600   
$nwConnectionProperties.IpSecConfiguration.QuickMode.IdleDisconnectSeconds = 500   
$nwConnectionProperties.IpSecConfiguration.QuickMode.SALifeTimeKiloBytes = 2000   

$nwConnectionProperties.IpSecConfiguration.MainMode = New-Object Microsoft.Windows.NetworkController.MainMode   
$nwConnectionProperties.IpSecConfiguration.MainMode.DiffieHellmanGroup = "Group2"   
$nwConnectionProperties.IpSecConfiguration.MainMode.IntegrityAlgorithm = "SHA256"   
$nwConnectionProperties.IpSecConfiguration.MainMode.EncryptionAlgorithm = "AES256"   
$nwConnectionProperties.IpSecConfiguration.MainMode.SALifeTimeSeconds = 28800
$nwConnectionProperties.IpSecConfiguration.MainMode.SALifeTimeKiloBytes = 2000   

# L3 specific configuration (leave blank for IPSec)  
$nwConnectionProperties.IPAddresses = @()   
$nwConnectionProperties.PeerIPAddresses = @()   

# Update the IPv4 Routes that are reachable over the site-to-site VPN Tunnel  
$nwConnectionProperties.Routes = @()   
$ipv4Route = New-Object Microsoft.Windows.NetworkController.RouteInfo   
$ipv4Route.DestinationPrefix = "<<On premise subnet that must be reachable over the VPN tunnel. Ex: 10.0.0.0/24>>"   
$ipv4Route.metric = 10   
$nwConnectionProperties.Routes += $ipv4Route   

# Tunnel Destination (Remote Endpoint) Address  
$nwConnectionProperties.DestinationIPAddress = "<<Public IP address of the On-Premise VPN gateway. Ex: 192.168.3.4>>"   

# Add the new Network Connection for the tenant. Note that the virtual gateway must be created before creating the IPsec connection. $uri is the REST URI of your deployment and must be in the form of “https://<REST URI>”  
New-NetworkControllerVirtualGatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId $virtualGW.ResourceId -ResourceId "Contoso_IPSecGW" -Properties $nwConnectionProperties -Force
```

## <a name="testing-results"></a>テストの結果

広範なパフォーマンスのテスト ラボでの SDN ゲートウェイのテストを行った。 テストでは、SDN シナリオおよび非 SDN シナリオで Windows Server 2019 でゲートウェイのネットワーク パフォーマンスを比較しましたがあります。 結果を検索し、ブログ記事ではキャプチャされた設定の詳細をテストできます[ここ](https://blogs.technet.microsoft.com/networking/2018/08/15/high-performance-gateways/)します。

---