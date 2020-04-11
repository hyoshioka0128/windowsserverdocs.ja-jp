---
title: bitsadmin util と enableanalytics のチャネル
description: BITS クライアント分析チャネルを有効または無効にする**bitsadmin util および enableanalytics のチャネル**に関する Windows コマンドのトピック。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0d7645aa-b91b-4ed7-b630-a1e1be6f6ae9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f8ff1f835415979036fdc0f8aa637fe693e57d46
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122685"
---
# <a name="bitsadmin-util-and-enableanalyticchannel"></a>bitsadmin util と enableanalytics のチャネル

BITS クライアント分析チャネルを有効または無効にします。

## <a name="syntax"></a>構文

```
bitsadmin /util /enableanalyticchannel TRUE|FALSE
```

| パラメーター | 説明 |
| --------- | ---------- |
| TRUE または FALSE | **TRUE**を指定すると、指定したファイルのコンテンツの検証が有効になり、 **FALSE**の場合は無効になります。 |

## <a name="examples"></a>例

次の例では、BITS クライアント分析チャネルを有効にします。

```
C:\>bitsadmin /util / enableanalyticchannel TRUE
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)