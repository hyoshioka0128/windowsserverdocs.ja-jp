---
title: 影の一覧表示
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fe568423-00ae-4ede-a1e7-07977cb50ad1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d22fc3bbe644983eaf072a430e565a0d34d1c4dd
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724471"
---
# <a name="list-shadows"></a>影の一覧表示



システム上の永続的なシャドウコピーと永続的でないシャドウコピーを一覧表示します。

## <a name="syntax"></a>構文

```
list shadows {all | set <SetID> | id <ShadowID>}
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|すべて|すべてのシャドウコピーを一覧表示します。|
|set \<SetID>|指定されたシャドウコピーセット ID に属するシャドウコピーを一覧表示します。|
|id \<ShadowID>|指定されたシャドウコピー ID を持つシャドウコピーを一覧表示します。|

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)