---
title: ネットワーク アダプターを選択する
description: このトピックでは、Windows Server 2016 は、ネットワーク サブシステムのパフォーマンス チューニング ガイドの一部です。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: a6615411-83d9-495f-8a6a-1ebc8b12f164
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2b50f4b286e90a450278243c0294ea0aa7f221bc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875853"
---
# <a name="choosing-a-network-adapter"></a>ネットワーク アダプターを選択する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックを使用すると、いくつかの購買の選択に影響を与えるネットワーク アダプターの機能について説明します。

ネットワーク集中型アプリケーションでは、高パフォーマンスのネットワーク アダプターが必要です。 このセクションでは、ネットワーク アダプターと最適なネットワーク パフォーマンスを実現するために別のネットワーク アダプター設定を構成する方法の選択に関する考慮事項について説明します。

> [!TIP]
>  Windows PowerShell を使用して、ネットワーク アダプターの設定を構成できます。 詳細については、次を参照してください。 [Windows PowerShell のネットワーク アダプター コマンドレット](https://technet.microsoft.com/library/jj134956.aspx)します。

##  <a name="bkmk_offload"></a> オフロード機能

中央処理装置からタスクをオフロードする\(CPU\)ネットワーク アダプターがシステム全体のパフォーマンスを向上すると、サーバー上の CPU 使用率を減らすことができます。

マイクロソフト製品内のネットワーク スタックが 1 つにオフロードまたは多くのタスクが適切なネットワーク アダプターを選択した場合は、ネットワーク アダプターにオフロード機能します。 次の表には、Windows Server 2016 で利用できるさまざまなオフロード機能の概要が説明します。
  
|型の負荷を軽減します。|説明|
|------------------|-----------------|  
|Tcp チェックサムの計算|ネットワーク スタックは、計算と伝送制御プロトコルの検証をオフロードできます\(TCP\)上のチェックサムがコードのパスを送受信します。 計算と IPv4 の検証もオフロードでき、IPv6 のチェックサムがコードのパスを送受信します。|  
|Udp チェックサムの計算 |ネットワーク スタックは、計算とユーザー データグラム プロトコルの検証をオフロードできます\(UDP\)上のチェックサムがコードのパスを送受信します。|
|IPv4 のチェックサムの計算 |ネットワーク スタックには、計算と IPv4 のコード パスの送受信を上のチェックサムの検証をオフロードできます。 |
|IPv6 のチェックサムの計算 |ネットワーク スタックには、計算と IPv6 のコード パスの送受信を上のチェックサムの検証をオフロードできます。 | 
|大きな TCP パケットのセグメント化|TCP/IP トランスポート層は、v2 の Large Send Offload をサポートしています (LSOv2)。 LSOv2、TCP/IP トランスポート層はネットワーク アダプターに大きな TCP パケットのセグメント化をオフロードできます。|  
|Receive Side Scaling \(RSS\)|RSS は、ネットワークを効率的に分散できるようにするネットワーク ドライバー テクノロジは、マルチプロセッサ システムで複数の cpu 処理を受信します。 RSS の詳細については、このトピックの後半に提供されます。|  
|Receive Segment Coalescing \(RSC\)|RSC は、ヘッダーの処理を最小限に抑えるにまとめてグループ パケットする機能は、ホストを実行するために必要なは。 受信したペイロードの 64 KB の最大値を結合して、1 つの大きなパケット処理のためにします。 RSC の詳細については、このトピックの後半に提供されます。|  
  
###  <a name="bkmk_rss"></a> Receive Side Scaling

Windows Server 2016、Windows Server 2012、Windows Server 2012 R2、Windows Server 2008 R2、および Windows Server 2008 は、Receive Side Scaling をサポート\(RSS\)します。 

ハードウェア リソースを共有する複数の論理プロセッサを持つ一部のサーバーが構成されて\(物理コアなど\)同時マルチ スレッドとして処理されると\(SMT\)ピア。 Intel ハイパー スレッド テクノロジは、例を示します。 RSS は、ネットワーク処理コアごとに 1 つの論理プロセッサに指示します。 たとえば、Intel ハイパー スレッディング、4 コア、8 個の論理プロセッサとサーバーで RSS 処理に使用が 4 個の論理プロセッサ ネットワーク。  

RSS は、順序を維持同じ論理プロセッサ上で同じ TCP 接続に属するパケットが処理されるように、論理プロセッサ間で着信ネットワーク I/O のパケットを配布します。 

残高 UDP ユニキャストとマルチキャスト トラフィックは、RSS も読み込むし、関連するフローをルーティング\(これは、ソースおよび宛先アドレスのハッシュによって決まります\)同じ論理プロセッサに関連の到着の順序を保持します。 これにより、スケーラビリティと受信量が多いシナリオを対象となる論理プロセッサよりも少ないネットワーク アダプターを持つサーバーのパフォーマンスが向上します。 

#### <a name="configuring-rss"></a>RSS の構成

Windows Server 2016 では、Windows PowerShell コマンドレットと RSS プロファイルを使用して RSS を構成できます。 

RSS プロファイルを使用して定義することができます、 **– プロファイル**のパラメーター、 **Set-netadapterrss** Windows PowerShell コマンドレット。

**RSS 構成用の Windows PowerShell コマンド**

次のコマンドレットを使用すると、「およびネットワーク アダプターごとに RSS パラメーターを変更することができます。
  
>[!NOTE]
>各コマンドレットの構文とパラメーターを含むコマンドに関する詳細なリファレンスについては、次のリンクをクリックできます。 さらに、コマンドレット名を渡すことができます**Get-help**各コマンドの詳細について Windows PowerShell プロンプトでします。  

- [無効にする NetAdapterRss](https://technet.microsoft.com/library/jj130892)します。 このコマンドでは、指定したネットワーク アダプターで RSS を無効にします。

- [有効にする NetAdapterRss](https://technet.microsoft.com/library/jj130859)します。 このコマンドは、指定したネットワーク アダプターで RSS を使用できます。
  
- [Get-netadapterrss](https://technet.microsoft.com/library/jj130912)します。 このコマンドは、指定したネットワーク アダプターの RSS プロパティを取得します。
  
- [Set-netadapterrss](https://technet.microsoft.com/library/jj130863)します。 このコマンドは、指定したネットワーク アダプターで RSS プロパティを設定します。  

#### <a name="rss-profiles"></a>RSS プロファイル

使用することができます、 **– プロファイル**論理プロセッサは、ネットワーク アダプターに割り当てられているを指定する Set-netadapterrss コマンドレットのパラメーター。 このパラメーターの使用可能な値は次のとおりです。

- **最も近い**します。 ネットワーク アダプターの基本の RSS プロセッサ近くにある論理プロセッサ番号は、適しています。 このプロファイルでは、オペレーティング システムを論理プロセッサの負荷に基づいて動的に再調整する場合があります。
  
- **ClosestStatic**します。 ネットワーク アダプターの基本の RSS プロセッサ近くの論理プロセッサ番号は、適しています。 このプロファイルでは、オペレーティング システムが論理プロセッサの負荷に基づいて動的に再調整はできません。
  
- **NUMA**します。 一般に、論理プロセッサ番号は負荷を分散する異なる NUMA ノードで選択されています。 このプロファイルでは、オペレーティング システムを論理プロセッサの負荷に基づいて動的に再調整する場合があります。
  
- **NUMAStatic**します。 これは、**既定のプロファイル**します。 一般に、論理プロセッサ番号は負荷を分散する異なる NUMA ノードで選択されています。 このプロファイルでは、オペレーティング システムが論理プロセッサの負荷に基づいて動的に再調整はできません。

- **控えめな**します。 RSS は、できるだけ少ないプロセッサを使用して、負荷に対応します。 このオプションは、割り込みの数を減らすのに役立ちます。

シナリオ、ワークロードの特性に応じての他のパラメーターを使用することも、 **Set-netadapterrss** Windows PowerShell コマンドレットを次を指定します。

- -ネットワーク アダプターごとに、RSS の論理プロセッサの数を使用できます。
- 論理プロセッサの範囲の開始オフセットです。
- ネットワーク アダプターがメモリを割り当て元となるノードです。

次に、追加**Set-netadapterrss** RSS を構成に使用できるパラメーター。

>[!NOTE]
>ネットワーク アダプター名の下には、各パラメーターの構文の例で**イーサネット**の値の例として提供される、 **– 名前**のパラメーター、 **Set-netadapterrss**コマンド。 コマンドレットを実行するときにを使用するネットワーク アダプターの名前が環境に適していることを確認します。

- **\* MaxProcessors**:使用するには、RSS プロセッサの最大数を設定します。 これにより、特定のインターフェイスで、アプリケーション トラフィックがプロセッサの最大数にバインドされています。 構文例を次に示します。

     `Set-NetAdapterRss –Name “Ethernet” –MaxProcessors <value>`

- **\* BaseProcessorGroup**:NUMA ノードの基本のプロセッサ グループを設定します。 これにより、RSS で使用されるプロセッサの配列が影響します。 構文例を次に示します。

     `Set-NetAdapterRss –Name “Ethernet” –BaseProcessorGroup <value>`
  
- **\* MaxProcessorGroup**:NUMA ノードの最大プロセッサ グループを設定します。 これにより、RSS で使用されるプロセッサの配列が影響します。 これに設定すると、最大のプロセッサ グループが制限され k グループ内での配置は、負荷分散します。 構文例を次に示します。

     `Set-NetAdapterRss –Name “Ethernet” –MaxProcessorGroup <value>`

- **\* BaseProcessorNumber**:NUMA ノードの基本のプロセッサ数を設定します。 これにより、RSS で使用されるプロセッサの配列が影響します。 これにより、ネットワーク アダプター間でプロセッサをパーティション分割できます。 これは、範囲の RSS プロセッサの論理プロセッサの最初の各アダプターに割り当てられています。 構文例を次に示します。

     `Set-NetAdapterRss –Name “Ethernet” –BaseProcessorNumber <Byte Value>`

- **\* NumaNode**:各ネットワーク アダプターからのメモリを割り当てることができます、NUMA ノード。 K グループ内または異なる k グループを指定できます。 構文例を次に示します。

     `Set-NetAdapterRss –Name “Ethernet” –NumaNodeID <value>`

- **\* NumberofReceiveQueues**:論理プロセッサがある受信トラフィックの使用率が低いと思われる\(などで表示されているタスク マネージャーとして\)、既定値は 2 から、ネットワーク アダプターでサポートされている最大の RSS のキューの数を増やすことをお試しください. ネットワーク アダプター ドライバーの一部として RSS キュー数を変更するオプションがあります。 構文例を次に示します。

     `Set-NetAdapterRss –Name “Ethernet” –NumberOfReceiveQueues <value>`

詳細については、ダウンロードするには、次のリンクをクリックします[Scalable Networking:。受信処理のボトルネックを排除-Introducing RSS](https://download.microsoft.com/download/5/D/6/5D6EAF2B-7DDF-476B-93DC-7CF0072878E6/NDIS_RSS.doc) Word 形式。
  
#### <a name="understanding-rss-performance"></a>RSS のパフォーマンスを理解します。

RSS をチューニングするには、構成と負荷分散のロジックを理解する必要があります。 RSS 設定が有効になってを実行すると、出力を確認できることを確認する、 **Get-netadapterrss** Windows PowerShell コマンドレット。 このコマンドレットの出力例を次に示します。
  
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

設定されたパラメーターをエコーするには、だけでなくは、出力の重要な側面は、間接指定テーブルの出力を示します。 間接指定テーブルには、受信トラフィックを分散に使用されるハッシュ テーブルのバケットが表示されます。 N:c 表記が Numa K を指定する、この例では、受信トラフィックに使用される CPU グループ: インデックスのペア。 正確に 2 つの一意のエントリがわかります (0:0、0:4)、k グループ 0/cpu0 と k グループ 0 と cpu 4 をそれぞれ表しますを。

このシステム (k グループ 0) と、n に 1 つだけの k グループがある (n < = 128) 間接指定テーブル エントリ。 受信キューの数が 2、2 つだけのプロセッサに設定されているため (0:0, 0:4) 最大プロセッサは 8 に設定されていても、選択されます。 実際には、間接指定テーブルでは、のみ利用できる 8 から 2 つの Cpu を使用する着信トラフィックをハッシュは。

Cpu をフル活用するには、RSS の受信キューの数は最大プロセッサ以上をする必要があります。 前の例では、8 以上受信キューを設定する必要があります。

#### <a name="nic-teaming-and-rss"></a>NIC チーミングと RSS

NIC チーミングを使用して別のネットワーク インターフェイス カード チーミングは、ネットワーク アダプターでは、RSS を有効にすることができます。 このシナリオでは、RSS を使用する、基になる物理ネットワーク アダプターのみを構成できます。 ユーザーは、チーム化されたネットワーク アダプターで RSS コマンドレットを設定することはできません。
  
###  <a name="bkmk_rsc"></a> Receive Segment Coalescing (RSC)

Receive Segment Coalescing \(RSC\)処理が受信したデータ量が特定の IP ヘッダーの数を減らすことでパフォーマンスを向上します。 グループ化して受信したデータのパフォーマンスをスケールするために使用する必要があります\(結合または\)より大きな単位に小さいパケット。

このアプローチは、待機時間を影響のスループットの増加に示すようにほとんどの場合の利点があります。 受信の負荷の高いワークロードのスループットを増やすには、RSC をお勧めします。 RSC をサポートするネットワーク アダプターの展開を検討します。 

これらのネットワーク アダプターの RSC が上にあることを確認します\(これは、既定の設定\)特定のワークロードがない限り、\(などの低待機時間、スループットのネットワークを低\)RSC に接続して利用できる表示.

#### <a name="understanding-rsc-diagnostics"></a>RSC の診断について

RSC は、Windows PowerShell コマンドレットを使用して診断できます**Get NetAdapterRsc**と**Get NetAdapterStatistics**します。

Get NetAdapterRsc コマンドレットを実行するときの出力例を次に示します。

```  

PS C:\Users\Administrator> Get-NetAdapterRsc  
  
Name                       IPv4Enabled  IPv6Enabled  IPv4Operational IPv6Operational               IPv4FailureReason              IPv6Failure  
                                            Reason  
----                           -----------  -----------  --------------- --------------- ----------------- ------------  
Ethernet                       True         False        True            False                  NoFailure       NicProperties  
  
```  

**取得**コマンドレットは、RSC がインターフェイスで有効になっているかどうかと、TCP により、RSC を運用状態にするかどうかを示します。 失敗の理由は、そのインターフェイスの RSC を有効にするエラーの詳細を提供します。

上記のシナリオでは、IPv4 RSC は、インターフェイスでサポートされており、運用は。 診断エラーについては、1 つにまとめられたバイトまたは例外が原因で確認できます。 これは、結合の問題を示す値を提供します。

Get NetAdapterStatistics コマンドレットを実行するときの出力例を次に示します。

```  
PS C:\Users\Administrator> $x = Get-NetAdapterStatistics “myAdapter”   
PS C:\Users\Administrator> $x.rscstatistics  
  
CoalescedBytes       : 0  
CoalescedPackets     : 0  
CoalescingEvents     : 0  
CoalescingExceptions : 0  
  
```  

#### <a name="rsc-and-virtualization"></a>RSC と仮想化

RSC は、ホスト ネットワーク アダプターが HYPER-V 仮想スイッチにバインドされていない場合にのみ、物理ホストでサポートされます。 RSC は、ホストが HYPER-V 仮想スイッチにバインドされている場合、オペレーティング システムによって無効です。 さらに、仮想マシンは、仮想ネットワーク アダプターでは、RSC をサポートしていないために RSC の利点を取得できません。

仮想マシンには、RSC を有効にできるときに単一ルート入出力仮想化\(SR-IOV\)を有効にします。 この場合、仮想関数をサポートして RSC 機能です。そのため、仮想マシンでは、RSC の利点も受け取ります。

##  <a name="bkmk_resources"></a> ネットワーク アダプターのリソース

いくつかのネットワーク アダプターは、最適なパフォーマンスを実現するためのリソースを積極的に管理します。 使用してリソースを手動で構成することはいくつかのネットワーク アダプター、**高度なネットワーク**アダプターのタブ。 このようなアダプターの場合は、受信バッファーの数など、パラメーターの数値の値を設定し、バッファーを送信できます。

ネットワーク アダプターのリソースを構成すると、次の Windows PowerShell コマンドレットを使用して単純化されます。

- [Get-NetAdapterAdvancedProperty](https://technet.microsoft.com/library/jj130901.aspx)

- [Set-NetAdapterAdvancedProperty](https://technet.microsoft.com/library/jj130894.aspx)

- [Enable-NetAdapter](https://technet.microsoft.com/library/jj130876.aspx)

- [Enable-NetAdapterBinding](https://technet.microsoft.com/library/jj130913.aspx)

- [Enable-NetAdapterChecksumOffload](https://technet.microsoft.com/library/jj130918.aspx)

- [Enable-NetAdapterIPSecOffload](https://technet.microsoft.com/library/jj130890.aspx)

- [Enable-NetAdapterLso](https://technet.microsoft.com/library/jj130922.aspx)

- [Enable-NetAdapterPowerManagement](https://technet.microsoft.com/library/jj130907.aspx)

- [Enable-NetAdapterQos](https://technet.microsoft.com/library/jj130866.aspx)

- [Enable-NetAdapterRDMA](https://technet.microsoft.com/library/jj130909.aspx)

- [Enable-NetAdapterSriov](https://technet.microsoft.com/library/jj130899.aspx)

詳細については、次を参照してください。 [Windows PowerShell のネットワーク アダプター コマンドレット](https://technet.microsoft.com/library/jj134956.aspx)します。

このガイドのすべてのトピックへのリンクを参照してください。[ネットワーク サブシステムのパフォーマンス チューニング](net-sub-performance-top.md)します。