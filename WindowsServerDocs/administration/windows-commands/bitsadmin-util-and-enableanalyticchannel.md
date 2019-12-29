---
title: bitsadmin util と enableanalytics のチャネル
description: '**Bitsadmin util と enableanalytics のチャネル**の Windows コマンドに関するトピック-BITS クライアント分析チャネルを有効または無効にします。'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 2c73c704e0c49c6f8309ce0a5c9646afb3392f79
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380263"
---
# <a name="bitsadmin-util-and-enableanalyticchannel"></a>bitsadmin util と enableanalytics のチャネル



BITS クライアント分析チャネルを有効または無効にします。

## <a name="syntax"></a>構文

```
bitsadmin /Util /EnableAnalyticChannel TRUE|FALSE
```

## <a name="BKMK_examples"></a>例

次の例では、BITS クライアント分析チャネルを有効にします。
```
C:\>bitsadmin /Util / EnableAnalyticChannel TRUE
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)