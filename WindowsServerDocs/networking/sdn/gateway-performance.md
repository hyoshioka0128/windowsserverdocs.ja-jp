---
title: Windows Server 2019 ゲートウェイのパフォーマンス
manager: grcusanz
ms.topic: get-started-article
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/22/2018
ms.openlocfilehash: d7ca57b9cb1013d1e6c1081bdf7c5c50fa6a918d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969539"
---
# <a name="windows-server-2019-gateway-performance"></a>Windows Server 2019 ゲートウェイのパフォーマンス

>適用対象: Windows Server


Windows Server 2016 では、お客様の懸念事項の1つは、SDN ゲートウェイが最新のネットワークのスループット要件を満たすことができなかったことです。 Ipsec と GRE トンネルのネットワークスループットは、IPsec 接続が約 300 Mbps で、GRE 接続が約 2.5 Gbps であるという単一の接続スループットに制限されていました。

Windows Server 2019 では、数 soaring は 1.8 Gbps、15 Gbps は IPsec と GRE 接続に対して大幅に改善されました。 これにより、CPU サイクル/バイトあたりの CPU 使用率が大幅に減少し、非常に高いパフォーマンスのスループットが実現され、CPU 使用率が大幅に減少します。

## <a name="enable-high-performance-with-gateways-in-windows-server-2019"></a>Windows Server 2019 でゲートウェイを使用して高パフォーマンスを実現する

**GRE 接続**の場合、ゲートウェイ vm 上で Windows Server 2019 のビルドをデプロイ/アップグレードすると、パフォーマンスが向上したことが自動的に確認されます。 手動の手順は含まれません。

**IPsec 接続**の場合、既定では、仮想ネットワークの接続を作成すると、Windows Server 2016 のデータパスとパフォーマンス番号が取得されます。 Windows Server 2019 のデータパスを有効にするには、次の手順を実行します。

   1. SDN ゲートウェイ VM で、[**サービス**] コンソール (services.msc) にアクセスします。
   2. **Azure ゲートウェイサービス**という名前のサービスを探し、スタートアップの種類を [**自動**] に設定します。
   3. ゲートウェイ VM を再起動します。
      このゲートウェイのアクティブな接続は、冗長なゲートウェイ VM にフェールオーバーします。
   4. ゲートウェイ Vm の残りの部分に対して、前の手順を繰り返します。

>[!TIP]
>最適なパフォーマンスの結果を得るには、IPsec 接続の [quickMode 設定] の cipherTransformationConstant と authenticationTransformConstant で**GCMAES256** cipher suite が使用されていることを確認します。
>
>最大のパフォーマンスを向上させるには、ゲートウェイホストハードウェアが AES-NI および PCLMULQDQ CPU 命令セットをサポートしている必要があります。 これらは、Westmere (32nm) 以降の Intel CPU で使用できます。ただし、AES-NI が無効になっているモデルは除きます。 ハードウェアベンダーのドキュメントを参照して、CPU が AES-NI と PCLMULQDQ の CPU 命令セットをサポートしているかどうかを確認できます。

次に示すのは、最適なセキュリティアルゴリズムを使用した IPsec 接続の REST サンプルです。

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

## <a name="testing-results"></a>テスト結果

Microsoft では、テストラボで SDN ゲートウェイの広範なパフォーマンステストを行ってきました。 このテストでは、SDN シナリオと非 SDN シナリオで、Windows Server 2019 とゲートウェイネットワークパフォーマンスを比較しました。 検索結果とテストセットアップの詳細については、[こちら](https://blogs.technet.microsoft.com/networking/2018/08/15/high-performance-gateways/)のブログ記事で確認できます。

---