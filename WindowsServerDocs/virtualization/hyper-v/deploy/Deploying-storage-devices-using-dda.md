---
title: 個別のデバイスの割り当てを使用して、NVMe ストレージ デバイスをデプロイします。
description: DDA を使用して、ストレージ デバイスをデプロイする方法について説明します
ms.prod: windows-server-threshold
ms.service: na
ms.technology: hyper-v
ms.tgt_pltfrm: na
ms.topic: article
author: chrishuybregts
ms.author: chrihu
ms.assetid: 1c36107e-78c9-4ec0-a313-6ed557ac0ffc
ms.openlocfilehash: d6fe54789d37386d5dc782ef8a2ca26b47adc69e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841363"
---
# <a name="deploy-nvme-storage-devices-using-discrete-device-assignment"></a>個別のデバイスの割り当てを使用して、NVMe ストレージ デバイスをデプロイします。

>適用先:Microsoft HYPER-V Server 2016、Windows Server 2016

Windows Server 2016 以降では、VM に PCIe デバイス全体を渡すの個別のデバイスの割り当てまたは DDA を使用できます。  これにより、ネイティブのデバイス ドライバーを利用している間に NVMe ストレージまたは VM 内からのグラフィックス カードなどのデバイスへのアクセスを高パフォーマンスをできます。  参照してください、[個別のデバイスの割り当てを使用して展開するデバイスの計画](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md)デバイス作業について詳しくは、可能なセキュリティへの影響など、どのような。DDA でデバイスを使用する 3 つの手順があります。
-   DDA の VM を構成します。
-   パーティションをホストからデバイスのマウントを解除します。
-   ゲスト VM へのデバイスの割り当てください。

すべてのコマンドは、管理者として Windows PowerShell コンソールでのホストに実行できます。

## <a name="configure-the-vm-for-dda"></a>DDA の VM を構成します。
個別のデバイスの割り当ては、Vm にいくつかの制限を適用し、次の手順を実行する必要があります。

1.  実行して、「自動停止アクション」、vm をオフを構成します。

```
Set-VM -Name VMName -AutomaticStopAction TurnOff
```

## <a name="dismount-the-device-from-the-host-partition"></a>パーティションをホストからデバイスのマウントを解除します。

### <a name="locating-the-devices-location-path"></a>デバイスの場所のパスを検索します。
マウントを解除して、ホストからデバイスをマウントするには、PCI 場所のパスが必要です。  場所のパスの例は、次のように:`"PCIROOT(20)#PCI(0300)#PCI(0000)#PCI(0800)#PCI(0000)"`します。   配置の詳細について、場所のパスはご覧ください。[個別のデバイスの割り当てを使用して展開するデバイスの計画](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md)します。

### <a name="disable-the-device"></a>デバイスを無効にします。
デバイス マネージャーまたは PowerShell を使用して、デバイスが"無効にしてください"  

### <a name="dismount-the-device"></a>デバイスのマウントを解除します。
```
Dismount-VMHostAssignableDevice -LocationPath $locationPath
```

## <a name="assigning-the-device-to-the-guest-vm"></a>ゲスト VM へのデバイスの割り当てください。
最後の手順では、VM が存在するように、デバイスへのアクセスを HYPER-V に連絡します。  上記で見つかった場所のパス、だけでなく、vm の名前を知っている必要があります。

```
Add-VMAssignableDevice -LocationPath $locationPath -VMName VMName
```

## <a name="whats-next"></a>次の内容
VM で、デバイスが正常にマウントされると、その VM を起動し、ベア メタル システムを実行していた場合通常と同様に、デバイスと対話できるようになりました。  これを確認するには、ゲスト VM でデバイス マネージャーを開き、表示、ハードウェアは、に表示されます。

## <a name="removing-a-device-and-returning-it-to-the-host"></a>デバイスを削除して、ホストに戻す
その元の状態にはデバイスを返す場合は、VM を停止し、次を発行する必要があります。
```
#Remove the device from the VM
Remove-VMAssignableDevice -LocationPath $locationPath -VMName VMName
#Mount the device back in the host
Mount-VMHostAssignableDevice -LocationPath $locationPath
```
できますし、再度有効にするデバイス マネージャーでデバイスと、ホスト オペレーティング システムをもう一度、デバイスと対話することになります。
