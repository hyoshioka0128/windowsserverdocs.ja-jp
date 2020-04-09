---
title: bitsadmin の例
description: 次の例は、bitsadmin ツールを使用して最も一般的なタスクを実行する方法を示しています。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: cb8f8374-ba6e-4a68-85a1-9a95b8215354
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 05/31/2018
ms.openlocfilehash: 96447410f76e4402c456b5ec402cc730480aedaf
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850805"
---
# <a name="bitsadmin-examples"></a>bitsadmin の例

次の例は、`bitsadmin` ツールを使用して最も一般的なタスクを実行する方法を示しています。

## <a name="transfer-a-file"></a>ファイルの転送

**/転送**スイッチは、以下に示すタスクを実行するためのショートカットです。 このスイッチは、ジョブを作成し、ファイルをジョブに追加し、転送キューでジョブをアクティブ化して、ジョブを完了します。 BITSAdmin は、転送が完了するかエラーが発生するまで、MS-DOS ウィンドウに進行状況の情報を表示し続けます。

`bitsadmin /transfer myDownloadJob /download /priority normal https://downloadsrv/10mb.zip c:\\10mb.zip`

## <a name="create-a-download-job"></a>ダウンロードジョブを作成する

**/Create**スイッチを使用して、mydownloadjob という名前のダウンロードジョブを作成します。

### <a name="syntax"></a>構文

```
bitsadmin /create myDownloadJob
```

BITSAdmin は、ジョブを一意に識別する GUID を返します。 その後の呼び出しでは、GUID またはジョブ名を使用します。 次のテキストはサンプル出力です。

#### <a name="sample-output"></a>サンプル出力

`created job {C775D194-090F-431F-B5FB-8334D00D1CB6}`

## <a name="add-files-to-the-download-job"></a>ダウンロードジョブにファイルを追加する

**/Addfile**スイッチを使用して、ジョブにファイルを追加します。 追加するファイルごとにこの呼び出しを繰り返します。

複数のジョブが myDownloadJob を名前として使用する場合は、ジョブを一意に識別するために、myDownloadJob をジョブの GUID に置き換える必要があります。

### <a name="syntax"></a>構文

```
bitsadmin /addfile myDownloadJob https://downloadsrv/10mb.zip c:\\10mb.zip
```

## <a name="activate-the-download-job"></a>ダウンロードジョブのアクティブ化

新しいジョブを作成すると、BITS によってジョブが中断されます。 転送キューでジョブをアクティブ化するには、 **/resume**スイッチを使用します。

複数のジョブが myDownloadJob を名前として使用する場合は、ジョブを一意に識別するために、myDownloadJob をジョブの GUID に置き換える必要があります。

### <a name="syntax"></a>構文

`bitsadmin /resume myDownloadJob`

## <a name="determine-the-progress-of-the-download-job"></a>ダウンロードジョブの進行状況を確認する

**/Info**スイッチを使用して、ジョブの状態と転送されたファイルの数とバイト数を返します。 状態が転送されると、BITS はジョブ内のすべてのファイルを正常に転送しました。

- **/Verbose**引数を使用して、ジョブの詳細を取得します。

- **/List**または **/monitor**スイッチを使用して、転送キュー内のすべてのジョブを取得します。

複数のジョブが myDownloadJob を名前として使用する場合は、ジョブを一意に識別するために、myDownloadJob をジョブの GUID に置き換える必要があります。

### <a name="syntax"></a>構文

`bitsadmin /info myDownloadJob /verbose`

#### <a name="sample-output"></a>サンプル出力

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

## <a name="completing-the-download-job"></a>ダウンロードジョブの完了

ジョブの状態が [転送済み] になると、そのジョブ内のすべてのファイルが BITS によって正常に転送されます。 ただし、 **[完了]** スイッチを使用するまで、ファイルは使用できません。

複数のジョブが myDownloadJob を名前として使用する場合は、ジョブを一意に識別するために、myDownloadJob をジョブの GUID に置き換える必要があります。

### <a name="syntax"></a>構文

`bitsadmin /complete myDownloadJob`

## <a name="monitoring-jobs-in-the-transfer-queue"></a>転送キュー内のジョブの監視

**/List**、 **/monitor**、または **/info**スイッチを使用して、転送キュー内のジョブを監視します。 **/List**スイッチは、キュー内のすべてのジョブに関する情報を提供します。

## <a name="list-switch"></a>/list スイッチ

**/List**スイッチは、ジョブの状態と転送キュー内のすべてのジョブについて転送されたファイルの数およびバイト数を返します。

### <a name="syntax"></a>構文

`bitsadmin /list`

#### <a name="sample-output-for-the-list-switch"></a>/List スイッチのサンプル出力

```
{6AF46E48-41D3-453F-B7AF-A694BBC823F7} job1 SUSPENDED 0 / 0 0 / 0
{482FCAF0-74BF-469B-8929-5CCD028C9499} job2 TRANSIENT_ERROR 0 / 1 0 / UNKNOWN

Listed 2 job(s).
```

## <a name="monitor-switch"></a>/モニタースイッチ

**/モニター**スイッチは、ジョブの状態と転送キュー内のすべてのジョブについて転送されたファイル数とバイト数を返し、データを5秒ごとに更新します。 更新を停止するには、CTRL + C キーを押します。

### <a name="syntax"></a>構文

`bitsadmin /monitor`

#### <a name="sample-output"></a>サンプル出力

```
MONITORING BACKGROUND COPY MANAGER(5 second refresh)
{6AF46E48-41D3-453F-B7AF-A694BBC823F7} job1 SUSPENDED 0 / 0 0 / 0
{482FCAF0-74BF-469B-8929-5CCD028C9499} job2 TRANSIENT_ERROR 0 / 1 0 / UNKNOWN
{0B138008-304B-4264-B021-FD04455588FF} job3 TRANSFERRED 1 / 1 100379370 / 100379370
```

## <a name="deleting-jobs-from-the-transfer-queue"></a>転送キューからジョブを削除しています

転送キューからすべてのジョブを削除するには、 **/リセット**スイッチを使用します。

### <a name="syntax"></a>構文

`bitsadmin /reset`

#### <a name="sample-output"></a>サンプル出力

```
{DC61A20C-44AB-4768-B175-8000D02545B9} canceled.
{BB6E91F3-6EDA-4BB4-9E01-5C5CBB5411F8} canceled.
2 out of 2 jobs canceled.
```
