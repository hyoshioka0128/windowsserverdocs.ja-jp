---
title: nslookup server
description: Nslookup サーバーコマンドの参照記事。既定のサーバーを指定したドメインネームシステム (DNS) ドメインに変更します。
ms.topic: article
ms.assetid: 608267f8-f7b4-412a-8dcd-e08b5ffc2085
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: eacb1807810627956fcf75455e861d3ac381cf13
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87885784"
---
# <a name="nslookup-server"></a>nslookup server

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定したドメインネームシステム (DNS) ドメインに既定のサーバーを変更します。

このコマンドは、現在の既定のサーバーを使用して、指定された DSN ドメインに関する情報を検索します。 最初のサーバーを使用して情報を参照する場合は、 [nslookup lserver](nslookup-lserver.md)コマンドを使用します。

## <a name="syntax"></a>構文

```
server <DNSdomain>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<DNSdomain>` | 既定のサーバーの DNS ドメインを指定します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |
| /help | コマンド プロンプトにヘルプを表示します。 |

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [nslookup lserver](nslookup-lserver.md)
