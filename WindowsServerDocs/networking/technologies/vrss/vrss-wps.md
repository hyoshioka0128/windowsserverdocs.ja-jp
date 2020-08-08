---
title: RSS および vRSS 用の Windows PowerShell コマンド
description: このトピックでは、Receive Side Scaling (RSS) と仮想 RSS (vRSS) 用の Windows PowerShell コマンドに関するテクニカルリファレンス情報をすばやく見つける方法について説明します。
ms.topic: article
ms.assetid: 49e93b9f-46d9-4cee-bcda-1c4634893ddd
ms.localizationpriority: medium
manager: dougkim
ms.author: lizross
author: eross-msft
ms.date: 09/05/2018
ms.openlocfilehash: 424344147ff926694709aa60fbf57380fbbf665b
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87996405"
---
# <a name="windows-powershell-commands-for-rss-and-vrss"></a>RSS および vRSS 用の Windows PowerShell コマンド

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、Receive Side Scaling \( RSS \) および virtual RSS vRSS 用の Windows PowerShell コマンドに関するテクニカルリファレンス情報をすばやく見つける方法について説明し \( \) ます。

複数のプロセッサまたは複数のコアを持つ物理コンピューターで RSS を構成するには、次の RSS コマンドを使用します。 \( \) サポートされているオペレーティングシステムを実行している仮想マシン VM で、同じコマンドを使用して vRSS を構成できます。 詳細については、「 [Windows PowerShell のネットワークアダプターコマンドレット](/powershell/module/netadapter/?view=win10-ps)」を参照してください。

## <a name="configure-vmq"></a>VMQ の構成

vRSS を使用するには、VMQ が有効で構成されている必要があります。 次の Windows PowerShell コマンドを使用して、VMQ 設定を管理できます。

- [Get-netadaptervmq](/powershell/module/netadapter/disable-netadaptervmq?view=win10-ps)
- [Get-netadaptervmq](/powershell/module/netadapter/enable-netadaptervmq?view=win10-ps)
- [Get-netadaptervmq](/powershell/module/netadapter/get-netadaptervmq?view=win10-ps)
- [Get-netadaptervmq](/powershell/module/netadapter/set-netadaptervmq?view=win10-ps)

## <a name="enable-and-configure-rss-on-a-native-host"></a>ネイティブホストで RSS を有効にして構成する

次の PowerShell コマンドを使用して、ネイティブホストで RSS を構成し、VM またはホスト仮想 NIC (vNIC) で RSS を管理します。 これらのコマンドのパラメーターの一部は、Hyper-v ホストの仮想マシンキュー VMQ にも影響を与える可能性があり \( \) ます。

>[!IMPORTANT]
>VRSS を有効にして使用するには、VM またはホスト vNIC で RSS を有効にする必要があります。

- [Set-netadapterrss](/powershell/module/netadapter/disable-netadapterrss?view=win10-ps)
- [Set-netadapterrss](/powershell/module/netadapter/enable-netadapterrss?view=win10-ps)
- [Set-netadapterrss](/powershell/module/netadapter/get-netadapterrss?view=win10-ps)
- [Set-netadapterrss](/powershell/module/netadapter/Set-NetAdapterRss?view=win10-ps)

## <a name="enable-vrss-on-the-hyper-v-virtual-switch-port"></a>Hyper-v 仮想スイッチポートでの vRSS の有効化 \-

VRSS では、VM で RSS を有効にするだけでなく、Hyper-v 仮想スイッチポートで vRSS を有効にする必要があり \- ます。

VRSS の現在の設定を確認し、VM の機能を有効または無効にします。

   **現在の設定を表示します。**

   ```PowerShell
   Get-VMNetworkAdapter <vm-name> | fl
   ```

   **機能を有効にします。**

   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssEnabled [$True|$False]
   ```

## <a name="enable-or-disable-vrss-on-a-host-vnic"></a>ホスト vNIC での vRSS の有効化または無効化

VRSS の現在の設定を確認し、ホスト vNIC の機能を有効または無効にします。

   **現在の設定を表示します。**

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS | fl
   ```

   **機能を有効または無効にします。**

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssEnabled [$True|$False]
   ```

## <a name="configure-the-scheduling-mode-on-the-hyper-v-virtual-switch-port"></a>Hyper-v 仮想スイッチポートでスケジュールモードを構成する
>適用対象:Windows Server 2019

Windows Server 2019 では、vRSS はネットワークトラフィックを動的に処理するために使用する論理プロセッサを更新できます。  ドライバーがサポートされているデバイスでは、このスケジュールモードが既定で有効になっています。

システムの現在のスケジューリングモードを確認するか、VM のスケジュールモードを変更します。

   **現在の設定を表示します。**

   ```PowerShell
   Get-VMNetworkAdapter <vm-name> | Select 'VRSSQueue'
   ```

   **スケジュールモードを設定または変更します。**

   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssQueueSchedulingMode [Dynamic|$StaticVrss|StaticVMQ]
   ```

## <a name="configure-the-scheduling-mode-on-a-host-vnic"></a>ホスト vNIC でスケジュールモードを構成する
>適用対象:Windows Server 2019

現在のスケジュールモードを確認したり、ホスト vNIC のスケジュールモードを変更したりするには、次の Windows PowerShell コマンドを使用します。

   **現在の設定を表示します。**

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS | Select 'VRSSQueue'
   ```

   **スケジュールモードを設定または変更します。**

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssQueueSchedulingMode -VrssQueueSchedulingMode [Dynamic|$StaticVrss|StaticVMQ]
   ```


## <a name="related-topics"></a>関連トピック
詳細については、次の参照トピックを参照してください。

- [VMNetworkAdapter](/powershell/module/hyper-v/get-vmnetworkadapter?view=win10-ps)
- [Set-VMNetworkAdapter](/powershell/module/hyper-v/set-vmnetworkadapter?view=win10-ps)

詳細については、「[仮想 Receive Side Scaling (vRSS)](vrss-top.md)」を参照してください。