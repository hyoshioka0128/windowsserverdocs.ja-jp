---
title: HYPER-V の仮想ローカル エリア ネットワークを構成します。
description: 使用するため、HYPER-V ホスト上の仮想マシンで仮想ローカル エリア ネットワーク (VLAN) を構成する手順を示します。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8510a709-001c-4eee-b6d6-c451e8a8a836
author: KBDAzure
ms.author: kathydav
ms.date: 10/11/2016
ms.openlocfilehash: 5b5eaf175e7c09124aaa3f7a33523e8b87a9ae84
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848463"
---
# <a name="configure-virtual-local-area-networks-for-hyper-v"></a>HYPER-V の仮想ローカル エリア ネットワークを構成します。
仮想ローカル エリア ネットワーク\(Vlan\)ネットワーク トラフィックを分離する 1 つの方法を提供します。 Vlan はスイッチと 802.1 q をサポートするルーターで構成されます。 複数の Vlan を構成してそれらの間に通信する場合は、許可するネットワーク デバイスを構成する必要があります。 

次の Vlan を構成する必要があります。  
  
-   物理ネットワーク アダプターとドライバー 802.1 q をサポートする VLAN タグ付けします。  
-   802.1 q をサポートする物理ネットワーク スイッチ VLAN タグ付けします。  
  
ホストで、物理スイッチ ポートでのネットワーク トラフィックを許可する仮想スイッチを構成します。 これは、仮想マシンで内部的に使用する VLAN Id です。 次に、すべてのネットワーク通信、仮想マシンが使用する VLAN を指定する仮想マシンを構成します。  
  
#### <a name="to-allow-a-virtual-switch-to-use-a-vlan"></a>VLAN を使用する仮想スイッチを許可するには  
  
1.  オープン ハイパー\-V マネージャー。  
  
2.  アクションのメニューから**仮想スイッチ マネージャー**します。  
  
3.  **仮想スイッチ**Vlan をサポートする物理ネットワーク アダプターに接続して、仮想スイッチを選択します。 

4. VLAN ID を右側のペインで選択**仮想 LAN id を有効にする**VLAN ID の数値を入力し、  
  
    VLAN ID を設定すると、仮想スイッチに接続されている物理ネットワーク アダプターを経由するすべてのトラフィックにタグ付けされます。  
  
#### <a name="to-allow-a-virtual-machine-to-use-a-vlan"></a>VLAN を使用する仮想マシンを許可するには  
  
1.  オープン ハイパー\-V マネージャー。  
  
2.  結果ウィンドウで **仮想マシン**、適切な仮想マシンを選択し、右クリック**設定**します。  

3.  **ハードウェア**VLAN に設定されている仮想スイッチを選択します。
  
4.  右側のウィンドウで次のように選択します。**仮想 LAN id を有効にする**、し、仮想スイッチに指定した 1 つとして、同じ VLAN ID を入力します。 

を仮想マシンが複数の Vlan を使用する必要がある場合は、次のいずれかの操作を行います。  
  
-   仮想スイッチを適切な VLAN Id を割り当てるを複数の仮想ネットワーク アダプターを接続します。 IP アドレスを正しく構成することを確認し、正しい IP アドレスを使用して、トラフィックすることも、VLAN 経由でルーティングします。  
  
-   トランク モードを使用して word の仮想ネットワーク アダプターを構成、[設定\-VMNetworkAdapterVlan](https://technet.microsoft.com/library/hh848475.aspx)コマンドレット。
  
## <a name="see-also"></a>関連項目  
 
[ハイパー\-仮想スイッチの概要](https://technet.microsoft.com/windows-server-docs/networking/technologies/hyper-v-virtual-switch/hyper-v-virtual-switch)