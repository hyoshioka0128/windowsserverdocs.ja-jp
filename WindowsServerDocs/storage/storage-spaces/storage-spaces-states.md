---
title: 記憶域スペースと記憶域スペースダイレクトの正常性と動作状態
description: 記憶域スペースダイレクトと記憶域スペース (物理ディスク、プール、仮想ディスクを含む) のさまざまな正常性と動作状態と、その対処方法について説明します。
author: jasongerend
ms.author: jgerend
ms.date: 12/06/2019
ms.topic: article
ms.prod: windows-server
ms.technology: storage-spaces
manager: brianlic
ms.openlocfilehash: e0e763be5691ea7804421ec3ba5ab7882bdb8c3d
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474519"
---
# <a name="troubleshoot-storage-spaces-and-storage-spaces-direct-health-and-operational-states"></a>記憶域スペースのトラブルシューティングと、正常性と動作状態の記憶域スペースダイレクト

> 適用対象: Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server (半期チャネル)、Windows 10、Windows 8.1

このトピックでは、記憶域プール、仮想ディスク (記憶域スペース内のボリュームの下にある)、および[記憶域スペースダイレクト](storage-spaces-direct-overview.md)と[記憶域スペース](overview.md)のドライブの状態と動作状態について説明します。 これらの状態は、読み取り専用の構成のために仮想ディスクを削除できない理由など、さまざまな問題のトラブルシューティングを試みる場合に非常に重要です。 また、ドライブをプールに追加できない理由 (CannotPoolReason) についても説明します。

記憶域スペースには、次に示すように、記憶域*プール*に追加された*物理ディスク*(ハードドライブ、ssd など) と3つの主要なオブジェクトがあります。これにより、プール内の空き領域から*仮想ディスク*を作成できるようになります。 プールのメタデータは、プール内の各ドライブに書き込まれます。 ボリュームは仮想ディスク上に作成され、ファイルが格納されますが、ここではボリュームについては説明しません。

![物理ディスクが記憶域プールに追加され、プール領域から作成された仮想ディスク](media/storage-spaces-states/storage-spaces-object-model.png)

状態と動作状態は、サーバーマネージャー、または PowerShell を使用して表示できます。 次に、クラスターノードのほとんどが不足している記憶域スペースダイレクトクラスターでの (ほとんど問題のない) 正常性状態と操作状態の例を示します (**操作状態**を追加するには、列ヘッダーを右クリックします)。 これはすばらしいクラスターではありません。

![記憶域スペースダイレクトクラスターに存在しない2つのノードの結果を表示するサーバーマネージャー (不足している物理ディスクと仮想ディスクの多くは異常な状態にあります)](media/storage-spaces-states/unhealthy-disks-in-server-manager.png)

## <a name="storage-pool-states"></a>記憶域プールの状態

各記憶域プールの正常性状態は、**正常**、**警告**、または**不明な**状態であり / **Unhealthy**、1つまたは複数の動作状態です。

プールの状態を確認するには、次の PowerShell コマンドを使用します。

```PowerShell
Get-StoragePool -IsPrimordial $False | Select-Object HealthStatus, OperationalStatus, ReadOnlyReason
```

次の出力例は、読み取り専用の動作状態の不明なヘルス状態の記憶域プールを示しています。

```
FriendlyName                OperationalStatus HealthStatus IsPrimordial IsReadOnly
------------                ----------------- ------------ ------------ ----------
S2D on StorageSpacesDirect1 Read-only         Unknown      False        True
```

以降のセクションでは、正常性状態と操作状態について説明します。

### <a name="pool-health-state-healthy"></a>プールのヘルス状態: 正常

| 操作状態    | 説明 |
| ---------            | ---------  |
| [OK] | 記憶域プールは正常です。 |

### <a name="pool-health-state-warning"></a>プールのヘルス状態: 警告

記憶域プールが**警告**のヘルス状態にある場合、プールにアクセスできることを意味しますが、1つまたは複数のドライブに障害が発生しているか、または不足しています。 その結果、記憶域プールの回復性が低下する可能性があります。

