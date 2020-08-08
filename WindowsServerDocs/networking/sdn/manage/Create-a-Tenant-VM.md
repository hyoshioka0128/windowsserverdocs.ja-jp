---
title: VM を作成し、テナントの仮想ネットワークまたは VLAN に接続する
description: このトピックでは、テナント VM を作成し、Hyper-v ネットワーク仮想化を使用して作成した仮想ネットワークまたは仮想ローカルエリアネットワーク (VLAN) に接続する方法について説明します。
manager: grcusanz
ms.topic: article
ms.assetid: 3c62f533-1815-4f08-96b1-dc271f5a2b36
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/24/2018
ms.openlocfilehash: 2ca1c308ee38726d02ef19ebdfa4c83086fef0a7
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87995151"
---
# <a name="create-a-vm-and-connect-to-a-tenant-virtual-network-or-vlan"></a>VM を作成し、テナントの仮想ネットワークまたは VLAN に接続する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、テナント VM を作成し、Hyper-v ネットワーク仮想化を使用して作成した仮想ネットワークまたは仮想ローカルエリアネットワーク (VLAN) に接続します。 Windows PowerShell Network Controller コマンドレットを使用して、仮想ネットワークまたは NetworkControllerRESTWrappers に接続し、VLAN に接続することができます。

仮想アプライアンスを展開するには、このトピックで説明するプロセスを使用します。 いくつかの追加の手順で、Virtual Network の他の Vm との間でやり取りされるデータパケットを処理または検査するようにアプライアンスを構成できます。

このトピックのセクションには、多くのパラメーターの値の例を含む Windows PowerShell コマンドの例が含まれています。 これらのコマンドで値の例は、これらのコマンドを実行する前に、展開に対応する値を置き換えることを確認します。


## <a name="prerequisites"></a>前提条件

1. Vm の有効期間中、静的 MAC アドレスを使用して作成された VM ネットワークアダプター。<p>VM の有効期間中に MAC アドレスが変更された場合、ネットワークコントローラーはネットワークアダプターに必要なポリシーを構成できません。 ネットワークのポリシーを構成しないと、ネットワークアダプターはネットワークトラフィックを処理できず、ネットワークとの通信はすべて失敗します。

2. VM が起動時にネットワークアクセスを必要とする場合は、vm ネットワークアダプターポートでインターフェイス ID を設定するまで VM を起動しないでください。 インターフェイス ID を設定する前に VM を起動し、ネットワークインターフェイスが存在しない場合、VM はネットワークコントローラーのネットワークと、すべてのポリシーが適用されていると通信できません。

3. このネットワークインターフェイスにカスタム Acl が必要な場合は、トピック「 [Access Control リスト (acl) を使用してデータセンターのネットワークトラフィックフローを管理する](./use-acls-for-traffic-flow.md)」の手順に従って、acl を作成します。

この例のコマンドを使用する前に、Virtual Network が既に作成されていることを確認してください。 詳細については、「[テナント仮想ネットワークの作成、削除、または更新](./create,-delete,-or-update-tenant-virtual-networks.md)」を参照してください。

## <a name="create-a-vm-and-connect-to-a-virtual-network-by-using-the-windows-powershell-network-controller-cmdlets"></a>Windows PowerShell ネットワークコントローラーコマンドレットを使用して VM を作成し、Virtual Network に接続する


1. 静的 MAC アドレスを持つ vm ネットワークアダプターを使用して VM を作成します。

   ```PowerShell
   New-VM -Generation 2 -Name "MyVM" -Path "C:\VMs\MyVM" -MemoryStartupBytes 4GB -VHDPath "c:\VMs\MyVM\Virtual Hard Disks\WindowsServer2016.vhdx" -SwitchName "SDNvSwitch"

   Set-VM -Name "MyVM" -ProcessorCount 4

   Set-VMNetworkAdapter -VMName "MyVM" -StaticMacAddress "00-11-22-33-44-55"
   ```

2. ネットワークアダプターの接続先のサブネットを含む仮想ネットワークを取得します。

   ```Powershell
   $vnet = get-networkcontrollervirtualnetwork -connectionuri $uri -ResourceId "Contoso_WebTier"
   ```

