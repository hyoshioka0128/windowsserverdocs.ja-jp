---
title: ネットワーク アダプターを選択する
description: このトピックは、Windows Server 2016 のネットワークサブシステムのパフォーマンスチューニングガイドに含まれています。
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: a6615411-83d9-495f-8a6a-1ebc8b12f164
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9271cf4e5f50adf93f421e830a226507034ac454
ms.sourcegitcommit: 1c75e4b3f5895f9fa33efffd06822dca301d4835
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77517477"
---
# <a name="choosing-a-network-adapter"></a>ネットワーク アダプターを選択する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、購入の選択肢に影響する可能性があるネットワークアダプターの機能について説明します。

ネットワーク集中型のアプリケーションには、高パフォーマンスのネットワークアダプターが必要です。 ここでは、ネットワークアダプターを選択する際の考慮事項について説明します。また、ネットワークパフォーマンスを最大限に高めるために、さまざまなネットワークアダプター設定を構成する方法についても説明します。

> [!TIP]
>  Windows PowerShell を使用して、ネットワークアダプターの設定を構成できます。 詳細については、「 [Windows PowerShell のネットワークアダプターコマンドレット](https://docs.microsoft.com/powershell/module/netadapter)」を参照してください。

##  <a name="bkmk_offload"></a>オフロード機能

中央処理装置 \(CPU\) をネットワークアダプターにオフロードすると、サーバーの CPU 使用率が低下し、システム全体のパフォーマンスが向上します。

Microsoft 製品のネットワークスタックは、適切なオフロード機能を備えたネットワークアダプターを選択した場合に、1つまたは複数のタスクをネットワークアダプターにオフロードすることができます。 次の表では、Windows Server 2016 で使用できるさまざまなオフロード機能の概要を簡単に説明します。
  
|オフロードの種類|説明|
|------------------|-----------------|  
|TCP のチェックサム計算|ネットワークスタックは、送信および受信のコードパスで TCP\) チェックサムを \(、伝送制御プロトコルの計算と検証をオフロードできます。 また、送信と受信のコードパスで、IPv4 チェックサムおよび IPv6 チェックサムの計算と検証をオフロードすることもできます。|  
|UDP のチェックサム計算 |ネットワークスタックは、送信と受信のコードパスで UDP\) チェックサムを \(、ユーザーデータグラムプロトコルの計算と検証をオフロードできます。|
|IPv4 のチェックサム計算 |ネットワークスタックは、送信および受信のコードパスで、IPv4 チェックサムの計算と検証をオフロードできます。 |
|IPv6 のチェックサム計算 |ネットワークスタックは、送信および受信のコードパスで、IPv6 チェックサムの計算と検証をオフロードできます。 | 
|大きな TCP パケットのセグメント化|TCP/IP トランスポート層は、Large Send Offload v2 (LSOv2) をサポートしています。 LSOv2 を使用すると、TCP/IP トランスポート層は、大きな TCP パケットのセグメント化をネットワークアダプターにオフロードできます。|  
|Receive Side Scaling \(RSS\)|RSS は、マルチプロセッサシステムの複数の Cpu にわたってネットワークの受信処理を効率的に分散できるようにするネットワークドライバーテクノロジです。 RSS の詳細については、このトピックの後半で説明します。|  
|RSC\) \(の受信セグメントの結合|RSC は、パケットをグループ化して、ホストが実行するために必要なヘッダー処理を最小限に抑えることができます。 受信したペイロードの最大 64 KB を1つの大きなパケットに結合して処理することができます。 RSC の詳細については、このトピックの後半で説明します。|  
  
###  <a name="bkmk_rss"></a>Receive Side Scaling

Windows Server 2016、Windows Server 2012、Windows Server 2012 R2、Windows Server 2008 R2、および Windows Server 2008 では、RSS\)\(の Receive Side Scaling がサポートされています。 

一部のサーバーは、物理コア\) などのハードウェアリソース \(を共有し、同時にマルチスレッド \(SMT\) ピアとして扱われる複数の論理プロセッサで構成されています。 Intel ハイパースレッディングテクノロジは一例です。 RSS は、ネットワーク処理をコアあたり最大1つの論理プロセッサに転送します。 たとえば、Intel ハイパースレッディング、4コア、8個の論理プロセッサを搭載したサーバーでは、RSS はネットワーク処理に4つ以下の論理プロセッサを使用します。  

RSS は、受信ネットワーク i/o パケットを論理プロセッサ間に分散して、同じ TCP 接続に属するパケットが同じ論理プロセッサ上で処理されるようにします。これにより、順序が維持されます。 

また、RSS は UDP ユニキャストトラフィックとマルチキャストトラフィックの負荷を分散し、関連するフロー \(ルーティングします。これは、送信元と送信先の\) アドレスを同じ論理プロセッサにハッシュすることによって決定され、関連する到着の順序が維持されます。 これにより、使用可能な論理プロセッサよりもネットワークアダプターの数が少ないサーバーで、受信を集中的に使用するシナリオのスケーラビリティとパフォーマンスを向上させることができます。 

#### <a name="configuring-rss"></a>RSS の構成

Windows Server 2016 では、Windows PowerShell コマンドレットと RSS プロファイルを使用して RSS を構成できます。 

RSS プロファイルを定義するには、 **Set-netadapterrss** Windows PowerShell コマンドレットの **– Profile**パラメーターを使用します。

**RSS 構成用の Windows PowerShell コマンド**

次のコマンドレットを使用すると、ネットワークアダプターごとに RSS パラメーターを表示および変更できます。
  
>[!NOTE]
>各コマンドレットの構文とパラメーターを含む詳細なコマンドリファレンスについては、次のリンクをクリックしてください。 また、各コマンドの詳細については、Windows PowerShell プロンプトで**get-help**にコマンドレット名を渡すこともできます。  

- [Set-netadapterrss を無効に](https://docs.microsoft.com/powershell/module/netadapter/Disable-NetAdapterRss)します。 このコマンドは、指定したネットワークアダプターで RSS を無効にします。

- [Set-netadapterrss を有効に](https://docs.microsoft.com/powershell/module/netadapter/Enable-NetAdapterRss)します。 このコマンドは、指定したネットワークアダプターで RSS を有効にします。
  
- [Set-netadapterrss](https://docs.microsoft.com/powershell/module/netadapter/Get-NetAdapterRss)。 このコマンドは、指定したネットワークアダプターの RSS プロパティを取得します。
  
- [Set-netadapterrss](https://docs.microsoft.com/powershell/module/netadapter/Set-NetAdapterRss)。 このコマンドは、指定したネットワークアダプターの RSS プロパティを設定します。  

#### <a name="rss-profiles"></a>RSS プロファイル

Set-netadapterrss コマンドレットの **– Profile**パラメーターを使用して、どの論理プロセッサをどのネットワークアダプターに割り当てるかを指定できます。 このパラメーターに使用できる値は次のとおりです。

- **最も近い**。 ネットワークアダプターの基本 RSS プロセッサに近い論理プロセッサ番号が推奨されます。 このプロファイルでは、オペレーティングシステムが負荷に基づいて論理プロセッサを動的に再調整することがあります。
  
- **Closeststatic**。 ネットワークアダプターの基本 RSS プロセッサの近くにある論理プロセッサ番号をお勧めします。 このプロファイルでは、オペレーティングシステムは、負荷に基づいて論理プロセッサを動的に再調整しません。
  
- **NUMA**。 多くの場合、負荷を分散するために、異なる NUMA ノードで論理プロセッサ番号が選択されます。 このプロファイルでは、オペレーティングシステムが負荷に基づいて論理プロセッサを動的に再調整することがあります。
  
- **Numastatic**。 これは**既定のプロファイル**です。 多くの場合、負荷を分散するために、異なる NUMA ノードで論理プロセッサ番号が選択されます。 このプロファイルでは、オペレーティングシステムは、負荷に基づいて論理プロセッサを動的に再調整しません。

- **控えめ**。 RSS は、負荷を維持するために、できるだけ少ないプロセッサを使用します。 このオプションを使用すると、割り込みの回数を減らすことができます。

シナリオとワークロードの特性に応じて、 **Set-netadapterrss** Windows PowerShell コマンドレットの他のパラメーターを使用して、次の項目を指定することもできます。

- ネットワークアダプターごとに、RSS に使用できる論理プロセッサの数を指定します。
- 論理プロセッサの範囲の開始オフセット。
- ネットワークアダプターがメモリを割り当てるノード。

RSS の構成に使用できる追加の**set-netadapterrss**パラメーターを次に示します。

>[!NOTE]
>次の各パラメーターの構文例では、 **set-netadapterrss**コマンドの **– name**パラメーターの値の例として、ネットワークアダプター名**Ethernet**が使用されます。 コマンドレットを実行するときは、使用するネットワークアダプターの名前が環境に適していることを確認してください。

- **\* maxprocessors**: 使用する RSS プロセッサの最大数を設定します。 これにより、アプリケーショントラフィックが特定のインターフェイスの最大プロセッサ数にバインドされます。 構文例を次に示します。

     `Set-NetAdapterRss –Name “Ethernet” –MaxProcessors <value>`

- **\* BaseProcessorGroup**: NUMA ノードの基本プロセッサグループを設定します。 これは、RSS によって使用されるプロセッサ配列に影響します。 構文例を次に示します。

     `Set-NetAdapterRss –Name “Ethernet” –BaseProcessorGroup <value>`
  
- **\* MaxProcessorGroup**: NUMA ノードの最大プロセッサグループを設定します。 これは、RSS によって使用されるプロセッサ配列に影響します。 これを設定すると、負荷分散が k グループ内に揃うように、最大プロセッサグループが制限されます。 構文例を次に示します。

     `Set-NetAdapterRss –Name “Ethernet” –MaxProcessorGroup <value>`

- **\* BaseProcessorNumber**: NUMA ノードの基本プロセッサ番号を設定します。 これは、RSS によって使用されるプロセッサ配列に影響します。 これにより、ネットワークアダプター間でプロセッサをパーティション分割できます。 これは、各アダプターに割り当てられている RSS プロセッサの範囲内の最初の論理プロセッサです。 構文例を次に示します。

     `Set-NetAdapterRss –Name “Ethernet” –BaseProcessorNumber <Byte Value>`

- **\* NumaNode**: 各ネットワークアダプターがメモリを割り当てることができる NUMA ノード。 これは、k グループ内、または異なる k グループのいずれかにすることができます。 構文例を次に示します。

     `Set-NetAdapterRss –Name “Ethernet” –NumaNodeID <value>`

- **NumberofReceiveQueues の\*** : 受信トラフィックに対して論理プロセッサの使用率が低いと思われる場合は \(タスクマネージャー\)で表示されているように、RSS キューの数を既定値の2からネットワークアダプターでサポートされている最大値に増やします。 ネットワークアダプターには、ドライバーの一部として RSS キューの数を変更するオプションがある場合があります。 構文例を次に示します。

     `Set-NetAdapterRss –Name “Ethernet” –NumberOfReceiveQueues <value>`

詳細については、次のリンクをクリックして、拡張性の高いネットワークをダウンロードし[ます。受信処理のボトルネックを排除](https://download.microsoft.com/download/5/D/6/5D6EAF2B-7DDF-476B-93DC-7CF0072878E6/NDIS_RSS.doc)する: Word 形式で RSS を紹介します。
  
#### <a name="understanding-rss-performance"></a>RSS パフォーマンスについて

RSS を調整するには、構成と負荷分散ロジックを理解する必要があります。 RSS 設定が有効になっていることを確認するには、 **Set-netadapterrss** Windows PowerShell コマンドレットを実行したときに出力を確認します。 このコマンドレットの出力例を次に示します。
  
```

PS C:\Users\Administrator> get-netadapterrss  
Name                           : testnic 2  
InterfaceDescription           : Broadcom BCM5708C NetXtreme II GigE (NDIS VBD Client) #66
Enabled                        : True
NumberOfReceiveQueues          : 2
Profile                        : NUMAStatic
BaseProcessor: [Group:Number]  : 0:0
MaxProcessor: [Group:Number]   : 0:15
MaxProcessors                  : 8
  
IndirectionTable: [Group:Number]:
     0:0    0:4    0:0    0:4    0:0    0:4    0:0    0:4  
…   
(# indirection table entries are a power of 2 and based on # of processors)  
…   
                          0:0    0:4    0:0    0:4    0:0    0:4    0:0    0:4  
```  

設定されたパラメーターをエコーするだけでなく、出力の主要な側面は間接テーブルの出力です。 "間接" テーブルには、着信トラフィックの分散に使用されるハッシュテーブルバケットが表示されます。 この例では、n:c 表記によって、受信トラフィックを送信するために使用される Numa K-Group: CPU インデックスペアが指定されています。 一意のエントリ (0:0 と 0:4) が2つだけ表示されます。これは、それぞれ k-group 0/cpu0 と k-group 0/cpu 4 を表します。

このシステム (k グループ 0) と n (n < = 128) の間接テーブルエントリには、k グループが1つだけあります。 受信キューの数は2に設定されているため、最大プロセッサ数が8に設定されている場合でも、2つのプロセッサ (0:0、0:4) のみが選択されます。 実際には、間接テーブルは受信トラフィックをハッシュして、使用可能な8から2つの Cpu のみを使用します。

Cpu を最大限に活用するには、RSS 受信キューの数が最大プロセッサ以上である必要があります。 前の例では、受信キューを8以上に設定する必要があります。

#### <a name="nic-teaming-and-rss"></a>NIC チーミングと RSS

NIC チーミングを使用して、別のネットワークインターフェイスカードとチーミングされているネットワークアダプターで RSS を有効にすることができます。 このシナリオでは、基になる物理ネットワークアダプターのみが RSS を使用するように構成できます。 ユーザーは、チーム化されたネットワークアダプターで RSS コマンドレットを設定することはできません。
  
###  <a name="bkmk_rsc"></a>受信セグメント合体 (RSC)

受信したデータ量に対して処理される IP ヘッダーの数を減らすことによって、RSC\) \(受信セグメントを結合することで、パフォーマンスを向上させることができます。 これは、\(をグループ化するか、小さいパケット\) 結合して、より大きな単位に分割することで、受信したデータのパフォーマンスを向上させるために使用する必要があります。

この方法は、ほとんどの場合、スループットの向上による待機時間に影響を与える可能性があります。 受信負荷の高いワークロードのスループットを向上させるには、RSC をお勧めします。 RSC をサポートするネットワークアダプターを展開することを検討してください。 

これらのネットワークアダプターでは、rsc がオン \(になっていることを確認します。これは、特定のワーク \(ロード (たとえば、低待機時間、低スループットのネットワーク\)、RSC がオフになっていることを示す\)など) がない限り、既定の設定です。

#### <a name="understanding-rsc-diagnostics"></a>RSC 診断について

RSC を診断するには、Windows PowerShell コマンドレット**NetAdapterRsc**と**NetAdapterStatistics**を使用します。

NetAdapterRsc コマンドレットを実行したときの出力例を次に示します。

```  

PS C:\Users\Administrator> Get-NetAdapterRsc  
  
Name                       IPv4Enabled  IPv6Enabled  IPv4Operational IPv6Operational               IPv4FailureReason              IPv6Failure  
                                            Reason  
----                           -----------  -----------  --------------- --------------- ----------------- ------------  
Ethernet                       True         False        True            False                  NoFailure       NicProperties  
  
```  

**Get**コマンドレットは、インターフェイスで rsc が有効になっているかどうか、および TCP が rsc を動作状態にできるかどうかを示します。 このエラーの理由により、そのインターフェイスで RSC を有効にできなかったことが詳細に示されます。

前のシナリオでは、IPv4 RSC がサポートされており、インターフェイスで操作できます。 診断エラーを理解するために、結合されたバイトまたは例外が発生したことを確認できます。 これにより、結合の問題が示されます。

NetAdapterStatistics コマンドレットを実行したときの出力例を次に示します。

```  
PS C:\Users\Administrator> $x = Get-NetAdapterStatistics “myAdapter”   
PS C:\Users\Administrator> $x.rscstatistics  
  
CoalescedBytes       : 0  
CoalescedPackets     : 0  
CoalescingEvents     : 0  
CoalescingExceptions : 0  
  
```  

#### <a name="rsc-and-virtualization"></a>RSC と仮想化

RSC は、ホストネットワークアダプターが Hyper-v 仮想スイッチにバインドされていない場合にのみ、物理ホストでサポートされます。 ホストが Hyper-v 仮想スイッチにバインドされている場合、オペレーティングシステムは RSC を無効にします。 また、仮想ネットワークアダプターでは RSC がサポートされないため、仮想マシンで RSC の利点は得られません。

単一のルート入出力仮想化 \(SR-IOV\) が有効になっている場合、仮想マシンに対して RSC を有効にすることができます。 この場合、仮想関数は RSC 機能をサポートしています。そのため、仮想マシンは RSC の利点も得られます。

##  <a name="bkmk_resources"></a>ネットワークアダプターのリソース

ネットワークアダプターの中には、最適なパフォーマンスを実現するためにリソースを積極的に管理するものがあります。 複数のネットワークアダプターを使用すると、アダプターの **[ネットワークの詳細設定**] タブを使用してリソースを手動で構成できます。 このようなアダプターでは、受信バッファーの数や送信バッファーなど、多数のパラメーターの値を設定できます。

次の Windows PowerShell コマンドレットを使用すると、ネットワークアダプターのリソースの構成が簡単になります。

- [NetAdapterAdvancedProperty](https://docs.microsoft.com/powershell/module/netadapter/Get-NetAdapterAdvancedProperty)

- [NetAdapterAdvancedProperty](https://docs.microsoft.com/powershell/module/netadapter/Set-NetAdapterAdvancedProperty)

- [有効にする-NetAdapter](https://docs.microsoft.com/powershell/module/netadapter/Enable-NetAdapte)

- [NetAdapterBinding](https://docs.microsoft.com/powershell/module/netadapter/Enable-NetAdapterBinding)

- [NetAdapterChecksumOffload](https://docs.microsoft.com/powershell/module/netadapter/Enable-NetAdapterChecksumOffload)

- [NetAdapterIPSecOffload](https://docs.microsoft.com/powershell/module/netadapter/Enable-NetAdapterChecksumOffload)

- [NetAdapterLso](https://docs.microsoft.com/powershell/module/netadapter/Enable-NetAdapterLso)

- [NetAdapterPowerManagement](https://docs.microsoft.com/powershell/module/netadapter/Enable-NetAdapterPowerManagement)

- [Get-netadapterqos](https://docs.microsoft.com/powershell/module/netadapter/Enable-NetAdapterQos)

- [NetAdapterRDMA](https://docs.microsoft.com/powershell/module/netadapter/Enable-NetAdapterRDMA)

- [Get-netadaptersriov](https://docs.microsoft.com/powershell/module/netadapter/Enable-NetAdapterSriov)

詳細については、「 [Windows PowerShell のネットワークアダプターコマンドレット](https://docs.microsoft.com/powershell/module/netadapter)」を参照してください。

このガイドのすべてのトピックへのリンクについては、「[ネットワークサブシステムのパフォーマンスチューニング](net-sub-performance-top.md)」を参照してください。
