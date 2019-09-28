---
title: telnet 送信
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c217abc-1182-466e-914c-1ff16755021b vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 958e0e507e5a0ae836da98de8d677a116dbb38bd
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383633"
---
# <a name="telnet-send"></a>telnet: 送信

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Telnet サーバーに telnet コマンドを送信します。   
## <a name="syntax"></a>構文  
```  
sen[d] {ao | ayt | brk | esc | ip | synch | <string>} [?]  
```  
### <a name="parameters"></a>パラメーター  

| パラメーター |                     説明                      |
|-----------|------------------------------------------------------|
|    ao     |       Telnet コマンドの中止出力を送信します。        |
|    ayt    |       Telnet コマンドを送信します。       |
|    brk    |            Telnet コマンド brk を送信します。            |
|    esc キー    |      現在の telnet エスケープ文字を送信します。      |
|    ip     |     Telnet コマンドの割り込みプロセスを送信します。     |
|   同期   |           Telnet コマンド同期を送信します。           |
| <string>  | 入力した任意の文字列を telnet サーバーに送信します。 |
|     ?     |     このコマンドに関連するヘルプを表示します。      |

## <a name="BKMK_Examples"></a>例  
Telnet サーバーに送信されます。  
```  
sen ayt  
```  
## <a name="additional-references"></a>その他の参照情報  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
