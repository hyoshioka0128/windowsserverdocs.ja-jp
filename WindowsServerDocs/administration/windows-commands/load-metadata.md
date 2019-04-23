---
title: メタデータを読み込み
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: b52b5040fc8c834b04cad83ca4b0cfab103fdc43
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59871333"
---
# <a name="load-metadata"></a>メタデータを読み込み



移動可能なシャドウ コピーをインポートする前に、メタデータの .cab ファイルの読み込みまたは復元の場合、ライター メタデータを読み込みます。 パラメーターを指定せずに使用されている場合**メタデータの読み込み**コマンド プロンプトでヘルプを表示します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
load metadata [<Drive>:][<Path>]<MetaData.cab>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[\<ドライブ >:] [<Path>]|メタデータ ファイルの場所を指定します。|
|MetaData.cab|読み込むメタデータ .cab ファイルを指定します。|

## <a name="remarks"></a>注釈

-   使用することができます、**インポート**移動可能なシャドウ コピーをインポートするコマンドがで指定されたメタデータに基づいた**メタデータの読み込み**します。
-   このコマンドは、前に必要な**復元を開始**選択されているライターと復元のコンポーネントを読み込むコマンド。

## <a name="BKMK_examples"></a>例

既定の場所から metafile.cab をという名前のメタデータ ファイルを読み込むには、次のように入力します。
```
load metadata metafile.cab
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)