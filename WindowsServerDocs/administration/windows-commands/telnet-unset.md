---
title: telnet の設定解除
description: 以前に設定したオプションをオフにする telnet 設定のリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: da9a0d99-1930-4858-93c7-0e9c3797ee09 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d88f5e479564cad8e2ec7e82dbb4f4cef35cd012
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721458"
---
# <a name="telnet-unset"></a>telnet: 未設定

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

以前の set オプションをオフにします。   

## <a name="syntax"></a>構文  
```  
u[nset] {bsasdel | crlf | delasbs | escape | localecho | logging | ntlm} [?]  
```  
#### <a name="parameters"></a>パラメーター  
|パラメーター|[説明]|  
|-------|--------|  
|bsasdel|送信 **Backspace** として、 **Backspace**します。|  
|crlf|送信、 **Enter** CR としてキー。 呼ばれるモードを改行します。|  
|delasbs|Delete**を** **delete**として送信します。|  
|エスケープ|エスケープ文字の設定を削除します。|  
|localecho|Localecho オフにします。|  
|logging|ログ記録をオフにします。|  
|ntlm|NTLM 認証をオフにします。|  
|?|このコマンドのヘルプを表示します。|  
## <a name="examples"></a>例  
ログをオフにします。  
```  
u logging  
```  
## <a name="additional-references"></a>その他のリファレンス  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
