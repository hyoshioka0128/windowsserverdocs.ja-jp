---
title: ネットワーク アダプターを選択します。
description: このトピックは、Windows Server 2016 のネットワーク サブシステムのパフォーマンス チューニング ガイドの一部です。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: a6615411-83d9-495f-8a6a-1ebc8b12f164
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4b3b9d206273dfd0e9115ebc27cf28aa960bfb0f
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="choosing-a-network-adapter"></a>ネットワーク アダプターを選択します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、いくつかの購入、選択内容に影響を与えるネットワーク アダプターの機能について説明します。

ネットワーク負荷の高いアプリケーションでは、高パフォーマンスのネットワーク アダプターが必要です。 このセクションでは、ネットワーク アダプターと、最適なネットワーク パフォーマンスを実現するために別のネットワーク アダプターの設定を構成する方法の選択に関する考慮事項について説明します。

> [!TIP]
>  ネットワーク アダプターの設定を構成するには、Windows PowerShell を使用します。 詳細については、次を参照してください。[Windows PowerShell のネットワーク アダプター コマンドレット](https://technet.microsoft.com/library/jj134956.aspx)します。

##  <a name="bkmk_offload"></a>オフロード機能

中央処理装置からタスクをオフロードするネットワーク アダプターに \(CPU\) はシステム全体のパフォーマンスが向上と、サーバー上の CPU 使用率を削減できます。

Microsoft 製品で、ネットワーク スタックのいずれかの負荷を軽減できますかより多くのタスクを持つ適切なネットワーク アダプターを選択した場合は、ネットワーク アダプターにオフロード機能します。 次の表は、Windows Server 2016 で利用できるさまざまなオフロード機能の概要を示します。
  
|オフロードの種類|説明|
|------------------|-----------------|  
|TCP のチェックサムの計算|ネットワーク スタックが、計算の負荷を軽減し、上の伝送制御プロトコル \(TCP\) チェックサムの検証コード パスを送受信します。 IPv6 チェックサムの送受信を行うコード パスと計算と IPv4 の検証もオフロード、ことができます。|  
|Udp チェックサムの計算 |ネットワーク スタックが、計算の負荷を軽減し、上のユーザー データグラム プロトコル \(UDP\) チェックサムの検証コード パスを送受信します。|
|IPv4 のチェックサムの計算 |ネットワーク スタックは、計算と IPv4 のコード パスの送受信を上のチェックサムの検証にオフロードします。 |
|IPv6 のチェックサムの計算 |ネットワーク スタックは、計算と IPv6 のコード パスの送受信を上のチェックサムの検証にオフロードします。 | 
|大量の TCP パケットのセグメント化|TCP/IP のトランスポート層大規模な送信オフロード v2 のサポート (LSOv2)。 LSOv2、TCP/IP のトランスポート層は、ネットワーク アダプターに大量の TCP パケットのセグメント化をオフロードできます。|  
|Receive Side Scaling \(RSS\)|RSS は、ネットワークの効率的な分散を実現するネットワーク ドライバー テクノロジは、マルチプロセッサ システムで複数の cpu 処理を受信します。 RSS の詳細については、このトピックの後に提供されます。|  
|Segment Coalescing \(RSC\) が表示されます。|RSC は、まとめてを処理するヘッダーを最小限に抑えるグループ パケットする機能は、ホストを実行するために必要なです。 受信したペイロードの 64 KB の最大値は、単一の大規模なパケット処理のために結合されたことができます。 RSC の詳細については、このトピックの後に提供されます。|  
  
###  <a name="bkmk_rss"></a>受信側 Scaling

Windows Server 2016、Windows Server 2012、Windows Server 2012 R2、Windows Server 2008 R2、および Windows Server 2008 は、Receive Side Scaling \(RSS\) をサポートします。 

ハードウェア リソースを共有する複数の論理プロセッサを搭載した一部のサーバーが構成されている \ (など、物理 core\) し、ピアが同時マルチスレッド \(SMT\) として扱われます。 Intel ハイパー スレッディング テクノロジは、例を示します。 RSS は、ネットワークの処理コアあたり 1 つの論理プロセッサを指示します。 たとえば、Intel ハイパー スレッディング、4 コア、8 個の論理プロセッサとサーバーで RSS 4 個を超えるの論理プロセッサの使用ネットワーク処理します。  

RSS は、順序が保た同じ論理プロセッサ上と同じ TCP 接続に属しているパケットを処理できるように、論理プロセッサ間での着信ネットワーク I/O パケットを配布します。 

RSS を読み込むも残高 UDP ユニキャスト、マルチキャスト トラフィック、および関連のフローをルーティング \ (これは、ソースと宛先 addresses\ ハッシュによって決定されます) を同じ論理プロセッサの関連到着順序を維持します。 これは、スケーラビリティとパフォーマンスの論理プロセッサの使用可能なよりも少ないネットワーク アダプターを持つサーバーの受信の負荷が高いシナリオを強化するのに役立ちます。 

#### <a name="configuring-rss"></a>RSS の構成

Windows Server 2016 では、Windows PowerShell コマンドレットと RSS プロファイルを使用して RSS を構成できます。 

RSS プロファイルを定義するにを使用して、**– プロファイル**のパラメーター、**Set-netadapterrss** Windows PowerShell コマンドレット。

**RSS 構成用の Windows PowerShell コマンド**

次のコマンドレットを使用するを参照してくださいし、ネットワーク アダプターごとの RSS パラメーターを変更できます。
  
>[!NOTE]
>構文やパラメーターを含め、各コマンドレットの詳細なコマンド リファレンスについては、次のリンクをクリックすることができます。 さらに、コマンドレット名を渡すことができる**Get-help**各コマンドの詳細について Windows PowerShell プロンプトでします。  

- [無効にする NetAdapterRss](https://technet.microsoft.com/library/jj130892)します。 このコマンドは、指定したネットワーク アダプターで RSS を無効にします。

- [有効にする NetAdapterRss](https://technet.microsoft.com/library/jj130859)します。 このコマンドは、指定したネットワーク アダプターで RSS を使用できます。
  
- [Get-netadapterrss](https://technet.microsoft.com/library/jj130912)します。 このコマンドは、指定したネットワーク アダプターの RSS のプロパティを取得します。
  
- [Set-netadapterrss](https://technet.microsoft.com/library/jj130863)します。 このコマンドは、指定したネットワーク アダプターで RSS プロパティを設定します。  

#### <a name="rss-profiles"></a>RSS プロファイル

使用することができます、**– プロファイル**先ネットワーク アダプターに割り当てられた論理プロセッサを指定する Set-NetAdapterRss コマンドレットのパラメーターです。 このパラメーターの使用可能な値は次のとおりです。

- **最も近い**します。 基本の RSS プロセッサをネットワーク アダプターの近くにある論理プロセッサ番号は、優先的に使用します。 このプロファイル、オペレーティング システムが論理プロセッサの負荷に基づいて動的に再調整可能性があります。
  
- **ClosestStatic**します。 ネットワーク アダプターの基本 RSS プロセッサ近くの論理プロセッサ番号は、優先的に使用します。 このプロファイル、オペレーティング システムは論理プロセッサの負荷に基づいて動的を再調整できません。
  
- **NUMA**します。 一般に、論理プロセッサ番号は負荷を分散する別の NUMA ノードで選択されます。 このプロファイル、オペレーティング システムが論理プロセッサの負荷に基づいて動的に再調整可能性があります。
  
- **NUMAStatic**します。 これは、**既定のプロファイル**します。 一般に、論理プロセッサ番号は負荷を分散する別の NUMA ノードで選択されます。 このプロファイル、オペレーティング システムは論理プロセッサの負荷に基づいて動的を再調整できません。

- **保守的な**します。 RSS は負荷に対応できるだけ少ないプロセッサを使用します。 このオプションは、割り込みの数を減らすのに役立ちます。

シナリオとワークロードの特性、に応じて、他のパラメーターを使用することも、**Set-netadapterrss** Windows PowerShell コマンドレットを次を指定します。

- 各ネットワーク アダプターごとに、RSS の論理プロセッサの数を使用できます。
- 論理プロセッサの範囲の開始オフセット。
- ノードは、元のネットワーク アダプターがメモリを割り当てます。

次に、その他**Set-netadapterrss**パラメーター RSS の構成に使用することができます。

>[!NOTE]
>ネットワーク アダプター名の下には、各パラメータの構文の例で**イーサネット**の例の値として使用される、**– 名**のパラメーター、**Set-netadapterrss**コマンド。 コマンドレットを実行するときに使用するネットワーク アダプターの名前が、環境に適していることを確認します。

- **\ * MaxProcessors**: 使用するには、RSS プロセッサの最大数を設定します。 これにより、特定のインターフェイスで、アプリケーションのトラフィックはプロセッサの最大数にバインドされます。 構文の例:

     `Set-NetAdapterRss –Name “Ethernet” –MaxProcessors <value>`

- **\ * BaseProcessorGroup**: NUMA ノードの基本プロセッサ グループを設定します。 これは、RSS で使用されるプロセッサ配列に影響します。 構文の例:

     `Set-NetAdapterRss –Name “Ethernet” –BaseProcessorGroup <value>`
  
- **\ * MaxProcessorGroup**: NUMA ノードの最大プロセッサ グループを設定します。 これは、RSS で使用されるプロセッサ配列に影響します。 この設定を制限する最大プロセッサ グループ k グループ内の配置の負荷分散できるようにします。 構文の例:

     `Set-NetAdapterRss –Name “Ethernet” –MaxProcessorGroup <value>`

- **\ * BaseProcessorNumber**: NUMA ノードの基本プロセッサ数を設定します。 これは、RSS で使用されるプロセッサ配列に影響します。 これにより、ネットワーク アダプター間でのプロセッサをパーティション分割できます。 これは、各アダプターに割り当てられている範囲の RSS プロセッサの 1 番目論理プロセッサです。 構文の例:

     `Set-NetAdapterRss –Name “Ethernet” –BaseProcessorNumber <Byte Value>`

- **\ * NumaNode**: 各ネットワーク アダプターからのメモリを割り当てることができます、NUMA ノードです。 K グループ内にある、または異なる k グループを指定できます。 構文の例:

     `Set-NetAdapterRss –Name “Ethernet” –NumaNodeID <value>`

- **\ * NumberofReceiveQueues**: 論理プロセッサが受信トラフィックの使用率の低いできると思われる \ (たとえば、タスク Manager\ に表示される)、ネットワーク アダプターでサポートされている最大値を既定の 2 から RSS キュー数を増やすことを試すことができます。 ネットワーク アダプター ドライバーの一部として RSS キュー数を変更するオプションがあります。 構文の例:

     `Set-NetAdapterRss –Name “Ethernet” –NumberOfReceiveQueues <value>`

詳細については、リンクをクリックして、次をダウンロードする[拡張性の高いネットワーク: 受信処理のボトルネックを排除する — Introducing RSS](https://download.microsoft.com/download/5/D/6/5D6EAF2B-7DDF-476B-93DC-7CF0072878E6/NDIS_RSS.doc) Word 形式でします。
  
#### <a name="understanding-rss-performance"></a>RSS のパフォーマンスを理解します。

RSS を調整するには、構成と負荷分散のロジックを理解する必要があります。 確認する、RSS の設定が有効にされた出力を確認するを実行すると、**Get-netadapterrss** Windows PowerShell コマンドレット。 このコマンドレットの出力の例を次に示します。
  
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

設定されたパラメーターをエコーでだけでなく、出力の重要な側面は間接指定テーブルの出力です。 間接指定テーブルは、入力方向のトラフィックを分散するために使用するハッシュ テーブルのバケットを表示します。 この例では、n:c 表記法を指定 Numa K-受信トラフィックを転送するために使用するグループ: CPU インデックス ペア。 お正確に 2 つの一意のエントリを参照してください (0:0 と 0:4)、表示されている k グループ 0/cpu0 と k グループ 0/cpu 4 では、それぞれします。

このシステム (k グループ 0) と、n k のグループが 1 つだけ (n < = 128) 間接指定テーブルのエントリ。 受信キューの数が 2, 2 プロセッサに設定されているため (0:0, 0:4) は、選択の最大プロセッサを 8 に設定されていてもします。 実際には、間接指定テーブルには、のみ利用可能な 8 から 2 つの Cpu を使用する入力方向のトラフィックがハッシュ化します。

Cpu を十分に活用するには、RSS の受信キューの数があります最大プロセッサ以上。 前の例では、受信キューを 8 以上に設定してください。

#### <a name="nic-teaming-and-rss"></a>NIC チーミングと RSS

NIC チーミングを使用して別のネットワーク インターフェイス カードでは、チーム化されたネットワーク アダプターで RSS を有効にすることができます。 このシナリオでは、RSS を使用する基礎となる物理ネットワーク アダプターのみを構成できます。 ユーザーは、チーム化されたネットワーク アダプターで RSS コマンドレットを設定することはできません。
  
###  <a name="bkmk_rsc"></a>セグメント Coalescing (RSC) が表示されます。

処理が受信したデータ量が特定の IP ヘッダーの数を削減してセグメント Coalescing \(RSC\) によりパフォーマンスが表示されます。 受信したデータのパフォーマンスをグループ化 \(or coalescing\) によって小さいパケットに拡張より大きい単位のヘルプを使用してください。

このアプローチは、スループットの増加に表示されるほとんどの場合にメリットがあります待機時間の影響を与えることができます。 受信の負荷の高いワークロードのスループットを増やすには、RSC をお勧めします。 RSC をサポートするネットワーク アダプターを展開することを検討してください。 

これらのネットワーク アダプターでは、RSC が上にあることを確認 \ (これは既定 setting\) 特定のワークロードがない限り、\ (たとえば、低待機時間、低スループット networking\) RSC を無効にされている恩恵を表示します。

#### <a name="understanding-rsc-diagnostics"></a>RSC 診断を理解します。

RSC を診断するには、Windows PowerShell コマンドレットを使用して**Get NetAdapterRsc**と**Get NetAdapterStatistics**します。

Get-NetAdapterRsc コマンドレットを実行するときに出力の例を次に示します。

```  

PS C:\Users\Administrator> Get-NetAdapterRsc  
  
Name                       IPv4Enabled  IPv6Enabled  IPv4Operational IPv6Operational               IPv4FailureReason              IPv6Failure  
                                            Reason  
----                           -----------  -----------  --------------- --------------- ----------------- ------------  
Ethernet                       True         False        True            False                  NoFailure       NicProperties  
  
```  

**取得**コマンドレットは、RSC がインターフェイスで有効になっているかどうかと TCP により、RSC を動作状態にするかどうかを示します。 失敗の理由では、そのインターフェイスで、RSC を有効にする、この失敗に関する詳細を説明します。

前のシナリオで IPv4 RSC は、インターフェイスではサポートされていると運用します。 エラーの診断を理解するため、結合されたバイト数または例外の原因となったを参照していずれかのことができます。 これは、結合の問題を示す値を提供します。

Get-NetAdapterStatistics コマンドレットを実行するときに出力の例を次に示します。

```  
PS C:\Users\Administrator> $x = Get-NetAdapterStatistics “myAdapter”   
PS C:\Users\Administrator> $x.rscstatistics  
  
CoalescedBytes       : 0  
CoalescedPackets     : 0  
CoalescingEvents     : 0  
CoalescingExceptions : 0  
  
```  

#### <a name="rsc-and-virtualization"></a>RSC と仮想化

RSC は、ホスト ネットワーク アダプターが Hyper-V 仮想スイッチにバインドされていない場合に、物理ホストでのみサポートされます。 ホストが Hyper-V 仮想スイッチにバインドされているときに、オペレーティング システムによって RSC が無効になります。 さらに、仮想マシンは、仮想ネットワーク アダプターでは、RSC をサポートしていないために RSC の利点を取得しません。

RSC は、単一ルート入出力仮想化 \(SR-IOV\) が有効にすると、バーチャル マシンの有効にすることができます。 ここでは、仮想機能をサポートして RSC 機能です。したがって、バーチャル マシンは、RSC の利点も表示されます。

##  <a name="bkmk_resources"></a>ネットワーク アダプターのリソース

いくつかのネットワーク アダプターは、アクティブに最適なパフォーマンスを実現するために、リソースを管理します。 使用してリソースを手動で構成することはいくつかのネットワーク アダプター、**高度なネットワーク**アダプターのタブ。 このようなアダプターの数、受信バッファーの数などのパラメーターの値を設定し、バッファーを送信できます。

次の Windows PowerShell コマンドレットを使用してネットワーク アダプターのリソースの構成が簡略化します。

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

詳細については、次を参照してください。[Windows PowerShell のネットワーク アダプター コマンドレット](https://technet.microsoft.com/library/jj134956.aspx)します。

このガイドのすべてのトピックへのリンクを参照してください。[ネットワーク サブシステムのパフォーマンス チューニング](net-sub-performance-top.md)します。