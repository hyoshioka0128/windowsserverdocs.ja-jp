---
title: Windows エラー報告を使用したフェールオーバークラスターのトラブルシューティング
description: WER レポートを使用したフェールオーバークラスターのトラブルシューティング。レポートを収集して一般的な問題を診断する方法の詳細については、「」を確認してください。
keywords: フェールオーバークラスター、WER レポート、診断、クラスター、Windows エラー報告
ms.prod: windows-server
ms.technology: storage-failover-clustering
ms.author: vpetter
ms.topic: article
author: vpetter
ms.date: 03/27/2018
ms.localizationpriority: ''
ms.openlocfilehash: 46c633af8cf82ac43d2a787a7193685d88ad0ecc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361009"
---
# <a name="troubleshooting-a-failover-cluster-using-windows-error-reporting"></a>Windows エラー報告を使用したフェールオーバークラスターのトラブルシューティング 

> 適用対象:Windows Server 2019、Windows Server 2016、Windows Server

Windows エラー報告 (WER) は、高度な管理者または階層3のサポートが Windows によって検出された情報を収集し、マイクロソフトに報告するために役立つ、柔軟なイベントベースのフィードバックインフラストラクチャです。とは、使用可能な任意のソリューションをユーザーに提供します。 この[リファレンス](https://docs.microsoft.com/powershell/module/windowserrorreporting/)では、すべての WindowsErrorReporting コマンドレットの説明と構文について説明します。

以下に示すトラブルシューティングの情報は、エスカレートされた高度な問題のトラブルシューティングに役立ちます。また、トリアージのためにデータをマイクロソフトに送信することが必要になる場合もあります。

## <a name="enabling-event-channels"></a>イベントチャネルの有効化

Windows Server をインストールすると、多くのイベントチャネルが既定で有効になります。 しかし、問題を診断する際には、システムの問題のトリアージと診断に役立つことがあるため、これらのイベントチャネルの一部を有効にすることが必要になる場合があります。

必要に応じて、クラスター内の各サーバーノードで追加のイベントチャネルを有効にすることができます。ただし、このアプローチには2つの問題があります。

1. クラスターに追加するすべての新しいサーバーノードで同じイベントチャネルを有効にする必要があります。
2. 診断時には、特定のイベントチャネルを有効にし、エラーを再現し、根本原因になるまでこのプロセスを繰り返すことが面倒な場合があります。

これらの問題を回避するには、クラスターの起動時にイベントチャネルを有効にします。 クラスターで有効になっているイベントチャネルの一覧は、パブリックプロパティ**EnabledEventLogs**を使用して構成できます。 既定では、次のイベントチャネルが有効になっています。

```powershell
PS C:\Windows\system32> (get-cluster).EnabledEventLogs
```

この場合の出力例を以下に示します。
```
Microsoft-Windows-Hyper-V-VmSwitch-Diagnostic,4,0xFFFFFFFD
Microsoft-Windows-SMBDirect/Debug,4
Microsoft-Windows-SMBServer/Analytic
Microsoft-Windows-Kernel-LiveDump/Analytic
```

**EnabledEventLogs**プロパティは、次の形式の文字列です。各文字列は、**チャネル名、ログレベル、キーワードマスク**の形式です。 **キーワードマスク**には、16進数 (プレフィックス 0x)、8進数 (プレフィックス 0)、または10進数 (プレフィックスなし) の番号を指定できます。 たとえば、新しいイベントチャネルを一覧に追加し、**ログレベル**と**キーワードマスクの**両方を構成するには、次のように実行します。

```powershell
(get-cluster).EnabledEventLogs += "Microsoft-Windows-WinINet/Analytic,2,321"
```

**ログレベル**を設定するが、既定値では**キーワードマスク**をそのまま使用する場合は、次のコマンドのいずれかを使用できます。

```powershell
(get-cluster).EnabledEventLogs += "Microsoft-Windows-WinINet/Analytic,2"
(get-cluster).EnabledEventLogs += "Microsoft-Windows-WinINet/Analytic,2,"
```

**ログレベル**を既定値のままにしておき、**キーワードマスク**を設定する場合は、次のコマンドを実行します。

```powershell
(get-cluster).EnabledEventLogs += "Microsoft-Windows-WinINet/Analytic,,0xf1"
```

**ログレベル**と**キーワードマスク**の両方を既定値で保持する場合は、次のコマンドのいずれかを実行します。

```powershell
(get-cluster).EnabledEventLogs += "Microsoft-Windows-WinINet/Analytic"
(get-cluster).EnabledEventLogs += "Microsoft-Windows-WinINet/Analytic,"
(get-cluster).EnabledEventLogs += "Microsoft-Windows-WinINet/Analytic,,"
```

これらのイベントチャネルは、クラスターサービスの開始時または**EnabledEventLogs**プロパティが変更されたときに、すべてのクラスターノードで有効になります。

## <a name="gathering-logs"></a>ログの収集

イベントチャネルを有効にした後、 **DumpLogQuery**を使用してログを収集できます。 パブリックリソースの種類のプロパティ**DumpLogQuery**は mutistring の値です。 各文字列は、[ここで説明する XPATH クエリ](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85).aspx)です。

