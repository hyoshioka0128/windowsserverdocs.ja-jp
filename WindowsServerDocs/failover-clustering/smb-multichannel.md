---
ms.assetid: a6343f1c-e9dd-4a02-91ad-39bd519d66cd
title: "簡素化された SMB マルチ チャネルと複数 NIC のクラスター ネットワーク"
ms.prod: windows-server-threshold
ms.technology: storage-failover-clustering
ms.topic: article
author: RobHindman
ms.author: robhind
ms.date: 09/15/2016
ms.openlocfilehash: 45d8364adf9d3db24a8e6d8f7bc91178ce7d1551
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="simplified-smb-multichannel-and-multi-nic-cluster-networks"></a>簡素化された SMB マルチ チャネルと複数 NIC のクラスター ネットワーク

> 適用対象: Windows Server (半期チャネル)、Windows Server 2016

SMB マルチ チャネルとマルチを簡略化された<abbr title="ネットワーク インターフェイス カード">NIC</abbr>クラスター ネットワークが、同じクラスター ネットワーク サブネット上の複数の Nic の使用を有効にして SMB マルチ チャネルを自動的に有効にする Windows Server 2016 の新機能です。  

簡素化された SMB マルチ チャネルと複数 NIC のクラスター ネットワークは、次の利点を提供します。  
- すべての Nic が、同じスイッチを使用しているノードで自動的に認識フェールオーバー クラスタ リング]、[同じサブネットの追加構成が必要ないです。  
- SMB マルチ チャネルは自動的に有効にします。  
- クラスター専用 (プライベート) ネットワークにのみ IPv6 リンク ローカル (fe 80) の IP アドレスのリソースを持つネットワークが認識されます。  
- 1 つの IP アドレス リソースでは、各クラスター アクセス ポイント (CAP) ネットワーク名 (NN) でを既定で構成されます。  
- クラスター検証を不要になったは、同じサブネット上の複数の Nic が見つかったときに、警告メッセージを発行します。  

## <a name="requirements"></a>要件  
-   同じスイッチを使用して、サーバーごとの複数の Nic/サブネット。  

## <a name="how-to-take-advantage-of-multi-nic-clusters-networks-and-simplified-smb-multichannel"></a>クラスター ネットワークおよび簡素化された SMB マルチ チャネルを複数 NIC の活用する方法  
このセクションでは、Windows Server 2016 での新しい複数 NIC のクラスター ネットワークと簡略化された SMB マルチ チャネル機能を活用する方法について説明します。  

### <a name="use-at-least-two-networks-for-failover-clustering"></a>フェールオーバー クラスタ リング用には、少なくとも 2 つのネットワークを使用します。   
まれですが、ネットワーク スイッチが失敗する - フェールオーバー クラスタ リング用には、少なくとも 2 つのネットワークを使用することを引き続きお勧めします。 検出されたすべてのネットワークでは、クラスターのハートビートが使用されます。 単一障害点を回避するために、フェールオーバー クラスターの 1 つのネットワークを使用しないでください。 理想的がある複数の物理的な通信パス、クラスター内のノードとない単一障害点の間。  

![フェールオーバー クラスタ リングの 2 つのネットワーク図](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig1.png)  
**図 1: フェールオーバー クラスタ リング用には、少なくとも 2 つのネットワークを使用します。**  

### <a name="use-multiple-nics-across-clusters"></a>クラスター間で複数の Nic を使用してください。  

複数の Nic を複数のクラスターの記憶域と記憶域ワークロードのクラスターの両方で使用する場合は、簡素化された SMB マルチ チャネルの利点を最大限が実現されます。 これにより、ネットワークの使用をより効率的なワークロード クラスター (Hyper-V、SQL Server フェールオーバー クラスタ インスタンス、記憶域レプリカなど) を SMB マルチ チャネルと結果を使用します。 収束 (非集約型とも呼ばれます) でクラスターの構成で、対応するスケール アウト ファイル サーバー クラスターが Hyper-V のワークロードのデータを格納するために使用されるまたは SQL Server フェールオーバー クラスタ インスタンス クラスターでは、このネットワーク「北南サブネット」とも呼ばれます/ネットワークします。 多くのお客様は、RDMA 対応の NIC カードとスイッチに投資することによって、このネットワークのスループットを最大化します。  

![北南 SMB サブネットの図](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig2.png)  
**図 2: の [最大ネットワーク スループットを実現するには、スケール アウト ファイル サーバー クラスターと Hyper-V や SQL Server フェールオーバー クラスタ インスタンス クラスター - 北南サブネットを共有する両方で使用複数の Nic**  

![SMB マルチ チャネルを活用する同じサブネット内の複数の Nic を使用して 2 つのクラスターの [screencap]](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig3.png)  
**図 3: 2 つのクラスター (記憶域、SQL Server 用のスケール アウト ファイル サーバー<abbr title="フェールオーバー クラスタ リング インスタンス">FCI</abbr>ワークロードの) どちらも、SMB マルチ チャネルを活用し、ネットワーク スループットを向上させる、同じサブネット内の複数の Nic を使用します。** 

## <a name="automatic-recognition-of-ipv6-link-local-private-networks"></a>IPv6 リンク ローカル プライベート ネットワークの自動認識  
(クラスターのみ) のプライベート ネットワークと複数 Nic が検出されると、クラスターは自動的に認識 IPv6 リンク ローカル (fe 80) の IP アドレス各 NIC の各サブネットにします。 このセーブ データ管理者時間 IPv6 リンク ローカル (fe 80) の IP アドレス リソースを手動で構成する必要がなくなったため。  

プライベート (クラスターのみ) の 1 つ以上のネットワークを使用する場合は、ネットワークのパフォーマンスが減少するので、サブネットを通過するルーティングが構成されていないことを確認する IPv6 ルーティングの構成を確認します。  

![フェールオーバー クラスター マネージャーの UI でのネットワークの自動構成の [screencap]](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig4.png)  
**図 4: IPv6 リンク ローカル (fe 80) アドレスの自動リソースの構成**  

## <a name="throughput-and-fault-tolerance"></a>スループットとフォールト トレランス  
Windows Server 2016 は自動的に NIC の機能を検出し、各 NIC を最速の可能な構成で使用を試みます。 チーム化された Nic、RSS を使用して Nic および枚の RDMA 機能をすべて使用できます。 次の表は、これらのテクノロジを使用する場合のトレードオフをまとめたものです。 複数の RDMA 対応の Nic を使用する場合は、最大スループットが実現されます。 詳細については、次を参照してください。[SMB Mutlichannel の基本](https://blogs.technet.microsoft.com/josebda/2012/06/28/the-basics-of-smb-multichannel-a-feature-of-windows-server-2012-and-smb-3-0/)します。

![NIC のさまざまな構成のスループットとフォールト トレランスの図](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig5.png)  
**さまざまな NIC conifigurations の図 5: スループットとフォールト トレランス**   

## <a name="frequently-asked-questions"></a>よく寄せられる質問  
**クラスターのハートビートの複数 NIC のネットワーク内のすべての Nic を使用しますか。**  
    うん。  

**複数 NIC のネットワークは、クラスターの通信にのみ使用できますか。 または、のみを使用するクライアントとクラスター通信のですか。**  
    いずれかの構成は機能 - クラスター ネットワークのすべての役割が複数 NIC のネットワークで動作します。  

**SMB マルチ チャネルにも使用とクラスターの CSV トラフィックですか。**  
    はい、既定ですべてのクラスターと CSV トラフィックは複数 NIC の利用可能なネットワーク使用できます。 管理者は、フェールオーバー クラスタ リングの PowerShell コマンドレットまたはフェールオーバー クラスター マネージャーの UI を使用してネットワークの役割を変更することができます。  

**SMB マルチ チャネルの設定を表示する方法**  
    使用して、**Get SMBServerConfiguration**コマンドレット、EnableMultiChannel プロパティの値を探します。  

**複数 NIC のネットワーク上の PlumbAllCrossSubnetRoutes 尊重クラスター共通プロパティですか。**  
     うん。  

## <a name="see-also"></a>参照してください。  
- [Windows Server のフェールオーバー クラスタ リングの新機能](whats-new-in-failover-clustering.md)  
