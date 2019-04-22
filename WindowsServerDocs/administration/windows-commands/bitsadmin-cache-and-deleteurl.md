---
title: bitsadmin キャッシュと deleteurl
description: Windows コマンド」のトピック**bitsadmin キャッシュと deleteurl** -指定された URL のすべてのキャッシュ エントリを削除します。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: a831c49e1461761cb7466b46e7a5ad8e037f4ec9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816653"
---
# <a name="bitsadmin-cache-and-deleteurl"></a>bitsadmin キャッシュと deleteurl



指定された url には、すべてのキャッシュ エントリを削除します。

## <a name="syntax"></a>構文

```
bitsadmin /DeleteURL url
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|url|リモート ファイルを識別する Uniform Resource Locator します。|

## <a name="BKMK_examples"></a>例

次の例では、すべてのキャッシュ エントリを削除します。 https://www.microsoft.com/en/us/default.aspx
```
C:\>bitsadmin /DeleteURL https://www.microsoft.com/en/us/default.aspx 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)