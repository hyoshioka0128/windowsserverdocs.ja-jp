---
title: HNV ゲートウェイでのパフォーマンス チューニング ソフトウェア定義ネットワーク
description: HNV ゲートウェイのパフォーマンス チューニング ガイドライン ソフトウェア定義ネットワーク
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: grcusanz; AnPaul
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 217428b84a00b2e2231a15cb3878d0abcec1d9ad
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827323"
---
# <a name="hnv-gateway-performance-tuning-in-software-defined-networks"></a>HNV ゲートウェイでのパフォーマンス チューニング ソフトウェア定義ネットワーク

このトピックでは、ハードウェアの仕様とは、HYPER-V を実行して、Windows Server ゲートウェイ仮想マシン (Vm) の構成パラメーターに加え、Windows Server ゲートウェイ仮想マシンをホストするサーバーの構成に関する推奨事項を提供します. Windows Server ゲートウェイ Vm に最適なパフォーマンスを抽出するため、これらのガイドラインに従うことが期待されます。
次のセクションでは、Windows Server ゲートウェイを展開するときのハードウェアと構成の要件を示します。
1. Hyper-V ハードウェアの推奨事項
2. Hyper-V ホストの構成
3. Windows Server ゲートウェイ VM の構成

## <a name="hyper-v-hardware-recommendations"></a>Hyper-V ハードウェアの推奨事項

Windows Server 2016 と HYPER-V を実行している各サーバーの推奨される最小ハードウェア構成を次に示します。

| サーバー コンポーネント               | 仕様                                                                                                                                                                                                                                                                   |
|--------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 中央処理装置 (CPU)  | Non-uniform Memory アーキテクチャ (NUMA) ノード:2 <br> 最適なパフォーマンスをホスト上の複数の Windows Server ゲートウェイ Vm がある場合、各ゲートウェイ VM は、1 つの NUMA ノードへのフル アクセスが必要です。 ホストの物理アダプターによって使用される NUMA ノードと異なる場合があります。 |
| NUMA ノードごとのコア            | 2                                                                                                                                                                                                                                                                               |
| ハイパー スレッディング                | 無効になります。 ハイパー スレッディングによって、Windows Server ゲートウェイのパフォーマンスは向上しません。                                                                                                                                                                                           |
| ランダム アクセス メモリ (RAM)     | 48 GB                                                                                                                                                                                                                                                                           |
| ネットワーク インターフェイス カード (NIC) | 2 つの 10 GB Nic 回線速度でゲートウェイのパフォーマンスによって異なります。 回線速度が 10 gbps 未満の場合は、同じ係数を使用してゲートウェイのトンネルのスループット数も下がります。                                                                                          |

Windows Server ゲートウェイ VM に割り当てられた仮想プロセッサの数が、NUMA ノードのプロセッサ数を超えていないことを確認します。 たとえば、NUMA ノードには 8 個のコアがある場合は、仮想プロセッサの数は 8 個以下にする必要があります。 最適なパフォーマンスを 8 が必要です。 NUMA ノードの数と NUMA ノードごとのコア数を検索するには、各 Hyper-V ホストで次の Windows PowerShell スクリプトを実行します。

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

8 個の仮想プロセッサと少なくとも 8 GB の RAM を 1 つのゲートウェイ VM には、ゲートウェイ Vm の数を選択するときに NUMA ノードごとに 8 個のコアがある場合は、各 HYPER-V ホストにインストールするお勧めします。 この場合は、1 つの NUMA ノードは、ホスト マシンには専用です。

## <a name="hyper-v-host-configuration"></a>HYPER-V ホストの構成

Windows Server 2016 と Hyper-v ホストと持つを実行している各サーバーの推奨構成を次にワークロードは、Windows Server ゲートウェイ Vm を実行します。 これらの構成の手順には、Windows PowerShell コマンドの例が使用されています。 これらの例にはプレースホルダーが含まれており、使用する環境でコマンドを実行するときに実際の値を指定する必要があります。 たとえば、ネットワーク アダプター名のプレース ホルダーには"NIC1 でしょうか。 "NIC2。 でしょうか。 これらのプレースホルダーを使うコマンドを実行するときに、プレースホルダーを使用するのではなく、使用するサーバー上のネットワーク アダプターの実際の名前を使用します。そのようにしないと、コマンドは失敗します。

>[!Note]
> 以下の Windows PowerShelll コマンドを実行するには、Administrators グループのメンバーであることが必要です。

