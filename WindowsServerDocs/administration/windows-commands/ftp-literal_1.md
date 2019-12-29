---
title: ftp literal_1
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fb81aa2d-07fa-4e79-bf44-1fb5526fdf14 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 393dea27e8567a72a5bd25c927282ade93e317c9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376271"
---
# <a name="ftp-literal_1"></a>ftp: literal_1

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012 は、逐語的引数をリモート ftp サーバーに送信します。 単一の ftp 応答コードが返されます。   

## <a name="syntax"></a>構文  
```  
literal <Argument> [ ]  
```  
### <a name="parameters"></a>パラメーター  

| パラメーター  |                    説明                    |
|------------|---------------------------------------------------|
| <Argument> | Ftp サーバーに送信する引数を指定します。 |

## <a name="remarks"></a>コメント  
**Literal**コマンドは、 **quote**コマンドと同じです。  
## <a name="BKMK_Examples"></a>例  
リモート ftp サーバーに**quit**コマンドを送信します。  
```  
literal quit  
```  
## <a name="additional-references"></a>その他の参照情報  
-   [ftp: 引用](ftp-quote.md)  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
