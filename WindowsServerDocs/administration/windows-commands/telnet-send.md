---
title: telnet send
description: Telnet サーバーに telnet コマンドを送信する telnet 送信の参照記事。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7c217abc-1182-466e-914c-1ff16755021b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 44a0415a3516fcb15cd292c9e4c9c0a4a18e5ad9
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85937368"
---
# <a name="telnet-send"></a>telnet: 送信

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Telnet サーバーに telnet コマンドを送信します。

## <a name="syntax"></a>構文
```
sen[d] {ao | ayt | brk | esc | ip | synch | <string>} [?]
```
#### <a name="parameters"></a>パラメーター

| パラメーター |                     説明                      |
|-----------|------------------------------------------------------|
|    ao     |       Telnet コマンドの中止出力を送信します。        |
|    ayt    |       Telnet コマンドを送信します。       |
|    brk    |            Telnet コマンド brk を送信します。            |
|    esc    |      現在の telnet エスケープ文字を送信します。      |
|    ip     |     Telnet コマンドの割り込みプロセスを送信します。     |
|   同期   |           Telnet コマンド同期を送信します。           |
| <string>  | 入力した任意の文字列を telnet サーバーに送信します。 |
|     ?     |     このコマンドに関連するヘルプを表示します。      |

## <a name="examples"></a>例
Telnet サーバーに送信されます。
```
sen ayt
```
## <a name="additional-references"></a>その他の参照情報
- [コマンド ライン構文の記号](command-line-syntax-key.md)
