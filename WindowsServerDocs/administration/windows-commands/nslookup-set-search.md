---
title: nslookup set search
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 064ac660-8b04-4af9-8b2c-e4e0549771b8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d95ebe30ce45430787bebbfe63766a571a436bbf
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436591"
---
# <a name="nslookup-set-search"></a>nslookup set search



応答が受信されるまでは、ドメインの DNS 検索リストにドメイン ネーム システム (DNS) ドメイン名、要求に追加します。 これは、セット、検索要求を少なくとも 1 つのピリオドを含めるときに適用されますが、末尾のピリオドで終わらない。

## <a name="syntax"></a>構文

```
set [no]search
```

## <a name="parameters"></a>パラメーター

|  パラメーター   |                                                                          説明                                                                          |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **nosearch** |                            要求にドメインの DNS 検索リストにドメイン ネーム システム (DNS) ドメイン名を追加することを停止します。                            |
|  **search**  | 応答が受信されるまでは、ドメインの DNS 検索リストにドメイン ネーム システム (DNS) ドメイン名、要求に追加します。 既定の構文は**検索**します。 |
|    {0} のヘルプ     |                                                                              ?}                                                                               |

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)