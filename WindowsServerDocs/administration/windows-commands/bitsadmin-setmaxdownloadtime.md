---
title: bitsadmin setmaxdownloadtime
description: '**Bitsadmin setmaxdownloadtime**の Windows コマンドのトピック-ダウンロードのタイムアウトを秒単位で設定します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 16b96cf1-5738-415c-9b9d-c4ea8d5e4fec
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 985453de5bd2f4a06b5635ae5b0a9794d30175b0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380561"
---
# <a name="bitsadmin-setmaxdownloadtime"></a>bitsadmin setmaxdownloadtime



ダウンロードタイムアウトを秒単位で設定します。

## <a name="syntax"></a>構文

```
bitsadmin /SetMaxDownloadTime <Job> <Timeout>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|Timeout|タイムアウト (秒)|

## <a name="remarks"></a>コメント

-   なし

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブのタイムアウトを10秒に設定します。
```
C:\>bitsadmin /SetMaxDownloadTime myDownloadJob 10
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)