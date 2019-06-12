---
title: 個別のデバイスの割り当てを使用してグラフィックス デバイスをデプロイします。
description: DDA を使用して、Windows Server でのグラフィックス デバイスをデプロイする方法について説明します
ms.prod: windows-server-threshold
ms.service: na
ms.technology: hyper-v
ms.tgt_pltfrm: na
ms.topic: article
author: chrishuybregts
ms.author: chrihu
ms.assetid: 67a01889-fa36-4bc6-841d-363d76df6a66
ms.openlocfilehash: 6c528535fd34f57957a37992843933d4cd9f8824
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447871"
---
# <a name="deploy-graphics-devices-using-discrete-device-assignment"></a>個別のデバイスの割り当てを使用してグラフィックス デバイスをデプロイします。

>適用先:Microsoft HYPER-V Server 2016、Windows Server 2016、Windows Server 2019、Microsoft HYPER-V Server 2019  

Windows Server 2016 以降では、VM に PCIe デバイス全体を渡すの個別のデバイスの割り当てまたは DDA を使用できます。  これにより、高パフォーマンスへのアクセスなどのデバイスを[NVMe ストレージ](./Deploying-storage-devices-using-dda.md)またはネイティブのデバイス ドライバーを利用している間に、VM 内からのグラフィックス カード。  参照してください、[個別のデバイスの割り当てを使用して展開するデバイスの計画](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md)デバイス作業について詳しくは、可能なセキュリティへの影響など、どのような。

デバイスの割り当てが不連続でデバイスを使用する 3 つの手順があります。
-   個別のデバイスの割り当ての VM を構成します。
-   パーティションをホストからデバイスのマウントを解除します。
-   ゲスト VM へのデバイスの割り当てください。

すべてのコマンドは、管理者として Windows PowerShell コンソールでのホストに実行できます。

## <a name="configure-the-vm-for-dda"></a>DDA の VM を構成します。
個別のデバイスの割り当ては、Vm にいくつかの制限を適用し、次の手順を実行する必要があります。

1.  実行して、「自動停止アクション」、vm をオフを構成します。

```
Set-VM -Name VMName -AutomaticStopAction TurnOff
```

### <a name="some-additional-vm-preparation-is-required-for-graphics-devices"></a>いくつか追加の VM の準備がグラフィックス デバイスに必要です。

