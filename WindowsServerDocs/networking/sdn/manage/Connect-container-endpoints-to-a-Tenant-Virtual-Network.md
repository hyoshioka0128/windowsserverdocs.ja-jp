---
title: コンテナーのエンドポイントをテナントの仮想ネットワークに接続する
description: このトピックで紹介する SDN を使って作成された既存のテナント仮想ネットワークにコンテナーのエンドポイントを接続する方法。 L2 ブリッジ (および必要に応じて l2tunnel) を使用するテナントの VM でのコンテナー ネットワークを作成する Docker 用の Windows libnetwork プラグインで使用可能なネットワーク ドライバー。
manager: ravirao
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7af1eb6-d035-4f74-a25b-d4b7e4ea9329
ms.author: pashort
author: jmesser81
ms.date: 08/24/2018
ms.openlocfilehash: cb9c7157ffb07233e41e1c933f6775f1cd0766a9
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446353"
---
# <a name="connect-container-endpoints-to-a-tenant-virtual-network"></a>コンテナーのエンドポイントをテナントの仮想ネットワークに接続する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックで紹介する SDN を使って作成された既存のテナント仮想ネットワークにコンテナーのエンドポイントを接続する方法。 使用する、 *l2bridge* (および必要に応じて*l2tunnel*)、テナントの VM でのコンテナー ネットワークを作成する Docker 用の Windows libnetwork プラグインで使用可能なネットワーク ドライバー。

