---
title: bitsadmin の例
description: Bitsadmin ツールを使用して最も一般的なタスクを実行する方法を示す例。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: cb8f8374-ba6e-4a68-85a1-9a95b8215354
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 05/31/2018
ms.openlocfilehash: 1db9dd387d7b9cc39c582ce79e5163c83579b613
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83819632"
---
# <a name="bitsadmin-examples"></a>bitsadmin の例

次の例は、ツールを使用して最も一般的なタスクを実行する方法を示して `bitsadmin` います。

## <a name="transfer-a-file"></a>ファイルの転送

ジョブを作成するには、ファイルを追加し、転送キューでジョブをアクティブ化して、ジョブを完了します。

`bitsadmin /transfer myDownloadJob /download /priority normal https://downloadsrv/10mb.zip c:\\10mb.zip`

BITSAdmin は、転送が完了するかエラーが発生するまで、MS-DOS ウィンドウに進行状況の情報を表示し続けます。

## <a name="create-a-download-job"></a>ダウンロードジョブを作成する

*Mydownloadjob*という名前のダウンロードジョブを作成するには、次のようにします。

```
bitsadmin /create myDownloadJob
```

BITSAdmin は、ジョブを一意に識別する GUID を返します。 その後の呼び出しでは、GUID またはジョブ名を使用します。 次のテキストはサンプル出力です。

### <a name="sample-output"></a>サンプル出力

`created job {C775D194-090F-431F-B5FB-8334D00D1CB6}`

## <a name="add-files-to-the-download-job"></a>ダウンロードジョブにファイルを追加する

ジョブにファイルを追加するには、次のようにします。

```
bitsadmin /addfile myDownloadJob https://downloadsrv/10mb.zip c:\\10mb.zip
```

追加するファイルごとにこの呼び出しを繰り返します。 複数のジョブが*Mydownloadjob*を名前として使用している場合は、ジョブの GUID を使用して、ジョブの完了を一意に識別する必要があります。

## <a name="activate-the-download-job"></a>ダウンロードジョブのアクティブ化

新しいジョブを作成すると、BITS によって自動的にジョブが中断されます。 転送キューでジョブをアクティブ化するには:

```
bitsadmin /resume myDownloadJob
```

複数のジョブが*Mydownloadjob*を名前として使用している場合は、ジョブの GUID を使用して、ジョブの完了を一意に識別する必要があります。

## <a name="determine-the-progress-of-the-download-job"></a>ダウンロードジョブの進行状況を確認する

**/Info**スイッチは、ジョブの状態と転送されたファイルの数とバイト数を返します。 状態がと表示されている場合は、BITS によって `TRANSFERRED` ジョブ内のすべてのファイルが正常に転送されたことを意味します。 また、 **/verbose**引数を追加してジョブの完全な詳細情報を取得し、 **/list**または **/monitor**を追加して、転送キュー内のすべてのジョブを取得することもできます。

ジョブの状態を取得するには、次のようにします。

```
bitsadmin /info myDownloadJob /verbose
```

複数のジョブが*Mydownloadjob*を名前として使用している場合は、ジョブの GUID を使用して、ジョブの完了を一意に識別する必要があります。

## <a name="complete-the-download-job"></a>ダウンロードジョブの完了

状態の変更後にジョブを完了するには、次の手順を実行し `TRANSFERRED` ます。

```
bitsadmin /complete myDownloadJob
```

このスイッチは、 `/complete` ジョブ内のファイルが使用可能になる前に実行する必要があります。 複数のジョブが*Mydownloadjob*を名前として使用している場合は、ジョブの GUID を使用して、ジョブの完了を一意に識別する必要があります。

## <a name="monitor-jobs-in-the-transfer-queue-using-the-list-switch"></a>/List スイッチを使用して転送キュー内のジョブを監視する

ジョブの状態と転送キュー内のすべてのジョブについて転送されたファイル数およびバイト数を返すには、次のようにします。

```
bitsadmin /list
```

### <a name="sample-output"></a>サンプル出力

```
{6AF46E48-41D3-453F-B7AF-A694BBC823F7} job1 SUSPENDED 0 / 0 0 / 0
{482FCAF0-74BF-469B-8929-5CCD028C9499} job2 TRANSIENT_ERROR 0 / 1 0 / UNKNOWN

Listed 2 job(s).
```

## <a name="monitor-jobs-in-the-transfer-queue-using-the-monitor-switch"></a>/モニタースイッチを使用して転送キュー内のジョブを監視する

ジョブの状態と転送キュー内のすべてのジョブについて転送されたファイル数およびバイト数を返すには、5秒ごとにデータを更新します。

```
bitsadmin /monitor
```

> [!NOTE]
> 更新を停止するには、CTRL + C キーを押します。

### <a name="sample-output"></a>サンプル出力

```
MONITORING BACKGROUND COPY MANAGER(5 second refresh)
{6AF46E48-41D3-453F-B7AF-A694BBC823F7} job1 SUSPENDED 0 / 0 0 / 0
{482FCAF0-74BF-469B-8929-5CCD028C9499} job2 TRANSIENT_ERROR 0 / 1 0 / UNKNOWN
{0B138008-304B-4264-B021-FD04455588FF} job3 TRANSFERRED 1 / 1 100379370 / 100379370
```

## <a name="monitor-jobs-in-the-transfer-queue-using-the-info-switch"></a>/Info スイッチを使用して転送キュー内のジョブを監視する

ジョブの状態と転送されたファイル数およびバイト数を返すには、次のようにします。

```
bitsadmin /info
```

### <a name="sample-output"></a>サンプル出力

```
GUID: {482FCAF0-74BF-469B-8929-5CCD028C9499} DISPLAY: myDownloadJob
TYPE: DOWNLOAD STATE: TRANSIENT_ERROR OWNER: domain\user
PRIORITY: NORMAL FILES: 0 / 1 BYTES: 0 / UNKNOWN
CREATION TIME: 12/17/2002 1:21:17 PM MODIFICATION TIME: 12/17/2002 1:21:30 PM
COMPLETION TIME: UNKNOWN
NOTIFY INTERFACE: UNREGISTERED NOTIFICATION FLAGS: 3
RETRY DELAY: 600 NO PROGRESS TIMEOUT: 1209600 ERROR COUNT: 0
PROXY USAGE: PRECONFIG PROXY LIST: NULL PROXY BYPASS LIST: NULL
ERROR FILE:    https://downloadsrv/10mb.zip -> c:\10mb.zip
ERROR CODE:    0x80072ee7 - The server name or address could not be resolved
ERROR CONTEXT: 0x00000005 - The error occurred while the remote file was being
processed.
DESCRIPTION:
JOB FILES:
0 / UNKNOWN WORKING https://downloadsrv/10mb.zip -> c:\10mb.zip
NOTIFICATION COMMAND LINE: none
```

## <a name="delete-jobs-from-the-transfer-queue"></a>転送キューからジョブを削除する

転送キューからすべてのジョブを削除するには、/reset スイッチを使用します。

```
bitsadmin /reset
```

### <a name="sample-output"></a>サンプル出力

```
{DC61A20C-44AB-4768-B175-8000D02545B9} canceled.
{BB6E91F3-6EDA-4BB4-9E01-5C5CBB5411F8} canceled.
2 out of 2 jobs canceled.
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
