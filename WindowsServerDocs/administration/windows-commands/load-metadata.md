---
title: メタデータの読み込み
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2c535487-668b-44fc-babb-ff59cf7d190e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 025f75743d61889c4b987e9a2a575d1c599f04c1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374618"
---
# <a name="load-metadata"></a>メタデータの読み込み



転送可能なシャドウコピーをインポートする前に、または復元の場合にライターメタデータを読み込む前に、メタデータ .cab ファイルを読み込みます。 パラメーターを指定せずに使用した場合、**メタデータの読み込み**コマンドプロンプトでヘルプが表示されます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
load metadata [<Drive>:][<Path>]<MetaData.cab>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[\<Drive >:][<Path>]|メタデータファイルの場所を指定します。|
|メタデータ .cab|読み込むメタデータ .cab ファイルを指定します。|

## <a name="remarks"></a>コメント

-   **Import**コマンドを使用すると、**読み込みメタ**データによって指定されたメタデータに基づいて、転送可能なシャドウコピーをインポートできます。
-   このコマンドは、 **[復元の開始]** コマンドを使用して、選択したライターと復元用のコンポーネントを読み込む前に必要です。

## <a name="BKMK_examples"></a>例

既定の場所から metafile というメタデータファイルを読み込むには、次のように入力します。
```
load metadata metafile.cab
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)