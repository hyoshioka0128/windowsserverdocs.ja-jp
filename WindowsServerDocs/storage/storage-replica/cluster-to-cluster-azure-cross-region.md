---
title: Azure リージョンを超えてクラスター間の記憶域レプリカを構成する
description: クラスターに記憶域レプリケーション間の Azure リージョン
keywords: 記憶域レプリカ、サーバー マネージャー、Windows Server、Azure では、リージョン、別のリージョン間のクラスター
author: arduppal
ms.author: arduppal
ms.date: 12/19/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage-replica
manager: mchad
ms.openlocfilehash: d9999f786639ff4aa303ed34ade14849cda8feec
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2019
ms.locfileid: "65475911"
---
# <a name="cluster-to-cluster-storage-replica-cross-region-in-azure"></a>Azure リージョンを超えてクラスター間の記憶域レプリカを構成する

> 適用対象:Windows Server 2019、Windows Server 2016、Windows Server (半期チャネル)

Azure では、リージョンをまたがるアプリケーションをクラスターにクラスターの記憶域レプリカを構成できます。 次の例では、2 つのノードを使用しますが、クラスターをクラスターに記憶域レプリカは 2 つのノードに制限はありません。 次の図は、2 つのノードの記憶域スペース ダイレクト クラスターを互いと通信できる、同じドメインには、リージョンをまたがるです。

