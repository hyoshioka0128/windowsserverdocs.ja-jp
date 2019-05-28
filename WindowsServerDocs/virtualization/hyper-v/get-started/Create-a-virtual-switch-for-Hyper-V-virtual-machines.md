---
title: HYPER-V 仮想マシン用の仮想スイッチを作成します。
description: HYPER-V マネージャーまたは Windows PowerShell を使用して仮想スイッチを作成する手順については、します。
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
ms.openlocfilehash: 2668f9fa21c8efbad455d82c7e110ff89b729187
ms.sourcegitcommit: 8ba2c4de3bafa487a46c13c40e4a488bf95b6c33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/25/2019
ms.locfileid: "66222877"
---
# <a name="create-a-virtual-switch-for-hyper-v-virtual-machines"></a>HYPER-V 仮想マシン用の仮想スイッチを作成します。

>適用先:Windows 10、Windows Server 2016、Microsoft HYPER-V Server 2016、Windows Server 2019、Microsoft HYPER-V Server 2019
  
仮想スイッチは、他のコンピューターと通信するために、HYPER-V ホストで作成された仮想マシンを使用します。 Windows server、Hyper-v の役割を初めてインストールすると、仮想スイッチを作成できます。 その他の仮想スイッチを作成するには、HYPER-V マネージャーまたは Windows PowerShell を使用します。 仮想スイッチの詳細については、次を参照してください。 [、Hyper-v 仮想スイッチ](../../hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md)します。  
  
仮想マシンのネットワークには、複雑な件名を指定できます。 ように使用するいくつかの新しい仮想スイッチ機能があると[スイッチ埋め込みチーミング (SET)](../../hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md#switch-embedded-teaming-set)します。 基本的なネットワー キングはかなり簡単に実行できます。 このトピックでは、hyper-v ネットワークの仮想マシンを作成できるようにするのに十分なだけについて説明します。 ネットワーク インフラストラクチャを設定する方法の詳細については、確認、[ネットワーク](../../../networking/Networking.md)ドキュメント。   
  
## <a name="create-a-virtual-switch-by-using-hyper-v-manager"></a>HYPER-V マネージャーを使用して仮想スイッチを作成します。  
  
1.  HYPER-V マネージャーを開き、HYPER-V ホストのコンピューター名を選択します。  
  
2.  選択**アクション** > **仮想スイッチ マネージャー**します。  
  
    ![メニュー オプションのアクションを示すスクリーン ショット > 仮想スイッチ マネージャー](../media/Hyper-V-Action-VSwitchManager.png)  
  
3.  必要な仮想スイッチの種類を選択します。  
  
    |接続の種類|説明|  
    |-------------------|---------------|  
    |外部リンク|サーバーと外部のネットワーク上のクライアントと通信する物理ネットワークに、仮想マシンにアクセスします。 互いに通信を同じ HYPER-V サーバー上には、仮想マシンを許可します。|  
    |内部|および仮想マシンと管理ホスト オペレーティング システムの間、同じ HYPER-V サーバー上の仮想マシン間の通信を許可します。|  
    |Private|同じ HYPER-V サーバー上の仮想マシン間の通信を許可するだけです。 プライベート ネットワークは、HYPER-V サーバー上のすべての外部ネットワーク トラフィックから分離されます。 この種類のネットワークは、する必要があります、隔離されたテスト ドメインなど、分離されたネットワーク環境を作成する場合に便利です。|  
  
4.  選択**仮想スイッチの作成**です。  
  
5.  仮想スイッチの名前を追加します。  
  
6.  外部を選択した場合を使用するネットワーク アダプター (NIC) と、次の表で説明されているその他のオプションを選択します。  
  
    ![外部ネットワーク オプションを示しているスクリーン ショット](../media/Hyper-V-NewVSwitch-ExternalOptions.png)  
  
    |設定名|説明|  
    |----------------|---------------|  
    |管理オペレーティング システムにこのネットワーク アダプターの共有を許可する|HYPER-V ホストが仮想スイッチの使用を共有できるようにして、NIC または NIC チームの仮想マシンの場合は、このオプションを選択します。 これを有効に、ホストは、構成設定のいずれかを使用のサービスの品質 (QoS) 設定、セキュリティ設定、またはその他の機能、HYPER-V 仮想スイッチのように仮想スイッチ。|  
    |シングル ルート I/O 仮想化 (SR-IOV) を有効にします。|バーチャル マシン スイッチをバイパスし、物理 NIC に直接移動する仮想マシン トラフィックを許可する場合にのみ、このオプションを選択します 詳細については、次を参照してください。[シングル ルート I/O 仮想化](https://technet.microsoft.com/library/dn641211.aspx#Sec4)ポスターのコンパニオン リファレンス。HYPER-V ネットワーク。|  
  
7.  管理 HYPER-V ホストのオペレーティング システムまたは同じ仮想スイッチを共有する他の仮想マシンからネットワーク トラフィックを分離する場合は、選択**仮想 LAN id を管理オペレーティング システムを有効にする**します。 任意の数に VLAN ID を変更したり、既定値のままにできます。 これは、管理オペレーティング システムがこの仮想スイッチを介したすべてのネットワーク通信用に使用する仮想 LAN 識別番号です。  
  
    ![VLAN ID オプションを示しているスクリーン ショット](../media/Hyper-V-NewSwitch-VLAN.png)  
  
8.  **[OK]** をクリックします。  
  
9. **[はい]** をクリックします。  
  
    ![「保留中の変更可能性がありますが中断されるネットワーク接続」メッセージを示すスクリーン ショット](../media/Hyper-V-NewVSwitch-DisruptNetwork.png)  
  
## <a name="create-a-virtual-switch-by-using-windows-powershell"></a>Windows PowerShell を使用して仮想スイッチを作成します。  
  
1.  Windows デスクトップ上で、[スタート] ボタンをクリックし、**Windows PowerShell** という名前の一部を入力します。  
  
2.  Windows PowerShell を右クリックして **管理者として実行**します。  
  
3.  実行して既存のネットワーク アダプターを見つける、 [Get-netadapter](https://technet.microsoft.com/library/jj130867.aspx)コマンドレット。 仮想スイッチを使用するネットワーク アダプターの名前をメモしておきます。  
  
    ```  
    Get-NetAdapter  
    ```  
  
4.  使用して仮想スイッチを作成、 [New-vmswitch](https://technet.microsoft.com/library/hh848455.aspx)コマンドレット。 など、外部仮想スイッチを作成する、イーサネット ネットワーク アダプターを使用して、ExternalSwitch をという名前を使用して**管理オペレーティング システムにこのネットワーク アダプターの共有を許可する**次のコマンドを実行する電源をオンにします。  
  
    ```  
    New-VMSwitch -name ExternalSwitch  -NetAdapterName Ethernet -AllowManagementOS $true  
    ```  
  
    内部スイッチを作成するには、次のコマンドを実行します。  
  
    ```  
    New-VMSwitch -name InternalSwitch -SwitchType Internal  
    ```  
  
    プライベートのスイッチを作成するには、次のコマンドを実行します。  
  
    ```  
    New-VMSwitch -name PrivateSwitch -SwitchType Private  
    ```  
  
Windows Server 2016 で強化されたか、新しい仮想スイッチ機能に対応するより高度な Windows PowerShell スクリプトでは、次を参照してください。[リモート ダイレクト メモリ アクセスとスイッチ埋め込みチーミング](../../hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)します。  

  
## <a name="next-step"></a>次の手順  
[Hyper-V で仮想マシンを作成する](Create-a-virtual-machine-in-Hyper-V.md)  
  


