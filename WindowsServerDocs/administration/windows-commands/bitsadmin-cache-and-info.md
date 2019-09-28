---
title: bitsadmin cache と info
description: '**Bitsadmin cache および info**の Windows コマンドに関するトピックでは、特定のキャッシュエントリがダンプされます。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 15975cbf-dba6-49ca-a725-d15ce1952de5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 11963ff5640ef30e597e5e802778aff121c0efb3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381971"
---
# <a name="bitsadmin-cache-and-info"></a>bitsadmin cache と info



特定のキャッシュエントリをダンプします。

## <a name="syntax"></a>構文

```
bitsadmin /Cache /Info RecordID [/Verbose] 
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|RecordID|キャッシュエントリに関連付けられている GUID。|

## <a name="BKMK_examples"></a>例

次の例では、{6511FB02-E195-40A2-B595-E8E2F8F47702} の RecordID を使用して、キャッシュエントリをダンプします。
```
C:\>bitsadmin /Cache /Info {6511FB02-E195-40A2-B595-E8E2F8F47702} 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)