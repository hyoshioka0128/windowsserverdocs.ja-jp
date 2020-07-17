---
title: ftp remotehelp
description: リモートコマンドのヘルプを表示する、ftp remotehelp コマンドのリファレンス記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ef23adf3-ead4-44c8-ac1d-c8a6f4b2bf73
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 54d784751291515a022a561ca9600e3e967a9d8e
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925740"
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

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [ftp quote](ftp-quote.md)

- [ftp literal](ftp-literal_1.md)

- [追加の FTP ガイダンス](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
