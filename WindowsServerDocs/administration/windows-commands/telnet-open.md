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
ms.openlocfilehash: a87c4bac000a63af806705e9371a79d7370a34c1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838243"
---
# <a name="telnet-open"></a>telnet: を開く

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Telnet サーバーに接続します。    
## <a name="syntax"></a>構文  
```  
o[pen] <hostname> [<Port>]  
```  
### <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|<hostname>|コンピューター名または IP アドレスを指定します。|  
|[<Port>]|Telnet サーバーがリッスンする TCP ポートを指定します。 既定値は、TCP ポート 23 です。|  
## <a name="BKMK_Examples"></a>例  
Telnet.microsoft.com で telnet サーバーに接続します。  
```  
o telnet.microsoft.com  
```  
## <a name="additional-references"></a>その他の参照  
-   [コマンドライン構文キー](command-line-syntax-key.md)  
