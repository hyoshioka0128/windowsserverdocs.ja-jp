---
title: bitsadmin setvalidationstate
description: Windows コマンド」のトピック**bitsadmin setvalidationstate** -ジョブ内の指定されたファイルのコンテンツの検証状態を設定します。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: a832e8f3d21681f67a4486df33c387e5a8456718
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434872"
---
# <a name="bitsadmin-setvalidationstate"></a>bitsadmin setvalidationstate



ジョブ内の指定されたファイルのコンテンツの検証の状態を設定します。

## <a name="syntax"></a>構文

```
bitsadmin /SetValidationState <Job> <file index> <true|false> 
```

## <a name="parameters"></a>パラメーター

| パラメーター  |          説明           |
|------------|--------------------------------|
|    Job     | ジョブの表示名または GUID |
| ファイルのインデックス |         0 から始まります          |
|    True    |             False              |

## <a name="BKMK_examples"></a>例

次の例では、ファイル 2 のコンテンツの検証の状態を設定を TRUE という名前のジョブに*myJob*します。
```
C:\>bitsadmin /SetValidationState myJob 2 TRUE 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)