---
title: ftp の見積もり
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4500a1d3-c091-42c7-a909-f61df7f2e993 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0b1aaf9eadfd9c51048ad41106ce6532f6f9588b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865883"
---
# <a name="ftp-quote"></a>ftp: 見積もり

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート ftp サーバーには、逐語的引数を送信します。 1 つの ftp 応答コードが返されます。   
## <a name="syntax"></a>構文  
```  
quote <Argument>[ ]  
```  
### <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|<Argument>|Ftp サーバーに送信する引数を指定します。|  
## <a name="remarks"></a>注釈  
**見積もり** コマンドと同じ、 **リテラル** コマンドです。  
## <a name="BKMK_Examples"></a>例  
送信、**終了**リモート ftp サーバーにコマンド。  
```  
quote quit  
```  
## <a name="additional-references"></a>その他の参照  
-   [ftp: literal_1](ftp-literal_1.md)  
-   [コマンドライン構文キー](command-line-syntax-key.md)  
