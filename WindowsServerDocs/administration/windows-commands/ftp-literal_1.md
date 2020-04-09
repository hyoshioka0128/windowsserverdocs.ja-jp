---
title: ftp literal_1
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fb81aa2d-07fa-4e79-bf44-1fb5526fdf14 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f502bb56c94734870962f56cfb85dcc17ddc3f93
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843395"
---
# <a name="ftp-literal_1"></a>ftp: literal_1

>適用対象: windows Server (半期チャネル)、Windows server 2016、Windows Server 2012 R2、Windows Server 2012 は、逐語的引数をリモート ftp サーバーに送信します。 単一の ftp 応答コードが返されます。   

## <a name="syntax"></a>構文  
```  
literal <Argument> [ ]  
```  
#### <a name="parameters"></a>パラメーター  

| パラメーター  |                    説明                    |
|------------|---------------------------------------------------|
| <Argument> | Ftp サーバーに送信する引数を指定します。 |

## <a name="remarks"></a>コメント  
**Literal**コマンドは、 **quote**コマンドと同じです。  
## <a name="examples"></a><a name=BKMK_Examples></a>例  
リモート ftp サーバーに**quit**コマンドを送信します。  
```  
literal quit  
```  
## <a name="additional-references"></a>その他の参照情報  
-   [ftp: 引用](ftp-quote.md)  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
