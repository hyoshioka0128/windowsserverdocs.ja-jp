---
title: RSS および vRSS 用の Windows PowerShell コマンド
description: このトピックでは、受信側のスケーリング (RSS) や仮想 RSS (vRSS) の Windows PowerShell コマンドに関するテクニカル リファレンス情報をすばやく検索する方法について説明します。
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
ms.sourcegitcommit: 9ed4c9fe04ebf3ef488170503c9a354c992b6fde
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/03/2018
ms.locfileid: "4339270"
---
# RSS および vRSS 用の Windows PowerShell コマンド

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、すばやく Receive Side Scaling \(RSS\) および仮想 RSS \(vRSS\) 向けの Windows PowerShell コマンドに関するテクニカル リファレンス情報を検索する方法について説明します。

複数のプロセッサまたは複数のコアを物理コンピューター上の RSS を構成するのにには、次の RSS コマンドを使用します。 同じコマンドを使用して仮想マシンで vRSS を構成することができますが、サポートされているオペレーティング システムが実行されている \(VM\) します。 詳細については、 [Windows PowerShell でのネットワーク アダプター コマンドレット](https://docs.microsoft.com/powershell/module/netadapter/?view=win10-ps)を参照してください。

## VMQ を構成します。

vRSS は VMQ が有効にして構成する必要があります。 次の Windows PowerShell コマンドを使用して、VMQ 設定を管理することができます。

- [無効にする NetAdapterVmq](https://docs.microsoft.com/powershell/module/netadapter/disable-netadaptervmq?view=win10-ps)
- [有効にする NetAdapterVmq](https://docs.microsoft.com/powershell/module/netadapter/enable-netadaptervmq?view=win10-ps)
- [Get NetAdapterVmq](https://docs.microsoft.com/powershell/module/netadapter/get-netadaptervmq?view=win10-ps)
- [セット NetAdapterVmq](https://docs.microsoft.com/powershell/module/netadapter/set-netadaptervmq?view=win10-ps)

## 有効にして、ネイティブのホスト上の RSS の構成

次の PowerShell コマンドを使用してネイティブ ホスト上の RSS を構成したり、管理 RSS VM またはホスト仮想 NIC (vNIC)。 HYPER-V ホストの仮想マシンのキュー \(VMQ\) にも影響いくつかの次のコマンドのパラメーターがあります。  

>[!IMPORTANT]
>有効にして、vRSS を使用するための前提条件の RSS VM またはホスト vNIC を有効です。

- [無効にする NetAdapterRss](https://docs.microsoft.com/powershell/module/netadapter/disable-netadapterrss?view=win10-ps)
- [有効にする NetAdapterRss](https://docs.microsoft.com/powershell/module/netadapter/enable-netadapterrss?view=win10-ps)
- [Get NetAdapterRss](https://docs.microsoft.com/powershell/module/netadapter/get-netadapterrss?view=win10-ps)
- [セット NetAdapterRss](https://docs.microsoft.com/powershell/module/netadapter/Set-NetAdapterRss?view=win10-ps)

## Hyper \-v 仮想スイッチ ポートで vRSS を有効にします。

VM の RSS を有効にするだけでなく vRSS では、hyper \-v 仮想スイッチ ポートで vRSS を有効にする必要があります。 

VRSS に存在する設定を判断し、有効または VM の機能を無効にします。

   **現在の設定を表示するには。** 

   ```PowerShell
   Get-VMNetworkAdapter <vm-name> | fl
   ```

   **この機能を有効になります。**
   
   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssEnabled [$True|$False]
   ```

## 有効または無効にホスト vNIC vRSS

VRSS に存在する設定を判断し、有効またはホスト vNIC の機能を無効にします。

   **現在の設定を表示するには。** 

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS | fl
   ```

   **有効にするか、機能を無効にします。** 

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssEnabled [$True|$False]
   ```

## HYPER-V 仮想スイッチ ポートでスケジュール設定のモードを構成します。 
>適用対象: Windows Server 2019

Windows Server 2019 vRSS は動的にネットワーク トラフィックを処理するために使用する論理プロセッサを更新できます。  サポートされているドライバーのデバイスには、既定で有効になっているこのスケジュール モードがあります。 

VM のスケジュール設定のモードを変更するか、システムに存在するスケジュール モードのかを決定します。

   **現在の設定を表示するには。** 

   ```PowerShell
   Get-VMNetworkAdapter <vm-name> | Select 'VRSSQueue'
   ```

   **設定またはスケジュール設定のモードを変更します。**

   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssQueueSchedulingMode [Dynamic|$StaticVrss|StaticVMQ]
   ```

## ホスト vNIC をスケジュール設定のモードを構成します。
>適用対象: Windows Server 2019

存在するスケジュール モードを判断する、またはホスト vNIC のスケジュール設定のモードを変更するには、次の Windows PowerShell コマンドを使用します。

   **現在の設定を表示するには。** 

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS | Select 'VRSSQueue'
   ```

   **設定またはスケジュール設定のモードを変更します。** 

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssQueueSchedulingMode -VrssQueueSchedulingMode [Dynamic|$StaticVrss|StaticVMQ]
   ```


## 関連トピック 
詳細については、次のリファレンス トピックを参照してください。

- [Get VMNetworkAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/get-vmnetworkadapter)
- [セット VMNetworkAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/set-vmnetworkadapter)

詳細については、 [Virtual Receive Side Scaling (vRSS)](vrss-top.md)を参照してください。