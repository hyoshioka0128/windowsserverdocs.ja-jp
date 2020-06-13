---
title: nslookup set recurse
description: Nslookup set 再帰コマンドのリファレンストピックでは、指定されたサーバー上の情報が見つからない場合に、他のサーバーを照会するようにドメインネームシステム (DNS) ネームサーバーに指示します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d1b7a93f-dfb0-4ccd-b230-e0953057fada
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 082ba3bd926d1f47be5510c2340804b1b92991f1
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721618"
---
# <a name="nslookup-set-recurse"></a>nslookup set recurse

指定されたサーバー上の情報が見つからない場合に、他のサーバーを照会するようにドメインネームシステム (DNS) ネームサーバーに指示します。

## <a name="syntax"></a>構文

```
set [no]recurse
```

### <a name="parameters"></a>パラメーター

| パラメーター | Description |
| ---------- | ---------- |
| norecurse | 指定されたサーバーで情報が見つからない場合に、ドメインネームシステム (DNS) ネームサーバーで他のサーバーのクエリを実行しないようにします。 |
| recurse | 指定されたサーバー上の情報が見つからない場合に、他のサーバーを照会するようにドメインネームシステム (DNS) ネームサーバーに指示します。 これが既定値です。 |
| /? | コマンド プロンプトにヘルプを表示します。 |
| /help | コマンド プロンプトにヘルプを表示します。 |

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
