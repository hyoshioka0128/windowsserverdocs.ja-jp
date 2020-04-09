---
title: ftp remotehelp_1
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ef23adf3-ead4-44c8-ac1d-c8a6f4b2bf73 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3c4a4ffec01fce5cde8b2aa9dd1fa0704f3a85ff
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843055"
---
# <a name="ftp-remotehelp_1"></a>ftp: remotehelp_1

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートコマンドのヘルプを表示します。   
## <a name="syntax"></a>構文  
```  
remotehelp [<Command>]  
```  
#### <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|[<Command>]|ヘルプを表示するコマンドの名前を指定します。 *コマンド*が指定されていない場合、 **ftp**では、すべてのリモートコマンドの一覧が表示されます。|  
## <a name="remarks"></a>コメント  
**引用符**または**リテラル**を使用してリモートコマンドを実行できます。  
## <a name="examples"></a><a name=BKMK_Examples></a>例  
リモートコマンドの一覧を表示します。  
```  
remotehelp  
```  
この**コマンドの構文**を表示します。  
```  
remotehelp feat  
```  
## <a name="additional-references"></a>その他の参照情報  
-   [ftp: 引用](ftp-quote.md)  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
