---
title: Hyper-v の仮想ローカルエリアネットワークを構成する
description: Hyper-v ホスト上のバーチャルマシンで使用する仮想ローカルエリアネットワーク (VLAN) を構成する手順について説明します。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8510a709-001c-4eee-b6d6-c451e8a8a836
author: KBDAzure
ms.author: kathydav
ms.date: 10/11/2016
ms.openlocfilehash: f2c240a3ad9f9783e509efb288cc6c6410339685
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364281"
---
# <a name="configure-virtual-local-area-networks-for-hyper-v"></a>Hyper-v の仮想ローカルエリアネットワークを構成する
仮想ローカルエリアネットワーク \(VLANs @ no__t は、ネットワークトラフィックを分離するための1つの方法を提供します。 Vlan は、802.1 q をサポートするスイッチとルーターで構成されます。 複数の Vlan を構成し、それらの間で通信が行われるようにするには、ネットワークデバイスでそのような構成を行う必要があります。 

Vlan を構成するには、次のものが必要です。  
  
-   802.1 q VLAN タグ付けをサポートする物理ネットワークアダプターとドライバー。  
-   802.1 q VLAN タグ付けをサポートする物理ネットワークスイッチ。  
  
ホストでは、物理スイッチポートのネットワークトラフィックを許可するように仮想スイッチを構成します。 これは、仮想マシンで内部的に使用する VLAN Id を対象としています。 次に、仮想マシンがすべてのネットワーク通信に使用する VLAN を指定するように、仮想マシンを構成します。  
  
#### <a name="to-allow-a-virtual-switch-to-use-a-vlan"></a>仮想スイッチで VLAN を使用できるようにするには  
  
1.  ハイパー @ no__t-0V Manager を開きます。  
  
2.  操作 メニューの **仮想スイッチマネージャー** をクリックします。  
  
3.  **[仮想スイッチ]** で、vlan をサポートする物理ネットワークアダプターに接続されている仮想スイッチを選択します。 

4. 右側のウィンドウの VLAN ID で、**仮想 LAN の識別を有効にする** を選択し、vlan id の番号を入力します。  
  
    仮想スイッチに接続されている物理ネットワークアダプターを経由するすべてのトラフィックには、設定した VLAN ID がタグ付けされます。  
  
#### <a name="to-allow-a-virtual-machine-to-use-a-vlan"></a>バーチャルマシンで VLAN を使用できるようにするには  
  
1.  ハイパー @ no__t-0V Manager を開きます。  
  
2.  結果ウィンドウの  **Virtual Machines**で、適切な仮想マシンを選択し、**設定** を右クリックします。  

3.  **[ハードウェア]** で、VLAN が設定されている仮想スイッチを選択します。
  
4.  右側のウィンドウで、 **[仮想 LAN の識別を有効にする]** を選択し、仮想スイッチに指定したものと同じ VLAN ID を入力します。 

仮想マシンでより多くの Vlan を使用する必要がある場合は、次のいずれかの操作を行います。  
  
-   より多くの仮想ネットワークアダプターを適切な仮想スイッチに接続し、VLAN Id を割り当てます。 IP アドレスが正しく構成されていること、および VLAN 経由でルーティングするトラフィックにも正しい IP アドレスが使用されていることを確認してください。  
  
-   [Set @ no__t-1VMNetworkAdapterVlan](https://technet.microsoft.com/library/hh848475.aspx) cmdlt を使用して、仮想ネットワークワードアダプタをトランクモードで構成します。
  
## <a name="see-also"></a>関連項目  
 
[ハイパー @ no__t-1V 仮想スイッチ](https://technet.microsoft.com/windows-server-docs/networking/technologies/hyper-v-virtual-switch/hyper-v-virtual-switch)