プロセスの詳しいチュートリアルについては、以下のビデオをご覧ください。
> [!video https://www.microsoft.com/en-us/videoplayer/embed/RE26xeW]

![アーキテクチャ ダイアグラム ポジティブサムの C2C SR Azure 内で同じリージョン。](media\Cluster-to-cluster-azure-cross-region\architecture.png)
> [!IMPORTANT]
> 参照先のすべての例では、上の図に固有です。


1. Azure portal で作成[リソース グループ](https://ms.portal.azure.com/#create/Microsoft.ResourceGroup)2 つの異なるリージョンにします。

    たとえば、 **SR AZ2AZ**で**米国西部 2**と**SR AZCROSS**で**米国中西部**、上記のようです。

2. 2 つ作成[可用性セット](https://ms.portal.azure.com/#create/Microsoft.AvailabilitySet-ARM)、各クラスターのリソース グループごとに 1 つ。
    - 可用性セット (**az2azAS1**) で (**SR AZ2AZ**)
    - 可用性セット (**azcross-AS**) で (**SR AZCROSS**)

3. 2 つの仮想ネットワークを作成します。
   - 作成、[仮想ネットワーク](https://ms.portal.azure.com/#create/Microsoft.VirtualNetwork-ARM)(**az2az Vnet**) 最初のリソース グループ内 (**SR AZ2AZ**)、1 つのサブネットと 1 つのゲートウェイ サブネットを持ちます。
   - 作成、[仮想ネットワーク](https://ms.portal.azure.com/#create/Microsoft.VirtualNetwork-ARM)(**azcross VNET**) 2 つ目のリソース グループ内 (**SR AZCROSS**)、1 つのサブネットと 1 つのゲートウェイ サブネットを持ちます。

4. 2 つのネットワーク セキュリティ グループを作成します。
   - 作成、[ネットワーク セキュリティ グループ](https://ms.portal.azure.com/#create/Microsoft.NetworkSecurityGroup-ARM)(**az2az NSG**) 最初のリソース グループ内 (**SR AZ2AZ**)。
   - 作成、[ネットワーク セキュリティ グループ](https://ms.portal.azure.com/#create/Microsoft.NetworkSecurityGroup-ARM)(**azcross NSG**) 2 つ目のリソース グループ内 (**SR AZCROSS**)。

   両方のネットワーク セキュリティ グループに RDP:3389 の 1 つの受信セキュリティ規則を追加します。 セットアップが完了したら、このルールを削除することができます。

5. Windows Server の作成[仮想マシン](https://ms.portal.azure.com/#create/Microsoft.WindowsServer2016Datacenter-ARM)で以前に作成したリソース グループ。

   ドメイン コント ローラー (**az2azDC**)。 ドメイン コント ローラーの 3 番目の可用性セットを作成または 2 つの可用性セットのいずれかで、ドメイン コント ローラーを追加することができます。 これを追加する、2 つのクラスター用に作成された可用性セットには場合、割り当てる標準パブリック IP アドレス VM の作成中。
      - Active Directory ドメイン サービスをインストールします。
      - ドメイン (contoso.com) を作成します。
      - 管理者特権 (contosoadmin) を持つユーザーを作成します。

   2 つの仮想マシンの作成 (**az2az1**、 **az2az2**)、リソース グループ内 (**SR AZ2AZ**) 仮想ネットワークを使用して (**az2az Vnet**) とネットワーク セキュリティ グループ (**az2az NSG**) 可用性セット (**az2azAS1**)。 自体の作成時に、各仮想マシンに標準のパブリック IP アドレスを割り当てます。
      - 各マシンとして、少なくとも 2 つの管理対象ディスクを追加します。
      - フェールオーバー クラスタ リングと記憶域レプリカ機能をインストールします。

   2 つの仮想マシンの作成 (**azcross1**、 **azcross2**)、リソース グループ内 (**SR AZCROSS**) 仮想ネットワークを使用して (**azcross VNET**) とネットワーク セキュリティ グループ (**azcross NSG**) 可用性セット (**azcross-AS**)。 自体の作成時に、各仮想マシンに標準のパブリック IP アドレスを割り当てる
      - 各マシンに少なくとも 2 つの管理対象ディスクを追加します。
      - フェールオーバー クラスタ リングと記憶域レプリカ機能をインストールします。

   すべてのノードをドメインに接続し、以前に作成したユーザーに管理者特権を提供します。

   仮想ネットワークの DNS サーバーをドメイン コント ローラーのプライベート IP アドレスに変更します。
   - 例では、ドメイン コント ローラーで**az2azDC**がプライベート IP アドレス (10.3.0.8)。 仮想ネットワーク内 (**az2az Vnet**と**azcross VNET**) DNS サーバー 10.3.0.8 を変更します。 

    例では、"contoso.com"のすべてのノードを接続し、"contosoadmin"に、管理者権限を提供します。
   - すべてのノードから contosoadmin としてログインします。 
 
6. クラスターの作成 (**SRAZC1**、 **SRAZCross**)。

   たとえば、PowerShell コマンドを次に示します
   ```powershell
      New-Cluster -Name SRAZC1 -Node az2az1,az2az2 –StaticAddress 10.3.0.100
   ```
   ```powershell
      New-Cluster -Name SRAZCross -Node azcross1,azcross2 –StaticAddress 10.0.0.10
   ```

7. 記憶域スペース ダイレクトを有効にします。

   ```powershell
      Enable-clusterS2D
   ```

   > [!NOTE]
   > 各クラスターの仮想ディスクとボリュームを作成します。 データとログ用に別の 1 つです。

8. 内部の Standard SKU の作成[ロード バランサー](https://ms.portal.azure.com/#create/Microsoft.LoadBalancer-ARM)クラスターごとに (**azlbr1**、 **azlbazcross**)。

   ロード バランサーの静的プライベート IP アドレスとしてクラスターの IP アドレスを指定します。
      - azlbr1 = > フロント エンド IP:10.3.0.100 (仮想ネットワークから未使用の IP アドレスを取得 (**az2az Vnet**) サブネット)
      - 各ロード バランサーのバックエンド プールを作成します。 関連付けられているクラスター ノードを追加します。
      - ポート 59999 の正常性プローブを作成します。
      - 負荷分散規則を作成します。Floating IP を有効になっていると、HA ポートを許可します。

   ロード バランサーの静的プライベート IP アドレスとしてクラスターの IP アドレスを指定します。 
      - azlbazcross = > フロント エンド IP:10.0.0.10 (仮想ネットワークから未使用の IP アドレスを取得 (**azcross VNET**) サブネット)
      - 各ロード バランサーのバックエンド プールを作成します。 関連付けられているクラスター ノードを追加します。
      - ポート 59999 の正常性プローブを作成します。
      - 負荷分散規則を作成します。Floating IP を有効になっていると、HA ポートを許可します。 

9. 作成[仮想ネットワーク ゲートウェイ](https://ms.portal.azure.com/#create/Microsoft.VirtualNetworkGateway-ARM)Vnet 対 Vnet 接続用です。

 - 最初の仮想ネットワーク ゲートウェイの作成 (**az2az VNetGateway**) 最初のリソース グループ内 (**SR AZ2AZ**)
 - ゲートウェイの種類 = VPN、および VPN の種類 = ルート ベース

 - 2 番目の仮想ネットワーク ゲートウェイの作成 (**azcross VNetGateway**) 2 つ目のリソース グループ内 (**SR AZCROSS**)
 - ゲートウェイの種類 = VPN、および VPN の種類 = ルート ベース

 - 2 番目の仮想ネットワーク ゲートウェイを最初の仮想ネットワーク ゲートウェイから Vnet 対 Vnet 接続を作成します。 共有キーを提供します。

 - 最初の仮想ネットワーク ゲートウェイに 2 つ目の仮想ネットワーク ゲートウェイから Vnet 対 Vnet 接続を作成します。 上記の手順では、同じ共有キーを提供します。 

10. 各クラスター ノードでは、ポート 59999 (正常性プローブ) を開きます。

   各ノードで、次のコマンドを実行します。

   ```powershell
      netsh advfirewall firewall add rule name=PROBEPORT dir=in protocol=tcp action=allow localport=59999 remoteip=any profile=any 
   ```

11. クラスターの正常性プローブ ポート 59999 メッセージをリッスンし、このリソースを所有しているノードからの応答するように指示します。

   1 回から実行クラスターごとに、クラスターの 1 つのノード。 
    
   この例では、"ILBIP"、構成値に基づいてを変更してください。 1 つのノードから、次のコマンドを実行**az2az1**/**az2az2**

   ```PowerShell
     $ClusterNetworkName = "Cluster Network 1" # Cluster network name (Use Get-ClusterNetwork on Windows Server 2012 or higher to find the name. And use Get-ClusterResource to find the IPResourceName).
     $IPResourceName = "Cluster IP Address" # IP Address cluster resource name.
     $ILBIP = "10.3.0.100" # IP Address in Internal Load Balancer (ILB) - The static IP address for the load balancer configured in the Azure portal.
     [int]$ProbePort = 59999
     Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";”ProbeFailureThreshold”=5;"EnableDhcp"=0}  
   ```

12. 1 つのノードから、次のコマンドを実行**azcross1**/**azcross2**
   ```PowerShell
     $ClusterNetworkName = "Cluster Network 1" # Cluster network name (Use Get-ClusterNetwork on Windows Server 2012 or higher to find the name. And use Get-ClusterResource to find the IPResourceName).
     $IPResourceName = "Cluster IP Address" # IP Address cluster resource name.
     $ILBIP = "10.0.0.10" # IP Address in Internal Load Balancer (ILB) - The static IP address for the load balancer configured in the Azure portal.
     [int]$ProbePort = 59999
     Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";”ProbeFailureThreshold”=5;"EnableDhcp"=0}  
   ```

   両方のクラスターが接続/相互通信を確認してください。

   いずれか、他のクラスターに接続または他のクラスターの現在のクラスターのノードの 1 つから応答を確認するフェールオーバー クラスター マネージャーの「クラスターに接続」機能を使用します。

   例を使用しています。
   ```powershell
      Get-Cluster -Name SRAZC1 (ran from azcross1)
   ```
   ```powershell
      Get-Cluster -Name SRAZCross (ran from az2az1) 
   ```

13. 両方のクラスターのクラウド監視を作成します。 2 つ作成[ストレージ アカウント](https://ms.portal.azure.com/#create/Microsoft.StorageAccount-ARM)(**az2azcw**、**azcrosssa**)、Azure リソース グループごとに各クラスターのいずれかで (**SR AZ2AZ**、 **SR-AZCROSS**)。
   
   - [アクセス キー] から、ストレージ アカウント名とキーをコピーします。
   - 「フェールオーバー クラスター マネージャー」から、クラウドのミラーリング監視サーバーを作成し、上記のアカウント名とキーを使用して作成しています。 

14. 実行[クラスター検証テストの](../../failover-clustering/create-failover-cluster.md#validate-the-configuration)次の手順に進む前に

15. Windows PowerShell を起動し、[Test-SRTopology](https://docs.microsoft.com/powershell/module/storagereplica/test-srtopology?view=win10-ps) コマンドレットを使用して、記憶域レプリカのすべての要件を満たしているかどうかを判別します。 このコマンドレットは、簡単なテストのために要件のみモードで使用することも、実行時間の長いパフォーマンス評価モードで使用することもできます。
 
16. クラスター-クラスターの記憶域レプリカを構成します。
双方向で別のクラスターに 1 つのクラスターからのアクセスを許可します。

   例。
   ```powershell
     Grant-SRAccess -ComputerName az2az1 -Cluster SRAZCross
   ```
Windows Server 2016 を使用している場合は、このコマンドを実行しても。

   ```powershell
     Grant-SRAccess -ComputerName azcross1 -Cluster SRAZC1
   ```

17. 2 つのクラスターの記憶域レプリカのパートナーシップを作成します。</ol>

   - クラスターの**SRAZC1**
      - ボリュームの場所:-c:\ClusterStorage\DataDisk1
      - ログの場所:-g:
   - クラスターの**SRAZCross**
      - ボリュームの場所:-c:\ClusterStorage\DataDiskCross
      - ログの場所:-g:

コマンドを実行します。

```powershell
PowerShell

New-SRPartnership -SourceComputerName SRAZC1 -SourceRGName rg01 -SourceVolumeName c:\ClusterStorage\DataDisk1 -SourceLogVolumeName  g: -DestinationComputerName SRAZCross -DestinationRGName rg02 -DestinationVolumeName c:\ClusterStorage\DataDiskCross -DestinationLogVolumeName  g:
```