一部のハードウェアは、内の VM は、特定の方法で構成されている場合に優れています。  詳細についての次の構成が必要かどうかは、ハードウェアの製造元にご連絡ください。 追加の詳細を確認できます[個別のデバイスの割り当てを使用して展開するデバイスの計画](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md)とこの[ブログの投稿。](https://blogs.technet.microsoft.com/virtualization/2015/11/23/discrete-device-assignment-gpus/)

1. 書き込み、CPU 上で結合を有効にします。
   ```
   Set-VM -GuestControlledCacheTypes $true -VMName VMName
   ```
2. 32 ビット MMIO スペースを構成します。
   ```
   Set-VM -LowMemoryMappedIoSpace 3Gb -VMName VMName
   ```
3. 32 ビット MMIO 領域よりも大きい値を構成します。
   ```
   Set-VM -HighMemoryMappedIoSpace 33280Mb -VMName VMName
   ```
   上記の MMIO 領域値が妥当な値を 1 つの gpu を搭載した実験の設定に注意してください。  VM の起動後に、デバイスがリソース不足に関連したエラーを報告している場合、これらの値を変更する必要がありますが可能性があります。  また、複数の Gpu を割り当てない場合はもこれらの値を大きく必要があります。

## <a name="dismount-the-device-from-the-host-partition"></a>パーティションをホストからデバイスのマウントを解除します。
### <a name="optional---install-the-partitioning-driver"></a>省略可能 - パーティション分割のドライバーをインストールします。
個別のデバイスの割り当ては、ハードウェアのベンダーと協力に自分のデバイスでセキュリティ対策のドライバーを提供する機能を提供します。  このドライバーがないことは、ゲスト VM にインストールするデバイス ドライバーと同じに注意してください。  これがこのドライバーを提供するハードウェアの製造元の裁量により、最大ただし場合は、提供インストールしてください前にホスト パーティションから、デバイスのマウントを解除します。  連絡してください、ハードウェアのベンダーの詳細については軽減策のドライバーがある場合
> パーティション分割のドライバーが指定されていない場合のマウント解除中に使用する必要あります、`-force`セキュリティ警告を回避するにはオプションです。 詳細をお読みください、これを行ってのセキュリティの影響について[個別のデバイスの割り当てを使用して展開するデバイスの計画](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md)します。

### <a name="locating-the-devices-location-path"></a>デバイスの場所のパスを検索します。
マウントを解除して、ホストからデバイスをマウントするには、PCI 場所のパスが必要です。  場所のパスの例は、次のように:`"PCIROOT(20)#PCI(0300)#PCI(0000)#PCI(0800)#PCI(0000)"`します。  配置の詳細について、場所のパスはご覧ください。[個別のデバイスの割り当てを使用して展開するデバイスの計画](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md)します。

### <a name="disable-the-device"></a>デバイスを無効にします。
デバイス マネージャーまたは PowerShell を使用して、デバイスが"無効にしてください"  

### <a name="dismount-the-device"></a>デバイスのマウントを解除します。
によって、ベンダーに軽減策のドライバーが指定されている場合か、必要がありますを使用する、"-強制的に"かどうかのオプションします。
- 軽減策のドライバーがインストールされている場合
  ```
  Dismount-VMHostAssignableDevice -LocationPath $locationPath
  ```
- 軽減策のドライバーがインストールされていない場合
  ```
  Dismount-VMHostAssignableDevice -force -LocationPath $locationPath
  ```

## <a name="assigning-the-device-to-the-guest-vm"></a>ゲスト VM へのデバイスの割り当てください。
最後の手順では、VM が存在するように、デバイスへのアクセスを HYPER-V に連絡します。  上記で見つかった場所のパス、だけでなく、vm の名前を知っている必要があります。

```
Add-VMAssignableDevice -LocationPath $locationPath -VMName VMName
```

## <a name="whats-next"></a>次の内容
VM で、デバイスが正常にマウントされると、その VM を起動し、ベア メタル システムを実行していた場合通常と同様に、デバイスと対話できるようになりました。  これは、VM のハードウェアの製造元のドライバーをインストールできるようになりましたし、アプリケーションが存在するハードウェアを参照してください。 できることを意味します。  これを確認するには、ゲスト VM でデバイス マネージャーを開き、表示、ハードウェアは、に表示されます。

## <a name="removing-a-device-and-returning-it-to-the-host"></a>デバイスを削除して、ホストに戻す
その元の状態にはデバイスを返す場合は、VM を停止し、次を発行する必要があります。
```
#Remove the device from the VM
Remove-VMAssignableDevice -LocationPath $locationPath -VMName VMName
#Mount the device back in the host
Mount-VMHostAssignableDevice -LocationPath $locationPath
```
できますし、再度有効にするデバイス マネージャーでデバイスと、ホスト オペレーティング システムをもう一度、デバイスと対話することになります。

## <a name="examples"></a>例

### <a name="mounting-a-gpu-to-a-vm"></a>VM の GPU のマウント
この例では、NVIDIA の製造元によって最初の GPU の実行を VM に割り当てる"ddatest1"をという名前の VM を構成するのに PowerShell を使用します。  
```
#Configure the VM for a Discrete Device Assignment
$vm =   "ddatest1"
#Set automatic stop action to TurnOff
Set-VM -Name $vm -AutomaticStopAction TurnOff
#Enable Write-Combining on the CPU
Set-VM -GuestControlledCacheTypes $true -VMName $vm
#Configure 32 bit MMIO space
Set-VM -LowMemoryMappedIoSpace 3Gb -VMName $vm
#Configure Greater than 32 bit MMIO space
Set-VM -HighMemoryMappedIoSpace 33280Mb -VMName $vm

#Find the Location Path and disable the Device
#Enumerate all PNP Devices on the system
$pnpdevs = Get-PnpDevice -presentOnly
#Select only those devices that are Display devices manufactured by NVIDIA
$gpudevs = $pnpdevs |where-object {$_.Class -like "Display" -and $_.Manufacturer -like "NVIDIA"}
#Select the location path of the first device that's available to be dismounted by the host.
$locationPath = ($gpudevs | Get-PnpDeviceProperty DEVPKEY_Device_LocationPaths).data[0]
#Disable the PNP Device
Disable-PnpDevice  -InstanceId $gpudevs[0].InstanceId

#Dismount the Device from the Host
Dismount-VMHostAssignableDevice -force -LocationPath $locationPath

#Assign the device to the guest VM.
Add-VMAssignableDevice -LocationPath $locationPath -VMName $vm
```