トラブルシューティングを行うときに、追加のイベントチャネルを収集する必要がある場合は、追加のクエリを追加したり、一覧を変更したりして、 **DumpLogQuery**プロパティを変更できます。

これを行うには、[まず、次のよう](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Diagnostics/Get-WinEvent?view=powershell-5.1)に使用して、XPATH クエリをテストします。

```powershell
get-WinEvent -FilterXML "<QueryList><Query><Select Path='Microsoft-Windows-GroupPolicy/Operational'>*[System[TimeCreated[timediff(@SystemTime) &gt;= 600000]]]</Select></Query></QueryList>"
```

次に、リソースの**DumpLogQuery**プロパティにクエリを追加します。

```powershell
(Get-ClusterResourceType -Name "Physical Disk".DumpLogQuery += "<QueryList><Query><Select Path='Microsoft-Windows-GroupPolicy/Operational'>*[System[TimeCreated[timediff(@SystemTime) &gt;= 600000]]]</Select></Query></QueryList>"
```

使用するクエリの一覧を取得するには、次のように実行します。
```powershell
(Get-ClusterResourceType -Name "Physical Disk").DumpLogQuery
```

## <a name="gathering-windows-error-reporting-reports"></a>Windows エラー報告レポートの収集

Windows エラー報告レポートは **%ProgramData%\Microsoft\Windows\WER**に格納されます。

**WER**フォルダー内のレポートに**は、Watson**にアップロードされるのを待機しているレポートが含まれています。

```powershell
PS C:\Windows\system32> dir c:\ProgramData\Microsoft\Windows\WER\ReportQueue
```

