---
title: ftp 引用符
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4500a1d3-c091-42c7-a909-f61df7f2e993 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1bf13704150d602fbfa4e3b1a3fb1774d3bf7363
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843035"
---
# <a name="ftp-quote"></a>ftp: 引用

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

は、逐語的引数をリモート ftp サーバーに送信します。 単一の ftp 応答コードが返されます。   
## <a name="syntax"></a>構文  
```  
quote <Argument>[ ]  
```  
#### <a name="parameters"></a>パラメーター  

| パラメーター  |                    説明                    |
|------------|---------------------------------------------------|
| <Argument> | Ftp サーバーに送信する引数を指定します。 |

## <a name="remarks"></a>コメント  
**見積もり** コマンドと同じ、 **リテラル** コマンドです。  
## <a name="examples"></a><a name=BKMK_Examples></a>例  
リモート ftp サーバーに**quit**コマンドを送信します。  
```  
quote quit  
```  
## <a name="additional-references"></a>その他の参照情報  
-   [ftp: literal_1](ftp-literal_1.md)  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
