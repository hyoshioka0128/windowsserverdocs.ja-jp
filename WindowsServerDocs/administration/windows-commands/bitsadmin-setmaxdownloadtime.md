---
title: bitsadmin setmaxdownloadtime
description: ダウンロードタイムアウトを秒単位で設定する bitsadmin setmaxdownloadtime コマンドの参照記事。
ms.topic: article
ms.assetid: 16b96cf1-5738-415c-9b9d-c4ea8d5e4fec
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5453c476f304bce3564167da93518793d7eef043
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893120"
---
# <a name="bitsadmin-setmaxdownloadtime"></a>bitsadmin setmaxdownloadtime

ダウンロードタイムアウトを秒単位で設定します。

## <a name="syntax"></a>構文

```
bitsadmin /setmaxdownloadtime <job> <timeout>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| ジョブ (job) | ジョブの表示名または GUID。 |
| timeout | ダウンロードタイムアウトの長さ (秒単位)。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブのタイムアウトを10秒に設定します。

```
bitsadmin /setmaxdownloadtime myDownloadJob 10
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