|操作状態    |説明|
|---------            |---------  |
|低下しています|記憶域プールに障害が発生しているか、ドライブが不足しています。 この状態は、プールメタデータをホストしているドライブでのみ発生します。 <br><br>**操作**: ドライブの状態を確認し、障害が発生したドライブを交換してから、追加のエラーが発生します。|

### <a name="pool-health-state-unknown-or-unhealthy"></a>プールのヘルス状態: 不明または異常

記憶域プールが不明または異常**な**状態**Unhealthy**にある場合は、記憶域プールが読み取り専用で、プールが**警告**または**OK**の正常性状態に戻るまで変更できないことを意味します。

|操作状態    |読み取り専用の理由 |説明|
|---------            |---------       |--------   |
|読み取り専用|Incomplete (不完全)|これは、記憶域プールが[クォーラム](understand-quorum.md)を失った場合に発生する可能性があります。つまり、プール内のほとんどのドライブが故障しているか、何らかの理由でオフラインになっていることを意味します。 プールがクォーラムを失った場合、記憶域スペースは、十分な数のドライブが再び使用可能になるまで、プールの構成を自動的に読み取り専用に設定します。<br><br>**アクション:** <br>1. 不足しているドライブを再接続します。記憶域スペースダイレクトを使用している場合は、すべてのサーバーをオンラインにします。 <br>2. 管理アクセス許可を使用して PowerShell セッションを開き、次のように入力して、プールを読み取り/書き込みに戻します。<br><br> <code>Get-StoragePool <PoolName> -IsPrimordial $False \| Set-StoragePool -IsReadOnly $false</code>|
||ポリシー|管理者が記憶域プールを読み取り専用に設定している。<br><br>**アクション:** クラスター化された記憶域プールをフェールオーバークラスターマネージャーの読み取り/書き込みアクセスに設定するには、[**プール**] に移動し、プールを右クリックして、[**オンライン**にする] を選択します。<br><br>その他のサーバーと Pc については、管理アクセス許可を使用して PowerShell セッションを開き、次のように入力します。<br><br><code>Get-StoragePool <PoolName> \| Set-StoragePool -IsReadOnly $false</code><br><br> |
||開始中|記憶域スペースは、プール内でのドライブの接続を開始または待機しています。 これは一時的な状態である必要があります。 完全に開始されると、プールは別の動作状態に移行する必要があります。<br><br>**アクション:** プールが*開始*状態のままである場合は、プール内のすべてのドライブが正常に接続されていることを確認します。|

