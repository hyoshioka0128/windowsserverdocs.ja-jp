---
title: エイリアスの追加します。
description: Windows コマンド」のトピック**エイリアスの追加**-別名の環境にエイリアスを追加します。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 50de932ea0153546816face61f0852a08707ea85
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862223"
---
# <a name="add-alias"></a>エイリアスの追加します。



エイリアスの環境にエイリアスを追加します。 パラメーターを指定せずに使用されている場合**エイリアスの追加**コマンド プロンプトでヘルプを表示します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
add alias <AliasName> <AliasValue>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<AliasName>|エイリアスの名前を指定します。|
|\<AliasValue>|エイリアスの値を指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

-   エイリアスは、メタデータ ファイルに保存されに読み込まれます、**メタデータの読み込み**コマンド。

## <a name="BKMK_examples"></a>例

など、別名では、すべての影を一覧表示するには、次のように入力します。
```
list shadows all
```
VSS_SHADOW_x で、既定のエイリアスが割り当てられているシャドウ コピーを次に示します。
```
* Shadow Copy ID = {ff47165a-1946-4a0c-b7f4-80f46a309278}
%VSS_SHADOW_1%
```
このシャドウ コピーに割り当てる System1 という名前の新しいエイリアスには、次のように入力します。
```
add alias System1 %VSS_SHADOW_1%
```
または、シャドウ コピー ID を使用して別名を割り当てることができます。
```
add alias System1 {ff47165a-1946-4a0c-b7f4-80f46a309278}
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)