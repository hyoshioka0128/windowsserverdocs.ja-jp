---
title: bdehdcfg newdriveletter
description: Bdehdcfg newdriveletter コマンドの参照記事。システムドライブとして使用されるドライブの部分に新しいドライブ文字を割り当てます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f1f200a0-6850-4f0d-9047-f9f982a590f8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f210056f74e930ad39361c9fc0cbf05d6e1894f4
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923490"
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
