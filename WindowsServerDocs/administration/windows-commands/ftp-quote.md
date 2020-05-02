---
title: ftp 引用符
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4500a1d3-c091-42c7-a909-f61df7f2e993 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1101dd6a5fa163df8d43d182e9d0dfe66e340b60
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725141"
---
# <a name="ftp-quote"></a>ftp: 引用

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

は、逐語的引数をリモート ftp サーバーに送信します。 単一の ftp 応答コードが返されます。   
## <a name="syntax"></a>構文  
```  
quote <Argument>[ ]  
```  
#### <a name="parameters"></a>パラメーター  

| パラメーター  |                    [説明]                    |
|------------|---------------------------------------------------|
| <Argument> | Ftp サーバーに送信する引数を指定します。 |

## <a name="remarks"></a>Remarks  
**見積もり** コマンドと同じ、 **リテラル** コマンドです。  
## <a name="examples"></a>例  
リモート ftp サーバーに**quit**コマンドを送信します。  
```  
quote quit  
```  
## <a name="additional-references"></a>その他のリファレンス  
-   [ftp: literal_1](ftp-literal_1.md)  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
