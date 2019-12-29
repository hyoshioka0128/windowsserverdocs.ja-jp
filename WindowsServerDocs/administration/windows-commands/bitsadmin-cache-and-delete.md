---
title: bitsadmin cache と delete
description: '**Bitsadmin cache と delete**の Windows コマンドのトピックでは、特定のキャッシュエントリが削除されます。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 22540273-55a5-46ea-869b-6df2aa6808a1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 87c3ffd7e0c9c43e8e2eb6e5d5a1d98610a4d9ad
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382074"
---
# <a name="bitsadmin-cache-and-delete"></a>bitsadmin cache と delete



特定のキャッシュエントリを削除します。

## <a name="syntax"></a>構文

```
bitsadmin /Cache /Delete RecordID 
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|RecordID|キャッシュエントリに関連付けられている GUID。|

## <a name="BKMK_examples"></a>例

次の例では、{6511FB02-E195-40A2-B595-E8E2F8F47702} の RecordID を使用して、キャッシュエントリを削除します。
```
C:\>bitsadmin /Cache /Delete {6511FB02-E195-40A2-B595-E8E2F8F47702} 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)