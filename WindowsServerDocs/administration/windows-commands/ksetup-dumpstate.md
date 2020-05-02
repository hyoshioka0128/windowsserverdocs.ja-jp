---
title: 'ksetup: dumpstate'
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3ef2f7b8-97af-4f42-9542-cff324840637
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 27a7e3154b9dfa663b88b04857ea7650995613c6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724640"
---
# <a name="ksetupdumpstate"></a>ksetup: dumpstate



コンピューターに定義されているすべての領域の領域設定の現在の状態を表示します。

## <a name="syntax"></a>構文

```
ksetup /dumpstate
```

#### <a name="parameters"></a>パラメーター

なし

## <a name="remarks"></a>Remarks

このコマンドの出力には、既定の領域 (コンピューターがメンバーとなっているドメイン) と、このコンピューターで定義されているすべての領域が含まれます。 各領域には次のものが含まれます。
-   この領域に関連付けられているすべてのキー配布センター (Kdc)
-   この領域のすべての**設定領域**フラグ
-   KDC パスワード

このコマンドでは、DNS の検出またはコマンド**ksetup/domain**によって指定されたドメイン名は表示されません。

このコマンドでは、 **ksetup/setcomputerpassword**コマンドを使用して設定されたコンピューターパスワードは表示されません。

**Ksetup**は、 **Ksetup/dumpstate**と同じ出力を生成します。

## <a name="examples"></a>例

コンピューター上のほとんどの Kerberos 領域構成を検索します。
```
ksetup /dumpstate
```

## <a name="additional-references"></a>その他のリファレンス

-   [Ksetup](ksetup.md)
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)