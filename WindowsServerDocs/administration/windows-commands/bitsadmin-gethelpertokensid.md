---
title: bitsadmin gei pertokensid
description: '**Bitsadmin ge pertokensid**の Windows コマンドのトピックが設定されている場合は、BITS 転送ジョブのヘルパートークンの SID を返します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: a8c2a9f319defd8ac9acd36063ee079c24ad8ae0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381593"
---
# <a name="bitsadmin-gethelpertokensid"></a>bitsadmin gei pertokensid

BITS 転送ジョブの [ヘルパートークン](/windows/desktop/bits/helper-tokens-for-bits-transfer-jobs)が設定されている場合、その SID を返します。

**BITS 3.0 以前**: サポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /GetHelperTokensID <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)
