---
title: nslookup server
description: Nslookup server コマンドのリファレンストピックでは、既定のサーバーを指定したドメインネームシステム (DNS) ドメインに変更します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 608267f8-f7b4-412a-8dcd-e08b5ffc2085
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1a153bb39e3c7c4114334e7fa16b0f287b8b7fe8
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721624"
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

| パラメーター | Description |
| --------- | ----------- |
| `<DNSdomain>` | 既定のサーバーの DNS ドメインを指定します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |
| /help | コマンド プロンプトにヘルプを表示します。 |

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [nslookup lserver](nslookup-lserver.md)
