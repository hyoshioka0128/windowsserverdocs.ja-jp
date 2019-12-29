---
title: ソフトウェア定義ネットワークでの HNV ゲートウェイのパフォーマンスチューニング
description: ソフトウェア定義ネットワークに関する HNV ゲートウェイのパフォーマンスチューニングガイドライン
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: grcusanz; AnPaul
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 907b160b143af18a8ede3a9a7975fa8b22753118
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383496"
---
# <a name="hnv-gateway-performance-tuning-in-software-defined-networks"></a>ソフトウェア定義ネットワークでの HNV ゲートウェイのパフォーマンスチューニング

このトピックでは、Windows Server ゲートウェイの仮想マシン (Vm) の構成パラメーターに加えて、Hyper-v を実行し、Windows Server ゲートウェイの仮想マシンをホストするサーバーのハードウェア仕様と構成に関する推奨事項について説明します. Windows Server ゲートウェイ Vm から最適なパフォーマンスを得るために、これらのガイドラインに従うことが想定されています。
次のセクションでは、Windows Server ゲートウェイを展開するときのハードウェアと構成の要件を示します。
1. Hyper-V ハードウェアの推奨事項
2. Hyper-V ホストの構成
3. Windows Server ゲートウェイの VM 構成

## <a name="hyper-v-hardware-recommendations"></a>Hyper-V ハードウェアの推奨事項

次に、Windows Server 2016 および Hyper-v を実行している各サーバーに推奨される最小ハードウェア構成を示します。

| サーバー コンポーネント               | 仕様                                                                                                                                                                                                                                                                   |
|--------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 中央処理装置 (CPU)  | Non-uniform Memory Architecture (NUMA) ノード:2 <br> ホスト上に複数の Windows Server ゲートウェイ Vm がある場合、最適なパフォーマンスを得るには、各ゲートウェイ VM に1つの NUMA ノードへのフルアクセス権を付与する必要があります。 ホストの物理アダプターによって使用される NUMA ノードとは別のものにする必要があります。 |
| NUMA ノードごとのコア            | 2                                                                                                                                                                                                                                                                               |
| ハイパースレッディング                | 無効になります。 ハイパー スレッディングによって、Windows Server ゲートウェイのパフォーマンスは向上しません。                                                                                                                                                                                           |
| ランダム アクセス メモリ (RAM)     | 48 GB                                                                                                                                                                                                                                                                           |
| ネットワーク インターフェイス カード (NIC) | 2 10 GB Nic の場合、ゲートウェイのパフォーマンスは回線速度によって異なります。 回線レートが10Gbps 未満の場合は、ゲートウェイトンネルスループットの数値も同じ要因によって停止されます。                                                                                          |

Windows Server ゲートウェイ VM に割り当てられた仮想プロセッサの数が、NUMA ノードのプロセッサ数を超えていないことを確認します。 たとえば、NUMA ノードには 8 個のコアがある場合は、仮想プロセッサの数は 8 個以下にする必要があります。 最適なパフォーマンスを得るには、8にする必要があります。 NUMA ノードの数と NUMA ノードごとのコア数を検索するには、各 Hyper-V ホストで次の Windows PowerShell スクリプトを実行します。

```PowerShell
$nodes = [object[]] $(gwmi –Namespace root\virtualization\v2 -Class MSVM_NumaNode)
$cores = ($nodes | Measure-Object NumberOfProcessorCores -sum).Sum
$lps = ($nodes | Measure-Object NumberOfLogicalProcessors -sum).Sum


Write-Host "Number of NUMA Nodes: ", $nodes.count
Write-Host ("Total Number of Cores: ", $cores)
Write-Host ("Total Number of Logical Processors: ", $lps)
```

>[!Important]
> NUMA ノード間で仮想プロセッサを割り当てると、Windows Server ゲートウェイのパフォーマンスに悪影響を及ぼす場合があります。 複数の VM を実行し、そのそれぞれに 1 つの NUMA ノードから仮想プロセッサを割り当てると、1 つの VM にすべての仮想プロセッサを割り当てた場合に比べて全体的なパフォーマンスは向上します。

