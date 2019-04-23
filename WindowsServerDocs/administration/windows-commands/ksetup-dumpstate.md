---
title: ksetup:dumpstate
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 8e5e8f20188fc27cc08dfd37c5fdbd811925f476
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863123"
---
# <a name="ksetupdumpstate"></a>ksetup:dumpstate



コンピューターで定義されているすべての領域の領域の設定の現在の状態を表示します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /dumpstate
```

### <a name="parameters"></a>パラメーター

なし

## <a name="remarks"></a>注釈

このコマンドの出力には、既定の領域 (コンピューターのメンバーであるドメイン) が含まれています。 このコンピューターで定義されているすべての領域とします。 以下は、各領域に含まれています。
-   すべてのキー配布センター (Kdc) この領域に関連付けられています。
-   すべての**セット レルム**この領域のフラグ
-   KDC パスワード

このコマンドで DNS 検出によって、またはコマンドで指定されたドメイン名が表示されない**ksetup/domain**します。

このコマンドでは、コマンドを使用して設定されているコンピューターのパスワードは表示されません**ksetup/setcomputerpassword**します。

**Ksetup**と同じ出力を生成**ksetup/dumpstate**します。

## <a name="BKMK_Examples"></a>例

コンピューターの Kerberos 領域の構成のほとんどを検索します。
```
ksetup /dumpstate
```

#### <a name="additional-references"></a>その他の参照情報

-   [Ksetup](ksetup.md)
-   [コマンドライン構文キー](command-line-syntax-key.md)