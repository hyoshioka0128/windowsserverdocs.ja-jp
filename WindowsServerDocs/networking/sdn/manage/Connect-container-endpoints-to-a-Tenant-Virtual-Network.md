---
title: コンテナーのエンドポイントをテナントの仮想ネットワークに接続する
description: このトピックでは、SDN を使用して作成された既存のテナント仮想ネットワークにコンテナーエンドポイントを接続する方法について説明します。 Docker 用の Windows libnetwork プラグインで利用できる l2bridge (および必要に応じて l2tunnel) ネットワークドライバーを使用して、テナント VM にコンテナーネットワークを作成します。
manager: ravirao
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7af1eb6-d035-4f74-a25b-d4b7e4ea9329
ms.author: pashort
author: jmesser81
ms.date: 08/24/2018
ms.openlocfilehash: 83996f7ffb82d01c9f36945efa022f0dd0b9825b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355819"
---
# <a name="connect-container-endpoints-to-a-tenant-virtual-network"></a>コンテナーのエンドポイントをテナントの仮想ネットワークに接続する

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、SDN を使用して作成された既存のテナント仮想ネットワークにコンテナーエンドポイントを接続する方法について説明します。 Docker 用の Windows libnetwork プラグインで利用できる*l2bridge* (および必要に応じて*l2tunnel*) ネットワークドライバーを使用して、テナント VM にコンテナーネットワークを作成します。

