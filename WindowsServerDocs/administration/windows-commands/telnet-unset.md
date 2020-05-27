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
ms.openlocfilehash: c121d6501f87ae1218381871bcbf536d9407ba31
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83821042"
---
# <a name="telnet-unset"></a>telnet: 未設定

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

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
|logging|ログ記録をオフにします。|
|ntlm|NTLM 認証をオフにします。|
|?|このコマンドのヘルプを表示します。|
## <a name="examples"></a>例
ログをオフにします。
```
u logging
```
## <a name="additional-references"></a>その他のリファレンス
- [コマンド ライン構文の記号](command-line-syntax-key.md)
