---
title: bdehdcfg newdriveletter
description: Bdehdcfg newdriveletter コマンドの参照記事。システムドライブとして使用されるドライブの部分に新しいドライブ文字を割り当てます。
ms.topic: article
ms.assetid: f1f200a0-6850-4f0d-9047-f9f982a590f8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b13bae914f06af4b282ed558384c9cdc14f5bc11
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87895104"
---
# <a name="bdehdcfg-newdriveletter"></a>bdehdcfg: newdriveletter

システムドライブとして使用されるドライブの部分に新しいドライブ文字を割り当てます。 ベストプラクティスとして、システムドライブにドライブ文字を割り当てないことをお勧めします。

## <a name="syntax"></a>構文

```
bdehdcfg -target {default|unallocated|<drive_letter> shrink|<drive_letter> merge} -newdriveletter <drive_letter>
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------| ----------- |
| `<drive_letter>` | 指定されたターゲットドライブに割り当てられるドライブ文字を定義します。 |

## <a name="examples"></a>例

ドライブ文字を既定のドライブに割り当てるには、次のようにし `P` ます。

```
bdehdcfg -target default -newdriveletter P:
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bdehdcfg](bdehdcfg.md)
