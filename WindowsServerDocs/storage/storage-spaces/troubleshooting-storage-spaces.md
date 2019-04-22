---
title: 記憶域スペース ダイレクトのトラブルシューティング
description: 記憶域スペース ダイレクト展開のトラブルシューティングを行う方法について説明します。
keywords: 記憶域スペース
ms.prod: windows-server-threshold
ms.author: ''
ms.technology: storage-spaces
ms.topic: article
author: kaushika-msft
ms.date: 10/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: ecf3cb5703a90976dce15abbd0c9fdd1d4aa24ec
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812633"
---
# <a name="troubleshoot-storage-spaces-direct"></a>直接記憶域スペースをトラブルシューティングします。

記憶域スペース ダイレクト展開のトラブルシューティングを行うには、次の情報を使用します。

一般に、次の手順を開始します。

1. SSD の型/モデルは、Windows Server カタログを使用して Windows Server 2016 の認定を確認します。 仕入先でドライブが記憶域スペース ダイレクトのサポートされていることを確認します。
2. 障害のある、すべてのドライブのストレージを検査します。 記憶域の管理ソフトウェアを使用して、ドライブの状態を確認します。 障害のある、ベンダーと連携して、ドライブの場合は。 
3. 記憶域を更新し、必要に応じて、ドライブのファームウェアします。
   最新の Windows 更新プログラムがすべてのノードにインストールされていることを確認します。 Windows Server 2016 の最新の更新プログラムを取得できる[ https://aka.ms/update2016](https://aka.ms/update2016)します。
4. ネットワーク アダプターのドライバーとファームウェアを更新します。
5. クラスター検証を実行し、記憶域スペース ダイレクトのセクションを確認して、キャッシュに使用されるドライブが正しく報告されることを確認し、エラーはありません。

問題がまだあるを場合は、以下のシナリオを確認します。

## <a name="virtual-disk-resources-are-in-no-redundancy-state"></a>仮想ディスク リソースが No 冗長性の状態
記憶域スペース ダイレクトのシステムのノードは再起動が予期せずクラッシュや電源障害が原因です。 次に、1 つまたは複数の仮想ディスクをオンラインにならない場合があり、「冗長性を情報が不足しています。」の説明を参照してください。
    
|FriendlyName|ResiliencySettingName| OperationalStatus| HealthStatus| IsManualAttach|サイズ| PSComputerName|
|------------|---------------------| -----------------| ------------| --------------|-----| --------------|
|Disk4| Mirror (ミラー)| OK|  正常| True|  10 TB|  ノード 01.conto.|
|Disk3         |Mirror (ミラー)                 |OK                          |正常       |True            |10 TB | ノード 01.conto.|
|Disk2         |Mirror (ミラー)                 |非冗長               |Unhealthy     |True            |10 TB | ノード 01.conto.|
|Disk1         |Mirror (ミラー)                 |{冗長性なし、InService}  |Unhealthy     |True            |10 TB | ノード 01.conto.| 

さらに、仮想ディスクをオンラインにすると、次の情報が (DiskRecoveryAction) クラスターのログに記録されます。  

```
[Verbose] 00002904.00001040::YYYY/MM/DD-12:03:44.891 INFO [RES] Physical Disk <DiskName>: OnlineThread: SuGetSpace returned 0.
[Verbose] 00002904.00001040:: YYYY/MM/DD -12:03:44.891 WARN [RES] Physical Disk < DiskName>: Underlying virtual disk is in 'no redundancy' state; its volume(s) may fail to mount.
[Verbose] 00002904.00001040:: YYYY/MM/DD -12:03:44.891 ERR [RES] Physical Disk <DiskName>: Failing online due to virtual disk in 'no redundancy' state. If you would like to attempt to online the disk anyway, first set this resource's private property 'DiskRecoveryAction' to 1. We will try to bring the disk online for recovery, but even if successful, its volume(s) or CSV may be unavailable. 
``` 

**いいえ冗長性の動作状態**ディスクが失敗するか、システムが仮想ディスクのデータにアクセスできない場合に発生することができます。 この問題は、ノードのメンテナンス中にノードの再起動が発生した場合に発生することができます。
    
この問題を解決するには、次の手順を実行します。

1. CSV から影響を受けた仮想ディスクを削除します。 クラスター内の「使用可能記憶域」グループに配置され、「物理ディスク」のリソースの種類として表示を開始

   ```powershell
   Remove-ClusterSharedVolume -name "VdiskName"
   ``` 
2. No 冗長性状態にあるすべてのディスク上の次のコマンドの実行、使用可能記憶域グループを所有しているノード。 ノードを「使用可能記憶域」グループを識別するためには、次のコマンドを実行できます。

   ```powershell
   Get-ClusterGroup
   ```
3. ディスクの復旧アクションを設定し、ディスクを開始します。
   ```powershell
   Get-ClusterResource "VdiskName" | Set-ClusterParameter -Name DiskRecoveryAction -Value 1
   Start-ClusterResource -Name "VdiskName"
   ```
4. 修復が自動的に開始する必要があります。 修復を完了するまで待ちます。 中断状態に移動して、もう一度開始し、可能性があります。 進行状況を監視します。 
    - 実行**Get-storagejob**が完了したときに表示して、修復の状態を監視します。
    - 実行**Get-virtualdisk** HealthStatus の正常性の領域を返すことを確認します。
5. 修復後が完了し、仮想ディスクは、正常では、仮想ディスク パラメーター戻すです。

   ```powershell
    Get-ClusterResource "VdiskName" | Set-ClusterParameter -Name DiskRecoveryAction -Value 0
   ```
6. オフラインにしてから、DiskRecoveryAction を有効にするためにもう一度オンライン ディスクを実行します。

   ```powershell
   Stop-ClusterResource "VdiskName"
   Start-ClusterResource "VdiskName"
   ``` 
7. 影響を受けた仮想ディスクを CSV に追加します。

   ```powershell
   Add-ClusterSharedVolume -name "VdiskName"
   ```

**DiskRecoveryAction**チェックなしの読み取り/書き込みモードでの領域のボリュームをアタッチできるようにするスイッチで上書きします。 プロパティを使用すると、ボリュームがオンラインにしない理由に診断を行うことができます。 メンテナンス モードに非常に似ていますが、失敗状態のリソースを呼び出すことができます。 "No 冗長性など、"アクセスを見いだすことのできる状況で役に立ちますデータにアクセスすることもできますなデータをでき、それをコピーします。 DiskRecoveryAction プロパティは、2018 年 2 月 22日の更新プログラム、KB 4077525 で追加されました。
    
    
## <a name="detached-status-in-a-cluster"></a>クラスターでのデタッチの状態 

実行すると、 **Get-virtualdisk**コマンドレットでは、1 つまたは複数記憶域スペース ダイレクト仮想ディスクをデタッチ OperationalStatus します。 ただし、によって報告されます、HealthStatus、 **Get-physicaldisk**コマンドレットは、すべての物理ディスクが正常な状態でいることを示します。

出力の例を次に、 **Get-virtualdisk**コマンドレット。

|FriendlyName|  ResiliencySettingName|  OperationalStatus|   HealthStatus|  IsManualAttach|  サイズ|   PSComputerName|
|-|-|-|-|-|-|-|
|Disk4|         Mirror (ミラー)|                 OK|                  正常|       True|            10 TB|  ノード 01.conto.|
|Disk3|         Mirror (ミラー)|                 OK|                  正常|       True|            10 TB|  ノード 01.conto.|
|Disk2|         Mirror (ミラー)|                 Detached|            Unknown|       True|            10 TB|  ノード 01.conto.|
|Disk1|         Mirror (ミラー)|                 Detached|            Unknown|       True|            10 TB|  ノード 01.conto.| 


さらに、ノードで、次のイベントが記録されます。

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

**デタッチの動作状態**ダーティ領域 (DRT) の追跡ログがいっぱいの場合に発生することができます。 記憶域スペース (DRT) の追跡をミラー化されたスペースをダーティ領域を使用して、電源障害が発生したときに、記憶域スペースが再実行または記憶域スペースを柔軟に戻す操作を元に戻すことができるかどうかを確認する実行中の更新メタデータを記録するかどうかを確認するには電源を復旧すると、一貫性のある状態と、システムが再び起動します。 DRT ログがいっぱいで、DRT メタデータが同期フラッシュされるまで、仮想ディスクがオンラインにできません。 このプロセスでは、完了に数時間かかる場合、フル スキャンを実行している必要があります。
    
この問題を解決するには、次の手順を実行します。
1. CSV から影響を受けた仮想ディスクを削除します。

   ```powershell
   Remove-ClusterSharedVolume -name "VdiskName"
   ``` 
2. オンラインではないすべてのディスク上には、次のコマンドを実行します。 

   ```powershell
   Get-ClusterResource -Name "VdiskName" | Set-ClusterParameter DiskRunChkDsk 7
   Start-ClusterResource -Name "VdiskName"
   ``` 
3. デタッチされたボリュームがオンラインであるすべてのノードで、次のコマンドを実行します。 

   ```powershell
   Get-ScheduledTask -TaskName "Data Integrity Scan for Crash Recovery" | Start-ScheduledTask 
   ```
   このタスクは、デタッチされたボリュームがオンラインのすべてのノードで開始する必要があります。 修復が自動的に開始する必要があります。 修復を完了するまで待ちます。 中断状態に移動して、もう一度開始し、可能性があります。 進行状況を監視します。 
   - 実行**Get-storagejob**が完了したときに表示して、修復の状態を監視します。
   -  実行**Get-virtualdisk**し、領域を返します HealthStatus の正常性を確認します。
    - 「データ整合性スキャンのクラッシュ回復」が、記憶域ジョブとして表示しないタスクと進行状況のインジケーターはありません。 タスクが表示されている場合、実行中として実行しています。 完了すると、完了したが表示されます。
    
       さらに、次のコマンドレットを使用して、実行中のスケジュール タスクの状態を表示できます。 
       ```powershell
       Get-ScheduledTask | ? State -eq running
       ``` 
4. 「データ整合性スキャンのクラッシュ復旧」を完了するとすぐに修復が完了して、仮想ディスクは、正常、仮想ディスク パラメーター戻すには。 

   ```powershell
   Get-ClusterResource -Name "VdiskName" | Set-ClusterParameter DiskRunChkDsk 0 
   ```
5. 影響を受けた仮想ディスクを CSV に追加します。    

   ```powershell
   Add-ClusterSharedVolume -name "VdiskName"
   ```  
**DiskRunChkdsk 値 7**領域ボリュームをアタッチし、読み取り専用モードでは、パーティションを保持するために使用します。 修復をトリガーすることによって空白を自己検出と自動修復ができるようにします。 修復の実行は 1 回自動的にマウントします。 また、任意のデータをコピーすることができますにアクセスすることができるデータにアクセスすることもできます。 完全な DRT ログなどのいくつかのエラー状態のクラッシュ回復のスケジュールされたタスクに対してデータ整合性スキャンを実行する必要があります。
    
**クラッシュ回復のタスクのデータ整合性スキャン**を同期し、完全なダーティ領域 (DRT) の追跡のログを消去するために使用します。 このタスクは完了に数時間をかかります。 「データ整合性スキャンのクラッシュ回復」が、記憶域ジョブとして表示しないタスクと進行状況のインジケーターはありません。 タスクが表示されている場合、実行中として実行しています。 完了すると、完了済みとして表示されます。 タスクをキャンセルするか、またはこのタスクの実行中にノードを再起動する場合、タスクは、最初からやり直す必要があります。

詳細については、次を参照してください。[記憶域スペース ダイレクトのトラブルシューティングの正常性と操作状態](storage-spaces-states.md)します。
    
## <a name="event-5120-with-statusiotimeout-c00000b5"></a>イベント 5120 STATUS_IO_TIMEOUT c00000b5 を 

>[!重要な} 以下の記憶域メンテナンス モードの手順を使用してインストールする修正プログラムと更新プログラムの適用中にこれらの現象が発生している可能性を減らすためには、推奨は、 [2018 年 10 月 18 日、Windows Server 2016 用の累積更新プログラム](https://support.microsoft.com/help/4462928)以降のバージョンを使用しているノードは現在からリリースされた Windows Server 2016 累積的な更新をインストールしているときに[2018 年 5 月 8 日](https://support.microsoft.com/help/4103723)に[、2018 年 10 月 9 日](https://support.microsoft.com/help/KB4462917)します。

リリースされた累積更新プログラムには、Windows Server 2016 でノードを再起動した後は、イベント 5120 STATUS_IO_TIMEOUT c00000b5 を得られる[2018 年 5 月 8 日 KB 4103723](https://support.microsoft.com/help/4103723)に[2018 年 10 月 9 日 KB 4462917](https://support.microsoft.com/help/4462917)をインストールします。

ノードを再起動すると、イベント 5120 は、システム イベント ログに記録され、次のエラー コードのいずれかが含まれています。

```
Event Source: Microsoft-Windows-FailoverClustering
Event ID: 5120
Description:    Cluster Shared Volume 'CSVName' ('Cluster Virtual Disk (CSVName)') has entered a paused state because of 'STATUS_IO_TIMEOUT(c00000b5)'. All I/O will temporarily be queued until a path to the volume is reestablished. 

Cluster Shared Volume ‘CSVName’ ('Cluster Virtual Disk (CSVName)') has entered a paused state because of 'STATUS_CONNECTION_DISCONNECTED(c000020c)'. All I/O will temporarily be queued until a path to the volume is reestablished.    
```

イベント、5120 がログに記録すると、その他の現象が発生する可能性があります、またはパフォーマンスに影響があるデバッグ情報を収集するライブのダンプが生成されます。 ライブのダンプを生成するには、メモリ ダンプ ファイルを書き込むためのスナップショットを作成を有効にする簡単な一時停止が作成されます。 システムに大量のメモリがある、ストレス条件下で、クラスター メンバーシップから外れますしてもログに記録される次のイベント 1135 ノードがあります。

```
Event source: Microsoft-Windows-FailoverClustering
Event ID: 1135  
Description: Cluster node 'NODENAME'was removed from the active failover cluster membership. The Cluster service on this node may have stopped. This could also be due to the node having lost communication with other active nodes in the failover cluster. Run the Validate a Configuration wizard to check your network configuration. If the condition persists, check for hardware or software errors related to the network adapters on this node. Also check for failures in any other network components to which the node is connected such as hubs, switches, or bridges.
```

変更は、記憶域スペース ダイレクト クラスター内の SMB ネットワーク セッションの SMB の回復力のある処理を追加する、2018 年 5 月 8 日の累積的な更新で導入されました。 これは、一時的なネットワーク障害に対する回復力と RoCE でのネットワークの輻輳の処理方法向上のために行われました。

ノードを再起動するとに、SMB 接続が再接続するときのタイムアウトとタイムアウトを待機これらの機能強化も誤って増加します。 これらの問題がストレス条件下でシステムに影響を与えることができます。 計画外のダウンタイム中に最大 60 秒間の IO の一時停止も観測されましたシステムが待機するタイムアウトへの接続中。

この問題を解決するには、インストール、 [2018 年 10 月 18 日、Windows Server 2016 用の累積更新プログラム](https://support.microsoft.com/help/4462928)以降のバージョン。

*注*この更新プログラムは、CSV のタイムアウトとこの問題を解決する SMB 接続のタイムアウトを揃えて配置します。 回避策」セクションで説明されているライブのダンプの生成を無効にする変更は実装しません。
    
### <a name="shutdown-process-flow"></a>シャット ダウン プロセス フロー:

1. Get-virtualdisk コマンドレットを実行し、HealthStatus 値が"健全"であるかどうかを確認します。
2. 次のコマンドレットを実行して、ノード ドレインを実行します。

   ```powershell
   Suspend-ClusterNode -Drain
   ```
3. 次のコマンドレットを実行して、記憶域メンテナンス モードでは、そのノードでディスクを配置します。 

   ```powershell
   Get-StorageFaultDomain -type StorageScaleUnit | Where-Object {$_.FriendlyName -eq "<NodeName>"} | Enable-StorageMaintenanceMode
   ```
4. 実行、 **Get-physicaldisk**コマンドレット、OperationalStatus 値がメンテナンス モードであるかどうかを確認します。
5. 実行、 **Restart-computer**コマンドレットをノードを再起動します。
6. ノードを再起動した後は、次のコマンドレットを実行して記憶域メンテナンス モードからそのノード上のディスクを削除します。

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

### <a name="disabling-live-dumps"></a>ライブのダンプを無効にします。
システムで大量のメモリがあり、ストレス条件下ではライブのダンプ生成の影響を軽減するためにさらにライブ ダンプの生成を無効にする可能性があります。 3 つのオプションを以下に示します。

>[!Caution]
>この手順では、Microsoft サポートは、この問題を調査する必要がある診断情報のコレクションを防ぐことができます。 サポート担当者は、特定のトラブルシューティング シナリオに基づくライブのダンプの生成を再度有効にするよう要求する必要があります。

以下に示すようには、ライブのダンプを無効にする 2 つの方法があります。

#### <a name="method-1-recommended-in-this-scenario"></a>メソッドの 1 (このシナリオで推奨)
ライブのダンプをシステム全体を含む、すべてのダンプを完全に無効にするには、次の手順に従います。

1. 次のレジストリ キーを作成します。HKLM\System\CurrentControlSet\Control\CrashControl\ForceDumpsDisabled
2. 新しい  **ForceDumpsDisabled**キー、GuardedHost、として REG_DWORD プロパティを作成および 0x10000000 にその値を設定します。
3. 各クラスター ノードに新しいレジストリ キーを適用します。

>[!NOTE]
>%N の変更を反映するには、コンピューターを再起動する必要があります。

このレジストリ キーが設定すると、ライブ ダンプの作成は失敗し、"STATUS_NOT_SUPPORTED"エラーを生成します。

#### <a name="method-2"></a>方法 2
既定では、Windows エラー報告により、7 日間レポート種類ごとに 1 つだけ LiveDump と 5 日間ごとにマシンあたり 1 つだけ LiveDump です。 のみを許可する 1 つ LiveDump マシンで永久に次のレジストリ キーを設定して変更できます。
```
reg add "HKLM\Software\Microsoft\Windows\Windows Error Reporting\FullLiveKernelReports" /v SystemThrottleThreshold /t REG_DWORD /d 0xFFFFFFFF /f
```
```
reg add "HKLM\Software\Microsoft\Windows\Windows Error Reporting\FullLiveKernelReports" /v ComponentThrottleThreshold /t REG_DWORD /d 0xFFFFFFFF /f
```

*注*変更を反映するには、コンピューターを再起動する必要があります。

### <a name="method-3"></a>方法 3
ライブのダンプ (イベント、5120 を記録する場合) などのクラスターの生成を無効にするには、次のコマンドレットを実行します。

```powershell
(Get-Cluster).DumpPolicy = ((Get-Cluster).DumpPolicy -band 0xFFFFFFFFFFFFFFFE)
```
このコマンドレットは、コンピューターを再起動しなくても、すべてのクラスター ノードで有効になります。
    
## <a name="slow-io-performance"></a>低速の IO パフォーマンス

低速の IO パフォーマンスを表示している場合は、記憶域スペース ダイレクト構成でキャッシュが有効になっているかどうかを確認します。 

チェックする 2 つの方法はあります。 
     
 
1. クラスター ログを使用します。 任意のテキスト エディターで、クラスター ログを開き、検索"[ステージ SBL ディスク ステージ]." これは、ログで生成されたノード上のディスクの一覧表示されます。 

     キャッシュには、ディスクの使用例が有効になります。状態が CacheDiskStateInitializedAndBound、およびがここで、GUID が存在することは、ここで注意してください。 

   ```
   [=== SBL Disks ===]
    {26e2e40f-a243-1196-49e3-8522f987df76},3,false,true,1,48,{1ff348f1-d10d-7a1a-d781-4734f4440481},CacheDiskStateInitializedAndBound,1,8087,54,false,false,HGST    ,HUH721010AL4200 ,        7PG3N2ER,A21D,{d5e27a3b-42fb-410a-81c6-9d8cc12da20c},[R/M 0 R/U 0 R/T 0 W/M 0 W/U 0 W/T 0],
    ```

    キャッシュが有効になっていません。ここで GUID が存在するがないと、状態が CacheDiskStateNonHybrid 確認できます。 
    ```
   [=== SBL Disks ===]
    {426f7f04-e975-fc9d-28fd-72a32f811b7d},12,false,true,1,24,{00000000-0000-0000-0000-000000000000},CacheDiskStateNonHybrid,0,0,0,false,false,HGST    ,HUH721010AL4200 ,        7PGXXG6C,A21D,{d5e27a3b-42fb-410a-81c6-9d8cc12da20c},[R/M 0 R/U 0 R/T 0 W/M 0 W/U 0 W/T 0],
    ```

    キャッシュが有効になっていません。既定では、同じ型のケースのすべてのディスクがときに無効です。 ここで GUID が存在するがないと、状態が CacheDiskStateIneligibleDataPartition 確認できます。 
    ```
    {d543f90c-798b-d2fe-7f0a-cb226c77eeed},10,false,false,1,20,{00000000-0000-0000-0000-000000000000},CacheDiskStateIneligibleDataPartition,0,0,0,false,false,NVMe    ,INTEL SSDPE7KX02,  PHLF7330004V2P0LGN,0170,{79b4d631-976f-4c94-a783-df950389fd38},[R/M 0 R/U 0 R/T 0 W/M 0 W/U 0 W/T 0], 
    ```  
2. Get-PhysicalDisk.xml、SDDCDiagnosticInfo からを使用します。
    1. 使用して XML ファイルを開く"$d Import-clixml GetPhysicalDisk.XML ="
    2. 「ストレージ ・ ipmo」の実行します。
    3. "$d"を実行します。 いないジャーナルを自動選択は、使用状況は、このような出力に表示されます。 

   |FriendlyName|  SerialNumber| MediaType| CanPool| OperationalStatus| HealthStatus| 使用方法| サイズ|
   |-----------|------------|---------| -------| -----------------| ------------| -----| ----|
   |NVMe INTEL SSDPE7KX02| PHLF733000372P0LGN| SSD| False|   OK|                正常|      自動選択 1.82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF7504008J2P0LGN| SSD|  False|    OK|                正常| 自動選択| 1.82 TB|
   |NVMe INTEL SSDPE7KX02| PHLF7504005F2P0LGN| SSD|  False|  OK|                正常| 自動選択| 1.82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF7504002A2P0LGN| SSD| False| OK|    正常| 自動選択| 1.82 TB|
   |NVMe INTEL SSDPE7KX02| PHLF7504004T2P0LGN |SSD| False|OK|       正常| 自動選択| 1.82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF7504002E2P0LGN| SSD| False| OK|      正常| 自動選択| 1.82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF7330002Z2P0LGN| SSD| False| OK|      正常|自動選択| 1.82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF733000272P0LGN |SSD| False| OK|  正常| 自動選択| 1.82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF7330001J2P0LGN |SSD| False| OK| 正常| 自動選択| 1.82 TB|
   |NVMe INTEL SSDPE7KX02| PHLF733000302P0LGN |SSD| False| OK|正常| 自動選択| 1.82 TB|
   |NVMe INTEL SSDPE7KX02| PHLF7330004D2P0LGN |SSD| False| OK| 正常| 自動選択 |1.82 TB|
    
## <a name="how-to-destroy-an-existing-cluster-so-you-can-use-the-same-disks-again"></a>同じディスクをもう一度使用できるように、既存のクラスターを破棄する方法

記憶域スペース ダイレクト クラスターで記憶域スペース ダイレクトを無効にしてしたらで説明されているクリーンアップ プロセスを使用して[ドライブをクリーニング](deploy-storage-spaces-direct.md#step-31-clean-drives)、クラスター化された記憶域プールがオフラインの状態に残っておよびヘルス サービスはから削除クラスター。

次の手順では、ファントムの記憶域プールを削除します。 
   ```powershell
   Get-ClusterResource -Name "Cluster Pool 1" | Remove-ClusterResource
   ```

ここを実行する場合**Get-physicaldisk**任意のノードには、プールに含まれていたすべてのディスクが表示されます。 たとえば、4 ノードはそれぞれ 100 GB の各ノードに表示される 4 つの SAS ディスクを含むクラスター ラボで。 その場合は、記憶域スペース ダイレクトを無効にする SBL (記憶域バス層) を削除しますを実行する場合、フィルターのまま**Get-physicaldisk**、ローカルの OS ディスクを除外する 4 つのディスクを報告する必要があります。 代わりに 16 を代わりに報告ことにします。 これは、クラスター内のすべてのノードで同じです。 実行すると、 **Get-disk**コマンドでは、このサンプル出力に示すよう番号 0、1、2、および、ローカルに接続されたディスクが表示されます。

|数値| フレンドリ名| シリアル番号|HealthStatus|OperationalStatus|合計サイズ| パーティションの形式|
|-|-|-|-|-|-|-|-|
|0|Msft Virtu.  ||正常 | オンライン|  127 GB| GPT|
||Msft Virtu. ||正常| オフライン| 100 GB| RAW|
||Msft Virtu. ||正常| オフライン| 100 GB| RAW|
||Msft Virtu. ||正常| オフライン| 100 GB| RAW|
||Msft Virtu. ||正常| オフライン| 100 GB| RAW|
|1|Msft Virtu.||正常| オフライン| 100 GB| RAW|
||Msft Virtu. ||正常| オフライン| 100 GB| RAW|
|2|Msft Virtu.||正常| オフライン| 100 GB| RAW|
||Msft Virtu. ||正常| オフライン| 100 GB| RAW|
||Msft Virtu. ||正常| オフライン| 100 GB| RAW|
||Msft Virtu. ||正常| オフライン| 100 GB| RAW|
||Msft Virtu. ||正常| オフライン| 100 GB| RAW|
|4|Msft Virtu.||正常| オフライン| 100 GB| RAW|
|3|Msft Virtu.||正常| オフライン| 100 GB| RAW|
||Msft Virtu. ||正常| オフライン| 100 GB| RAW|
||Msft Virtu. ||正常| オフライン| 100 GB| RAW|
||Msft Virtu. ||正常| オフライン| 100 GB| RAW|

    
## <a name="error-message-about-unsupported-media-type-when-you-create-an-storage-spaces-direct-cluster-using-enable-clusters2d"></a>「サポートされていないメディアの種類」に関するエラー メッセージ Enable-clusters2d を使用して、記憶域スペース ダイレクト クラスターを作成する場合  

実行すると次のようなエラーが発生、 **Enable-clusters2d**コマンドレット。

![シナリオ 6 エラー メッセージ](media/troubleshooting/scenario-error-message.png)

この問題を解決するには、HBA アダプターは、HBA モードで構成されたことを確認します。 RAID モードで HBA は構成されていません。  
    
## <a name="enable-clusterstoragespacesdirect-hangs-at-waiting-until-sbl-disks-are-surfaced-or-at-27"></a>'SBL まで待機しているディスクが表示される'、または 27% で、ClusterStorageSpacesDirect がハングします。

検証レポートでは、次の情報が表示されます。

    Disk <identifier> connected to node <nodename> returned a SCSI Port Association and the corresponding enclosure device could not be found. The hardware is not compatible with Storage Spaces Direct (S2D), contact the hardware vendor to verify support for SCSI Enclosure Services (SES). 
    
  
ディスクと HBA カードの間にある HPE SAS エキスパンダーのカードに問題があります。 SAS エキスパンダーは、展開と展開コントロール自体に接続されている最初のドライブ間で重複する ID を作成します。  これが解決された[HPE スマート配列コント ローラー SAS Expander ファームウェア。4.02](https://support.hpe.com/hpsc/swd/public/detail?sp4ts.oid=7304566&swItemId=MTX_ef8d0bf4006542e194854eea6a&swEnvOid=4184#tab3).
    
## <a name="intel-ssd-dc-p4600-series-has-a-non-unique-nguid"></a>Intel SSD DC P4600 シリーズが一意でない NGUID
問題を表示し、Intel SSD DC P4600 シリーズのデバイスが 0100000001000000E4D25C000014E214 または次の例で 0100000001000000E4D25C0000EEE214 など複数の名前空間の 16 バイト NGUID のようなレポートするようですがあります。

|一意の id| deviceid |MediaType| BusType| シリアル番号| size|canpool| friendlyname| OperationalStatus|
|-|-|-|-|-|-|-|-|-
|5000CCA251D12E30| 0| HDD| SAS| 7PKR197G|                  10000831348736 |False|HGST| HUH721010AL4200| OK|
|eui.0100000001000000E4D25C000014E214 |4|SSD| NVMe|   0100_0000_0100_0000_E4D2_5C00_0014_E214.|1600321314816|True| INTEL| SSDPE2KE016T7|  OK|
|eui.0100000001000000E4D25C000014E214 |5|        SSD|       NVMe|    0100_0000_0100_0000_E4D2_5C00_0014_E214.|  1600321314816|    True| INTEL| SSDPE2KE016T7|  OK|
|eui.0100000001000000E4D25C0000EEE214| 6|        SSD|       NVMe|    0100_0000_0100_0000_E4D2_5C00_00EE_E214.|  1600321314816|    True| INTEL| SSDPE2KE016T7|  OK|
|eui.0100000001000000E4D25C0000EEE214| 7|        SSD|       NVMe|    0100_0000_0100_0000_E4D2_5C00_00EE_E214.|  1600321314816|    True| INTEL| SSDPE2KE016T7|  OK|

この問題を解決するには、最新バージョンに Intel ドライブのファームウェアを更新します。  ファームウェアのバージョンこの問題を解決するのには、2018 年 5 月から QDV101B1 が呼ばれます。

[Intel SSD のデータ センター ツールの 2018 年 5 月リリース](https://downloadmirror.intel.com/27778/eng/Intel_SSD_Data_Center_Tool_3_0_12_Release_Notes_330715-026.pdf)ファームウェア更新 QDV101B1、Intel SSD DC P4600 シリーズが含まれています。

    
## <a name="physical-disk-healthy-and-operational-status-is-removing-from-pool"></a>物理ディスク「"健全"、」と操作の状態が「プールから削除する」 

Windows Server 2016 記憶域スペース ダイレクト クラスターの場合は、表示がありますの 1 つ以上の物理ディスク HealthStatus「正常」として、OperationalStatus は「(削除して、[ok] のプールから)」 

「プールからの削除」を目的としたときに設定されます**Remove-physicaldisk**と呼ばれるが、状態を維持し、削除操作が失敗した場合は、回復を許可する状態で格納します。 次のメソッドのいずれかを 健全、OperationalStatus を手動で変更できます。

- プールから物理ディスクを削除し、再度追加します。
- 実行、[クリア PhysicalDiskHealthData.ps1 スクリプト](https://go.microsoft.com/fwlink/?linkid=2034205)インテントをオフにします。 (としてダウンロードできる、します。TXT ファイルです。 として保存する必要があります、します。PS1 ファイルを実行します。)

スクリプトを実行する方法を示すいくつかの例を次に示します。

- 使用して、 **SerialNumber**パラメーターを"健全"に設定する必要があるディスクを指定します。 シリアル番号を取得する**WMI MSFT_PhysicalDisk**または**Get-physicaldisk**します。 (私たちだけを使用している 0 s 以下のシリアル番号の。)
   
   ```powershell
   Clear-PhysicalDiskHealthData -Intent -Policy -SerialNumber 000000000000000 -Verbose -Force
    ```

- 使用して、 **UniqueId**ディスクを指定するパラメーター (からもう一度**WMI MSFT_PhysicalDisk**または**Get-physicaldisk**)。

   ```powershell
   Clear-PhysicalDiskHealthData -Intent -Policy -UniqueId 00000000000000000 -Verbose -Force
   ```

## <a name="file-copy-is-slow"></a>ファイルのコピーが遅い

ファイル エクスプ ローラーを使用して仮想ディスクに大容量の VHD をコピーする問題が表示される可能性があります - ファイルのコピーが予想より長引いています。

ファイル エクスプ ローラーを使用して、仮想ディスクに大容量の VHD をコピーするには、Robocopy または Xcopy はありません、推奨されるメソッドをこの期待されるパフォーマンスよりも低速になります。 コピー プロセスは、記憶域スタックの下位に位置し、代わりにローカル コピーのプロセスと同様に機能する記憶域スペース ダイレクトのスタックでは説明しません。

VMFleet と Diskspd を使用して、ロード テストとストレス テストをお勧め記憶域スペース ダイレクトのパフォーマンスをテストする場合、サーバー ベースの行を取得し、記憶域スペース ダイレクトのパフォーマンスの期待値を設定します。

## <a name="expected-events-that-you-would-see-on-rest-of-the-nodes-during-the-reboot-of-a-node"></a>ノードの再起動中に他のノードに表示するイベントが必要です。 

これらのイベントを無視するも安全です。 

    Event ID 205: Windows lost communication with physical disk {XXXXXXXXXXXXXXXXXXXX }. This can occur if a cable failed or was disconnected, or if the disk itself failed. 

    Event ID 203: Windows lost communication with physical disk {xxxxxxxxxxxxxxxxxxxxxxxx }. This can occur if a cable failed or was disconnected, or if the disk itself failed. 

Azure Vm で実行している場合は、このイベントを無視できます。

    Event ID 32: The driver detected that the device \Device\Harddisk5\DR5 has its write cache enabled. Data corruption may occur. 
    
## <a name="slow-performance-or-lost-communication-io-error-detached-or-no-redundancy-errors-for-deployments-that-use-intel-p3x00-nvme-devices"></a>パフォーマンスの低下または「紛失の通信、」"IO Error"、「デタッチ」または「No 冗長性」エラー Intel P3x00 NVMe デバイスを使用するデプロイ

「メンテナンス リリース 8」より前に、のファームウェア バージョン NVM Express (NVMe) デバイスの Intel P3x00 ファミリに基づいてハードウェアを使用している一部の記憶域スペース ダイレクトのユーザーに影響する重大な問題を特定できました 

>[!NOTE]
> 個々 の Oem 固有のファームウェア バージョン文字列を含む NVMe デバイスの Intel P3x00 ファミリに基づくデバイスがあります。 最新のファームウェアのバージョンの詳細については、OEM にお問い合わせください。

利用可能な最新のファームウェアをすぐに適用することをお勧め、Intel P3x00 ファミリ NVMe デバイスに基づいて、デプロイのハードウェアを使用する場合 (少なくともメンテナンス リリース 8)。 これは、 [Microsoft サポート記事](https://support.microsoft.com/en-us/help/4052341/slow-performance-or-lost-communication-io-error-detached-or-no-redunda)この問題に関する追加情報を提供します。 
