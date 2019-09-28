---
title: 'ksetup: dumpstate'
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3ef2f7b8-97af-4f42-9542-cff324840637
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 625d05b2fea9ae58681648c64e309aa8b2a201ed
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375000"
---
# <a name="ksetupdumpstate"></a>ksetup: dumpstate



コンピューターに定義されているすべての領域の領域設定の現在の状態を表示します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /dumpstate
```

### <a name="parameters"></a>パラメーター

なし

## <a name="remarks"></a>コメント

このコマンドの出力には、既定の領域 (コンピューターがメンバーとなっているドメイン) と、このコンピューターで定義されているすべての領域が含まれます。 各領域には次のものが含まれます。
-   この領域に関連付けられているすべてのキー配布センター (Kdc)
-   この領域のすべての**設定領域**フラグ
-   KDC パスワード

このコマンドでは、DNS の検出またはコマンド**ksetup/domain**によって指定されたドメイン名は表示されません。

このコマンドでは、 **ksetup/setcomputerpassword**コマンドを使用して設定されたコンピューターパスワードは表示されません。

**Ksetup**は、 **Ksetup/dumpstate**と同じ出力を生成します。

## <a name="BKMK_Examples"></a>例

コンピューター上のほとんどの Kerberos 領域構成を検索します。
```
ksetup /dumpstate
```

#### <a name="additional-references"></a>その他の参照情報

-   [Ksetup](ksetup.md)
-   [コマンド ライン構文の記号](command-line-syntax-key.md)