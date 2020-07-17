---
title: nslookup set root
description: Nslookup set root コマンドのリファレンス記事。クエリに使用されるルートサーバーの名前を変更します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8ad5393c-d4fd-4594-8187-576b1dcde60a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 866cc0f9c7c7e4ea99416c1be1fd8de3d374ca64
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935671"
---
# <a name="nslookup-set-root"></a>nslookup set root

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

クエリに使用するルートサーバーの名前を変更します。

> [!NOTE]
> このコマンドでは、 [nslookup root](nslookup-root.md)コマンドがサポートされています。

## <a name="syntax"></a>構文

```
set root=<rootserver>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ---------- |
| `<rootserver>` | ルートサーバーの新しい名前を指定します。 既定値は**ns.nic.ddn.mil**です。 |
| /? | コマンド プロンプトにヘルプを表示します。 |
| /help | コマンド プロンプトにヘルプを表示します。 |

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [nslookup root](nslookup-root.md)
