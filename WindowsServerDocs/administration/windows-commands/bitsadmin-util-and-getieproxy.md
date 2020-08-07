---
title: bitsadmin util および getieproxy
description: 指定されたサービスアカウントのプロキシの使用状況を取得する bitsadmin util と getieproxy コマンドの参照記事。
ms.topic: article
ms.assetid: 6d50c7e3-f4eb-4ca5-9f0c-4ed396087db6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 78d24395a22d41369127b115971597598b69ec05
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87880926"
---
# <a name="bitsadmin-util-and-getieproxy"></a>bitsadmin util および getieproxy

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定されたサービスアカウントのプロキシの使用状況を取得します。 このコマンドは、サービスアカウントに指定したプロキシ使用量だけでなく、各プロキシの使用状況の値を表示します。 特定のサービスアカウントのプロキシ使用法の設定の詳細については、「 [bitsadmin util and setieproxy](bitsadmin-util-and-setieproxy.md)コマンド」を参照してください。

## <a name="syntax"></a>構文

```
bitsadmin /util /getieproxy <account> [/conn <connectionname>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ---------- |
| account | プロキシ設定を取得するサービスアカウントを指定します。 次の値を指定できます。<ul><li>LOCALSYSTEM</li><li>   NETWORKSERVICE</li><li>LOCALSERVICE.</li></ul> |
| connectionname | 省略可能。 **/Conn**パラメーターと共に使用して、使用するモデム接続を指定します。 **/Conn**パラメーターを指定しない場合、BITS は LAN 接続を使用します。 |

## <a name="examples"></a>例

ネットワークサービスアカウントのプロキシの使用状況を表示するには、次のようにします。

```
bitsadmin /util /getieproxy NETWORKSERVICE
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin util コマンド](bitsadmin-util.md)

- [bitsadmin コマンド](bitsadmin.md)
