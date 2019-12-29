---
title: bitsadmin cache と deleteurl
description: '**Bitsadmin cache と deleteurl**の Windows コマンドに関するトピックでは、指定された url のすべてのキャッシュエントリが削除されます。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e108b76b-fae9-4c16-bf4c-d74c9f025953
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 869d3bc0f011cc82aaea9b7468667964051e1c00
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382058"
---
# <a name="bitsadmin-cache-and-deleteurl"></a>bitsadmin cache と deleteurl



指定された URL のすべてのキャッシュエントリを削除します。

## <a name="syntax"></a>構文

```
bitsadmin /DeleteURL url
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|url|リモートファイルを識別する Uniform Resource Locator。|

## <a name="BKMK_examples"></a>例

次の例では、 https://www.microsoft.com/en/us/default.aspx のすべてのキャッシュエントリを削除します。
```
C:\>bitsadmin /DeleteURL https://www.microsoft.com/en/us/default.aspx 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)