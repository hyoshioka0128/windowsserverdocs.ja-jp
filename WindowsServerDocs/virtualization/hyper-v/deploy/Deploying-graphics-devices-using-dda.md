---
title: 個別のデバイスの割り当てを使用してグラフィックスデバイスをデプロイする
description: DDA を使用して Windows Server でグラフィックスデバイスを展開する方法について説明します。
ms.prod: windows-server
ms.technology: hyper-v
ms.topic: article
author: chrishuybregts
ms.author: chrihu
ms.assetid: 67a01889-fa36-4bc6-841d-363d76df6a66
ms.date: 08/21/2019
ms.openlocfilehash: 07f0ba19aaf998bb7b2fe8cf4ef1ba6cf8cae322
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860915"
---
# <a name="deploy-graphics-devices-using-discrete-device-assignment"></a>個別のデバイスの割り当てを使用してグラフィックスデバイスをデプロイする

> 適用対象: Microsoft Hyper-V Server 2016、Windows Server 2016、Windows Server 2019、Microsoft Hyper-V Server 2019  

Windows Server 2016 以降では、個別のデバイス割り当て (DDA) を使用して、PCIe デバイス全体を VM に渡すことができます。  これにより、デバイスのネイティブドライバーを利用できるのに対して、VM 内から[NVMe ストレージ](./Deploying-storage-devices-using-dda.md)やグラフィックスカードなどのデバイスに高パフォーマンスでアクセスできるようになります。  デバイスの展開については、デバイス[の個別割り当てを使用したデバイスの展開計画](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md)に関するページを参照してください。

デバイスに個別のデバイス割り当てを使用するには、次の3つの手順を実行します。
-   個別のデバイスの割り当て用に VM を構成する
-   ホストパーティションからデバイスのマウントを解除する
-   ゲスト VM へのデバイスの割り当て

すべてのコマンドは、Windows PowerShell コンソールのホストで管理者として実行できます。

## <a name="configure-the-vm-for-dda"></a>DDA 用に VM を構成する
個別のデバイスの割り当てによって、Vm にいくつかの制限が課され、次の手順を実行する必要があります。

1.  を実行して、VM の "自動停止アクション" を TurnOff に構成します。

```
Set-VM -Name VMName -AutomaticStopAction TurnOff
```

### <a name="some-additional-vm-preparation-is-required-for-graphics-devices"></a>グラフィックスデバイスには、追加の VM 準備が必要です。

