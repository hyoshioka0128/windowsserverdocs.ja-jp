---
title: エイリアスの追加
description: '**エイリアスの追加**に関する Windows コマンドのトピック-エイリアス環境にエイリアスを追加します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5fe12f5d-11e9-4f3d-b7f9-40b26c8685e5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f2834376e497f54eadf1d9077e74f9c398202c5a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382817"
---
# <a name="add-alias"></a>エイリアスの追加



エイリアスをエイリアス環境に追加します。 パラメーターを指定せずに使用する場合、**エイリアスの追加**コマンドプロンプトでヘルプを表示します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
add alias <AliasName> <AliasValue>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<AliasName >|エイリアスの名前を指定します。|
|\<エイリアス値 >|エイリアスの値を指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>コメント

-   エイリアスはメタデータファイルに保存され、**メタデータの読み込み**コマンドを使用して読み込まれます。

## <a name="BKMK_examples"></a>例

エイリアスを含むすべての影を一覧表示するには、次のように入力します。
```
list shadows all
```
次の抜粋は、既定のエイリアスである VSS_SHADOW_x が割り当てられているシャドウコピーを示しています。
```
* Shadow Copy ID = {ff47165a-1946-4a0c-b7f4-80f46a309278}
%VSS_SHADOW_1%
```
System1 という名前の新しいエイリアスをこのシャドウコピーに割り当てるには、次のように入力します。
```
add alias System1 %VSS_SHADOW_1%
```
または、シャドウコピー ID を使用してエイリアスを割り当てることもできます。
```
add alias System1 {ff47165a-1946-4a0c-b7f4-80f46a309278}
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)