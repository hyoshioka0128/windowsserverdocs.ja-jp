---
title: ktmutil
description: カーネルトランザクションマネージャーユーティリティを起動する ktmutil コマンドの参照記事です。
ms.topic: article
ms.assetid: 53bc56df-f0e5-443b-ab20-bbf8b11d4a9a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ff65e7e228f4876e51e3132d3a430ceec3837053
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87887664"
---
# <a name="ktmutil"></a>ktmutil

カーネルトランザクションマネージャーユーティリティを開始します。 パラメーターを指定せずに使用した場合、 **ktmutil**は使用可能なサブコマンドを表示します。

## <a name="syntax"></a>構文

```
ktmutil list tms
ktmutil list transactions [{TmGUID}]
ktmutil resolve complete {TmGUID} {RmGUID} {EnGUID}
ktmutil resolve commit {TxGUID}
ktmutil resolve rollback {TxGUID}
ktmutil force commit {GUID}
ktmutil force rollback {GUID}
ktmutil forget
```

## <a name="examples"></a>例


GUID 311a9209-03f4-11dc-918f-00188b8f707b を持つ Indoubt トランザクションを強制的にコミットするには、次のように入力します。

```
ktmutil force commit {311a9209-03f4-11dc-918f-00188b8f707b}
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)