この場合の出力例を以下に示します。
```
Volume in drive C is INSTALLTO
Volume Serial Number is 4031-E397

Directory of C:\ProgramData\Microsoft\Windows\WER\ReportQueue

<date>  <time>    <DIR>          .
<date>  <time>    <DIR>          ..
<date>  <time>    <DIR>          Critical_Physical Disk_1cbd8ffecbc8a1a0e7819e4262e3ece2909a157a_00000000_02d10a3f
<date>  <time>    <DIR>          Critical_Physical Disk_1cbd8ffecbc8a1a0e7819e4262e3ece2909a157a_00000000_0588dd06
<date>  <time>    <DIR>          Critical_Physical Disk_1cbd8ffecbc8a1a0e7819e4262e3ece2909a157a_00000000_10d55ef5
<date>  <time>    <DIR>          Critical_Physical Disk_1cbd8ffecbc8a1a0e7819e4262e3ece2909a157a_00000000_13258c8c
<date>  <time>    <DIR>          Critical_Physical Disk_1cbd8ffecbc8a1a0e7819e4262e3ece2909a157a_00000000_13a8c4ac
<date>  <time>    <DIR>          Critical_Physical Disk_1cbd8ffecbc8a1a0e7819e4262e3ece2909a157a_00000000_13dcf4d3
<date>  <time>    <DIR>          Critical_Physical Disk_1cbd8ffecbc8a1a0e7819e4262e3ece2909a157a_00000000_1721a0b0
<date>  <time>    <DIR>          Critical_Physical Disk_1cbd8ffecbc8a1a0e7819e4262e3ece2909a157a_00000000_1839758a
<date>  <time>    <DIR>          Critical_Physical Disk_1cbd8ffecbc8a1a0e7819e4262e3ece2909a157a_00000000_1d4131cb
<date>  <time>    <DIR>          Critical_Physical Disk_1cbd8ffecbc8a1a0e7819e4262e3ece2909a157a_00000000_23551d79
<date>  <time>    <DIR>          Critical_Physical Disk_1cbd8ffecbc8a1a0e7819e4262e3ece2909a157a_00000000_2468ad4c
<date>  <time>    <DIR>          Critical_Physical Disk_1cbd8ffecbc8a1a0e7819e4262e3ece2909a157a_00000000_255d4d61
<date>  <time>    <DIR>          Critical_Physical Disk_1cbd8ffecbc8a1a0e7819e4262e3ece2909a157a_00000000_cab_08289734
<date>  <time>    <DIR>          Critical_Physical Disk_64acaf7e4590828ae8a3ac3c8b31da9a789586d4_00000000_cab_1d94712e
<date>  <time>    <DIR>          Critical_Physical Disk_ae39f5243a104f21ac5b04a39efeac4c126754_00000000_003359cb
<date>  <time>    <DIR>          Critical_Physical Disk_ae39f5243a104f21ac5b04a39efeac4c126754_00000000_cab_1b293b17
<date>  <time>    <DIR>          Critical_Physical Disk_b46b8883d892cfa8a26263afca228b17df8133d_00000000_cab_08abc39c
<date>  <time>    <DIR>          Kernel_166_1234dacd2d1a219a3696b6e64a736408fc785cc_00000000_cab_19c8a127
               0 File(s)              0 bytes
              20 Dir(s)  23,291,658,240 bytes free
```

**WER**フォルダー内に、レポート**アーカイブ**フォルダーには、既に Watson にアップロードされているレポートが含まれています。 これらのレポートのデータは削除されますが、**レポートの wer**ファイルは保持されます。

```powershell
PS C:\Windows\system32> dir C:\ProgramData\Microsoft\Windows\WER\ReportArchive
```

この場合の出力例を以下に示します。
```
Volume in drive C is INSTALLTO
Volume Serial Number is 4031-E397

Directory of c:\ProgramData\Microsoft\Windows\WER\ReportArchive

<date>  <time>    <DIR>          .
<date>  <time>    <DIR>          ..
<date>  <time>    <DIR>          Critical_powershell.exe_7dd54f49935ce48b2dd99d1c64df29a5cfb73db_00000000_cab_096cc802
               0 File(s)              0 bytes
               3 Dir(s)  23,291,658,240 bytes free

```

