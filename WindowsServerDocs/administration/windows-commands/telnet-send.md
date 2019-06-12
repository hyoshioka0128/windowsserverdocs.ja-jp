---
title: telnet の送信
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 36dc7f861e88cf991af57dda2f150107c6870f0f
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441043"
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
|    ao     |       Telnet コマンドの出力を中止を送信します。        |
|    ayt    |       Are You There telnet コマンドを送信します。       |
|    brk    |            Telnet コマンドの brk を送信します。            |
|    esc キー    |      現在の telnet のエスケープ文字を送信します。      |
|    ip     |     プロセスを中断 telnet コマンドを送信します。     |
|   同期   |           Telnet コマンドの synch を送信します。           |
| <string>  | Telnet サーバーを入力する任意の文字列を送信します。 |
|     ?     |     このコマンドに関連付けヘルプを表示します。      |

## <a name="BKMK_Examples"></a>例  
送信は、telnet サーバーに存在します。  
```  
sen ayt  
```  
## <a name="additional-references"></a>その他の参照  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
