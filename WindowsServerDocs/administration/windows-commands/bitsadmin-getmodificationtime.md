---
title: bitsadmin getmodificationtime
description: Bitsadmin getmodificationtime コマンドの参照記事。ジョブが最後に変更された時刻、またはデータが正常に転送された日時を取得します。
ms.topic: article
ms.assetid: e543945e-92c4-491e-8c2d-344f8a3e342d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d89d3382c738ffc473135579eb58590f06774d5c
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894167"
---
# <a name="bitsadmin-getmodificationtime"></a>bitsadmin getmodificationtime

ジョブが最後に変更された時刻、またはデータが正常に転送された日時を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getmodificationtime <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブの最終更新時刻を取得するには、次のようにします。

```
bitsadmin /getmodificationtime myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
