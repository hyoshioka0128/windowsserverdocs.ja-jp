---
title: telnet を開く
description: Telnet サーバーに接続する telnet を開くための Windows コマンドに関するトピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
s.topic: article
ms.assetid: e30ad68c-2366-4754-ac36-311a2392902a vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b100d2b53a340a083f22d4fd88c42363642d5da5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80833335"
---
# <a name="telnet-open"></a>telnet: 開く

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

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

## <a name="examples"></a><a name=BKMK_Examples></a>例  
Telnet.microsoft.com で telnet サーバーに接続します。  
```  
o telnet.microsoft.com  
```  
## <a name="additional-references"></a>その他の参照情報  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
