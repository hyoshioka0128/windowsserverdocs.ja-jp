---
title: bdehdcfg newdriveletter
description: Bdehdcfg newdriveletter - の Windows コマンド」のトピックでは、システム ドライブとして使用されるドライブの領域に新しいドライブ文字が割り当てられます。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f1f200a0-6850-4f0d-9047-f9f982a590f8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cd40942dfb724d46c0fa9a43c4646e1db09d2a76
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887143"
---
# <a name="bdehdcfg-newdriveletter"></a>bdehdcfg: newdriveletter



システム ドライブとして使用されるドライブの領域に新しいドライブ文字を割り当てます。 このコマンドの使用方法の例は、次を参照してください。[例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge} -newdriveletter <DriveLetter>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ドライブ文字 >|指定されたターゲット ドライブに割り当てられるドライブ文字を定義します。|

## <a name="remarks"></a>注釈

ベスト プラクティスとしては、システム ドライブにドライブ文字を割り当てないことをお勧めします。

## <a name="BKMK_Examples"></a>例

次の例は、P. ドライブ文字が割り当てられている既定のドライブを示しています。
```
bdehdcfg -target default -newdriveletter P:
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンドライン構文キー](command-line-syntax-key.md)
-   [Bdehdcfg](bdehdcfg.md)