---
title: bitsadmin getcompletiontime
description: Bitsadmin get time コマンドの参照記事。これは、ジョブがデータの転送を終了した時刻を取得します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7a4b3c1c-9832-4724-86b2-cce3c01bfa28
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e07dd6a345cd1bd58277ef08e08802a62d6e6772
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923101"
---
# <a name="bitsadmin-getcompletiontime"></a>bitsadmin getcompletiontime

ジョブがデータの転送を終了した時刻を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getcompletiontime <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブがデータの転送を終了した時刻を取得するには、次の操作を行います。

```
bitsadmin /getcompletiontime myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
