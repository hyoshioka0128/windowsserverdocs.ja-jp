---
title: バーチャル マシンを作成し、テナントの仮想ネットワークまたは VLAN に接続
description: このトピックでは、テナント ワークロードを管理および Windows Server 2016 での仮想ネットワークに方法について、ソフトウェア定義ネットワーク ガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3c62f533-1815-4f08-96b1-dc271f5a2b36
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 001eb3efa073e4ffbdfad41f88949303159a7274
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="create-a-vm-and-connect-to-a-tenant-virtual-network-or-vlan"></a>バーチャル マシンを作成し、テナントの仮想ネットワークまたは VLAN に接続

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、テナントの仮想を作成する \(VM\) マシンし、Hyper-V ネットワーク仮想化を使用して作成するか、仮想ネットワークまたは仮想ローカル エリア ネットワーク \(VLAN\) を VM に接続します。 

このトピックには、次のセクションが含まれています。

- [バーチャル マシンを作成し、Windows PowerShell のネットワーク コントローラーのコマンドレットを使用して仮想ネットワークに接続](#bkmk_vn)
- [バーチャル マシンを作成し、NetworkControllerRESTWrappers を使用して、VLAN に接続](#bkmk_vlan)

## <a name="requirements"></a>要件
次のセクションの手順を実行する前に、次の要件に注意してください。

1. 作成する必要がある VM ネットワーク アダプターに静的なメディアの \(MAC\) アドレス VM の有効期間中に、VM の MAC アドレスが変更しないように、アクセス制御します。 
>[!NOTE]
>VM の有効期間中に、VM の MAC アドレスが変更された場合、ネットワーク コントローラーは、ネットワーク アダプターの必要なポリシーを構成できません。 ネットワーク アダプターのポリシーが構成されていない場合は、ネットワーク アダプターは、ネットワーク トラフィックを処理できなくされ、ネットワークとの通信がすべて失敗します。 

2. VM は、スタートアップ時にネットワーク アクセスを必要とする場合は、最終的な構成手順 - ネットワーク アダプターのポート、VM 上のインターフェイス ID を設定した後になるまで VM が起動しないことが重要です。 この手順を完了する前に VM を起動する場合、VM 通信できない、ネットワーク上でネットワーク コントローラーにネットワーク インターフェイスが作成され、コントローラーのすべての該当するポリシー - 仮想ネットワーク ポリシーが適用されるまで \(ACLs\)、およびサービス \(QoS\) の品質のアクセス制御リストします。

また、仮想アプライアンスを展開するためには、このトピックで説明されているプロセスを使用することができます。 いくつかの手順が追加された処理または仮想ネットワーク上の他のバーチャル マシンとの間を流れるデータ パケットを検査するアプライアンスを構成できます。

>[!IMPORTANT]
>次のセクションでには、多くのパラメーターの値例にはが含まれている Windows PowerShell コマンド例にはが含まれます。 これらのコマンドを実行する前に、展開に適切な値を持つこれらのコマンドで値の例を置き換えることを確認します。  

## <a name="bkmk_vn"></a>バーチャル マシンを作成し、Windows PowerShell のネットワーク コントローラーのコマンドレットを使用して仮想ネットワークに接続

このセクションには、次のトピックが含まれています。

1.  [静的 MAC アドレスを持つ VM ネットワーク アダプターと VM を作成します。](#bkmk_create)
2.  [ネットワーク アダプターに接続するサブネットを含む仮想ネットワークを取得します。](#bkmk_getvn)
3.  [ネットワーク コントローラーで、ネットワーク インターフェイスのオブジェクトを作成します。](#bkmk_object)
4.  [ネットワーク コントローラーからのネットワーク インターフェイスの InstanceId を取得します。](#bkmk_getinstance)
5.  [Hyper-V VM ネットワーク アダプターのポート インターフェイス ID を設定します。](#bkmk_setinstance)
6.  [VM を起動します。](#bkmk_start)

### <a name="bkmk_create"></a>静的 MAC アドレスを持つ VM ネットワーク アダプターと VM を作成します。

静的 MAC アドレスを持つネットワーク アダプターを使用してバーチャル マシンを作成するには、次のコマンド例を使用します。

    
    New-VM -Generation 2 -Name "MyVM" -Path "C:\VMs\MyVM" -MemoryStartupBytes 4GB -VHDPath "c:\VMs\MyVM\Virtual Hard Disks\WindowsServer2016.vhdx" -SwitchName "SDNvSwitch" 
    
    Set-VM -Name "MyVM" -ProcessorCount 4
    
    Set-VMNetworkAdapter -VMName "MyVM" -StaticMacAddress "00-11-22-33-44-55" 
    

### <a name="bkmk_getvn"></a>ネットワーク アダプターに接続するサブネットを含む仮想ネットワークを取得します。
この例のコマンドを使用する前に仮想ネットワークが既に作成されたことを確認します。 詳細については、次を参照してください。[作成、削除、または更新プログラムのテナント仮想ネットワーク](https://technet.microsoft.com/windows-server-docs/networking/sdn/manage/create%2c-delete%2c-or-update-tenant-virtual-networks)します。

仮想ネットワークを取得するには、次のコマンド例を使用します。

    
    $vnet = get-networkcontrollervirtualnetwork -connectionuri $uri -ResourceId “Contoso_WebTier”
    

>[!NOTE]
>このネットワーク インターフェイスのカスタムの Acl を必要とする場合、ACL 今すぐ作成」トピックの手順を使用して[使用アクセス制御リスト (Acl) の管理データ センター ネットワーク トラフィック フロー](../../sdn/manage/Use-Access-Control-Lists--ACLs--to-Manage-Datacenter-Network-Traffic-Flow.md)

### <a name="bkmk_object"></a>ネットワーク コントローラーで、ネットワーク インターフェイスのオブジェクトを作成します。

ネットワーク コントローラーで、ネットワーク インターフェイスのオブジェクトを作成するには、次のコマンド例を使用します。

>[!NOTE]
>前の手順の後に、カスタムの ACL を作成した場合は、ここで使用できます。

    
    $vmnicproperties = new-object Microsoft.Windows.NetworkController.NetworkInterfaceProperties
    $vmnicproperties.PrivateMacAddress = "001122334455" 
    $vmnicproperties.PrivateMacAllocationMethod = "Static" 
    $vmnicproperties.IsPrimary = $true 

    $vmnicproperties.DnsSettings = new-object Microsoft.Windows.NetworkController.NetworkInterfaceDnsSettings
    $vmnicproperties.DnsSettings.DnsServers = @("24.30.1.11", "24.30.1.12")
    
    $ipconfiguration = new-object Microsoft.Windows.NetworkController.NetworkInterfaceIpConfiguration
    $ipconfiguration.resourceid = "MyVM_IP1"
    $ipconfiguration.properties = new-object Microsoft.Windows.NetworkController.NetworkInterfaceIpConfigurationProperties
    $ipconfiguration.properties.PrivateIPAddress = “24.30.1.101”
    $ipconfiguration.properties.PrivateIPAllocationMethod = "Static"
    
    $ipconfiguration.properties.Subnet = new-object Microsoft.Windows.NetworkController.Subnet
    $ipconfiguration.properties.subnet.ResourceRef = $vnet.Properties.Subnets[0].ResourceRef
    
    $vmnicproperties.IpConfigurations = @($ipconfiguration)
    New-NetworkControllerNetworkInterface –ResourceID “MyVM_Ethernet1” –Properties $vmnicproperties –ConnectionUri $uri
    

### <a name="bkmk_getinstance"></a>ネットワーク コントローラーからのネットワーク インターフェイスの InstanceId を取得します。
ネットワーク コントローラーから、ネットワーク インターフェイスの InstanceId を取得するには、次のコマンド例を使用します。

    
    $nic = Get-NetworkControllerNetworkInterface -ConnectionUri $uri -ResourceId "MyVM-Ethernet1"
    

### <a name="bkmk_setinstance"></a>Hyper-V VM ネットワーク アダプターのポート インターフェイス ID を設定します。
Hyper-V VM のネットワーク アダプターのポートのインターフェイス ID を設定するには、次のコマンド例を使用します。

>[!NOTE]
>これらのコマンドは、VM がインストールされている Hyper-V ホスト上で実行する必要があります。

    
    #Do not change the hardcoded IDs in this section, because they are fixed values and must not change.
    
    $FeatureId = "9940cd46-8b06-43bb-b9d5-93d50381fd56"
    
    $vmNics = Get-VMNetworkAdapter -VMName “MyVM”
    
    $CurrentFeature = Get-VMSwitchExtensionPortFeature -FeatureId $FeatureId -VMNetworkAdapter $vmNics
    
    if ($CurrentFeature -eq $null)
    {
    $Feature = Get-VMSystemSwitchExtensionPortFeature -FeatureId $FeatureId
    
    $Feature.SettingData.ProfileId = "{$($nic.InstanceId)}"
    $Feature.SettingData.NetCfgInstanceId = "{56785678-a0e5-4a26-bc9b-c0cba27311a3}"
    $Feature.SettingData.CdnLabelString = "TestCdn"
    $Feature.SettingData.CdnLabelId = 1111
    $Feature.SettingData.ProfileName = "Testprofile"
    $Feature.SettingData.VendorId = "{1FA41B39-B444-4E43-B35A-E1F7985FD548}"
    $Feature.SettingData.VendorName = "NetworkController"
    $Feature.SettingData.ProfileData = 1
    
    Add-VMSwitchExtensionPortFeature -VMSwitchExtensionFeature  $Feature -VMNetworkAdapter $vmNics
    }
    else
    {
    $CurrentFeature.SettingData.ProfileId = "{$($nic.InstanceId)}"
    $CurrentFeature.SettingData.ProfileData = 1
    
    Set-VMSwitchExtensionPortFeature -VMSwitchExtensionFeature $CurrentFeature  -VMNetworkAdapter $vmNic
    }
    

### <a name="bkmk_start"></a>VM を起動します。
VM を起動するには、次のコマンド例を使用します。

    
    Get-VM -Name “MyVM” | Start-VM 
    
ようになりましたが正常にバーチャル マシンを作成、VM をテナント仮想ネットワークに接続されているしてテナントのワークロードを処理できるように、VM を起動します。

## <a name="bkmk_vlan"></a>バーチャル マシンを作成し、NetworkControllerRESTWrappers を使用して、VLAN に接続

このセクションには、次のトピックが含まれています。

1. [VM を作成し、静的な MAC アドレスを割り当てる](#bkmk_mac)
2. [VM ネットワーク アダプターで VLAN ID を設定します。](#bkmk_vid)
3. [論理ネットワークのサブネットを取得し、ネットワーク インターフェイスを作成します。](#bkmk_subnet)
4. [Hyper-V ポートの InstanceId を設定します。](#bkmk_instance)
5. [VM を起動します。](#bkmk_startvlan)


###<a name="bkmk_mac"></a>VM を作成し、静的な MAC アドレスを割り当てる
バーチャル マシンを作成して、VM に静的なメディア アクセス制御 \(MAC\) アドレスを割り当てる、次の例のコマンドを使用できます。

    New-VM -Generation 2 -Name "MyVM" -Path "C:\VMs\MyVM" -MemoryStartupBytes 4GB -VHDPath "c:\VMs\MyVM\Virtual Hard Disks\WindowsServer2016.vhdx" -SwitchName "SDNvSwitch" 

    Set-VM -Name "MyVM" -ProcessorCount 4

    Set-VMNetworkAdapter -VMName "MyVM" -StaticMacAddress "00-11-22-33-44-55" 

###<a name="bkmk_vid"></a>VM ネットワーク アダプターで VLAN ID を設定します。
ネットワーク アダプターで VLAN ID を設定するには、次のコマンド例を使用できます。


    Set-VMNetworkAdapterIsolation –VMName “MyVM” -AllowUntaggedTraffic $true -IsolationMode VLAN -DefaultIsolationId 123


###<a name="bkmk_subnet"></a>論理ネットワークのサブネットを取得し、ネットワーク インターフェイスを作成します。

論理ネットワークのサブネットを取得し、論理ネットワークのサブネットを使用して、ネットワーク インターフェイスを作成するには、次の例のコマンドを使用できます。


    $logicalnet = get-networkcontrollerLogicalNetwork -connectionuri $uri -ResourceId "00000000-2222-1111-9999-000000000002"

    $vmnicproperties = new-object Microsoft.Windows.NetworkController.NetworkInterfaceProperties
    $vmnicproperties.PrivateMacAddress = "00-1D-C8-B7-01-02"
    $vmnicproperties.PrivateMacAllocationMethod = "Static"
    $vmnicproperties.IsPrimary = $true 
    
    $vmnicproperties.DnsSettings = new-object Microsoft.Windows.NetworkController.NetworkInterfaceDnsSettings
    $vmnicproperties.DnsSettings.DnsServers = $logicalnet.Properties.Subnets[0].DNSServers

    $ipconfiguration = new-object Microsoft.Windows.NetworkController.NetworkInterfaceIpConfiguration
    $ipconfiguration.resourceid = "MyVM_Ip1"
    $ipconfiguration.properties = new-object Microsoft.Windows.NetworkController.NetworkInterfaceIpConfigurationProperties
    $ipconfiguration.properties.PrivateIPAddress = “10.127.132.177”
    $ipconfiguration.properties.PrivateIPAllocationMethod = "Static"

    $ipconfiguration.properties.Subnet = new-object Microsoft.Windows.NetworkController.Subnet
    $ipconfiguration.properties.subnet.ResourceRef = $logicalnet.Properties.Subnets[0].ResourceRef

    $vmnicproperties.IpConfigurations = @($ipconfiguration)
    $vnic = New-NetworkControllerNetworkInterface –ResourceID “MyVM_Ethernet1” –Properties $vmnicproperties –ConnectionUri $uri

    $vnic.InstanceId
    

###<a name="bkmk_instance"></a>Hyper-V ポートの InstanceId を設定します。
Hyper-V ポートの InstanceId を設定するに使用できます、次の例のコマンド、Hyper-V ホスト上の VM が置かれています。

  
    #The hardcoded Ids in this section are fixed values and must not change.
    $FeatureId = "9940cd46-8b06-43bb-b9d5-93d50381fd56"

    $vmNics = Get-VMNetworkAdapter -VMName “MyVM”

    $CurrentFeature = Get-VMSwitchExtensionPortFeature -FeatureId $FeatureId -VMNetworkAdapter $vmNic
        
    if ($CurrentFeature -eq $null)
    {
        $Feature = Get-VMSystemSwitchExtensionFeature -FeatureId $FeatureId
        
        $Feature.SettingData.ProfileId = "{$InstanceId}"
        $Feature.SettingData.NetCfgInstanceId = "{56785678-a0e5-4a26-bc9b-c0cba27311a3}"
        $Feature.SettingData.CdnLabelString = "TestCdn"
        $Feature.SettingData.CdnLabelId = 1111
        $Feature.SettingData.ProfileName = "Testprofile"
        $Feature.SettingData.VendorId = "{1FA41B39-B444-4E43-B35A-E1F7985FD548}"
        $Feature.SettingData.VendorName = "NetworkController"
        $Feature.SettingData.ProfileData = 1
                
        Add-VMSwitchExtensionFeature -VMSwitchExtensionFeature  $Feature -VMNetworkAdapter $vmNic
    }        
    else
    {
        $CurrentFeature.SettingData.ProfileId = "{$InstanceId}"
        $CurrentFeature.SettingData.ProfileData = 1

        Set-VMSwitchExtensionPortFeature -VMSwitchExtensionFeature $CurrentFeature  -VMNetworkAdapter $vmNic
    }


###<a name="bkmk_startvlan"></a>VM を起動します。
VM を起動するには、次のコマンド例を使用することができます。


    Get-VM -Name “MyVM” | Start-VM 

ようになりましたが正常にバーチャル マシンを作成、VM を VLAN に接続されているしてテナントのワークロードを処理できるように、VM を起動します。

  

