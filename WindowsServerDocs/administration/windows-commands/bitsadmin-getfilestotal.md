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
ms.openlocfilehash: 27cf04e8745aeab5cd1f2ce379c8506be642fea2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381606"
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

# #

[コマンドライン構文のキー](command-line-syntax-key.md)関連項目