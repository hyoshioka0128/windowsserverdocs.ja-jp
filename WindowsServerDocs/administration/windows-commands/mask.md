---
title: mask
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bf301474-d74a-44e7-9fad-c8a11e7ca3bd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a1cb92caacb955449c1baaad411fdbe4cdf05b73
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80839645"
---
# <a name="mask"></a>mask



**インポート**コマンドを使用してインポートされたハードウェアシャドウコピーを削除します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
mask <ShadowSetID>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|ShadowSetID|指定されたシャドウコピーセット ID に属するシャドウコピーを削除します。|

## <a name="remarks"></a>コメント

-   *ShadowSetID*の代わりに、既存のエイリアスまたは環境変数を使用できます。 既存のエイリアスを表示するには、パラメーターを指定せずに**add**を使用します。

## <a name="examples"></a><a name=BKMK_examples></a>例

インポートされたシャドウコピー% Import_1% を削除するには、次のように入力します。
```
mask %Import_1%
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)