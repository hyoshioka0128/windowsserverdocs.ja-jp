---
title: bitsadmin cache と setlimit
description: '**Bitsadmin cache と setlimit**の Windows コマンドのトピックでは、キャッシュサイズの制限を設定します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 46578835-d5ce-423b-be4d-62ddb9e1908d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 88a10ce8599202e237daa6822cf62806d3c21429
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381941"
---
# <a name="bitsadmin-cache-and-setlimit"></a>bitsadmin cache と setlimit



キャッシュサイズの制限を設定します。

## <a name="syntax"></a>構文

```
bitsadmin /Cache /SetLimit Percent
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|~|ハードディスクの合計領域に対する割合として定義されているキャッシュの制限。|

## <a name="BKMK_examples"></a>例

次の例では、キャッシュサイズを 50% に制限しています。
```
C:\>bitsadmin /Cache /SetLimit 50 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)