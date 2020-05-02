---
title: メタデータの読み込み
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2c535487-668b-44fc-babb-ff59cf7d190e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3d3132bca86533ec3f2d0a27247bd3c116cf55b6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724466"
---
# <a name="load-metadata"></a>メタデータの読み込み



転送可能なシャドウコピーをインポートする前に、または復元の場合にライターメタデータを読み込む前に、メタデータ .cab ファイルを読み込みます。 パラメーターを指定せずに使用した場合、**メタデータの読み込み**コマンドプロンプトでヘルプが表示されます。



## <a name="syntax"></a>構文

```
load metadata [<Drive>:][<Path>]<MetaData.cab>
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|[\<ドライブ>:][<Path>]|メタデータファイルの場所を指定します。|
|メタデータ .cab|読み込むメタデータ .cab ファイルを指定します。|

## <a name="remarks"></a>Remarks

-   **Import**コマンドを使用すると、**読み込みメタ**データによって指定されたメタデータに基づいて、転送可能なシャドウコピーをインポートできます。
-   このコマンドは、[**復元の開始**] コマンドを使用して、選択したライターと復元用のコンポーネントを読み込む前に必要です。

## <a name="examples"></a>例

既定の場所から metafile というメタデータファイルを読み込むには、次のように入力します。
```
load metadata metafile.cab
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)