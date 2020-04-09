---
title: bitsadmin setvalidationstate
description: Bitsadmin setvalidationstate の Windows コマンドに関するトピックでは、ジョブ内の指定されたファイルのコンテンツ検証の状態を設定します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e8fc8e8c-171c-4681-8057-6986b018e576
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: de6480596b55b3a483076297f32ce52a975915db
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849115"
---
# <a name="bitsadmin-setvalidationstate"></a>bitsadmin setvalidationstate

ジョブ内の指定されたファイルのコンテンツ検証の状態を設定します。

## <a name="syntax"></a>構文

```
bitsadmin /SetValidationState <Job> <file index> <true|false> 
```

### <a name="parameters"></a>パラメーター

| パラメーター  |          説明           |
|------------|--------------------------------|
|    Job     | ジョブの表示名または GUID |
| ファイルインデックス |         0から開始          |
|    True    |             False              |

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *myjob*という名前のジョブについて、ファイル2のコンテンツ検証の状態を TRUE に設定します。
```
C:\>bitsadmin /SetValidationState myJob 2 TRUE 
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)