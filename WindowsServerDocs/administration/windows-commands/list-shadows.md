---
title: 影の一覧表示
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fe568423-00ae-4ede-a1e7-07977cb50ad1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2640c04aef34cd6433efe529ac08c0294ba1c3b9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374762"
---
# <a name="list-shadows"></a>影の一覧表示



システム上の永続的なシャドウコピーと永続的でないシャドウコピーを一覧表示します。

## <a name="syntax"></a>構文

```
list shadows {all | set <SetID> | id <ShadowID>}
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|all|すべてのシャドウコピーを一覧表示します。|
|\<SetID > を設定します|指定されたシャドウコピーセット ID に属するシャドウコピーを一覧表示します。|
|id \<ShadowID >|指定されたシャドウコピー ID を持つシャドウコピーを一覧表示します。|

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)