[コンテナー ネットワーク ドライバー](https://docs.microsoft.com/virtualization/windowscontainers/container-networking/network-drivers-topologies)説明したトピックでは、複数のネットワーク ドライバーを Windows 上の Docker を利用します。 SDN を使用して、 *l2bridge*と*l2tunnel*ドライバー。 両方のドライバーでは、各コンテナーのエンドポイントは、コンテナー ホスト (テナント) の仮想マシンと同じ仮想サブネットにあります。 

ホスト ネットワーク サービス (HNS)、プライベート クラウドのプラグインでは、コンテナーのエンドポイントの IP アドレスを動的に割り当てます。 コンテナー エンドポイントは、一意の IP アドレスを持つが、レイヤー 2 アドレス変換により、コンテナー ホスト (テナント) の仮想マシンの同じ MAC アドレスを共有します。 

これらのコンテナーのエンドポイントのネットワーク ポリシー (Acl、カプセル化、および QoS) はネットワーク コント ローラーで受信すると、物理的な HYPER-V ホストに適用し、上位層の管理システムで定義されています。 

間の差、 *l2bridge*と*l2tunnel*ドライバーは。


|                                                                                                                                                                                                                                                                            l2bridge                                                                                                                                                                                                                                                                            |                                                                                                 l2tunnel                                                                                                  |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 上に存在するコンテナーのエンドポイント: <ul><li>同じコンテナーでは、仮想マシンをホストし、同じサブネットにあるすべてのネットワーク トラフィックが HYPER-V 仮想スイッチのブリッジします。 </li><li>別のコンテナーは、Vm をホストまたは異なるサブネット上、物理的な HYPER-V ホストに転送されるトラフィックがあります。 </li></ul>物理ホストに同じホスト上で、同じサブネット内のコンテナー間のネットワーク トラフィックをフローしないために、ネットワーク ポリシーが適用されませんを取得します。 ネットワーク ポリシーには、のみにホスト間またはクロス サブネットのコンテナーのネットワーク トラフィックが適用されます。 | *すべて*ホストやサブネットに関係なく、物理的な HYPER-V ホストに 2 つのコンテナー エンドポイント間のネットワーク トラフィックが転送されます。 クロス サブネットとホスト間の両方のネットワーク トラフィックをネットワーク ポリシーが適用されます。 |

---

>[!NOTE]
>これらのネットワーク モードは、Azure パブリック クラウドでテナントの仮想ネットワークに接続している windows コンテナーのエンドポイントには機能しません。


## <a name="prerequisites"></a>前提条件
-  ネットワーク コント ローラーと、展開済み SDN インフラストラクチャ。
-  テナントの仮想ネットワークが作成されました。
-  Docker がインストールされていると、HYPER-V 機能を有効に、デプロイされたテナントの仮想マシンを Windows コンテナー機能が有効にします。 HYPER-V の機能は、l2 ブリッジと l2tunnel のネットワークのいくつかのバイナリをインストールする必要があります。

   ```powershell
   # To install HyperV feature without checks for nested virtualization
   dism /Online /Enable-Feature /FeatureName:Microsoft-Hyper-V /All 
   ```

>[!Note]
>[入れ子になった仮想化](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/nesting)仮想化拡張機能を公開する場合は必要ありません、HYPER-V コンテナーを使用するとします。 


## <a name="workflow"></a>ワークフロー

[1.ネットワーク コント ローラー (HYPER-V ホスト) を既存の VM の NIC リソースへの複数の IP 構成の追加](#1-add-multiple-ip-configurations)
[2。コンテナーのエンドポイント (HYPER-V ホスト) の CA IP アドレスを割り当てる、ホスト上のネットワーク プロキシを有効にする](#2-enable-the-network-proxy)
[3。プライベート クラウドをコンテナー エンドポイント (コンテナー ホスト VM) への CA IP アドレスを割り当てるにはプラグインをインストール](#3-install-the-private-cloud-plug-in)
[4。作成、 *l2bridge*または*l2tunnel* docker (コンテナー ホスト VM) を使用してネットワーク](#4-create-an-l2bridge-container-network)

>[!NOTE]
>System Center Virtual Machine Manager を作成した VM の NIC リソースでは、複数の IP 構成はサポートされていません。 勧めこれらの展開の種類のネットワーク コント ローラーの PowerShell を使用して帯域外の VM の NIC リソースを作成します。

### <a name="1-add-multiple-ip-configurations"></a>1. 複数の IP 構成を追加します。
この手順でテナントの仮想マシンの VM NIC が 192.168.1.9 の IP アドレスを持つ 1 つの IP 構成に備え 192.168.1.0/24 IP サブネット内の 'VNet1' の VNet のリソース ID と"Subnet1"の VM サブネットのリソースに接続されてと仮定します。 コンテナーの 10 個の IP アドレスから 192.168.1.101 - 追加は 192.168.1.110 します。

```powershell
Import-Module NetworkController

# Specify Network Controller REST IP or FQDN
$uri = "<NC REST IP or FQDN>"
$vnetResourceId = "VNet1"
$vsubnetResourceId = "Subnet1"

$vmnic= Get-NetworkControllerNetworkInterface -ConnectionUri $uri | where {$_.properties.IpConfigurations.Properties.PrivateIPAddress -eq "192.168.1.9" }
$vmsubnet = Get-NetworkControllerVirtualSubnet -VirtualNetworkId $vnetResourceId -ResourceId $vsubnetResourceId -ConnectionUri $uri

# For this demo, we will assume an ACL has already been defined; any ACL can be applied here
$allowallacl = Get-NetworkControllerAccessControlList -ConnectionUri $uri -ResourceId "AllowAll"


foreach ($i in 1..10)
{
    $newipconfig = new-object Microsoft.Windows.NetworkController.NetworkInterfaceIpConfiguration
    $props = new-object Microsoft.Windows.NetworkController.NetworkInterfaceIpConfigurationProperties

    $resourceid = "IP_192_168_1_1"
    if ($i -eq 10) 
    {
        $resourceid += "10"
        $ipstr = "192.168.1.110"
    }
    else
    {
        $resourceid += "0$i"
        $ipstr = "192.168.1.10$i"
    }

    $newipconfig.ResourceId = $resourceid
    $props.PrivateIPAddress = $ipstr    

    $props.PrivateIPAllocationMethod = "Static"
    $props.Subnet = new-object Microsoft.Windows.NetworkController.Subnet
    $props.Subnet.ResourceRef = $vmsubnet.ResourceRef
    $props.AccessControlList = new-object Microsoft.Windows.NetworkController.AccessControlList
    $props.AccessControlList.ResourceRef = $allowallacl.ResourceRef

    $newipconfig.Properties = $props
    $vmnic.Properties.IpConfigurations += $newipconfig
}

New-NetworkControllerNetworkInterface -ResourceId $vmnic.ResourceId -Properties $vmnic.Properties -ConnectionUri $uri
```

### <a name="2-enable-the-network-proxy"></a>2. ネットワーク プロキシを有効にします。
この手順では、コンテナー ホストの仮想マシンの複数の IP アドレスを割り当てるネットワーク プロキシを有効にします。 

ネットワーク プロキシを有効にするには実行、 [ConfigureMCNP.ps1](https://github.com/Microsoft/SDN/blob/master/Containers/ConfigureMCNP.ps1)にスクリプト、 **HYPER-V ホスト**コンテナー ホスト (テナント) の仮想マシンをホストします。

```powershell
PS C:\> ConfigureMCNP.ps1
```

### <a name="3-install-the-private-cloud-plug-in"></a>3.プライベート クラウドのプラグインのインストールします。
この手順では、HYPER-V ホスト上のネットワーク プロキシとの通信に HNS を許可するプラグイン インストールします。

プラグインをインストールするには、実行、 [InstallPrivateCloudPlugin.ps1](https://github.com/Microsoft/SDN/blob/master/Containers/InstallPrivateCloudPlugin.ps1)内でのスクリプトを作成、**コンテナー ホスト (テナント) の仮想マシン**します。


```powershell
PS C:\> InstallPrivateCloudPlugin.ps1
```

### <a name="4-create-an-l2bridge-container-network"></a>4。作成、 *l2bridge*コンテナー ネットワーク
この手順で使用して、`docker network create`コマンドを**コンテナー ホスト (テナント) の仮想マシン**l2 ブリッジ ネットワークを作成します。 

```powershell
# Create the container network
C:\> docker network create -d l2bridge --subnet="192.168.1.0/24" --gateway="192.168.1.1" MyContainerOverlayNetwork

# Attach a container to the MyContainerOverlayNetwork 
C:\> docker run -it --network=MyContainerOverlayNetwork <image> <cmd>
```

>[!NOTE]
>静的 IP の割り当てはサポートされていません*l2bridge*または*l2tunnel*コンテナー ネットワークを Microsoft SDN スタックを使用するとします。

## <a name="more-information"></a>詳細情報
SDN インフラストラクチャのデプロイに関する詳細については、次を参照してください。[ソフトウェア定義ネットワーク インフラストラクチャの展開](https://docs.microsoft.com/windows-server/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure)します。

