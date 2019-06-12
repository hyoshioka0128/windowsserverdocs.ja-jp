---
title: Azure で同じリージョン内で記憶域レプリカをクラスターにクラスター
description: クラスターを Azure で同じリージョン内のクラスター ストレージのレプリケーション
keywords: 記憶域レプリカ、サーバー マネージャー、Windows Server、Azure、クラスター、同じリージョン
author: arduppal
ms.author: arduppal
ms.date: 04/26/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage-replica
manager: mchad
ms.openlocfilehash: 9cf998087e23f45fe5981aef6d1ff5b7b4e85b9b
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447613"
---
# <a name="cluster-to-cluster-storage-replica-within-the-same-region-in-azure"></a>Azure で同じリージョン内で記憶域レプリカをクラスターにクラスター

> 適用対象:Windows Server 2019、Windows Server 2016、Windows Server (半期チャネル)

Azure では、同じリージョン内でクラスターをクラスターに記憶域レプリケーションを構成できます。 次の例では、2 つのノードを使用しますが、クラスターをクラスターに記憶域レプリカは 2 つのノードに制限はありません。 次の図は、相互に通信できる 2 つのノードの記憶域スペース ダイレクト クラスターが同じドメインおよび同じリージョン内で。

プロセスの詳しいチュートリアルについては、以下のビデオをご覧ください。

第 1 部
> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE26f2Y]

第 2 部
> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE269Pq]

![アーキテクチャ図は、同じリージョン内で Azure でのクラスター-クラスター記憶域レプリカを紹介します。](media/Cluster-to-cluster-azure-one-region/architecture.png)
> [!IMPORTANT]
> 参照先のすべての例では、上の図に固有です。

