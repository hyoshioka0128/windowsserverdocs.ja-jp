---
title: list
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: aacc93e1c7a16a7327ddbd17515f19cf41a5b458
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825543"
---
# <a name="list"></a>list



ライター、シャドウ コピー、または現在登録されているシャドウ コピー プロバイダーは、システム上にあるを一覧表示します。 パラメーターを指定せずに使用されている場合**一覧**コマンド プロンプトでヘルプを表示します。

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
|ライター|ライターの一覧を表示します。 参照してください[List](list-writers.md)構文およびパラメーターについてです。|
|シャドウ|永続的および既存の非永続的なシャドウ コピーを一覧表示します。 参照してください[影を一覧表示](list-shadows.md)構文およびパラメーターについてです。|
|プロバイダー|現在、リストには、シャドウ コピー プロバイダーが登録されています。 参照してください[プロバイダーの一覧表示](list-providers.md)構文およびパラメーターについてです。|

## <a name="BKMK_examples"></a>例

すべてのシャドウ コピーを一覧表示には、次のように入力します。
```
list shadows all
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)