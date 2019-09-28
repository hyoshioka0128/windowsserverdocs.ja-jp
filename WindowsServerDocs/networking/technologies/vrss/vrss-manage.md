---
title: vRSS の管理
description: このトピックでは、Windows PowerShell コマンドを使用して、仮想マシン (Vm) および Hyper-v ホストで vRSS を管理します。
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 0fe5bfc3-591f-4a19-b98a-0668d4c9f93a
ms.localizationpriority: medium
manager: dougkim
ms.date: 09/05/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9d528f7e658d61f613eedc635fb81d8f18fd59aa
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405166"
---
# <a name="manage-vrss"></a>vRSS の管理

このトピックでは、Windows PowerShell コマンドを使用して、仮想マシン @no__t 0VMs @ no__t とハイパー @ no__t-2V ホストで vRSS を管理します。

>[!NOTE]
>このトピックに記載されているコマンドの詳細については、「 [RSS および vRSS 用の Windows PowerShell コマンド](vrss-wps.md)」を参照してください。

## <a name="vmq-on-hyper-v-hosts"></a>Hyper-v ホスト上の VMQ

Hyper-v ホストでは、VMQ プロセッサを制御するキーワードを使用する必要があります。

**現在の設定を表示します。** 

```PowerShell
Get-NetAdapterVmq
```

**VMQ の設定を構成します。** 

```PowerShell
Set-NetAdapterVmq
```


## <a name="vrss-on-hyper-v-switch-ports"></a>Hyper-v スイッチポートでの vRSS

Hyper-v ホストでは、Hyper-v 仮想スイッチポートで vRSS を有効にする必要もあります。

**現在の設定を表示します。**

```PowerShell
Get-VMNetworkAdapter <vm-name> | fl

Get-VMNetworkAdapter -ManagementOS | fl
```
    
次の設定はどちらも**True**にする必要があります。 

- VrssEnabledRequested:True
- VrssEnabled:True
    
>[!IMPORTANT]
>一部のリソース制限条件では、ハイパー @ no__t-0V 仮想スイッチポートでこの機能を有効にできないことがあります。 これは一時的な状態であり、今後この機能を使用できるようになる可能性があります。
>
>**Vrssenabled**が**True**の場合、この機能はこのハイパー @ No__t-2v 仮想スイッチポート (つまり、この VM または vNIC) で有効になります。

**スイッチポート vRSS 設定を構成します。**

```PowerShell
Set-VMNetworkAdapter <vm-name> -VrssEnabled $TRUE
    
Set-VMNetworkAdapter -ManagementOS -VrssEnabled $TRUE
```

## <a name="vrss-in-vms-and-host-vnics"></a>Vm とホスト vNICs の vRSS

ネイティブ RSS で使用するのと同じコマンドを使用して、Vm とホスト vNICs で vRSS 設定を構成することもできます。これは、ホスト vNICs で RSS を有効にする方法でもあります。  

**現在の設定を表示します。**

```PowerShell
Get-NetAdapterRSS
```

**VRSS 設定を構成します。**

```PowerShell
Set-NetAdapterRss
```

>[!NOTE]
> VM 内でプロファイルを設定しても、作業のスケジュールには影響しません。 ハイパー @ no__t-0V はすべてのスケジューリングの決定を行い、VM 内のプロファイルを無視します。

## <a name="disable-vrss"></a>VRSS を無効にする

以前に説明した設定をすべて無効にするには、vRSS を無効にします。

- 物理 NIC または VM の VMQ を無効にします。

  >[!CAUTION]
  >物理 NIC で VMQ を無効にすると、受信パケットを処理するハイパー @ no__t-0V ホストの機能に深刻な影響が及びます。

- ハイパー @ no__t-1V ホストのハイパー @ no__t-0V 仮想スイッチポートで、VM の vRSS を無効にします。

   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssEnabled $FALSE
   ```

- Hyper-v ホスト上のハイパー @ no__t-0V 仮想スイッチポートで、ホスト vNIC の vRSS を無効にします。

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssEnabled $FALSE
   ```

- Vm で RSS を無効にするか、ホスト vNIC @ no__t を @no__t VM 内 @no__t で無効にするか、ホスト @ no__t-3 を使用します。

   ```PowerShell
   Disable-NetAdapterRSS *
   ```
