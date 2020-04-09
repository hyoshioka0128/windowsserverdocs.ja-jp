---
title: 'ksetup: dumpstate'
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3ef2f7b8-97af-4f42-9542-cff324840637
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 46f827d26d867392db4cbef92cf5be496aee8d74
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841515"
---
# <a name="ksetupdumpstate"></a>ksetup: dumpstate



コンピューターに定義されているすべての領域の領域設定の現在の状態を表示します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /dumpstate
```

#### <a name="parameters"></a>パラメーター

なし

## <a name="remarks"></a>コメント

このコマンドの出力には、既定の領域 (コンピューターがメンバーとなっているドメイン) と、このコンピューターで定義されているすべての領域が含まれます。 各領域には次のものが含まれます。
-   この領域に関連付けられているすべてのキー配布センター (Kdc)
-   この領域のすべての**設定領域**フラグ
-   KDC パスワード

このコマンドでは、DNS の検出またはコマンド**ksetup/domain**によって指定されたドメイン名は表示されません。

このコマンドでは、 **ksetup/setcomputerpassword**コマンドを使用して設定されたコンピューターパスワードは表示されません。

**Ksetup**は、 **Ksetup/dumpstate**と同じ出力を生成します。

## <a name="examples"></a><a name=BKMK_Examples></a>例

コンピューター上のほとんどの Kerberos 領域構成を検索します。
```
ksetup /dumpstate
```

## <a name="additional-references"></a>その他の参照情報

-   [Ksetup](ksetup.md)
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)