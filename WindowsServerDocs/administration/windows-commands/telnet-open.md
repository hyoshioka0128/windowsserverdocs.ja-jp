---
title: telnet を開く
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e30ad68c-2366-4754-ac36-311a2392902a vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 186664a75978f589a9a26047c72b9db74dd2dc4d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441118"
---
# <a name="telnet-open"></a>telnet: を開く

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Telnet サーバーに接続します。    
## <a name="syntax"></a>構文  
```  
o[pen] <hostname> [<Port>]  
```  
### <a name="parameters"></a>パラメーター  

| パラメーター  |                                        説明                                         |
|------------|--------------------------------------------------------------------------------------------|
| <hostname> |                         コンピューター名または IP アドレスを指定します。                         |
|  [<Port>]  | Telnet サーバーがリッスンする TCP ポートを指定します。 既定値は、TCP ポート 23 です。 |

## <a name="BKMK_Examples"></a>例  
Telnet.microsoft.com で telnet サーバーに接続します。  
```  
o telnet.microsoft.com  
```  
## <a name="additional-references"></a>その他の参照  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
