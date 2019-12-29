---
title: bitsadmin list
description: '**Bitsadmin list**の Windows コマンドのトピック-現在のユーザーが所有している転送ジョブの一覧を表示します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1416965e-e0e6-49cf-b1d4-b286d3cf8716
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bd4787f51dc2a7843ff6cf5c4f786658e530ad8f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381098"
---
# <a name="bitsadmin-list"></a>bitsadmin list



現在のユーザーが所有している転送ジョブの一覧を表示します。

## <a name="syntax"></a>構文

```
bitsadmin /List [/allusers][/verbose]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/Allusers|省略可能—すべてのユーザーのジョブを一覧表示します。|
|/Verbose|省略可能: 各ジョブの詳細情報を提供します。|

## <a name="remarks"></a>コメント

/Allusers パラメーターを使用するには、管理者特権が必要です。

## <a name="BKMK_examples"></a>例

次の例では、現在のユーザーが所有しているジョブに関する情報を取得します。
```
C:\>bitsadmin /List 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)