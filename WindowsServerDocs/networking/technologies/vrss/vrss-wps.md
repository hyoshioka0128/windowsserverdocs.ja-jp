---
title: RSS および vRSS 用 Windows PowerShell コマンド
description: このトピックでは、Receive Side Scaling (RSS) と仮想 RSS (vRSS) の Windows PowerShell コマンドに関するテクニカル リファレンス情報をすばやく検索する方法について説明します。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 49e93b9f-46d9-4cee-bcda-1c4634893ddd
ms.localizationpriority: medium
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/05/2018
ms.openlocfilehash: 10039388009e32c10d71067b835bad65db5607ef
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833263"
---
# <a name="windows-powershell-commands-for-rss-and-vrss"></a>RSS および vRSS 用 Windows PowerShell コマンド

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは、Receive Side Scaling の Windows PowerShell コマンドに関するテクニカル リファレンス情報をすばやく検索する方法について説明します\(RSS\)および仮想 RSS \(vRSS\)します。

複数のプロセッサまたは複数のコアを持つ物理コンピューターで RSS を構成するのにには、次の RSS コマンドを使用します。 同じコマンドを使用するには、仮想マシンで vRSS を構成する\(VM\)サポートされるオペレーティング システムが実行されています。 詳細については、次を参照してください。 [Windows PowerShell のネットワーク アダプター コマンドレット](https://docs.microsoft.com/powershell/module/netadapter/?view=win10-ps)します。

## <a name="configure-vmq"></a>VMQ を構成します。

vRSS では、VMQ が有効にされ構成されている必要があります。 次の Windows PowerShell コマンドを使用して、VMQ 設定を管理することができます。

- [Disable-NetAdapterVmq](https://docs.microsoft.com/powershell/module/netadapter/disable-netadaptervmq?view=win10-ps)
- [Enable-NetAdapterVmq](https://docs.microsoft.com/powershell/module/netadapter/enable-netadaptervmq?view=win10-ps)
- [Get-NetAdapterVmq](https://docs.microsoft.com/powershell/module/netadapter/get-netadaptervmq?view=win10-ps)
- [Set-NetAdapterVmq](https://docs.microsoft.com/powershell/module/netadapter/set-netadaptervmq?view=win10-ps)

## <a name="enable-and-configure-rss-on-a-native-host"></a>有効にして、RSS をネイティブ ホストの構成

ネイティブ ホスト上で RSS を構成できるだけでなく、RSS、VM またはホストを管理する次の PowerShell コマンドを使用して、仮想 NIC (vNIC)。 仮想マシン キューに影響する可能性もこれらのコマンドのパラメーターのいくつか\(VMQ\)で HYPER-V ホスト。  

>[!IMPORTANT]
>有効にして、vRSS を使用するための前提条件は、VM またはホスト vNIC の RSS を有効にします。

- [Disable-NetAdapterRss](https://docs.microsoft.com/powershell/module/netadapter/disable-netadapterrss?view=win10-ps)
- [Enable-NetAdapterRss](https://docs.microsoft.com/powershell/module/netadapter/enable-netadapterrss?view=win10-ps)
- [Get-NetAdapterRss](https://docs.microsoft.com/powershell/module/netadapter/get-netadapterrss?view=win10-ps)
- [Set-NetAdapterRss](https://docs.microsoft.com/powershell/module/netadapter/Set-NetAdapterRss?view=win10-ps)

## <a name="enable-vrss-on-the-hyper-v-virtual-switch-port"></a>Hyper で vRSS を有効にする\-V 仮想スイッチ ポート

VRSS が Hyper で vRSS を有効にすることを必要、VM で RSS を有効にするだけでなく\-V 仮想スイッチ ポート。 

VRSS の現在の設定を確認および有効または VM の機能を無効にします。

   **現在の設定を表示するには。** 

   ```PowerShell
   Get-VMNetworkAdapter <vm-name> | fl
   ```

   **この機能を有効になります。**
   
   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssEnabled [$True|$False]
   ```

## <a name="enable-or-disable-vrss-on-a-host-vnic"></a>有効にするか、ホスト vNIC で vRSS を無効にします。

VRSS、存在する設定を確認および有効またはホスト vNIC の機能を無効にします。

   **現在の設定を表示するには。** 

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS | fl
   ```

   **有効または無効にします。** 

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssEnabled [$True|$False]
   ```

## <a name="configure-the-scheduling-mode-on-the-hyper-v-virtual-switch-port"></a>HYPER-V 仮想スイッチ ポートでスケジュール モードを構成します。 
>適用対象:Windows Server 2019

Windows Server の 2019 vRSS は動的にネットワーク トラフィックの処理に使用される論理プロセッサを更新できます。  サポートされているドライバーとデバイスには、既定で有効になっているこのスケジュールのモードがあります。 

システムでは、存在するスケジュール モードの決定または VM のスケジュールのモードを変更します。

   **現在の設定を表示するには。** 

   ```PowerShell
   Get-VMNetworkAdapter <vm-name> | Select 'VRSSQueue'
   ```

   **設定またはスケジュール モードを変更します。**

   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssQueueSchedulingMode [Dynamic|$StaticVrss|StaticVMQ]
   ```

## <a name="configure-the-scheduling-mode-on-a-host-vnic"></a>ホスト vNIC のスケジューリングのモードを構成します。
>適用対象:Windows Server 2019

存在するスケジュール モードの決定、またはホスト vNIC のスケジューリングのモードを変更するには、次の Windows PowerShell コマンドを使用します。

   **現在の設定を表示するには。** 

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS | Select 'VRSSQueue'
   ```

   **設定またはスケジュール モードを変更します。** 

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssQueueSchedulingMode -VrssQueueSchedulingMode [Dynamic|$StaticVrss|StaticVMQ]
   ```


## <a name="related-topics"></a>関連トピック 
詳細については、次のリファレンス トピックを参照してください。

- [Get-VMNetworkAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/get-vmnetworkadapter)
- [Set-VMNetworkAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/set-vmnetworkadapter)

詳細については、次を参照してください。[仮想 Receive Side Scaling (vRSS)](vrss-top.md)します。