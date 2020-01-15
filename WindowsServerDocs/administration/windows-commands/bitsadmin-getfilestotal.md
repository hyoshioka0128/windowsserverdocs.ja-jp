---
title: bitsadmin getfilestotal
description: '**Bitsadmin getfilestotal**の Windows コマンドトピックでは、指定されたジョブ内のファイルの数を取得します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c5de113e-f29c-4cd3-9392-0e300018d516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e5c28d8e970bd7db896073bf8cddb168ffe9deff
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2020
ms.locfileid: "75946843"
---
# <a name="bitsadmin-getfilestotal"></a>bitsadmin getfilestotal



指定されたジョブ内のファイルの数を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetFilesTotal <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブに含まれているファイルの数を取得します。
```
C:\>bitsadmin /GetFilesTotal myDownloadJob
```

## <a name="see-also"></a>関連項目

[コマンド ライン構文の記号](command-line-syntax-key.md)
