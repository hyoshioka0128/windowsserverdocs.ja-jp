---
title: 日数
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eeab0aef-2ba5-441a-a10d-bbef6f0d7e3e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3b076e12c833645833f53a06476e62bbf44f2690
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384492"
---
# <a name="retain"></a>日数



ブートとして使用する既存のダイナミック シンプル ボリュームまたはシステム ボリュームを準備します。

## <a name="syntax"></a>構文

```
retain
```

## <a name="remarks"></a>コメント

-   マスター ブート レコード (MBR) ダイナミック ディスクでは、このコマンドは、マスター ブート レコードにパーティション エントリを作成します。
-   GUID パーティション テーブル (GPT) ダイナミック ディスク上は、このコマンドは、GUID パーティション テーブルにパーティション エントリを作成します。

#### <a name="additional-references"></a>その他の参照情報

