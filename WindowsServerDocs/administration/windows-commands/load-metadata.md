---
title: メタデータの読み込み
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2c535487-668b-44fc-babb-ff59cf7d190e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b8db98611fd78c6e30070901effafddd6e678c16
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841025"
---
# <a name="load-metadata"></a>メタデータの読み込み



転送可能なシャドウコピーをインポートする前に、または復元の場合にライターメタデータを読み込む前に、メタデータ .cab ファイルを読み込みます。 パラメーターを指定せずに使用した場合、**メタデータの読み込み**コマンドプロンプトでヘルプが表示されます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
load metadata [<Drive>:][<Path>]<MetaData.cab>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[\<ドライブ >:][<Path>]|メタデータファイルの場所を指定します。|
|メタデータ .cab|読み込むメタデータ .cab ファイルを指定します。|

## <a name="remarks"></a>コメント

-   **Import**コマンドを使用すると、**読み込みメタ**データによって指定されたメタデータに基づいて、転送可能なシャドウコピーをインポートできます。
-   このコマンドは、 **[復元の開始]** コマンドを使用して、選択したライターと復元用のコンポーネントを読み込む前に必要です。

## <a name="examples"></a><a name=BKMK_examples></a>例

既定の場所から metafile というメタデータファイルを読み込むには、次のように入力します。
```
load metadata metafile.cab
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)