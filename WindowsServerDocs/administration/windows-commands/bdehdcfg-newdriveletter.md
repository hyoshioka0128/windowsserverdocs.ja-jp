---
title: bdehdcfg newdriveletter
description: Bdehdcfg newdriveletter コマンドのリファレンストピック。これにより、システムドライブとして使用されるドライブの部分に新しいドライブ文字が割り当てられます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f1f200a0-6850-4f0d-9047-f9f982a590f8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: da09ae1469c6fc8370e6bd0f2f7a8f3efd8dc4f0
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718663"
---
# <a name="bdehdcfg-newdriveletter"></a>bdehdcfg: newdriveletter

システムドライブとして使用されるドライブの部分に新しいドライブ文字を割り当てます。 ベストプラクティスとして、システムドライブにドライブ文字を割り当てないことをお勧めします。

## <a name="syntax"></a>構文

```
bdehdcfg -target {default|unallocated|<drive_letter> shrink|<drive_letter> merge} -newdriveletter <drive_letter>
```

#### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| ---------| ----------- |
| `<drive_letter>` | 指定されたターゲットドライブに割り当てられるドライブ文字を定義します。 |

## <a name="examples"></a>例

ドライブ文字`P`を既定のドライブに割り当てるには、次のようにします。

```
bdehdcfg -target default -newdriveletter P:
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bdehdcfg](bdehdcfg.md)
