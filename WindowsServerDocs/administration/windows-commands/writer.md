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
ms.openlocfilehash: 87b10952c6a851b5536a1589b994b265e8699f59
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826403"
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
名前、"システム ライターのライターを除外します? か 種類:
```
writer exclude "System Writer"
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)