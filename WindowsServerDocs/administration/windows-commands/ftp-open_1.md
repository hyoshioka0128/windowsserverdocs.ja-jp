---
title: ftp open_1
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4b61926a-dc60-4b4c-96d3-64e5c91c18ba vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 45de8b3c210fe0925ac3cc43c41d3e092d5dfe16
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438505"
---
# <a name="ftp-open1"></a>ftp: open_1

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定された ftp サーバーに接続します。   
## <a name="syntax"></a>構文  
```  
open <computer> [<Port>]  
```  
### <a name="parameters"></a>パラメーター  

| パラメーター  |                                           説明                                            |
|------------|--------------------------------------------------------------------------------------------------|
| <computer> |                接続を試みているリモート コンピューターを指定します。                 |
|  [<Port>]  | Ftp サーバーへの接続に使用する TCP ポート番号を指定します。 既定では、TCP ポート 21 を使用します。 |

## <a name="remarks"></a>注釈  
(この場合、DNS サーバーまたはホスト ファイルがあります)、IP アドレスまたはコンピューター名を使用して、**コンピューター**します。  
## <a name="BKMK_Examples"></a>例  
Ftp サーバーに接続**専用**します。  
```  
Open ftp.microsoft.com  
```  
Ftp サーバーに接続**専用**755 の TCP ポートでリッスンします。  
```  
open ftp.microsoft.com 755  
```  
## <a name="additional-references"></a>その他の参照  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
