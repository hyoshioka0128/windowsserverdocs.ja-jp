---
title: bitsadmin setvalidationstate
description: '**Bitsadmin setvalidationstate**の Windows コマンドトピック-ジョブ内の指定されたファイルのコンテンツ検証の状態を設定します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e8fc8e8c-171c-4681-8057-6986b018e576
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 37d7fa3a8a91abf1e7b6ac5a51b6cebd78984a91
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380398"
---
# <a name="bitsadmin-setvalidationstate"></a>bitsadmin setvalidationstate



ジョブ内の指定されたファイルのコンテンツ検証の状態を設定します。

## <a name="syntax"></a>構文

```
bitsadmin /SetValidationState <Job> <file index> <true|false> 
```

## <a name="parameters"></a>パラメーター

| パラメーター  |          説明           |
|------------|--------------------------------|
|    Job     | ジョブの表示名または GUID |
| ファイルインデックス |         0から開始          |
|    True    |             False              |

## <a name="BKMK_examples"></a>例

次の例では、 *myjob*という名前のジョブについて、ファイル2のコンテンツ検証の状態を TRUE に設定します。
```
C:\>bitsadmin /SetValidationState myJob 2 TRUE 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)