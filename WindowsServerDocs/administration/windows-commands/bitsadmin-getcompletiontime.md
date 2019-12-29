---
title: bitsadmin getcompletiontime
description: '**Bitsadmin get time**の Windows コマンドトピック-ジョブがデータの転送を終了した時刻を取得します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7a4b3c1c-9832-4724-86b2-cce3c01bfa28
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 190467d5f3a7b7244ed0d7ab3b75d4cbbf56c8d5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381738"
---
# <a name="bitsadmin-getcompletiontime"></a>bitsadmin getcompletiontime



ジョブがデータの転送を終了した時刻を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetCompletionTime <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブがデータの転送を終了した時刻を取得します。
```
C:\>bitsadmin /GetCompletionTime myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)