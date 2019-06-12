---
title: ライター
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7cf98295-411d-4705-8573-f898ff45c140
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8aee4ecca85c7d5f46ee79f3ad928b746c02e7bb
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439979"
---
# <a name="writer"></a>ライター



ライターまたはコンポーネントが含まれるか、バックアップまたは復元の手順からライターまたはコンポーネントを除外することを確認します。 パラメーターを指定せずに使用されている場合**ライター**コマンド プロンプトでヘルプを表示します。

## <a name="syntax"></a>構文

```
writer verify [<Writer> | <Component>]
writer exclude [<Writer> | <Component>]
```

## <a name="parameters"></a>パラメーター

| パラメーター  |                                                                                      説明                                                                                      |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   verify   | バックアップまたは復元の手順で、指定したライターまたはコンポーネントが含まれることを確認します。 バックアップまたは復元の手順は、ライターまたはコンポーネントが含まれていない場合は失敗します。 |
|  exclude   |                                                   バックアップまたは復元の手順から、指定したライターまたはコンポーネントを除外します。                                                    |
| [\<ライター > |                                                                                     <Component>]                                                                                      |

## <a name="BKMK_examples"></a>例

ライターを確認します (この例では、4dc3bdd4-ab48-4d07-adb0-3bee2926fd7f) については、GUID を指定することで、次のように入力します。
```
writer verify {4dc3bdd4-ab48-4d07-adb0-3bee2926fd7f}
```
「システム ライター」という名前のライターを除外するには、次のように入力します。
```
writer exclude "System Writer"
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)