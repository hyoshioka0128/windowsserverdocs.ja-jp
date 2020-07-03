---
title: bitsadmin getmodificationtime
description: Bitsadmin getmodificationtime コマンドの参照記事。ジョブが最後に変更された時刻、またはデータが正常に転送された日時を取得します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e543945e-92c4-491e-8c2d-344f8a3e342d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9055c0ac70bc2360601ecd1b1f91c8ad3908d704
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928164"
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