各 NUMA ノードに8個のコアがある場合に、各 Hyper-v ホストにインストールするゲートウェイ vm の数を選択する場合は、8個の仮想プロセッサと少なくとも 8 GB の RAM を搭載したゲートウェイ VM を1つ使用することをお勧めします。 この場合、1つの NUMA ノードがホストコンピューター専用になります。

## <a name="hyper-v-host-configuration"></a>Hyper-v ホストの構成

Windows Server 2016 と Hyper-v を実行し、ワークロードが Windows Server ゲートウェイ Vm を実行する各サーバーでは、次の構成をお勧めします。 これらの構成の手順には、Windows PowerShell コマンドの例が使用されています。 これらの例にはプレースホルダーが含まれており、使用する環境でコマンドを実行するときに実際の値を指定する必要があります。 たとえば、ネットワークアダプター名のプレースホルダーは、"NIC1" と "NIC2" です。 これらのプレースホルダーを使うコマンドを実行するときに、プレースホルダーを使用するのではなく、使用するサーバー上のネットワーク アダプターの実際の名前を使用します。そのようにしないと、コマンドは失敗します。

>[!Note]
> 以下の Windows PowerShelll コマンドを実行するには、Administrators グループのメンバーであることが必要です。

| 構成項目                          | Windows Powershell の構成                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|---------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| スイッチ埋め込みチーミング                     | 複数のネットワークアダプターを含む vswitch を作成すると、それらのアダプターのスイッチ埋め込みチーミングが自動的に有効になります。 <br> ```New-VMSwitch -Name TeamedvSwitch -NetAdapterName "NIC 1","NIC 2"``` <br> LBFO による従来のチーム化は、Windows Server 2016 の SDN ではサポートされていません。 スイッチ埋め込みチーミングを使用すると、仮想トラフィックと RDMA トラフィックに同じセットの Nic を使用できます。 これは、LBFO に基づく NIC チーミングではサポートされませんでした。                                                        |
| 物理 NIC での割り込み節度       | 既定の設定を使用します。 構成を確認するには、次の Windows PowerShell コマンドを使用します。 ```Get-NetAdapterAdvancedProperty```                                                                                                                                                                                                                                                                                                                                                                    |
| 物理 NIC での受信バッファー サイズ       | 物理 Nic がこのパラメーターの構成をサポートしているかどうかを確認するには、コマンド ```Get-NetAdapterAdvancedProperty``` を実行します。 このパラメーターがサポートされていない場合、コマンドからの出力には "受信バッファー" プロパティは含まれません。 NIC がこのパラメーターをサポートしている場合、次の Windows PowerShell コマンドを使用して受信バッファー サイズを設定できます。 <br>```Set-NetAdapterAdvancedProperty "NIC1" –DisplayName "Receive Buffers" –DisplayValue 3000``` <br>                          |
| 物理 NIC での送信バッファー サイズ          | 物理 Nic がこのパラメーターの構成をサポートしているかどうかを確認するには、コマンド ```Get-NetAdapterAdvancedProperty``` を実行します。 Nic がこのパラメーターをサポートしていない場合、コマンドの出力には "送信バッファー" プロパティは含まれません。 NIC がこのパラメーターをサポートしている場合、次の Windows PowerShell コマンドを使用して送信バッファー サイズを設定できます。 <br> ```Set-NetAdapterAdvancedProperty "NIC1" –DisplayName "Transmit Buffers" –DisplayValue 3000``` <br>                           |
| 物理 NIC での Receive Side Scaling (RSS) | Windows PowerShell コマンド Set-netadapterrss を実行して、物理 Nic の RSS が有効になっているかどうかを確認できます。 次の Windows PowerShell コマンドを使用して、ネットワークアダプターで RSS を有効にし、構成することができます。 <br> ```Enable-NetAdapterRss "NIC1","NIC2"```<br> ```Set-NetAdapterRss "NIC1","NIC2" –NumberOfReceiveQueues 16 -MaxProcessors``` <br> 注: VMMQ または VMQ が有効になっている場合、物理ネットワークアダプターで RSS を有効にする必要はありません。 ホスト仮想ネットワークアダプターで有効にすることができます。 |
| VMMQ                                        | VM の VMMQ を有効にするには、次のコマンドを実行します。 <br> ```Set-VmNetworkAdapter -VMName <gateway vm name>,-VrssEnabled $true -VmmqEnabled $true``` <br> 注: すべてのネットワークアダプターが VMMQ をサポートしているわけではありません。 現時点では、Chelsio T5 と T6、Mellanox CX-3 と CX-4、および QLogic 45xxx シリーズでサポートされています。                                                                                                                                                                                                                                      |
| NIC チームでの仮想マシン キュー (VMQ) | 次の Windows PowerShell コマンドを使用して、セットチームで VMQ を有効にすることができます。 <br>```Enable-NetAdapterVmq``` <br> 注: これは、HW が VMMQ をサポートしていない場合にのみ有効にする必要があります。 サポートされている場合は、パフォーマンスを向上させるために VMMQ を有効にする必要があります。                                                                                                                                                                                                                                                               |
>[!Note]
> VMQ と vRSS は、VM の負荷が高く、CPU が最大限に利用されている場合にのみ画像になります。 その後、少なくとも1つのプロセッサコアの最大値が表示されます。VMQ と vRSS は、処理負荷を複数のコアに分散させるのに役立ちます。 これは、ipsec トラフィックが1つのコアに限定されるため、IPsec トラフィックには適用されません。

