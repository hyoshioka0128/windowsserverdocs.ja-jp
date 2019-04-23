---
title: マスク
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bf301474-d74a-44e7-9fad-c8a11e7ca3bd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 353e6080d1f6c548bc907b58655f31d0bce6de8b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858023"
---
# <a name="mask"></a>マスク



使用してインポートされたハードウェアのシャドウ コピーを削除、**インポート**コマンド。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
mask <ShadowSetID>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|ShadowSetID|シャドウ コピー、指定したシャドウ コピー セット ID に属しているを削除します|

## <a name="remarks"></a>注釈

-   既存のエイリアスまたは環境変数の代わりに使用できます*ShadowSetID*します。 使用**追加**パラメーターに既存の別名を参照してください。

## <a name="BKMK_examples"></a>例

インポートされたシャドウ コピーの %import_1% を削除するには、次のように入力します。
```
mask %Import_1%
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)