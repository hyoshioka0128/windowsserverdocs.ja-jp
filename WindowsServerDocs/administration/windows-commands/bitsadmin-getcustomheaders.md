---
title: bitsadmin getcustomheaders
description: '**Bitsadmin getcustomheaders**の Windows コマンドトピックでは、ジョブからカスタム HTTP ヘッダーを取得します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1f0d38d3-e865-4474-81e8-773d65c3d1cc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 039669fca42803ff22eb4e3d13dfdef5f0a06f93
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381661"
---
# <a name="bitsadmin-getcustomheaders"></a>bitsadmin getcustomheaders



ジョブからカスタム HTTP ヘッダーを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetCustomHeaders <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブのカスタムヘッダーを取得します。
```
C:\>bitsadmin /GetCustomHeaders myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)