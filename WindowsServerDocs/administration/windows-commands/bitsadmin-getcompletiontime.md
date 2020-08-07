---
title: bitsadmin getcompletiontime
description: Bitsadmin get time コマンドの参照記事。これは、ジョブがデータの転送を終了した時刻を取得します。
ms.topic: article
ms.assetid: 7a4b3c1c-9832-4724-86b2-cce3c01bfa28
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a242ec3689bef6e4ecd2bb961f532efbb874e98c
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894479"
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
