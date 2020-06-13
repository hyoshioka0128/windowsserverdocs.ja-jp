---
title: nslookup set root
description: Nslookup set root コマンドのリファレンストピックでは、クエリに使用されるルートサーバーの名前を変更します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8ad5393c-d4fd-4594-8187-576b1dcde60a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1271dbeb0381d01e70380bded82a94ba20163853
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721455"
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

| パラメーター | Description |
| ---------- | ---------- |
| `<rootserver>` | ルートサーバーの新しい名前を指定します。 既定値は**ns.nic.ddn.mil**です。 |
| /? | コマンド プロンプトにヘルプを表示します。 |
| /help | コマンド プロンプトにヘルプを表示します。 |

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [nslookup root](nslookup-root.md)
