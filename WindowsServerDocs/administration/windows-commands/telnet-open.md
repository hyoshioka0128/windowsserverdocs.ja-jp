---
title: telnet を開く
description: Telnet サーバーに接続する telnet open のリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
s.topic: article
ms.assetid: e30ad68c-2366-4754-ac36-311a2392902a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0be8aca4cb061df55674a405eb1cf2a5e643cb4f
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222717"
---
# <a name="telnet-open"></a>telnet: 開く

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Telnet サーバーに接続します。

## <a name="syntax"></a>構文
```
o[pen] <hostname> [<Port>]
```
#### <a name="parameters"></a>パラメーター

| パラメーター  |                                        説明                                         |
|------------|--------------------------------------------------------------------------------------------|
| <hostname> |                         コンピューター名または IP アドレスを指定します。                         |
|  [<Port>]  | Telnet サーバーがリッスンしている TCP ポートを指定します。 既定値は、TCP ポート 23 です。 |

## <a name="examples"></a>例
Telnet.microsoft.com で telnet サーバーに接続します。
```
o telnet.microsoft.com
```
## <a name="additional-references"></a>その他のリファレンス
- [コマンド ライン構文の記号](command-line-syntax-key.md)
