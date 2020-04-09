---
title: リスト
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 57b6c8d0-872e-4dba-9715-1db8ab892e98
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d60c42b868a1e9a26e3168e4b489573f9f87e179
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841105"
---
# <a name="list"></a>リスト



システム上にあるライター、シャドウコピー、または現在登録されているシャドウコピープロバイダーの一覧を表示します。 パラメーターを指定せずに使用した場合、**一覧**にはコマンドプロンプトでヘルプが表示されます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
list writers [metadata | detailed | status]
list shadows {all | set <SetID> | id <ShadowID>}
list providers
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|ライタ|ライターを一覧表示します。 構文とパラメーターについては、「[ライターの一覧](list-writers.md)」を参照してください。|
|shadows|永続化および既存の非永続的シャドウコピーの一覧を表示します。 構文とパラメーターについては、「[影の一覧](list-shadows.md)」を参照してください。|
|プロバイダー|現在登録されているシャドウコピープロバイダーを一覧表示します。 構文とパラメーターについては、「[プロバイダーの一覧](list-providers.md)」を参照してください。|

## <a name="examples"></a><a name=BKMK_examples></a>例

すべてのシャドウコピーを一覧表示するには、次のように入力します。
```
list shadows all
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)