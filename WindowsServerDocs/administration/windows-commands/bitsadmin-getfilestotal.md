---
title: bitsadmin getfilestotal
description: Bitsadmin getfilestotal コマンドの参照記事。指定されたジョブ内のファイルの数を取得します。
ms.topic: article
ms.assetid: c5de113e-f29c-4cd3-9392-0e300018d516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 09867e5ed8b060f7a9cbfe573c6e98bfbac831df
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894331"
---
# <a name="bitsadmin-getfilestotal"></a>bitsadmin getfilestotal

指定されたジョブ内のファイルの数を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getfilestotal <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブに含まれるファイルの数を取得するには、次のようにします。

```
bitsadmin /getfilestotal myDownloadJob
```

## <a name="see-also"></a>参照

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
