---
title: 記憶域スペース ダイレクトの正常性と操作状態
description: 検索して、別の正常性と記憶域スペース ダイレクトと (物理ディスク、プール、および仮想ディスクを含む)、記憶域スペースの操作の状態を理解する方法とそれらについての対処方法。
keywords: 記憶域スペース、デタッチするには、仮想ディスク、物理ディスクは、機能低下
author: jasongerend
ms.author: jgerend
ms.date: 10/17/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage-spaces
manager: brianlic
ms.openlocfilehash: 5090a68270438bd9a06c7d50f9d4abca066d31e6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849143"
---
# <a name="troubleshoot-storage-spaces-direct-health-and-operational-states"></a>記憶域スペース ダイレクトの正常性と操作状態をトラブルシューティングします。

> 適用対象:Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server (半期チャネル)、Windows 10、Windows 8.1

このトピックでは、正常性と仮想ディスク (記憶域スペースでボリュームの下に配置) を記憶域プールの操作の状態について説明しに存在するドライブ[記憶域スペース ダイレクト](storage-spaces-direct-overview.md)と[記憶域スペース](overview.md)します。 これらの状態理由読み取り専用の構成があるため、仮想ディスクを削除することはできませんなどのさまざまな問題をトラブルシューティングする際に役に立つことができます。 プール (CannotPoolReason) にドライブを追加できない理由も説明します。

記憶域スペースが 3 つのプライマリ オブジェクト -*物理ディスク*(ハード ドライブ、Ssd など) に追加される、*記憶域プール*、作成できるように、記憶域を仮想化*の仮想ディスク*から次のように、プールのディスク領域を解放します。 プールのメタデータは、プール内の各ドライブに書き込まれます。 ボリュームが仮想ディスク上に作成され、ファイルを格納しますが、ここでのボリュームについては説明しません。

![物理ディスクを記憶域プールを追加してから仮想ディスクを作成し、プールの領域](media/storage-spaces-states/storage-spaces-object-model.png)

サーバー マネージャーで、または PowerShell を使用した正常性と操作状態を表示できます。 さまざまな (不適切なほとんどの場合) の正常性とそのクラスター ノードの大部分が不足している記憶域スペース ダイレクト クラスターでの操作の状態の例を次に示します (追加する列ヘッダーを右クリックして**動作状態**)。 これは、満足のクラスターがありません。

![サーバー マネージャーの多数の物理ディスクと異常な状態に仮想ディスクがありません - 記憶域スペース ダイレクト クラスターに不足している 2 つのノードの結果を表示](media/storage-spaces-states/unhealthy-disks-in-server-manager.png)

## <a name="storage-pool-states"></a>記憶域プールの状態

