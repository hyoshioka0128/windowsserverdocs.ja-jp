---
title: コンテキストの設定
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fc16c7dd-e8f0-4c2a-8742-0bddb2848bfd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 16f71d831f374f495abf2239cb8e694eee69efdf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370982"
---
# <a name="set-contex"></a>セットのコンテキスト



シャドウ コピーの作成のコンテキストを設定します。 パラメーターを指定せずに使用する場合 **セット コンテキスト** コマンド プロンプトでヘルプを表示します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
set context {clientaccessible | persistent [nowriters] | volatile [nowriters]}
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|clientaccessible|シャドウ コピーがクライアントのバージョンの Windows で使用できることを指定します。|
|一貫|シャドウ コピーがプログラムの終了、リセット、または再起動の間で永続化することを指定します。|
|揮発性|上のシャドウ コピーの削除は、終了またはリセットします。|
|nowriters|すべてのライターを除外することを指定します。|

## <a name="remarks"></a>コメント

-   *Clientaccessible* コンテキストは既定では永続的です。

## <a name="BKMK_examples"></a>例

シャドウ コピーが DiskShadow を終了するときに削除されないようにするには、次のように入力します。
```
set context persistent
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)