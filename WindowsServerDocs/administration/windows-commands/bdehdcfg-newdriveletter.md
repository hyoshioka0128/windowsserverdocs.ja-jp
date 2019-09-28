---
title: bdehdcfg newdriveletter
description: Bdehdcfg newdriveletter の Windows コマンドトピックでは、システムドライブとして使用されるドライブの部分に新しいドライブ文字を割り当てます。
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: e2abd4a686f358b5dd844514735edb3ffaa13845
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382231"
---
# <a name="bdehdcfg-newdriveletter"></a>bdehdcfg: newdriveletter



システムドライブとして使用されるドライブの部分に新しいドライブ文字を割り当てます。 このコマンドを使用する方法の例については、「[例](#BKMK_Examples)」を参照してください。

## <a name="syntax"></a>構文

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge} -newdriveletter <DriveLetter>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|@no__t 0DriveLetter ドライブ文字 >|指定されたターゲットドライブに割り当てられるドライブ文字を定義します。|

## <a name="remarks"></a>コメント

ベストプラクティスとして、システムドライブにドライブ文字を割り当てないことをお勧めします。

## <a name="BKMK_Examples"></a>例

次の例は、ドライブ文字 P が割り当てられている既定のドライブを示しています。
```
bdehdcfg -target default -newdriveletter P:
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Bdehdcfg](bdehdcfg.md)