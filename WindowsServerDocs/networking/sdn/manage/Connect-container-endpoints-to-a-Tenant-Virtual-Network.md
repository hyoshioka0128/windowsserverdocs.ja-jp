---
title: コンテナーを仮想ネットワークに接続します。
description: このトピックでは、テナント ワークロードを管理および Windows Server 2016 での仮想ネットワークに方法について、ソフトウェア定義ネットワーク ガイドの一部です。
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
ms.openlocfilehash: 801cf4b8f71935eb72d820d47e523a310fa64562
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="connect-container-endpoints-to-a-tenant-virtual-network"></a>コンテナーのエンドポイントをテナントの仮想ネットワークに接続します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、コンテナーのエンドポイントを Microsoft ソフトウェアによるネットワーク制御 (SDN) スタックによって作成された既存のテナント仮想ネットワークに接続する方法を示します。 使用して、 *l2bridge* (し、必要に応じて*l2tunnel*) Docker コンテナーのホスト (テナント) の仮想マシンでコンテナー ネットワークを作成するための Windows libnetwork プラグインで利用可能なネットワーク ドライバーします。

説明に従って、[コンテナー ネットワーク](https://msdn.microsoft.com/en-us/virtualization/windowscontainers/management/container_networking)に関する MSDN のトピック、複数のネットワーク ドライバーは、Windows 上の Docker を使用します。 SDN に最も適したドライバーが*l2bridge*と*l2tunnel*します。 両方のドライバーでは、各コンテナーのエンドポイントは、コンテナー ホスト (テナント) の仮想マシンと同じ仮想サブネットでです。 コンテナーのエンドポイントの IP アドレスは、によって、ホスト ネットワーク サービス (HNS)、プライベート クラウドのプラグインを動的に割り当てられます。 コンテナーのエンドポイントは、一意の IP アドレスを持つが、レイヤー 2 アドレス変換のためには、コンテナー ホスト (テナント) 仮想マシンの同じ MAC アドレスを共有します。 ネットワーク ポリシー (例: Acl、カプセル化、および QoS) これらのコンテナーのエンドポイントが、ネットワーク コント ローラーで受信された物理的な HYPER-V ホストに適用され、上位層の管理システムで定義されています。 わずかな違いは、 *l2bridge*と*l2tunnel*ドライバーについては、以下に説明します。

- **L2 ブリッジ**-同じコンテナー ホストのバーチャル マシン上に存在し、同じサブネット内のコンテナーのエンドポイントがあるすべてのネットワーク トラフィックが HYPER-V 仮想スイッチでブリッジされます。 別のコンテナー ホスト Vm 上に存在するか、別のサブネットにあるコンテナーのエンドポイントでは、物理的な HYPER-V ホストに転送トラフィックがあります。 同じホスト上で、同じサブネット内のコンテナー間のネットワーク トラフィックは、物理ホストに伝達されません、ので、ネットワーク ポリシーは適用されません。 ポリシーは、コンテナーのホスト間またはサブネット間のネットワーク トラフィックに対してのみ適用されます。  
 
- **L2 トンネル** - *すべて*2 つのコンテナー エンドポイント間のネットワーク トラフィックがホストまたはサブネットに関係なく、物理的な HYPER-V ホストに転送します。 ネットワーク ポリシーは、クロス サブネットとホスト間の両方のネットワーク トラフィックに適用されます。   

>[!NOTE]
>これらのネットワーク モードは、Azure パブリック クラウドで、テナントの仮想ネットワークに接続している windows コンテナーのエンドポイントでは機能しません

## <a name="prerequistes"></a>前提
 * ネットワーク コント ローラーと、SDN インフラストラクチャが展開されています。
 * テナントの仮想ネットワークが作成されました。
 * Windows コンテナー機能を有効に、Docker をインストールするには、HYPER-V 機能を有効になっていると、テナントの仮想マシンが展開されました。

>[!Note]
>[入れ子になった仮想化](https://msdn.microsoft.com/en-us/virtualization/hyperv_on_windows/user_guide/nesting)仮想化拡張機能を公開する場合は必要ありませんし l2tunnel、l2 ブリッジ ネットワークのいくつかのバイナリをインストールする必要は HYPER-V コンテナー: HyperV の機能を使用して、

```powershell
# To install HyperV feature without checks for nested virtualization
dism /Online /Enable-Feature /FeatureName:Microsoft-Hyper-V /All 
```

 

## <a name="workflow"></a>ワークフロー

1. [ネットワーク コント ローラーを既存の VM NIC のリソースに複数の IP 構成を追加](#Add)(HYPER-V ホスト)
2. [コンテナー エンドポイントの CA IP アドレスを割り当てる、ホスト上のネットワーク プロキシを有効にする](#Enable)(HYPER-V ホスト) 
3. [コンテナーのエンドポイントに CA IP アドレスを割り当てるプラグインのプライベート クラウドのインストール](#Install)(コンテナー ホスト VM) 
4. [作成、 *l2bridge*または*l2tunnel* docker を使用してネットワーク](#Create)(コンテナー ホスト VM) 
 
>[!NOTE]
>System Center Virtual Machine Manager によって作成された VM の NIC のリソースには、複数の IP 構成はサポートされていません。 勧めこれらの展開の種類のネットワーク コント ローラーの PowerShell を使用して帯域外の VM NIC のリソースを作成します。

### <a name="Add"></a>1。 複数の IP 構成を追加します。

この例では、ものとテナントの仮想マシンの VM の NIC が既に 192.168.1.9 の IP アドレスを持つ 1 つの IP 構成があり、'VNet1' の VNet リソース ID および 'Subnet1' の VM サブネット リソースに接続されていること 192.168.1.0/24 IP サブネットにします。 コンテナーの 10 個の IP アドレスは追加 192.168.1.101 - からは 192.168.1.110 します。

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

### <a name="Enable"></a>2. ネットワーク プロキシを有効にします。

[ConfigureMCNP.ps1](https://github.com/Microsoft/SDN/blob/master/Containers/ConfigureMCNP.ps1>)

このスクリプトを実行、 **HYPER-V ホストで**をコンテナー ホストのバーチャル マシンの複数の IP アドレスを割り当てるネットワーク プロキシを有効にするには、コンテナー ホスト (テナント) 仮想マシンをホストしています。

```powershell
PS C:\> ConfigureMCNP.ps1
```

### <a name="Install"></a>3。 プライベート クラウドのプラグインをインストールします。

[InstallPrivateCloudPlugin.ps1](https://github.com/Microsoft/SDN/blob/master/Containers/InstallPrivateCloudPlugin.ps1)

内のこのスクリプトの実行、**コンテナー ホスト (テナント) の仮想マシン**ホスト ネットワーク Service (HNS)、Hyper-v ホスト上のネットワーク プロキシとの通信を許可するようにします。

```powershell
PS C:\> InstallPrivateCloudPlugin.ps1
```

### <a name="Create"></a>4. を作成する、 *l2bridge*コンテナー ネットワーク

**コンテナー ホスト (テナント) の仮想マシン**を使用して、 `docker network create` l2bridge ネットワークを作成するコマンド

```powershell
# Create the container network
C:\> docker network create -d l2bridge --subnet="192.168.1.0/24" --gateway="192.168.1.1" MyContainerOverlayNetwork

# Attach a container to the MyContainerOverlayNetwork 
C:\> docker run -it --network=MyContainerOverlayNetwork <image> <cmd>
```

>[!NOTE]
>静的 IP の割り当てはサポートされていない*l2bridge*または*l2tunnel*コンテナー ネットワーク Microsoft SDN スタックを使用するとします。

## <a name="more-information"></a>詳細について
SDN インフラストラクチャの展開に関する詳細 infortation は、次を参照してください。[ソフトウェア定義ネットワーク インフラストラクチャの展開](https://technet.microsoft.com/en-us/windows-server-docs/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure)します。

