---
title: telnet の設定解除
description: Telnet 設定解除の Windows コマンドに関するトピック。これにより、以前に設定したオプションがオフになります。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: da9a0d99-1930-4858-93c7-0e9c3797ee09 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 34d52eedb2a5547ad0e3f2912dbe2a250eaf8fc5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80833145"
---
# <a name="telnet-unset"></a>telnet: 未設定

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

以前の set オプションをオフにします。   

## <a name="syntax"></a>構文  
```  
u[nset] {bsasdel | crlf | delasbs | escape | localecho | logging | ntlm} [?]  
```  
#### <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|bsasdel|送信 **Backspace** として、 **Backspace**します。|  
|crlf|送信、 **Enter** CR としてキー。 呼ばれるモードを改行します。|  
|delasbs|Delete**を** **delete**として送信します。|  
|エスケープ|エスケープ文字の設定を削除します。|  
|localecho|Localecho オフにします。|  
|ログ記録|ログをオフにします。|  
|ntlm|NTLM 認証をオフにします。|  
|?|このコマンドのヘルプを表示します。|  
## <a name="examples"></a><a name=BKMK_Examples></a>例  
ログをオフにします。  
```  
u logging  
```  
## <a name="additional-references"></a>その他の参照情報  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
