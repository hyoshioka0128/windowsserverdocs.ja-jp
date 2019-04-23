---
ms.assetid: a6343f1c-e9dd-4a02-91ad-39bd519d66cd
title: 簡略化された SMB マルチチャネルと複数 NIC のクラスター ネットワーク
ms.prod: windows-server-threshold
ms.technology: storage-failover-clustering
ms.topic: article
author: RobHindman
ms.author: robhind
ms.date: 09/15/2016
ms.openlocfilehash: 45d8364adf9d3db24a8e6d8f7bc91178ce7d1551
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881133"
---
# <a name="simplified-smb-multichannel-and-multi-nic-cluster-networks"></a>簡略化された SMB マルチチャネルと複数 NIC のクラスター ネットワーク

> 適用対象:Windows Server 2016 の Windows Server (半期チャネル)

簡略化された SMB マルチ チャネルおよびマルチ<abbr title="ネットワーク インターフェイス カード">NIC</abbr>クラスター ネットワークが、同じクラスターのネットワークのサブネット上の複数の Nic の使用を有効にし、SMB マルチ チャネルを自動的に有効にする Windows Server 2016 の新機能です。  

簡略化された SMB マルチ チャネルと複数 NIC のクラスター ネットワークは、次の利点を提供します。  
- すべての Nic を同じスイッチを使用しているノードで自動的に認識フェールオーバー クラスタ リング]、[同じサブネットの追加構成が必要ないです。  
- SMB マルチ チャネルは自動的に有効にします。  
- クラスター専用の (プライベート) ネットワークをのみ IPv6 リンク ローカル (fe 80) の IP アドレス リソースを持つネットワークが認識されます。  
- 1 つの IP アドレス リソースは、各クラスター アクセス ポイント (CAP) ネットワーク名 (NN) でを既定で構成されます。  
- 不要になったクラスターの検証は、同じサブネット上に複数の Nic があるときに警告メッセージを発行します。  

## <a name="requirements"></a>必要条件  
-   同じスイッチを使用して、サーバーごとの複数の Nic/サブネット。  

## <a name="how-to-take-advantage-of-multi-nic-clusters-networks-and-simplified-smb-multichannel"></a>クラスター ネットワークと簡略化された SMB マルチ チャネルを複数の NIC を活用する方法  
このセクションでは、Windows Server 2016 での新しい複数 NIC のクラスター ネットワークと簡略化された SMB マルチ チャネル機能を活用する方法について説明します。  

### <a name="use-at-least-two-networks-for-failover-clustering"></a>フェールオーバー クラスタ リングに少なくとも 2 つのネットワークを使用します。   
まれですが、ネットワーク スイッチが失敗する-フェールオーバー クラスタ リングに少なくとも 2 つのネットワークを使用するがベスト プラクティスとしています。 クラスター ハートビートにあるすべてのネットワークが使用されます。 単一障害点を回避するために、フェールオーバー クラスターの 1 つのネットワークを使用しないでください。 理想的には、必要があります複数の物理的な通信パスと、クラスター内のノードとなしの単一障害点の間。  

![フェールオーバー クラスタ リングについては、2 つのネットワーク図](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig1.png)  
**図 1: フェールオーバー クラスタ リングに少なくとも 2 つのネットワークを使用します。**  

### <a name="use-multiple-nics-across-clusters"></a>クラスター間での複数の Nic を使用します。  

記憶域と記憶域ワークロードのクラスターの両方でのクラスター間で複数の Nic を使用する場合、簡略化された SMB マルチ チャネルの最大のメリットが実現されます。 これにより、ワークロード クラスター (HYPER-V、SQL Server フェールオーバー クラスター インスタンス、記憶域レプリカなど) を使用して、SMB マルチ チャネルと結果がでネットワークのより効率的に使用できます。 収束 (細分類とも呼ばれます) でのクラスターのスケール アウト ファイル サーバー クラスターが、HYPER-V のワークロードのデータを格納するために使用される、クラスターで SQL Server フェールオーバー クラスター インスタンスは、このネットワークは、「北-南サブネット」と呼ばれる多くの場合、または位置の構成/ネットワーク. 多くのお客様は、RDMA 対応の NIC カードとスイッチに投資することにより、このネットワークのスループットを最大化します。  

![北-南 SMB サブネットの図](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig2.png)  
**図 2:最大ネットワーク スループットを実現するには、複数の Nic を使用して、スケール アウト ファイル サーバー クラスターと HYPER-V や SQL Server フェールオーバー クラスター インスタンスのクラスターの両方で - 北-南サブネットを共有します。**  

![SMB マルチ チャネルを活用する同じサブネット内の複数の Nic を使用して 2 つのクラスターのスクリーン ショット](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig3.png)  
**図 3:2 つのクラスター (storage、SQL Server 用のスケール アウト ファイル サーバー<abbr title="フェールオーバー クラスタ リング インスタンス">FCI</abbr>ワークロードの) SMB マルチ チャネルを活用して、ネットワークの向上を実現する、同じサブネット内の複数の Nic を使用して両方スループット。** 

## <a name="automatic-recognition-of-ipv6-link-local-private-networks"></a>IPv6 リンク ローカルのプライベート ネットワークの自動認識  
複数の Nic を持つ (クラスターの場合のみ) のプライベート ネットワークが検出されると、クラスターは自動的に認識 IPv6 リンク ローカル (fe 80) の IP アドレス各 NIC の各サブネットにします。 この時間を節減できる IPv6 リンク ローカル (fe 80) の IP アドレス リソースを手動で構成する必要が不要になったためです。  

1 つ以上の (クラスターの場合のみ) のプライベート ネットワークを使用する場合は、これにより、ネットワークのパフォーマンスが低下するために、サブネットを通過するルーティングが構成されていないことを確認する IPv6 ルーティングの構成を確認します。  

![フェールオーバー クラスター マネージャーの UI でのネットワークの自動構成のスクリーン ショット](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig4.png)  
**図 4:自動アドレスが IPv6 リンク ローカル (fe 80) リソースの構成**  

## <a name="throughput-and-fault-tolerance"></a>スループットとフォールト トレランス  
Windows Server 2016 は、自動的に NIC 機能を検出し、考えられる最速の構成で各 NIC の使用を試みます。 Nic チーミングは、RSS を使用して Nic および RDMA 機能を使用して Nic をすべて使用できます。 次の表は、これらのテクノロジを使用する場合、上のトレードオフをまとめたものです。 複数の RDMA 対応の Nic を使用する場合、最大のスループットが実現されます。 詳細については、次を参照してください。 [SMB Mutlichannel の基本](https://blogs.technet.microsoft.com/josebda/2012/06/28/the-basics-of-smb-multichannel-a-feature-of-windows-server-2012-and-smb-3-0/)します。

![NIC の構成がさまざまなスループットとフォールト トレランスの図解](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig5.png)  
**図 5:さまざまな NIC conifigurations のスループットおよびフォールト トレランス**   

## <a name="frequently-asked-questions"></a>よく寄せられる質問  
**クラスター ハートビートの複数の NIC のネットワーク内のすべての Nic を使用しますか。**  
    [はい]。  

**複数の NIC のネットワークをのみのクラスター通信に使用できますか。またはにのみ使用できますのクライアントとクラスター通信でしょうか。**  
    いずれかの構成は機能 - すべてのクラスター ネットワークの役割は、複数の NIC のネットワークで動作します。  

**SMB マルチ チャネルは CSV とクラスター トラフィックにも使用されるでしょうか。**  
    はい、既定ですべてのクラスターと CSV トラフィックを使用して、使用可能な複数 NIC のネットワーク。 管理者は、フェールオーバー クラスタ リングの PowerShell コマンドレットまたはフェールオーバー クラスター マネージャーの UI を使用して、ネットワークの役割を変更します。  

**SMB マルチ チャネルの設定を表示することができますか。**  
    使用して、 **Get SMBServerConfiguration**コマンドレット、EnableMultiChannel プロパティの値を検索します。  

**複数の NIC のネットワーク PlumbAllCrossSubnetRoutes 尊重クラスター共通プロパティがあるか。**  
     [はい]。  

## <a name="see-also"></a>関連項目  
- [新機能では、Windows Server フェールオーバー クラスタ リングの新機能](whats-new-in-failover-clustering.md)  
