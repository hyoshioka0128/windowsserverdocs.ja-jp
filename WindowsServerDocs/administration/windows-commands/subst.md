---
title: subst
description: パスをドライブ文字に関連付ける方法について説明します。
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3e69234c-2312-4343-868b-afc1017c622a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f3010d1e58fbd360b8311512e6664873b020c12b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383748"
---
# <a name="subst"></a>subst



ドライブ文字をパスに関連付けます。 パラメーターを指定せずに使用する場合 **subst** 仮想ドライブの名前が有効で表示されます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
subst [<Drive1>: [<Drive2>:]<Path>] 
subst <Drive1>: /d
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ドライブ 1 >:|パスに割り当てる仮想ドライブを指定します。|
|[\<Path 2 >:] \< パス >|物理ドライブと仮想ドライブに指定するパスを指定します。|
|/d|置き換えられた (仮想) ドライブを削除します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>コメント

-   次のコマンドは機能しません。 **subst**コマンドで指定されているドライブでは使用できません。

    **chkdsk**

    **diskcomp**

    **diskcopy**

    **format**

    **label**

    **recover**
-   *ドライブ 1* パラメーターがで指定された範囲内である必要があります、 **リソース** コマンドです。 ない場合は、 **subst** 次のエラー メッセージが表示されます。

    `Invalid parameter - drive1:`

## <a name="BKMK_examples"></a>例

仮想ドライブ Z B:\User\Betty\Forms のパスを作成するには、次のように入力します。
```
subst z: b:\user\betty\forms 
```
完全なパスを入力する代わりに次のように、コロンで後に仮想ドライブの文字を入力してこのディレクトリに移動することができます。
```
z: 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)