## <a name="windows-server-gateway-vm-configuration"></a>Windows Server ゲートウェイ VM の構成

両方の Hyper-v ホストで、Windows Server ゲートウェイを使用してゲートウェイとして構成されている複数の Vm を構成できます。 仮想スイッチ マネージャーを使用して、Hyper-V ホストの NIC チームにバインドされている Hyper-V 仮想スイッチを作成できます。 最適なパフォーマンスを得るには、1つのゲートウェイ VM を Hyper-v ホストに展開する必要があります。
各 Windows Server ゲートウェイ VM の推奨構成を次に示します。

| 構成項目                 | Windows Powershell の構成                                                                                                                                                                                                                                                                                                                                                               |
|------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Memory                             | 8 GB                                                                                                                                                                                                                                                                                                                                                                                           |
| 仮想ネットワーク アダプターの数 | 次の特定の用途を持つ3枚の Nic:管理オペレーティングシステムによって使用される管理の場合は1、外部ネットワークへのアクセスを提供する1外部ネットワーク (内部ネットワークのみにアクセスを提供する場合は 1)。                                                                                                                                                            |
| Receive Side Scaling (RSS)         | 管理 NIC の既定の RSS 設定をそのまま使用できます。 次の例の構成は 8 個の仮想プロセッサがある VM 用です。 外部および内部の Nic の場合、次の Windows PowerShell コマンドを使用して、Baseset を0に設定し、MaxRssProcessors を8に設定して RSS を有効にすることができます。 <br> ```Set-NetAdapterRss "Internal","External" –BaseProcNumber 0 –MaxProcessorNumber 8``` <br> |
| 送信側バッファー                   | 管理 NIC の既定の送信側バッファー設定を保持することができます。 内部 Nic と外部 Nic の両方について、次の Windows PowerShell コマンドを使用して、32 MB の RAM で送信側バッファーを構成できます。 <br> ```Set-NetAdapterAdvancedProperty "Internal","External" –DisplayName "Send Buffer Size" –DisplayValue "32MB"``` <br>                                                       |
| 受信側バッファー                | 管理 NIC の既定の受信側バッファー設定を保持することができます。 内部 Nic と外部 Nic の両方について、次の Windows PowerShell コマンドを使用して、16 MB の RAM で受信側バッファーを構成できます。 <br> ```Set-NetAdapterAdvancedProperty "Internal","External" –DisplayName "Receive Buffer Size" –DisplayValue "16MB"``` <br>                                            |
| 前方最適化               | 管理 NIC の既定の転送最適化設定をそのまま使用できます。 内部 Nic と外部 Nic の両方について、次の Windows PowerShell コマンドを使用して、転送の最適化を有効にすることができます。 <br> ```Set-NetAdapterAdvancedProperty "Internal","External" –DisplayName "Forward Optimization" –DisplayValue "1"``` <br>                                                                      |
