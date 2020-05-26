---
title: 影の一覧表示
description: シャドウの一覧表示コマンドのリファレンストピックです。このコマンドは、システム上の永続的なシャドウコピーと永続的でないシャドウコピーを一覧表示します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fe568423-00ae-4ede-a1e7-07977cb50ad1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9e0261a25c7a70a0c8690d578cadc9e73ff9a62e
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83817172"
---
# <a name="list-shadows"></a>影の一覧表示

システム上の永続的なシャドウコピーと永続的でないシャドウコピーを一覧表示します。

## <a name="syntax"></a>構文

```
list shadows {all | set <setID> | id <shadowID>}
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ---------- |
| すべて | すべてのシャドウコピーを一覧表示します。 |
| 一連`<setID>` | 指定されたシャドウコピーセット ID に属するシャドウコピーを一覧表示します。 |
| 番号`<shadowID>` | 指定されたシャドウコピー ID を持つシャドウコピーを一覧表示します。 |

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)