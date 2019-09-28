---
title: bitsadmin getfilestransferred
description: '**Bitsadmin getfilestransferred**の Windows コマンドに関するトピックでは、指定したジョブで転送されたファイルの数を取得します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e282815c-938b-4ac0-a09d-9baafb656dcb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d02d9d7bc216a5ad7ca922e716c368f64c4b9a44
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381602"
---
# <a name="bitsadmin-getfilestransferred"></a>bitsadmin getfilestransferred



指定したジョブで転送されたファイルの数を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetFilesTransferred <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブで転送されたファイルの数を取得します。
```
C:\>bitsadmin /GetFilesTransferred myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)