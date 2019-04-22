---
title: 記憶域スペース ダイレクト - よく寄せられる質問
description: 直接記憶域スペースについてを説明します
keywords: 記憶域スペース
ms.prod: windows-server-threshold
ms.author: kaushik
ms.technology: storage-spaces
ms.topic: article
author: kaushika-msft
ms.date: 10/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: b17aa7ddc783e95fbcc19fe3913192d245133c7f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818913"
---
# <a name="storage-spaces-direct---frequently-asked-questions-faq"></a>記憶域スペース ダイレクト - よく寄せられる質問 (FAQ)

この記事では、一般的なを一覧表示し、よく寄せられる質問に関連する[記憶域スペース ダイレクト](storage-spaces-direct-overview.md)します。

## <a name="when-you-use-storage-spaces-direct-with-3-nodes-can-you-get-both-performance-and-capacity-tiers"></a>3 つのノードで記憶域スペース ダイレクトを使用するとすればパフォーマンスと容量のレベルの両方ですか。

はい、2 つのノード、または 3 ノードの記憶域スペース ダイレクト構成では、パフォーマンスと容量の層の両方を取得できます。 ただし、2 つのデバイスの容量があることを確認する必要があります。 つまり、次の 3 つすべての種類のデバイスを使用する必要があります。NVME、SSD および HDD。
 
## <a name="refs-file-system-provides-real-time-tiaring-with-storage-spaces-direct-does-refs-provides-the-same-functionality-with-shared-storage-spaces-in-2016"></a>Refs ファイル システムでは、リアルタイム tiaring 記憶域スペース ダイレクトを提供します。 REFS 機能を提供します、同じ共有記憶域スペースで 2016 でしょうか。

いいえ、リアルタイムで 2016年での共有記憶域スペースの階層制御は取得されません。 これは、専用記憶域スペース ダイレクトです。 
 
## <a name="can-i-use-an-ntfs-file-system-with-storage-spaces-direct"></a>記憶域スペース ダイレクトで NTFS ファイル システムを使用できますか。
  
はい、記憶域スペース ダイレクト、NTFS ファイル システムを使用することができます。 ただし、REFS をお勧めします。 NTFS では、リアルタイム階層化は提供されません。 
 
## <a name="i-have-configured-2-node-storage-spaces-direct-clusters-where-the-virtual-disk-is-configured-as-2-way-mirror-resiliency-if-i-add-a-new-fault-domain-will-the-resiliency-of-the-existing-virtual-disk-change"></a>仮想ディスクが 2 方向ミラー回復性として構成されているノード記憶域スペース ダイレクト クラスター、2 つを構成しました。 新しい障害ドメインを追加した場合は、既存の仮想ディスクの回復性を変更しますか。

新しい障害ドメインを追加した後、作成した新しい仮想ディスクは 3 方向ミラーにジャンプします。 ただし、既存の仮想ディスクは、双方向ミラー化されたディスクに残ります。 新しい回復性のメリットを得られる、既存のボリュームから、新しい仮想ディスクにデータをコピーできます。
 
## <a name="the-storage-spaces-direct-was-created-using-the-autoconfig0-switch-and-the-pool-created-manually-when-i-try-to-query-the-storage-spaces-direct-pool-to-create-a-new-volume-i-get-a-message-that-says-enable-clusters2d-again-what-should-i-do"></a>記憶域スペース ダイレクトで作成された、autoconfig:0スイッチと、プールを手動で作成します。 新しいボリュームを作成する記憶域スペース ダイレクトのプールを照会しようとすると、"Enable-clusters2d もう一度"を示すメッセージが取得します。どうしたらいいでしょう。

既定で有効にする S2D のコマンドレットを使用して記憶域スペース ダイレクトを構成する場合、コマンドレットではすべてできます。 プールと、階層を作成します。 Autoconfig:0 を使用する場合、手動ですべて行う必要があります。 プールのみを作成した場合、層は必ずしも作成されません。 使用して層をまったく作成されないや接続されているデバイスに対応する方法で階層を作成していない場合、"Enable-clusters2d もう一度"エラー メッセージが表示されます。 運用環境で自動構成スイッチを使用しないことをお勧めします。 
 
## <a name="is-it-possible-to-add-a-spinning-disk-hdd-to-the-storage-spaces-direct-pool-after-you-have-created-storage-spaces-direct-with-ssd-devices"></a>SSD デバイスで記憶域スペース ダイレクトを作成した後、記憶域スペース ダイレクトのプールにスピン ディスク (HDD) を追加することはできますか。

いいえ。 既定では、キャッシュ ディスクを構成、しなかった場合は、1 つのデバイスの種類を使用して、プールを作成してすべてのディスク容量に使用されます。 NVME ディスクを追加するには、その構成にし、NVME ディスク キャッシュを構成します。
 
