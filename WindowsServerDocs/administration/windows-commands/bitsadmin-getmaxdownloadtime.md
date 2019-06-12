---
title: bitsadmin getmaxdownloadtime
description: Windows コマンド」のトピック**bitsadmin getmaxdownloadtime** -ダウンロード タイムアウトを秒単位で取得します。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: d067d6a0821d9af4784c02c6a332e8eddd2352c0
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434945"
---
# <a name="bitsadmin-getmaxdownloadtime"></a>bitsadmin getmaxdownloadtime

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ダウンロード タイムアウトを秒単位で取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetMaxDownloadtime <Job> 
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------|--------|
|Job|ジョブの表示名または GUID|

## <a name="remarks"></a>注釈

-   N\/A

## <a name="BKMK_examples"></a>例
次の例では、という名前のジョブの最大ダウンロード時間を取得します。 *myDownloadJob* (秒)。

```
C:\>bitsadmin /GetMaxDownloadtime myDownloadJob
```

## <a name="additional-references"></a>その他の参照
[コマンド ライン構文の記号](command-line-syntax-key.md)


