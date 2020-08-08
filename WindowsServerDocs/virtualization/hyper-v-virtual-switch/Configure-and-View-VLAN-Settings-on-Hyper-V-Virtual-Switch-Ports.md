---
title: Hyper-V 仮想スイッチ ポートで VLAN 設定を構成および表示する
description: このトピックでは、Windows Server 2016 の Hyper-v 仮想スイッチポートで仮想ローカルエリアネットワーク (VLAN) 設定を構成および表示するためのベストプラクティスについて説明します。
manager: brianlic
ms.topic: article
ms.assetid: 69e0e28a-98ae-4ade-bd27-ce2ad7eb310f
ms.author: lizross
author: eross-msft
ms.openlocfilehash: ac7d3f4ea17e35b42d974d1e29c692e8510c35ef
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87995693"
---
# <a name="configure-and-view-vlan-settings-on-hyper-v-virtual-switch-ports"></a>Hyper-V 仮想スイッチ ポートで VLAN 設定を構成および表示する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、Hyper-v 仮想スイッチポートで仮想ローカルエリアネットワーク (VLAN) の設定を構成および表示するためのベストプラクティスについて説明します。

Hyper-v 仮想スイッチポートで VLAN 設定を構成する場合は、Windows &reg; Server 2016 Hyper-v マネージャーまたは System Center Virtual Machine Manager (VMM) のいずれかを使用できます。

VMM を使用している場合、VMM は次の Windows PowerShell コマンドを使用してスイッチポートを構成します。

```
Set-VMNetworkAdapterIsolation <VM-name|-managementOS> -IsolationMode VLAN -DefaultIsolationID <vlan-value> -AllowUntaggedTraffic $True
```
VMM を使用せず、Windows Server のスイッチポートを構成する場合は、Hyper-v マネージャーコンソールまたは次の Windows PowerShell コマンドを使用できます。
```
Set-VMNetworkAdapterVlan <VM-name|-managementOS> -Access -VlanID <vlan-value>
```

Hyper-v 仮想スイッチポートで VLAN 設定を構成するには、これら2つの方法があります。スイッチポート設定を表示しようとすると、構成されていても、VLAN 設定が構成されていないと表示されることがあります。

## <a name="use-the-same-method-to-configure-and-view-switch-port-vlan-settings"></a>同じ方法を使用してスイッチポート VLAN 設定を構成および表示する

これらの問題が発生しないようにするには、スイッチポート VLAN 設定の構成に使用したスイッチポート VLAN 設定を表示するのと同じ方法を使用する必要があります。

VLAN スイッチのポート設定を構成および表示するには、次の操作を行う必要があります。

- VMM またはネットワークコントローラーを使用してネットワークを設定および管理していて、ソフトウェアによるネットワーク制御 (SDN) を展開している場合は、 **VMNetworkAdapterIsolation**コマンドレットを使用する必要があります。
- Windows Server 2016 Hyper-v マネージャーまたは Windows PowerShell コマンドレットを使用していて、ソフトウェアで定義されたネットワーク (SDN) を展開していない場合は、 **set-vmnetworkadaptervlan**コマンドレットを使用する必要があります。

### <a name="possible-issues"></a>考えられる問題

これらのガイドラインに従っていない場合は、次の問題が発生する可能性があります。

- SDN を展開し、VMM、ネットワークコントローラー、または**VMNetworkAdapterIsolation**コマンドレットを使用して Hyper-v 仮想スイッチポートで vlan 設定を構成する場合: hyper-v マネージャーを使用するか、 **set-vmnetworkadaptervlan を取得**して構成設定を表示すると、コマンド出力に VLAN 設定が表示されません。 代わりに、 **VMNetworkIsolation**コマンドレットを使用して、VLAN 設定を表示する必要があります。
- SDN を展開していない状況で、代わりに Hyper-v マネージャーまたは**set-vmnetworkadaptervlan**コマンドレットを使用して Hyper-v 仮想スイッチポートの VLAN 設定を構成する場合: **VMNetworkIsolation**コマンドレットを使用して構成設定を表示すると、コマンド出力に VLAN 設定が表示されません。 代わりに、 **Get set-vmnetworkadaptervlan**コマンドレットを使用して、VLAN 設定を表示する必要があります。

また、両方の構成方法を使用して、同じスイッチポート VLAN 設定を構成しないようにすることも重要です。 この場合、スイッチポートが正しく構成されていないため、ネットワーク通信でエラーが発生する可能性があります。

### <a name="resources"></a>リソース

このトピックで説明されている Windows PowerShell コマンドの詳細については、以下を参照してください。

- [VmNetworkAdapterIsolation](/powershell/module/hyper-v/set-vmnetworkadapterisolation?view=win10-ps)
- [VmNetworkAdapterIsolation](/powershell/module/hyper-v/get-vmnetworkadapterisolation?view=win10-ps)
- [Set-vmnetworkadaptervlan](/powershell/module/hyper-v/set-vmnetworkadaptervlan?view=win10-ps)
- [Set-vmnetworkadaptervlan](/powershell/module/hyper-v/get-vmnetworkadaptervlan?view=win10-ps)