---
title: telnet を開く
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 4528b728c89bbdfc99de94c7fefebb18c8e1ad97
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383646"
---
# <a name="telnet-open"></a>telnet: 開く

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
|  [<Port>]  | Telnet サーバーがリッスンしている TCP ポートを指定します。 既定値は、TCP ポート 23 です。 |

## <a name="BKMK_Examples"></a>例  
Telnet.microsoft.com で telnet サーバーに接続します。  
```  
o telnet.microsoft.com  
```  
## <a name="additional-references"></a>その他の参照情報  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
