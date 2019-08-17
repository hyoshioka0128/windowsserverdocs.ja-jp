---
title: HYPER-V 仮想マシン用の仮想スイッチを作成します。
description: Hyper-v マネージャーまたは Windows PowerShell を使用して仮想スイッチを作成する手順について説明します。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: fdc8063c-47ce-4448-b445-d7ff9894dc17
author: KBDAzure
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: 3c0ba19183dd68a86d995293f663accf10e91df9
ms.sourcegitcommit: 0467b8e69de66e3184a42440dd55cccca584ba95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2019
ms.locfileid: "69546383"
---
# <a name="create-a-virtual-switch-for-hyper-v-virtual-machines"></a>HYPER-V 仮想マシン用の仮想スイッチを作成します。

>適用先:Windows 10、Windows Server 2016、Microsoft Hyper-v Server 2016、Windows Server 2019、Microsoft Hyper-v Server 2019
  
仮想スイッチを使用すると、Hyper-v ホスト上で作成された仮想マシンが他のコンピューターと通信できるようになります。 Windows Server に Hyper-v の役割を初めてインストールするときに、仮想スイッチを作成できます。 追加の仮想スイッチを作成するには、Hyper-v マネージャーまたは Windows PowerShell を使用します。 仮想スイッチの詳細については、「 [Hyper-v 仮想スイッチ](../../hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md)」を参照してください。  
  
仮想マシンネットワークは複雑なサブジェクトになることがあります。 また、[スイッチ埋め込みチーミング (SET)](../../hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md#switch-embedded-teaming-set)と同様に、いくつかの新しい仮想スイッチ機能を使用することもできます。 しかし、基本的なネットワークはとても簡単です。 このトピックでは、Hyper-v でネットワーク化された仮想マシンを作成できるように、十分に説明します。 ネットワークインフラストラクチャをセットアップする方法の詳細については、[ネットワーク](../../../networking/Networking.md)のドキュメントを参照してください。   
  
## <a name="create-a-virtual-switch-by-using-hyper-v-manager"></a>Hyper-v マネージャーを使用して仮想スイッチを作成する  
  
1.  Hyper-v マネージャーを開き、Hyper-v ホストコンピューター名を選択します。  
  
2.  [**アクション** > ] **[仮想スイッチマネージャー]** を選択します。  
  
    ![仮想スイッチマネージャー > メニューオプションアクションを示すスクリーンショット](../media/Hyper-V-Action-VSwitchManager.png)  
  
3.  目的の仮想スイッチの種類を選択します。  
  
    |接続の種類|説明|  
    |-------------------|---------------|  
    |外部リンク|外部ネットワーク上のサーバーおよびクライアントと通信するために、仮想マシンに物理ネットワークへのアクセスを提供します。 同じ Hyper-v サーバー上の仮想マシンが相互に通信できるようにします。|  
    |Internal|同じ Hyper-v サーバー上の仮想マシン間、および仮想マシンと管理ホストオペレーティングシステムの間の通信を許可します。|  
    |プライベート|では、同じ Hyper-v サーバー上の仮想マシン間の通信のみが許可されます。 プライベートネットワークは、Hyper-v サーバー上のすべての外部ネットワークトラフィックから分離されます。 この種類のネットワークは、分離されたテストドメインのように、分離されたネットワーク環境を作成する必要がある場合に便利です。|  
  
4.  **[仮想スイッチの作成]** を選択します。  
  
5.  仮想スイッチの名前を追加します。  
  
6.  [外部] を選択した場合は、使用するネットワークアダプター (NIC) と、次の表に記載されているその他のオプションを選択します。  
  
    ![外部ネットワークオプションを示すスクリーンショット](../media/Hyper-V-NewVSwitch-ExternalOptions.png)  
  
    |設定名|説明|  
    |----------------|---------------|  
    |管理オペレーティング システムにこのネットワーク アダプターの共有を許可する|仮想スイッチ、NIC、または NIC チームの使用を Hyper-v ホストが仮想マシンと共有できるようにする場合は、このオプションを選択します。 これを有効にすると、ホストは、サービスの品質 (QoS) 設定、セキュリティ設定、または Hyper-v 仮想スイッチのその他の機能など、仮想スイッチに構成した設定のいずれかを使用できます。|  
    |シングルルート i/o 仮想化 (SR-IOV) を有効にする|このオプションは、仮想マシンのトラフィックが仮想マシンのスイッチをバイパスして物理 NIC に直接移動できるようにする場合にのみ選択します。 詳細については、ポスターコンパニオンリファレンスの「[シングルルート I/o 仮想化](https://technet.microsoft.com/library/dn641211.aspx#Sec4)」を参照してください。Hyper-v ネットワーク。|  
  
7.  管理 Hyper-v ホストオペレーティングシステムまたは同じ仮想スイッチを共有する他の仮想マシンからネットワークトラフィックを分離する場合は、[**管理オペレーティングシステムの仮想 LAN id を有効に**する] を選択します。 VLAN ID は任意の数に変更することも、既定のままにすることもできます。 これは、管理オペレーティングシステムがこの仮想スイッチ経由のすべてのネットワーク通信に使用する仮想 LAN 識別番号です。  
  
    ![VLAN ID オプションを示すスクリーンショット](../media/Hyper-V-NewSwitch-VLAN.png)  
  
8.  **[OK]** をクリックします。  
  
9. **[はい]** をクリックします。  
  
    !["保留中の変更によりネットワーク接続が中断される可能性がある" というメッセージを示すスクリーンショット](../media/Hyper-V-NewVSwitch-DisruptNetwork.png)  
  
## <a name="create-a-virtual-switch-by-using-windows-powershell"></a>Windows PowerShell を使用して仮想スイッチを作成する  
  
1.  Windows デスクトップ上で、[スタート] ボタンをクリックし、**Windows PowerShell** という名前の一部を入力します。  
  
2.  Windows PowerShell を右クリックして **管理者として実行**します。  
  
3.  [Get NetAdapter](https://technet.microsoft.com/library/jj130867.aspx)コマンドレットを実行して、既存のネットワークアダプターを検索します。 仮想スイッチに使用するネットワークアダプターの名前をメモしておきます。  
  
    ```  
    Get-NetAdapter  
    ```  
  
4.  [新しい-VMSwitch](https://technet.microsoft.com/library/hh848455.aspx)コマンドレットを使用して仮想スイッチを作成します。 たとえば、ExternalSwitch という名前の外部仮想スイッチを作成し、イーサネットネットワークアダプターを使用して、 **[管理オペレーティングシステムによるこのネットワークアダプターの共有を許可する]** がオンになっている場合は、次のコマンドを実行します。  
  
    ```  
    New-VMSwitch -name ExternalSwitch  -NetAdapterName Ethernet -AllowManagementOS $true  
    ```  
  
    内部スイッチを作成するには、次のコマンドを実行します。  
  
    ```  
    New-VMSwitch -name InternalSwitch -SwitchType Internal  
    ```  
  
    プライベートスイッチを作成するには、次のコマンドを実行します。  
  
    ```  
    New-VMSwitch -name PrivateSwitch -SwitchType Private  
    ```  
  
Windows Server 2016 の強化されたまたは新しい仮想スイッチ機能をカバーする、より高度な Windows PowerShell スクリプトについては、「[リモートダイレクトメモリアクセスとスイッチ埋め込みチーミング](../../hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)」を参照してください。  

  
## <a name="next-step"></a>次の手順  
[Hyper-V で仮想マシンを作成する](Create-a-virtual-machine-in-Hyper-V.md)  
  