| 構成項目                          | Windows Powershell 構成                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|---------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| スイッチ埋め込みチーミング                     | 複数のネットワーク アダプター、vswitch を作成するときに自動的に、スイッチ埋め込みのこれらのアダプターのチーミングを有効します。 <br> ```New-VMSwitch -Name TeamedvSwitch -NetAdapterName "NIC 1","NIC 2"``` <br> Windows Server 2016 の SDN では、LBFO を従来のチーミングはサポートされていません。 スイッチ埋め込みチーミング仮想トラフィックと RDMA のトラフィックの Nic の同じセットを使用することができます。 これは、LBFO に基づいての NIC チーミングでサポートされていません。                                                        |
| 物理 NIC での割り込み節度       | 既定の設定を使用します。 構成を確認するには、次の Windows PowerShell コマンドを使用できます。 ```Get-NetAdapterAdvancedProperty```                                                                                                                                                                                                                                                                                                                                                                    |
| 物理 NIC での受信バッファー サイズ       | 物理 Nic は、コマンドを実行してこのパラメーターの構成をサポートしているかどうかを確認する```Get-NetAdapterAdvancedProperty```します。 このパラメーターをサポートしていない場合、コマンドの出力は、プロパティは含まれません"Receive Buffers。 でしょうか。 NIC がこのパラメーターをサポートしている場合、次の Windows PowerShell コマンドを使用して受信バッファー サイズを設定できます。 <br>```Set-NetAdapterAdvancedProperty “NIC1�? –DisplayName “Receive Buffers�? –DisplayValue 3000``` <br>                          |
| 物理 NIC での送信バッファー サイズ          | 物理 Nic は、コマンドを実行してこのパラメーターの構成をサポートしているかどうかを確認する```Get-NetAdapterAdvancedProperty```します。 コマンドの出力がプロパティを含まない場合は、Nic は、このパラメーターをサポートしていない、"バッファーを送信します。 でしょうか。 NIC がこのパラメーターをサポートしている場合、次の Windows PowerShell コマンドを使用して送信バッファー サイズを設定できます。 <br> ```Set-NetAdapterAdvancedProperty “NIC1�? –DisplayName “Transmit Buffers�? –DisplayValue 3000``` <br>                           |
| 物理 NIC での Receive Side Scaling (RSS) | 物理的な Nic に RSS Get-netadapterrss Windows PowerShell コマンドを実行して有効になっているがあるかどうかを確認できます。 有効にして、ネットワーク アダプターで RSS を構成するのには、次の Windows PowerShell コマンドを使用できます。 <br> ```Enable-NetAdapterRss “NIC1�?,�?NIC2�?```<br> ```Set-NetAdapterRss “NIC1�?,�?NIC2�? –NumberOfReceiveQueues 16 -MaxProcessors``` <br> 注: VMMQ または VMQ が有効になっている場合、RSS が物理ネットワーク アダプターで有効にするのにはありません。 ホストの仮想ネットワーク アダプターで有効にすることができます。 |
| VMMQ                                        | VMMQ vm を有効にするには、次のコマンドを実行します。 <br> ```Set-VmNetworkAdapter -VMName <gateway vm name>,-VrssEnabled $true -VmmqEnabled $true``` <br> 注: すべてのネットワーク アダプターでは、VMMQ をサポートします。 現時点では、Chelsio T5 と T6、Mellanox CX 3 と CX 4、および QLogic 45xxx シリーズではサポートされて                                                                                                                                                                                                                                      |
| NIC チームでの仮想マシン キュー (VMQ) | 次の Windows PowerShell コマンドを使用して、セット チームで VMQ を有効にできます。 <br>```Enable-NetAdapterVmq``` <br> 注: これは、ハードウェアが VMMQ をサポートしていない場合にのみ有効にします。 、サポートされている場合は、パフォーマンス向上のため VMMQ を有効にする必要があります。                                                                                                                                                                                                                                                               |
>[!Note]
> VMQ と vRSS は、画像には、VM の負荷が高いと、CPU が最大値に使用されている場合にのみです。 のみが少なくとも 1 つのプロセッサ コア max アウトです。VMQ および vRSS を複数のコアに処理負荷を分散する有益なります。 これは該当しません IPsec トラフィックの IPsec トラフィックは、1 つのコアに限定します。

## <a name="windows-server-gateway-vm-configuration"></a>Windows Server ゲートウェイ VM の構成

両方の HYPER-V ホストでは、Windows Server ゲートウェイによってゲートウェイとして構成されている複数の Vm を構成できます。 仮想スイッチ マネージャーを使用して、Hyper-V ホストの NIC チームにバインドされている Hyper-V 仮想スイッチを作成できます。 最適なパフォーマンスを HYPER-V ホスト上の 1 つのゲートウェイ VM をデプロイする必要がありますに注意してください。
各 Windows Server ゲートウェイ VM の推奨構成を次に示します。

| 構成項目                 | Windows Powershell 構成                                                                                                                                                                                                                                                                                                                                                               |
|------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| メモリ                             | 8 GB                                                                                                                                                                                                                                                                                                                                                                                           |
| 仮想ネットワーク アダプターの数 | 次の特定の 3 個の Nic を使用します。管理オペレーティング システムの 1 つは内部ネットワークのみへのアクセスを提供する、外部ネットワークへのアクセスを提供する 1 つの外部で使用される管理用の 1。                                                                                                                                                            |
| Receive Side Scaling (RSS)         | 既定の管理 nic RSS の設定を保持できます。 次の例の構成は 8 個の仮想プロセッサがある VM 用です。 外部と内部 Nic には値が 0、MaxRssProcessors を 8 以下の Windows PowerShell コマンドを使用して RSS を有効にできます。 <br> ```Set-NetAdapterRss “Internal�?,�?External�? –BaseProcNumber 0 –MaxProcessorNumber 8``` <br> |
| 送信側バッファー                   | 既定の管理 NIC の送信側バッファー設定を保持できます。 内部と外部 Nic の両方に次の Windows PowerShell コマンドを使用して、32 MB の RAM と送信側バッファーを構成できます。 <br> ```Set-NetAdapterAdvancedProperty “Internal�?,�?External�? –DisplayName “Send Buffer Size�? –DisplayValue “32MB�?``` <br>                                                       |
| 受信側バッファー                | 既定の管理 NIC の受信側バッファー設定を保持できます。 内部と外部 Nic の両方で、次の Windows PowerShell コマンドを使用して、16 MB の RAM と受信側バッファーを構成できます。 <br> ```Set-NetAdapterAdvancedProperty “Internal�?,�?External�? –DisplayName “Receive Buffer Size�? –DisplayValue “16MB�?``` <br>                                            |
| 前方最適化               | 既定の管理 NIC の前方最適化設定を保持できます。 内部と外部 Nic の両方では、次の Windows PowerShell コマンドを使用して前方最適化を有効にできます。 <br> ```Set-NetAdapterAdvancedProperty “Internal�?,�?External�? –DisplayName “Forward Optimization�? –DisplayValue “1�?``` <br>                                                                      |
