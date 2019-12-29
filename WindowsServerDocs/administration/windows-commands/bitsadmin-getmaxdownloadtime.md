---
title: bitsadmin getmaxdownloadtime
description: '**Bitsadmin getmaxdownloadtime**の Windows コマンドに関するトピックでは、ダウンロードのタイムアウトを秒単位で取得します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cdce64f6-7125-489d-be3c-4af1dfc8c46a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 39a19f86e97c1a525b5beb0c5f3b23dff349cb19
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381577"
---
# <a name="bitsadmin-getmaxdownloadtime"></a>bitsadmin getmaxdownloadtime

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ダウンロードタイムアウトを秒単位で取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetMaxDownloadtime <Job> 
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------|--------|
|Job|ジョブの表示名または GUID|

## <a name="remarks"></a>コメント

-   N\/A

## <a name="BKMK_examples"></a>例
次の例では、 *Mydownloadjob*という名前のジョブの最大ダウンロード時間を秒単位で取得します。

```
C:\>bitsadmin /GetMaxDownloadtime myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報
[コマンド ライン構文の記号](command-line-syntax-key.md)


