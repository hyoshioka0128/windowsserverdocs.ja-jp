---
title: bitsadmin util および enableanalyticchannel
description: BITS クライアント分析チャネルを有効または無効にする bitsadmin util および enableanalytics のチャネルコマンドのリファレンス記事です。
ms.topic: article
ms.assetid: 0d7645aa-b91b-4ed7-b630-a1e1be6f6ae9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2c4577f635444c1830e232e1baeb12fac8c75476
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87880958"
---
# <a name="bitsadmin-util-and-enableanalyticchannel"></a>bitsadmin util および enableanalyticchannel

BITS クライアント分析チャネルを有効または無効にします。

## <a name="syntax"></a>構文

```
bitsadmin /util /enableanalyticchannel TRUE|FALSE
```

| パラメーター | 説明 |
| --------- | ---------- |
| TRUE または FALSE | **TRUE**を指定すると、指定したファイルのコンテンツの検証が有効になり、 **FALSE**の場合は無効になります。 |

## <a name="examples"></a>例

BITS クライアントの分析チャネルをオンまたはオフにします。

```
bitsadmin /util / enableanalyticchannel TRUE
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin util コマンド](bitsadmin-util.md)

- [bitsadmin コマンド](bitsadmin.md)
