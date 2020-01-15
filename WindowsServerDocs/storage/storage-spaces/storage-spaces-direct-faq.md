---
title: 記憶域スペースダイレクトに関してよく寄せられる質問
description: 記憶域スペースダイレクトの詳細
keywords: 記憶域
ms.prod: windows-server
ms.author: kaushik
ms.technology: storage-spaces
ms.topic: article
author: kaushika-msft
ms.date: 10/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: 19dcc1c57fe7c7eea74b003553a0b0a6ab5508aa
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2020
ms.locfileid: "75950237"
---
# <a name="storage-spaces-direct---frequently-asked-questions-faq"></a>記憶域スペースダイレクトに関してよく寄せられる質問 (FAQ)

この記事では、[記憶域スペースダイレクト](storage-spaces-direct-overview.md)に関してよく寄せられる質問とその回答を示します。

## <a name="when-you-use-storage-spaces-direct-with-3-nodes-can-you-get-both-performance-and-capacity-tiers"></a>3つのノードで記憶域スペースダイレクトを使用する場合、パフォーマンスレベルと容量レベルの両方を取得できますか。

はい。2ノードまたは3ノードの記憶域スペースダイレクト構成では、パフォーマンスと容量の両方の層を取得できます。 ただし、2つの容量デバイスがあることを確認する必要があります。 つまり、NVME、SSD、HDD の3種類のデバイスをすべて使用する必要があります。
 
## <a name="refs-file-system-provides-real-time-tiaring-with-storage-spaces-direct-does-refs-provides-the-same-functionality-with-shared-storage-spaces-in-2016"></a>Refs ファイルシステムでは、記憶域スペースダイレクトを使用したリアルタイムの tiaring が提供されます。 REFS では、2016の共有記憶域スペースと同じ機能が提供されますか。

いいえ。2016では、共有記憶域スペースを使用したリアルタイムの階層化は得られません。 これは記憶域スペースダイレクトのみです。 
 
## <a name="can-i-use-an-ntfs-file-system-with-storage-spaces-direct"></a>記憶域スペースダイレクトで NTFS ファイルシステムを使用できますか。
  
はい。記憶域スペースダイレクトで NTFS ファイルシステムを使用できます。 ただし、REFS をお勧めします。 NTFS では、リアルタイムの階層化は提供されません。 
 
## <a name="i-have-configured-2-node-storage-spaces-direct-clusters-where-the-virtual-disk-is-configured-as-2-way-mirror-resiliency-if-i-add-a-new-fault-domain-will-the-resiliency-of-the-existing-virtual-disk-change"></a>2つのノード記憶域スペースダイレクトクラスターを構成しました。ここでは、仮想ディスクが2方向ミラーの回復性として構成されています。 新しい障害ドメインを追加した場合、既存の仮想ディスクの回復性は変更されますか。

新しい障害ドメインを追加すると、作成した新しい仮想ディスクは3方向ミラーに移動します。 ただし、既存の仮想ディスクは2方向ミラーディスクのままです。 既存のボリュームから新しい仮想ディスクにデータをコピーすることで、新しい回復性の利点を得ることができます。
 
## <a name="the-storage-spaces-direct-was-created-using-the-autoconfig0-switch-and-the-pool-created-manually-when-i-try-to-query-the-storage-spaces-direct-pool-to-create-a-new-volume-i-get-a-message-that-says-enable-clusters2d-again-what-should-i-do"></a>記憶域スペースダイレクトが autoconfig を使用して作成されました: 0スイッチとプールを手動で作成します。 記憶域スペースダイレクトプールに対してクエリを実行して新しいボリュームを作成しようとすると、"Enable-clusters2d を再度有効にする" というメッセージが表示されます。どうしたらいいでしょう。

既定では、S2D コマンドレットを使用して記憶域スペースダイレクトを構成すると、コマンドレットによってすべてのことが行われます。 プールと層が作成されます。 Autoconfig: 0 を使用する場合は、すべてを手動で実行する必要があります。 プールのみを作成した場合、階層は必ずしも作成されません。 接続されているデバイスに対応する方法で階層をまったく作成していないか、作成されていない階層を作成した場合は、"Enable-clusters2d を再度有効にする" というエラーメッセージが表示されます。 運用環境では、autoconfig スイッチを使用しないことをお勧めします。 
 
## <a name="is-it-possible-to-add-a-spinning-disk-hdd-to-the-storage-spaces-direct-pool-after-you-have-created-storage-spaces-direct-with-ssd-devices"></a>SSD デバイスで記憶域スペースダイレクトを作成した後、スピンディスク (HDD) を記憶域スペースダイレクトプールに追加することはできますか。

いいえ。 既定では、単一のデバイスの種類を使用してプールを作成すると、キャッシュディスクが構成されず、すべてのディスクが容量に使用されます。 構成に NVME ディスクを追加することができ、NVME ディスクはキャッシュ用に構成されます。
 
