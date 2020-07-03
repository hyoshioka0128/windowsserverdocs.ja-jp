---
title: list shadows
description: '[シャドウの一覧表示] コマンドの参照記事。システム上の永続的なシャドウコピーと永続的でないシャドウコピーが一覧表示されます。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fe568423-00ae-4ede-a1e7-07977cb50ad1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fcf1946f5b2424eb7aa13af51bd6ff13c43349c1
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931791"
---
# <a name="list-shadows"></a>list shadows

システム上の永続的なシャドウコピーと永続的でないシャドウコピーを一覧表示します。

## <a name="syntax"></a>構文

```
list shadows {all | set <setID> | id <shadowID>}
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ---------- |
| all | すべてのシャドウコピーを一覧表示します。 |
| 一連`<setID>` | 指定されたシャドウコピーセット ID に属するシャドウコピーを一覧表示します。 |
| 番号`<shadowID>` | 指定されたシャドウコピー ID を持つシャドウコピーを一覧表示します。 |

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)