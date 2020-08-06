---
title: 記憶域スペースダイレクトのトラブルシューティング
description: 記憶域スペースダイレクトのデプロイのトラブルシューティング方法について説明します。
ms.prod: windows-server
ms.author: ''
ms.technology: storage-spaces
ms.topic: article
author: kaushika-msft
ms.date: 10/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: ca3a1ec8462f96c1f6a018d1148b7824cdf8cc20
ms.sourcegitcommit: acfdb7b2ad283d74f526972b47c371de903d2a3d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/05/2020
ms.locfileid: "87769470"
---
# <a name="troubleshoot-storage-spaces-direct"></a>記憶域スペースダイレクトのトラブルシューティング

> 適用先:Windows Server 2019、Windows Server 2016

記憶域スペースダイレクトの展開のトラブルシューティングを行うには、次の情報を使用します。

一般に、次の手順で開始します。

1. Windows server カタログを使用して、SSD の製造元とモデルが Windows Server 2016 および Windows Server 2019 に対して認定されていることを確認します。 記憶域スペースダイレクトでドライブがサポートされていることをベンダーに確認します。
2. 記憶域に障害が発生しているドライブがないかどうかを調べます。 記憶域管理ソフトウェアを使用して、ドライブの状態を確認します。 ドライブのいずれかに問題がある場合は、ベンダーと協力してください。
3. 必要に応じて、記憶域を更新し、ファームウェアをドライブします。
   すべてのノードに最新の Windows 更新プログラムがインストールされていることを確認します。 Windows Server 2016 の最新の更新プログラムは、windows 10 および windows server [2016 の更新履歴](https://aka.ms/update2016)と、windows [10 および windows server 2019 更新](https://support.microsoft.com/help/4464619)プログラムの履歴から windows server 2019 用に入手できます。
4. ネットワークアダプターのドライバーとファームウェアを更新します。
5. クラスター検証を実行し、[記憶域スペースダイレクト] セクションを確認し、キャッシュに使用されるドライブが正しく報告され、エラーが発生していないことを確認します。

問題が解決しない場合は、以下のシナリオを確認してください。

## <a name="virtual-disk-resources-are-in-no-redundancy-state"></a>仮想ディスクリソースが冗長状態ではありません
クラッシュまたは電源障害により、記憶域スペースダイレクトシステムのノードが予期せず再起動します。 次に、1つまたは複数の仮想ディスクがオンラインにならず、"冗長な情報が不足しています" という説明が表示されます。

|FriendlyName|ResiliencySettingName| OperationalStatus| HealthStatus| IsManualAttach|サイズ| PSComputerName|
|------------|---------------------| -----------------| ------------| --------------|-----| --------------|
|Disk4| ミラー| [OK]|  Healthy| True|  10 TB|  ノード-01...|
|Disk3         |ミラー                 |[OK]                          |Healthy       |True            |10 TB | ノード-01...|
|Disk2         |ミラー                 |冗長性なし               |異常     |True            |10 TB | ノード-01...|
|Disk1         |ミラー                 |{冗長性なし、InService}  |異常     |True            |10 TB | ノード-01...|

さらに、仮想ディスクをオンラインにしようとすると、次の情報がクラスターログ (DiskRecoveryAction) に記録されます。

```
[Verbose] 00002904.00001040::YYYY/MM/DD-12:03:44.891 INFO [RES] Physical Disk <DiskName>: OnlineThread: SuGetSpace returned 0.
[Verbose] 00002904.00001040:: YYYY/MM/DD -12:03:44.891 WARN [RES] Physical Disk < DiskName>: Underlying virtual disk is in 'no redundancy' state; its volume(s) may fail to mount.
[Verbose] 00002904.00001040:: YYYY/MM/DD -12:03:44.891 ERR [RES] Physical Disk <DiskName>: Failing online due to virtual disk in 'no redundancy' state. If you would like to attempt to online the disk anyway, first set this resource's private property 'DiskRecoveryAction' to 1. We will try to bring the disk online for recovery, but even if successful, its volume(s) or CSV may be unavailable.
```

ディスクに障害が発生した場合、またはシステムが仮想ディスク上のデータにアクセスできない場合、**冗長性のない操作状態**が発生する可能性があります。 ノードのメンテナンス中にノードで再起動が行われると、この問題が発生する可能性があります。

この問題を解決するには、次の手順を実行します。

1. 影響を受けた仮想ディスクを CSV から削除します。 これにより、クラスターの "使用可能記憶域" グループにそれらが配置され、"物理ディスク" の ResourceType として表示されるようになります。

   ```powershell
   Remove-ClusterSharedVolume -name "VdiskName"
   ```
2. 使用可能な記憶域グループを所有しているノードで、冗長性のない状態にあるすべてのディスクに対して次のコマンドを実行します。 "使用可能記憶域" グループがあるノードを特定するには、次のコマンドを実行します。

   ```powershell
   Get-ClusterGroup
   ```
3. ディスクの回復操作を設定してから、ディスクを起動してください。
   ```powershell
   Get-ClusterResource "VdiskName" | Set-ClusterParameter -Name DiskRecoveryAction -Value 1
   Start-ClusterResource -Name "VdiskName"
   ```
4. 修復が自動的に開始されます。 修復が完了するまで待ちます。 中断状態になり、再び開始される可能性があります。 進行状況を監視するには:
    - **Get StorageJob**を実行して、修復の状態を監視し、いつ完了したかを確認します。
    - **VirtualDisk**を実行し、そのスペースが正常な HealthStatus を返していることを確認します。
5. 修復が完了し、仮想ディスクが正常な状態になったら、仮想ディスクのパラメーターを再び変更します。

   ```powershell
    Get-ClusterResource "VdiskName" | Set-ClusterParameter -Name DiskRecoveryAction -Value 0
   ```
6. ディスクをオフラインにし、もう一度オンラインにして、DiskRecoveryAction が有効になるようにします。

   ```powershell
   Stop-ClusterResource "VdiskName"
   Start-ClusterResource "VdiskName"
   ```
7. 影響を受けた仮想ディスクを CSV に再び追加します。

   ```powershell
   Add-ClusterSharedVolume -name "VdiskName"
   ```

**Diskrecoveryaction**は、チェックを行わずに領域ボリュームを読み取り/書き込みモードでアタッチできる上書きスイッチです。 プロパティを使用すると、ボリュームがオンラインにならない理由について診断を行うことができます。 これはメンテナンスモードによく似ていますが、障害が発生した状態のリソースで呼び出すことができます。 また、データにアクセスすることもできます。これは、"冗長性がありません" などの状況で役立つことがあります。この場合、可能なデータにアクセスしてコピーできます。 DiskRecoveryAction プロパティは、2018年2月22日、更新プログラム、KB 4077525 で追加されました。


## <a name="detached-status-in-a-cluster"></a>クラスターでのデタッチされた状態

**VirtualDisk**コマンドレットを実行すると、1つまたは複数の記憶域スペースダイレクトの仮想ディスクの OperationalStatus が切断されます。 ただし **、HealthStatus コマンドレット**によって報告されるのは、すべての物理ディスクが正常な状態であることを示しています。

**VirtualDisk**コマンドレットからの出力の例を次に示します。

|FriendlyName|  ResiliencySettingName|  OperationalStatus|   HealthStatus|  IsManualAttach|  サイズ|   PSComputerName|
|-|-|-|-|-|-|-|
|Disk4|         ミラー|                 [OK]|                  Healthy|       True|            10 TB|  ノード-01...|
|Disk3|         ミラー|                 [OK]|                  Healthy|       True|            10 TB|  ノード-01...|
|Disk2|         ミラー|                 デタッチ|            Unknown|       True|            10 TB|  ノード-01...|
|Disk1|         ミラー|                 デタッチ|            Unknown|       True|            10 TB|  ノード-01...|


さらに、ノードに次のイベントが記録される場合があります。

```
Log Name: Microsoft-Windows-StorageSpaces-Driver/Operational
Source: Microsoft-Windows-StorageSpaces-Driver
Event ID: 311
Level: Error
User: SYSTEM
Computer: Node#.contoso.local
Description: Virtual disk {GUID} requires a data integrity scan.

Data on the disk is out-of-sync and a data integrity scan is required.

To start the scan, run the following command:
Get-ScheduledTask -TaskName "Data Integrity Scan for Crash Recovery" | Start-ScheduledTask

Once you have resolved the condition listed above, you can online the disk by using the following commands in PowerShell:

Get-VirtualDisk | ?{ $_.ObjectId -Match "{GUID}" } | Get-Disk | Set-Disk -IsReadOnly $false
Get-VirtualDisk | ?{ $_.ObjectId -Match "{GUID}" } | Get-Disk | Set-Disk -IsOffline  $false
------------------------------------------------------------

Log Name: System
Source: Microsoft-Windows-ReFS
Event ID: 134
Level: Error
User: SYSTEM
Computer: Node#.contoso.local
Description: The file system was unable to write metadata to the media backing volume <VolumeId>. A write failed with status "A device which does not exist was specified." ReFS will take the volume offline. It may be mounted again automatically.
------------------------------------------------------------
Log Name: Microsoft-Windows-ReFS/Operational
Source: Microsoft-Windows-ReFS
Event ID: 5
Level: Error
User: SYSTEM
Computer: Node#.contoso.local
Description: ReFS failed to mount the volume.
Context: 0xffffbb89f53f4180
Error: A device which does not exist was specified.
Volume GUID:{00000000-0000-0000-0000-000000000000}
DeviceName:
Volume Name:
```

デタッチされた**動作状態**は、ダーティ領域追跡 (DRT) ログがいっぱいになった場合に発生する可能性があります。 記憶域スペースでは、ミラー化されたスペースに対してダーティ領域の追跡 (DRT) を使用して、電源障害が発生したときに、記憶域スペースが復元操作を再実行または元に戻して、停電やシステムが復旧したときに記憶域スペースを柔軟かつ一貫した状態に戻すことができるようにします。 DRT ログがいっぱいになった場合、DRT メタデータが同期されてフラッシュされるまで、仮想ディスクをオンラインにすることはできません。 このプロセスではフルスキャンを実行する必要がありますが、完了するまでに数時間かかることがあります。

この問題を解決するには、次の手順を実行します。
1. 影響を受けた仮想ディスクを CSV から削除します。

   ```powershell
   Remove-ClusterSharedVolume -name "VdiskName"
   ```
2. オンラインになっていないすべてのディスクで、次のコマンドを実行します。

   ```powershell
   Get-ClusterResource -Name "VdiskName" | Set-ClusterParameter DiskRunChkDsk 7
   Start-ClusterResource -Name "VdiskName"
   ```
3. デタッチされたボリュームがオンラインになっているすべてのノードで、次のコマンドを実行します。

   ```powershell
   Get-ScheduledTask -TaskName "Data Integrity Scan for Crash Recovery" | Start-ScheduledTask
   ```
   このタスクは、デタッチされたボリュームがオンラインになっているすべてのノードで開始する必要があります。 修復が自動的に開始されます。 修復が完了するまで待ちます。 中断状態になり、再び開始される可能性があります。 進行状況を監視するには:
   - **Get StorageJob**を実行して、修復の状態を監視し、いつ完了したかを確認します。
   - **VirtualDisk**を実行し、スペースが正常な HealthStatus を返していることを確認します。
     - "クラッシュ回復のデータ整合性スキャン" は、記憶域ジョブとして表示されないタスクであり、進行状況インジケーターはありません。 タスクが実行中であると表示されている場合は、実行されています。 完了すると、[完了] と表示されます。

       また、次のコマンドレットを使用すると、実行中のスケジュールタスクの状態を表示できます。
       ```powershell
       Get-ScheduledTask | ? State -eq running
       ```
4. "クラッシュ回復のデータ整合性スキャン" が完了するとすぐに、修復が完了し、仮想ディスクが正常な状態に戻り、仮想ディスクのパラメーターを変更します。

   ```powershell
   Get-ClusterResource -Name "VdiskName" | Set-ClusterParameter DiskRunChkDsk 0
   ```

5. ディスクをオフラインにし、もう一度オンラインにして、DiskRecoveryAction が有効になるようにします。

   ```powershell
   Stop-ClusterResource "VdiskName"
   Start-ClusterResource "VdiskName"
   ```

6. 影響を受けた仮想ディスクを CSV に再び追加します。

   ```powershell
   Add-ClusterSharedVolume -name "VdiskName"
   ```
   **Diskrunchkdsk 値 7**を使用して、領域ボリュームをアタッチし、パーティションを読み取り専用モードにします。 これにより、修復をトリガーすることによって、スペースを自己検出し、自己回復することができます。 修復は、マウントされると自動的に実行されます。 また、データにアクセスすることもできます。これは、コピーできるあらゆるデータにアクセスするのに役立ちます。 完全な DRT ログなどの一部のエラー状態では、スケジュールされたクラッシュ復旧タスクのデータ整合性スキャンを実行する必要があります。

**クラッシュ回復タスクのデータ整合性スキャン**は、完全なダーティリージョン追跡 (DRT) ログの同期と消去に使用されます。 このタスクの完了には数時間かかることがあります。 "クラッシュ回復のデータ整合性スキャン" は、記憶域ジョブとして表示されないタスクであり、進行状況インジケーターはありません。 タスクが実行中であると表示されている場合は、実行されています。 完了すると、完了として表示されます。 このタスクの実行中にタスクをキャンセルするか、ノードを再起動する場合、タスクは最初からやり直す必要があります。

詳細については、「[記憶域スペースダイレクトの正常性と動作状態のトラブルシューティング](storage-spaces-states.md)」を参照してください。

## <a name="event-5120-with-status_io_timeout-c00000b5"></a>STATUS_IO_TIMEOUT c00000b5 のイベント5120

> [!Important]
> **Windows Server 2016 の場合:** 修正プログラムを適用している間にこのような現象が発生する可能性を減らすために、以下のストレージメンテナンスモードの手順を使用して、2018年5月[2018 8](https://support.microsoft.com/help/4103723)日から[10 月 2018 9](https://support.microsoft.com/help/KB4462917)日にリリースされた windows server 2016 の累積的な更新プログラムがノードにインストールされている場合に、 [windows server 2016 以降の累積的な更新プログラム](https://support.microsoft.com/help/4462928)

Windows Server 2016 上のノードを再起動した後、5120年5月8日から[2018 kb 4103723](https://support.microsoft.com/help/4103723)から[10 月9日の 2018 kb](https://support.microsoft.com/help/4462917) c00000b5 にリリースされた累積的な更新プログラムを使用して、イベント STATUS_IO_TIMEOUT を受け取る場合があります。

ノードを再起動すると、イベント5120がシステムイベントログに記録され、次のいずれかのエラーコードが表示されます。

```
Event Source: Microsoft-Windows-FailoverClustering
Event ID: 5120
Description:    Cluster Shared Volume 'CSVName' ('Cluster Virtual Disk (CSVName)') has entered a paused state because of 'STATUS_IO_TIMEOUT(c00000b5)'. All I/O will temporarily be queued until a path to the volume is reestablished.

Cluster Shared Volume 'CSVName' ('Cluster Virtual Disk (CSVName)') has entered a paused state because of 'STATUS_CONNECTION_DISCONNECTED(c000020c)'. All I/O will temporarily be queued until a path to the volume is reestablished.
```

イベント5120がログに記録されると、デバッグ情報を収集するためにライブダンプが生成されます。これにより、追加の現象が発生したり、パフォーマンスに影響が生じたりする可能性があります。 ライブダンプを生成すると、短い一時停止が作成され、メモリのスナップショットを取得してダンプファイルを書き込むことができるようになります。 大量のメモリを搭載し、負荷がかかっているシステムでは、ノードがクラスターメンバーシップから削除され、次のイベント1135がログに記録される可能性があります。

```
Event source: Microsoft-Windows-FailoverClustering
Event ID: 1135
Description: Cluster node 'NODENAME'was removed from the active failover cluster membership. The Cluster service on this node may have stopped. This could also be due to the node having lost communication with other active nodes in the failover cluster. Run the Validate a Configuration wizard to check your network configuration. If the condition persists, check for hardware or software errors related to the network adapters on this node. Also check for failures in any other network components to which the node is connected such as hubs, switches, or bridges.
```

2018年5月8で導入された変更は、クラスター内 SMB ネットワークセッション記憶域スペースダイレクトの SMB 弾性ハンドルを追加するための累積的な更新プログラムである Windows Server 2016 です。 これは、一時的なネットワーク障害に対する回復性を向上させ、RoCE がネットワークの輻輳を処理する方法を改善するために行われました。 また、これらの機能強化により、SMB 接続の再接続が試行され、ノードの再起動時のタイムアウトを待機したときに、タイムアウトが大幅に増加しました。 これらの問題は、負荷がかかっているシステムに影響を与える可能性があります。 予定外のダウンタイム時には、システムがタイムアウトへの接続を待機している間、最大60秒の IO が一時停止されています。この問題を解決するには、 [2018 年10月18日の累積的な更新プログラム (Windows Server 2016 以降の](https://support.microsoft.com/help/4462928)バージョン) をインストールします。

*メモ*この更新では、CSV タイムアウトと SMB 接続タイムアウトを整合させることで、この問題を解決します。 「回避策」セクションで説明したライブダンプ生成を無効にする変更は実装されていません。

### <a name="shutdown-process-flow"></a>シャットダウンプロセスフロー:

1. VirtualDisk コマンドレットを実行し、HealthStatus の値が健全であることを確認します。
2. 次のコマンドレットを実行して、ノードをドレインします。

   ```powershell
   Suspend-ClusterNode -Drain
   ```
3. 次のコマンドレットを実行して、そのノードのディスクをストレージメンテナンスモードにします。

   ```powershell
   Get-StorageFaultDomain -type StorageScaleUnit | Where-Object {$_.FriendlyName -eq "<NodeName>"} | Enable-StorageMaintenanceMode
   ```
4. **Get PhysicalDisk**コマンドレットを実行し、OperationalStatus 値がメンテナンスモードであることを確認します。
5. コンピューターの**再**起動コマンドレットを実行して、ノードを再起動します。
6. ノードが再起動した後、次のコマンドレットを実行して、そのノードのディスクをストレージメンテナンスモードから削除します。

   ```powershell
   Get-StorageFaultDomain -type StorageScaleUnit | Where-Object {$_.FriendlyName -eq "<NodeName>"} | Disable-StorageMaintenanceMode
   ```
7. 次のコマンドレットを実行して、ノードを再開します。

   ```powershell
   Resume-ClusterNode
   ```
8. 次のコマンドレットを実行して、再同期ジョブの状態を確認します。

   ```powershell
   Get-StorageJob
   ```

### <a name="disabling-live-dumps"></a>ライブダンプの無効化
メモリが多数あり、ストレスがかかっているシステムでのライブダンプ生成の影響を軽減するために、ライブダンプ生成を無効にすることもできます。 次の3つのオプションがあります。

>[!Caution]
>この手順を実行すると、この問題の調査に必要な Microsoft サポート診断情報が収集されなくなる可能性があります。 サポートエージェントは、特定のトラブルシューティングシナリオに基づいて、ライブダンプ生成を再度有効にするように要求することがあります。

ライブダンプを無効にするには、次に示す2つの方法があります。

#### <a name="method-1-recommended-in-this-scenario"></a>方法 1 (このシナリオで推奨)
ライブダンプシステム全体を含め、すべてのダンプを完全に無効にするには、次の手順を実行します。

1. 次のレジストリキーを作成します: HKLM\System\CurrentControlSet\Control\CrashControl\ForceDumpsDisabled
2. 新しい**ForceDumpsDisabled**キーの下に、"GuardedHost" として REG_DWORD プロパティを作成し、その値を0x10000000 に設定します。
3. 各クラスターノードに新しいレジストリキーを適用します。

>[!NOTE]
>N の変更を有効にするには、コンピューターを再起動する必要があります。

このレジストリキーが設定されると、ライブダンプの作成は失敗し、"STATUS_NOT_SUPPORTED" エラーが生成されます。

#### <a name="method-2"></a>方法 2
既定では、Windows エラー報告では、レポートの種類ごとに7日につき1つの LiveDump のみが許可されます。また、コンピューターあたりの LiveDump は、5日につき1つだけです。 これを変更するには、次のレジストリキーを設定します。これにより、コンピューター上の LiveDump を無期限に許可することができます。
```
reg add "HKLM\Software\Microsoft\Windows\Windows Error Reporting\FullLiveKernelReports" /v SystemThrottleThreshold /t REG_DWORD /d 0xFFFFFFFF /f
```
```
reg add "HKLM\Software\Microsoft\Windows\Windows Error Reporting\FullLiveKernelReports" /v ComponentThrottleThreshold /t REG_DWORD /d 0xFFFFFFFF /f
```

*メモ*変更を有効にするには、コンピューターを再起動する必要があります。

### <a name="method-3"></a>方法3
ライブダンプのクラスター生成を無効にするには (イベント5120がログに記録されたときなど)、次のコマンドレットを実行します。

```powershell
(Get-Cluster).DumpPolicy = ((Get-Cluster).DumpPolicy -band 0xFFFFFFFFFFFFFFFE)
```
このコマンドレットは、コンピューターを再起動しなくても、すべてのクラスターノードに直ちに影響します。

## <a name="slow-io-performance"></a>低速 IO パフォーマンス

IO パフォーマンスの低下が見られる場合は、記憶域スペースダイレクト構成でキャッシュが有効になっているかどうかを確認してください。

確認するには、次の2つの方法があります。


1. クラスターログを使用します。 任意のテキストエディターでクラスターログを開き、"[= = = SBL Disks = = =]" を検索します。 これは、ログが生成されたノード上のディスクの一覧になります。

     キャッシュが有効なディスクの例: この状態は Cachediskstateinitializer Edandbound であり、ここには GUID があることに注意してください。

   ```
   [=== SBL Disks ===]
    {26e2e40f-a243-1196-49e3-8522f987df76},3,false,true,1,48,{1ff348f1-d10d-7a1a-d781-4734f4440481},CacheDiskStateInitializedAndBound,1,8087,54,false,false,HGST    ,HUH721010AL4200 ,        7PG3N2ER,A21D,{d5e27a3b-42fb-410a-81c6-9d8cc12da20c},[R/M 0 R/U 0 R/T 0 W/M 0 W/U 0 W/T 0],
    ```

    キャッシュが有効になっていません: ここでは、GUID が存在せず、状態が CacheDiskStateNonHybrid であることがわかります。
    ```
   [=== SBL Disks ===]
    {426f7f04-e975-fc9d-28fd-72a32f811b7d},12,false,true,1,24,{00000000-0000-0000-0000-000000000000},CacheDiskStateNonHybrid,0,0,0,false,false,HGST    ,HUH721010AL4200 ,        7PGXXG6C,A21D,{d5e27a3b-42fb-410a-81c6-9d8cc12da20c},[R/M 0 R/U 0 R/T 0 W/M 0 W/U 0 W/T 0],
    ```

    キャッシュが有効になっていない: すべてのディスクが同じ種類の場合、既定では有効になりません。 ここで、GUID が存在せず、状態が CacheDiskStateIneligibleDataPartition であることがわかります。
    ```
    {d543f90c-798b-d2fe-7f0a-cb226c77eeed},10,false,false,1,20,{00000000-0000-0000-0000-000000000000},CacheDiskStateIneligibleDataPartition,0,0,0,false,false,NVMe    ,INTEL SSDPE7KX02,  PHLF7330004V2P0LGN,0170,{79b4d631-976f-4c94-a783-df950389fd38},[R/M 0 R/U 0 R/T 0 W/M 0 W/U 0 W/T 0],
    ```
2. SDDCDiagnosticInfo からの Get-PhysicalDisk.xml の使用
    1. "$D = Export-clixml GetPhysicalDisk.XML" を使用して XML ファイルを開きます。
    2. "Ipmo ストレージ" の実行
    3. "$d" を実行します。 使用法は自動選択であり、Journal ではなく、次のような出力が表示されることに注意してください。

   |FriendlyName|  SerialNumber| MediaType| CanPool| OperationalStatus| HealthStatus| 使用法| サイズ|
   |-----------|------------|---------| -------| -----------------| ------------| -----| ----|
   |NVMe INTEL SSDPE7KX02| PHLF733000372P0LGN| SSD| False|   [OK]|                Healthy|      1.82 TB を自動選択|
   |NVMe INTEL SSDPE7KX02 |PHLF7504008J2P0LGN| SSD|  False|    [OK]|                Healthy| 自動選択| 1.82 TB|
   |NVMe INTEL SSDPE7KX02| PHLF7504005F2P0LGN| SSD|  False|  [OK]|                Healthy| 自動選択| 1.82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF7504002A2P0LGN| SSD| False| [OK]|    Healthy| 自動選択| 1.82 TB|
   |NVMe INTEL SSDPE7KX02| PHLF7504004T2P0LGN |SSD| False|[OK]|       Healthy| 自動選択| 1.82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF7504002E2P0LGN| SSD| False| [OK]|      Healthy| 自動選択| 1.82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF7330002Z2P0LGN| SSD| False| [OK]|      Healthy|自動選択| 1.82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF733000272P0LGN |SSD| False| [OK]|  Healthy| 自動選択| 1.82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF7330001J2P0LGN |SSD| False| [OK]| Healthy| 自動選択| 1.82 TB|
   |NVMe INTEL SSDPE7KX02| PHLF733000302P0LGN |SSD| False| [OK]|Healthy| 自動選択| 1.82 TB|
   |NVMe INTEL SSDPE7KX02| PHLF7330004D2P0LGN |SSD| False| [OK]| Healthy| 自動選択 |1.82 TB|

## <a name="how-to-destroy-an-existing-cluster-so-you-can-use-the-same-disks-again"></a>同じディスクを再び使用できるように既存のクラスターを破棄する方法

記憶域スペースダイレクトクラスターでは、記憶域スペースダイレクトを無効にして[クリーンドライブ](deploy-storage-spaces-direct.md#step-31-clean-drives)に記載されているクリーンアッププロセスを使用すると、クラスター化された記憶域プールは依然としてオフライン状態のままで、ヘルスサービスはクラスターから削除されます。

次の手順では、ファントム記憶域プールを削除します。
   ```powershell
   Get-ClusterResource -Name "Cluster Pool 1" | Remove-ClusterResource
   ```

これで、いずれかのノードで**Get-PhysicalDisk**を実行すると、プール内にあったすべてのディスクが表示されます。 たとえば、4つの SAS ディスクを搭載した4ノードクラスターを備えたラボでは、各ノードに 100 GB が表示されます。 この場合、記憶域スペースダイレクトを無効にすると、SBL (記憶域バスレイヤー) が削除されますが、フィルターは解除されます。この場合、 **Get PhysicalDisk**を実行すると、ローカル OS ディスクを除く4つのディスクを報告する必要があります。 代わりに、16を報告しました。 これは、クラスター内のすべてのノードで同じです。 **Get Disk**コマンドを実行すると、次のサンプル出力に示すように、ローカルに接続されているディスクの番号が0、1、2などになります。

|Number| フレンドリ名| シリアル番号|HealthStatus|OperationalStatus|総サイズ| パーティションの形式|
|-|-|-|-|-|-|-|-|
|0|Msft Virtu...  ||Healthy | オンライン|  127 GB| GPT|
||Msft Virtu... ||Healthy| オフライン| 100 GB| RAW|
||Msft Virtu... ||Healthy| オフライン| 100 GB| RAW|
||Msft Virtu... ||Healthy| オフライン| 100 GB| RAW|
||Msft Virtu... ||Healthy| オフライン| 100 GB| RAW|
|1|Msft Virtu...||Healthy| オフライン| 100 GB| RAW|
||Msft Virtu... ||Healthy| オフライン| 100 GB| RAW|
|2|Msft Virtu...||Healthy| オフライン| 100 GB| RAW|
||Msft Virtu... ||Healthy| オフライン| 100 GB| RAW|
||Msft Virtu... ||Healthy| オフライン| 100 GB| RAW|
||Msft Virtu... ||Healthy| オフライン| 100 GB| RAW|
||Msft Virtu... ||Healthy| オフライン| 100 GB| RAW|
|4|Msft Virtu...||Healthy| オフライン| 100 GB| RAW|
|3|Msft Virtu...||Healthy| オフライン| 100 GB| RAW|
||Msft Virtu... ||Healthy| オフライン| 100 GB| RAW|
||Msft Virtu... ||Healthy| オフライン| 100 GB| RAW|
||Msft Virtu... ||Healthy| オフライン| 100 GB| RAW|

## <a name="error-message-about-unsupported-media-type-when-you-create-an-storage-spaces-direct-cluster-using-enable-clusters2d"></a>Enable-clusters2d を使用して記憶域スペースダイレクトクラスターを作成するときの "サポートされていないメディアの種類" に関するエラーメッセージ

**Enable-clusters2d**コマンドレットを実行すると、次のようなエラーが表示されることがあります。

![シナリオ6のエラーメッセージ](media/troubleshooting/scenario-error-message.png)

この問題を解決するには、hba アダプターが HBA モードで構成されていることを確認します。 RAID モードで構成する必要がある HBA はありません。

## <a name="enable-clusterstoragespacesdirect-hangs-at-waiting-until-sbl-disks-are-surfaced-or-at-27"></a>"SBL ディスクが表示されるまでの待機中" または27% で ClusterStorageSpacesDirect がハングする

検証レポートには、次の情報が表示されます。

`<identifier>`ノードに接続されたディスク `<nodename>` が SCSI ポートの関連付けを返しましたが、対応するエンクロージャデバイスが見つかりませんでした。 ハードウェアが記憶域スペースダイレクト (S2D) と互換性がない場合は、ハードウェアの製造元に問い合わせて、SCSI エンクロージャサービス (SES) のサポートを確認してください。

この問題は、ディスクと HBA カードの間にある HPE SAS エクスパンダーカードを使用しています。 SAS エクスパンダーは、エキスパンダーに接続されている最初のドライブとエキスパンダー自体の間に重複する ID を作成します。  これは[Hpe Smart Array CONTROLLER SAS エクスパンダーファームウェア: 4.02](https://support.hpe.com/hpsc/swd/public/detail?sp4ts.oid=7304566&swItemId=MTX_ef8d0bf4006542e194854eea6a&swEnvOid=4184#tab3)で解決されました。

## <a name="intel-ssd-dc-p4600-series-has-a-non-unique-nguid"></a>Intel SSD DC P4600 シリーズには一意ではない n があります。
Intel SSD DC P4600 シリーズデバイスが、次の例のように、0100000001000000E4D25C000014E214 や0100000001000000E4D25C0000EEE214 などの複数の名前空間について、同様の16バイトを報告していると思われる問題が発生する可能性があります。


|               uniqueid               | deviceid | MediaType | BusType |               serialnumber               |      size      | canpool | フレンドリ | OperationalStatus |
|--------------------------------------|----------|-----------|---------|------------------------------------------|----------------|---------|--------------|-------------------|
|           5000CCA251D12E30           |    0     |    HDD    |   SAS   |                 7PKR197G                 | 10000831348736 |  False  |     HGST     |  HUH721010AL4200  |
| 0100000001000000E4D25C000014E214 |    4     |    SSD    |  NVMe   | 0100_0000_0100_0000_E4D2_5C00_0014_E214。 | 1600321314816  |  True   |    INTEL     |   SSDPE2KE016T7   |
| 0100000001000000E4D25C000014E214 |    5     |    SSD    |  NVMe   | 0100_0000_0100_0000_E4D2_5C00_0014_E214。 | 1600321314816  |  True   |    INTEL     |   SSDPE2KE016T7   |
| 0100000001000000E4D25C0000EEE214 |    6     |    SSD    |  NVMe   | 0100_0000_0100_0000_E4D2_5C00_00EE_E214。 | 1600321314816  |  True   |    INTEL     |   SSDPE2KE016T7   |
| 0100000001000000E4D25C0000EEE214 |    7     |    SSD    |  NVMe   | 0100_0000_0100_0000_E4D2_5C00_00EE_E214。 | 1600321314816  |  True   |    INTEL     |   SSDPE2KE016T7   |

この問題を解決するには、Intel ドライブのファームウェアを最新バージョンに更新します。  2018年5月のファームウェアバージョン QDV101B1 は、この問題を解決することがわかっています。

[INTEL Ssd Data Center ツールの2018年5月リリース](https://downloadmirror.intel.com/27778/eng/Intel_SSD_Data_Center_Tool_3_0_12_Release_Notes_330715-026.pdf)には、INTEL Ssd DC P4600 シリーズ用のファームウェア更新プログラム QDV101B1 が含まれています。


## <a name="physical-disk-healthy-and-operational-status-is-removing-from-pool"></a>物理ディスクは "正常" で、動作状態は "プールから削除しています"

Windows Server 2016 記憶域スペースダイレクトクラスターでは、1つ以上の物理ディスクの HealthStatus が "健全" と表示されることがあります。一方、OperationalStatus は "(プールから削除, OK)" です。

"プールからの削除" は、 **remove-PhysicalDisk**が呼び出されて状態を維持するために正常性に格納され、削除操作が失敗した場合に回復を許可する場合に設定されます。 次のいずれかの方法を使用して、OperationalStatus を手動で健全に変更できます。

- 物理ディスクをプールから削除してから、もう一度追加してください。
- [Clear-PhysicalDiskHealthData.ps1 スクリプト](https://go.microsoft.com/fwlink/?linkid=2034205)を実行して目的をクリアします。 (としてダウンロードできます。TXT ファイル。 これをとして保存する必要があります。PS1 ファイルを実行する前に実行してください)。

スクリプトの実行方法を示すいくつかの例を次に示します。

- "健全" に設定する必要があるディスクを指定するには、[**シリアル**状態のパラメーターを使用します。 シリアル番号は、 **WMI MSFT_PhysicalDisk**または **-PhysicalDisk**から取得できます。 (以下のシリアル番号には0を使用しています)。

   ```powershell
   Clear-PhysicalDiskHealthData -Intent -Policy -SerialNumber 000000000000000 -Verbose -Force
    ```

- **UniqueId**パラメーターを使用して、ディスクを指定します ( **WMI MSFT_PhysicalDisk**または**get-help**)。

   ```powershell
   Clear-PhysicalDiskHealthData -Intent -Policy -UniqueId 00000000000000000 -Verbose -Force
   ```

## <a name="file-copy-is-slow"></a>ファイルのコピー速度が遅い

ファイルエクスプローラーを使用して大きな VHD を仮想ディスクにコピーするときに問題が発生することがあります。ファイルのコピーに予想以上に時間がかかっています。

ファイルエクスプローラー、Robocopy、または Xcopy を使用して大規模な VHD を仮想ディスクにコピーすることは、予想されるパフォーマンスよりも低速になるため、では推奨されません。 コピープロセスは、ストレージスタックの下位にある記憶域スペースダイレクトスタックを経由せず、代わりにローカルコピープロセスとして機能します。

記憶域スペースダイレクトのパフォーマンスをテストする場合は、VMFleet と Diskspd を使用してサーバーを読み込んでストレステストを行ってベースラインを取得し、記憶域スペースダイレクトパフォーマンスの期待値を設定することをお勧めします。

## <a name="expected-events-that-you-would-see-on-rest-of-the-nodes-during-the-reboot-of-a-node"></a>ノードの再起動中に、残りのノードに表示されるイベントが想定されています。

これらのイベントを無視しても安全です。

```
Event ID 205: Windows lost communication with physical disk {XXXXXXXXXXXXXXXXXXXX }. This can occur if a cable failed or was disconnected, or if the disk itself failed.

Event ID 203: Windows lost communication with physical disk {xxxxxxxxxxxxxxxxxxxxxxxx }. This can occur if a cable failed or was disconnected, or if the disk itself failed.
```

Azure Vm を実行している場合は、このイベントを無視してもかまいません。`Event ID 32: The driver detected that the device \Device\Harddisk5\DR5 has its write cache enabled. Data corruption may occur.`

## <a name="slow-performance-or-lost-communication-io-error-detached-or-no-redundancy-errors-for-deployments-that-use-intel-p3x00-nvme-devices"></a>Intel P3x00 NVMe デバイスを使用する展開で、パフォーマンスが低下したり、"通信が失われました"、"IO エラー"、"切断されました"、"冗長性がありません" エラーが発生する

ここでは、"メンテナンスリリース 8" の前に、ファームウェアのバージョンが含まれている NVM Express (NVMe) デバイスの Intel P3x00 ファミリに基づいてハードウェアを使用している一部の記憶域スペースダイレクトユーザーに影響する重大な問題を特定しました。

>[!NOTE]
> 個々の Oem は、固有のファームウェアバージョン文字列を使用して、Intel P3x00 ファミリの NVMe デバイスをベースとするデバイスを持つことができます。 最新のファームウェアバージョンの詳細については、OEM にお問い合わせください。

デバイスの Intel P3x00 ファミリに基づくハードウェアを展開で使用している場合は、すぐに利用可能な最新のファームウェアを適用することをお勧めします (少なくともメンテナンスリリース 8)。 この[Microsoft サポートの記事](https://support.microsoft.com/help/4052341/slow-performance-or-lost-communication-io-error-detached-or-no-redunda)では、この問題に関する追加情報を提供します。
