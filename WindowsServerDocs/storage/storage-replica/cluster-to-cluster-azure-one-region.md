---
title: Azure の同じリージョン内のクラスター記憶域レプリカへのクラスター化
description: クラスターからクラスターへのストレージレプリケーション (Azure の同じリージョン内)
keywords: 記憶域レプリカ、サーバーマネージャー、Windows Server、Azure、クラスター、同じリージョン
author: arduppal
ms.author: arduppal
ms.date: 04/26/2019
ms.topic: article
ms.prod: windows-server
ms.technology: storage-replica
manager: mchad
ms.openlocfilehash: 55d9c600c86b6b64efdb5c7d4437697539f887ae
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402950"
---
# <a name="cluster-to-cluster-storage-replica-within-the-same-region-in-azure"></a>Azure の同じリージョン内のクラスター記憶域レプリカへのクラスター化

> 適用対象:Windows Server 2019、Windows Server 2016、Windows Server (半期チャネル)

Azure の同じリージョン内でストレージレプリケーションをクラスター化するようにクラスターを構成できます。 次の例では、2ノードクラスターを使用していますが、クラスターへのクラスターの記憶域レプリカは2ノードクラスターに制限されていません。 次の図は、相互に通信できる2ノード記憶域スペースダイレクトクラスターであり、同じドメイン内にあり、同じリージョン内に存在します。

プロセスの完全なチュートリアルについては、以下のビデオをご覧ください。

パート1
> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE26f2Y]

パート2
> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE269Pq]

![アーキテクチャダイアグラムでは、同じリージョン内の Azure のクラスター間ストレージレプリカが紹介されています。](media/Cluster-to-cluster-azure-one-region/architecture.png)
> [!IMPORTANT]
> 参照されるすべての例は、上記の図に固有です。

