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
ms.openlocfilehash: 868f7ac58a69c067681bf0597524fbaa5a25984f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842423"
---
#<a name="bitsadmin-getmaxdownloadtime"></a>bitsadmin getmaxdownloadtime

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
[コマンドライン構文キー](command-line-syntax-key.md)