VM が特定の方法で構成されていると、一部のハードウェアのパフォーマンスが向上します。  ハードウェアに次の構成が必要かどうかの詳細については、ハードウェアベンダーにお問い合わせください。 その他の詳細につい[ては、「個別のデバイスの割り当てを使用したデバイスのデプロイ計画](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md)」と、このブログの投稿を参照して[ください。](https://techcommunity.microsoft.com/t5/Virtualization/Discrete-Device-Assignment-GPUs/ba-p/382266)

1. CPU で書き込み結合を有効にする
   ```
   Set-VM -GuestControlledCacheTypes $true -VMName VMName
   ```
2. 32ビット MMIO space の構成
   ```
   Set-VM -LowMemoryMappedIoSpace 3Gb -VMName VMName
   ```
3. 32ビット MMIO space を超える構成
   ```
   Set-VM -HighMemoryMappedIoSpace 33280Mb -VMName VMName
   ```
   > [!TIP] 
   > 上の MMIO space 値は、1つの GPU を試すために設定する妥当な値です。  VM を起動した後、デバイスがリソース不足に関連するエラーを報告している場合は、これらの値を変更する必要があります。 MMIO の要件を正確に計算する方法については、 [「個別のデバイスの割り当てを使用したデバイスの展開計画](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md)」を参照してください。

## <a name="dismount-the-device-from-the-host-partition"></a>ホストパーティションからデバイスのマウントを解除する
### <a name="optional---install-the-partitioning-driver"></a>オプション-パーティションドライバーをインストールする
個別のデバイスの割り当てにより、ハードウェア venders は、セキュリティ対策ドライバーをデバイスに提供することができます。  このドライバーは、ゲスト VM にインストールされるデバイスドライバーと同じではないことに注意してください。  このドライバーを提供するには、ハードウェアベンダーの判断が必要です。ただし、提供されている場合は、ホストパーティションからデバイスをマウント解除する前にインストールしてください。  軽減ドライバーがあるかどうかの詳細については、ハードウェアベンダーにお問い合わせください。
> パーティション分割ドライバーが指定されていない場合は、マウント解除中に、`-force` オプションを使用してセキュリティ警告を回避する必要があります。 [個別のデバイスの割り当てを使用してデバイスを展開する計画](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md)については、セキュリティへの影響について詳しくお読みください。

### <a name="locating-the-devices-location-path"></a>デバイスの場所のパスを特定する
ホストからデバイスをマウント解除してマウントするには、PCI ロケーションパスが必要です。  ロケーションパスの例は次のようになります: `"PCIROOT(20)#PCI(0300)#PCI(0000)#PCI(0800)#PCI(0000)"`。  場所のパスの詳細については、「[個別のデバイスの割り当てを使用したデバイスの展開の計画](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md)」を参照してください。

### <a name="disable-the-device"></a>デバイスを無効にする
デバイスマネージャーまたは PowerShell を使用して、デバイスが "無効" になっていることを確認します。  

### <a name="dismount-the-device"></a>デバイスのマウントを解除する
ベンダーが軽減ドライバーを提供したかどうかによって、"-force" オプションを使用する必要があります。
- 軽減ドライバーがインストールされている場合
  ```
  Dismount-VMHostAssignableDevice -LocationPath $locationPath
  ```
- 軽減ドライバーがインストールされていない場合
  ```
  Dismount-VMHostAssignableDevice -force -LocationPath $locationPath
  ```

## <a name="assigning-the-device-to-the-guest-vm"></a>ゲスト VM へのデバイスの割り当て
最後の手順では、VM がデバイスにアクセスできる必要があることを Hyper-v に指示します。  上に示した場所のパスに加えて、vm の名前を把握しておく必要があります。

```
Add-VMAssignableDevice -LocationPath $locationPath -VMName VMName
```

## <a name="whats-next"></a>次の課題
デバイスが VM に正常にマウントされると、その VM を起動して、ベアメタルシステムで実行されていた場合と同じように、通常どおりにデバイスと対話できるようになります。  これにより、ハードウェアベンダーのドライバーを VM にインストールできるようになり、アプリケーションはそのハードウェアが存在することを確認できるようになります。  これを確認するには、ゲスト VM でデバイスマネージャーを開き、ハードウェアが表示されていることを確認します。

## <a name="removing-a-device-and-returning-it-to-the-host"></a>デバイスを削除してホストに戻す
デバイスを元の状態に戻す場合は、VM を停止し、次のものを発行する必要があります。
```
#Remove the device from the VM
Remove-VMAssignableDevice -LocationPath $locationPath -VMName VMName
#Mount the device back in the host
Mount-VMHostAssignableDevice -LocationPath $locationPath
```
デバイスマネージャーでデバイスを再度有効にすると、ホストオペレーティングシステムがデバイスと再び対話できるようになります。

## <a name="example"></a>例

### <a name="mounting-a-gpu-to-a-vm"></a>GPU を VM にマウントする
この例では、PowerShell を使用して "ddatest1" という名前の VM を構成し、製造元の NVIDIA が使用できる最初の GPU を取得して VM に割り当てます。  
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

## <a name="troubleshooting"></a>トラブルシューティング

GPU を VM に渡したが、リモートデスクトップまたはアプリケーションが GPU を認識していない場合は、次の一般的な問題を確認してください。

- GPU ベンダーがサポートしているドライバーの最新バージョンがインストールされていること、およびデバイスマネージャーでデバイスの状態を確認することで、ドライバーがエラーを報告していないことを確認します。
- デバイスに、VM 内に割り当てられている MMIO 領域が十分にあることを確認します。 詳細については、「 [MMIO Space](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md#mmio-space)」を参照してください。
- この構成で使用されているベンダーがサポートしている GPU を使用していることを確認します。 たとえば、一部のベンダーでは、VM に渡されたときにコンシューマーカードが動作しなくなります。
- 実行中のアプリケーションが VM 内での実行をサポートしていること、および GPU とそれに関連付けられているドライバーの両方がアプリケーションでサポートされていることを確認します。 一部のアプリケーションでは、Gpu と環境のリストが許可されています。
- ゲストでリモートデスクトップセッションホストの役割または Windows Multipoint Services を使用している場合は、特定のグループポリシーエントリが既定の GPU の使用を許可するように設定されていることを確認する必要があります。 ゲスト (またはゲストのローカルグループポリシーエディター) に適用されているグループポリシーオブジェクトを使用して、次のグループポリシー項目に移動します。**コンピューターの構成** > **管理者テンプレート** > **Windows コンポーネント** ** > リモートデスクトップサービス > リモートデスクトップセッションホスト** **リモートセッション環境** > **すべての > セッションでハードウェアの既定のグラフィックスアダプターを使用** **リモートデスクトップサービス。** ポリシーが適用されたら、この値を [有効] に設定し、VM を再起動します。
