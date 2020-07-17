---
title: nslookup set recurse
description: Nslookup set 再帰コマンドのリファレンス記事。指定されたサーバーで情報が見つからない場合に、他のサーバーを照会するようにドメインネームシステム (DNS) ネームサーバーに指示します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d1b7a93f-dfb0-4ccd-b230-e0953057fada
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dd65eaa9ba60e2a3cdf79e808b2efccb28b7d455
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935693"
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
