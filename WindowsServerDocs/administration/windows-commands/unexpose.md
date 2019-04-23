---
title: 非公開にします
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 58dc7d0f-52e9-4587-9487-d3b4c3e52640
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fe9cb5dfd8ae6c71fdc72ddc1e8421229f98f5d0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837473"
---
# <a name="unexpose"></a>非公開にします



使用して公開されたシャドウ コピーを unexposes、**公開**コマンド。 公開されているシャドウ コピーは、そのシャドウ ID、ドライブ文字、共有、またはマウント ポイントで指定できます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
unexpose {<ShadowID> | <Drive:> | <Share> | <MountPoint>}
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ShadowID>|指定したシャドウ ID で指定されたシャドウ コピーを unexposes します。|
|\<ドライブ: >|指定したドライブ文字 (たとえば、ドライブ P) に関連付けられているシャドウ コピーを unexposes します。|
|\<Share>|指定した共有に関連付けられたシャドウ コピーを unexposes (たとえば、 \\ \\ *MachineName*\)します。|
|\<MountPoint>|指定されたマウント ポイントに関連付けられたシャドウ コピーを unexposes (C:\shadowcopy など\)します。|

## <a name="remarks"></a>注釈

-   既存のエイリアスまたは環境変数の代わりに使用できます*ShadowID*します。 使用**追加**パラメーターに既存の別名を参照してください。

## <a name="BKMK_examples"></a>例

P のドライブに関連付けられているシャドウ コピーを非公開には、次のように入力します。
```
unexpose P:
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)