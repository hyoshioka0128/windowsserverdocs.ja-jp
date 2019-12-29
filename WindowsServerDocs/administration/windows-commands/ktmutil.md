---
title: ktmutil
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 53bc56df-f0e5-443b-ab20-bbf8b11d4a9a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d1a8fbc6360eca628d380a9c24612d952120162d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374778"
---
# <a name="ktmutil"></a>ktmutil



カーネルトランザクションマネージャーユーティリティを開始します。 パラメーターを指定せずに使用した場合、 **ktmutil**は使用可能なサブコマンドを表示します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
ktmutil list tms 
ktmutil list transactions [{TmGuid}]
ktmutil resolve complete {TmGuid} {RmGuid} {EnGuid}
ktmutil resolve commit {TxGuid}
ktmutil resolve rollback {TxGuid}
ktmutil force commit {??Guid}
ktmutil force rollback {??Guid}
ktmutil forget
```

## <a name="parameters"></a>パラメーター

## <a name="remarks"></a>コメント

## <a name="BKMK_examples"></a>例

GUID 311a9209-03f4-11dc-918f-00188b8f707b を持つ Indoubt トランザクションを強制的にコミットするには、次のように入力します。
```
ktmutil force commit {311a9209-03f4-11dc-918f-00188b8f707b}
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)