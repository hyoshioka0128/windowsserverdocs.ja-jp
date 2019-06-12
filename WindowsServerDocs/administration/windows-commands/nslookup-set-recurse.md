---
title: nslookup set recurse
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d1b7a93f-dfb0-4ccd-b230-e0953057fada
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: de948d9e182cf6489c1869a5725bce8319484293
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436675"
---
# <a name="nslookup-set-recurse"></a>nslookup set recurse



ドメイン ネーム システム (DNS) サーバーに情報があるない場合は、他のサーバーを照会するように指示します。

## <a name="syntax"></a>構文

```
set [no]recurse
```

## <a name="parameters"></a>パラメーター

|   パラメーター   |                                                                  説明                                                                  |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| **norecurse** |                情報があるない場合は、他のサーバーを照会できないドメイン ネーム システム (DNS) のネーム サーバーを停止します。                |
|  **recurse**  | ドメイン ネーム システム (DNS) サーバーに情報があるない場合は、他のサーバーを照会するように指示します。 既定の構文は**recurse**します。 |
|     {0} のヘルプ     |                                                                      ?}                                                                       |

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)