---
title: bitsadmin info
description: の Windows コマンドに**関するトピックでは、指定されたジョブに関する概要情報が表示されます。** -bitsadmin info
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5c306677-0d64-41c0-8276-5bba7750cecb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3b6710d73860315fcd13670669871cd310ffb41c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381079"
---
# <a name="bitsadmin-info"></a>bitsadmin info



指定されたジョブに関する概要情報を表示します。

## <a name="syntax"></a>構文

```
bitsadmin /Info <Job> [/verbose]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="remarks"></a>コメント

/Verbose パラメーターを使用して、ジョブに関する詳細情報を提供します。

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブに関する情報を取得します。
```
C:\>bitsadmin /Info myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)