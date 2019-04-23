---
title: bitsadmin util と enableanalyticchannel
description: Windows コマンド」のトピック**bitsadmin util と enableanalyticchannel** - を有効または BITS クライアント分析チャネルを無効にします。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0d7645aa-b91b-4ed7-b630-a1e1be6f6ae9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 814442a4d9b1a4d6e45b28f41a89b7a144be1cbf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877323"
---
# <a name="bitsadmin-util-and-enableanalyticchannel"></a>bitsadmin util と enableanalyticchannel



有効または、BITS クライアント分析チャネルを無効にします。

## <a name="syntax"></a>構文

```
bitsadmin /Util /EnableAnalyticChannel TRUE|FALSE
```

## <a name="BKMK_examples"></a>例

次の例では、BITS クライアント分析チャネルを有効します。
```
C:\>bitsadmin /Util / EnableAnalyticChannel TRUE
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)