---
title: retain
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: eeab0aef-2ba5-441a-a10d-bbef6f0d7e3e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 891192c0d6b1687cf6bffea0f57d1853e023b776
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80835765"
---
# <a name="retain"></a>retain



ブートとして使用する既存のダイナミック シンプル ボリュームまたはシステム ボリュームを準備します。

## <a name="syntax"></a>構文

```
retain
```

## <a name="remarks"></a>コメント

-   マスター ブート レコード (MBR) ダイナミック ディスクでは、このコマンドは、マスター ブート レコードにパーティション エントリを作成します。
-   GUID パーティション テーブル (GPT) ダイナミック ディスク上は、このコマンドは、GUID パーティション テーブルにパーティション エントリを作成します。

## <a name="additional-references"></a>その他の参照情報

