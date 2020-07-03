---
title: nslookup server
description: Nslookup サーバーコマンドの参照記事。既定のサーバーを指定したドメインネームシステム (DNS) ドメインに変更します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 608267f8-f7b4-412a-8dcd-e08b5ffc2085
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ec66534d475502ee68f9fabb58b214d25e6e0aaf
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931267"
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
