---
title: ftp remotehelp_1
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ef23adf3-ead4-44c8-ac1d-c8a6f4b2bf73 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bac6fbe4a55c3fed4caab4e30ba848ec9ea68e21
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376027"
---
# <a name="ftp-remotehelp_1"></a>ftp: remotehelp_1

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートコマンドのヘルプを表示します。   
## <a name="syntax"></a>構文  
```  
remotehelp [<Command>]  
```  
### <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|[<Command>]|ヘルプを表示するコマンドの名前を指定します。 *コマンド*が指定されていない場合、 **ftp**では、すべてのリモートコマンドの一覧が表示されます。|  
## <a name="remarks"></a>コメント  
**引用符**または**リテラル**を使用してリモートコマンドを実行できます。  
## <a name="BKMK_Examples"></a>例  
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
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