Windows エラー報告には、問題レポートのエクスペリエンスをカスタマイズするための多くの設定が用意されています。 詳細については、Windows エラー報告の[ドキュメント](https://msdn.microsoft.com/library/windows/desktop/bb513638(v=vs.85).aspx)を参照してください。


## <a name="troubleshooting-using-windows-error-reporting-reports"></a>Windows エラー報告レポートの使用に関するトラブルシューティング

### <a name="physical-disk-failed-to-come-online"></a>物理ディスクをオンラインにできませんでした

この問題を診断するには、WER レポートフォルダーに移動します。

```powershell
PS C:\Windows\system32> dir C:\ProgramData\Microsoft\Windows\WER\ReportArchive\Critical_PhysicalDisk_b46b8883d892cfa8a26263afca228b17df8133d_00000000_cab_08abc39c
```

この場合の出力例を以下に示します。
```
Volume in drive C is INSTALLTO
Volume Serial Number is 4031-E397

<date>  <time>    <DIR>          .
<date>  <time>    <DIR>          ..
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_1.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_10.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_11.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_12.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_13.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_14.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_15.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_16.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_17.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_18.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_19.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_2.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_20.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_21.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_22.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_23.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_24.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_25.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_26.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_27.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_28.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_29.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_3.evtx
<date>  <time>         1,118,208 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_30.evtx
<date>  <time>         1,118,208 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_31.evtx
<date>  <time>         1,118,208 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_32.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_33.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_34.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_35.evtx
<date>  <time>         2,166,784 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_36.evtx
<date>  <time>         1,118,208 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_37.evtx
<date>  <time>            33,194 Report.wer
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_38.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_39.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_4.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_40.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_41.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_5.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_6.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_7.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_8.evtx
<date>  <time>            69,632 CLUSWER_RHS_ERROR_8d06c544-47a4-4396-96ec-af644f45c70a_9.evtx
<date>  <time>             7,382 WERC263.tmp.WERInternalMetadata.xml
<date>  <time>            59,202 WERC36D.tmp.csv
<date>  <time>            13,340 WERC38D.tmp.txt
```

次に、**レポートの wer**ファイルからトリアージを開始します。これにより、失敗したことがわかります。

```
EventType=Failover_clustering_resource_error 
<skip>
Sig[0].Name=ResourceType
Sig[0].Value=Physical Disk
Sig[1].Name=CallType
Sig[1].Value=ONLINERESOURCE
Sig[2].Name=RHSCallResult
Sig[2].Value=5018
Sig[3].Name=ApplicationCallResult
Sig[3].Value=999
Sig[4].Name=DumpPolicy
Sig[4].Value=5225058577
DynamicSig[1].Name=OS Version
DynamicSig[1].Value=10.0.17051.2.0.0.400.8
DynamicSig[2].Name=Locale ID
DynamicSig[2].Value=1033
DynamicSig[27].Name=ResourceName
DynamicSig[27].Value=Cluster Disk 10
DynamicSig[28].Name=ReportId
DynamicSig[28].Value=8d06c544-47a4-4396-96ec-af644f45c70a
DynamicSig[29].Name=FailureTime
DynamicSig[29].Value=2017//12//12-22:38:05.485
```

リソースをオンラインにできなかったため、ダンプは収集されませんでしたが、Windows エラー報告レポートはログを収集しました。 Microsoft Message Analyzer を使用してすべての .evtx ファイルを開くと、システムチャネル、アプリケーションチャネル、フェールオーバークラスター診断チャネル、およびその他のクエリを使用して収集されたすべての情報が表示されます **。** 汎用チャネル。

```powershell
PS C:\Windows\system32> (Get-ClusterResourceType -Name "Physical Disk").DumpLogQuery
```

この場合の出力例を以下に示します。
```
<QueryList><Query Id="0"><Select Path="Microsoft-Windows-Kernel-PnP/Configuration">*[System[TimeCreated[timediff(@SystemTime) &lt;= 600000]]]</Select></Query></QueryList>
<QueryList><Query Id="0"><Select Path="Microsoft-Windows-ReFS/Operational">*[System[TimeCreated[timediff(@SystemTime) &lt;= 600000]]]</Select></Query></QueryList>
<QueryList><Query Id="0"><Select Path="Microsoft-Windows-Ntfs/Operational">*[System[TimeCreated[timediff(@SystemTime) &lt;= 600000]]]</Select></Query></QueryList>
<QueryList><Query Id="0"><Select Path="Microsoft-Windows-Ntfs/WHC">*[System[TimeCreated[timediff(@SystemTime) &lt;= 600000]]]</Select></Query></QueryList>
<QueryList><Query Id="0"><Select Path="Microsoft-Windows-Storage-Storport/Operational">*[System[TimeCreated[timediff(@SystemTime) &lt;= 600000]]]</Select></Query></QueryList>
<QueryList><Query Id="0"><Select Path="Microsoft-Windows-Storage-Storport/Health">*[System[TimeCreated[timediff(@SystemTime) &lt;= 600000]]]</Select></Query></QueryList>
<QueryList><Query Id="0"><Select Path="Microsoft-Windows-Storage-Storport/Admin">*[System[TimeCreated[timediff(@SystemTime) &lt;= 600000]]]</Select></Query></QueryList>
<QueryList><Query Id="0"><Select Path="Microsoft-Windows-Storage-ClassPnP/Operational">*[System[TimeCreated[timediff(@SystemTime) &lt;= 600000]]]</Select></Query></QueryList>
<QueryList><Query Id="0"><Select Path="Microsoft-Windows-Storage-ClassPnP/Admin">*[System[TimeCreated[timediff(@SystemTime) &lt;= 600000]]]</Select></Query></QueryList>
<QueryList><Query Id="0"><Select Path="Microsoft-Windows-PersistentMemory-ScmBus/Certification">*[System[TimeCreated[timediff(@SystemTime) &lt;= 86400000]]]</Select></Query></QueryList>
<QueryList><Query Id="0"><Select Path="Microsoft-Windows-PersistentMemory-ScmBus/Operational">*[System[TimeCreated[timediff(@SystemTime) &lt;= 600000]]]</Select></Query></QueryList>
<QueryList><Query Id="0"><Select Path="Microsoft-Windows-PersistentMemory-PmemDisk/Operational">*[System[TimeCreated[timediff(@SystemTime) &lt;= 600000]]]</Select></Query></QueryList>
<QueryList><Query Id="0"><Select Path="Microsoft-Windows-PersistentMemory-NvdimmN/Operational">*[System[TimeCreated[timediff(@SystemTime) &lt;= 600000]]]</Select></Query></QueryList>
<QueryList><Query Id="0"><Select Path="Microsoft-Windows-PersistentMemory-INvdimm/Operational">*[System[TimeCreated[timediff(@SystemTime) &lt;= 600000]]]</Select></Query></QueryList>
<QueryList><Query Id="0"><Select Path="Microsoft-Windows-PersistentMemory-VirtualNvdimm/Operational">*[System[TimeCreated[timediff(@SystemTime) &lt;= 600000]]]</Select></Query></QueryList>
<QueryList><Query Id="0"><Select Path="Microsoft-Windows-Storage-Disk/Admin">*[System[TimeCreated[timediff(@SystemTime) &lt;= 600000]]]</Select></Query></QueryList>
<QueryList><Query Id="0"><Select Path="Microsoft-Windows-Storage-Disk/Operational">*[System[TimeCreated[timediff(@SystemTime) &lt;= 600000]]]</Select></Query></QueryList>
<QueryList><Query Id="0"><Select Path="Microsoft-Windows-ScmDisk0101/Operational">*[System[TimeCreated[timediff(@SystemTime) &lt;= 600000]]]</Select></Query></QueryList>
<QueryList><Query Id="0"><Select Path="Microsoft-Windows-Partition/Diagnostic">*[System[TimeCreated[timediff(@SystemTime) &lt;= 600000]]]</Select></Query></QueryList>
<QueryList><Query Id="0"><Select Path="Microsoft-Windows-Volume/Diagnostic">*[System[TimeCreated[timediff(@SystemTime) &lt;= 600000]]]</Select></Query></QueryList>
<QueryList><Query Id="0"><Select Path="Microsoft-Windows-VolumeSnapshot-Driver/Operational">*[System[TimeCreated[timediff(@SystemTime) &lt;= 600000]]]</Select></Query></QueryList>
<QueryList><Query Id="0"><Select Path="Microsoft-Windows-FailoverClustering-Clusport/Operational">*[System[TimeCreated[timediff(@SystemTime) &lt;= 600000]]]</Select></Query></QueryList>
<QueryList><Query Id="0"><Select Path="Microsoft-Windows-FailoverClustering-ClusBflt/Operational">*[System[TimeCreated[timediff(@SystemTime) &lt;= 600000]]]</Select></Query></QueryList>
<QueryList><Query Id="0"><Select Path="Microsoft-Windows-StorageSpaces-Driver/Diagnostic">*[System[TimeCreated[timediff(@SystemTime) &lt;= 600000]]]</Select></Query></QueryList>
<QueryList><Query Id="0"><Select Path="Microsoft-Windows-StorageManagement/Operational">*[System[TimeCreated[timediff(@SystemTime) &lt;= 86400000]]]</Select></Query></QueryList>
<QueryList><Query Id="0"><Select Path="Microsoft-Windows-StorageSpaces-Driver/Operational">*[System[TimeCreated[timediff(@SystemTime) &lt;= 600000]]]</Select></Query></QueryList>
<QueryList><Query Id="0"><Select Path="Microsoft-Windows-Storage-Tiering/Admin">*[System[TimeCreated[timediff(@SystemTime) &lt;= 600000]]]</Select></Query></QueryList>
<QueryList><Query Id="0"><Select Path="Microsoft-Windows-Hyper-V-VmSwitch-Operational">*[System[TimeCreated[timediff(@SystemTime) &lt;= 600000]]]</Select></Query></QueryList>
<QueryList><Query Id="0"><Select Path="Microsoft-Windows-Hyper-V-VmSwitch-Diagnostic">*[System[TimeCreated[timediff(@SystemTime) &lt;= 600000]]]</Select></Query></QueryList>
```

Message Analyzer を使用すると、プロトコルメッセージングトラフィックをキャプチャ、表示、および分析できます。 また、Windows コンポーネントからのシステムイベントやその他のメッセージをトレースおよび評価することもできます。 [Microsoft Message Analyzer はここから](https://www.microsoft.com/download/details.aspx?id=44226)ダウンロードできます。 メッセージアナライザーにログを読み込むと、ログチャネルから次のプロバイダーとメッセージが表示されます。

![メッセージアナライザーへのログの読み込み](media/troubleshooting-using-WER-reports/loading-logs-into-message-analyzer.png)

プロバイダー別にグループ化して、次のビューを取得することもできます。

![プロバイダー別にグループ化されたログ](media/troubleshooting-using-WER-reports/logs-grouped-by-providers.png)

ディスクが失敗した原因を特定するには、 **FailoverClustering/diagnostics**と**FailoverClustering/DiagnosticVerbose**の下のイベントに移動します。 その後、次のクエリを実行します。**EventData ["LogString"] に "Cluster Disk 10" が含まれて**います。  これにより、次の出力が得られます。

![実行中のログクエリの出力](media/troubleshooting-using-WER-reports/output-of-running-log-query.png)


### <a name="physical-disk-timed-out"></a>物理ディスクがタイムアウトしました

この問題を診断するには、WER レポートフォルダーに移動します。 このフォルダーには、次に示すように、 **RHS**、 **resgen.exe、および**"**smphost**" サービスをホストするプロセスのログファイルとダンプファイルが含まれています。

```powershell
PS C:\Windows\system32> dir C:\ProgramData\Microsoft\Windows\WER\ReportArchive\Critical_PhysicalDisk_64acaf7e4590828ae8a3ac3c8b31da9a789586d4_00000000_cab_1d94712e
```

この場合の出力例を以下に示します。
```
Volume in drive C is INSTALLTO
Volume Serial Number is 4031-E397

<date>  <time>    <DIR>          .
<date>  <time>    <DIR>          ..
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_1.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_10.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_11.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_12.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_13.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_14.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_15.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_16.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_17.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_18.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_19.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_2.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_20.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_21.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_22.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_23.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_24.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_25.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_26.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_27.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_28.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_29.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_3.evtx
<date>  <time>         1,118,208 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_30.evtx
<date>  <time>         1,118,208 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_31.evtx
<date>  <time>         1,118,208 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_32.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_33.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_34.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_35.evtx
<date>  <time>         2,166,784 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_36.evtx
<date>  <time>         1,118,208 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_37.evtx
<date>  <time>        28,340,500 memory.hdmp
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_38.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_39.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_4.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_40.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_41.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_5.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_6.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_7.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_8.evtx
<date>  <time>            69,632 CLUSWER_RHS_HANG_75e60318-50c9-41e4-94d9-fb0f589cd224_9.evtx
<date>  <time>         4,466,943 minidump.0f14.mdmp
<date>  <time>         1,735,776 minidump.2200.mdmp
<date>  <time>            33,890 Report.wer
<date>  <time>            49,267 WER69FA.tmp.mdmp
<date>  <time>             5,706 WER70A2.tmp.WERInternalMetadata.xml
<date>  <time>            63,206 WER70E0.tmp.csv
<date>  <time>            13,340 WER7100.tmp.txt
```

次に、**レポートの wer**ファイルからトリアージを開始します。これにより、どの呼び出しまたはリソースがハングしているかがわかります。

```
EventType=Failover_clustering_resource_timeout_2
<skip>
Sig[0].Name=ResourceType
Sig[0].Value=Physical Disk
Sig[1].Name=CallType
Sig[1].Value=ONLINERESOURCE
Sig[2].Name=DumpPolicy
Sig[2].Value=5225058577
Sig[3].Name=ControlCode
Sig[3].Value=18
DynamicSig[1].Name=OS Version
DynamicSig[1].Value=10.0.17051.2.0.0.400.8
DynamicSig[2].Name=Locale ID
DynamicSig[2].Value=1033
DynamicSig[26].Name=ResourceName
DynamicSig[26].Value=Cluster Disk 10
DynamicSig[27].Name=ReportId
DynamicSig[27].Value=75e60318-50c9-41e4-94d9-fb0f589cd224
DynamicSig[29].Name=HangThreadId
DynamicSig[29].Value=10008
```

ダンプで収集するサービスとプロセスの一覧は、次のプロパティによって制御されます。**PS C:\Windows\system32 > (Get ClusterResourceType-Name "Physical Disk")。DumpServicesSmphost**

ハングが発生した原因を特定するには、dum ファイルを開きます。 その後、次のクエリを実行します。**EventData ["LogString"] に "Cluster Disk 10" が含まれています。** これにより、次の出力が得られます。

![実行中のログクエリ2の出力](media/troubleshooting-using-WER-reports/output-of-running-log-query-2.png)

このことは、次のように、メモリの**hdmp**ファイルのスレッドでクロス検証できます。

```
# 21  Id: 1d98.2718 Suspend: 0 Teb: 0000000b`f1f7b000 Unfrozen
# Child-SP          RetAddr           Call Site
00 0000000b`f3c7ec38 00007ff8`455d25ca ntdll!ZwDelayExecution+0x14 
01 0000000b`f3c7ec40 00007ff8`2ef19710 KERNELBASE!SleepEx+0x9a 
02 0000000b`f3c7ece0 00007ff8`3bdf7fbf clusres!ResHardDiskOnlineOrTurnOffMMThread+0x2b0 
03 0000000b`f3c7f960 00007ff8`391eed34 resutils!ClusWorkerStart+0x5f 
04 0000000b`f3c7f9d0 00000000`00000000 vfbasics+0xed34
```