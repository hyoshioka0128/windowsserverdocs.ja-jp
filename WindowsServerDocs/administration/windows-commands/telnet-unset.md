---
title: telnet の設定解除
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: e6f0eb98c4168d2f664780dad42ca1aea5463d24
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383483"
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
|delasbs|Delete**を** **delete**として送信します。|  
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
## <a name="additional-references"></a>その他の参照情報  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
