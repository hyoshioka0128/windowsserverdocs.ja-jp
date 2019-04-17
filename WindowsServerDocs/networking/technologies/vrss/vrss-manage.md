---
title: VRSS を管理します。
description: このトピックでは、Windows PowerShell コマンドを使用する、vRSS 仮想マシン (Vm) であり、HYPER-V ホストを管理します。
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
ms.sourcegitcommit: e84e328c13a701e8039b16a4824a6e58a6e59b0b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2018
ms.locfileid: "4133838"
---
# VRSS を管理します。

このトピックでは、Windows PowerShell コマンドを使用する、vRSS で hyper \-v ホストと仮想マシン \(VMs\) を管理します。

>[!NOTE]
>このトピックに記載されているコマンドの詳細については、 [RSS や vRSS 用の Windows PowerShell コマンド](vrss-wps.md)を参照してください。

## HYPER-V ホスト上の VMQ

HYPER-V ホストでは、VMQ プロセッサを制御するキーワードを使う必要があります。

**現在の設定を表示するには。** 

```PowerShell
Get-NetAdapterVmq
```

**VMQ 設定を構成します。** 

```PowerShell
Set-NetAdapterVmq
```


## HYPER-V で vRSS スイッチ ポート

HYPER-V ホストでは、hyper \-v 仮想スイッチ ポートで vRSS も有効にする必要があります。

**現在の設定を表示するには。**

```PowerShell
Get-VMNetworkAdapter <vm-name> | fl

Get-VMNetworkAdapter -ManagementOS | fl
```
    
**True**の両方の次の設定があります。 

- VrssEnabledRequested: True
- VrssEnabled: True
    
>[!IMPORTANT]
>一部のリソース制限条件下で、hyper \-v 仮想スイッチ ポートできないことがありますがこの機能を有効にします。 これは、一時的な状態であり、後続の時点で、この機能が利用可能ななる可能性があります。
>
>**VrssEnabled**が**True**のかどうか、この hyper \-v 仮想スイッチ ポートの機能が有効になっている、つまり、この VM または vNIC のします。

**スイッチ ポート vRSS 設定を構成します。**

```PowerShell
Set-VMNetworkAdapter <vm-name> -VrssEnabled $TRUE
    
Set-VMNetworkAdapter -ManagementOS -VrssEnabled $TRUE
```

## 仮想マシンとホストの Vnic vRSS

ネイティブ RSS はホスト Vnic で RSS を有効にするための方法でも仮想マシンとホストの Vnic vRSS 設定を構成するために使用する同じコマンドを使用することができます。  

**現在の設定を表示するには。**

```PowerShell
Get-NetAdapterRSS
```

**VRSS 設定を構成します。**

```PowerShell
Set-NetAdapterRss
```

>[!NOTE]
> VM 内部のプロファイルの設定には影響しません作業をスケジュールします。 Hyper \-v は、すべてのスケジュールの決定し、VM 内部のプロファイルを無視します。

## VRSS を無効にします。

前述の設定を無効にする vRSS を無効にすることができます。

- 物理 NIC または VM VMQ を無効にします。

  >[!CAUTION]
  >物理的な VMQ を無効にする NIC 深刻な影響 hyper \-v ホストの受信パケットを処理します。

- Hyper \-v ホスト上の hyper \-v 仮想スイッチ ポートでの VM の vRSS を無効にします。

   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssEnabled $FALSE
   ```

- Hyper \-v ホスト上の hyper \-v 仮想スイッチ ポートでホスト vNIC を vRSS を無効にします。

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssEnabled $FALSE
   ```

- VM の RSS を無効にする \(or host vNIC\)、VM 内部の \ (または、host\)

   ```PowerShell
   Disable-NetAdapterRSS *
   ```
