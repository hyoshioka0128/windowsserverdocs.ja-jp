---
title: bitsadmin getcompletiontime
description: Bitsadmin get time コマンドのリファレンストピック。これは、ジョブがデータの転送を完了した時刻を取得します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7a4b3c1c-9832-4724-86b2-cce3c01bfa28
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9b3721401e450ae60fb77534f8eb845ff5ac3443
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718116"
---
# <a name="bitsadmin-getcompletiontime"></a>bitsadmin getcompletiontime

ジョブがデータの転送を終了した時刻を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getcompletiontime <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブがデータの転送を終了した時刻を取得するには、次の操作を行います。

```
bitsadmin /getcompletiontime myDownloadJob
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
