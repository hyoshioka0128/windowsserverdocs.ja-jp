---
title: retain
description: 参照記事 * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: eeab0aef-2ba5-441a-a10d-bbef6f0d7e3e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 958ee0de7bd69c9391407ec6f4a832e1262746a2
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933070"
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

