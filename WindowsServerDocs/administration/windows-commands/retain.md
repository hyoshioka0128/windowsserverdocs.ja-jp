---
title: retain
description: 参照記事 * * * *-
ms.topic: article
ms.assetid: eeab0aef-2ba5-441a-a10d-bbef6f0d7e3e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9a0205f3b67bd99ca590c7ffc6fbd04b0eefd94f
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87883640"
---
# <a name="retain"></a>retain



ブートとして使用する既存のダイナミック シンプル ボリュームまたはシステム ボリュームを準備します。

## <a name="syntax"></a>構文

```
retain
```

## <a name="remarks"></a>Remarks

-   マスター ブート レコード (MBR) ダイナミック ディスクでは、このコマンドは、マスター ブート レコードにパーティション エントリを作成します。
-   GUID パーティション テーブル (GPT) ダイナミック ディスク上は、このコマンドは、GUID パーティション テーブルにパーティション エントリを作成します。

## <a name="additional-references"></a>その他の参照情報

