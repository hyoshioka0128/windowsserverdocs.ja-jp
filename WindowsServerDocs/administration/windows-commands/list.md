---
title: list
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 57b6c8d0-872e-4dba-9715-1db8ab892e98
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 91b42925fc822b10157bb488167d06fe82cfe1e3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374700"
---
# <a name="list"></a>list



システム上にあるライター、シャドウコピー、または現在登録されているシャドウコピープロバイダーの一覧を表示します。 パラメーターを指定せずに使用した場合、**一覧**にはコマンドプロンプトでヘルプが表示されます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
list writers [metadata | detailed | status]
list shadows {all | set <SetID> | id <ShadowID>}
list providers
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|書き込む|ライターを一覧表示します。 構文とパラメーターについては、「[ライターの一覧](list-writers.md)」を参照してください。|
|Shadows|永続化および既存の非永続的シャドウコピーの一覧を表示します。 構文とパラメーターについては、「[影の一覧](list-shadows.md)」を参照してください。|
|プロバイダー|現在登録されているシャドウコピープロバイダーを一覧表示します。 構文とパラメーターについては、「[プロバイダーの一覧](list-providers.md)」を参照してください。|

## <a name="BKMK_examples"></a>例

すべてのシャドウコピーを一覧表示するには、次のように入力します。
```
list shadows all
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)