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
ms.openlocfilehash: 94be02aa25867845436b83d052c4990ff9212975
ms.sourcegitcommit: 08eba714d3ceb5f2dfb5486d6b990da1aa4dcbdd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/14/2019
ms.locfileid: "65564684"
---
# <a name="writer"></a>ライター



ライターまたはコンポーネントが含まれるか、バックアップまたは復元の手順からライターまたはコンポーネントを除外することを確認します。 パラメーターを指定せずに使用されている場合**ライター**コマンド プロンプトでヘルプを表示します。

## <a name="syntax"></a>構文

```
writer verify [<Writer> | <Component>]
writer exclude [<Writer> | <Component>]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|verify|バックアップまたは復元の手順で、指定したライターまたはコンポーネントが含まれることを確認します。 バックアップまたは復元の手順は、ライターまたはコンポーネントが含まれていない場合は失敗します。|
|exclude|バックアップまたは復元の手順から、指定したライターまたはコンポーネントを除外します。|
|[\<ライター > | <Component>]|確認するか、除外するには、ライターまたはコンポーネントを指定します。 ライターが指定したは、ライター GUID またはライターの名前、「システム ライター」などです。|

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