---
title: bitsadmin setpriority
description: '**Bitsadmin setpriority**の Windows コマンドトピック-指定したジョブの優先順位を設定します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 90788363-01a2-4d7c-a560-a3eba45b5e9e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 60564350928f917ca1861684e042304d5d380426
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380440"
---
# <a name="bitsadmin-setpriority"></a>bitsadmin setpriority



指定されたジョブの優先順位を設定します。

## <a name="syntax"></a>構文

```
bitsadmin /SetPriority <Job> <Priority>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|[Priority]|次のいずれかの値です。</br>-前景</br>-高</br>-通常</br>-低|

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブの優先順位を normal に設定します。
```
C:\>bitsadmin /SetPriority myDownloadJob NORMAL
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)