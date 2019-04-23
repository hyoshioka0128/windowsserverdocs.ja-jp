---
title: bitsadmin 例
description: 次の例では、bitsadmin ツールを使用して、最も一般的なタスクを実行する方法を示します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cb8f8374-ba6e-4a68-85a1-9a95b8215354
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 05/31/2018
ms.openlocfilehash: 4b9deb4fc7fbfccf569250e965274009764054f7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849333"
---
# <a name="bitsadmin-examples"></a>bitsadmin 例

次の例を使用する方法を示して、`bitsadmin`ツールで最も一般的なタスクを実行します。

## <a name="transfer-a-file"></a>ファイルを転送します。

**/転送**スイッチは下記のタスクを実行するためのショートカットです。 このスイッチにジョブを作成、ジョブにファイルが追加されます、転送キュー内のジョブがアクティブになります、およびジョブが完了するとします。 BITSAdmin、転送が完了するか、エラーが発生するまで、MS-DOS ウィンドウに進行状況に関する情報を表示し続けます。

**bitsadmin/transfer myDownloadJob/download/priority 通常 https://downloadsrv/10mb.zipc:\\10mb.zip**

## <a name="create-a-download-job"></a>ダウンロード ジョブを作成します。

使用して、 **/create** myDownloadJob をという名前のダウンロード ジョブを作成するスイッチ。

**bitsadmin/myDownloadJob の作成**

BITSAdmin では、ジョブを一意に識別する GUID を返します。 後続の呼び出しで、GUID またはジョブの名前を使用します。 次のテキストは、サンプルの出力を示します。

``` syntax
Created job {C775D194-090F-431F-B5FB-8334D00D1CB6}.
```

次に、使用、 **/addfile**ダウンロード ジョブに 1 つまたは複数のファイルを追加するスイッチ。

## <a name="add-files-to-the-download-job"></a>ダウンロード ジョブにファイルを追加します。

使用して、 **/addfile**ジョブにファイルを追加するスイッチ。 各ファイルを追加するには、この呼び出しを繰り返します。 複数のジョブでは、myDownloadJob を使用して、名前に場合、は、ジョブを一意に識別するために、ジョブの GUID を持つ myDownloadJob を置き換える必要があります。

**bitsadmin/addfile myDownloadJob https://downloadsrv/10mb.zip c:\\10mb.zip**

転送キュー内のジョブを有効にするには、使用、 **/再開**スイッチします。

## <a name="activate-the-download-job"></a>ダウンロード ジョブをアクティブ化します。

新しいジョブを作成するときに、BITS はジョブを中断します。 転送キュー内のジョブを有効にするには、使用、 **/再開**スイッチします。 複数のジョブでは、myDownloadJob を使用して、名前に場合、は、ジョブを一意に識別するために、ジョブの GUID を持つ myDownloadJob を置き換える必要があります。

**bitsadmin/resume myDownloadJob**

ジョブの進行状況を調べるには、 **/list**、 **/info**、または**監視/** スイッチします。

## <a name="determine-the-progress-of-the-download-job"></a>ダウンロード ジョブの進行状況を把握します。

使用して、 **/info**スイッチ、ジョブの進行状況を判断します。 複数のジョブでは、myDownloadJob を使用して、名前に場合、は、ジョブを一意に識別するために、ジョブの GUID を持つ myDownloadJob を置き換える必要があります。

**bitsadmin/info myDownloadJob/verbose**

**/Info**スイッチは、ジョブの状態とファイルの転送されたバイト数を返します。 状態を転送すると、BITS はジョブ内のすべてのファイルを正常に転送が。 **/Verbose**引数は、ジョブの完全な詳細を提供します。 次のテキストは、サンプルの出力を示します。

``` syntax
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

転送キュー内のすべてのジョブの情報を受信するには、使用、 **/list**または**監視/** スイッチします。

## <a name="completing-the-download-job"></a>ダウンロード ジョブの完了

ジョブの状態を転送すると、BITS はジョブのすべてのファイルを正常に転送が。 ただし、ファイルは使用できませんを使用するまで、**完了/** スイッチします。 複数のジョブでは、myDownloadJob を使用して、名前に場合、は、ジョブを一意に識別するために、ジョブの GUID を持つ myDownloadJob を置き換える必要があります。

**bitsadmin myDownloadJob 完了/**

## <a name="monitoring-jobs-in-the-transfer-queue"></a>転送キュー内のジョブの監視

使用して、 **/list**、**監視/**、または **/info**転送キュー内のジョブを監視するスイッチ。 **/List**スイッチは、キュー内のすべてのジョブの情報を提供します。

**bitsadmin/list**

**/List**スイッチは、ジョブの状態とファイルの転送キュー内のすべてのジョブに転送されたバイト数を返します。 次のテキストは、サンプルの出力を示します。

``` syntax
{6AF46E48-41D3-453F-B7AF-A694BBC823F7} job1 SUSPENDED 0 / 0 0 / 0
{482FCAF0-74BF-469B-8929-5CCD028C9499} job2 TRANSIENT_ERROR 0 / 1 0 / UNKNOWN

Listed 2 job(s).
```

使用して、 **監視/** キュー内のすべてのジョブを監視するスイッチ。 **監視/** スイッチは、データを 5 秒ごとに更新します。 更新を停止するには、CTRL キーを押しながら C キーを入力します。

**bitsadmin/monitor**

**監視/** スイッチは、ジョブの状態とファイルの転送キュー内のすべてのジョブに転送されたバイト数を返します。 次のテキストは、サンプルの出力を示します。

``` syntax
MONITORING BACKGROUND COPY MANAGER(5 second refresh)
{6AF46E48-41D3-453F-B7AF-A694BBC823F7} job1 SUSPENDED 0 / 0 0 / 0
{482FCAF0-74BF-469B-8929-5CCD028C9499} job2 TRANSIENT_ERROR 0 / 1 0 / UNKNOWN
{0B138008-304B-4264-B021-FD04455588FF} job3 TRANSFERRED 1 / 1 100379370 / 100379370
```

## <a name="deleting-jobs-from-the-transfer-queue"></a>転送キューからジョブを削除します。

使用して、 **/リセット**転送キューからすべてのジョブを削除するスイッチ。

**bitsadmin /reset**

次のテキストは、サンプルの出力を示します。

``` syntax
{DC61A20C-44AB-4768-B175-8000D02545B9} canceled.
{BB6E91F3-6EDA-4BB4-9E01-5C5CBB5411F8} canceled.
2 out of 2 jobs canceled.
```
