---
title: nslookup set recurse
description: Nslookup set 再帰コマンドのリファレンス記事。指定されたサーバーで情報が見つからない場合に、他のサーバーを照会するようにドメインネームシステム (DNS) ネームサーバーに指示します。
ms.topic: article
ms.assetid: d1b7a93f-dfb0-4ccd-b230-e0953057fada
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 26a98e646f0915a684129d4b0205384f10c31d49
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87885575"
---
# <a name="nslookup-set-recurse"></a>nslookup set recurse

指定されたサーバー上の情報が見つからない場合に、他のサーバーを照会するようにドメインネームシステム (DNS) ネームサーバーに指示します。

## <a name="syntax"></a>構文

```
set [no]recurse
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ---------- |
| norecurse | 指定されたサーバーで情報が見つからない場合に、ドメインネームシステム (DNS) ネームサーバーで他のサーバーのクエリを実行しないようにします。 |
| recurse | 指定されたサーバー上の情報が見つからない場合に、他のサーバーを照会するようにドメインネームシステム (DNS) ネームサーバーに指示します。 これが既定値です。 |
| /? | コマンド プロンプトにヘルプを表示します。 |
| /help | コマンド プロンプトにヘルプを表示します。 |

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
