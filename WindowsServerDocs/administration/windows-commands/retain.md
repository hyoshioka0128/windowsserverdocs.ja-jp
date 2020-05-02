---
title: retain
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: eeab0aef-2ba5-441a-a10d-bbef6f0d7e3e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7391c0b60d07cc2eb5a6230b283ac180cc028508
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722340"
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

## <a name="additional-references"></a>その他のリファレンス

