---
title: コンテキストの設定
description: シャドウコピーの作成のコンテキストを設定する、Set context の参照記事。
ms.topic: article
ms.assetid: fc16c7dd-e8f0-4c2a-8742-0bddb2848bfd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3506a79ec713f26b16f58cd8cda3903ce6503adf
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87882704"
---
# <a name="set-contex"></a>セットのコンテキスト

シャドウ コピーの作成のコンテキストを設定します。 パラメーターを指定せずに使用する場合 **セット コンテキスト** コマンド プロンプトでヘルプを表示します。



## <a name="syntax"></a>構文

```
set context {clientaccessible | persistent [nowriters] | volatile [nowriters]}
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|clientaccessible|シャドウ コピーがクライアントのバージョンの Windows で使用できることを指定します。|
|一貫|シャドウ コピーがプログラムの終了、リセット、または再起動の間で永続化することを指定します。|
|volatile|上のシャドウ コピーの削除は、終了またはリセットします。|
|nowriters|すべてのライターを除外することを指定します。|

## <a name="remarks"></a>Remarks

-   *Clientaccessible* コンテキストは既定では永続的です。

## <a name="examples"></a>例

シャドウ コピーが DiskShadow を終了するときに削除されないようにするには、次のように入力します。
```
set context persistent
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)