3. ネットワークコントローラーにネットワークインターフェイスオブジェクトを作成します。

   >[!TIP]
   >この手順では、カスタム ACL を使用します。

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
   $ipconfiguration.properties.PrivateIPAddress = "24.30.1.101"
   $ipconfiguration.properties.PrivateIPAllocationMethod = "Static"

   $ipconfiguration.properties.Subnet = new-object Microsoft.Windows.NetworkController.Subnet
   $ipconfiguration.properties.subnet.ResourceRef = $vnet.Properties.Subnets[0].ResourceRef

   $vmnicproperties.IpConfigurations = @($ipconfiguration)
   New-NetworkControllerNetworkInterface –ResourceID "MyVM_Ethernet1" –Properties $vmnicproperties –ConnectionUri $uri
   ```

4. ネットワークコントローラーからネットワークインターフェイスの InstanceId を取得します。

   ```PowerShell
    $nic = Get-NetworkControllerNetworkInterface -ConnectionUri $uri -ResourceId "MyVM-Ethernet1"
   ```

5. Hyper-v VM ネットワークアダプターのポートで、インターフェイス ID を設定します。

   >[!NOTE]
   >これらのコマンドは、VM がインストールされている Hyper-v ホスト上で実行する必要があります。

   ```PowerShell
   #Do not change the hardcoded IDs in this section, because they are fixed values and must not change.

   $FeatureId = "9940cd46-8b06-43bb-b9d5-93d50381fd56"

   $vmNics = Get-VMNetworkAdapter -VMName "MyVM"

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
    Get-VM -Name "MyVM" | Start-VM
   ```

Vm を作成し、テナント Virtual Network に VM を接続して、テナントのワークロードを処理できるように VM を開始しました。

## <a name="create-a-vm-and-connect-to-a-vlan-by-using-networkcontrollerrestwrappers"></a>NetworkControllerRESTWrappers を使用して VM を作成し、VLAN に接続する


1. VM を作成し、VM に静的 MAC アドレスを割り当てます。

   ```PowerShell
   New-VM -Generation 2 -Name "MyVM" -Path "C:\VMs\MyVM" -MemoryStartupBytes 4GB -VHDPath "c:\VMs\MyVM\Virtual Hard Disks\WindowsServer2016.vhdx" -SwitchName "SDNvSwitch"

   Set-VM -Name "MyVM" -ProcessorCount 4

   Set-VMNetworkAdapter -VMName "MyVM" -StaticMacAddress "00-11-22-33-44-55"
   ```

2. VM ネットワークアダプターに VLAN ID を設定します。

   ```PowerShell
   Set-VMNetworkAdapterIsolation –VMName "MyVM" -AllowUntaggedTraffic $true -IsolationMode VLAN -DefaultIsolationId 123
   ```

3. 論理ネットワークサブネットを取得し、ネットワークインターフェイスを作成します。

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
    $ipconfiguration.properties.PrivateIPAddress = "10.127.132.177"
    $ipconfiguration.properties.PrivateIPAllocationMethod = "Static"

    $ipconfiguration.properties.Subnet = new-object Microsoft.Windows.NetworkController.Subnet
    $ipconfiguration.properties.subnet.ResourceRef = $logicalnet.Properties.Subnets[0].ResourceRef

    $vmnicproperties.IpConfigurations = @($ipconfiguration)
    $vnic = New-NetworkControllerNetworkInterface –ResourceID "MyVM_Ethernet1" –Properties $vmnicproperties –ConnectionUri $uri

    $vnic.InstanceId
   ```

4. Hyper-v ポートで InstanceId を設定します。

   ```PowerShell
   #The hardcoded Ids in this section are fixed values and must not change.
   $FeatureId = "9940cd46-8b06-43bb-b9d5-93d50381fd56"

   $vmNics = Get-VMNetworkAdapter -VMName "MyVM"

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
   Get-VM -Name "MyVM" | Start-VM
   ```

Vm が正常に作成され、VM が VLAN に接続され、VM が開始され、テナントのワークロードを処理できるようになりました。