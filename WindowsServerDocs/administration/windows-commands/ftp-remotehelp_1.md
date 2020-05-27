---
title: ftp remotehelp
description: リモートコマンドのヘルプを表示する、ftp remotehelp コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ef23adf3-ead4-44c8-ac1d-c8a6f4b2bf73
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 659de5487890b50aab9004f650e4584085e7306c
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820322"
---
# <a name="ftp-remotehelp"></a>ftp remotehelp

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートコマンドのヘルプを表示します。

## <a name="syntax"></a>構文

```
remotehelp [<command>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ------- | -------- |
| `[<command>]` | ヘルプを表示するコマンドの名前を指定します。 が `<command>` 指定されていない場合、このコマンドはすべてのリモートコマンドの一覧を表示します。 また、 [ftp 引用符](ftp-quote.md)または[ftp リテラル](ftp-literal_1.md)を使用してリモートコマンドを実行することもできます。 |

### <a name="examples"></a>例

リモートコマンドの一覧を表示するには、次のように入力します。

```
remotehelp
```

この*コマンドの構文*を表示するには、次のように入力します。

```
remotehelp feat
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [ftp 引用符](ftp-quote.md)

- [ftp リテラル](ftp-literal_1.md)

- [追加の FTP ガイダンス](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
