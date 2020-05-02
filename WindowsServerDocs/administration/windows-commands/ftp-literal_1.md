---
title: ftp literal_1
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fb81aa2d-07fa-4e79-bf44-1fb5526fdf14 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fc4f8aff5a22da93330a12a75e5f368285366216
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725257"
---
# <a name="ftp-literal_1"></a>ftp: literal_1

> 適用対象: windows server (半期チャネル)、Windows Server 2019、Windows Server 2016、windows Server 2012 R2、Windows Server 2012 は、逐語的引数をリモート ftp サーバーに送信します。 単一の ftp 応答コードが返されます。   

## <a name="syntax"></a>構文  
```  
literal <Argument> [ ]  
```  
#### <a name="parameters"></a>パラメーター  

| パラメーター  |                    [説明]                    |
|------------|---------------------------------------------------|
| <Argument> | Ftp サーバーに送信する引数を指定します。 |

## <a name="remarks"></a>Remarks  
**Literal**コマンドは、 **quote**コマンドと同じです。  
## <a name="examples"></a>例  
リモート ftp サーバーに**quit**コマンドを送信します。  
```  
literal quit  
```  
## <a name="additional-references"></a>その他のリファレンス  
-   [ftp: 引用](ftp-quote.md)  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
