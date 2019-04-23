---
title: telnet の設定を解除
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da9a0d99-1930-4858-93c7-0e9c3797ee09 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 37c4d84d1664fdc13ea7ffec60bf981b264dba00
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853893"
---
# <a name="telnet-unset"></a>telnet: 未設定

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

以前の set オプションをオフにします。   
## <a name="syntax"></a>構文  
```  
u[nset] {bsasdel | crlf | delasbs | escape | localecho | logging | ntlm} [?]  
```  
### <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|bsasdel|送信 **Backspace** として、 **Backspace**します。|  
|crlf|送信、 **Enter** CR としてキー。 呼ばれるモードを改行します。|  
|delasbs|送信**削除**として**削除**します。|  
|エスケープ|エスケープ文字の設定を削除します。|  
|localecho|Localecho オフにします。|  
|logging|ログをオフにします。|  
|ntlm|NTLM 認証をオフにします。|  
|?|このコマンドのヘルプを表示します。|  
## <a name="BKMK_Examples"></a>例  
ログをオフにします。  
```  
u logging  
```  
## <a name="additional-references"></a>その他の参照  
-   [コマンドライン構文キー](command-line-syntax-key.md)  