「[読み取り専用構成を持つ記憶域プールの変更](https://social.technet.microsoft.com/wiki/contents/articles/14861.modifying-a-storage-pool-that-has-a-read-only-configuration.aspx)」も参照してください。

## <a name="virtual-disk-states"></a>仮想ディスクの状態

記憶域スペースでは、ボリュームは、プール内の空き領域から分割される仮想ディスク (記憶域スペース) に配置されます。 すべての仮想ディスクの正常性状態は、**正常**、**警告**、**異常**、または**不明**であり、1つまたは複数の動作状態です。

仮想ディスクの状態を確認するには、次の PowerShell コマンドを使用します。

```PowerShell
Get-VirtualDisk | Select-Object FriendlyName,HealthStatus, OperationalStatus, DetachedReason
```

デタッチされた仮想ディスクと、低下または不完全な仮想ディスクを示す出力の例を次に示します。

```
FriendlyName HealthStatus OperationalStatus      DetachedReason
------------ ------------ -----------------      --------------
Volume1      Unknown      Detached               By Policy
Volume2      Warning      {Degraded, Incomplete} None
```

以降のセクションでは、正常性状態と操作状態について説明します。

### <a name="virtual-disk-health-state-healthy"></a>仮想ディスクの正常性状態: 正常

|操作状態    |説明|
|---------            |---------          |
|[OK]    |仮想ディスクは正常です。|
|Suboptimal (最適でない)    |データが複数のドライブに均等に書き込まれていません。 <br><br>**操作**:[最適化-storagepool](https://technet.microsoft.com/itpro/powershell/windows/storage/optimize-storagepool)コマンドレットを実行して、記憶域プールのドライブ使用率を最適化します。|

### <a name="virtual-disk-health-state-warning"></a>仮想ディスクの正常性状態: 警告

仮想ディスクの正常性状態が "**警告**" の場合、1つまたは複数のデータのコピーが使用できないことを意味しますが、記憶域スペースはデータのコピーを少なくとも1つ読み取ることができます。

|操作状態    |説明|
|---------            |---------          |
|サービス中            |Windows は、ドライブを追加または削除した後など、仮想ディスクを修復しています。 修復が完了すると、仮想ディスクが "OK" の正常性状態に戻ります。|
|Incomplete (不完全)           |1つ以上のドライブで障害が発生したか、ドライブが不足しているため、仮想ディスクの回復性が低下します。 ただし、見つからないドライブにはデータの最新のコピーが格納されています。<br><br> **アクション**: <br>1. 不足しているドライブを再接続し、障害が発生したドライブを交換します。記憶域スペースダイレクトを使用している場合は、オフラインになっているすべてのサーバーをオンラインにします。 <br>2. 記憶域スペースダイレクトを使用していない場合は、次に[VirtualDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk)コマンドレットを使用して仮想ディスクを修復します。<br> 記憶域スペースダイレクトは、ドライブの再接続または交換後に、必要に応じて修復を自動的に開始します。|
|低下しています             |1つまたは複数のドライブに障害が発生したか、ドライブに不足しているため、仮想ディスクの回復性が低下します。 <br><br>**アクション**: <br> 1. 不足しているドライブを再接続し、障害が発生したドライブを交換します。記憶域スペースダイレクトを使用している場合は、オフラインになっているすべてのサーバーをオンラインにします。 <br> 2. 記憶域スペースダイレクトを使用していない場合は、次に[VirtualDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk)コマンドレットを使用して仮想ディスクを修復します。 <br>記憶域スペースダイレクトは、ドライブの再接続または交換後に、必要に応じて修復を自動的に開始します。|

### <a name="virtual-disk-health-state-unhealthy"></a>仮想ディスクの正常性状態: 異常

仮想ディスクのヘルス状態が**異常**な場合は、仮想ディスク上のデータの一部またはすべてに現在アクセスできません。

|操作状態    |説明|
|---------            |--------   |
|No redundancy (冗長性なし)|ドライブの数が多すぎるため、仮想ディスクのデータが失われました。<br><br>**操作**: 障害が発生したドライブを交換し、バックアップからデータを復元します。|

### <a name="virtual-disk-health-state-informationunknown"></a>仮想ディスクのヘルス状態: 情報/不明

また、管理者が仮想ディスクをオフラインにした場合、または仮想ディスクが切断された場合、仮想ディスクは、([記憶域スペース] コントロールパネル項目に示されているように)**情報**の正常性状態または**不明な**正常性状態 (PowerShell に表示されます) に配置できます。

|操作状態    |デタッチされた理由 |説明|
|---------            |---------       |--------   |
|デタッチ             |ポリシー別            |管理者が仮想ディスクをオフラインにしたか、または手動でアタッチするように仮想ディスクを設定しました。その場合は、Windows を再起動するたびに、仮想ディスクを手動で接続する必要があります。<br><br>**操作**: 仮想ディスクをオンラインに戻します。 仮想ディスクがクラスター化された記憶域プールにあるときにフェールオーバークラスターマネージャー、[**記憶域**プール] [仮想ディスク] の順に選択し、[  >  **Pools**  >  **Virtual Disks****オフライン**] 状態を表示する仮想ディスクを選択し、[**オンライン**にする] を選択します。 <br><br>クラスターにないときに仮想ディスクをオンラインに戻すには、管理者として PowerShell セッションを開き、次のコマンドを使用します。<br><br> <code>Get-VirtualDisk \| Where-Object -Filter { $_.OperationalStatus -eq "Detached" } \| Connect-VirtualDisk</code><br><br>Windows の再起動後に、クラスター化されていないすべての仮想ディスクを自動的に接続するには、管理者として PowerShell セッションを開き、次のコマンドを使用します。<br><br> <code>Get-VirtualDisk \| Set-VirtualDisk -ismanualattach $false</code>|
|            |異常なディスクの過半数 |この仮想ディスクで使用されているドライブが多すぎる、不足している、または古いデータがある。   <br><br>**アクション**: <br> 1. 不足しているドライブを再接続します。記憶域スペースダイレクトを使用している場合は、オフラインになっているすべてのサーバーをオンラインにします。 <br> 2. すべてのドライブとサーバーがオンラインになったら、障害が発生したドライブを置き換えます。 詳細については、「[ヘルスサービス](../../failover-clustering/health-service-overview.md)」を参照してください。 <br>記憶域スペースダイレクトは、ドライブの再接続または交換後に、必要に応じて修復を自動的に開始します。<br>3. 記憶域スペースダイレクトを使用していない場合は、次に、 [VirtualDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk)コマンドレットを使用して仮想ディスクを修復します。  <br><br>データのコピー数よりも多くのディスクで障害が発生し、仮想ディスクが障害の発生時に修復されなかった場合は、仮想ディスク上のすべてのデータが永久に失われます。 このような場合は、仮想ディスクを削除し、新しい仮想ディスクを作成してから、バックアップから復元します。|
|                     |Incomplete (不完全) |仮想ディスクを読み取るための十分なドライブがありません。    <br><br>**アクション**: <br> 1. 不足しているドライブを再接続します。記憶域スペースダイレクトを使用している場合は、オフラインになっているすべてのサーバーをオンラインにします。 <br> 2. すべてのドライブとサーバーがオンラインになったら、障害が発生したドライブを置き換えます。 詳細については、「[ヘルスサービス](../../failover-clustering/health-service-overview.md)」を参照してください。 <br>記憶域スペースダイレクトは、ドライブの再接続または交換後に、必要に応じて修復を自動的に開始します。<br>3. 記憶域スペースダイレクトを使用していない場合は、次に、 [VirtualDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk)コマンドレットを使用して仮想ディスクを修復します。<br><br>データのコピー数よりも多くのディスクで障害が発生し、仮想ディスクが障害の発生時に修復されなかった場合は、仮想ディスク上のすべてのデータが永久に失われます。 このような場合は、仮想ディスクを削除し、新しい仮想ディスクを作成してから、バックアップから復元します。|
| |タイムアウト|仮想ディスクの接続に時間がかかりすぎました <br><br> **アクション:** 頻繁に発生することはないので、条件が経過したかどうかを確認してみてください。 または、VirtualDisk コマンドレットを使用して仮想ディスクの接続を[解除](https://docs.microsoft.com/powershell/module/storage/disconnect-virtualdisk?view=win10-ps)してから、 [VirtualDisk](https://docs.microsoft.com/powershell/module/storage/connect-virtualdisk?view=win10-ps)コマンドレットを使用して再接続することもできます。 |

## <a name="drive-physical-disk-states"></a>ドライブ (物理ディスク) の状態

以降のセクションでは、ドライブの正常性状態について説明します。 プール内のドライブは、PowerShell では*物理ディスク*オブジェクトとして表されます。

### <a name="drive-health-state-healthy"></a>ドライブの正常性状態:Healthy

|操作状態    |説明|
|---------            |---------          |
|[OK]|ドライブは正常です。|
|サービス中|ドライブ内部でハウスキープ処理を実行中です。 操作が完了すると、ドライブは*OK*のヘルス状態に戻ります。|

### <a name="drive-health-state-warning"></a>ドライブの正常性状態: 警告

ドライブが [警告] 状態の場合には、データの読み取りと書き込みは正常に実行できるものの、ドライブに何らかの問題が発生しています。

|操作状態    |説明|
|---------            |---------          |
|通信の切断|ドライブが見つかりません。 記憶域スペースダイレクトを使用している場合は、サーバーがダウンしている可能性があります。<br><br>**操作**: 記憶域スペースダイレクトを使用している場合は、すべてのサーバーをオンラインに戻します。 それでも解決しない場合は、ドライブを再接続するか、交換してください。「> Windows エラー報告使用した[物理ディスク](../../failover-clustering/troubleshooting-using-wer-reports.md#physical-disk-timed-out)のトラブルシューティング」の手順に従って、このドライブに関する詳細な診断情報を取得してください。|
|Removing from pool (プールから削除中)|記憶域スペースは、記憶域プールからドライブを削除する処理中です。 <br><br> これは一時的な状態です。 削除が完了すると、ドライブがシステムにまだ接続されている場合、ドライブはルートプール内の別の動作状態 (通常は OK) に移行します。|
|Starting maintenance mode (メンテナンス モードを起動中)|管理者がドライブをメンテナンスモードにすると、記憶域スペースがメンテナンスモードになります。 これは一時的な状態です。ドライブはまもなく*メンテナンスモード*の状態になります。|
|メンテナンス モード|管理者はドライブをメンテナンスモードにし、ドライブからの読み取りと書き込みを停止します。 これは通常、ドライブのファームウェアを更新する前、またはエラーをテストする前に行います。<br><br>**操作**: ドライブのメンテナンスモードを終了するには、 [Disable-storagemtenantの](https://technet.microsoft.com/itpro/powershell/windows/storage/disable-storagemaintenancemode)コマンドレットを使用します。|
|Stopping maintenance mode (メンテナンス モードを停止中)|管理者はドライブのメンテナンスモードを終了しましたが、記憶域スペースはドライブをオンラインに戻す処理を行っています。 これは一時的な状態です。ドライブはすぐに別の状態になります (理想的には*正常*)。|
|予測される障害|ドライブは、エラーが発生したことを報告しました。<br><br>**操作**: ドライブを交換します。|
|IO エラー|ドライブにアクセスする際に一時的なエラーが発生しました。<br><br>**アクション**: <br>1. ドライブが**OK**状態に戻らない場合は、 [Reset-PhysicalDisk](https://docs.microsoft.com/powershell/module/storage/reset-physicaldisk)コマンドレットを使用してドライブをワイプすることができます。 <br> 2. [VirtualDisk](https://docs.microsoft.com/powershell/module/storage/repair-virtualdisk)を使用して、影響を受けている仮想ディスクの回復性を復元します。 <br>3. これが引き続き発生する場合は、ドライブを交換します。|
|一時的なエラー|ドライブに一時的なエラーが発生しました。 これは通常、ドライブが応答していないことを意味しますが、記憶域スペース保護パーティションがドライブから不適切に削除されたことを意味する可能性もあります。 <br><br>**アクション**: <br>1. ドライブが**OK**状態に戻らない場合は、 [Reset-PhysicalDisk](https://docs.microsoft.com/powershell/module/storage/reset-physicaldisk)コマンドレットを使用してドライブをワイプすることができます。 <br> 2. [VirtualDisk](https://docs.microsoft.com/powershell/module/storage/repair-virtualdisk)を使用して、影響を受けている仮想ディスクの回復性を復元します。 <br>3. この問題が引き続き発生する場合は、ドライブを交換するか、「> Windows エラー報告を使用したトラブルシューティング」の手順に従って、[物理ディスクをオンラインにできなかった](../../failover-clustering/troubleshooting-using-wer-reports.md#physical-disk-failed-to-come-online)ことを確認してください。|
|Abnormal latency (待機時間の異常)|ドライブのパフォーマンスが低下しています。記憶域スペースダイレクトのヘルスサービスによって測定されています。<br><br>**操作**: これが引き続き発生する場合は、記憶域スペース全体のパフォーマンスを低下させないようにドライブを交換します。

### <a name="drive-health-state-unhealthy"></a>ドライブの正常性状態:異常

状態が [異常] のドライブには、書き込みまたはアクセスができません。

|操作状態    |説明|
|---------            |---------          |
|使用不可|このドライブを記憶域スペースで使用することはできません。 詳細については、「[記憶域スペースダイレクトのハードウェア要件](storage-spaces-direct-hardware-requirements.md)」を参照してください。記憶域スペースダイレクトを使用していない場合は、「[記憶域スペースの概要](https://technet.microsoft.com/library/hh831739(v=ws.11).aspx#Requirements)」を参照してください。|
|Split|ドライブがプールから隔離されています。<br><br>**操作**: ドライブをリセットし、ドライブのすべてのデータを消去して、空のドライブとしてプールに追加し直します。 これを行うには、管理者として PowerShell セッションを開き、VirtualDisk コマンドレットを実行して[から、](https://technet.microsoft.com/itpro/powershell/windows/storage/reset-physicaldisk) [修復](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk)を実行します。 <br><br>このドライブに関する詳細な診断情報を取得するには、「Windows エラー報告を使用したトラブルシューティング」の手順に従って >[物理ディスクをオンラインにできませんでした](../../failover-clustering/troubleshooting-using-wer-reports.md#physical-disk-failed-to-come-online)。|
|古いメタデータ|記憶域スペースにより、ドライブに古いメタデータが見つかりました。<br><br>**Action**: これは一時的な状態である必要があります。 ドライブの状態が [OK] に戻らない場合は、 [VirtualDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk)を実行して、影響を受けている仮想ディスクに対する修復操作を開始できます。 それでも問題が解決しない場合は、 [PhysicalDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/reset-physicaldisk)コマンドレットを使用してドライブをリセットし、ドライブからすべてのデータをワイプしてから、 [VirtualDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk)を実行します。|
|認識されないメタデータ|記憶域スペースがドライブに認識できないメタデータを検出しました。これは通常、ドライブに別のプールのメタデータがあることを意味します。<br><br>**操作**: ドライブをワイプし、現在のプールに追加するには、ドライブをリセットします。 ドライブをリセットするには、管理者として PowerShell セッションを開き、VirtualDisk コマンドレットを実行して[から、](https://technet.microsoft.com/itpro/powershell/windows/storage/reset-physicaldisk) [修復](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk)を実行します。|
|エラーのあるメディア|ドライブにエラーが発生したので、このドライブが今後記憶域スペースで使われることはありません。<br><br>**操作**: ドライブを交換します。 <br><br>このドライブに関する詳細な診断情報を取得するには、「Windows エラー報告を使用したトラブルシューティング」の手順に従って >[物理ディスクをオンラインにできませんでした](../../failover-clustering/troubleshooting-using-wer-reports.md#physical-disk-failed-to-come-online)。|
|Device hardware failure (デバイスのハードウェア障害)|このデバイスでハードウェア障害が発生しました。 <br><br>**操作**: ドライブを交換します。|
|Updating firmware (ファームウェアを更新中)|ドライブのファームウェアを更新しています。 これは通常 1 分未満で終了する一時的な状態であり、その間の読み取りと書き込みはすべて、プール内の別のドライブにより処理されます。 詳細については、「[ドライブのファームウェアを更新](../update-firmware.md)する」を参照してください。|
|開始中|ドライブが稼働開始のための準備をしている状態です。 これは一時的な状態であり、準備が完了すると、ドライブが別の操作状態に移行します。|

## <a name="reasons-a-drive-cant-be-pooled"></a>ドライブをプールできない理由

一部のドライブは、記憶域プールに配置する準備ができていません。 物理ディスクのプロパティを見ると、ドライブがプールに適合していない理由を確認でき `CannotPoolReason` ます。 CannotPoolReason プロパティを表示する PowerShell スクリプトの例を次に示します。

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

次の表は、それぞれの理由をもう少し詳しく説明したものです。

|理由|説明|
|---|---|
|プール内|ドライブは既に記憶域プールに属しています。 <br><br>ドライブは、一度に1つの記憶域プールにしか属することができません。 このドライブを別の記憶域プールで使用するには、まず既存のプールからドライブを削除します。これにより、ドライブ上のデータをプール上の他のドライブに移動するように記憶域スペースに指示されます。 または、記憶域スペースに通知せずにドライブがプールから切断されている場合は、ドライブをリセットします。 <br><br>記憶域プールからドライブを安全に削除するには、[削除-PhysicalDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/remove-physicaldisk)を使用するか、サーバーマネージャー >**ファイルサービスおよび記憶域サービスの**  >  **記憶域プール**、>**物理ディスク**] の順に選択し、ドライブを右クリックして、[**ディスクの削除**] を選択します。<br><br>ドライブをリセットするには、"[リセット-PhysicalDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/reset-physicaldisk)" を使用します。|
|異常|ドライブが正常な状態にないため、交換が必要な可能性があります。|
|リムーバブル メディア|ドライブがリムーバブル ドライブとして分類されています。 <br><br>記憶域スペースは、Windows によってリムーバブルとして認識されるメディア (ブルーレイドライブなど) をサポートしていません。 多くの固定ドライブはリムーバブルスロットにありますが、一般に、Windows によってリムーバブルとして*分類*されるメディアは、記憶域スペースでの使用に適していません。|
|In use by cluster (クラスターで使用中)|ドライブが現在、フェールオーバー クラスターによって使用されています。|
|オフライン|ドライブがオフラインになっています。 <br><br>すべてのオフラインドライブをオンラインにして、を読み取り/書き込みに設定するには、PowerShell セッションを管理者として開き、次のスクリプトを使用します。<br><br><code>Get-Disk \| Where-Object -Property OperationalStatus -EQ "Offline" \| Set-Disk -IsOffline $false</code><br><br><code>Get-Disk \| Where-Object -Property IsReadOnly -EQ $true \| Set-Disk -IsReadOnly $false</code>|
|Insufficient capacity (容量の不足)|これは通常、ドライブの空き領域を占有しているパーティションがある場合に発生します。 <br><br>**操作**: ドライブ上のすべてのデータを消去して、ドライブ上のすべてのボリュームを削除します。 これを行う1つの方法は、[ディスクの消去](https://docs.microsoft.com/powershell/module/storage/clear-disk?view=win10-ps)PowerShell コマンドレットを使用することです。|
|Verification in progress (検証中)|[ヘルスサービス](../../failover-clustering/health-service-overview.md#supported-components-document)は、ドライブ上のドライブまたはファームウェアがサーバー管理者による使用が承認されているかどうかを確認しています。|
|検証できませんでした|[ヘルスサービス](../../failover-clustering/health-service-overview.md#supported-components-document)は、ドライブ上のドライブまたはファームウェアがサーバー管理者による使用が承認されているかどうかを確認できませんでした。|
|Firmware not compliant (非準拠ファームウェア)|[ヘルスサービス](../../failover-clustering/health-service-overview.md#supported-components-document)を使用して、物理ドライブのファームウェアが、サーバー管理者によって指定された承認済みファームウェアのリビジョンの一覧にありません。 |
|Hardware not compliant (非準拠ハードウェア)|このドライブは、[ヘルスサービス](../../failover-clustering/health-service-overview.md#supported-components-document)を使用して、サーバー管理者によって指定された承認済みストレージモデルの一覧に含まれていません。|

## <a name="additional-references"></a>その他のリファレンス

- [記憶域スペース ダイレクト](storage-spaces-direct-overview.md)
- [ハードウェア要件の記憶域スペースダイレクト](storage-spaces-direct-hardware-requirements.md)
- [クラスターとプール クォーラムの概要](understand-quorum.md)