## <a name="i-have-configured-a-2-rack-fault-domain-rack-1-has-2-fault-domains-rack-2-has-1-fault-domain-each-server-has-4-capacity-100-gb-devices-can-i-use-all-1200-gb-of-space-from-the-pool"></a>2 ラックのフォールト ドメインを構成しました。ラックの 1 が 2 つの障害ドメイン、ラック 2 が 1 の障害ドメイン。 各サーバーでは、4 つの容量の 100 GB デバイスがあります。 プールからすべての 1,200 GB の領域を使用できますか。

いいえ、800 GB のみを使用することができます。 ラックのフォールト ドメインには chuck それぞれそのため、双方向ミラー構成と、重複する land の別のラックがあることを確認する必要があります。
 
## <a name="what-should-the-cache-size-be-when-i-am-configuring-storage-spaces-direct"></a>どのようなキャッシュ サイズべき記憶域スペース ダイレクト設定しているときでしょうか。

ワーキング セットの対応するために、キャッシュのサイズを設定する必要があります (アクティブにするデータの読み取りまたは書き込みを特定の時点)、アプリケーションとワークロードの。

## <a name="how-can-i-determine-the-size-of-cache-that-is-being-used-by-storage-spaces-direct"></a>記憶域スペース ダイレクトで使用されているキャッシュのサイズを特定する方法はありますか

キャッシュ ミスを検査するのにには、PerfMon の組み込みのユーティリティを使用します。 キャッシュ ミス読み取り数/秒クラスター ストレージのハイブリッド ディスク カウンターからを確認します。 多くの読み取りには、キャッシュが不足しているが場合、キャッシュはサイズが小さすぎると、展開したい場合がありますに注意してください。 
 
## <a name="is-there-a-calculator-that-shows-the-exact-size-of-the-disks-that-are-being-set-aside-for-cache-capacity-and-resiliency-that-would-enable-me-to-plan-better"></a>キャッシュ、容量、およびより優れた計画することができるように、回復性の確保設定されるディスクの正確なサイズを示す計算ツールはありますか。

記憶域スペースの計算ツールを使用して、計画に役立つことができます。 使用可能になる http://aka.ms/s2dcalcします。
 
## <a name="what-is-the-best-configuration-that-you-would-recommend-when-configuring-6-servers-and-3-racks"></a>6 つのサーバーと 3 つのラックを構成するときにお勧めする最善の構成とは何ですか。

各ラックの 2 つのサーバーを使用すると、3 方向ミラーの仮想ディスクの回復性を取得できます。 ラックに配置の方法で、OS 構成を指定する場合にのみ、ラック構成を正しく動作することは覚えておいてください。 
 
## <a name="can-i-enable-maintenance-mode-for-a-specific-disk-on-a-specific-server-in-storage-spaces-direct-cluster"></a>記憶域スペース ダイレクト クラスター内の特定のサーバー上の特定のディスクのメンテナンス モードを有効にできますか。

はい、特定のディスクと特定の障害ドメインでの記憶域メンテナンス モードを有効にすることができます。 ノードを一時停止すると、有効にする StorageMaintenanceMode コマンドが自動的に呼び出されます。 次のコマンドを実行して、特定のディスクのことを有効ことができます。

```powershell
Get-PhysicalDisk -SerialNumber <SerialNumber> | Enable-StorageMaintenanceMode
```

## <a name="is-storage-spaces-direct-supported-on-my-hardware"></a>記憶域スペース ダイレクトではサポートされているハードウェアでしょうか。

サポートを確認、ハードウェアの製造元に問い合わせることをお勧めします。 ハードウェア ベンダーは、ハードウェアとかどうかのサポートかどうかについてのコメントにソリューションをテストします。 たとえばの執筆時点でこの、R730 などのサーバー/R730xd/8 個を超えるドライブ スロット R630 SES をサポートすることができ、記憶域スペース ダイレクトと互換性があります。 Dell は、記憶域スペース ダイレクト HBA330 のみをサポートします。 R620 は、SES をサポートしていませんし、記憶域スペース ダイレクトと互換性がありません。

多くのハードウェアのサポートについては、次の web サイトに移動します。Windows Server Catalog
 
## <a name="how-does-storage-spaces-direct-make-use-of-ses"></a>どの記憶域スペース ダイレクトを使用する SES でしょうか。

記憶域スペース ダイレクトされているスラブのデータとメタデータが回復力のある方法で障害ドメインを分散するかどうかを確認する、SCSI エンクロージャ サービス (SES) のマッピングを使用します。 ハードウェアが SES をサポートしていない場合、エンクロージャのマッピングはなく、データの配置は回復力のあるではありません。
 
## <a name="what-command-can-you-use-to-check-the-physical-extent-for-a-virtual-disk"></a>仮想ディスクの物理的なエクステントを確認するには、どのようなコマンドを使用できますか。
  
これ：

```powershell
get-virtualdisk -friendlyname “xyz” | get-physicalextent
```
