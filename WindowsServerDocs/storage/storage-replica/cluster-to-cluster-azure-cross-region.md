---
title: Azure リージョンを超えてクラスター間の記憶域レプリカを構成する
description: Azure のクラスターからクラスターへのストレージレプリケーションのクロスリージョン
author: arduppal
ms.author: arduppal
ms.date: 12/19/2018
ms.topic: article
ms.prod: windows-server
ms.technology: storage-replica
manager: mchad
ms.openlocfilehash: ee4f508cf0a65b59c3253d6865c649cc9652c569
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856305"
---
# <a name="cluster-to-cluster-storage-replica-cross-region-in-azure"></a>Azure リージョンを超えてクラスター間の記憶域レプリカを構成する

> 適用対象: Windows Server 2019、Windows Server 2016、Windows Server (半期チャネル)

Azure でリージョンをまたがるアプリケーションのストレージレプリカをクラスター化するようにクラスターを構成できます。 次の例では、2ノードクラスターを使用していますが、クラスターへのクラスターの記憶域レプリカは2ノードクラスターに制限されていません。 次の図は、相互に通信できる2ノード記憶域スペースダイレクトクラスターであり、同じドメイン内にあり、リージョンが異なる場合があります。

プロセスの完全なチュートリアルについては、以下のビデオをご覧ください。
> [!video https://www.microsoft.com/videoplayer/embed/RE26xeW]

![Azure での C2C SR を示すアーキテクチャ図は、同じリージョンにあります。](media/Cluster-to-cluster-azure-cross-region/architecture.png)
> [!IMPORTANT]
> 参照されるすべての例は、上記の図に固有です。


1. Azure portal で、2つの異なるリージョンに[リソースグループ](https://ms.portal.azure.com/#create/Microsoft.ResourceGroup)を作成します。

    たとえば、上の例のように、**米国西部 2**および**sr-iov**の**AZ2AZ** **は米国中西部にあり**ます。

2. 各クラスターの各リソースグループに1つずつ、2つの[可用性セット](https://ms.portal.azure.com/#create/Microsoft.AvailabilitySet-ARM)を作成します。
    - の可用性セット (**az2azAS1**) (**AZ2AZ**)
    - の可用性セット (**azcross**) (**sr-iov クロス**)

3. 2つの仮想ネットワークを作成する
   - 1つのサブネットと1つのゲートウェイサブネットを持つ、1つ目のリソースグループ (**az2az**) に[仮想ネットワーク](https://ms.portal.azure.com/#create/Microsoft.VirtualNetwork-ARM)(**az2az**) を作成します。
   - 2つ目のリソースグループ (**SR-IOV クロス**) に[仮想ネットワーク](https://ms.portal.azure.com/#create/Microsoft.VirtualNetwork-ARM)(**azcross VNET**) を作成し、1つのサブネットと1つのゲートウェイサブネットを作成します。

4. 2つのネットワークセキュリティグループを作成する
   - 最初のリソースグループ (**az2az**) に[ネットワークセキュリティグループ](https://ms.portal.azure.com/#create/Microsoft.NetworkSecurityGroup-ARM)(**az2az-nsg**) を作成します。
   - 2つ目のリソースグループ (**SR-IOV クロス**) に[ネットワークセキュリティグループ](https://ms.portal.azure.com/#create/Microsoft.NetworkSecurityGroup-ARM)(**azcross nsg**) を作成します。

   RDP: 3389 の1つの受信セキュリティ規則を両方のネットワークセキュリティグループに追加します。 セットアップが完了したら、この規則を削除することを選択できます。

5. 以前に作成したリソースグループに Windows Server[仮想マシン](https://ms.portal.azure.com/#create/Microsoft.WindowsServer2016Datacenter-ARM)を作成します。

   ドメインコントローラー (**az2azDC**)。 ドメインコントローラーの3つ目の可用性セットを作成するか、2つの可用性セットのいずれかにドメインコントローラーを追加するかを選択できます。 2つのクラスター用に作成された可用性セットにこれを追加する場合は、VM の作成時に標準のパブリック IP アドレスを割り当てます。
      - Active Directory ドメインサービスをインストールします。
      - ドメインを作成する (contoso.com)
      - 管理者特権を持つユーザーを作成する (contosoadmin)

   可用性セット (**AZ2AZ**) で仮想ネットワーク (**AZ2AZ**) とネットワークセキュリティグループ (**az2azAS1**) を使用して、リソースグループ (**AZ2AZ**) に2つの仮想マシン (**az2az1**、 **az2az2**) を作成します。 作成中に、各仮想マシンに標準のパブリック IP アドレスを割り当てます。
      - 各コンピューターに少なくとも2つの管理ディスクを追加する
      - フェールオーバークラスタリングと記憶域レプリカ機能をインストールする

   可用性セット (**azcross**) で仮想ネットワーク (**azcross VNET**) とネットワークセキュリティグループ (**azcross nsg**) を使用して、リソースグループ (**sr-iov**) に2つの仮想マシン (**azcross1**、 **azcross2**) を作成します。 作成中に標準のパブリック IP アドレスを各仮想マシンに割り当てる
      - 各コンピューターに少なくとも2つの管理ディスクを追加する
      - フェールオーバークラスタリングと記憶域レプリカ機能をインストールする

   すべてのノードをドメインに接続し、以前に作成したユーザーに管理者特権を付与します。

   仮想ネットワークの DNS サーバーをドメインコントローラーのプライベート IP アドレスに変更します。
   - この例では、ドメインコントローラー **az2azDC**にプライベート IP アドレス (10.3.0.8) があります。 Virtual Network (**az2az**と**azcross vnet**) で、DNS サーバー10.3.0.8 を変更します。 

     この例では、すべてのノードを "contoso.com" に接続し、管理者特権を "contosoadmin" に指定します。
   - すべてのノードから contosoadmin としてログインします。 
 
6. クラスターを作成します (**SRAZC1**、 **SRAZCross**)。

   例の PowerShell コマンドを次に示します。
   ```powershell
      New-Cluster -Name SRAZC1 -Node az2az1,az2az2 –StaticAddress 10.3.0.100
   ```
   ```powershell
      New-Cluster -Name SRAZCross -Node azcross1,azcross2 –StaticAddress 10.0.0.10
   ```

7. 記憶域スペースダイレクトを有効にします。

   ```powershell
      Enable-clusterS2D
   ```

   > [!NOTE]
   > クラスターごとに、仮想ディスクとボリュームを作成します。 1つはデータ用で、もう1つはログ用です。

8. 各クラスター (**azlbr1**、 **azlbazcross**) の内部 Standard SKU [Load Balancer](https://ms.portal.azure.com/#create/Microsoft.LoadBalancer-ARM)を作成します。

   クラスター IP アドレスをロードバランサーの静的プライベート IP アドレスとして指定します。
      - azlbr1 = > フロントエンド IP: 10.3.0.100 (仮想ネットワーク (**az2az**) サブネットから未使用の ip アドレスを取得する)
      - 各ロードバランサーのバックエンドプールを作成します。 関連付けられているクラスターノードを追加します。
      - 正常性プローブの作成: ポート59999
      - 負荷分散規則の作成: 有効な Floating IP を使用して HA ポートを許可します。

   クラスター IP アドレスをロードバランサーの静的プライベート IP アドレスとして指定します。 
      - azlbazcross = > フロントエンド IP: 10.0.0.10 (仮想ネットワーク (**AZクロス VNET**) サブネットから未使用の ip アドレスを取得する)
      - 各ロードバランサーのバックエンドプールを作成します。 関連付けられているクラスターノードを追加します。
      - 正常性プローブの作成: ポート59999
      - 負荷分散規則の作成: 有効な Floating IP を使用して HA ポートを許可します。 

9. Vnet 間接続用の[仮想ネットワークゲートウェイ](https://ms.portal.azure.com/#create/Microsoft.VirtualNetworkGateway-ARM)を作成します。

   - 1つ目のリソースグループに最初の仮想ネットワークゲートウェイ (**az2az-VNetGateway**) を作成する (**az2az**)
   - ゲートウェイの種類 = VPN、VPN の種類 = ルートベース

   - 2番目のリソースグループ (**SR-IOV クロス**) に2つ目の仮想ネットワークゲートウェイ (**Azcross vnetgateway**) を作成します。
   - ゲートウェイの種類 = VPN、VPN の種類 = ルートベース

   - 最初の仮想ネットワークゲートウェイから2番目の仮想ネットワークゲートウェイへの Vnet 間接続を作成します。 共有キーを指定する

   - 2番目の仮想ネットワークゲートウェイから最初の仮想ネットワークゲートウェイへの Vnet 間接続を作成します。 前の手順で指定したものと同じ共有キーを指定します。 

10. 各クラスターノードで、ポート 59999 (正常性プローブ) を開きます。

    各ノードで次のコマンドを実行します。

    ```powershell
      netsh advfirewall firewall add rule name=PROBEPORT dir=in protocol=tcp action=allow localport=59999 remoteip=any profile=any 
    ```

11. ポート59999で正常性プローブメッセージをリッスンし、現在このリソースを所有しているノードから応答するようにクラスターに指示します。

    クラスターの1つのノードからクラスターごとに1回実行します。 
    
    この例では、構成値に応じて "ILBIP" を変更してください。 任意の1つのノード**az2az1**/**az2az2**から次のコマンドを実行します。

    ```PowerShell
     $ClusterNetworkName = "Cluster Network 1" # Cluster network name (Use Get-ClusterNetwork on Windows Server 2012 or higher to find the name. And use Get-ClusterResource to find the IPResourceName).
     $IPResourceName = "Cluster IP Address" # IP Address cluster resource name.
     $ILBIP = "10.3.0.100" # IP Address in Internal Load Balancer (ILB) - The static IP address for the load balancer configured in the Azure portal.
     [int]$ProbePort = 59999
     Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"ProbeFailureThreshold"=5;"EnableDhcp"=0}  
    ```

12. 任意の1つのノード**azcross1**/**azcross2**から次のコマンドを実行します。
    ```PowerShell
     $ClusterNetworkName = "Cluster Network 1" # Cluster network name (Use Get-ClusterNetwork on Windows Server 2012 or higher to find the name. And use Get-ClusterResource to find the IPResourceName).
     $IPResourceName = "Cluster IP Address" # IP Address cluster resource name.
     $ILBIP = "10.0.0.10" # IP Address in Internal Load Balancer (ILB) - The static IP address for the load balancer configured in the Azure portal.
     [int]$ProbePort = 59999
     Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"ProbeFailureThreshold"=5;"EnableDhcp"=0}  
    ```

    両方のクラスターが相互に接続/通信できることを確認します。

    フェールオーバークラスターマネージャーで [クラスターに接続] 機能を使用してもう一方のクラスターに接続するか、他のクラスターが現在のクラスターのノードのいずれかから応答することを確認してください。

    次の例では、を使用しています。
    ```powershell
      Get-Cluster -Name SRAZC1 (ran from azcross1)
    ```
    ```powershell
      Get-Cluster -Name SRAZCross (ran from az2az1) 
    ```

13. 両方のクラスターのクラウド監視を作成します。 Azure に2つの[ストレージアカウント](https://ms.portal.azure.com/#create/Microsoft.StorageAccount-ARM)(**az2azcw**、**azクロス sa**) を作成します。各リソースグループの各クラスターに1つずつ (**AZ2AZ**、 **sr-iov クロス**) 作成します。
   
    - "アクセスキー" からストレージアカウントの名前とキーをコピーします。
    - "フェールオーバークラスターマネージャー" からクラウド監視を作成し、上記のアカウント名とキーを使用して作成します。 

14. 次の手順に進む前に、[クラスター検証テスト](../../failover-clustering/create-failover-cluster.md#validate-the-configuration)を実行してください

15. Windows PowerShell を起動し、[Test-SRTopology](https://docs.microsoft.com/powershell/module/storagereplica/test-srtopology?view=win10-ps) コマンドレットを使用して、記憶域レプリカのすべての要件を満たしているかどうかを判別します。 このコマンドレットは、簡単なテストのために要件のみモードで使用することも、実行時間の長いパフォーマンス評価モードで使用することもできます。
 
16. クラスター間の記憶域レプリカを構成します。
    あるクラスターから別のクラスターへのアクセスを双方向に許可します。

    例を次に示します。
    ```powershell
     Grant-SRAccess -ComputerName az2az1 -Cluster SRAZCross
    ```
    Windows Server 2016 を使用している場合は、次のコマンドも実行します。

    ```powershell
     Grant-SRAccess -ComputerName azcross1 -Cluster SRAZC1
    ```

17. 2つのクラスターのための SR パートナーシップを作成します。</ol>

    - Cluster **SRAZC1**の場合
      - ボリュームの場所:-c:\ClusterStorage\DataDisk1
      - ログの場所:-g:
    - Cluster **SRAZCross**の場合
      - ボリュームの場所:-c:\ClusterStorage\DataDiskCross
      - ログの場所:-g:

次のコマンドを実行します。

```powershell
PowerShell

New-SRPartnership -SourceComputerName SRAZC1 -SourceRGName rg01 -SourceVolumeName c:\ClusterStorage\DataDisk1 -SourceLogVolumeName  g: -DestinationComputerName SRAZCross -DestinationRGName rg02 -DestinationVolumeName c:\ClusterStorage\DataDiskCross -DestinationLogVolumeName  g:
```