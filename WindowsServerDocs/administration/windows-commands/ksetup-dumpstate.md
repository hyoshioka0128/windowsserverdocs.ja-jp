---
title: ksetup dumpstate
description: コンピューターで定義されているすべての領域の領域設定の現在の状態を表示する、ksetup dumpstate commnand の参照記事。
ms.topic: article
ms.assetid: 3ef2f7b8-97af-4f42-9542-cff324840637
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b9c59ad53a7e9d1fb149a0a0a87f5f00938d6a33
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87887956"
---
# <a name="ksetup-dumpstate"></a>ksetup dumpstate

コンピューターに定義されているすべての領域の領域設定の現在の状態を表示します。 このコマンドは、 **ksetup**コマンドと同じ出力を表示します。

## <a name="syntax"></a>構文

```
ksetup /dumpstate
```

### <a name="remarks"></a>Remarks

- このコマンドの出力には、既定の領域 (コンピューターがメンバーとなっているドメイン) と、このコンピューターで定義されているすべての領域が含まれます。 各領域には次のものが含まれます。

  - この領域に関連付けられているすべてのキー配布センター (Kdc)。

  - この領域のすべての**設定領域**フラグ。

  - KDC パスワード。

- このコマンドでは、DNS の検出またはコマンドによって指定されたドメイン名は表示されません `ksetup /domain` 。

- このコマンドでは、コマンドを使用してコンピューターのパスワードを設定することはできません `ksetup /setcomputerpassword` 。

## <a name="examples"></a>例

コンピューターで Kerberos 領域構成を見つけるには、次のように入力します。

```
ksetup /dumpstate
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [ksetup コマンド](ksetup.md)