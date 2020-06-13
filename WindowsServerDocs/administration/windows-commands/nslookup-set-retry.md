---
title: nslookup set retry
description: Nslookup set retry コマンドのリファレンストピックでは、指定されたサーバーから情報を取得する試行回数を設定します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 615fdfa2-fa29-47a8-8c9e-a6c5b45b3b71
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 268a9f0023c0e7e19e8ed413895f639444fe3b88
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721465"
---
# <a name="nslookup-set-retry"></a>nslookup set retry

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

一定の時間内に応答が受信されなかった場合、タイムアウト期間は2倍になり、要求は再送信されます。 このコマンドは、要求がサーバーに再送信されてから情報が得られるまでの回数を設定します。

> [!NOTE]
> 要求がタイムアウトになるまでの時間を変更するには、 [nslookup set timeout](nslookup-set-timeout.md)コマンドを使用します。

## <a name="syntax"></a>構文

```
set retry=<number>
```

### <a name="parameters"></a>パラメーター

| パラメーター | Description |
| ---------- | ---------- |
| `<number>` | 再試行回数の新しい値を指定します。 既定の再試行回数は**4**です。 |
| /? | コマンド プロンプトにヘルプを表示します。 |
| /help | コマンド プロンプトにヘルプを表示します。 |

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [nslookup set timeout](nslookup-set-timeout.md)