[コンテナーネットワークドライバー](https://docs.microsoft.com/virtualization/windowscontainers/container-networking/network-drivers-topologies)に関するトピックでは、Windows 上の Docker を通じて複数のネットワークドライバーを使用できることについて説明しました。 SDN の場合は、 *l2bridge*ドライバーと*l2tunnel*ドライバーを使用します。 どちらのドライバーでも、各コンテナーエンドポイントは、コンテナーホスト (テナント) 仮想マシンと同じ仮想サブネット内にあります。 

ホストネットワークサービス (HNS) は、プライベートクラウドプラグインを介して、コンテナーエンドポイントの IP アドレスを動的に割り当てます。 コンテナーエンドポイントには一意の IP アドレスがありますが、レイヤー2のアドレス変換によって、コンテナーホスト (テナント) 仮想マシンと同じ MAC アドレスが共有されます。 

これらのコンテナーエンドポイントのネットワークポリシー (Acl、カプセル化、QoS) は、ネットワークコントローラーによって受信され、上位層の管理システムで定義されている物理 Hyper-v ホストに適用されます。 

*L2bridge*ドライバーと*l2tunnel*ドライバーの違いは次のとおりです。


|                                                                                                                                                                                                                                                                            l2bridge                                                                                                                                                                                                                                                                            |                                                                                                 l2tunnel                                                                                                  |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 次に存在するコンテナーエンドポイント: <ul><li>同じコンテナーホスト仮想マシンと同じサブネット上のすべてのネットワークトラフィックが、Hyper-v 仮想スイッチ内でブリッジされます。 </li><li>異なるコンテナーホスト Vm または異なるサブネット上のトラフィックは、物理的な Hyper-v ホストに転送されます。 </li></ul>同じホスト上のコンテナーと同じサブネット内のコンテナー間のネットワークトラフィックが物理ホストにフローしないため、ネットワークポリシーは適用されません。 ネットワークポリシーは、クロスホストコンテナーまたはクロスサブネットコンテナーのネットワークトラフィックにのみ適用されます。 | 2つのコンテナーエンドポイント間の*すべて*のネットワークトラフィックは、ホストまたはサブネットに関係なく、物理的な hyper-v ホストに転送されます。 ネットワークポリシーは、クロスサブネットとクロスホストの両方のネットワークトラフィックに適用されます。 |

---

>[!NOTE]
>これらのネットワークモードは、windows コンテナーエンドポイントを Azure パブリッククラウド内のテナント仮想ネットワークに接続する場合には機能しません。


## <a name="prerequisites"></a>前提条件
-  ネットワークコントローラーを使用して展開された SDN インフラストラクチャ。
-  テナントの仮想ネットワークが作成されました。
-  Windows コンテナー機能が有効になっている、Docker がインストールされ、Hyper-v 機能が有効になっている、デプロイされたテナント仮想マシン。 Hyper-v 機能では、l2bridge および l2tunnel ネットワーク用に複数のバイナリをインストールする必要があります。

   ```powershell
   # To install HyperV feature without checks for nested virtualization
   dism /Online /Enable-Feature /FeatureName:Microsoft-Hyper-V /All 
   ```

>[!Note]
>[入れ子になった仮想](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/nesting)化と仮想化拡張機能の公開は、hyper-v コンテナーを使用する場合には必要ありません。 


## <a name="workflow"></a>ワークフロー

[1.ネットワークコントローラー (Hyper-v ホスト) を介して、既存の VM NIC リソースに複数の IP 構成を追加 ](#1-add-multiple-ip-configurations) @ no__t-1 @ no__t-22.ホストのネットワークプロキシで、コンテナーエンドポイント (Hyper-v ホスト) の CA IP アドレスを割り当てることができるようにするには、](#2-enable-the-network-proxy) @ no__t-1 @ no__t-23 を使用します。プライベートクラウドプラグインをインストールして、CA IP アドレスをコンテナーエンドポイント (コンテナーホスト VM) に割り当てます。 ](#3-install-the-private-cloud-plug-in) @ no__t-1 @ no__t-24。Docker (コンテナーホスト VM) を使用して*l2bridge*または*l2tunnel*ネットワークを作成する ](#4-create-an-l2bridge-container-network)

>[!NOTE]
>System Center Virtual Machine Manager によって作成された VM NIC リソースでは、複数の IP 構成はサポートされていません。 これらの展開の種類では、ネットワークコントローラー PowerShell を使用して、帯域外で VM NIC リソースを作成することをお勧めします。

### <a name="1-add-multiple-ip-configurations"></a>1. 複数の IP 構成を追加する
このステップでは、テナント仮想マシンの VM NIC に IP アドレス192.168.1.9 の IP 構成が1つあり、ip サブネットが 192.168.1.0/24 である ' Subnet1 ' の VNet リソース ID ' VNet1 ' と VM サブネットリソースに接続されていることを前提としています。 192.168.1.101 から192.168.1.110 のコンテナーに対して10個の IP アドレスを追加します。

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

### <a name="2-enable-the-network-proxy"></a>2. ネットワークプロキシを有効にする
このステップでは、ネットワークプロキシでコンテナーホスト仮想マシンに複数の IP アドレスを割り当てることができるようにします。 

ネットワークプロキシを有効にするには、コンテナーホスト (テナント) 仮想マシンをホストする**Hyper-v ホスト**で[ConfigureMCNP](https://github.com/Microsoft/SDN/blob/master/Containers/ConfigureMCNP.ps1)スクリプトを実行します。

```powershell
PS C:\> ConfigureMCNP.ps1
```

### <a name="3-install-the-private-cloud-plug-in"></a>3.プライベートクラウドプラグインをインストールする
この手順では、HNS が Hyper-v ホスト上のネットワークプロキシと通信できるように、プラグインをインストールします。

プラグインをインストールするには、**コンテナーホスト (テナント) の仮想マシン**内で[InstallPrivateCloudPlugin](https://github.com/Microsoft/SDN/blob/master/Containers/InstallPrivateCloudPlugin.ps1)スクリプトを実行します。


```powershell
PS C:\> InstallPrivateCloudPlugin.ps1
```

### <a name="4-create-an-l2bridge-container-network"></a>4。*L2bridge*コンテナーネットワークを作成する
このステップでは、**コンテナーホスト (テナント) 仮想マシン**で `docker network create` コマンドを使用して、l2bridge ネットワークを作成します。 

```powershell
# Create the container network
C:\> docker network create -d l2bridge --subnet="192.168.1.0/24" --gateway="192.168.1.1" MyContainerOverlayNetwork

# Attach a container to the MyContainerOverlayNetwork 
C:\> docker run -it --network=MyContainerOverlayNetwork <image> <cmd>
```

>[!NOTE]
>*L2bridge*または*l2tunnel* container network では、静的 IP の割り当ては、Microsoft SDN スタックではサポートされていません。

## <a name="more-information"></a>詳細情報
SDN インフラストラクチャの展開の詳細については、「[ソフトウェア定義ネットワークインフラストラクチャを展開する](https://docs.microsoft.com/windows-server/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure)」を参照してください。