## <a name="i-have-configured-a-2-rack-fault-domain-rack-1-has-2-fault-domains-rack-2-has-1-fault-domain-each-server-has-4-capacity-100-gb-devices-can-i-use-all-1200-gb-of-space-from-the-pool"></a>2ラック障害ドメインを構成しました: ラック1に2つの障害ドメインがあります。ラック2に1つの障害ドメインがあります。 各サーバーには、4つの容量 100 GB のデバイスがあります。 プールから 1200 GB の領域をすべて使用できますか。

いいえ、使用できるのは 800 GB のみです。 ラック障害ドメインでは、各 chuck とその複製が異なるラックに配置されるように、双方向ミラー構成を使用していることを確認する必要があります。
 
## <a name="what-should-the-cache-size-be-when-i-am-configuring-storage-spaces-direct"></a>記憶域スペースダイレクトを構成するときにキャッシュサイズはどのようになりますか。

キャッシュは、アプリケーションとワークロードのワーキングセット (任意の時点でアクティブに読み取りまたは書き込みが行われているデータ) に合わせてサイズを変更する必要があります。

## <a name="how-can-i-determine-the-size-of-cache-that-is-being-used-by-storage-spaces-direct"></a>記憶域スペースダイレクトによって使用されているキャッシュのサイズを確認する方法はありますか

組み込みのユーティリティ PerfMon を使用して、キャッシュミスを検査します。 Cluster Storage ハイブリッドディスクカウンターからキャッシュミス読み取り数/秒を確認します。 キャッシュが不足している読み取りの数が多すぎる場合は、キャッシュが小さすぎて拡張する必要があることに注意してください。 
 
## <a name="is-there-a-calculator-that-shows-the-exact-size-of-the-disks-that-are-being-set-aside-for-cache-capacity-and-resiliency-that-would-enable-me-to-plan-better"></a>キャッシュ、容量、回復性のために確保されているディスクの正確なサイズを示す電卓があるかどうかを確認できます。

記憶域スペース計算ツールを使用すると、計画に役立てることができます。 これは https://aka.ms/s2dcalc で入手できます。
 
## <a name="what-is-the-best-configuration-that-you-would-recommend-when-configuring-6-servers-and-3-racks"></a>6台のサーバーと3つのラックを構成するときに推奨される最適な構成は何ですか。

各ラックに2台のサーバーを使用して、3方向ミラーの仮想ディスクの回復性を確保します。 ラックに配置されている方法で OS に構成を提供している場合にのみ、ラック構成が正しく機能することに注意してください。 
 
## <a name="can-i-enable-maintenance-mode-for-a-specific-disk-on-a-specific-server-in-storage-spaces-direct-cluster"></a>記憶域スペースダイレクトクラスター内の特定のサーバーにある特定のディスクのメンテナンスモードを有効にすることはできますか。

はい、特定のディスクと特定の障害ドメインでストレージメンテナンスモードを有効にすることができます。 ノードを一時停止すると、自動的に有効になります。 次のコマンドを実行して、特定のディスクに対してこれを有効にすることができます。

```powershell
Get-PhysicalDisk -SerialNumber <SerialNumber> | Enable-StorageMaintenanceMode
```

## <a name="is-storage-spaces-direct-supported-on-my-hardware"></a>ハードウェアでは記憶域スペースダイレクトサポートされていますか。

ハードウェアの製造元に問い合わせて、サポートを確認することをお勧めします。 ハードウェアベンダーは、ハードウェア上でソリューションをテストし、サポートされているかどうかについてコメントします。 たとえば、このドキュメントの執筆時点では、R730/R730xd/R630 など、8個を超えるドライブスロットを持つサーバーは、SES をサポートし、記憶域スペースダイレクトと互換性があります。 Dell は、記憶域スペースダイレクトの HBA330 のみをサポートしています。 R620 は、SES をサポートしておらず、記憶域スペースダイレクトと互換性がありません。

ハードウェアのサポート情報の詳細については、次の web サイトを参照してください: Windows Server Catalog
 
## <a name="how-does-storage-spaces-direct-make-use-of-ses"></a>記憶域スペースダイレクトはどのようにして SES を利用しますか。

記憶域スペースダイレクトは、SCSI エンクロージャサービス (SES) マッピングを使用して、データのスラブとメタデータが耐障害ドメインに分散されるようにします。 ハードウェアで SES がサポートされていない場合は、エンクロージャのマッピングは存在せず、データの配置は回復力がありません。
 
## <a name="what-command-can-you-use-to-check-the-physical-extent-for-a-virtual-disk"></a>仮想ディスクの物理エクステントを確認するためにどのようなコマンドを使用できますか。
  
これ：

```powershell
get-virtualdisk -friendlyname “xyz” | get-physicalextent
```
