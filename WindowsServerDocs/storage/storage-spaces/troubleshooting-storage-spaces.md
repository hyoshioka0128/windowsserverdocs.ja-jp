---
title: 記憶域スペース ダイレクトのトラブルシューティング
description: 記憶域スペース ダイレクト展開をトラブルシューティングする方法について説明します。
keywords: 記憶域スペース
ms.prod: windows-server-threshold
ms.author: ''
ms.technology: storage-spaces
ms.topic: article
author: kaushika-msft
ms.date: 10/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: c7c9573732ff1cf5a998588b1aec81915c227ee2
ms.sourcegitcommit: 5d55c3ebd1ceee7229ea9a9989c69cf93757ed88
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2019
ms.locfileid: "9256935"
---
# 記憶域スペース ダイレクトのトラブルシューティングを行う

次の情報を使用して、記憶域スペース ダイレクトの展開をトラブルシューティングします。

一般に、次の手順を開始します。

1. Windows Server Catalog を使用して Windows Server 2016 の認定が SSD の製造元/モデルを確認します。 ベンダーでドライブが記憶域スペース ダイレクトのサポートされていることを確認します。
2. 障害のあるドライブのストレージを検査します。 記憶域管理ソフトウェアを使用すると、ドライブのステータスを確認できます。 いずれかの場合、ドライブ障害のある、ベンダーと協力します。 
3. 記憶域を更新し、必要に応じて、ドライブのファームウェアします。
   すべてのノードに最新の Windows 更新プログラムがインストールされていることを確認します。 Windows Server 2016 からの最新の更新プログラムを取得できます[https://aka.ms/update2016](https://aka.ms/update2016)します。
4. ネットワーク アダプターのドライバーとファームウェアを更新します。
5. クラスター検証を実行して、記憶域スペース ダイレクトのセクションを確認する、キャッシュで使用されるドライブが正しく表示されることを確認し、エラーなし。

問題がある場合でも場合、は、以下のシナリオを確認します。

## 仮想ディスクのリソースはいいえ冗長性の状態
記憶域スペース ダイレクト システムのノードを再起動予期せずクラッシュや電源障害があるためです。 次に、1 つまたは複数の仮想ディスクをオンラインにならない場合があり、「冗長性を情報が不足しています」の説明を参照してください。
    
|FriendlyName|ResiliencySettingName| OperationalStatus| HealthStatus| IsManualAttach|Size| PSComputerName|
|------------|---------------------| -----------------| ------------| --------------|-----| --------------|
|Disk4| Mirror (ミラー)| OK|  Healthy| True|  10 TB|  ノード 01.conto.|
|Disk3         |Mirror (ミラー)                 |OK                          |Healthy       |True            |10 TB | ノード 01.conto.|
|ディスク 2         |Mirror (ミラー)                 |非冗長               |Unhealthy     |True            |10 TB | ノード 01.conto.|
|Disk1         |Mirror (ミラー)                 |{冗長性なし、InService}  |Unhealthy     |True            |10 TB | ノード 01.conto.| 

さらに、仮想ディスクをオンラインにすると、次の情報が (DiskRecoveryAction) クラスターのログに記録されます。  

```
[Verbose] 00002904.00001040::YYYY/MM/DD-12:03:44.891 INFO [RES] Physical Disk <DiskName>: OnlineThread: SuGetSpace returned 0.
[Verbose] 00002904.00001040:: YYYY/MM/DD -12:03:44.891 WARN [RES] Physical Disk < DiskName>: Underlying virtual disk is in 'no redundancy' state; its volume(s) may fail to mount.
[Verbose] 00002904.00001040:: YYYY/MM/DD -12:03:44.891 ERR [RES] Physical Disk <DiskName>: Failing online due to virtual disk in 'no redundancy' state. If you would like to attempt to online the disk anyway, first set this resource's private property 'DiskRecoveryAction' to 1. We will try to bring the disk online for recovery, but even if successful, its volume(s) or CSV may be unavailable. 
``` 

**いいえ冗長性の操作状態**は、ディスクが失敗した場合や、システムは、仮想ディスク上のデータにアクセスすることができない場合に発生します。 この問題は、ノード上でメンテナンス時にノードで、再起動が発生した場合に発生することができます。
    
この問題を解決するのには、次の手順を実行します。

1. CSV から影響を受ける仮想ディスクを削除します。 「使用可能な記憶域」グループで、クラスター内に配置され、「物理ディスク」のリソースの種類を示すスタート

   ```powershell
   Remove-ClusterSharedVolume -name "VdiskName"
   ``` 
2. 利用可能な記憶域グループを所有しているノードで、いいえ冗長性の状態にあるすべてのディスクで次のコマンドを実行します。 ノード「利用可能な記憶域」グループを識別するには、次のコマンドを実行できます。

   ```powershell
   Get-ClusterGroup
   ```
3. ディスク回復アクションを設定し、ディスクを起動します。
   ```powershell
   Get-ClusterResource "VdiskName" | Set-ClusterParameter -Name DiskRecoveryAction -Value 1
   Start-ClusterResource -Name "VdiskName"
   ```
4. 修復が自動的に開始する必要があります。 修復を完了するまで待機します。 中断状態に移動し、再び起動して可能性があります。 進行状況を監視します。 
    - **Get StorageJob**修復のステータスを監視し、完了したときに表示を実行します。
    - **Get VirtualDisk**を実行し、スペース、HealthStatus の正常な状態を返すことを確認します。
5. 後の修復が完了すると仮想ディスクは、正常、仮想ディスクのパラメーターを戻すです。

   ```powershell
    Get-ClusterResource "VdiskName" | Set-ClusterParameter -Name DiskRecoveryAction -Value 0
   ```
6. オフラインと DiskRecoveryAction を有効にするためにもう一度し、オンラインのディスクを実行します。

   ```powershell
   Stop-ClusterResource "VdiskName"
   Start-ClusterResource "VdiskName"
   ``` 
7. CSV に影響を受ける仮想ディスクを追加します。

   ```powershell
   Add-ClusterSharedVolume -name "VdiskName"
   ```

**DiskRecoveryAction**は、読み取り/書き込みモード チェックなしでスペース ボリュームをアタッチできるようにするオーバーライド スイッチです。 プロパティを使用すると、ボリュームをオンラインにしない理由に診断を行うことができます。 メンテナンス モードとよく似ていますが、失敗の状態のリソースで呼び出すことができます。 「いいえ、冗長性」へのアクセスを取得するなどの状況で役に立ちますのデータにアクセスすることもできますデータをしてコピーします。 DiskRecoveryAction プロパティは、2018 年 2 月 22日の更新プログラム、KB 4077525 で追加されました。
    
    
## クラスター内からデタッチされた状態 

**Get VirtualDisk**コマンドレットを実行するときは、1 つ以上の記憶域スペース ダイレクトの仮想ディスクの OperationalStatus が切り離されます。 ただし、 **Get-physicaldisk**コマンドレットによって報告された HealthStatus では、すべての物理ディスクが正常な状態でありことを示します。

**Get VirtualDisk**コマンドレットの出力の例を次に示します。

|FriendlyName|  ResiliencySettingName|  OperationalStatus|   HealthStatus|  IsManualAttach|  Size|   PSComputerName|
|-|-|-|-|-|-|-|
|Disk4|         Mirror (ミラー)|                 OK|                  Healthy|       True|            10 TB|  ノード 01.conto.|
|Disk3|         Mirror (ミラー)|                 OK|                  Healthy|       True|            10 TB|  ノード 01.conto.|
|ディスク 2|         Mirror (ミラー)|                 デタッチ|            Unknown|       True|            10 TB|  ノード 01.conto.|
|Disk1|         Mirror (ミラー)|                 デタッチ|            Unknown|       True|            10 TB|  ノード 01.conto.| 


さらに、ノード上で次のイベントが記録されます。

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

**分離された操作の状態**は、(恐竜回収チーム) を追跡ダーティ領域ログがいっぱい場合に発生することができます。 記憶域スペースでは、ミラー スペース (恐竜回収チーム) を追跡ダーティの領域を使用して、電源障害が発生すると、記憶域スペースがやり直しまたはストレージ領域の形をもう一度柔軟性の高い操作を元に戻すことができるかどうかを確認するメタデータへの中の更新を記録することを確認電源が復元され、システムが起動するとき、一貫性のある状態。 恐竜回収チーム ログがいっぱいの場合は、仮想ディスク オンラインにできませんまで、恐竜回収チーム メタデータが同期され、フラッシュします。 このプロセスを終了するためのいくつかの時間かかることが、フル スキャンを実行している必要があります。
    
この問題を解決するのには、次の手順を実行します。
1. CSV から影響を受ける仮想ディスクを削除します。

   ```powershell
   Remove-ClusterSharedVolume -name "VdiskName"
   ``` 
2. すべてのディスクをオンラインになるいないで、次のコマンドを実行します。 

   ```powershell
   Get-ClusterResource -Name "VdiskName" | Set-ClusterParameter DiskRunChkDsk 7
   Start-ClusterResource -Name "VdiskName"
   ``` 
3. すべてのノードからデタッチされたボリュームはオンラインで、次のコマンドを実行します。 

   ```powershell
   Get-ScheduledTask -TaskName "Data Integrity Scan for Crash Recovery" | Start-ScheduledTask 
   ```
   このタスクは、すべてのノードからデタッチされたボリュームがオンラインで開始する必要があります。 修復が自動的に開始する必要があります。 修復を完了するまで待機します。 中断状態に移動し、再び起動して可能性があります。 進行状況を監視します。 
   - **Get StorageJob**修復のステータスを監視し、完了したときに表示を実行します。
   -  **Get VirtualDisk**を実行し、領域を返す、HealthStatus の正常な状態を確認します。
    - 「データ整合性スキャンのクラッシュ回復」は、記憶域ジョブとして表示されないタスクと進行状況インジケーターはありません。 タスクが表示されている場合、実行中として実行されています。 これが完了したら、完了したが表示されます。
    
       さらに、次のコマンドレットを使用して、実行中のタスクのスケジュールのステータスを表示できます。 
       ```powershell
       Get-ScheduledTask | ? State -eq running
       ``` 
4. 「データ整合性スキャンのクラッシュ回復」が完了したら、すぐ修復が完了すると、仮想ディスクは、正常、仮想ディスクのパラメーターを戻す。 

   ```powershell
   Get-ClusterResource -Name "VdiskName" | Set-ClusterParameter DiskRunChkDsk 0 
   ```
5. CSV に影響を受ける仮想ディスクを追加します。    

   ```powershell
   Add-ClusterSharedVolume -name "VdiskName"
   ```  
**DiskRunChkdsk 値 7**は、読み取り専用モードではスペース ボリュームをアタッチし、パーティションに使用されます。 これにより、スペースを自動検出と自動修復修復をトリガーできます。 修復が実行自動的に一度マウントします。 任意のデータをコピーすることができますへのアクセスを取得することができるデータにアクセスすることもできます。 完全な恐竜回収チーム ログなど、いくつかのフォールト条件クラッシュ回復スケジュールされたタスクのデータ整合性スキャンを実行する必要があります。
    
**クラッシュ回復タスクのデータ整合性スキャン**は、同期し、完全なダーティ領域 (恐竜回収チーム) を追跡のログをクリアに使用されます。 このタスクを完了する時間がかかることができます。 「データ整合性スキャンのクラッシュ回復」は、記憶域ジョブとして表示されないタスクと進行状況インジケーターはありません。 タスクが表示されている場合、実行中として実行されています。 これが完了したら、完了として表示されます。 タスクを取り消すか、このタスクの実行中には、ノードを再起動した場合は、タスクを最初からやり直す必要があります。

詳細については、[記憶域スペース ダイレクトのトラブルシューティングの正常性と動作状態](storage-spaces-states.md)を参照してください。
    
## イベント 5120 STATUS_IO_TIMEOUT c00000b5 を 

> [!Important]
> これらの現象を修正された更新プログラムを適用するときに発生する可能性を減らすためには、お勧め[Windows Server 2016 の累積的な更新プログラムを 2018 年 10 月 18日](https://support.microsoft.com/help/4462928)またはそれ以降のバージョンをインストールする手順の記憶域メンテナンス モードを使用するにはノード現在インストールされているリリースされた Windows Server 2016 の累積的な更新[、2018 年 5 月 8日](https://support.microsoft.com/help/4103723)から[、2018 年 10 月 9日](https://support.microsoft.com/help/KB4462917)までします。

Windows Server 2016 の累積的な更新[が 8、2018 KB 4103723](https://support.microsoft.com/help/4103723)から[KB 4462917 2018 年 10 月 9日](https://support.microsoft.com/help/4462917)インストールにリリースされたを持つノードを再起動した後は、イベント 5120 STATUS_IO_TIMEOUT c00000b5 を取得する可能性があります。

ノードを再起動すると、イベント 5120 はシステム イベント ログに記録し、次のエラー コードのいずれかが含まれています。

```
Event Source: Microsoft-Windows-FailoverClustering
Event ID: 5120
Description:    Cluster Shared Volume 'CSVName' ('Cluster Virtual Disk (CSVName)') has entered a paused state because of 'STATUS_IO_TIMEOUT(c00000b5)'. All I/O will temporarily be queued until a path to the volume is reestablished. 

Cluster Shared Volume ‘CSVName’ ('Cluster Virtual Disk (CSVName)') has entered a paused state because of 'STATUS_CONNECTION_DISCONNECTED(c000020c)'. All I/O will temporarily be queued until a path to the volume is reestablished.    
```

イベント、5120 が記録され、ライブ ダンプが生成され、追加現象が発生する場合もパフォーマンスに影響されるデバッグ情報を収集します。 ライブ ダンプを生成すると、メモリ ダンプ ファイルの書き込みのスナップショットを有効にする簡単な一時停止します。 大量のメモリがあり、負荷がシステムには、ノードをクラスター メンバーシップ外ドロップし、ログに記録する次のイベント 1135 も発生する可能性があります。

```
Event source: Microsoft-Windows-FailoverClustering
Event ID: 1135  
Description: Cluster node 'NODENAME'was removed from the active failover cluster membership. The Cluster service on this node may have stopped. This could also be due to the node having lost communication with other active nodes in the failover cluster. Run the Validate a Configuration wizard to check your network configuration. If the condition persists, check for hardware or software errors related to the network adapters on this node. Also check for failures in any other network components to which the node is connected such as hubs, switches, or bridges.
```

変更は、記憶域スペース ダイレクト クラスター内通信 SMB ネットワーク セッションの SMB 弾力性のある処理を追加する、2018 年 5 月 8日の累積的な更新プログラムで導入されました。 これは、一時的なネットワーク エラーを回復性を向上し、RoCE でネットワーク輻輳の処理方法を向上させるために行われました。

ノードが再起動されたときに、SMB 接続を再接続するときのタイムアウトおよびタイムアウトを待機してからこれらの機能強化誤っても増加します。 これらの問題の負荷がシステムに影響を与えることができます。 予期しないダウンタイム、中に最大 60 秒の IO の一時停止も観察されたシステムがタイムアウトへの接続を待機する間します。

この問題を解決するには、 [2018 年 10 月 18日 Windows Server 2016 の累積的な更新プログラム](https://support.microsoft.com/help/4462928)またはそれ以降のバージョンをインストールします。

*注:* この更新プログラムは、この問題を修正する SMB 接続のタイムアウトを CSV タイムアウトを配置します。 回避策」に記載されているライブ ダンプの生成を無効に変更は実装されません。
    
### プロセスの流れをシャット ダウンします。

1. Get VirtualDisk のコマンドレットを実行し、HealthStatus 値が正常にあるかどうかを確認します。
2. 次のコマンドレットを実行して、ノードをドレインします。

   ```powershell
   Suspend-ClusterNode -Drain
   ```
3. 次のコマンドレットを実行してのディスクを記憶域メンテナンス モードでは、そのノードに配置します。 

   ```powershell
   Get-StorageFaultDomain -type StorageScaleUnit | Where-Object {$_.FriendlyName -eq "<NodeName>"} | Enable-StorageMaintenanceMode
   ```
4. **Get-physicaldisk**のコマンドレットを実行し、その OperationalStatus 値は、メンテナンス モードであるかどうかを確認します。
5. ノードを再起動する**コンピューターを再起動**コマンドレットを実行します。
6. ノードを再起動した後は、次のコマンドレットを実行して、記憶域メンテナンス モードからそのノード上のディスクを削除します。

   ```powershell
   Get-StorageFaultDomain -type StorageScaleUnit | Where-Object {$_.FriendlyName -eq "<NodeName>"} | Disable-StorageMaintenanceMode
   ```
7. 次のコマンドレットを実行してノードを再開します。

   ```powershell
   Resume-ClusterNode
   ```
8. 再同期ジョブの状態を確認するには、次のコマンドレットを実行します。

   ```powershell
   Get-StorageJob
   ```

### ライブ ダンプを無効にします。
ライブ ダンプ生成すると、大量のメモリがあり、負荷がシステムでの影響を軽減するためにさらにライブ ダンプの生成を無効にする可能性があります。 以下は、3 つのオプションが提供されています。

>[!Caution]
>この手順では、Microsoft サポートは、この問題を調査する必要がある、診断情報の収集を防ぐことができます。 サポート エージェントは、特定のトラブルシューティング シナリオに基づいてライブ ダンプの生成を再度有効にするように依頼する必要があります。

以下のようには、ライブのダンプを無効にする 2 つの方法があります。

#### 方法 1 (このシナリオでは推奨)
ライブ ダンプ システム全体を含め、すべてのダンプを完全に無効にするには、次の手順に従います。

1. 次のレジストリ キーの作成: HKLM\System\CurrentControlSet\Control\CrashControl\ForceDumpsDisabled
2. 新しい**ForceDumpsDisabled**キーの下の GuardedHost、として REG_DWORD プロパティを作成し、0x10000000 にその値を設定します。
3. 各クラスター ノードに新しいレジストリ キーを適用します。

>[!NOTE]
>Nregistry 変更を有効にするには、コンピューターを再起動する必要があります。

このレジストリ キーが設定すると、ライブした後、ダンプの作成は失敗し、"STATUS_NOT_SUPPORTED"エラーを生成します。

#### 方法 2
既定では、Windows エラー報告によって、7 日間レポート種類ごとに 1 つだけ LiveDump と 5 日ごとのマシンあたり 1 つだけ LiveDump できます。 のみを許可する 1 つの LiveDump コンピューターで永続的に次のレジストリ キーを設定しているを変更できます。
```
reg add "HKLM\Software\Microsoft\Windows\Windows Error Reporting\FullLiveKernelReports" /v SystemThrottleThreshold /t REG_DWORD /d 0xFFFFFFFF /f
```
```
reg add "HKLM\Software\Microsoft\Windows\Windows Error Reporting\FullLiveKernelReports" /v ComponentThrottleThreshold /t REG_DWORD /d 0xFFFFFFFF /f
```

*注:* 変更を反映するためのコンピューターを再起動する必要があります。

### 方法 3
ライブ ダンプ (と、イベント 5120 を記録) などのクラスターの生成を無効にするには、次のコマンドレットを実行します。

```powershell
(Get-Cluster).DumpPolicy = ((Get-Cluster).DumpPolicy -band 0xFFFFFFFFFFFFFFFE)
```
このコマンドレットは、コンピューターを再起動することがなく、すべてのクラスター ノードの即時の影響です。
    
## IO パフォーマンスの低下

IO パフォーマンスの低下を表示している場合は、記憶域スペース ダイレクト構成でキャッシュが有効になっているかどうかを確認します。 

2 つの方法を確認するにがあります。 
     
 
1. クラスターのログを使用します。 任意のテキスト エディターでクラスターのログを開き、検索"[=== SBL ディスク ===]." これでログが生成されたノード上のディスクの一覧表示されます。 

     キャッシュの有効ディスクの例: ことに注意ここで状態が CacheDiskStateInitializedAndBound が存在する GUID を次にします。 

   ```
   [=== SBL Disks ===]
    {26e2e40f-a243-1196-49e3-8522f987df76},3,false,true,1,48,{1ff348f1-d10d-7a1a-d781-4734f4440481},CacheDiskStateInitializedAndBound,1,8087,54,false,false,HGST    ,HUH721010AL4200 ,        7PG3N2ER,A21D,{d5e27a3b-42fb-410a-81c6-9d8cc12da20c},[R/M 0 R/U 0 R/T 0 W/M 0 W/U 0 W/T 0],
    ```

    キャッシュは有効になっていない: ここで存在する GUID がないと、状態が CacheDiskStateNonHybrid 確認ことができます。 
    ```
   [=== SBL Disks ===]
    {426f7f04-e975-fc9d-28fd-72a32f811b7d},12,false,true,1,24,{00000000-0000-0000-0000-000000000000},CacheDiskStateNonHybrid,0,0,0,false,false,HGST    ,HUH721010AL4200 ,        7PGXXG6C,A21D,{d5e27a3b-42fb-410a-81c6-9d8cc12da20c},[R/M 0 R/U 0 R/T 0 W/M 0 W/U 0 W/T 0],
    ```

    キャッシュは有効になっていない: とすべてのディスクは、同じ種類のケースが既定で有効になっていません。 ここではなく GUID が存在する、状態が CacheDiskStateIneligibleDataPartition を確認できます。 
    ```
    {d543f90c-798b-d2fe-7f0a-cb226c77eeed},10,false,false,1,20,{00000000-0000-0000-0000-000000000000},CacheDiskStateIneligibleDataPartition,0,0,0,false,false,NVMe    ,INTEL SSDPE7KX02,  PHLF7330004V2P0LGN,0170,{79b4d631-976f-4c94-a783-df950389fd38},[R/M 0 R/U 0 R/T 0 W/M 0 W/U 0 W/T 0], 
    ```  
2. Get-PhysicalDisk.xml、SDDCDiagnosticInfo からの使用
    1. XML ファイルを開く"$d インポート Clixml GetPhysicalDisk.XML ="
    2. 「Ipmo 記憶域」を実行します。
    3. "$d"を実行します。 使用しないジャーナルする自動選択は、このような出力が表示されます。 

   |FriendlyName|  SerialNumber| MediaType| CanPool| OperationalStatus| HealthStatus| 使用方法| Size|
   |-----------|------------|---------| -------| -----------------| ------------| -----| ----|
   |NVMe INTEL SSDPE7KX02| PHLF733000372P0LGN| SSD| False|   OK|                Healthy|      自動選択 1.82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF7504008J2P0LGN| SSD|  False|    OK|                Healthy| 自動選択| 1.82 TB|
   |NVMe INTEL SSDPE7KX02| PHLF7504005F2P0LGN| SSD|  False|  OK|                Healthy| 自動選択| 1.82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF7504002A2P0LGN| SSD| False| OK|    Healthy| 自動選択| 1.82 TB|
   |NVMe INTEL SSDPE7KX02| PHLF7504004T2P0LGN |SSD| False|OK|       Healthy| 自動選択| 1.82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF7504002E2P0LGN| SSD| False| OK|      Healthy| 自動選択| 1.82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF7330002Z2P0LGN| SSD| False| OK|      Healthy|自動選択| 1.82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF733000272P0LGN |SSD| False| OK|  Healthy| 自動選択| 1.82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF7330001J2P0LGN |SSD| False| OK| Healthy| 自動選択| 1.82 TB|
   |NVMe INTEL SSDPE7KX02| PHLF733000302P0LGN |SSD| False| OK|Healthy| 自動選択| 1.82 TB|
   |NVMe INTEL SSDPE7KX02| PHLF7330004D2P0LGN |SSD| False| OK| Healthy| 自動選択 |1.82 TB|
    
## 同じディスクを再び使用できるように、既存のクラスターを破棄する方法

記憶域スペース ダイレクト クラスターでは、記憶域スペース ダイレクトを無効にし、[クリーンなドライブ](deploy-storage-spaces-direct.md#step-31-clean-drives)で説明されているクリーンアップ処理を使用するに、クラスター化された記憶域プールは、オフラインの状態で残っているし、ヘルス サービスはクラスターから削除されます。

次の手順では、ファントム記憶域プールを削除します。 
   ```powershell
   Get-ClusterResource -Name "Cluster Pool 1" | Remove-ClusterResource
   ```

これで、任意のノードで**Get-physicaldisk**を実行する場合、プール内のすべてのディスクが表示されます。 たとえば、4 ノードの 100 GB ごとの各ノードに表示される 4 の SAS ディスクでクラスター ラボで。 その場合は、記憶域スペース ダイレクトは無効にした後、SBL (記憶域バス層) が削除されるフィルターでは、そのままに**Get-physicaldisk**を実行する、ローカルの OS ディスクを除外する 4 つのディスクを報告する必要があります。 代わりに 16 を代わりに報告してにします。 これは、クラスター内のすべてのノードに同じです。 **Get ディスク**コマンドを実行すると、0, 1, 2 というように、この出力の例で示すよう番号ローカルで接続されたディスクが表示されます。

|Number| フレンドリ名| シリアル番号|HealthStatus|OperationalStatus|合計サイズ| パーティション スタイル|
|-|-|-|-|-|-|-|-|
|0|Msft Virtu.  ||Healthy | オンライン|  127 GB| GPT|
||Msft Virtu. ||Healthy| オフライン| 100 GB| RAW|
||Msft Virtu. ||Healthy| オフライン| 100 GB| RAW|
||Msft Virtu. ||Healthy| オフライン| 100 GB| RAW|
||Msft Virtu. ||Healthy| オフライン| 100 GB| RAW|
|1|Msft Virtu.||Healthy| オフライン| 100 GB| RAW|
||Msft Virtu. ||Healthy| オフライン| 100 GB| RAW|
|2|Msft Virtu.||Healthy| オフライン| 100 GB| RAW|
||Msft Virtu. ||Healthy| オフライン| 100 GB| RAW|
||Msft Virtu. ||Healthy| オフライン| 100 GB| RAW|
||Msft Virtu. ||Healthy| オフライン| 100 GB| RAW|
||Msft Virtu. ||Healthy| オフライン| 100 GB| RAW|
|4|Msft Virtu.||Healthy| オフライン| 100 GB| RAW|
|3|Msft Virtu.||Healthy| オフライン| 100 GB| RAW|
||Msft Virtu. ||Healthy| オフライン| 100 GB| RAW|
||Msft Virtu. ||Healthy| オフライン| 100 GB| RAW|
||Msft Virtu. ||Healthy| オフライン| 100 GB| RAW|

    
## 「サポートされていないメディアの種類」というエラー メッセージ Enable-clusters2d を使用して記憶域スペース ダイレクトのクラスターを作成する場合  

**Enable-clusters2d**コマンドレットを実行するときに、次のようなエラーが発生する可能性があります。

![シナリオ 6 エラー メッセージ](media/troubleshooting/scenario-error-message.png)

この問題を解決するには、HBA アダプターが HBA モードで構成されていることを確認します。 RAID モードでは HBA を構成するべきではありません。  
    
## Enable-clusterstoragespacesdirect ハング、'SBL まで待機しているディスクが表示される' または 27% で

検証レポートでは、次の情報が表示されます。

    Disk <identifier> connected to node <nodename> returned a SCSI Port Association and the corresponding enclosure device could not be found. The hardware is not compatible with Storage Spaces Direct (S2D), contact the hardware vendor to verify support for SCSI Enclosure Services (SES). 
    
  
ディスクと HBA カードの間にある HPE SAS エキスパンダー カードで問題が発生します。 SAS エキスパンダーでは、最初に、展開とエキスパンダー自体に接続されているドライブの間で重複する ID を作成します。  これが解決したら[HPE スマート配列コント ローラー SAS エキスパンダー ファームウェア: 4.02](https://support.hpe.com/hpsc/swd/public/detail?sp4ts.oid=7304566&swItemId=MTX_ef8d0bf4006542e194854eea6a&swEnvOid=4184#tab3)します。
    
## Intel SSD DC P4600 シリーズが一意でない NGUID
問題を表示し、Intel SSD DC P4600 シリーズのデバイスが 0100000001000000E4D25C000014E214 や次の例で 0100000001000000E4D25C0000EEE214 などの複数の名前空間の 16 バイト NGUID と同様に報告よう可能性があります。

|uniqueid| deviceid |MediaType| バスの種類| シリアル番号| size|canpool| フレンドリ名| OperationalStatus|
|-|-|-|-|-|-|-|-|-
|5000CCA251D12E30| 0| HDD| SAS| 7PKR197G|                  10000831348736 |False|HGST| HUH721010AL4200| OK|
|eui.0100000001000000E4D25C000014E214 |4|SSD| NVMe|   0100_0000_0100_0000_E4D2_5C00_0014_E214 します。|1600321314816|True| INTEL| SSDPE2KE016T7|  OK|
|eui.0100000001000000E4D25C000014E214 |5|        SSD|       NVMe|    0100_0000_0100_0000_E4D2_5C00_0014_E214 します。|  1600321314816|    True| INTEL| SSDPE2KE016T7|  OK|
|eui.0100000001000000E4D25C0000EEE214| 6|        SSD|       NVMe|    0100_0000_0100_0000_E4D2_5C00_00EE_E214 します。|  1600321314816|    True| INTEL| SSDPE2KE016T7|  OK|
|eui.0100000001000000E4D25C0000EEE214| 7|        SSD|       NVMe|    0100_0000_0100_0000_E4D2_5C00_00EE_E214 します。|  1600321314816|    True| INTEL| SSDPE2KE016T7|  OK|

この問題を解決するのには、最新バージョンに Intel ドライブのファームウェアを更新します。  ファームウェアのバージョンから 2018 年 5 月 QDV101B1 は、この問題を解決するのには呼ばれます。

[2018 年 5 月を Intel SSD データ センター ツールのリリース](https://downloadmirror.intel.com/27778/eng/Intel_SSD_Data_Center_Tool_3_0_12_Release_Notes_330715-026.pdf)には、ファームウェア更新 QDV101B1、Intel SSD DC P4600 シリーズが含まれます。

    
## 物理ディスク「正常、」、操作状態が「プールから削除する」 

、Windows Server 2016 記憶域スペース ダイレクト クラスターで表示されるの 1 つ以上の物理ディスク HealthStatus「正常です」として、OperationalStatus は「(削除プール、[ok] から)。」 

「プールから削除する」は、インテント設定**削除 PhysicalDisk**と呼ばれる、正常性の状態を維持し、削除操作が失敗した場合は、回復を許可するには保存されます。 以下のメソッドのいずれかで正常に、OperationalStatus を手動で変更できます。

- プールから物理ディスクを削除し、もう一度追加します。
- 意図をオフに[クリア PhysicalDiskHealthData.ps1 スクリプト](https://go.microsoft.com/fwlink/?linkid=2034205)を実行します。 (としてダウンロード用に提供します。TXT ファイルです。 として保存する必要があります、します。PS1 前にファイルを実行できます。)

スクリプトを実行する方法を示す例をいくつか示します。

- 正常に設定するのに必要があるディスクを指定するのにには、 **SerialNumber**パラメーターを使用します。 **WMI MSFT_PhysicalDisk**または**Get-physicaldisk**からシリアル番号を取得できます。 (だけを使用します 0 秒以下のシリアル番号の。)
   
   ```powershell
   Clear-PhysicalDiskHealthData -Intent -Policy -SerialNumber 000000000000000 -Verbose -Force
    ```

- **UniqueId**パラメーターを使用して、(もう一度**WMI MSFT_PhysicalDisk**または**Get-physicaldisk**) からディスクを指定します。

   ```powershell
   Clear-PhysicalDiskHealthData -Intent -Policy -UniqueId 00000000000000000 -Verbose -Force
   ```

## ファイルのコピーが遅い

ファイル エクスプ ローラーを使用して、仮想ディスクに大規模な VHD をコピーする問題を認識する可能性があります: ファイルのコピーが予想より長い時間がかかっています。

エクスプ ローラーを使って、仮想ディスクに大規模な VHD をコピーするには、Robocopy または Xcopy はありませんに推奨される方法このに予想されるパフォーマンスよりも遅くなります。 コピー プロセスは、低い数値含まれる場合は、記憶域スタックの代わりにローカル コピー プロセスのように見え、動作しますが、記憶域スペース ダイレクトのスタックを通過しません。

VMFleet と Diskspd を使用して負荷とストレス テストをお勧めします記憶域スペース ダイレクトのパフォーマンスをテストする場合は、サーバー ベースのラインを取得し、記憶域スペース ダイレクトのパフォーマンスへの期待を設定します。

## 表示される他のノードのノードの再起動時にイベントが必要です。 

これらのイベントを無視しても安全です。 

    Event ID 205: Windows lost communication with physical disk {XXXXXXXXXXXXXXXXXXXX }. This can occur if a cable failed or was disconnected, or if the disk itself failed. 

    Event ID 203: Windows lost communication with physical disk {xxxxxxxxxxxxxxxxxxxxxxxx }. This can occur if a cable failed or was disconnected, or if the disk itself failed. 

Azure Vm を実行している場合は、このイベントを無視することができます。

    Event ID 32: The driver detected that the device \Device\Harddisk5\DR5 has its write cache enabled. Data corruption may occur. 
    
## パフォーマンスが低下または"、"通信"IO Error,"「デタッチ」または「いいえ冗長性」エラー展開では Intel P3x00 NVMe デバイスを使用します。

「メンテナンス リリース 8」の前に、ファームウェアのバージョンと NVM Express (NVMe) デバイスの Intel P3x00 ファミリに基づくハードウェアを使用している一部の記憶域スペース ダイレクト ユーザーに影響する重大な問題を特定します 

>[!NOTE]
> 個々 の Oem は、Intel P3x00 ファミリの NVMe デバイス固有のファームウェア バージョン文字列に基づくデバイスでがあります。 最新のファームウェアのバージョンの詳細については、OEM がお問い合わせください。

利用可能な最新のファームウェアをすぐに適用することをお勧めする場合は、Intel P3x00 ファミリの NVMe デバイスに基づく展開では、ハードウェアを使っている場合 (少なくともメンテナンス リリース 8)。 この[Microsoft サポートの記事](https://support.microsoft.com/en-us/help/4052341/slow-performance-or-lost-communication-io-error-detached-or-no-redunda)では、この問題に関する追加情報を提供します。 
