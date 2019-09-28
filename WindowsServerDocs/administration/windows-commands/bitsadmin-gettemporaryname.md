---
title: bitsadmin get一時名
description: '**Bitsadmin gettemporary name**の Windows コマンドトピックでは、ジョブ内の指定されたファイルの一時ファイル名を報告します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68925edc-a801-4292-a812-7471c4f60fdd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7b665fae4c0bfdd5ea04b929be49f9590430b358
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381300"
---
# <a name="bitsadmin-gettemporaryname"></a>bitsadmin get一時名



ジョブ内の指定されたファイルの一時ファイル名を報告します。

## <a name="syntax"></a>構文

```
bitsadmin /GetTemporaryName <Job> <file index> 
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|ファイルインデックス|0から開始|

## <a name="BKMK_examples"></a>例

次の例では、 *myjob*という名前のジョブのファイル2の一時ファイル名を報告します。
```
C:\>bitsadmin /GetTemporaryName myJob 1 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)