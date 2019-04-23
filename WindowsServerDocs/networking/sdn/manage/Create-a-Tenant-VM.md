---
title: VM を作成し、テナントの仮想ネットワークまたは VLAN に接続する
description: このトピックで紹介するテナントの VM を作成し、HYPER-V ネットワーク仮想化で作成した、仮想ネットワークまたは仮想ローカル エリア ネットワーク (VLAN) に接続する方法。
manager: dougkim
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
ms.date: 08/24/2018
ms.openlocfilehash: e23e6c020c12dd4900caa368daae0cc6dbeceaf4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856813"
---
# <a name="create-a-vm-and-connect-to-a-tenant-virtual-network-or-vlan"></a>VM を作成し、テナントの仮想ネットワークまたは VLAN に接続する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは、テナント VM を作成し、HYPER-V ネットワーク仮想化で作成した、仮想ネットワークまたは仮想ローカル エリア ネットワーク (VLAN) に接続します。 Windows PowerShell のネットワーク コント ローラーのコマンドレットを使用して、仮想ネットワークまたは VLAN に接続する NetworkControllerRESTWrappers に接続することができます。

このトピックで説明するプロセスを使用して、仮想アプライアンスをデプロイします。 いくつかの追加の手順を処理するか、または、仮想ネットワーク上の他の Vm との間を流れるデータ パケットを検査するアプライアンスを構成できます。

このトピックのセクションには、多くのパラメーターの値例にはが含まれている Windows PowerShell コマンド例にはが含まれます。 これらのコマンドで値の例は、これらのコマンドを実行する前に、展開に対応する値を置き換えることを確認します。 


## <a name="prerequisites"></a>前提条件

1. VM のネットワーク アダプターが VM の有効期間にわたって静的 MAC アドレスを作成します。<p>VM の有効期間中に、MAC アドレスが変更された場合、ネットワーク コント ローラーは、ネットワーク アダプターの必要なポリシーを構成できません。 ネットワーク アダプターが、ネットワーク トラフィックを処理するを防ぎますネットワークのポリシーを構成しないと、すべてのネットワーク通信が失敗します。  

2. VM は、起動時にネットワーク アクセスを必要とする場合、VM ネットワーク アダプターのポート、インターフェイス ID を設定後まで、VM は開始されません。 インターフェイス ID を設定する前に VM を起動したネットワーク インターフェイスが存在しない場合は、VM がネットワーク コント ローラーと適用されるすべてのポリシーでネットワーク上で通信できません。

3. このネットワーク インターフェイスのカスタム Acl が必要な場合、ACL 今すぐ作成、トピックの手順を使用して[使用へのアクセス制御リスト (Acl) を管理データ センター ネットワーク トラフィックのフロー](../../sdn/manage/Use-Access-Control-Lists--ACLs--to-Manage-Datacenter-Network-Traffic-Flow.md)

この例のコマンドを使用する前に仮想ネットワークを既に作成したことを確認します。 詳細については、次を参照してください。 [Create、Delete、またはテナントの仮想ネットワークを更新](https://technet.microsoft.com/windows-server-docs/networking/sdn/manage/create%2c-delete%2c-or-update-tenant-virtual-networks)します。

## <a name="create-a-vm-and-connect-to-a-virtual-network-by-using-the-windows-powershell-network-controller-cmdlets"></a>VM を作成し、Windows PowerShell のネットワーク コント ローラーのコマンドレットを使用して仮想ネットワークに接続


1. 静的 MAC アドレスを持つ VM ネットワーク アダプターを使用した VM を作成します。 

   ```PowerShell    
   New-VM -Generation 2 -Name "MyVM" -Path "C:\VMs\MyVM" -MemoryStartupBytes 4GB -VHDPath "c:\VMs\MyVM\Virtual Hard Disks\WindowsServer2016.vhdx" -SwitchName "SDNvSwitch" 
    
   Set-VM -Name "MyVM" -ProcessorCount 4
    
   Set-VMNetworkAdapter -VMName "MyVM" -StaticMacAddress "00-11-22-33-44-55" 
   ```

2. ネットワーク アダプターに接続するサブネットを含む仮想ネットワークを取得します。

   ```Powershell 
   $vnet = get-networkcontrollervirtualnetwork -connectionuri $uri -ResourceId “Contoso_WebTier”
   ```

3. ネットワーク コント ローラーで、ネットワーク インターフェイス オブジェクトを作成します。

   >[!TIP]
   >この手順では、カスタムの ACL を使用します。

   ```PowerShell
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
   ```

4. ネットワーク インターフェイスのネットワーク コント ローラーからはインスタンス Id を取得します。

   ```PowerShell 
    $nic = Get-NetworkControllerNetworkInterface -ConnectionUri $uri -ResourceId "MyVM-Ethernet1"
   ```

5. HYPER-V VM のネットワーク アダプター ポートのインターフェイス ID を設定します。

   >[!NOTE]
   >これらのコマンドは、VM がインストールされている HYPER-V ホストで実行する必要があります。

   ```PowerShell 
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
   ```

6. VM を起動します。

   ```PowerShell
    Get-VM -Name “MyVM” | Start-VM 
   ```

VM を作成して、テナント仮想ネットワークに VM を接続、およびテナントのワークロードを処理できるように、VM の開始が正常が。

## <a name="create-a-vm-and-connect-to-a-vlan-by-using-networkcontrollerrestwrappers"></a>VM を作成し、NetworkControllerRESTWrappers を使用して、VLAN に接続


1. VM を作成し、静的 MAC アドレスを VM に割り当てます。

   ```PowerShell
   New-VM -Generation 2 -Name "MyVM" -Path "C:\VMs\MyVM" -MemoryStartupBytes 4GB -VHDPath "c:\VMs\MyVM\Virtual Hard Disks\WindowsServer2016.vhdx" -SwitchName "SDNvSwitch" 

   Set-VM -Name "MyVM" -ProcessorCount 4

   Set-VMNetworkAdapter -VMName "MyVM" -StaticMacAddress "00-11-22-33-44-55" 
   ```

2. VM ネットワーク アダプターの VLAN ID を設定します。

   ```PowerShell
   Set-VMNetworkAdapterIsolation –VMName “MyVM” -AllowUntaggedTraffic $true -IsolationMode VLAN -DefaultIsolationId 123
   ```

3. 論理ネットワークのサブネットを取得し、ネットワーク インターフェイスを作成します。 

   ```PowerShell
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
   ```

4. HYPER-V ポートではインスタンス Id を設定します。

   ```PowerShell  
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
   ```

5. VM を起動します。

   ```PowerShell
   Get-VM -Name “MyVM” | Start-VM 
   ```

VM を作成して、VM を VLAN に接続されている、およびテナントのワークロードを処理できるように、VM を開始が正常が。

  