1. リージョン内の Azure portal に[リソースグループ](https://ms.portal.azure.com/#create/Microsoft.ResourceGroup)を作成します (**米国西部 2**の**AZ2AZ** )。 
2. 上で作成したリソースグループ (**AZ2AZ**) に、クラスターごとに1つずつ、2つの[可用性セット](https://ms.portal.azure.com/#create/Microsoft.AvailabilitySet-ARM)を作成します。 
    a. 可用性セット (**az2azAS1**) b。 可用性セット (**az2azAS2**)
3. 以前に作成したリソースグループ (**az2az**) に[仮想ネットワーク](https://ms.portal.azure.com/#create/Microsoft.VirtualNetwork-ARM)(**az2az**) を作成し、少なくとも1つのサブネットを作成します。 
4. [ネットワークセキュリティグループ](https://ms.portal.azure.com/#create/Microsoft.NetworkSecurityGroup-ARM)(**az2az-nsg**) を作成し、RDP: 3389 に1つの受信セキュリティ規則を追加します。 セットアップが完了したら、この規則を削除することを選択できます。 
5. 以前に作成したリソースグループ (**AZ2AZ**) で Windows Server[仮想マシン](https://ms.portal.azure.com/#create/Microsoft.WindowsServer2016Datacenter-ARM)を作成します。 以前に作成した仮想ネットワーク (**az2az**) とネットワークセキュリティグループ (**az2az**) を使用します。 
   
   ドメインコントローラー (**az2azDC**)。 ドメインコントローラー用に3つ目の可用性セットを作成するか、2つの可用性セットのいずれかにドメインコントローラーを追加するかを選択できます。 2つのクラスター用に作成された可用性セットにこれを追加する場合は、VM の作成時に標準のパブリック IP アドレスを割り当てます。 
   - Active Directory ドメインサービスをインストールします。
   - ドメインを作成する (Contoso.com)
   - 管理者特権を持つユーザーを作成する (contosoadmin) 
   - 最初の可用性セット (**az2azAS1**) に2つの仮想マシン (**az2az1**、 **az2az2**) を作成します。 作成中に、各仮想マシンに標準のパブリック IP アドレスを割り当てます。
   - 各コンピューターに少なくとも2つの管理ディスクを追加する
   - フェールオーバークラスタリングと記憶域レプリカのインストール機能
   - 2つ目の可用性セット (**az2azAS2**) に2つの仮想マシン (**az2az3**、 **az2az4**) を作成します。 作成中に、標準のパブリック IP アドレスを各仮想マシンに割り当てます。 
   - 各マシンに少なくとも2つの管理ディスクを追加します。 
   - フェールオーバークラスタリングと記憶域レプリカの機能をインストールします。 
   
6. すべてのノードをドメインに接続し、以前に作成したユーザーに管理者特権を付与します。 

7. 仮想ネットワークの DNS サーバーをドメインコントローラーのプライベート IP アドレスに変更します。 
8. この例では、ドメインコントローラー **az2azDC**にプライベート IP アドレス (10.3.0.8) があります。 Virtual Network (**az2az**) で、DNS サーバー10.3.0.8 を変更します。 すべてのノードを "Contoso.com" に接続し、管理者特権を "contosoadmin" に指定します。
   - すべてのノードから contosoadmin としてログインします。 
    
9. クラスターを作成します (**SRAZC1**、 **SRAZC2**)。 
   この例の PowerShell コマンドを以下に示します。
   ```PowerShell
    New-Cluster -Name SRAZC1 -Node az2az1,az2az2 –StaticAddress 10.3.0.100
   ```
   ```PowerShell
    New-Cluster -Name SRAZC2 -Node az2az3,az2az4 –StaticAddress 10.3.0.101
   ```
10. 記憶域スペースダイレクトを有効にする
    ```PowerShell
    Enable-clusterS2D
    ```   
   
    クラスターごとに、仮想ディスクとボリュームを作成します。 1つはデータ用で、もう1つはログ用です。 
   
11. 各クラスター (**azlbr1**、**azlbr2**) の内部 Standard SKU [Load Balancer](https://ms.portal.azure.com/#create/Microsoft.LoadBalancer-ARM)を作成します。 
   
    クラスター IP アドレスをロードバランサーの静的プライベート IP アドレスとして指定します。
    - azlbr1 = > フロントエンド IP:10.3.0.100 (仮想ネットワーク (**az2az**) サブネットから未使用の IP アドレスを取得する)
    - 各ロードバランサーのバックエンドプールを作成します。 関連付けられているクラスターノードを追加します。
    - 正常性プローブの作成: ポート59999
    - 負荷分散規則の作成:有効な Floating IP を使用して HA ポートを許可します。 
   
    クラスター IP アドレスをロードバランサーの静的プライベート IP アドレスとして指定します。
    - azlbr2 = > フロントエンド IP:10.3.0.101 (仮想ネットワーク (**az2az**) サブネットから未使用の IP アドレスを取得する)
    - 各ロードバランサーのバックエンドプールを作成します。 関連付けられているクラスターノードを追加します。
    - 正常性プローブの作成: ポート59999
    - 負荷分散規則の作成:有効な Floating IP を使用して HA ポートを許可します。 
   
12. 各クラスターノードで、ポート 59999 (正常性プローブ) を開きます。 
   
    各ノードで次のコマンドを実行します。
    ```PowerShell
    netsh advfirewall firewall add rule name=PROBEPORT dir=in protocol=tcp action=allow localport=59999 remoteip=any profile=any 
    ```   
13. ポート59999で正常性プローブメッセージをリッスンし、現在このリソースを所有しているノードから応答するようにクラスターに指示します。 
    クラスターの1つのノードからクラスターごとに1回実行します。 
    
    この例では、構成値に応じて "ILBIP" を変更してください。 任意の1つのノード**az2az1**/**az2az2**から次のコマンドを実行します。

    ```PowerShell
     $ClusterNetworkName = "Cluster Network 1" # Cluster network name (Use Get-ClusterNetwork on Windows Server 2012 or higher to find the name. And use Get-ClusterResource to find the IPResourceName).
     $IPResourceName = "Cluster IP Address" # IP Address cluster resource name.
     $ILBIP = "10.3.0.100" # IP Address in Internal Load Balancer (ILB) - The static IP address for the load balancer configured in the Azure portal.
     [int]$ProbePort = 59999
     Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";”ProbeFailureThreshold”=5;"EnableDhcp"=0}
    ```

14. 任意の1つのノード**az2az3**/**az2az4**から次のコマンドを実行します。 

    ```PowerShell
    $ClusterNetworkName = "Cluster Network 1" # Cluster network name (Use Get-ClusterNetwork on Windows Server 2012 or higher to find the name. And use Get-ClusterResource to find the IPResourceName).
    $IPResourceName = "Cluster IP Address" # IP Address cluster resource name.
    $ILBIP = "10.3.0.101" # IP Address in Internal Load Balancer (ILB) - The static IP address for the load balancer configured in the Azure portal.
    [int]$ProbePort = 59999
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";”ProbeFailureThreshold”=5;"EnableDhcp"=0}  
    ```   
    両方のクラスターが相互に接続/通信できることを確認します。 

    フェールオーバークラスターマネージャーで [クラスターに接続] 機能を使用してもう一方のクラスターに接続するか、他のクラスターが現在のクラスターのノードのいずれかから応答することを確認してください。  
   
    ```PowerShell
     Get-Cluster -Name SRAZC1 (ran from az2az3)
    ```
    ```PowerShell
     Get-Cluster -Name SRAZC2 (ran from az2az1)
    ```   

15. 両方のクラスターにクラウド監視サーバーを作成します。 2つの[ストレージアカウント](https://ms.portal.azure.com/#create/Microsoft.StorageAccount-ARM)(**az2azcw**、 **az2azcw2**) を、同じリソースグループ (**AZ2AZ**) 内のクラスターごとに1つずつ作成します。

    - "アクセスキー" からストレージアカウントの名前とキーをコピーします。
    - "フェールオーバークラスターマネージャー" からクラウド監視を作成し、上記のアカウント名とキーを使用して作成します。

16. 次の手順に進む前に、[クラスター検証テスト](../../failover-clustering/create-failover-cluster.md#validate-the-configuration)を実行します。

17. Windows PowerShell を起動し、[Test-SRTopology](https://docs.microsoft.com/powershell/module/storagereplica/test-srtopology?view=win10-ps) コマンドレットを使用して、記憶域レプリカのすべての要件を満たしているかどうかを判別します。 クイックテストだけでなく、実行時間の長いパフォーマンス評価モードでも、このコマンドレットを使用できます。

18. クラスター間の記憶域レプリカを構成します。
   
    あるクラスターから別のクラスターへのアクセスを双方向に許可します。

    この例では、次のようになります。

    ```PowerShell
      Grant-SRAccess -ComputerName az2az1 -Cluster SRAZC2
    ```
    Windows Server 2016 を使用している場合は、次のコマンドも実行します。

    ```PowerShell
      Grant-SRAccess -ComputerName az2az3 -Cluster SRAZC1
    ```   
   
19. クラスターの SRPartnership を作成します。</ol>

    - クラスター **SRAZC1**の場合。
    - ボリュームの場所:-c:\ClusterStorage\DataDisk1
    - ログの場所:-g:
    - Cluster **SRAZC2**の場合
    - ボリュームの場所:-c:\ClusterStorage\DataDisk2
    - ログの場所:-g:

次のコマンドを実行します。

```PowerShell

New-SRPartnership -SourceComputerName SRAZC1 -SourceRGName rg01 -SourceVolumeName c:\ClusterStorage\DataDisk1 -SourceLogVolumeName  g: -DestinationComputerName **SRAZC2** -DestinationRGName rg02 -DestinationVolumeName c:\ClusterStorage\DataDisk2 -DestinationLogVolumeName  g:
```