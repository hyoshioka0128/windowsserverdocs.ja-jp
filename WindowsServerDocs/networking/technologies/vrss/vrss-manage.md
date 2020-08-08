---
title: vRSS の管理
description: このトピックでは、Windows PowerShell コマンドを使用して、仮想マシン (Vm) および Hyper-v ホストで vRSS を管理します。
ms.topic: article
ms.assetid: 0fe5bfc3-591f-4a19-b98a-0668d4c9f93a
ms.localizationpriority: medium
manager: dougkim
ms.date: 09/05/2018
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 553be94dd3fe94a74ee9deb84a5ac6d47265afec
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87955539"
---
# <a name="manage-vrss"></a>vRSS の管理

このトピックでは、Windows PowerShell コマンドを使用して、仮想マシン \( vm と hyper-v ホストで vRSS を管理し \) \- ます。

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

Hyper-v ホストでは、Hyper-v 仮想スイッチポートで vRSS も有効にする必要があり \- ます。

**現在の設定を表示します。**

```PowerShell
Get-VMNetworkAdapter <vm-name> | fl

Get-VMNetworkAdapter -ManagementOS | fl
```

次の設定はどちらも**True**にする必要があります。

- VrssEnabledRequested: True
- VrssEnabled: True

>[!IMPORTANT]
>一部のリソース制限条件では、Hyper-v \- 仮想スイッチポートでこの機能を有効にできない場合があります。 これは一時的な状態であり、今後この機能を使用できるようになる可能性があります。
>
>**Vrssenabled**が**True**の場合、この機能はこの \- VM または vNIC の hyper-v 仮想スイッチポートに対して有効になります。

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
> VM 内でプロファイルを設定しても、作業のスケジュールには影響しません。 Hyper-v \- は、すべてのスケジューリングの決定を行い、VM 内のプロファイルを無視します。

## <a name="disable-vrss"></a>VRSS を無効にする

以前に説明した設定をすべて無効にするには、vRSS を無効にします。

- 物理 NIC または VM の VMQ を無効にします。

  >[!CAUTION]
  >物理 NIC で VMQ を無効にすると、Hyper-v ホストが \- 着信パケットを処理する機能に深刻な影響を及ぼします。

- Hyper-v ホストの Hyper-v 仮想スイッチポートで、VM の vRSS を無効に \- \- します。

   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssEnabled $FALSE
   ```

- Hyper-v ホストの Hyper-v 仮想スイッチポートで、ホスト vNIC の vRSS を無効に \- \- します。

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssEnabled $FALSE
   ```

- Vm 内、または \( \) ホスト上のホスト VNIC で RSS を無効にする \(\)

   ```PowerShell
   Disable-NetAdapterRSS *
   ```
