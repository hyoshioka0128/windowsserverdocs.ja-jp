---
title: Linux 仮想マシンに関する考慮事項
description: Linux および BSD の仮想マシン
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Asmahi; SandySp; JoPoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: cc6aab7825754579269eb05e591ca2a3cf5a561b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869683"
---
# <a name="linux-virtual-machine-considerations"></a>Linux 仮想マシンに関する考慮事項

Linux と BSD の仮想マシン、HYPER-V で Windows 仮想マシンと比較する追加の考慮事項があります。

最初の考慮事項は、Integration Services が存在するかどうか、または啓蒙なしで、エミュレートされたハードウェアで単に、VM が実行されているかどうかは。 Integration services の組み込みまたはダウンロード可能な Linux および BSD のリリースのテーブルが表示されます。 [Windows 上の Hyper-v ではサポートされている Linux および FreeBSD の仮想マシン](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows)します。 これらのページの該当する Linux のディストリビューション リリース、およびそれらの機能に関する注意事項を使用できる HYPER-V 機能が利用可能なグリッドがあります。

ゲストで Integration Services が実行されている場合でも、最適なパフォーマンスは見られないレガシ ハードウェアを構成できます。 たとえば、構成し、レガシ ネットワーク アダプターを使用する代わりに、ゲストの仮想イーサネット アダプターを使用します。 Windows Server 2016 では、ネットワーク、SR-IOV はも利用できるように高度な。

## <a name="linux-network-performance"></a>Linux のネットワークのパフォーマンス

既定では Linux では、ハードウェア アクセラレータを有効および、既定の負荷を軽減します。 ホスト上の NIC のプロパティで vRSS を有効にして、Linux ゲストおり、vRSS を使用する場合は、機能を有効になります。 Powershell でこの同じパラメーターを変更できます、`EnableNetAdapterRSS`コマンド。

同様に、ゲストによって使用される物理 NIC で VMMQ (仮想スイッチの RSS) 機能を有効にする**プロパティ** > **構成しています.**  > **詳細**タブ > 設定**仮想スイッチの RSS**に**有効**または、次を使用して、Powershell で VMMQ を有効にします。

```PowerShell
 Set-VMNetworkAdapter -VMName **$VMName** -VmmqEnabled $True
 ```

ゲストで追加の TCP チューニング実行できる制限を増やすことで。 最適なパフォーマンスを複数の Cpu 負荷を分散させることと、ワークロードの詳細が生成されます最高のスループットでは、仮想化されたワークロードに「ベア メタル」よりも待機時間が長くなるものです。

ネットワークのベンチマークで有効ないくつか例チューニング パラメーターは次のとおりです。

```PowerShell
net.core.netdev_max_backlog = 30000
net.core.rmem_max = 67108864
net.core.wmem_max = 67108864
net.ipv4.tcp_wmem = 4096 12582912 33554432
net.ipv4.tcp_rmem = 4096 12582912 33554432
net.ipv4.tcp_max_syn_backlog = 80960
net.ipv4.tcp_slow_start_after_idle = 0
net.ipv4.tcp_tw_reuse = 1
net.ipv4.ip_local_port_range = 10240 65535
net.ipv4.tcp_abort_on_overflow = 1
```

ネットワーク microbenchmarks に役立つツールは Linux と Windows の両方で使用可能なある ntttcp、です。 Linux バージョンはオープン ソースから使用可能な[github.com ntttcp は linux 用](https://github.com/Microsoft/ntttcp-for-linux)します。 Windows のバージョンが記載されて、[ダウンロード センター](https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769)します。 ワークロードのチューニング時に、必要な数だけストリームを使用して、最適なスループットを取得することをお勧めします。 モデルのトラフィックに ntttcp を使用して、`-P`パラメーターは、使用の並列接続の数を設定します。

## <a name="linux-storage-performance"></a>Linux の記憶域のパフォーマンス

一覧表示されます、次のようないくつかのベスト プラクティス、 [HYPER-V 上の Linux で実行するためのベスト プラクティス](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/best-practices-for-running-linux-on-hyper-v)します。 Linux カーネルでは、さまざまなアルゴリズムの要求の順序を変更するさまざまな I/O スケジューラが。 NOOP は、スケジュールの決定、ハイパーバイザーによってを通過する先入れ先出しキューです。 Linux 仮想マシンを HYPER-V で実行されている場合、スケジューラとして NOOP を使用することをお勧めします。 ブート ローダーの構成では、特定のデバイスのスケジューラを変更する (/例については、etc/grub.conf)、追加`elevator=noop`カーネル パラメーター、および再起動します。

ネットワークと同様に、記憶域での Linux ゲストのパフォーマンスには、ホストをビジー状態に維持するための十分な深さの複数のキューからのほとんどがメリットがあります。 Microbenchmarking 記憶域のパフォーマンスは libaio エンジンと fio ベンチマーク ツールを使用しておそらく最適です。

## <a name="see-also"></a>関連項目

-   [HYPER-V 用語](terminology.md)

-   [HYPER-V のアーキテクチャ](architecture.md)

-   [HYPER-V サーバーの構成](configuration.md)

-   [HYPER-V のプロセッサのパフォーマンス](processor-performance.md)

-   [HYPER-V でメモリのパフォーマンス](memory-performance.md)

-   [HYPER-V ストレージの I/O パフォーマンス](storage-io-performance.md)

-   [HYPER-V ネットワークの I/O パフォーマンス](network-io-performance.md)

-   [仮想化環境のボトルネックの検出](detecting-virtualized-environment-bottlenecks.md)
