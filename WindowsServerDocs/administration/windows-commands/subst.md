---
title: subst
description: ドライブ文字とパスを関連付ける方法について説明します。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 858195de89ca8661cf47c25b6cf9b519cc4efbf8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858073"
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
|[\<ドライブ 2 >:]\<パス >|物理ドライブと仮想ドライブに指定するパスを指定します。|
|/d|置き換えられた (仮想) ドライブを削除します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

-   次のコマンドが動作しないで指定されているドライブでは使用できませんが、 **subst**コマンド。

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

[コマンドライン構文キー](command-line-syntax-key.md)