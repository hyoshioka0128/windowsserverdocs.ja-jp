---
title: bitsadmin monitor
description: Bitsadmin monitor コマンドの参照記事。現在のユーザーが所有している転送キュー内のジョブを監視します。
ms.topic: article
ms.assetid: 2c424d27-e011-49c2-b579-a2c235467c39
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3ba2cb315fb0696b8363506669aa41f1693bb758
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893665"
---
# <a name="bitsadmin-monitor"></a>bitsadmin monitor

現在のユーザーが所有している転送キュー内のジョブを監視します。

## <a name="syntax"></a>構文

```
bitsadmin /monitor [/allusers] [/refresh <seconds>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| /allusers | 省略可能。 すべてのユーザーのジョブを監視します。 このパラメーターを使用するには、管理者特権が必要です。 |
| /更新 | 省略可能。 によって指定された間隔でデータを更新し `<seconds>` ます。 既定の更新間隔は5秒です。 更新を停止するには、CTRL + C キーを押します。 |

## <a name="examples"></a>例

現在のユーザーが所有しているジョブの転送キューを監視し、60秒ごとに情報を更新すること。

```
bitsadmin /monitor /refresh 60
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
