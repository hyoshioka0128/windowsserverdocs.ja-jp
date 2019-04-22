---
title: Hyper-V 仮想スイッチ ポートで VLAN 設定を構成および表示する
description: このトピックを使用すると、構成、および Windows Server 2016 で HYPER-V 仮想スイッチ ポートでの仮想ローカル エリア ネットワーク (VLAN) の設定を表示するためのベスト プラクティスについて説明します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: article
ms.assetid: 69e0e28a-98ae-4ade-bd27-ce2ad7eb310f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1e4843b0ffee86d728736ae212b953bb7c8552c0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820553"
---
# <a name="configure-and-view-vlan-settings-on-hyper-v-virtual-switch-ports"></a>Hyper-V 仮想スイッチ ポートで VLAN 設定を構成および表示する

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

このトピックを使用すると、構成して、HYPER-V 仮想スイッチ ポートでの仮想ローカル エリア ネットワーク (VLAN) の設定を表示するためのベスト プラクティスについて説明します。

いずれかの Windows を使用するには、HYPER-V 仮想スイッチ ポートで VLAN 設定を構成する場合は、&reg; Server 2016 HYPER-V Manager または System Center Virtual Machine Manager (VMM)。

VMM を使用している場合 VMM は、次の Windows PowerShell コマンドを使用して、スイッチ ポートを構成します。

```
Set-VMNetworkAdapterIsolation <VM-name|-managementOS> -IsolationMode VLAN -DefaultIsolationID <vlan-value> -AllowUntaggedTraffic $True
```
VMM を使用していないし、Windows Server で、スイッチ ポートを構成する場合は、HYPER-V マネージャー コンソールまたは Windows PowerShell の次のコマンドを使用できます。
```
Set-VMNetworkAdapterVlan <VM-name|-managementOS> -Access -VlanID <vlan-value>
```

これら 2 つの方法、HYPER-V 仮想スイッチ ポートで VLAN 設定を構成するためには、スイッチのポート設定を表示しようとしたときに表示される VLAN 設定が構成されていないことに構成されている場合でもことはできます。

## <a name="use-the-same-method-to-configure-and-view-switch-port-vlan-settings"></a>同じメソッドを使用して構成し、スイッチ ポート VLAN 設定を表示するには

これらの問題が発生しないことを確認するには、スイッチ ポートの VLAN 設定を構成するのにために使用するスイッチ ポート VLAN 設定を表示するのに同じメソッドを使用する必要があります。

で構成して、VLAN のスイッチ ポートの設定を表示するには、次の操作を行う必要があります。

- ソフトウェア定義ネットワーク (SDN) を展開して、使用する必要がありますを設定して、ネットワークを管理する VMM またはネットワーク コント ローラーを使用する場合、 **VMNetworkAdapterIsolation**コマンドレット。 
- Windows Server 2016 HYPER-V マネージャーまたは Windows PowerShell のコマンドレットを使用している、ソフトウェア定義ネットワーク (SDN) を展開していない場合を使用する必要があります、 **VMNetworkAdapterVlan**コマンドレット。

### <a name="possible-issues"></a>考えられる問題

次のガイドラインに従わない場合は、次の問題が発生する可能性があります。

- SDN を展開して、VMM では、ネットワーク コント ローラーを使用する場所の状況で、または**VMNetworkAdapterIsolation** HYPER-V 仮想スイッチ ポートで VLAN 設定を構成するためのコマンドレット。HYPER-V マネージャーを使用する場合または**取得 VMNetworkAdapterVlan**構成設定を表示するコマンドの出力は表示されません、VLAN 設定します。 代わりに使用する必要があります、 **Get VMNetworkIsolation** VLAN 設定を表示するコマンドレットです。
- SDN を展開していないと、代わりに、HYPER-V マネージャーを使用して、状況で、または**VMNetworkAdapterVlan** HYPER-V 仮想スイッチ ポートで VLAN 設定を構成するためのコマンドレット。使用する場合、 **Get VMNetworkIsolation**構成の設定を表示するコマンドレット、コマンドの出力では、VLAN の設定は表示されません。 代わりに使用する必要があります、**取得 VMNetworkAdapterVlan** VLAN 設定を表示するコマンドレットです。

これらの構成方法の両方を使用して同じスイッチ ポート VLAN 設定を構成しようとすることが重要です。 これを行うと、スイッチ ポートが正しく構成されていない、し、結果は、ネットワーク通信の障害。

### <a name="resources"></a>参考資料

このトピックに記載されている Windows PowerShell コマンドの詳細については、次を参照してください。

- [Set-VmNetworkAdapterIsolation](https://technet.microsoft.com/library/dn464283.aspx)
- [Get-VmNetworkAdapterIsolation](https://technet.microsoft.com/library/dn464277.aspx)
- [Set-VMNetworkAdapterVlan](https://technet.microsoft.com/library/hh848475.aspx)
- [Get-VMNetworkAdapterVlan](https://technet.microsoft.com/library/hh848516.aspx)