1. 作成、[リソース グループ](https://ms.portal.azure.com/#create/Microsoft.ResourceGroup)リージョンで Azure portal で (**SR AZ2AZ**で**米国西部 2**)。 
2. 2 つ作成[可用性セット](https://ms.portal.azure.com/#create/Microsoft.AvailabilitySet-ARM)リソース グループ内 (**SR AZ2AZ**) クラスターごとに、上記で作成された 1 つ。 
    a. 可用性セット (**az2azAS1**) b。 可用性セット (**az2azAS2**)
3. 作成、[仮想ネットワーク](https://ms.portal.azure.com/#create/Microsoft.VirtualNetwork-ARM)(**az2az Vnet**) 以前に作成したリソース グループ内 (**SR AZ2AZ**)、として、少なくとも 1 つのサブネットを持ちます。 
4. 作成、[ネットワーク セキュリティ グループ](https://ms.portal.azure.com/#create/Microsoft.NetworkSecurityGroup-ARM)(**az2az NSG**)、RDP:3389 の 1 つの受信セキュリティ規則を追加します。 セットアップが完了したら、このルールを削除することができます。 
5. Windows Server の作成[仮想マシン](https://ms.portal.azure.com/#create/Microsoft.WindowsServer2016Datacenter-ARM)以前に作成したリソース グループ内 (**SR AZ2AZ**)。 以前に作成した仮想ネットワークを使用して (**az2az Vnet**) とネットワーク セキュリティ グループ (**az2az NSG**)。 
   
   ドメイン コント ローラー (**az2azDC**)。 ドメイン コント ローラーの 3 番目の可用性セットを作成または 2 つの可用性セットのいずれかで、ドメイン コント ローラーを追加することができます。 これを追加する、2 つのクラスター用に作成された可用性セットには場合、割り当てる標準パブリック IP アドレス VM の作成中。 
   - Active Directory ドメイン サービスをインストールします。
   - ドメイン (Contoso.com) を作成します。
   - 管理者特権 (contosoadmin) を持つユーザーを作成します。 
   - 2 つの仮想マシンの作成 (**az2az1**、 **az2az2**)、最初の可用性セット (**az2azAS1**)。 自体の作成時に、各仮想マシンに standard パブリック IP アドレスを割り当てます。
   - 各マシンとして、少なくとも 2 つの管理対象ディスクを追加します。
   - フェールオーバー クラスタ リングと記憶域レプリカ機能をインストールします。
   - 2 つの仮想マシンの作成 (**az2az3**、 **az2az4**)、2 つ目の可用性セット (**az2azAS2**)。 自体の作成時に、各仮想マシンに標準のパブリック IP アドレスを割り当てます。 
   - 各マシンとして、少なくとも 2 つの管理対象ディスクを追加します。 
   - フェールオーバー クラスタ リングと記憶域レプリカの機能をインストールします。 
   
6. すべてのノードをドメインに接続し、以前に作成したユーザーに管理者特権を提供します。 

7. 仮想ネットワークの DNS サーバーをドメイン コント ローラーのプライベート IP アドレスに変更します。 
8. この例では、ドメイン コント ローラー **az2azDC**がプライベート IP アドレス (10.3.0.8)。 仮想ネットワーク内 (**az2az Vnet**) DNS サーバー 10.3.0.8 を変更します。 "Contoso.com"のすべてのノードを接続し、"contosoadmin"に、管理者権限を指定します。
   - すべてのノードから contosoadmin としてログインします。 
    
9. クラスターの作成 (**SRAZC1**、 **SRAZC2**)。 
   この例の PowerShell コマンドを次に示します
   ```PowerShell
    New-Cluster -Name SRAZC1 -Node az2az1,az2az2 –StaticAddress 10.3.0.100
   ```
   ```PowerShell
    New-Cluster -Name SRAZC2 -Node az2az3,az2az4 –StaticAddress 10.3.0.101
   ```
10. 記憶域スペース ダイレクトを有効にします。
    ```PowerShell
    Enable-clusterS2D
    ```   
   
    各クラスターの仮想ディスクとボリュームを作成します。 データとログ用に別の 1 つです。 
   
11. 内部の Standard SKU の作成[ロード バランサー](https://ms.portal.azure.com/#create/Microsoft.LoadBalancer-ARM)クラスターごとに (**azlbr1**、**azlbr2**)。 
   
    ロード バランサーの静的プライベート IP アドレスとしてクラスターの IP アドレスを指定します。
    - azlbr1 = > フロント エンド IP:10.3.0.100 (仮想ネットワークから未使用の IP アドレスを取得 (**az2az Vnet**) サブネット)
    - 各ロード バランサーのバックエンド プールを作成します。 関連付けられているクラスター ノードを追加します。
    - ポート 59999 の正常性プローブを作成します。
    - 負荷分散規則を作成します。Floating IP を有効になっていると、HA ポートを許可します。 
   
    ロード バランサーの静的プライベート IP アドレスとしてクラスターの IP アドレスを指定します。
    - azlbr2 = > フロント エンド IP:10.3.0.101 (仮想ネットワークから未使用の IP アドレスを取得 (**az2az Vnet**) サブネット)
    - 各ロード バランサーのバックエンド プールを作成します。 関連付けられているクラスター ノードを追加します。
    - ポート 59999 の正常性プローブを作成します。
    - 負荷分散規則を作成します。Floating IP を有効になっていると、HA ポートを許可します。 
   
12. 各クラスター ノードでは、ポート 59999 (正常性プローブ) を開きます。 
   
    各ノードで、次のコマンドを実行します。
    ```PowerShell
    netsh advfirewall firewall add rule name=PROBEPORT dir=in protocol=tcp action=allow localport=59999 remoteip=any profile=any 
    ```   
13. クラスターの正常性プローブ ポート 59999 メッセージをリッスンし、このリソースを所有しているノードからの応答するように指示します。 
    1 回から実行クラスターごとに、クラスターの 1 つのノード。 
    
    この例では、"ILBIP"、構成値に基づいてを変更してください。 1 つのノードから、次のコマンドを実行**az2az1**/**az2az2**:

    ```PowerShell
     $ClusterNetworkName = "Cluster Network 1" # Cluster network name (Use Get-ClusterNetwork on Windows Server 2012 or higher to find the name. And use Get-ClusterResource to find the IPResourceName).
     $IPResourceName = "Cluster IP Address" # IP Address cluster resource name.
     $ILBIP = "10.3.0.100" # IP Address in Internal Load Balancer (ILB) - The static IP address for the load balancer configured in the Azure portal.
     [int]$ProbePort = 59999
     Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";”ProbeFailureThreshold”=5;"EnableDhcp"=0}
    ```

14. 1 つのノードから、次のコマンドを実行**az2az3**/**az2az4**します。 

    ```PowerShell
    $ClusterNetworkName = "Cluster Network 1" # Cluster network name (Use Get-ClusterNetwork on Windows Server 2012 or higher to find the name. And use Get-ClusterResource to find the IPResourceName).
    $IPResourceName = "Cluster IP Address" # IP Address cluster resource name.
    $ILBIP = "10.3.0.101" # IP Address in Internal Load Balancer (ILB) - The static IP address for the load balancer configured in the Azure portal.
    [int]$ProbePort = 59999
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";”ProbeFailureThreshold”=5;"EnableDhcp"=0}  
    ```   
    両方のクラスターが接続/相互通信を確認してください。 

    いずれか、他のクラスターに接続または他のクラスターの現在のクラスターのノードの 1 つから応答を確認するフェールオーバー クラスター マネージャーの「クラスターに接続」機能を使用します。  
   
    ```PowerShell
     Get-Cluster -Name SRAZC1 (ran from az2az3)
    ```
    ```PowerShell
     Get-Cluster -Name SRAZC2 (ran from az2az1)
    ```   

15. クラウドのミラーリング監視サーバーの両方のクラスターを作成します。 2 つ作成[ストレージ アカウント](https://ms.portal.azure.com/#create/Microsoft.StorageAccount-ARM)(**az2azcw**、 **az2azcw2**) で同じリソース グループ内の各クラスターの azure の 1 つ (**SR AZ2AZ**)。

    - [アクセス キー] から、ストレージ アカウント名とキーをコピーします。
    - 「フェールオーバー クラスター マネージャー」から、クラウドのミラーリング監視サーバーを作成し、上記のアカウント名とキーを使用して作成しています。

16. 実行[クラスター検証テストの](../../failover-clustering/create-failover-cluster.md#validate-the-configuration)次の手順に進む前にします。

17. Windows PowerShell を起動し、[Test-SRTopology](https://docs.microsoft.com/powershell/module/storagereplica/test-srtopology?view=win10-ps) コマンドレットを使用して、記憶域レプリカのすべての要件を満たしているかどうかを判別します。 実行時間の長いパフォーマンス評価モードとして、簡単なテスト要件のみモードでコマンドレットを使用することができます。

18. クラスター-クラスター記憶域レプリカを構成します。
   
    双方向で別のクラスターに 1 つのクラスターからのアクセスを許可します。

    この例では。

    ```PowerShell
      Grant-SRAccess -ComputerName az2az1 -Cluster SRAZC2
    ```
    このコマンドを実行するも Windows Server 2016 を使用する: 場合

    ```PowerShell
      Grant-SRAccess -ComputerName az2az3 -Cluster SRAZC1
    ```   
   
19. クラスターの場合、SRPartnership を作成します。</ol>

    - クラスターの**SRAZC1**します。
    - ボリュームの場所:-c:\ClusterStorage\DataDisk1
    - ログの場所:-g:
    - クラスターの**SRAZC2**
    - ボリュームの場所:-c:\ClusterStorage\DataDisk2
    - ログの場所:-g:

次のコマンドを実行します。

```PowerShell

New-SRPartnership -SourceComputerName SRAZC1 -SourceRGName rg01 -SourceVolumeName c:\ClusterStorage\DataDisk1 -SourceLogVolumeName  g: -DestinationComputerName **SRAZC2** -DestinationRGName rg02 -DestinationVolumeName c:\ClusterStorage\DataDisk2 -DestinationLogVolumeName  g:
```