---
title: bitsadmin キャッシュと setlimit
description: Windows コマンド」のトピック**bitsadmin キャッシュと setlimit** -キャッシュ サイズの制限を設定します。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 7d0b72c5ec6c779fa4ce3fa038352836cd9456ac
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852593"
---
# <a name="bitsadmin-cache-and-setlimit"></a>bitsadmin キャッシュと setlimit



キャッシュ サイズの制限を設定します。

## <a name="syntax"></a>構文

```
bitsadmin /Cache /SetLimit Percent
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|%|ハード_ディスクの合計領域の割合として定義されているキャッシュ制限.|

## <a name="BKMK_examples"></a>例

次の例では、50% にキャッシュ サイズを制限します。
```
C:\>bitsadmin /Cache /SetLimit 50 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)