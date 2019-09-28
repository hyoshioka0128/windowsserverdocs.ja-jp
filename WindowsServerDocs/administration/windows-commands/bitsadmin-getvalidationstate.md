---
title: bitsadmin getvalidationstate
description: '**Bitsadmin getvalidationstate**の Windows コマンドのトピック-ジョブ内の指定されたファイルのコンテンツ検証の状態を報告します。 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6ada3f1f-9967-4262-9d22-ed641e23f516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ca4269a596010258edd0479f5a7e9844bc9c98df
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381262"
---
# <a name="bitsadmin-getvalidationstate"></a>bitsadmin getvalidationstate



ジョブ内の指定されたファイルのコンテンツ検証の状態を報告します。

## <a name="syntax"></a>構文

```
bitsadmin /GetValidationState <Job> <file index> 
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|ファイルインデックス|0から開始|

## <a name="BKMK_examples"></a>例

次の例では、 *myjob*という名前のジョブ内にあるファイル2のコンテンツ検証の状態を取得します。
```
C:\>bitsadmin /GetValidationState myJob 1
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)