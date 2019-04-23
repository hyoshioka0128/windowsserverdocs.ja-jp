---
title: vRSS の管理
description: このトピックでは、vRSS で仮想マシン (Vm) と、HYPER-V ホストを管理するのに、Windows PowerShell コマンドを使用します。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 0fe5bfc3-591f-4a19-b98a-0668d4c9f93a
ms.localizationpriority: medium
manager: dougkim
ms.date: 09/05/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8af800608bee7037b48141a7a2edb0c872a7aac0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856193"
---
# <a name="manage-vrss"></a>vRSS の管理

このトピックでは、仮想マシンで vRSS を管理する Windows PowerShell コマンドを使用する\(Vm\)とハイパー\-V ホスト。

>[!NOTE]
>このトピックで説明されているコマンドの詳細については、次を参照してください。 [RSS および vRSS 用 Windows PowerShell コマンド](vrss-wps.md)します。

## <a name="vmq-on-hyper-v-hosts"></a>HYPER-V ホストで VMQ

HYPER-V ホストで、VMQ プロセッサを制御するキーワードを使用する必要があります。

**現在の設定を表示するには。** 

```PowerShell
Get-NetAdapterVmq
```

**VMQ 設定を構成するには。** 

```PowerShell
Set-NetAdapterVmq
```


## <a name="vrss-on-hyper-v-switch-ports"></a>vRSS hyper-v スイッチ ポート

HYPER-V ホスト上も、ハイパースレッディングで vRSS を有効にする必要があります\-V 仮想スイッチ ポート。

**現在の設定を表示するには。**

```PowerShell
Get-VMNetworkAdapter <vm-name> | fl

Get-VMNetworkAdapter -ManagementOS | fl
```
    
次の設定の両方にする必要があります**True**します。 

- VrssEnabledRequested:True
- VrssEnabled:True
    
>[!IMPORTANT]
>一部のリソース制限条件、Hyper \-V 仮想スイッチ ポートがこの機能を有効にすることがない可能性があります。 これは、一時的な状態であり、後続時に、機能が利用可能ななる可能性があります。
>
>場合**VrssEnabled**は**True**、機能がこのハイパースレッディングを有効にし、\-V 仮想スイッチ ポート-は、この VM または vNIC します。

**スイッチ ポート vRSS 設定を構成するには。**

```PowerShell
Set-VMNetworkAdapter <vm-name> -VrssEnabled $TRUE
    
Set-VMNetworkAdapter -ManagementOS -VrssEnabled $TRUE
```

## <a name="vrss-in-vms-and-host-vnics"></a>Vm とホスト Vnic で vRSS

これはホスト Vnic で RSS を有効にする方法でも Vm とホストの Vnic で vRSS 設定を構成するネイティブ RSS に使用される同じコマンドを使用することができます。  

**現在の設定を表示するには。**

```PowerShell
Get-NetAdapterRSS
```

**VRSS 設定を構成するには。**

```PowerShell
Set-NetAdapterRss
```

>[!NOTE]
> VM 内でのプロファイルを設定では、作業のスケジュール設定、影響はありません。 ハイパー\-V は、すべての決定、スケジュール設定、および VM 内でプロファイルを無視します。

## <a name="disable-vrss"></a>VRSS を無効にします。

前に説明した設定を無効にする vRSS を無効にすることができます。

- 物理 NIC または VM VMQ が無効にします。

  >[!CAUTION]
  >物理 VMQ を無効にする NIC 深刻な影響が出ること、ハイパースレッディング\-受信パケットを処理するためにホストを展開します。

- Hyper マシンに対する vRSS を無効にする\-Hyper V の仮想スイッチ ポート\-V ホスト。

   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssEnabled $FALSE
   ```

- VRSS ホスト vNIC をハイパースレッディングを無効にする\-Hyper V の仮想スイッチ ポート\-V ホスト。

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssEnabled $FALSE
   ```

- VM で RSS を無効にする\(またはホスト vNIC\) 、VM 内で\(または、ホスト\)

   ```PowerShell
   Disable-NetAdapterRSS *
   ```