すべての記憶域プールが正常性状態の**健全**、**警告**、または**不明な**/**異常**も、1 つ以上操作の状態。

プールの状態を確認するには、次の PowerShell コマンドを使用します。

```PowerShell
Get-StoragePool -IsPrimordial $False | Select-Object HealthStatus, OperationalStatus, ReadOnlyReason
```

読み取り専用の動作状態は不明な正常性の状態で、記憶域プールを示す出力の例を次に示します。

```
FriendlyName                OperationalStatus HealthStatus IsPrimordial IsReadOnly
------------                ----------------- ------------ ------------ ----------
S2D on StorageSpacesDirect1 Read-only         Unknown      False        True
```

次のセクションでは、正常性と操作状態を示します。

### <a name="pool-health-state-healthy"></a>プールの正常性の状態:正常

|動作状態    |説明|
|---------            |---------  |
|OK|記憶域プールは正常です。|

### <a name="pool-health-state-warning"></a>プールの正常性の状態:警告

記憶域プールの場合、**警告**正常性状態では、プールは、アクセスできるが、1 つまたは複数のドライブが失敗したかが不足していることを意味します。 結果として、記憶域プールに回復性を低下がある可能性があります。

|動作状態    |説明|
|---------            |---------  |
|［低下］|記憶域プールには、不足しているかどうかのドライブがあります。 この状態は、プールのメタデータをホストしているドライブでのみ発生します。 <br><br>**アクション**:ドライブの状態を確認しはその他の障害が発生する前に、失敗したすべてのドライブを交換します。|

### <a name="pool-health-state-unknown-or-unhealthy"></a>プールの正常性の状態:不明または異常

記憶域プールの場合、**不明な**または**異常**正常性状態、つまり記憶域プールは読み取り専用にプールが返されるまでに変更することはできません、**警告**または**OK**正常性状態。

|動作状態    |読み取り専用の理由 |説明|
|---------            |---------       |--------   |
|読み取り専用かどうか|不完全です|これは、記憶域プールが失った場合に発生することがその[クォーラム](understand-quorum.md)プール内のほとんどのドライブが失敗したか、何らかの理由がオフラインにすることを意味します。 プールのクォーラムを失ったときに記憶域スペースが自動的に設定、プールの構成を読み取り専用に十分なドライブが再び使用可能になるまでです。<br><br>**アクション:** <br>1. 不足しているドライブを再接続し、記憶域スペース ダイレクトを使用して、場合は、オンラインのすべてのサーバーを表示します。 <br>2. プールを管理者権限で PowerShell セッションを開く」と入力し、読み取り/書き込みに設定します。<br><br> <code>Get-StoragePool <PoolName> -IsPrimordial $False \| Set-StoragePool -IsReadOnly $false</code>|
||ポリシー|管理者は、読み取り専用に記憶域プールを設定します。<br><br>**アクション:** 読み取り/書き込みアクセスでは、フェールオーバー クラスター マネージャーにクラスター化された記憶域プールを設定するに移動して**プール**プールを右クリックし、**オンライン**します。<br><br>その他のサーバーや Pc を使用して、管理者権限で PowerShell セッションを開くし、入力します。<br><br><code>Get-StoragePool <PoolName> \| Set-StoragePool -IsReadOnly $false</code><br><br> |
||Starting|記憶域スペースの開始またはドライブをプールに接続するために待機しています。 これは、一時的な状態でなければなりません。 完全に開始されると、プールは、さまざまな動作状態に移行する必要があります。<br><br>**アクション:** プール内に保持している場合、*開始*状態、プール内のすべてのドライブが正しく接続されているかどうかを確認してください。|

参照してください[読み取り専用の構成を持つ記憶域プールを変更する](https://social.technet.microsoft.com/wiki/contents/articles/14861.modifying-a-storage-pool-that-has-a-read-only-configuration.aspx)します。

## <a name="virtual-disk-states"></a>仮想ディスクの状態

記憶域スペースのボリュームは、プールに空き領域から分割した仮想ディスク (記憶域スペース) 上に配置されます。 すべての仮想ディスクが正常性状態の**健全**、**警告**、**異常**、または**不明な**と 1 つまたは複数の操作状態。

状態の仮想ディスクの中を確認するには、次の PowerShell コマンドを使用します。

```PowerShell
Get-VirtualDisk | Select-Object FriendlyName,HealthStatus, OperationalStatus, DetachedReason
```

デタッチされた仮想ディスクと低下/未完了の仮想ディスクを表示出力の例を次に示します。

```
FriendlyName HealthStatus OperationalStatus      DetachedReason
------------ ------------ -----------------      --------------
Volume1      Unknown      Detached               By Policy
Volume2      Warning      {Degraded, Incomplete} None
```

次のセクションでは、正常性と操作状態を示します。

### <a name="virtual-disk-health-state-healthy"></a>仮想ディスクのヘルス状態:正常

|動作状態    |説明|
|---------            |---------          |
|OK    |仮想ディスクは正常です。|
|最適ではないです。    |データはないドライブ間で均等に書き込まれます。 <br><br>**アクション**:実行して、記憶域プールのドライブ使用率の最適化、 [Optimize-storagepool](https://technet.microsoft.com/itpro/powershell/windows/storage/optimize-storagepool)コマンドレット。|

### <a name="virtual-disk-health-state-warning"></a>仮想ディスクのヘルス状態:警告

仮想ディスクの場合、**警告**正常性状態、記憶域スペースは、少なくとも 1 つのデータのコピーを読み取ることはできますが、データの 1 つまたは複数のコピーは使用できないことを意味します。

|動作状態    |説明|
|---------            |---------          |
|サービスで            |追加またはドライブを削除した後のなどの仮想ディスクは、Windows で修復しています。 修復が完了したら、仮想ディスクは、[ok] のヘルス状態に戻ります。|
|不完全です           |1 つまたは複数のドライブが失敗したかが欠落しているために、仮想ディスクの回復性が減少します。 ただし、不足しているドライブには、データのコピー最新の状態にはが含まれます。<br><br> **アクション**: <br>1. 不足している、すべてのドライブを再接続、失敗したドライブを交換および記憶域スペース ダイレクトを使用して場合、オンライン オフラインになっているすべてのサーバー。 <br>2. 仮想ディスクを使用して、次を修復するを使用していない記憶域スペース ダイレクトの場合、 [Repair-virtualdisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk)コマンドレット。<br> 記憶域スペース ダイレクト自動的に起動、修復を再接続またはドライブの交換後に必要な場合。|
|［低下］             |1 つまたは複数のドライブが失敗したかがないと、これらのドライブ上のデータのコピーが古くなったために、仮想ディスクの回復性が減少します。 <br><br>**アクション**: <br> 1. 不足している、すべてのドライブを再接続、失敗したドライブを交換および記憶域スペース ダイレクトを使用して場合、オンライン オフラインになっているすべてのサーバー。 <br> 2. 仮想ディスクを使用して、次を修復するを使用していない記憶域スペース ダイレクトの場合、 [Repair-virtualdisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk)コマンドレット。 <br>記憶域スペース ダイレクト自動的に起動、修復を再接続またはドライブの交換後に必要な場合。|

### <a name="virtual-disk-health-state-unhealthy"></a>仮想ディスクのヘルス状態:Unhealthy

仮想ディスクの場合、**異常**正常性状態、仮想ディスク上のデータのすべてまたは一部が現在アクセスできません。

|動作状態    |説明|
|---------            |--------   |
|非冗長|仮想ディスクが多すぎるドライブが失敗したため、データを失った。<br><br>**アクション**:失敗したドライブを交換し、バックアップからデータを復元します。|

### <a name="virtual-disk-health-state-informationunknown"></a>仮想ディスクのヘルス状態:情報/不明

仮想ディスクにも、**情報**正常性状態に示すように、記憶域スペースのコントロール パネル項目) または**不明な**正常性状態 (PowerShell で表示される) と、管理者が仮想ディスクを要したかどうかオフラインまたは仮想ディスクがデタッチ済みになります。

|動作状態    |デタッチされた理由 |説明|
|---------            |---------       |--------   |
|Detached             |ポリシーによって            |この場合は、Windows が起動するたびに、仮想ディスクを手動でアタッチする必要があります、管理者が仮想ディスクをオフラインまたは手動の添付ファイルを必要とする仮想ディスクを設定します、。<br><br>**アクション**:仮想ディスクをオンラインに戻すを表示します。 フェールオーバー クラスター マネージャーでを選択するためには、仮想ディスクがクラスター化された記憶域プールの場合、**ストレージ** > **プール** > **仮想ディスク**、表示する仮想ディスクを選択、**オフライン**状態と、選択**オンライン**します。 <br><br>まとめる仮想ディスクをオンラインに戻すには、クラスターではないとき、PowerShell セッションを管理者として開きから次のコマンドを使用して再試行してください。<br><br> <code>Get-VirtualDisk \| Where-Object -Filter { $_.OperationalStatus -eq "Detached" } \| Connect-VirtualDisk</code><br><br>Windows の再起動後に自動的にすべての非クラスター化の仮想ディスクをアタッチ、管理者として PowerShell セッションを開くし、次のコマンドを使用しています。<br><br> <code>Get-VirtualDisk \| Set-VirtualDisk -ismanualattach $false</code>|
|            |異常な場合のマジョリティ ディスク |この仮想ディスクによって使用される多数のドライブは、失敗したかが指定されて、データは古いデータします。   <br><br>**アクション**: <br> 1. 不足しているドライブを再接続して場合、記憶域スペース ダイレクトを使用して、オンライン、オフラインになっているサーバー。 <br> 2. すべてのドライブやサーバーがオンライン後、失敗したすべてのドライブを交換してください。 参照してください[ヘルス サービス](../../failover-clustering/health-service-overview.md)詳細についてはします。 <br>記憶域スペース ダイレクト自動的に起動、修復を再接続またはドライブの交換後に必要な場合。<br>3.仮想ディスクを使用して、次を修復するを使用していない記憶域スペース ダイレクトの場合、 [Repair-virtualdisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk)コマンドレット。  <br><br>データのコピーがあるし、仮想ディスクが修復された中間の障害よりも多くのディスクが失敗した場合は、仮想ディスク上のすべてのデータを完全に失われます。 残念ながらここでは仮想ディスクを削除、仮想ディスクの新規作成し、バックアップから復元します。|
|                     |不完全です |十分なドライブでは、仮想ディスクの読み取りに存在します。    <br><br>**アクション**: <br> 1. 不足しているドライブを再接続して場合、記憶域スペース ダイレクトを使用して、オンライン、オフラインになっているサーバー。 <br> 2. すべてのドライブやサーバーがオンライン後、失敗したすべてのドライブを交換してください。 参照してください[ヘルス サービス](../../failover-clustering/health-service-overview.md)詳細についてはします。 <br>記憶域スペース ダイレクト自動的に起動、修復を再接続またはドライブの交換後に必要な場合。<br>3.仮想ディスクを使用して、次を修復するを使用していない記憶域スペース ダイレクトの場合、 [Repair-virtualdisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk)コマンドレット。<br><br>データのコピーがあるし、仮想ディスクが修復された中間の障害よりも多くのディスクが失敗した場合は、仮想ディスク上のすべてのデータを完全に失われます。 残念ながらここでは仮想ディスクを削除、仮想ディスクの新規作成し、バックアップから復元します。|
| |Timeout|仮想ディスクをアタッチする時間がかかりすぎます <br><br> **アクション:** これは、ことはできません発生する多くの場合、ため、時間条件を満たすかどうかに参照してください。 行うこともできます。 仮想ディスクを取り外し、または、 [Disconnect-virtualdisk](https://docs.microsoft.com/powershell/module/storage/disconnect-virtualdisk?view=win10-ps)コマンドレットを使用して、 [Connect-virtualdisk](https://docs.microsoft.com/powershell/module/storage/connect-virtualdisk?view=win10-ps)コマンドレットを再接続します。 |

## <a name="drive-physical-disk-states"></a>ドライブ (物理ディスク) の状態

次に、正常性状態がドライブであることを説明します。 プール内のドライブとして PowerShell で表される*物理ディスク*オブジェクト。

### <a name="drive-health-state-healthy"></a>ドライブの正常性の状態:正常

|動作状態    |説明|
|---------            |---------          |
|OK|ドライブは正常です。|
|サービスで|ドライブがいくつかの内部ハウスキープ処理操作を実行しています。 アクションが完了したら、ドライブを返す必要があります、 *OK*正常性状態。|

### <a name="drive-health-state-warning"></a>ドライブの正常性の状態:警告

警告状態は、ドライブの読み取りとデータを適切に記述が問題です。

|動作状態    |説明|
|---------            |---------          |
|通信の切断|ドライブがありません。 記憶域スペース ダイレクトを使用して場合、これは、サーバーがダウン可能性があります。<br><br>**アクション**:記憶域スペース ダイレクトを使用して、場合は、すべてのサーバーをオンラインに戻すを提供します。 ドライブを再接続、置換、または Windows エラー報告を使用したトラブルシューティングの手順に従ってそのドライブについての詳細な診断情報の取得を試みる場合、これが解決しない、>[物理ディスクがタイムアウト](../../failover-clustering/troubleshooting-using-wer-reports.md#physical-disk-timed-out)します。|
|プールから削除します。|記憶域スペースは、その記憶域プールからドライブを削除する予定です。 <br><br> これは、一時的な状態です。 削除が完了すると、ドライブがシステムに接続されている場合、ドライブに遷移別の動作状態 (通常は OK) primordial プールでします。|
|メンテナンス モードの開始|記憶域スペースは、管理者は、ドライブをメンテナンス モードにした後は、メンテナンス モードでドライブを配置する予定です。 これは一時的な状態です - ドライブがである必要があります間もなく、*メンテナンス モードで*状態。|
|メンテナンス モード|管理者は、読み取りし、ドライブから書き込みを停止する、ドライブをメンテナンス モードで配置されます。 ドライブのファームウェアを更新する前に、または失敗をテストするときに、これは通常に行われます。<br><br>**アクション**:メンテナンス モードからドライブを使用、[無効 StorageMaintenanceMode](https://technet.microsoft.com/itpro/powershell/windows/storage/disable-storagemaintenancemode)コマンドレット。|
|メンテナンス モードを停止しています|管理者が、ドライブをメンテナンス モードを終了し、記憶域スペースは、ドライブをオンラインに戻すプロセスではします。 これは一時的な状態です - ドライブする必要がありますが理想的です - 別の状態である早く*健全*します。|
|予測される障害|ドライブは、失敗した場合の近くにあることを報告します。<br><br>**アクション**:ドライブを交換します。|
|IO エラー|ドライブへのアクセス、一時的なエラーが発生しました。<br><br>**アクション**: <br>1. ドライブに移行しない場合、 **OK**状態を使用してもかまいません、 [Reset-physicaldisk](https://docs.microsoft.com/powershell/module/storage/reset-physicaldisk)コマンドレットは、ドライブをワイプします。 <br> 2. 使用[Repair-virtualdisk](https://docs.microsoft.com/powershell/module/storage/repair-virtualdisk)に影響を受けた仮想ディスクの回復性を復元します。 <br>3.これが発生している場合は、ドライブを交換します。|
|一時的なエラー|ドライブと一時エラーが発生しました。 これは通常、ドライブが応答ではありませんでしたも考えられますが保護パーティションがドライブから削除された不適切な記憶域スペースに意味します。 <br><br>**アクション**: <br>1. ドライブに移行しない場合、 **OK**状態を使用してもかまいません、 [Reset-physicaldisk](https://docs.microsoft.com/powershell/module/storage/reset-physicaldisk)コマンドレットは、ドライブをワイプします。 <br> 2. 使用[Repair-virtualdisk](https://docs.microsoft.com/powershell/module/storage/repair-virtualdisk)に影響を受けた仮想ディスクの回復性を復元します。 <br>3.これが発生している場合、ドライブを交換または Windows エラー報告を使用したトラブルシューティングの手順に従ってそのドライブについての詳細な診断情報の取得を試みる >[物理ディスクがオンラインにできない](../../failover-clustering/troubleshooting-using-wer-reports.md#physical-disk-failed-to-come-online)します。|
|異常な待機時間|ドライブのパフォーマンスが低いに、記憶域スペース ダイレクトにヘルス サービスで測定されます。<br><br>**アクション**:これが発生している場合は、全体としての記憶域スペースのパフォーマンスは削減されないので、ドライブを交換します。

### <a name="drive-health-state-unhealthy"></a>ドライブの正常性の状態:Unhealthy

異常な状態では、ドライブに書き込まれた現在またはアクセスできません。

|動作状態    |説明|
|---------            |---------          |
|使用できません。|このドライブは、記憶域スペースでは使用できません。 詳細については、次を参照してください。[記憶域スペース ダイレクトのハードウェア要件](storage-spaces-direct-hardware-requirements.md)場合使用していない記憶域スペース ダイレクト; を参照してください。[記憶域スペースの概要](https://technet.microsoft.com/library/hh831739(v=ws.11).aspx#Requirements)します。|
|分割|ドライブは、プールから区切られたになります。<br><br>**アクション**:ドライブからすべてのデータを消去して、空のドライブとしてプールに追加して、ドライブをリセットします。 これを行うには、実行、管理者として PowerShell セッションを開く、 [Reset-physicaldisk](https://technet.microsoft.com/itpro/powershell/windows/storage/reset-physicaldisk)コマンドレット、し、実行[Repair-virtualdisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk)します。 <br><br>そのドライブについての詳細な診断情報を取得するには、Windows エラー報告を使用したトラブルシューティングの手順に従います >[物理ディスクがオンラインにできない](../../failover-clustering/troubleshooting-using-wer-reports.md#physical-disk-failed-to-come-online)します。|
|古いメタデータ|記憶域スペースでは、ドライブの古いメタデータが見つかりました。<br><br>**アクション**:これは、一時的な状態でなければなりません。 実行することができる場合は、ドライブは、OK に移行しない、 [Repair-virtualdisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk)で修復操作を開始する影響を受けた仮想ディスク。 使用してドライブをリセットするには、問題が解決されない場合、 [Reset-physicaldisk](https://technet.microsoft.com/itpro/powershell/windows/storage/reset-physicaldisk)コマンドレットは、ドライブ、および実行のすべてのデータをワイプ[Repair-virtualdisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk)します。|
|認識されないメタデータ|記憶域スペースでは、通常はドライブがそれを別のプールからメタデータがあることを意味すると、ドライブの認識できないメタデータが見つかりました。<br><br>**アクション**:ドライブをワイプし、現在のプールに追加して、ドライブをリセットします。 ドライブをリセットするには、管理者は、実行、PowerShell セッションを開きます、 [Reset-physicaldisk](https://technet.microsoft.com/itpro/powershell/windows/storage/reset-physicaldisk)コマンドレットを実行し、 [Repair-virtualdisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk)。|
|失敗したメディア|ドライブは失敗し、記憶域スペースではもう使われません。<br><br>**アクション**:ドライブを交換します。 <br><br>そのドライブについての詳細な診断情報を取得するには、Windows エラー報告を使用したトラブルシューティングの手順に従います >[物理ディスクがオンラインにできない](../../failover-clustering/troubleshooting-using-wer-reports.md#physical-disk-failed-to-come-online)します。|
|デバイスのハードウェア障害|このドライブでハードウェア障害が発生しました。 <br><br>**アクション**:ドライブを交換します。|
|ファームウェアの更新|Windows は、ドライブのファームウェアを更新しています。 これは、通常は 1 分未満を継続して、プール内の他のドライブがすべて処理時間の読み取りし、書き込みを一時的な状態です。 詳細については、次を参照してください。[ドライブのファームウェア更新](../update-firmware.md)します。|
|Starting|ドライブは、操作の準備ができます。 一時的な状態で完了すると、ドライブは、さまざまな動作状態に移行する必要がありますがあります。|

## <a name="reasons-a-drive-cant-be-pooled"></a>上の理由から、ドライブをプールすることはできません。

だけいくつかのドライブは、記憶域プールに配置する準備ができていません。 ドライブを調べることでプールを対象となるできない理由を見つけることができます、`CannotPoolReason`物理ディスクのプロパティ。 CannotPoolReason プロパティを表示する PowerShell スクリプトの例を次に示します。

```PowerShell
Get-PhysicalDisk | Format-Table FriendlyName,MediaType,Size,CanPool,CannotPoolReason
```

出力例を次に示します。

```
FriendlyName          MediaType          Size CanPool CannotPoolReason
------------          ---------          ---- ------- ----------------
ATA MZ7LM120HCFD00D3  SSD        120034123776   False Insufficient Capacity
Msft Virtual Disk     SSD         10737418240    True
Generic Physical Disk SSD        119990648832   False In a Pool
```

次の表では、それぞれの理由について少し詳しく説明を示します。

|Reason|説明|
|---|---|
|プール内|ドライブは、既に記憶域プールに属しています。 <br><br>ドライブは、一度に 1 つのストレージ プールのみに属することができます。 このドライブを別の記憶域プールで使用するには、最初に既存のプール、記憶域スペース プール上で、ドライブ上の他のドライブにデータを移動するように指示するからドライブを削除します。 または、ドライブは、記憶域スペースを通知することがなく、プールから切断されている場合、ドライブをリセットします。 <br><br>記憶域プールからドライブを安全に削除するには、次のように使用します[Remove-physicaldisk](https://technet.microsoft.com/itpro/powershell/windows/storage/remove-physicaldisk)、サーバー マネージャーに移動または > **File and Storage Services** > **記憶域プール**、。>**物理ディスク**ドライブを右クリックし、**ディスクの削除**します。<br><br>ドライブをリセットするには、使用[Reset-physicaldisk](https://technet.microsoft.com/itpro/powershell/windows/storage/reset-physicaldisk)します。|
|正常ではありません。|ドライブは、正常な状態にないし、交換する必要があります。|
|リムーバブル メディア|ドライブは、リムーバブル ドライブとして分類されます。 <br><br>記憶域スペースは、ブルーレイ ドライブなどのリムーバブルと Windows によって認識されるメディアをサポートしていません。 固定の多くがドライブは、リムーバブルのスロットに一般に、メディアの*分類*リムーバブルとしての Windows では、記憶域スペースで使用に適していません。|
|クラスターで使用中|ドライブは、フェールオーバー クラスターによって使用されています。|
|オフライン|ドライブがオフラインです。 <br><br>すべてのオフラインのドライブをオンラインと読み取り/書き込みに設定するには、PowerShell セッションを管理者としてを開きを次のスクリプトを使用します。<br><br><code>Get-Disk \| Where-Object -Property OperationalStatus -EQ "Offline" \| Set-Disk -IsOffline $false</code><br><br><code>Get-Disk \| Where-Object -Property IsReadOnly -EQ $true \| Set-Disk -IsReadOnly $false</code>|
|容量の不足|これは通常、ドライブの空き領域を占有するパーティションがある場合に発生します。 <br><br>**アクション**:ドライブ上のすべてのデータを消去、ドライブ上にあるボリュームを削除します。 1 つの簡単な方法が使用するには、 [Clear-disk](https://docs.microsoft.com/powershell/module/storage/clear-disk?view=win10-ps) PowerShell コマンドレット。|
|検証中です。|[ヘルス サービス](../../failover-clustering/health-service-overview.md#supported-components-document)はかどうか、ドライブまたはドライブのファームウェアの使用が承認サーバーの管理者を確認します。|
|検証に失敗しました|[ヘルス サービス](../../failover-clustering/health-service-overview.md#supported-components-document)かどうか、ドライブまたはドライブのファームウェアの使用が承認サーバーの管理者を確認できませんでした。|
|ファームウェアに準拠していません。|物理ドライブのファームウェアが承認されたファームウェアのリビジョンを使用して、サーバー管理者によって指定のリストにない、[ヘルス サービス](../../failover-clustering/health-service-overview.md#supported-components-document)します。 |
|準拠していないハードウェア|使用して、サーバー管理者によって指定された承認済みのストレージ モデルの一覧で、ドライブがない、[ヘルス サービス](../../failover-clustering/health-service-overview.md#supported-components-document)します。|

## <a name="see-also"></a>関連項目

- [記憶域スペース ダイレクト](storage-spaces-direct-overview.md)
- [記憶域スペース ダイレクトのハードウェア要件](storage-spaces-direct-hardware-requirements.md)
- [クラスターとプールのクォーラムを理解します。](understand-quorum.md)