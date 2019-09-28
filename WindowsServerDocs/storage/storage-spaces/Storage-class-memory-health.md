---
ms.assetid: 2bab6bf6-90e7-46a7-b917-14a7a8f55366
title: Windows での記憶域クラス メモリ (NVDIMM-N) の正常性管理
ms.prod: windows-server
ms.author: jgerend
ms.manager: dongill
ms.technology: storage-spaces
ms.topic: article
author: JasonGerend
ms.date: 06/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: 03d986832e14e0dd7b80324de3c9f14d0537dba5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402907"
---
# <a name="storage-class-memory-nvdimm-n-health-management-in-windows"></a>Windows での記憶域クラス メモリ (NVDIMM-N) の正常性管理

> 適用先:Windows Server 2019、Windows Server 2016、Windows Server (半期チャネル)、Windows 10

この記事では、Windows の記憶域クラス メモリ (NVDIMM-N) デバイスに固有のエラー処理と正常性管理に関する情報をシステム管理者および IT プロフェッショナルに提供して、記憶域クラス メモリと従来の記憶装置の違いを明らかにします。

Windows での記憶域クラス メモリ デバイスのサポートについてご存知ない場合は、以下のショート ビデオで概要が説明されています。
- [Windows Server 2016 でのブロック記憶域としての非揮発性メモリ (NVDIMM-N) の使用](https://channel9.msdn.com/Events/Build/2016/P466)
- [非揮発性メモリ (NVDIMM) を Windows Server 2016 のバイトアドレス可能な記憶域として使用する](https://channel9.msdn.com/Events/Build/2016/P470)
- [Windows Server 2016 で永続メモリを使用して SQL Server 2016 のパフォーマンスを向上させる](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-Windows-Server-2016-SCM--FAST)

「[記憶域スペースダイレクトでの永続メモリの理解と配置](deploy-pmem.md)」も参照してください。

JEDEC 準拠 NVDIMM-N 記憶域クラス メモリ デバイスは、Windows Server 2016 および Windows 10 (バージョン 1607) 以降の Windows において、ネイティブ ドライバーでサポートされます。 これらのデバイスの動作は他のディスク (HDD や SSD) に似ていますが、いくつかの違いがあります。

ここに記載されているすべての状態は、めったに発生しないと思われますが、ハードウェアが使用されている状態に依存します。

以下のさまざまなケースで、記憶域スペース構成を参照することがあります。 特に注目するのは、記憶域スペースでミラー化されたライトバック キャッシュとして 2 つの NVDIMM-N デバイスを使用する構成です。 そのような構成をセットアップするには、「[NVDIMM-N ライトバック キャッシュを使った記憶域スペースの構成](https://msdn.microsoft.com/library/mt650885.aspx)」を参照してください。

Windows Server 2016 では、記憶域スペースの GUI に、NVDIMM-N バスの種類が "不明" として表示されます。 これは機能が失われたわけでも、プール、記憶域 VD が作成できないことを示すものでもはありません。 バスの種類は、次のコマンドを実行して確認できます。

```powershell
PS C:\>Get-PhysicalDisk | fl
```
コマンドレットの出力の BusType パラメーターに、バスの種類が "SCM" と正しく表示されます。

## <a name="checking-the-health-of-storage-class-memory"></a>記憶域クラス メモリの正常性確認
記憶域クラス メモリの正常性を照会するには、Windows PowerShell セッションで、次のコマンドを使用します。

```powershell
PS C:\> Get-PhysicalDisk | where BusType -eq "SCM" | select SerialNumber, HealthStatus, OperationalStatus, OperationalDetails
```

これにより、この出力例が得られます。

| SerialNumber | HealthStatus | OperationalStatus | OperationalDetails |
| --- | --- | --- | --- |
| 802c-01-1602-117cb5fc | 正常 | OK | |
| 802c-01-1602-117cb64f | 警告 | Predictive Failure | {Threshold Exceeded,NVDIMM\_N Error} |

> [!NOTE]
> イベントで指定された NVDIMM-N デバイスの物理的な場所を検索するには、イベント ビューアーのイベントの **[詳細]** タブで、 **[EventData]**  >  **[Location]** に移動します。 Windows Server 2016 では NVDIMM-N デバイスの場所が正しく表示されませんが、これは Windows Server バージョン 1709 で修正されています。

さまざまな正常性の状態を理解するには、以下のセクションをご覧ください。

## <a name="warning-health-status"></a>"Warning" (警告) の正常性状態

これは、記憶域クラス メモリ デバイスの正常性を確認すると、以下の出力例が示すように正常性状態として**警告**が表示される状態です。

| SerialNumber | HealthStatus | OperationalStatus | OperationalDetails |
| --- | --- | --- | --- |
| 802c-01-1602-117cb5fc | 正常 | OK | |
| 802c-01-1602-117cb64f | 警告 | Predictive Failure | {Threshold Exceeded,NVDIMM\_N Error} |

この状態について、以下の表で説明します。

| | 説明 |
| --- | --- |
| 起こり得る状態 | NVDIMM-N 警告しきい値違反 |
| 根本原因 | NVDIMM-N デバイスは、温度、NVM の有効期間、電源の有効期間など、さまざまなしきい値を追跡します。 これらのしきい値のいずれかを超えると、オペレーティング システムに通知されます。 |
| 通常の動作 | デバイスは引き続き完全に動作します。 これは警告であり、エラーではありません。 |
| 記憶域スペースの動作 | デバイスは引き続き完全に動作します。 これは警告であり、エラーではありません。 |
| 詳細情報 | PhysicalDisk オブジェクトの OperationalStatus フィールド。 EventLog – Microsoft-Windows-ScmDisk0101/Operational |
| 操作 | 警告しきい値の違反によっては、NVDIMM-N のすべてまたは特定部分の交換を検討することが賢明である場合があります。 たとえば、NVM の有効期間しきい値の違反が発生した場合に、NVDIMM-N を交換することが合理的である場合があります。 |

## <a name="writes-to-an-nvdimm-n-fail"></a>NVDIMM-N への書き込みが失敗する

この状態では、記憶域クラス メモリ デバイスの正常性を確認すると、以下の出力例が示すように、正常性状態が **Unhealthy** (異常)、操作状態が **IO Error**(IO エラー) と表示されます。

| SerialNumber | HealthStatus | OperationalStatus | OperationalDetails |
| --- | --- | --- | --- |
| 802c-01-1602-117cb5fc | 正常 | OK | |
| 802c-01-1602-117cb64f | Unhealthy | {Stale Metadata, IO Error, Transient Error} | {Lost Data Persistence, Lost Data, NV...} |

この状態について、以下の表で説明します。

| | 説明 |
| --- | --- |
| 起こり得る状態 | 永続性/バックアップ電力の喪失 |
|根本原因|NVDIMM-N デバイスは、永続性のためにバックアップ電源 (通常ではバッテリやスーパー キャパシター) に依存しています。 このバックアップ電源を利用できない場合、またはデバイスが何らかの理由 (コントローラー/Flash エラー) でバックアップを実行できない場合は、データが危険にさらされており、Windows は影響を受けているデバイスへのさらなる書き込みを阻止します。 データを退避させるための読み取りは引き続き可能です。|
|通常の動作|NTFS ボリュームのマウントが解除されます。<br>PhysicalDisk の正常性状態フィールドには、影響を受けているすべての NVDIMM-N デバイスについて "Unhealthy" (異常)が表示されます。|
|記憶域スペースの動作|影響を受けている NVDIMM-N が 1 つだけである限り、記憶域スペースは操作可能であり続けます。 複数のデバイスが影響を受けている場合、記憶域スペースへの書き込みは失敗します。 <br>PhysicalDisk の正常性状態フィールドには、影響を受けているすべての NVDIMM-N デバイスについて "Unhealthy" (異常)が表示されます。|
|詳細情報|PhysicalDisk オブジェクトの OperationalStatus フィールド。<br>EventLog – Microsoft-Windows-ScmDisk0101/Operational|
|操作|影響を受けている NVDIMM-N のデータをバックアップすることをお勧めします。 読み取りアクセスを可能にするには、ディスクを手動でオンライン化します (ディスクは読み取り専用の NTFS ボリュームとして表されます)。<br><br>この状態を完全に解消するには、根本原因を解決する必要があります (すなわち、問題に応じて、電源を修理するか、または NVDIMM-N を交換します)。NVDIMM-N 上のボリュームは、オフライン化してから再びオンライン化するか、またはシステムを再起動する必要があります。<br><br>記憶域スペースで NVDIMM-N を再び使用するには、**Reset-PhysicalDisk** コマンドレットを使用します。これにより、デバイスが再統合されて、修復プロセスが開始されます。|

## <a name="nvdimm-n-is-shown-with-a-capacity-of-0-bytes-or-as-a-generic-physical-disk"></a>NVDIMM-N が、"0" バイトの容量として表示されるか、または "Generic Physical Disk" (汎用物理ディスク) と表示される

これは、記憶域クラス メモリ デバイスが 0 バイトの容量として表示されて初期化できない状態であるか、または記憶域クラス メモリ デバイスが "汎用物理ディスク" オブジェクトとして公開されて、以下の出力例が示すように操作状態として**通信の切断**が表示される状態です。

| SerialNumber | HealthStatus | OperationalStatus | OperationalDetails |
| --- | --- | --- | --- |
|802c-01-1602-117cb5fc|正常|OK||
||警告|通信の切断||

この状態について、以下の表で説明します。

||説明|
|---|---|
|起こり得る状態|BIOS が NVDIMM-N を OS に公開しなかった|
|根本原因|NVDIMM-N デバイスは DRAM がベースとなっています。 破損している DRAM アドレスが参照されている場合、ほとんどの CPU はマシン チェックを開始して、サーバーを再起動します。 次に、一部のサーバー プラットフォームは、NVDIMM の割り当てを解除します。これにより、OS は NVDIMM にアクセスできなくなり、別のマシン チェックが実行される可能性があります。 NVDIMM-N が故障したために交換する必要があることを BIOS が検出した場合にも、これが発生する可能性があります。|
|通常の動作|NVDIMM-N は 0 バイトの容量で未初期化として表示されて、読み取りまたは書き込みは不可能です。|
|記憶域スペースの動作|(影響を受けている NVDIMM-N が 1 つだけである場合) 記憶域スペースは操作可能であり続けます。<br>NVDIMM-N PhysicalDisk オブジェクトは、正常性状態が "警告" である "汎用物理ディスク" として表示されます。|
|詳細情報|PhysicalDisk オブジェクトの OperationalStatus フィールド。 <br>EventLog – Microsoft-Windows-ScmDisk0101/Operational|
|操作|サーバー プラットフォームが NVDIMM-N デバイスをホスト OS に再び公開するように、NVDIMM-N デバイスを交換またはサニタイズする必要があります。 他の修正不可能なエラーが発生する可能性もあることから、デバイスの交換をお推めします。 代替デバイスを記憶域スペース構成に追加するには、**Add-Physicaldisk** コマンドレットを使用します。|

## <a name="nvdimm-n-is-shown-as-a-raw-or-empty-disk-after-a-reboot"></a>NVDIMM-N は、再起動後に RAW または空のディスクとして表示されます。

この状態では、記憶域クラス メモリ デバイスの正常性を確認すると、以下の出力例が示すように、正常性状態が **Unhealthy** (異常)、操作状態が **Unrecognized Metadata** (認識されないメタデータ) と表示されます。

| SerialNumber | HealthStatus | OperationalStatus | OperationalDetails |
| --- | --- | --- | --- |
|802c-01-1602-117cb5fc|正常|OK|{Unknown}|
|802c-01-1602-117cb64f|Unhealthy|{Unrecognized Metadata, Stale Metadata}|{Unknown}|

この状態について、以下の表で説明します。

||説明|
|---|---|
|起こり得る状態|バックアップ/復元エラー|
|根本原因|バックアップまたは復元手順のエラーによって、NVDIMM-N のすべてのデータが失われる可能性があります。 オペレーティング システムが読み込まれると、パーティションやファイル システムがない新しい NVDIMM-N として表示されて、RAW として表されます。すなわち、これにはファイル システムがありません。|
|通常の動作|NVDIMM-N は、読み取り専用モードになります。 再使用を開始するには、明示的なユーザー対処が必要です。|
|記憶域スペースの動作|影響を受けている NVDIMM が 1 つだけである場合は、記憶域スペースは操作可能であり続けます。<br>NVDIMM-N 物理ディスク オブジェクトは、正常性状態が "Unhealthy" (異常) と表示され、記憶域スペースで使用されることはありません。|
|詳細情報|PhysicalDisk オブジェクトの OperationalStatus フィールド。<br>EventLog – Microsoft-Windows-ScmDisk0101/Operational|
|操作|ユーザーが、影響を受けたデバイスを交換したくない場合は、**Reset-PhysicalDisk** コマンドレットを使用して、影響を受けている NVDIMM-N の読み取り専用状態を解消することができます。 記憶域スペースの環境では、これにより、記憶域スペースへの NVDIMM-N の再統合と修復プロセスの開始も試行されます。|

## <a name="interleaved-sets"></a>インターリーブ セット

多くの場合、インターリーブ セットをプラットフォームの BIOS で作成し、複数の NVDIMM-N デバイスが ホスト オペレーティング システムで単一デバイスとして認識されるようにすることができます。

Windows Server 2016 および Windows 10 Anniversary Edition では、NVDIMM-N のインターリーブ セットはサポートされません。

この記事を執筆している時点では、そのようなセットに含まれる個々の NVDIMM-N を正しく識別して、具体的にどのデバイスがエラーを引き起こした可能性があるのか、あるいは修理を必要としているのかをユーザーに明確に知らせるメカニズムはホスト オペレーティング システムにありません。


